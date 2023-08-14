# SQL-DiabetesDB

An SQL Analysis of Female Diabetic patients based on certain diagnotic instance measurements.
Several constraints were placed on the selection of these instances from a larger database. 
In particular, all patients here are females at least 21 years old of Pima Indian heritage. 
This dataset is originally from the National Institute of Diabetes and Digestive and Kidney
Diseases.

The objective this project is to determine the trend and relations between instances with diabetes.

Table1 has 10 columns and 100 rows(filename : Table1)
BMITBL has 2 columns and 4 rows(filename : BMITBL)
(Please check TablesCreation file to get the code for table creation)

The questions that are framed are follows:

1. Use Case-When statement to provide BMI_RANGE to each BMI value in Table1.(filename : CASEWHEN)
2. Use Aggregate function to find the Average age of women.(filename : AVGW)
3. Find the number patients in each BMI_RANGE.(filename : BMIRC)
4. Find the details of patients with age 20-40 with BMI as 'Normal'.(filename : Q1)
5. Print REG, BMI, Age and Result(diabetic or Non-Diabetic) of patients with BMI > 24.9(Above 'Normal').(filename : Q2)
6. Count the number of Diabetic and Non - Diabetic patients. (filename : Q3)
7. Count and print the number of patients with no diabetes with respect to BMI_RANGES.(filename : Q4)
8. Show the BMI_RANGE with respect to diabetic and non-diabetic patients column wise.(filename : Q5)
9. Create a Table for Blood Pressure with below details, and count diabetic and non-diabetic patients
   with BMI not in Normal Range with Blood Pressure ranges defined below.(filename: Q6)
    1. Normal : below 80
    2. Hypertension1 : between 80(inclusive) and 89
    3. Hypertension2 : between 89(inclusive) and 120
    4. Hypertensive Crisis : above 120(inclusive)
10. Show the Blood Pressure and count od diabetic and non-diabetic patients with BMI as 'Normal'.(filename : Q7)
11. Show the number of diabetic and non-diabetic patients with BMI > 24.9 and Blood Pressure above 80.(filename : Q8)




