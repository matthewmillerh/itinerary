# Itinerary Project

This project is a web application built with Vue 3 and Vite, designed to help users create and manage itineraries. It leverages Mapbox GL JS for interactive map displays and communicates with a MySQL database.

## Key Features

* Interactive map integration using Mapbox GL JS.
* Itinerary creation and management.
* Data storage and retrieval with MySQL.
* Modern and responsive user interface built with Vue 3 and Tailwind CSS.

## Technologies Used

* Vue 3
* Vue Router
* Vite
* Tailwind CSS

## Prerequisites

* Node.js and npm installed

## Installation

1.  Clone the repository.
2.  Install dependencies:

    ```sh
    npm install
    ```

## Development

###   Compile and Hot-Reload for Development

```sh
npm run dev
This will start the development server with hot-reloading.

Compile and Minify for Production
Bash

npm run build
This will create a production-ready build of the application.

Configuration
jsconfig.json: Configures path aliases for easier imports (e.g., @/* for ./src/*).
postcss.config.js: Configures PostCSS plugins, including Tailwind CSS and Autoprefixer.
tailwind.config.js: Configures Tailwind CSS settings.
vite.config.js: Configures Vite build options and aliases.

Additional Notes
Font Awesome is used for icons (included via CDN in index.html).