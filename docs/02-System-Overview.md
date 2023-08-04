---
layout: default
title: System Overview
nav_order: 3
---

# System Overview

## Automations

The automations integrated into the system primarily focus on streamlining the generation of Deals (Quotes), marking the commencement of the sales process. Initially, quote creation was a tedious task managed on a Monday.com board, where the process was triggered via a button leading to a Monday.com App. This design, however, stored all information and intermediate variables directly on the board, complicating the process of navigation and access to crucial information.

The current system initiates when the user creates a new item on the designated board. This action triggers a webhook that sends a new record to the system database automatically. Subsequently, a link to the form specific to the newly created item is posted on the Monday.com board, granting users direct access to the form through this link. Notably, the system uses the Monday ID to uniquely identify items in accordance with its design.

To enhance clarity and improve efficiency, the system incorporates the following automations:

### 1. Form Design

- The creation date is defaulted to "today".
- New contacts or products can be directly added via the form, prompting updates in both the database and the corresponding Monday.com board.
- Detailed information for each quote is automatically displayed upon opening the form for modification.
- Prices for kits are auto-filled during product input.
- Calculations are displayed in real-time as the form is being populated, including:
  - Expiry date
  - Item-wise subtotal price
  - Quote subtotal price
  - Post-discount price
  - Tax value
  - Total quote price
- Existing contact information is auto-populated upon selection.
- The backend database automatically updates upon form submission.

### 2. Interaction with Monday.com

- When a new item is created on the dedicated board, a webhook is sent from Monday.com, leading to the creation of a corresponding record in the database.
- After the backend creation of the new item, a link to the form is sent to the dedicated board.
- If a contact's detailed information undergoes changes, both the backend and Monday.com are updated accordingly.
- Upon form submission, a PDF file is automatically generated and uploaded to the Monday.com board.
- The Monday.com boards are updated automatically when the form is submitted.

## Backend

The backend is built using Django and Django REST Framework. This part of the system is responsible for defining models, APIs, handling webhooks, and generating PDFs. Data is stored in a MariaDB database. The backend has the following structure:

- `backend/`: The root directory for the backend.
    - `backend/`: The Python package for the backend.
    - `betterform/`: Defines the models and APIs using Django and Django REST Framework.
    - `createpdf/`: Utilizes Jinja and WeasyPrint to create PDF files.
    - `monday/`: Handles the monday.com API to receive webhooks and initialize the quote process.

## Frontend

The frontend is built using Vue.js with TypeScript and the Ant Design Vue UI library. It primarily contains form components for the quote creation process. The frontend has the following structure:

- `frontend/`: The root directory for the frontend.
    - `src/`: Contains the source files for the Vue.js application.
        - `components/`: Contains the Vue.js components used in the application, which include:
            - `ModalForms/`: Contains the modal form components used in the quote form to create new contact or product.
                - `ContactModal.vue`: The modal form component for creating contacts.
                - `ProductModal.vue`: The modal form component for creating products.
            - `QuoteForm.vue`: The form component for creating quotes.
            - `InvoiceForm.vue`: The form component for creating invoices.
            - `ContactForm.vue`: The form component for managing contact information.
            - `ProductForm.vue`: The form component for managing product information.

The system is designed such that the backend and frontend work together to provide a seamless user experience. The backend handles all data management and processing tasks, while the frontend provides a user-friendly interface for data entry and display.

Please refer to the corresponding backend and frontend documentation sections for more detailed information.