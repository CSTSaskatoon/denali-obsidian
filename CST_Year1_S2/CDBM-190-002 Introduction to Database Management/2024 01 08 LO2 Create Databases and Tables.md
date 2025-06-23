---
quickshare-date: 2024-01-10 10:59:05
quickshare-url: "https://noteshare.space/note/clr80zawx157701mwlm7fwu0o#JY6N08Ob+07aVjHKLSpaZicBu+jcCMp1upAu4u7CcdU"
---
# Conventions for Access
Object (tables and such) names should have no spaces and Camel notation (Ex. CategoryID)
Datatypes (Autonumber, short text, long text) are like variable types
### Creating a new database
Can use templates but it's probably more work than just starting from scratch
### Access Fields
#### Field name
- 64 Character limitation
- A name cannot include a period, exclamation point, brackets ()[] or an accent graph
- Cannot start with a space
- Must be unique within the table
- There are reserve words
#### Field Syntax
- Avoid spaces in names
- Avoid long names
- Table names should start in uppercase
- Field names should start with lowercase
#### Field data types
for example, the _Text_ data type can store either text or numbers, but the _number_ data type can only store numbers
##### Things to Consider
- Match what you want to store with the datatype
### Data Types
#### Short Text
#### Long Text
#### Numbers
Allows positive and negative numbers. Can also contain a  decimal point, comma, a plus sign, minus sign. Use for data that will be used in calculations
#### Large Numbers
#### Date/Time
#### AutoNumber
#### Yes/No
#### Lookup Wizard
Allows you to create a field that lets you choose a value from another table or from a list of values using a combo box
### Field Description (optional)
### Field Properties
dependant on the datatype
Enable you to alter the appearance and behaviour of the field (Add a dollar sign to format as currency)
### Primary key
used to uniquely identify each record in a table
You can have more than one field identified as the Primary Key - referred to as a concatenated Primary Key
PK are important because they are used to create relationships between tables
Access is a relational Database management system
If your database doesn't have unique values that can be used to identify records (Multiple people with the same name), you need to add a record ID field to be the Primary Key
Essentially, Primary Key links tables together which means that each record needs to be _100% unique_
### Guidelines for Designing Tables
Each table contains information about the same subject, and each field in the table contains individual facts about the table's subject
Ex. a customer table may include company name, address, city, phone number, province
- Fields need to relate to the subject of the table
- *Don't include derived or calculated data* (this is done with queries)
- Store info in the smallest logical part (Last Name and First Name are separate fields)
- identify a primary key (**must be unique**)
### Making a database
#### Identify the required fields
Movie Name
Genre
Directors name
Directors DOB
Directors location of birth
Directors bio
Directors movies
Release Date
Writer Name
Writer year born
Writer year died
Writers bio
Writers location of birth
Movie Stars name
Movie Stars DOB
Movie Stars birth location
Movie Stars movies
Storyline
Language
Budget
Production company name
Production company address
Production company CEO
Runtime
#### Combining fields to make tables (*Normalization*), determine field types and sizes
##### Movie Table
MovieID - AutoNumber
Movie Name - Short Text (250 Characters)
Movie Genre - Short Text (30 Characters)
Release Date - Date/Time
Storyline - Long Text
Language - Short Text (30 Characters)
Budget - Currency
Runtime - Number - Integer
#### Identify Primary Key
Since we don't have a field with unique values, we will add a "MovieID" field which will be an AutoNumber