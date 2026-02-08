# covid clinical-trail-study-



import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from google.colab import files

try:
    df = pd.read_csv("COVID clinical trials.csv")
except FileNotFoundError:
    print("File not found. Please upload the 'COVID clinical trials.csv'")
    uploaded = files.upload()
    if uploaded:
        # Assuming the user uploads the correct file
        for fn in uploaded.keys():
            print(f'User uploaded file "{fn}" with length {len(uploaded[fn])} bytes')
            df = pd.read_csv(fn)
    else:
        print("No file was uploaded. Please upload the file to proceed.")
        df = None

if df is not None:
    print("Dataset loaded successfully.")



df.head()
df.info()
df.describe()

df.info()
print("Missing Values in Each Column:\n")
print(df.isnull().sum())

df['Gender'].fillna("All", inplace=True)
df['Age'].fillna("Not Mentioned", inplace=True)
df['Phases'].fillna("Unknown", inplace=True)
df['Enrollment'].fillna(0, inplace=True)


# Fill missing values in various columns with 'Not Specified'
df['Acronym'].fillna('Not Specified', inplace=True)
df['Interventions'].fillna('Not Specified', inplace=True)
df['Outcome Measures'].fillna('Not Specified', inplace=True)
df['Study Designs'].fillna('Not Specified', inplace=True)
df['Other IDs'].fillna('Not Specified', inplace=True)
df['Start Date'].fillna('Not Specified', inplace=True)
df['Primary Completion Date'].fillna('Not Specified', inplace=True)
df['Completion Date'].fillna('Not Specified', inplace=True)
df['Locations'].fillna('Not Specified', inplace=True)

# Display the number of missing values after imputation
print("Missing Values After Imputation:")
print(df.isnull().sum())

df['Enrollment'] = pd.to_numeric(df['Enrollment'], errors='coerce')


status_counts = df['Status'].value_counts()

print(status_counts)

status_counts.plot(kind="bar")
plt.title("Clinical Trials by Status")
plt.xlabel("Trial Status")
plt.ylabel("Number of Trials")
plt.show()

import pandas as pd
import matplotlib.pyplot as plt
from google.colab import files

try:
    df = pd.read_csv("COVID clinical trials.csv")
except FileNotFoundError:
    print("File not found. Please upload the 'COVID clinical trials.csv'")
    uploaded = files.upload()
    if uploaded:
        for fn in uploaded.keys():
            print(f'User uploaded file "{fn}" with length {len(uploaded[fn])} bytes')
            df = pd.read_csv(fn)
    else:
        print("No file was uploaded. Please upload the file to proceed.")
        df = None

if df is not None:
    # Fill missing values for 'Phases' as done in previous preprocessing steps
    df['Phases'].fillna("Unknown", inplace=True)

  phase_counts = df['Phases'].value_counts()

   print(phase_counts)

  phase_counts.plot(kind="bar")
    plt.title("Trials Distribution by Phase")
    plt.xlabel("Trial Phase")
    plt.ylabel("Count")
    plt.show()



gender_counts = df['Gender'].value_counts()

print(gender_counts)

gender_counts.plot(kind="pie", autopct="%1.1f%%")
plt.title("Gender Distribution in Trials")
plt.ylabel("")
plt.show()

status_counts = df['Status'].value_counts()

print(status_counts)

status_counts.plot(kind="bar")
plt.title("Clinical Trials by Status")
plt.xlabel("Trial Status")
plt.ylabel("Number of Trials")
plt.show()


age_counts = df['Age'].value_counts().head(10)

print(age_counts)

age_counts.plot(kind="bar")
plt.title("Top 10 Age Groups in Trials")
plt.xlabel("Age Group")
plt.ylabel("Number of Trials")
plt.show()




top_sponsors = df['Sponsor/Collaborators'].value_counts().head(10)

print(top_sponsors)

top_sponsors.plot(kind="bar")
plt.title("Top 10 Sponsors Conducting Trials")
plt.xlabel("Sponsors")
plt.ylabel("Number of Trials")
plt.show()


top_conditions = df['Conditions'].value_counts().head(10)

print(top_conditions)

top_conditions.plot(kind="bar")
plt.title("Top 10 Reported Conditions")
plt.xlabel("Condition")
plt.ylabel("Count")
plt.show()


print("Enrollment Summary:\n")
print(df['Enrollment'].describe())



df['Enrollment'].plot(kind="hist", bins=30)
plt.title("Enrollment Distribution")
plt.xlabel("Number of Participants")
plt.show()



study_type_counts = df['Study Type'].value_counts()

print(study_type_counts)

study_type_counts.plot(kind="bar")
plt.title("Study Type Distribution")
plt.xlabel("Study Type")
plt.ylabel("Count")
plt.show()

df['Country'] = df['Locations'].astype(str).apply(lambda x: x.split(",")[-1])

top_countries = df['Country'].value_counts().head(10)

print(top_countries)

top_countries.plot(kind="bar")
plt.title("Top 10 Countries Conducting Trials")
plt.xlabel("Country")
plt.ylabel("Number of Trials")
plt.show()


print("Most Common Trial Status:", df['Status'].mode()[0])
print("Most Common Trial Phase:", df['Phases'].mode()[0])
print("Most Common Gender Eligibility:", df['Gender'].mode()[0])
print("Top Sponsor:", df['Sponsor/Collaborators'].mode()[0])
print("Top Country:", df['Country'].mode()[0])

df.to_csv("Cleaned_COVID_Clinical_Trials.csv", index=False)

print("Cleaned dataset saved successfully!")
























    
