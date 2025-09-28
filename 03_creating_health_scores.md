[Previous](./02_managing_assets_job_plans.md) | [Next](./04_creating_more_health_scores_and_risk_numbers.md)

# **Module 3: Create Health Group & Scores**

## **Create Health Group**

Health Scoring Groups group similar assets for custom scoring structures. This lets users prioritize work and investments.

---

### **Step 1. Navigate to the Assets application**  

---

![Image](../images/image_75b.png)


Filter to show only desired assets. Use direct table filters or the three-dot menu.

---

![Image](../images/image_75.png)

---

### **Step 2. Save the list to a query**  
Use **Save Current Query**.

---

![Image](../images/image_76.png)

---

### **Step 3. Provide a unique name and description**  
Query Name = {your_initial}-PUMPS

Mark as **Public**.

---

![Image](../images/image_77.png)

---

### **Step 4. Navigate to Maximo Health**  
Using the External Application Navigator.

---

![Image](../images/image_78b.png)

---

### **Step 5. Dismiss Pop-up**  
Click **Do Not Show Again** and **Manually Setup Later** in the Default Score activation pop-up.

---

![Image](../images/image_80.png)

---

### **Step 6. Navigate to Score Settings**  
Use the Internal Application Navigator.

---

![Image](../images/image_81a.png)

---

### **Step 7. Create a new Score or duplicate default**  
We will create from scratch → Click **Create Scoring Group**.

---

![Image](../images/image_82.png)

---

### **Step 8. Provide Name & Description**  
Select the query using **Select**.

---

![Image](../images/image_83.png)

---

### **Step 9. Search for the Query created earlier**

---

![Image](../images/image_84.png)

---

### **Step 10. Click ‘Create’**


---

## **Create Health Scores**

---

Health, Criticality, and Risk scores require contributors. These are built from Maximo Manage data (or integrated Maximo Monitor data). Ensure the following sections are populated for the demo:

* Health:  Populated by contributors and score config  
* Criticality: Populated by contributors and score config  
* Risk: Populated by contributors and score config  
* End of Life: Typically considers Health + RUL  
* RUL (Remaining Useful Life):** Not populated via UI (requires advanced setup)
    * This uses the Install Date and Expected End of Life fields on the asset record
* Age – Years since install date
    * This uses Install Date of the Asset
* Effective Age – Age of the Asset considering external factors
    * Generally, takes into account the health and RUL of the asset
    * This is not currently able to be populated via health UI and requires advanced setup
* Next PM -
    * This looks at the next time a PM record will be auto generated for the asset
    * This requires a PM record to be generated before appearing
* MRR – Maintenance Replacement Ratio
    * Considers all costs of maintenance compared to the cost of replacement
    * Looks at Total Cost of Asset and Replacement Cost of asset
* MTBF – Mean time Between Failure
    * Set a Threshold for what the minimum MTBF should be for corrective work on an asset class

![Image](../images/image_85.png)


Once our scores are defined, and the required asset data is populated, we will have a dashboard as shown above. To accomplish this, we will need to do a few things: Create Contributors for Scores, Add Contributors to scores and Add Thresholds to the Out of the Box KPIs.

---

## **Steps**

### **Step 1.Nevigating Back**
On the **Maximo Health**, click the **Score Settings** on the top left.

![Image](../images/image_169.png)



### **Step 2. Open Threshold Settings**
On the **Maximo Health → Score Settings Menu**, click the **Threshold** tab.

![Image](../images/image_86.png)

---

### **Step 3. Create a New Threshold**
Click **Create Threshold**.

![Image](../images/image_87a.png)

---

Step 4. **Provide the following details:**
   - **Name**  "{Your_Initials}-MTBF"
   - **Description**
   - **Threshold:** 14 days

![Image](../images/image_88.png)

---

Step 5. **Navigate to the Contributors tab**  
   *Contributors are formulas that make up a health score. A single contributor can be used for multiple score types. Some contributors may require additional configuration in **Manage** by creating new relationships for the Asset table.*

![Image](../images/image_89.png)

---

Step 6. **Create a New Contributor**  
   Click the **Create Contributor** button in the top-right corner.

![Image](../images/image_90.png)



## Contributor Screen

On the Create Contributor screen, we will see a few options and fields:

* **Duplicate**: This will allow you to select a contributor to duplicate the setting and formulas for. This is beneficial when you have complex contributors
* **Name**: Provide a unique, and meaningful name – If you are in a shared system, you will want to tag with your initials to prevent duplicates
* **Description**: Describe what the formula is doing
* **Object**: Health scores can be for assets or locations; the selection of this object indicates what table we are starting from. If your contributor requires a relationship, and the object selected is 'Asset', then the relationship being referenced needs to be on the Asset Object in the Data base configuration application
* **Data Source**: If meter is selected, it will calculate the scoring results differently using an upper limit and a lower limit while automatically providing the formula for METERVAL. If formula is selected, you will provide a best and worst value and the formula
* **Unit of Measure**: What to be displayed next to the calculated results
* **Formula**: This will contain the calculation for the contributor function. In this formula, you will reference relationships and attributes either directly, or within functions. The general format will be `RELATIONSHIP$ATTRIBUTE`
* **Value Normalization**: For formulas, we select the 'best' value and the 'worst' value for the formula results to be put on a scale from 0 to 100. For meters, you will use an upper and lower threshold. Additionally, if the meter has a record, you can default to use those limits

