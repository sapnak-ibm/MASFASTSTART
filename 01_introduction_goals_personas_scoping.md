[Previous](../modules/01a-health-and-monitoring.md) | [Next](./02_managing_assets_job_plans.md)

# **Module 1: Overview**  
### Maximo Mobile + Health Hands-on Lab

---

## **Overview & Discovery**

### **Business Case**

Maximo Health is designed to provide a detailed view of asset health and provide comparison dashboards for an overall view of all assets. It is aimed at reliability engineers whose primary goal is to keep assets up and running across various industries.  
Health combines IoT sensor data, work order history, manual meter readings, and more to create a **one-stop shop** for Reliability-Centered Maintenance.

---

![Image](../images/image_1.png)

---

Maximo Mobile provides technicians the ability to capture data and perform corrective or preventive work on the go. Historically, users had to return to a desktop to update work or log details, causing delays. With mobile access, technicians can now record meter readings, failures, inspection data, and more **in real-time**, improving data accuracy and preparing clients for AI-driven insights.

---

## **Goals**

Common business value goals to communicate to clients:

- **Reduce Unplanned Downtime**  
    *Considerations: Cost of Failures, Average Time to Repair*

- **Increase Asset Production**  
    *Considerations: Loss of Production Time*

- **Optimize Maintenance Practices**  
    *Considerations: Cost of extra trips to assets vs. preventive maintenance vs. over-maintenance costs*

- **Optimize Technician Practices**  
    *Considerations: Reduce time between work orders, increase productivity, increase data capture*

---

## **Story**

This scenario involves three personas:

- **Reliability Engineer** – Maintains asset health, reduces downtime, and analyzes performance.  
- **Maintenance Manager / Planner** – Plans work, assigns work, and manages job plans and schedules.  
- **Technician** – Performs physical repairs and maintenance tasks.

---

![Image](../images/image_2.png)

---

## **Scoping**

When implementing Maximo Mobile + Health, define the following:

---

### **1. Asset Class of Focus**  
Select an asset with available SMEs and data for playback sessions.  

![Image](../images/image_3.png)

---

### **2. Health Score for the Asset Class**  
Work with SMEs to define contributors and weights for health scores, ensuring they are quantifiable. Contributors should have defined “Best” and “Worst” values for normalization.  

Example: Two contributor groups (Maintenance History and Meter History) plus Remaining Useful Life (RUL).  
SMEs collaborate with designers to identify all data sources.  

![Image](../images/image_4.png)

*Note:* Criticality and Risk scores can also be included but are optional. By default, asset priority can represent criticality, and **Health × Criticality = Risk**.

---

## 🧠 **Key Maximo Concepts (Before You Begin)**

Before you dive into creating records and navigating Maximo, it's helpful to understand the core building blocks of asset management in Maximo:

### 🔧 **Job Plan**
A **Job Plan** is a reusable template that outlines the steps, materials, labor, and estimated duration required to perform a specific maintenance activity. Think of it as the playbook for a task.

- Used in **Preventative Maintenance** to standardize recurring tasks
- May include checklists, safety plans, and required parts
- Can be revised and version-controlled

### 🛠️ **Work Order**
A **Work Order** is a specific instance of work that needs to be performed on an asset. It can be generated manually or automatically (e.g., from a PM).

- Assigned to technicians
- Tracks labor, materials, and downtime
- Serves as the execution record for maintenance activities

### ⏱️ **Preventative Maintenance (PM)**
A **Preventative Maintenance** record automates the creation of Work Orders based on time or usage.

- Linked to a Job Plan
- Triggers work based on a set schedule (e.g., every 6 months) or a meter reading (e.g., every 100 hours)
- Helps ensure routine maintenance is never missed

### 📊 **Health Score**
A **Health Score** quantifies the condition of an asset based on configurable data inputs:

- Contributors can include maintenance history, sensor data, or meter readings
- Scores are normalized (0–100 scale) and grouped (e.g., Meter Health vs Maintenance Health)
- Combined with Criticality and Risk to help prioritize asset maintenance

