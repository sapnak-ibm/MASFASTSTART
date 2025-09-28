[Previous](./05_creating_health_views_and_mobile_access.md) | [Next](./08_maximo_database_queries.md)

# **Module 7: Maximo Mobile Customization – Add Spare Parts Toggle**

## **Module Goal**

This lab guides you through customizing the Maximo Mobile Technician application in MAS 9.1. You'll add a toggle that filters material items based on whether they are spare parts for the asset. All steps use the MAS UI—no Docker or external MAF tools required.

---

### **What You Will Learn**

- How to access Application Configuration in MAS 9.1
- How to duplicate the TECHMOBILE application
- How to modify `app.xml` and `AppCustomizations.js` to support a spare parts toggle
- How to preview and publish your changes

---

## **Lab Requirements**

- Access to MAS 9.1 with `admin` credentials
- A configured TECHMOBILE application
- At least one work order with an associated asset and spare parts configured
- At least one approved work order assigned to your user for testing
- Familiarity with the Maximo Manage UI

---

## **Prerequisites: Set Up Test Data**

### **Create Test Work Order with Asset**

1. Navigate to **Work Orders** → **Work Order Tracking** in Maximo Manage
2. Create a new work order:
   - Provide a description (e.g., "Test Mobile Customization")
   - Assign an **Asset** (important for spare parts filtering)
     for example Burner, Gas Fired - For Boiler
   - Assign to yourself as **Owner** using Select Owner
     for example "Steve Miller"
   - Initiate Work Order
     Memo is optional, click OK

---

![Image](../labs/images/wotracking.png)

---

![Image](../labs/images/wotracking2.png)

---

![Image](../labs/images/wotracking3.png)

---

![Image](../labs/images/wotracking4.png)

---

![Image](../labs/images/wotracking5.png)

---

3. **Approve** the work order (Status = APPR)

---

![Image](../labs/images/wotracking6.png)

---

4. Ensure the asset has **spare parts** configured (Optional):
   For this demo, the Asset: Burner, Gas Filer - For Boiler does not have spare parts you can optionally add
   them via the "Assets" menu. You can skip this in this module, the mobile customization option will show up but no spare parts will be listed.
   - Go to **Assets** → **Assets**
   - Find your asset and navigate to **Spare Parts** tab
   - Add some items as spare parts if none exist

---

## **Lab Steps**

### **Step 1: Access the Application Configuration Tool**

1. From MAS, navigate to **Application Administration** in the left navigation
2. Click on **Application Configuration**

---

![Image](../labs/images/mobile1.png)

---

3. You'll see a list of customizable applications (mobile and desktop)

---

### **Step 2: Preview the Default Application**

1. Locate **TECHMOBILE** in the application list
2. Click on **TECHMOBILE** to open it
3. Select **AppCustomizations.js** from the dropdown
4. Click **Preview** to see the default Mobile application

![Image](../labs/images/mobile7.png)

---

5. Note: It will take some time to load, but you'll see the default Mobile application page

![Image](../labs/images/mobile6.png)

---

6. Navigate around to familiarize yourself with the current interface
7. Go back to the Application Configuration page

---

### **Step 3: Duplicate the TECHMOBILE Application**

1. In the Application Configuration list, locate **TECHMOBILE**
2. Click the **three-dot menu** (⋮) next to TECHMOBILE
3. Choose **Duplicate**

---

![Image](../labs/images/mobile4.png)

---

4. In the duplicate dialog:
   - **Application name**: `TECHMOBILECOPY` (or use your initials like `TECHMOBILE_[YourInitials]`)
   - **Description**: `Spare Parts Toggle Customization`
5. Click **Duplicate**
6. Once created, click on your new duplicated app to enter the code editor

---

### **Step 4: Enable Mobile Download for New App**

1. In your duplicated application, click **Edit** (if not already in edit mode)
2. In the application settings dialog:
   - Toggle **ON** the "Enable mobile download" option
   - Click **Save**

---

![Image](../labs/images/enabledl.png)

---

3. This ensures your customized app can be downloaded by mobile devices

---

### **Step 5: Declare Spare Part Attribute in `app.xml`**

1. Ensure you're editing `app.xml` (select it from the dropdown if needed)
2. Search for `assetLookupDS`
3. Locate the `<maximo-datasource>` with `id="assetLookupDS"`
4. Find the `<schema>` section within this datasource
5. Add the following attribute inside the schema (around line where other attributes are defined):
   ```xml
   <attribute id="a1_qm__a" name="rel.sparepart{itemnum,itemsetid,quantity}"/>
   ```
6. **Save** your changes

---

### **Step 6: Add the Toggle Button**

1. Still in `app.xml`, search for `djpqr`
2. Locate the `<box>` with `id="djpqr"`
3. Add the following toggle button code inside this box:
   ```xml
   <toggle id="a1_bg4re"
           label="Filter Spare Part"
           on-toggle="changeSpareToggle"
           readonly="{!woDetailsReportWork.item.assetnumber}"
           toggled="{page.state.addSparePart}"/>
   ```
4. **Save** your changes

---

### **Step 7: Modify Material Lookup Buttons**

1. In `app.xml`, search for `wrkd5` to find the end tag
2. Within this section, locate the `<button>` with `id="dmn9g"`
3. **Replace** the existing button with these **two buttons**:

   ```xml
   <button hidden="{!page.state.addSparePart || !woDetailsReportWork.item.assetnumber}"
           icon="carbon:chevron--right"
           id="a1_bede6"
           kind="ghost"
           on-click="openSparePartLookup"
           on-click-arg="{{'page':page,'app':app,'item':woDetailsReportWork.item}}"
           padding="false"/>

   <button hidden="{page.state.addSparePart &amp;&amp; woDetailsReportWork.item.assetnumber}"
           icon="carbon:chevron--right"
           id="dmn9g"
           kind="ghost"
           on-click="customOpenMaterialLookup"
           on-click-arg="{{'page':page,'app':app}}"
           padding="false"/>
   ```

   **Note**: The `&amp;&amp;` is the XML-encoded version of `&&`

