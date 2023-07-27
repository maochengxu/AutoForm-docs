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

To allow clean separation between the frontend and the backend, the Django backend is a REST API built with Django REST Framework (DRF). Please refer to its [documentation](https://www.django-rest-framework.org/) for more details. 

## Structure

The directory structure of the backend is clean:

- `backend/`: The root directory for the backend.
    - `backend/`: The Python package for the backend.
        - `collected_static/`: Contains the static files, including the admin system and the REST API.
        - `settings/`: Defines the settings of the backend.
            - `base.py`: The base settings.
            - `dev.py`: The development settings.
            - `prod.py`: The production settings. Must be kept secret.
    - `betterform/`: Defines the models and APIs using Django and DRF.
        - `migrations/`: Contains the migrations of the database.
        - `admin.py`: Defines the admin system.
        - `apps.py`: Defines the app.
        - `models.py`: Defines the models. The models are built with Django's ORM.
        - `serializers.py`: Defines the serializers. DRF uses serializers to serialize and deserialize the data.
        - `views.py`: Defines the APIs. The APIs are built with DRF's generic views.
        - `urls.py`: Defines the URLs of the APIs.
    - `createpdf/`: Utilizes Jinja and WeasyPrint to create PDF files.
        - `assets/`: Contains the assets for the PDF files.
            - `templates/`: Contains the HTML templates for the PDF files.
            - `tmp/`: The temporary directory for the PDF files.
        - `views.py`: Defines the APIs for creating PDF files.
        - `urls.py`: Defines the URLs of the APIs.
    - `monday/`: Handles the monday.com API to receive webhooks and initialize the quote process.
        - `mondayapi/`: Handles the monday.com API.
            - `MondayQuery.py`: A wrapper for the monday.com API.
            - `config.json`: The configuration file for the monday.com API. Must be kept secret.
        - `views.py`: Defines the APIs for receiving webhooks and updating Monday.com boards.
        - `urls.py`: Defines the URLs of the APIs.
    - `manage.py`: Django's command-line utility.