### ⚙️ **Meters**
**Meters** record real-time values tied to an asset’s performance or condition.

- Types: Gauge (variable), Continuous (only increases), Characteristic (qualitative)
- Common meters: Temperature, Pressure, Oil Quality
- Used in PM triggers and Health Score contributors

### 👤 **Person and Labor Records**
Before work can be assigned or executed in Maximo, you must also set up:

- **Person records**: Represent individual users or employees
- **Labor records**: Link a person to their craft (e.g., Mechanic, Electrician) and availability

These foundational elements are required to simulate work execution in Maximo Mobile.

---


## 🧭 **What You Will Do in This Lab (Complete Walkthrough Overview)**

This hands-on lab will guide you step-by-step through configuring and using Maximo Mobile + Health using a realistic asset scenario. Here's everything you will do:

### 🧱 Access the Maximo UI
- Access and log in to **Maximo Application Suite (MAS)**

---

### 🏗️ Asset Creation & Configuration
You’ll create a realistic **Pump asset**, complete with:
- **Asset number** and **description**
- **Location** hierarchy (create a new location of type 'Operating')
- **Priority**, **Installation date**, **Expected End of Life**
- **Budgeted and Replacement Cost**
- Upload a **photo/image** of the asset
- Set status to `Operating`

---

### 📏 Meter Configuration
- Create a **Meter Group** and associate with your Pump asset
- Add the following meters:
  - `TEMP-F` (Temperature, Gauge type)
  - `PRESSURE` (Gauge type)
  - `OILCOLOR` (Characteristic type)
- Enter **initial readings** for these meters

---

### 👤 Person, Labor, and Craft Setup
- Create a **Person record**
- Create a **Labor record** linked to that person
- Assign a **Craft** (e.g., Mechanic)
- Set the **Time Zone** for the labor record

---

### 📋 Job Plan Creation
You’ll define a Job Plan template that includes:
- Multiple **Tasks** (e.g., inspect impeller, replace seal, check temperature)
- **Labor** requirements (using Craft, not specific person)
- **Materials** (e.g., XMP-3400 Seal, 12853 Impeller)
- Activate the job plan

---

### 🗓️ Preventative Maintenance (PM) Setup
- Create a **PM record** linked to your pump and job plan
- Set a **6-month time-based frequency**
- Activate the PM

---

### 📈 Maximo Health Configuration
- Save a **query** for your pump to use as a filter
- Create a **Health Scoring Group**
- Define **Contributors** for:
  - Maintenance History (e.g., MTBF, Total CM Cost)
  - Meter Data (e.g., Pressure, Oil Quality, Temperature)
  - RUL (Remaining Useful Life)
- Organize contributors into **Contributor Groups**
- Set **thresholds**, assign **weights**, and **activate scores** for:
  - Health
  - Criticality (e.g., Priority, Replacement Cost)
  - Risk (based on Health × Criticality)

---

### 🗃️ Create a Health View
- Navigate to **Asset Health** UI
- Filter using saved query
- Switch to **Matrix View**
- Save a **personal view** with colored health/risk indicators

---

### 📱 Maximo Mobile Demonstration
- Download Maximo Mobile from App Store or Google Play
- Log in using Technician credentials
- Perform work:
  - **Start work**, **receive materials**, **log downtime**
  - Complete tasks and **enter meter readings**
  - **Create a follow-up work order** for observed issues
  - Record unplanned materials (e.g., used impeller)
  - **Mark work order as complete**

---

### 🔁 Refresh and Analyze Health Scores
- Return to Maximo Health to view:
  - **Updated Health Score**
  - Impact of meter readings and work order on asset status

---

This comprehensive scenario simulates a full maintenance lifecycle and data capture process that prepares your environment for real-time analytics, predictive maintenance, and AI-assisted optimization.
---
---



[Previous](../modules/01a-health-and-monitoring.md) | [Next](./02_managing_assets_job_plans.md)