4. **Save** the file

---

### **Step 8: Add Custom Logic to `AppCustomizations.js`**

1. Switch to the **AppCustomizations.js** tab from the dropdown
2. You should see the basic structure with a `return` statement
3. **Add** the following three functions inside the returned object (after line 6, before the closing brace):

   ```javascript
   async openSparePartLookup(event){
     let item = event.item;
     let sparepartitems = [];

     if (item.assetnumber) {
       // Get spare parts for the asset
       let assetDs = this.app.findDatasource("assetLookupDS");
       assetDs.setQBE('assetnum', '=', item.assetnumber);
       assetDs.setQBE('siteid', '=', item.siteid);
       let result = await assetDs.searchQBE();

       if(result.length === 1 && result[0].sparepart){
         result[0].sparepart.forEach((part)=> {
           sparepartitems.push(part.itemnum);
         });
       }
     }

     let itemDS = this.app.findDatasource("itemsDS");
     if (sparepartitems.length > 0){
       // Filter item datasource to only valid spare parts
       itemDS.setQBE("itemnum", "in", sparepartitems);
     } else {
       // Show empty list since none were found
       itemDS.setQBE("itemnum", "=", "ITEMNOTFOUND");
     }

     await itemDS.searchQBE();
     event.page.showDialog('materialLookup');
   }

   async changeSpareToggle(event){
     this.app.currentPage.state.addSparePart = event.target.checked;
   }

   async customOpenMaterialLookup(event){
     // Clear our QBE filter
     let itemDS = this.app.findDatasource("itemsDS");
     itemDS.clearQBE();
     await itemDS.searchQBE(undefined, true);
     event.page.showDialog('materialLookup');
   }
   ```

4. **Save** the file

---

### **Step 9: Preview and Test the Changes**

1. From the Application Configuration editor, click **Preview** in the action dropdown

2. A new tab will open with the Technician UI running on a preview port
3. **Test the functionality**:

   - Navigate to your approved work order

     ![Image](../images/mobile1.png)

     ![Image](../images/mobile2.png)

   - Click on the **Report Work** button

     ![Image](../images/mobile3.png)

   - Look for **Materials used** section
   - Click the **triple-dot menu** (⋮) next to "Materials used"

     ![Image](../images/mobile4.png)

   - Click **Add items**
   - **Observe the new toggle**: "Filter Spare Part" should appear at the top

     ![Image](../images/mobile5.png)

4. **Test Toggle OFF**:

   - Ensure toggle is set to **OFF** (No)
   - Click the **right arrow** for Material
   - You should see **all available materials**

     ![Image](../images/mobile6.png)

5. **Test Toggle ON**:

   - Go back and set the toggle to **ON** (Yes)
   - Click the **right arrow** for Material
   - You should see **only spare parts** for the selected asset
   - If no spare parts exist, the list will be empty

     ![Image](../images/mobile7.png)

---

### **Step 10: Publish the Application**

1. Return to the Application Configuration main page
2. Find your duplicated app in the list
3. Within your app, expand the drop down on the top right of the page
4. Select **Publish**
5. Wait for the publishing process to complete (monitor progress in console if available)
6. Once published, your changes will be available in the live MAS environment

   ![Image](../images/mobile8.png)

---

### **Step 11: Validate in Production Environment**

1. Navigate to **Work Orders** → **Role Based Applications** → **Technicians** (or your custom app name)
2. Open your test work order
3. Follow the same testing steps as in Step 9 to verify the toggle works in the live environment
4. If you have access to mobile devices, the same functionality will be available there

   ![Image](../images/mobile9.png)
   
---

## **Troubleshooting**

### **Common Issues**

- **Toggle doesn't appear**: Check that the `djpqr` box ID is correct in your environment
- **No spare parts shown**: Verify that spare parts are configured for your test asset
- **JavaScript errors**: Ensure all commas are properly placed in `AppCustomizations.js`
- **Preview not loading**: Clear browser cache and try again
- **Publish fails**: Check console logs for detailed error messages

### **Verification Steps**

- Ensure the asset in your work order has spare parts configured
- Verify the work order is approved and assigned to you
- Check that your duplicated app has "Enable mobile download" turned on
- Confirm all XML tags are properly closed and IDs are unique

---

## **Expected Behavior Summary**

- **Toggle OFF**: Shows all available materials when adding items to work order
- **Toggle ON**: Shows only spare parts associated with the work order's asset
- **No Asset**: Toggle is disabled (readonly)
- **No Spare Parts**: Empty list when toggle is ON

---

## **Conclusion**

You have successfully customized the Maximo Mobile Technician application to include a dynamic spare parts filter using MAS 9.1's built-in Application Configuration. This approach eliminates the need for Docker or external MAF tools—everything is managed through the modern MAS interface.

The customization demonstrates:

- XML configuration for UI elements
- JavaScript logic for dynamic filtering
- Integration with Maximo's datasource system
- Mobile-responsive design patterns

---

## **Next Steps**

- Explore other mobile customization possibilities
- Consider adding validation rules or additional filters
- Test the functionality on actual mobile devices
- Document your customizations for team knowledge sharing

[Previous](./06_more_health_views_and_mobile.md)
