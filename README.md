# Sales Order Management System

This project is a **Sales Order Management** System designed using **SAP ABAP** with a **module pool program** and **Report/ALV Program**. The project includes two main components:

- [ ] **Sales Order Document Creation:** Allows users to create sales orders with relevant header and item details.
- [ ] **Sales Order Register:** Displays sales order data in an interactive ALV report, fetched from custom Z tables, based on input parameters.

The project uses **BAPI** Function Module (**BAPI_SALESORDER_CREATEFROMDAT2**) for the creation of sales orders and handles both the header and item details efficiently.

---

## Table of Contents

- Project Description
- Features
- Technologies Used
- Module Pool Program Overview
   - Screen 100 (Header Details)
   - Screen 200 (Item Details)
- BAPI Integration
- Sales Order Register
- Validation Logic
- Database Design
- Custom Tables
- Table Relationships
- License

---

## Project Description

The **Sales Order Management System** enables users to create and maintain sales order data in a user-friendly and interactive manner. The project is developed using a **module pool program** (also called a dialog program) in SAP ABAP. The program consists of two main screens:

- **Screen 100** for entering header details (Sales Order Type, Sales Organization, Distribution Channel, and Division).
- **Screen 200** for entering item details such as Material, Quantity, Price, and more.

The project also features a **Sales Order Register**, which displays sales order data from custom tables in the form of an **interactive ALV report**.

---

## Features

- **Sales Order Creation:** User-friendly interface for creating sales orders using a dialog program.
- **BAPI Integration:** Uses the BAPI function `BAPI_SALESORDER_CREATEFROMDAT2` for the actual creation of sales orders.
- **Interactive ALV Report:** Displays the sales order data in a dynamic and interactive ALV report, allowing for easy viewing and filtering of records.
- **Custom Z Tables:** Data is stored and fetched from custom Z tables (`Z_VBAK`, `Z_VBAP`, `Z_VBPA`, `Z_KONV`) to manage the sales order details.
- **Row-Level Validation:** Ensures that no duplicate rows are entered in the item table for sales orders, maintaining data integrity.
- **Modular Design:** The project follows a modular design approach with separate screens for header and item details.

---

## Technologies Used

- **SAP ABAP**
- **Module Pool Programming (Dialog Programming)**
- **ALV (ABAP List Viewer)**
- **BAPI (Business Application Programming Interface)**
- **Custom Z Tables**
- **SAP Standard Table of Sales & Distribution**

---

## Module Pool Program Overview

### Screen 100 (Header Details)
- **Fields:**
   - Sales Order Type (`AUART`)
   - Sales Organization (`VKORG`)
   - Distribution Channel (`VTWEG`)
   - Division (`SPART`)

   This screen is designed to collect the necessary header information required for the creation of a sales order. The user provides input for these fields, and upon pressing the Enter button, they are navigated to the second screen.

### Screen 200 (Item Details)

- **Displayed Fields:**
   - Sales Order No (`VBELN`)
   - Sales Order Type (`AUART`)
   - Sales Order Date (`ERDAT`)
   - Purchase Order (`BSTDK`)
   - Customer Code (`KUNNR`)
   - Customer Name (`NAME1`)
   - Customer Reference (`BSTKD`)
   - Total Amount (`NETWR`)

- **Input Fields in Table Control:**
   - Item No (`POSNR`)
   - Material (`MATNR`)
   - Material Description (`MAKTX`)
   - Plant (`WERKS`)
   - Storage Location (`LGORT`)
   - Quantity (`KWMENG`)
   - Price (`KBETR`)
   - Discount (`Discount`)
   - Net Value (`NETWR`)

   The second screen shows the header fields in display mode while allowing the user to input item-level data. A **Table Control** is used to input multiple line items for the sales order.

--- 

## BAPI Integration

For creating the sales order, the project uses the **BAPI_SALESORDER_CREATEFROMDAT2** function module. The BAPI is integrated into the backend logic of the module pool program and is triggered once the user completes the input for both header and item details.

**Steps:**
- Header data from Screen 100 is passed to the BAPI.
- Item data from Screen 200 (entered via Table Control) is passed to the BAPI.
- The BAPI creates the sales order and returns the sales order number (`VBELN`), which is then displayed on the second screen.

---

## Sales Order Register

The **Sales Order Register** is a separate program that fetches and displays sales order data from custom tables (`Z_VBAK`, `Z_VBAP`, `Z_VBPA`, `Z_KONV`). The report is presented in an interactive ALV format, allowing users to filter and sort the data.

- **Input Parameters:**
   - Sales Organization (`VKORG`)
   - Order Date (`ERDAT`)
   - Distribution Channel (`VTWEG`)
   - Division (`SPART`)
   - Sales Order No (`VBELN`)

   The ALV report is built using the data fetched from the custom tables and provides detailed information about the sales orders.

--- 

## Validation Logic

A key feature of the project is the validation applied in the Table Control on Screen 200. The validation ensures that no duplicate rows (with the same combination of Material, Plant, Quantity, etc.) are entered. This check is performed during the **PAI** (**Process After Input**) event.

- **Logic:**
   - Loop through each row of the Table Control.
   - Compare the values of all fields in each row with other rows.
   - If a duplicate is found, display an error message and prevent the user from saving the sales order.

---

## Database Design

### Custom Tables

The data for sales orders is stored in custom Z tables:

- `Z_VBAK` (Sales Order Header Data)
- `Z_VBAP` (Sales Order Item Data)
- `Z_VBPA` (Partner Data)
- `Z_KONV` (Conditions Data)

### Table Relationships

The tables are linked using the sales order number (`VBELN`) as the primary key. The header and item tables (`Z_VBAK` and `Z_VBAP`) have a one-to-many relationship, where each header can have multiple items.

---

## License

This project is licensed under the **MIT** License.

---

