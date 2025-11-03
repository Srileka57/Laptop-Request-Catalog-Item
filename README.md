# Laptop-Request-Catalog-Item
🖥️ ServiceNow Project: Laptop Request Catalog Item
📘 Project Overview

The Laptop Request Catalog Item project automates the process of requesting laptops within an organization using ServiceNow’s Service Catalog module.
This replaces the existing manual process, which was time-consuming and error-prone, with an automated, dynamic, and user-friendly catalog item.

The project ensures accurate data collection, reduces delays, and provides a clear, guided experience for employees requesting laptops.

🎯 Objective

To create a Service Catalog Item that allows employees to request laptops efficiently, with:

Dynamic form fields

Validation and visibility logic

Form reset functionality

Proper governance and migration support through Update Sets

🧩 Modules Used

Service Catalog (Catalog Definitions, Maintain Items, Variables)

Catalog UI Policies

UI Actions

System Update Sets

⚙️ Project Steps
🔹 1. Create a Local Update Set

Navigate to All → Update Sets → Local Update Sets

Click New

Enter:

Name: Laptop Request

Click Submit and Make Current

Perform all further configurations under this update set

🔹 2. Create Service Catalog Item

Navigate to All → Service Catalog → Catalog Definitions → Maintain Items

Click New and fill the details:

Name: Laptop Request

Catalog: Service Catalog

Category: Hardware

Short Description: Use this item to request a new laptop

Click Save

🔹 3. Add Variables

Add variables under the Variables related list of the catalog item:

Order	Variable Name	Type	Internal Name	Description
100	Laptop Model	Single Line Text	laptop_model	Enter laptop model
200	Justification	Multi Line Text	justification	Reason for laptop request
300	Additional Accessories	Checkbox	additional_accessories	Check if accessories are needed
400	Accessories Details	Multi Line Text	accessories_details	Enter accessory details

✅ These variables capture user inputs dynamically.

🔹 4. Create Catalog UI Policy

Go to Service Catalog → Catalog Definitions → Maintain Items

Open Laptop Request

Scroll to Catalog UI Policies → click New

Short Description: Show Accessories Details

Condition: additional_accessories is true

Click Save

Then create a UI Policy Action:

Variable Name: accessories_details

Mandatory: True

Visible: True

Order: 100

✅ This makes the Accessories Details field visible and mandatory when “Additional Accessories” is checked.

🔹 5. Create a UI Action (Reset Form)

Navigate to All → System Definition → UI Actions

Click New

Enter the following:

Table: sc_cart

Order: 100

Action Name: Reset Form

Client: ✅ Checked

Add the script:

function resetForm() {
    g_form.clearForm(); // Clears all fields in the form
    alert("The form has been reset.");
}


Click Save

✅ This adds a Reset Form button that clears all fields instantly.

🔹 6. Exporting Update Set

Navigate to All → Update Sets → Local Update Sets

Open the Laptop Request update set

Set State: Complete

In the Updates tab, verify all included changes

Click Export to XML to download the update set

🔹 7. Importing Update Set into Another Instance

Open another instance (in Incognito)

Go to All → Update Sets → Retrieved Update Sets

Click Import Update Set from XML

Upload the exported XML file

Open the imported update set (Laptop Request Project)

Click Preview Update Set → Commit Update Set

Verify the related updates after commit

✅ All changes are now available in the new instance.

🔹 8. Testing the Catalog Item

Go to Service Catalog → Catalog → Hardware

Open Laptop Request

Verify the following:

Three fields appear initially: Laptop Model, Justification, Additional Accessories

When Additional Accessories is checked → Accessories Details appears and becomes mandatory

Clicking Reset Form clears all fields

✅ The dynamic behavior and validations work as expected.

🧪 Output / Result

Dynamic field visibility implemented successfully

UI Policy and UI Action work as intended

Update Set exported and imported correctly

Catalog item functions properly in the target instance

🏁 Conclusion

The Laptop Request Catalog Item successfully streamlines the laptop request process in ServiceNow.
This project demonstrates:

Use of Service Catalog for request automation

Implementation of dynamic UI behavior using policies and actions

Configuration migration via Update Sets

Enhanced user experience and data accuracy

Through this project, the manual and error-prone process is replaced with a smart, automated, and efficient workflow, improving both IT service delivery and employee satisfaction.
