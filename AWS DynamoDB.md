# Create a DynamoDB table
Amazon DynamoDB is a NoSQL Database in the cloud, suitable for anyone needing a reliable and fully managed NoSQL solution. DynamoDB is designed to provide automated storage scaling and low latency. It is particularly useful when your application must read and store massive amounts of data and you need speed and reliability (Amazon works with replicas of your database in three different Availability Zones). Amazon DynamoDB is totally managed. You simply select an AWS region, define the needed indexes for each table you will create, and Amazon takes care of everything else.

## Service used:
* DynamoDB service
## Project Objectives
* Create and configure DynamoDB tables
* Add and edit rows in DynamoDB tables
* Query information in DynamoDB

## Step 1: Logging In to the Amazon Web Services Console
Login to your AWS account with your credentials.

## Step 2: Creating a DynamoDB Table with a Partition Key

1. From the AWS Management Console, in the search bar at the top, enter DynamoDB, and under Services, click the DynamoDB result.

2. To start creating a new DyanmoDB table, on the right-hand side, click Create table.

3. In the Table details section, enter the following:
* Table Name: Forum
* Partition Key: Enter Name and ensure type is String

4. In the Settings section, select Customize settings.

5. In the Read/write capacity settings section, under Capacity mode, select Provisioned and enter the following:
* Read Capacity:
    * Provisioned capacity units: 10
* Write Capacity: 
    * Provisioned capacity units: 2

6. Scroll to the bottom and click Create table.

In this step, we created a DynamoDB table.

## Step 3: Creating a DynamoDB Table with Local and Global Secondary Indexes

1. On the right-hand side of the page, click Create table.

2. Enter the following in the Table details section:
```
Table name: Thread
Partition key:
    Name: Enter ForumName
    Type: Select String
Sort key:
    Name: Enter Subject
    Type: Select String

```
3. In the Settings section, select Customize settings.

4. Under Read/write capacity settings, ensure Provisioned is selected for Capacity mode, and enter the following:
```
Read capacity:
    Provisioned capacity units: 10
Write capacity:
    Provisioned capacity units: 2
```
5. Scroll down to the Secondary indexes section and click Create local index.

6. Enter the following to configure your local secondary index:
```
Sort Key:
    Name: Enter CreationDate
    Type: Select String
Attribute projections: Select All
```
7. To finish creating the local secondary index, at the bottom, click Create index.

8. Scroll to the bottom and click Create table.

In contrast to a Local Secondary Index, a Global Secondary Index is an index with a partition and sort key that can be different from those in the table. It is considered "global" because queries on the index can span all of the data in a table, across all partitions.

9. Click Create table once more to start creating another table.

10. Enter the following in the Table details section:
```
Table Name: Reply
Partition key:
    Name: Enter ID
    Type: Select String
Sort key:
    Name: Enter CreationDate
    Type: Select String
```
11. In the Settings section, select Customize settings.

12. In the Read/write capacity settings section, ensure the Capacity mode is Provisioned, and enter the following:
```
Read capacity:
    Provisioned capacity units:Enter 10
Write capacity:
    Provisioned capacity units:Enter 5
```
13. Scroll down to the Secondary indexes section, and click Create global index.

14. Enter the following:
```
Partition key:
    Name: Enter ID 
    Type: Select String
Sort key:
    Name: Enter Sticky
    Type: Select String
Attribute projections: Select All
```
15. To finish creating the global secondary index, at the bottom, click Create index.

16. Click Create global index again and enter the following:
```
Partition key:
    Name: Enter AuthorId
    Type: Select String
Sort key:
    Name: Enter CreationDate
    Type: Select String
Attribute projections: Select All
```
17. To finish creating the global secondary index, at the bottom, click Create index.

18. Scroll to the bottom and click Create table.

In this step, we used the DynamoDB dashboard to create multiple DynamoDB tables with local and global secondary indexes.

## Step 4: Inserting Items Into a DynamoDB Table
After creating all the needed tables, you are ready to fill them with demo data.

1. In the left-hand menu, click Explore items.

2. In the Tables list, select Forum

3. On the right-hand side, click Create item under Items returned.

4. In the Value textbox next to Name - Partition key, enter a name for your forum (can be anything you wish).


5. To add another attribute for this item, click Add new attribute and select String from the list of types.

6. In the Attribute name textbox, enter Description and in the Value textbox, enter any value you'd like.

7. At the bottom, click Create item.

8. Repeat steps 3-7 three more times so that end up with four entries in the Forum table.

9. Select the Thread table and click Create Item.

10. Provide any values you'd like for ForumName, Subject and CreationDate, keeping in mind that the ForumName value must match the name of one of your forums.

Note: Thread is a "Partition and Sort" table with the CreationDate-index Local Secondary Index. For being able to save a Thread item, you have to provide:
```
1.ForumName (the table Primary Key)
2.Subject (the table Sort Key)
3.CreationDate (the Local Secondary Index Sort Key)
```
Note: You will have to click Add new attribute to add the CreationDate attribute and specify a value.

11. At the bottom, click Create item.

12. Repeat steps 9-11 three more times until you have four items in the Thread table.

In this step, We inserted several items into two of your DynamoDB tables.

## Step 5: Editing DynamoDB Table Items
1. On the Explore items page, select the Forum table.

2. Select any item in the table and click on its name to get to the Item editor page.

3. Click inside any value and make an update to its contents.

Warning: Note that modifying the partition key will result in changing the values of the item keys. This will delete and recreate the item with new keys.

4. At the bottom of the page, click Save and close.

In this step, you used the DynamoDB console to edit items in a table.

## Step 6: Querying a DynamoDB Table
DynamoDB provides two commands for searching data on the table: scan and query. A scan operation examines every item on the table and returns all the data attributes for each one of them. When you initially navigate to the Items tab for a table, a scan is performed by default.

1. In the left-hand menu, click PartiQL editor.

PartiQL is a SQL (Structured Query Language) compatible language for Amazon DynamoDB. As well as querying tables, you can use it to insert new items and update existing ones.

2. Under Tables, click the three dots next to the  Thread and click Scan table.

The Query 1 editor will be populated with a PartiQL query that selects all items from the  Thread.

3. To execute the PartiQL table, under the editor, click Run.

4. Scroll down to see the results under Items returned.

5. To query for a specific item, replace the contents of the Query 1 editor with the following, and click Run:
```
SELECT * FROM "Thread" WHERE "Subject" = 'Intro to cool stuff'
```
This time, you will only see items returned that satisfy the value of the WHERE condition.

In this step, you practiced using the DynamoDB dashboard to query a table.

## Step 7: Deleting a DynamoDB Table
1. In the left-hand menu, click Tables.

2. In the Tables table, select the Thread table.

3. On the right-hand side, click Delete.

4. In the confirmation textbox, enter confirm and click Delete.

5. To update the Tables table, click the refresh icon.

In this step, you used the DynamoDB dashboard to delete a DynamoDB table.















































































