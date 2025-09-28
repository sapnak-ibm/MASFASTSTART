[Previous](./07_maximo_mobile_spare_parts_toggle_lab.md)

# **Module 8: Maximo Database Queries**

## **Module Goal**

This lab expands upon the concept of Maximo relationships introduced in Lab 3. Instead of working with object relationships within the MAS UI you will write you own SQL queries to extract data directly from Maximo's relational database.

---

### **What You Will Learn**

- How to write Maximo SQL queries
- One-to-many Maximo object relationships
- Best practices for extracting data from Maximo

---

## **Lab Requirements**

- Access to MAS 9.1 with `admin` or `maxadmin` credentials
- Familiarity with the Maximo Manage UI
- Familiarity with relational databases
- A SQL GUI for writing and running queries

---

## **Prerequisite Steps**

### **Step 1 - Optional Relational Database Review**

If you would like to review SQL fundamentals check out this short youtube video to catch up to speed.
Link: [SQL Explained in 100 Seconds](https://www.youtube.com/watch?v=zsjvFFKOm3c)

### **Step 2 - Database GUI Connected to Maximo**

This lab was conducted with Dbeaver Community Edition; the setup instructions can be found [here](https://ibm.box.com/s/abhl16rx6785hrpknzdxvybqd3y6c8l9).

### **Step 3a - Set up Test Data**

The queries in the lab require at least one asset that is associated with at least two workorders. Each workorder needs at least 3 worklogs. Reusing any data from the previous labs is okay so long as these conditions are met.

If needed, the prerequisite steps 3b - 3e show how to set the data up.

### **Step 3b - Create Your Asset**

![Image](../labs/images/m8_asset.png)

### **Step 3c - Create a Work Order and Add the Asset to it**

![Image](../labs/images/m8_wo.png)

### **Step 3d - Add Three Worklogs With Summaries to the Work Order**

![Image](../labs/images/m8_worklog1.png)

### **Step 3e - Duplicate Your Work ORder and Add Three More Work Logs to it**

![Image](../labs/images/m8_wo2.png)

---

## **Lab Steps**

### **Step 1: Run a Query That Returns Your Asset Record**

Paste and run the following query to retrieve your asset record:

```sql
Select
    *
FROM
    maximo.asset a
WHERE
    a.assetnum = '[YOURASSETNUM]'
    AND a.siteid = 'BEDFORD';
```

![Image](../labs/images/asset_query.png)

---

### **Step 2: Run a Query that Returns the Work Order Records that Correspond to Your Asset**

Paste and run the following query to return all of your asset's workorder records:

```sql
Select
    *
FROM
    maximo.workorder wo
WHERE
    wo.assetnum = '[YOURASSETNUM]'
    AND wo.siteid = 'BEDFORD';
```

Note down one of the wonums for one of the work orders returned. This will be used in your query for step 3.

![Image](../labs/images/wo_query.png)

---

### **Step 3: Run a Query that Returns the Work Logs Associated With a Work Order**

Paste and run the following query to return all of the work logs for a given work order:

```sql
SELECT
    *
FROM
    maximo.worklog wl
WHERE
    wl.recordkey = '[YOURWONUM]'
    AND wl.class = 'WORKORDER'
    AND wl.siteid = 'BEDFORD'
```

![Image](../labs/images/worklog_query.png)

---

### **Step 4: Combine the Previous Three Queries into a Single Query**

As you may have noticed, we needed the result from the second query to run the third query and if we don't know the assetnums at first we may need to run the first query to get the assetnums as input for the second query. This can quickly become tedious if there are many objects returned in the queries. In this step we are going to run a single query that returns all the data from the first 3 queries.

Also you may have noticed that each query so far returns all columns for each object. This may be needed in some circumstances, but often it's a best practice to filter the columns to only include the ones you need.

Paste and run the following comprehensive query. All you need to supply as input is your asset's assetnum.

```sql
SELECT
a.assetnum, a.siteid, wo.wonum, wo.woclass, wl.worklogid, wl.logtype, wl.description
FROM
    maximo.asset a
    LEFT JOIN maximo.workorder wo ON a.assetnum = wo.assetnum
    AND a.siteid = wo.siteid
    LEFT JOIN maximo.worklog wl ON wl.recordkey = wo.wonum
    AND wl.siteid = wo.siteid
    AND wl.class = 'WORKORDER'
WHERE
    a.assetnum = '[YOURASSETNUM]'
    AND a.siteid = 'BEDFORD';
```

![Image](../labs/images/full_query.png)

Note that with table joins duplicate values are okay and expected. For example, since there are 3 work logs for each work order there are 3 rows returned for each work order record.

---
