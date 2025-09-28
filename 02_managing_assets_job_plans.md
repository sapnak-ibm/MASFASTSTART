[Previous](./01_introduction_goals_personas_scoping.md) | [Next](./03_creating_health_scores.md)

# **Module 2: Create Asset Records**

The asset record ideally comes from the client. Key details include:

- **Asset Number**
- **Location Hierarchy** (for easy querying)
- **Asset Description**
- **Priority**
- **Installation Date**
- **Manufacturer’s Expected End of Life**
- **Meters**
- **Image** (can be generic)
- **Budgeted Cost**
- **Replacement Cost**
- **Any additional details provided by client SMEs during Health Score discovery**

---

In this example, we create a Pump Asset Record from scratch for a mobile demo and health dashboard.

---

### **Step 1. Login to Maximo Manage via the Suite Navigator**

![Image](../images/image_39.png)

---

### **Step 2. Using the Internal Application Navigator, open the ‘Assets’ Application**

![Image](../images/image_40.png)

![Image](../images/image_41.png)

---

### **Step 3. Click ‘New Asset Record’ to open the Asset Creation form**

![Image](../images/image_42.png)

---

### **Step 4. Provide an asset number and description**
Use "{Your_Initial}PUMP123" as your asset 

![Image](../images/image_43.png)

---

### **Step 5. Scroll down and use the internal navigation to ‘Go To’ Locations**

![Image](../images/image_44b.png)

---

### **Step 6. Click ‘New Location’ and provide a Location Number, Description, and Type = ‘Operating’**

![Image](../images/image_45.png)

---

### **Step 7. Save the record, then Click ‘Return with Value’ to return the location to the asset record**

![Image](../images/image_46.png)

---

### **Step 8. Add an Asset Priority (1–5)**

![Image](../images/image_47.png)

---

### **Step 9. Scroll down and set: Installation Date, Expected End of Life, Estimated EOL, Budgeted Cost, Replacement Cost**

![Image](../images/image_48.png)

---

### **Step 10. Using More Actions, click ‘Add/Update Image’ and upload an image of the asset (or a similar asset).**
You can download this image from this page and upload it.

Example image:

![Image](../images/image_49.jpg)

Adding an image is a small detail that greatly improves demo visuals.

![Image](../images/image_50.png)

---

### **Step 11. Update the status to ‘Operating’**

![Image](../images/image_51.png)

![Image](../images/image_52.png)

---

### **Step 12. Navigate to the ‘Meters’ Tab**

---

### **Step 13. Go to the ‘Meter Group’ application and create a new group**

![Image](../images/image_53.png)

---

### **Step 14. Name the meter group to match the Asset Class**

![Image](../images/image_54.png)

---

### **Step 15. Begin adding relevant meters to the group.**  
Defined during Health Score discussions with the client.  
Key rules:  
- **Gauge meters** = numeric up/down  
- **Continuous meters** = always increasing  
- **Characteristic meters** = tied to a Domain of Values  

Example meters:  
- TEMP-F  
- PRESSURE  
- OILCOLOR  

Use the plus button, then **Select Value**.
![Image](../images/image_55.png)

---

## **Step 16. Filter the list by the desired value**  
(TEMP-F, PRESSURE, OILCOLOR) by typing the value into the ‘Meter’ field and clicking **Enter/Return**, then selecting the desired meter. Repeat this process to populate the meter group with all 3 meters.

---

![Image](../images/image_56.png)

---

### **Step 17. Save the record**  
Once all three meters are created, click **Return with Value** to bring the new meters to the asset record.

![Image](../images/image_57b.png)

---

### **Step 18. Click Save on the asset record**

---

### **Step 19. Add Initial Meter Readings**  
In the Assets application, add initial readings to test Health Scores later.  
Navigate to **More Actions → Enter Meter Readings**.

---

![Image](../images/image_58.png)

---

### **Step 20. Enter a new reading for each line**  
- Oil color → Select a reading  
- Pressure & Temperature → Enter numeric values  

---

![Image](../images/image_59.png)

---

## **Create Craft/Labor Record**


