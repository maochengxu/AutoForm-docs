---
layout: default
title: Frontend (Vue3)
nav_order: 5
---

# Frontend

## Overview

The frontend is built using [Vue.js](https://vuejs.org/) with TypeScript and the [Ant Design Vue](https://antdv.com/docs/vue/introduce) UI library. It primarily contains form components for the quote creation process.

The forms are written in the Single-File Components (SFC) format using [Composition API](https://vuejs.org/guide/extras/composition-api-faq.html#what-is-composition-api) (Vue3). The building of the frontend is relied on [Vite](https://vitejs.dev/).

## Structure

Let's look at the directory structure of the frontend:

- `frontend/`: The root directory for the frontend.
    - `dist/`: Contains the built files for the frontend.
    - `public/`: Contains the static files for the frontend.
    - `src/`: Contains the source files for the Vue.js application.
        - `components/`: Contains the Vue.js components used in the application, which include:
            - `QuoteForm.vue`: The form component for creating quotes.
            - `InvoiceForm.vue`: The form component for creating invoices.
            - `ContactForm.vue`: The form component for managing contact information.
            - `ProductForm.vue`: The form component for managing product information.
        - `App.vue`: The root component of the Vue.js application.
        - `main.ts`: The entry point of the Vue.js application.
        - `router.ts`: The router of the Vue.js application.
        - `types.ts`: The type definitions for the Vue.js application.
    - `.env.development`: Contains the environment variables for development.
    - `.env.production`: Contains the environment variables for production.


## Routing

The frontend uses the [Vue Router](https://router.vuejs.org/) to manage the routing of the application. The routes are defined in `src/router.ts`:

```typescript
const routes = [
    {
        path: '/form/:id',
        name: 'form',
        component: QuoteForm
    },
    ... // Other routes
];
```

## Communicating with backend

The frontend communicates with the backend using the [axios](https://axios-http.com/) library. The data are passed using the JSON format. The API base URL is defined in the `.env` file:

```
VITE_APP_API_BASE_URL=http://127.0.0.1:8000
VITE_APP_FORM_BASE_URL=http://localhost:5173
```

{: .note}
Always remember to add the .env file before building the frontend project.

## Security

Django has a built-in security feature that prevents cross-site request forgery (CSRF). To use this feature, the frontend needs to send a CSRF token to the backend. The token is stored in the cookie of the frontend when a GET request is made for the first time. The backend will check the token in the cookie and the token in the request header. If they are the same, the request will be accepted.

However, in our system the backend is just an API and the frontend may not send a GET request to the backend, so the cookie does not have the CSRF token. To solve this problem, we need to add the CSRF token to the request header manually. We need to request the CSRF token from the backend and add it to the request header of the frontend. The following code shows how to do this:

```typescript
import axios from 'axios';

// Get the CSRF token from the backend
const csrfToken = await axios.get('/api/csrf/');

// Add the CSRF token to the POST request header
axios.defaults.headers.post['X-CSRFToken'] = csrfToken.data.csrfToken;
```
