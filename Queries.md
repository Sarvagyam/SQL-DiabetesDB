#### 1. Use Case-When statement to provide BMI_RANGE to each BMI value in Table1.(filename : CASEWHEN)

````sql
SELECT BMI,
CASE 
	WHEN BMI <=18.5 THEN ‘Underweight’
	WHEN BMI >18.5 AND BMI <=24.9 THEN ‘Normal’
	WHEN BMI>24.9 AND BMI <=29.9 THEN ‘Overweight’
	ELSE ‘Obese’
END AS BMI_RANGE
FROM Table1;
````


#### 2. Use Aggregate function to find the Average age of women.(filename : AVGW)

````sql
SELECT AVG(Age) FROM Table1;
````


#### 3. Find the number patients in each BMI_RANGE.(filename : BMIRC)

````sql
SELECT DISTINCT(BMI_RANGE), COUNT(*) FROM BMITBL
GROUP BY BMI_RANGE;
````


#### 4. Find the details of patients with age 20-40 with BMI as 'Normal'.(filename : Q1)

````sql
SELECT * FROM BMITBL JOIN Table1 ON (REG_B = REG)
WHERE (Table1.Age BETWEEN 20 AND 40)
AND BMI = ‘Normal’;
````


#### 5. Print REG, BMI, Age and Result(diabetic or Non-Diabetic) of patients with BMI > 24.9(Above 'Normal').(filename : Q2)

````sql
SELECT REG, Table1.BMI, Age,
CASE 
WHEN Outcome = 0 THEN ‘Non-Diabetic’
ELSE ‘Diabetic’
	END AS RESULT
	FROM BMITBL JOIN Table1 ON (REG_B=REG)
	WHERE BMITBL.BMI > 24.9;
````


#### 6. Count the number of Diabetic and Non - Diabetic patients. (filename : Q3)

````sql
SELECT 
CASE 
	WHEN Outcome = 0 THEN ‘Non-Diabetic’
	ELSE ‘Diabetic’
END AS Result, COUNT(Outcome)
FROM BMITBL JOIN Table1 ON (REG_B = REG)
GROUP BY Result ;
````


#### 7. Count and print the number of patients with no diabetes with respect to BMI_RANGES.(filename : Q4)

````sql
SELECT BMI_RANGE, COUNT(*) FROM Table1 JOIN BMITBL 
ON (REG = REG_B)
WHERE Outcome = 0
GROUP BY BMI_RANGE;
````


#### 8.	Show the BMI_RANGE with respect to diabetic and non-diabetic patients column wise.(filename : Q5)

````sql
SELECT BMI_RANGE,
SUM(CASE
	WHEN Outcome =1 THEN 1 ELSE 0 END) Diabetic,
SUM(CASE 
	WHEN Outcome=0 THEN 1 ELSE 0 END) NonDiabetic
FROM Table1 JOIN BMITBL ON (REG=REG_B)
GROUP BY BMI_RANGE;
````


#### 9. Create a Table for Blood Pressure with below details, and count diabetic and non-diabetic patients
  #### with BMI not in Normal Range with Blood Pressure ranges defined below.(filename: Q6)
 ####   1. Normal : below 80
 ####   2. Hypertension1 : between 80(inclusive) and 89
 ####   3. Hypertension2 : between 89(inclusive) and 120
 ####   4. Hypertensive Crisis : above 120(inclusive)
 
### TABLE CREATION QUERY:

````sql
CREATE TABLE BPTBL(`REG_P` int, `BP` int, `BP_RANGE` CHAR(20))
INSERT INTO BPTBL(`REG_P`,’BP’,’BP_RANGE’)
SELECT REG, BloodPressure,
CASE 
	WHEN BloodPressure < 80 THEN ‘Normal’
	WHEN BloodPressure >= 80 AND BloodPressure < 89 THEN ‘Hypertension S1’
	WHEN BloodPressure >= 89 AND BloodPressure < 120 THEN ‘Hypertension S2’
	ELSE ‘Hypertensive Crisis’
END
FROM Table1;
````

#### QUERY:

````sql
SELECT BP_RANGE,
SUM(CASE
	WHEN Outcome =0 THEN 1 ELSE 0 END) NonDiabetic,
SUM(CASE 
	WHEN Outcome =1 THEN 1 ELSE 0 END) Diabetic
FROM BMPTBL JOIN Table1 ON (REG_P = REG)
WHERE BMI > 24.9 OR BMI < 18.9
GROUP BY BP_RANGE;
````


#### 9. Show the Blood Pressure and count od diabetic and non-diabetic patients with BMI as 'Normal'.(filename : Q7)

````sql
SELECT BP_RANGE,
SUM(CASE 
	WHEN Outcome =0 THEN 1 ELSE 0 END) NonDiabetic,
SUM(CASE
	WHEN Outcome =1 THEN 1 ELSE 0 END) Diabetic
FROM BPTBL JOIN Table1 ON (REG_P = REG)
	          JOIN BMITBL ON (REG_B = REG_P)
WHERE BMI_RANGE = ‘Normal’
GROUP BY BP_RANGE;
11. Show the number of diabetic and non-diabetic patients with BMI > 24.9 and Blood Pressure above 80.(filename : Q8)
SELECT 
SUM(CASE
	WHEN Outcome = 0 THEN 1 ELSE 0 END) NonDiabetic,
SUM(CASE
	WHEN Outcome = 1 THEN 1 ELSE 0 END) Diabetic
FROM BPTBL JOIN Table1 ON (REG_P = REG)
	          JOIN BMITBL ON (REG_P = REG_B)
WHERE BP > 80 AND BMITBL.BMI_RANGE IN (‘Obese’,’Overweight’);
````