### **Step 1. Navigate to the ‘Labor’ Application**  
Using the Internal Application Navigator.

---

![Image](../images/image_60b.png)

---

### **Step 2. Create a new Labor record**  
Use the **New Labor** button on the left-hand Common Actions panel.

Add labor name, associate with your person record, then go to the **Crafts** Tab.  

Use your Firstname initial + Lastname

---

![Image](../images/image_61.png)

If your "Person" does not exist, Follow these steps to create a new person

![Image](../images/image_61b.png)

![Image](../images/image_61c.png)

---

### **Step 3. Provide Craft details**  

In some cases, you may need to create a new craft for the client use case (we use *Mechanic* here).

In order to create a new craft, Scroll down to Crafts

![Image](../images/image_62b.png)

Click "New Craft" and enter necessary information before Saving and clicking "Return With Value"
![Image](../images/image_62c.png)


---

![Image](../images/image_62.png)

---

![Image](../images/image_63.png)

---

### **Step 4. Save the record and return to the ‘Labor’ Tab**

---

### **Step 5. Scroll down and set the Time Zone**  
Set it to your current time zone.

---

![Image](../images/image_64.png)

---

### **Step 6. Save the record**

---

## **Create Job Plan**

A job plan is a structured work event detailing:  
- Materials needed  
- Steps to complete  
- Labor requirements  
- Estimated time  

Often paired with Preventive Maintenance to generate Work Orders.  

---

### **Step 1. Navigate to the Job Plans application**

---

![Image](../images/image_65.png)

---

![Image](../images/image_66.png)

---

### **Step 2. Create a new Job Plan for your pump**  
(Usually provided by SMEs, but here we create a simple plan with tasks, materials, labor, and safety plan.)

---

### **Step 3. Provide a unique Job Plan number, description, and Duration**
Use JPPUMP{your_initials} as Job Plan name

---

![Image](../images/image_67.png)

---

### **Step 4. Add Job Plan tasks**  
Scroll down to Job Plans Tasks to add tasks.

*Tip: Task Numbers increment by 10 for flexibility.*

![Image](../images/image_67b.png)
![Image](../images/image_67c.png)

---

### **Step 5. Add Labor Record**  
Scroll down to the table below and Add a labor record for the Mechanic Craft defined in the associated labor record. Recall – this is a template, so we do not want to reference the labor record, only the craft. The Labor record will be associated at the work order level during the scheduling and assignment process.


---

![Image](../images/image_68.png)

---

### **Step 6. Select the same craft assigned to your user’s labor record**  
Note associated skill levels.

---

![Image](../images/image_68b.png)

---

### **Step 7. Move to the ‘Materials’ tab**  
Add spare parts:  
- **XMP-3400** – Seal to be replaced  
- **12853** – Impeller (optional replacement)

![Image](../images/image_68c.png)

---
![Image](../images/image_68d.png)

---

### **Step 8. Update Status from ‘DRAFT’ to ‘ACTIVE’**  
*Job Plans are revision controlled; use **Create Revision** for updates.*

---

![Image](../images/image_69.png)

---

**Note:** Job Plans can include additional features like inspection forms, safety plans, dynamic calculations, appointments, and more.

---

## **Create Preventive Maintenance Record**


### **Step 1. Navigate to the Preventive Maintenance application**

---

![Image](../images/image_70.png)

---

### **Step 2. Create a new Preventive Maintenance record**  

Provide a description and asset number.
![Image](../images/image_168.png)

---

### **Step 3. Apply the Job Plan**  
Scroll down to Work Order Information section. Attach the Job Plan created earlier and apply the PM work type.

---

![Image](../images/image_71.png)

---

### **Step 4. Apply the Asset created earlier**
({your_initials}PUMP123)

---

![Image](../images/image_72.png)

---

### **Step 5. Set Frequency**  
Go to the **Frequency** Tab and set Time-Based Frequency to **every 6 months**.

---

![Image](../images/image_73.png)

---

### **Step 6. Update Status to ‘Active’**  
Save the record.

---

![Image](../images/image_74.png)

---

[Previous](./01_introduction_goals_personas_scoping.md) | [Next](./03_creating_health_scores.md)
