[Previous](./05_creating_health_views_and_mobile_access.md) | [Next](./07_maximo_mobile_spare_parts_toggle_lab.md)

# **Module 6: Health Score Dashboard**


### **Review Health Scores**

As a Reliability Engineer:

- Review assets by **health**, **risk**, and **criticality**.
- Prioritize work and reduce unplanned downtime.

---

### **Step 1: Navigate to Health Application**

![Image](../images/image_165.png)

---

Here, I can see all of the assets under my supervision. I can organize the list as needed for quick comparison and analysis – or use the Matrix View to see a high-level clustering of assets that need attention.

---

### **Step 2: Click the Matrix View button**

![Image](../images/image_125.png)

---

### **Step 3: Drill into the asset with the lowest health score**

Using the asset comparison, drill into the asset with the lowest health score.

![Image](../images/image_126.png)

---

_Note: In this example, we only have one asset. In a live POC, you should have at least 2–3 assets, ideally one that needs attention._

---

### **Step 4: View Asset Details**

We can see more details as designed by the reliability engineer’s custom view. Click into the asset that needs attention most to access its detailed dashboard.

![Image](../images/image_127.png)

---

### **Step 5: Review and Analyze Health Scores**

Scroll through the page and discuss:

- Configured scores created with SMEs
- Asset health history

Ensure you move the timeline to only show data since it has been calculated.

![Image](../images/image_128.png)

---

### **Step 6: Click on the ‘Actions’ button**

Located in the top-right corner.

![Image](../images/image_129.png)

---

**Note:** Based on the health and criticality of this asset, you may want to:

- Create an inspection
- Schedule corrective activity
- Plan a replacement

For this demo, we will **review scheduled maintenance** using the asset timeline and Maintenance History chart.

---

### **Step 7: Review the Asset Timeline and Maintenance History**

---

### **Step 8: Sort by Scheduled Start**

In the maintenance history section, sort by scheduled start. Notice the PM is coming up soon.

![Image](../images/image_130.png)

---

Instead of creating an extra inspection or corrective maintenance record, we will drill into this PM and **move the scheduled start up** to avoid unplanned downtime.

---

### **Step 9: Open the Work Order and Update the Scheduled Start**

Update it to **tomorrow’s date**.


---

## **Assign Work Order**

As a Maintenance Manager, review and assign work based on priority and scheduled dates. Assign the right personnel with proper skills.

---

### **Step 1: Navigate to Work Order Tracking**

Open the newly generated work order.

---

### **Step 2: Assign Your Labor Record**

Assign your labor record to your user and ensure:

- The work order is **Approved**
- A **Scheduled Start Date** is set

| ![Image](../images/image_131.png) | ![Image](../images/image_132.png) |

---



## **Perform Work on Mobile**

As a technician, use **Maximo Mobile** to review work, gather materials, and perform assigned tasks without relying on desktop or paper.

---

### **Step 1: Open Maximo Mobile → Click "My Schedule"**

![Image](../images/image_133.png)

---

### **Step 2: Sort Assigned Work by Priority**

| ![Image](../images/image_134.png) | ![Image](../images/image_135.png) |

---

### **Step 3: Update Sort Order and Confirm**

Click the blue check in the top right.

![Image](../images/image_136.png)

---

### **Step 4: Open Your Assigned Work Order**

Click **Start Work** to begin tracking labor time.

![Image](../images/image_137.png)

---

### **Step 5: Collect Materials and Tools**

Click **Materials and Tools** → Select reserved items.

![Image](../images/image_138.png)

---

### **Step 6: Select Items**

| ![Image](../images/image_139.png) | ![Image](../images/image_140.png) |

---

### **Step 7: Receive the Seal**

For now, receive only the Seal. The impeller may be replaced later.

| ![Image](../images/image_141.png) | ![Image](../images/image_142.png) |

---

### **Step 8: Mark Asset as Offline**

Click **Downtime** before starting work to:

- Prevent IoT anomalies
- Track accurate production output

| ![Image](../images/image_143.png) | ![Image](../images/image_144.png) |

---

### **Step 9: Enter Downtime Code**

Use **"Adjust"** for this PM task.

![Image](../images/image_145.png)

---

### **Step 10: Open Task List**

Follow steps and mark each task as complete.  
If you find an issue (e.g., impeller wear), note it for follow-up.

![Image](../images/image_146.png)

---

### **Step 11: Complete Tasks 10–60**

Mark as complete.

![Image](../images/image_147.png)

---

### **Step 12: Record Meter Readings**

Task 70 requires recording:

- Temp
- Pressure
- Oil Color

![Image](../images/image_148.png)

---

### **Step 13: Open "Meter Readings"**

![Image](../images/image_149.png)

---

### **Step 14: Enter Readings**

| ![Image](../images/image_150.png) | ![Image](../images/image_151.png) |

---

### **Step 15: Create a Follow-Up Work Order**

If an issue is detected (e.g., housing crack), create a **Corrective Maintenance Work Order**.

![Image](../images/image_152.png)

---

### **Step 16: Add Work Order Details**

![Image](../images/image_153.png)

![Image](../images/image_154.png)

---

### **Step 17: Update Work Type to CM**

| ![Image](../images/image_155.png) | ![Image](../images/image_156.png) | ![Image](../images/image_157.png) |

---

### **Step 18: Save the Work Order**

![Image](../images/image_158.png)

---

### **Step 19: Complete Remaining Tasks**

| ![Image](../images/image_159.png) | ![Image](../images/image_160.png) |

---

### **Step 20: Add Material Usage (Impeller)**

![Image](../images/image_161.png)

---

### **Step 21: Select and Confirm**

| ![Image](../images/image_162.png) | ![Image](../images/image_163.png) |

---

### **Step 22: Complete the Work Order**

Mark as complete to stop the labor timer and log time.

![Image](../images/image_164.png)

---


## **Refresh Health Score**

### **Step 1: Return to Health Application and Refresh**

![Image](../images/image_165.png)

---

### **Step 2: Review Health Timeline**

Notice a new entry. Over multiple demonstrations, the Health UI will reflect improvements:

- Health increases after PM actions
- Timeline documents work and condition changes


---

## **Big Picture**

As clients move toward **Predictive Maintenance**, capturing accurate data becomes critical.

---

### **Key Goals**

1. Use Analytics, Machine Learning, and Asset Expertise to predict failures.
2. Capture **failure/problem codes** during events for modeling predictive scenarios.

---

![Image](../images/image_166.png)

---

### **AI and Automation**

- Generative AI tools like **Work Order Advisor** automate population of problem codes.
- Provides accurate targets for predictive failure models.
- Every Maximo release introduces more Agentic and AI-driven features, increasing the importance of **quality data collection by technicians**.

![Image](../images/image_167.png)

---

[Previous](./05_creating_health_views_and_mobile_access.md) | [Next](./maximo_mobile_spare_parts_toggle_lab.md)

