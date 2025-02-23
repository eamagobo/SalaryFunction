#importing the pandas
import pandas as pd
#load and lead the csv file to jupyter notebook
data = pd.read_csv("Total.csv")
#calling for data to display the first and last few columns and rows
data
Python function with input of name and return details of the employees
If you want to display employee details on a separate line use the \n function before the input
Python dictionary to procees the salary, follow the steps below;
import pandas as pd
Load the salary data file
file_path = "Total.csv"
df = pd.read_csv(file_path)

# Convert "Not Provided" to NaN
df.replace("Not Provided", pd.NA, inplace=True)

# Convert salary-related columns to numeric values
salary_columns = ["BasePay", "OvertimePay", "OtherPay", "TotalPay", "TotalPayBenefits"]
df[salary_columns] = df[salary_columns].apply(pd.to_numeric, errors="coerce")

# Create a salary dictionary
salary_dict = {}
for _, row in df.iterrows():
    name = row["EmployeeName"]
    record = {
        "JobTitle": row["JobTitle"],
        "BasePay": row["BasePay"],
        "OvertimePay": row["OvertimePay"],
        "OtherPay": row["OtherPay"],
        "TotalPay": row["TotalPay"],
        "TotalPayBenefits": row["TotalPayBenefits"],
        "Year": row["Year"],
    }
    
    if name in salary_dict:
        salary_dict[name].append(record)
    else:
        salary_dict[name] = [record]

# Display a sample entry
print(list(salary_dict.items())[:3])
Handling error follow the steps below;
try:
# Load the salary data file
    file_path = "Total.csv"
    df = pd.read_csv(file_path)
    
# Convert "Not Provided" to NaN
    df.replace("Not Provided", pd.NA, inplace=True)
    
# Convert salary-related columns to numeric values
    salary_columns = ["BasePay", "OvertimePay", "OtherPay", "TotalPay", "TotalPayBenefits"]
    df[salary_columns] = df[salary_columns].apply(pd.to_numeric, errors="coerce")
    
# Create a salary dictionary
    salary_dict = {}
    for _, row in df.iterrows():
        try:
            name = row["EmployeeName"]
            record = {
                "JobTitle": row["JobTitle"],
                "BasePay": row["BasePay"],
                "OvertimePay": row["OvertimePay"],
                "OtherPay": row["OtherPay"],
                "TotalPay": row["TotalPay"],
                "TotalPayBenefits": row["TotalPayBenefits"],
                "Year": row["Year"],
            }
            
            if name in salary_dict:
                salary_dict[name].append(record)
            else:
                salary_dict[name] = [record]
        except KeyError as e:
            print(f"Missing expected column in row: {e}")
        except Exception as e:
            print(f"Unexpected error processing row: {e}")
Error Handling  
# Display a sample entry
    print(list(salary_dict.items())[:3])
except FileNotFoundError:
    print("Error: The file 'Total.csv' was not found.")
except pd.errors.EmptyDataError:
    print("Error: The file is empty.")
except pd.errors.ParserError:
    print("Error: There was an issue parsing the file.")
except Exception as e:
    print(f"An unexpected error occurred: {e}")

Convert dictionary to dataframe and save as CSV file# Convert dictionary to DataFrame and save to CSV
salary_list = []
for name, records in salary_dict.items():
    for record in records:
        record["EmployeeName"] = name
        salary_list.append(record)
    
    output_df = pd.DataFrame(salary_list)
    output_df.to_csv("Processed_Salary_Data.csv", index=False)
    
print("Processed salary data saved to 'Processed_Salary_Data.csv'")
converted file will be saved in the same pandas directory
Download the file and zip in the folder named 'Employee Profile' and using r script to unzip the file