## Step 7a. Adding Relationships to Database Configuration:

Before we create the Contributors we will first need to add a new relationship in the Database Configuration in Manage
* Open up the Database Configuration in **Manage**. We recommend opening it in a new tab

    ![Image](../images/image_170.png)
* Open the *ASSET Table* Object
![Image](../images/image_91a.png)
* Go to the *Relationships* tab at the top
![Image](../images/image_91b.png)
* Click the '+' sign and fill out the following information:
Relationship: CMWO
Child Object: WorkOrder
Where Clause: `assetnum=:assetnum and siteid=:siteid and WORKTYPE='CM'`
![Image](../images/image_91c.png)

Save and then return back to the *Create a contributor* Page  

## Step 7b. Create the following Contributors:

### MTBF for Corrective Maintenance:

* Provide a name (which includes your initials) description for the mean time between failure function
* Set the object to 'Asset'
* The Data Source to 'Formula'
* For the formula, we will use two different functions, one MTBF and the other DURATION. Find details of these formulas in the documentation. Populate the formula box with: `MTBF("CMWO",-1,DURATION(0,13,0,0,0,0),"reportdate","actfinish")/30`
* Provide a best value with 100 days and the worst value with 0 days
* Press create to save
---
![Image](../images/image_91.png)
---

### Total Cost of a Corrective Maintenance:

* Using the same relationship above, we can create a new contributor for total cost of maintenance. Provide a name and description
* Set the Object to Asset
* Set the Data Source to Formula
* For the formula, we will use the `RELATIONSHIP$ATTRIBUTE` syntax: `(CMWO$ACTTOTALCOST)/REPLACECOST`
* ACTTOTALCOST is an attribute of work order, accessed through the CMWO relationship, and REPLACECOST is an attribute of the asset. It is a best practice to keep contributors as a ratio, as maintenance for a pump will be much more expensive than maintenance of a conveyor. Keeping this as a ratio allows for one contributor, with a best/worst value to be used across many asset classes
* Provide a Unit of Measure of %
* Provide a Best value of 25 and a worst value of 100

### Est Cost of Replacement:

* This example, we will be using asset attributes only. Provide a name and a description for the contributor
* Set the Object to Asset
* Set the Data Source to Formula
* Set the formula to: `REPLACECOST/BUDGETCOST`
* Set the Best value to 0 and the worst value to 100

### Pressure Meter

* This example, will use a simple Meter for Pressure. Pressure is a Guage meter. Provide a name and description for the contributor
* Set the object to Asset
* Set the Data Source to Meter
* Select the 'PRESSURE' meter
* Set the units to PSI (It should set based off the selected meter)
* Lower Limit: 30
* Upper Limit: 60
* **NOTE**: In some cases, you may want to use a Specification on the Asset to make the Pressure contributor Dynamic, specification values are referenced in formulas as `SPECVAL('{SPECNAME}')`

### Oil Meter
* This example will use a Characteristic Meter for Oil Color. Provide a name and description for the contributor
* Set the object to Asset
* Set the Data Source to Meter
* Select the ‘OILCOLOR’ meter
* This auto populates the formula with an IF statement. Update the IF statement to match this:
   ` IF(METERVAL("OILCOLOR")="LBROWN",4,IF(METERVAL("OILCOLOR")="DBROWN",6,IF(METERVAL("OILCOLOR")="TURBID",2,IF(METERVAL("OILCOLOR")="RED",3,IF(METERVAL("OILCOLOR")="CLEAR",1,IF(METERVAL("OILCOLOR")="BROWN",5,-1))))))`
* Best value: 0
* Worst Value: 6

### Temperature
* This is an example contributor for Motor Temperature
* Set the object to Asset
* Set the Data Source to Meter
* Meter Type contributor
* Select ‘TEMP-F’
* Unit: Fahrenheit
* Lower Limit: 150
* Upper Limit: 200

### Health Contributor
* Often, we find use cases to reference the result of another score within a score. Name this contributor ‘Health’ and provide a description
* Set the object to Asset
* Set the Data source to Formula
* Populate the formula with: `ASSETLOCSCORE("HEALTH")`
* Best Value: 100
* Worst Value: 0

### Criticality Contributor
* Name this contributor “Criticality" and provide a description
* Set the object to Asset
* Set the Data source to Formula
* Populate the formula with: `ASSETLOCSCORE("CRITICALITY")`
* Best Value: 0
* Worst Value: 100


[Previous](./02_managing_assets_job_plans.md) | [Next](./04_creating_more_health_scores_and_risk_numbers.md)
