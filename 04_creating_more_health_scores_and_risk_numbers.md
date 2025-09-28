[Previous](./03_creating_health_scores.md) | [Next](./05_creating_health_views_and_mobile_access.md)

# **Module 4: Create Health Scores Continued**

---

### **Step 8: Review Context**
Now that all contributors have been created, we can create the **Health Scores**.  
(*Note:* “Health Scores” typically include **Health**, **Risk**, and **Criticality**.  
Custom scores can also be created for additional scoring types.)

---

### **Step 9: Navigate to Your Scoring Group**
Go to the **Scoring Group** you created earlier.

![Image](../images/image_92.png)

---

### **Step 10: Select the Scoring Group**
Choose the group you created.

---

### **Step 11: Click ‘Add Score’**
Click the **Add Score** button.

![Image](../images/image_93.png)

---

### **Step 12: Select Health Score**
Select **Health** and click **Done**.  
(*Choose the blank Health score instead of default.*)

![Image](../images/image_94.png)

---

### **Step 13: Create Contributor Groups**
Contributor Groups allow multiple contributors to roll up into a component of the score.  

We will create:
- **Maintenance History**
- **Meter History**

Click the **Group** button (top right of Contributors chart).

![Image](../images/image_95.png)

---

### **Step 14: Create First Group**
- **Name:** Maintenance History  
- **Description:** Summary of Maintenance Activities  
Click **Create**.

![Image](../images/image_96.png)

---

### **Step 15: Create Second Group**
*Use Group button again*
- **Name:** Meters  
- **Description:** Summary of Pump Meters  
Click **Create**.

![Image](../images/image_171.png)

---

### **Step 16: Add Contributors**
- Open **Maintenance History** group.
- Click the **+** button (top right).

![Image](../images/image_97.png)

---

### **Step 17: Select Contributors**
- **OPENCMWO**
- **Mean Time between Failures (MTBF)**
- **Total Cost of CMs**

Click **Add**.

![Image](../images/image_98.png)

---

### **Step 18: Edit Weights**
Click the **Pencil** icon (top right) to edit weights.  
All weights within a group must total **100%**.

![Image](../images/image_99.png)

---

### **Step 19: Assign Weights**
- **MTBF:** 50%  
- **Total Cost of CMs:** 10%  
- **OPENCMWO:** 40%  

Click **Save**.

![Image](../images/image_100.png)

---

### **Step 20: Repeat for Meter Group**
Go back to the Previous Page using the Breadcrumb Menu and the top and repeat for the **Meters** group.

For the **Meters** group, use the following contributors and weights:
- **Motor Temperature:** 15%  
- **Oil Quality:** 50% 
- **Pressure:** 35%

---

### **Step 21: Add Remaining Useful Life (RUL)**
Navigate to the Health Score configuration page, and add the **RUL (Remaining Useful Life)** contributor to the Health Score using the **plus** button in the top right.

![Image](../images/image_101.png)

![Image](../images/image_172.png)

---

### **Step 22: Edit Weights**
Use the **Pencil** icon to edit the weights of the final Health Score.

![Image](../images/image_102.png)

---

### **Step 23: Activate Health Score**
Click the **Active** button in the top right to enable the health score.

![Image](../images/image_103.png)

---

### **Step 24: Repeat for Criticality and Risk**
Return to the **Health Score Group** page by clicking Pumps for client in the left hand corner and repeat the process for **Criticality** and **Risk**.  
These will not need contributor groups; all scores will be at the top level.


![Image](../images/image_173.png)

---

### **Step 25a: Critacilty**

Select Critacilty and click Done.  
(Choose the blank Critacilty score instead of default.) 

- Open Criticality group.  
- Click the + button (top right)   

Select Contributors  
  - Priority – 60%
  - Cost of Replacement – 40%

Click the Active button in the top right to enable the Criticality score.

![Image](../images/image_174.png)
    


---

### **Step 25b: Risk**

Select Risk and click Done.  
(Choose the blank Risk score instead of default.)  

- Open Risk group.  
- Click the + button (top right)  

Select Contributors  
- Health – 70%
- Criticality – 30%

Click the Active button in the top right to enable the Criticality score.



![Image](../images/image_175.png)


---

### **Step 26: Force Score Calculation**
Click the *Calculate Scores* button at the top if scores do not calculate automatically. If you see a red circle on the scores, that means it did not calculate properly. To troubleshoot, take these actions:
- Create a **test contributor**, add it to the score with 0% weight.
- Start with a **count function** on the relationship and confirm it returns a value.
- Gradually add components of the formula.
- If no result, validate the relationship by:
    - Replacing dynamic values (e.g., `:assetnum`) in the **where clause**.
    - Test the query in the child object application.

![Image](../images/image_104.png)


---

## **Create Health View**


### **Step 1: Navigate to Asset Health Page**
![Image](../images/image_105a.png)

---

### **Step 2: Click Filter (Top Right)**
![Image](../images/image_106.png)

---

### **Step 3: Edit Query**
Click the pencil icon and select the query created for the Health Scoring Group.

![Image](../images/image_107.png)

---

### **Step 4: Apply Filter**
![Image](../images/image_108.png)

---

### **Step 5: Switch to Matrix View**
Click the **Matrix View** button (top right).

![Image](../images/image_109.png)

---

### **Step 6: Confirm Dropdown**
Ensure it says **Criticality and Health**.

![Image](../images/image_110.png)

---

### **Step 7: Configure Settings**
Click the **Settings Cog** (top right).

![Image](../images/image_111.png)

---

### **Step 8: Toggle Default View**
Enable **Default**, then click **Save**.

![Image](../images/image_112.png)

---

### **Step 9: Save Personal View**
Use the dropdown in the top left → **Save as New View**.

![Image](../images/image_113.png)

---

### **Step 10: Provide Title**
Select **Save as my Default View**, then click **Save**.

![Image](../images/image_114.png)

---

**Tip:** For client POCs, ensure at least one asset falls in the **red zone**, signaling it needs immediate attention.

---


[Previous](./03_creating_health_scores.md) | [Next](./05_creating_health_views_and_mobile_access.md)
