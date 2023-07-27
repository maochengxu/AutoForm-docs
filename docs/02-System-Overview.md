---
layout: default
title: System Overview
nav_order: 3
---

# System Overview

The Augmented Quote Management System is primarily divided into two major parts: the backend and the frontend.

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
            - `QuoteForm`: The form component for creating quotes.
            - `InvoiceForm`: The form component for creating invoices.
            - `ContactForm`: The form component for managing contact information.
            - `ProductForm`: The form component for managing product information.

The system is designed such that the backend and frontend work together to provide a seamless user experience. The backend handles all data management and processing tasks, while the frontend provides a user-friendly interface for data entry and display.

Please refer to the corresponding backend and frontend documentation sections for more detailed information.
