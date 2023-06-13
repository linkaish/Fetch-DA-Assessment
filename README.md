# Fetch-DA-Assessment

## Task 1: Structured Relational Data Model
Below are two images showing how I structured this data model. As different receipt items could contain different table columns according to their natures, I select a subset of features that are helpful to this assessment analysis.

As shown in the second graph, **barcode** is the joinable key for tables **brands** and **receipt item** (one-to-many relationship; Note here in the image, it's shown as many-to-many relationship due to some data quality issues which I will explain in Task 3.); **receipt id** is the joinable key for tables **receipts** and **receipt item** (one-to-many relationship); **user id** is the joinable key for tables **receipts** and **users** (many-to-one relationship).

![alt text](https://github.com/linkaish/Fetch-DA-Assessment/blob/main/Task%201%3A%20Data%20Model/Data%20Model.png)
![alt text](https://github.com/linkaish/Fetch-DA-Assessment/blob/main/Task%201%3A%20Data%20Model/Entity%20Relationship%20Diagram.jpg)


## Task 2: SQL Query
[Query Answer](https://github.com/linkaish/Fetch-DA-Assessment/tree/main/Task%202:%20SQL%20Query)


## Task 3: Data Quality Evaluation


## Task 4: Communicate with Stakeholders
