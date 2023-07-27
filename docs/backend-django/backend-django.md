---
layout: default
title: Backend (Django)
nav_order: 4
has_children: true
---

# Backend

## Overview

The backend of the system is built with Python. Using Django, the backend provides necessary APIs for manipulating the database and creating the PDF file.

The design of the backend follows the Model, View & Template (MVT) pattern, the model deals with the database, the view deals with business logic, and the template deals with the pages.

To allow clean separation between the frontend and the backend, the Django backend is a REST API built with Django REST Framework. Please refer to its [documentation](https://www.django-rest-framework.org/) for more details. 

## Structure

The directory structure of the backend is clean:

- `backend/`: The root directory for the backend.
    - `backend/`: The Python package for the backend.
        - `collected_static/`: Contains the static files, including the admin system and the REST API.
        - `settings/`: Defines the settings of the backend.
    - `betterform/`: Defines the models and APIs using Django and Django REST Framework.
    - `createpdf/`: Utilizes Jinja and WeasyPrint to create PDF files.
    - `monday/`: Handles the monday.com API to receive webhooks and initialize the quote process.
    - `manage.py`: Django's command-line utility.
