# Django + Tailwind CSS Setup Guide

This guide explains how to set up Tailwind CSS and Flowbite in this Django project.

## 1. Initial Setup

The project starts with two key files:
- **`package.json`**: Contains the configuration for Tailwind CSS, Flowbite, and build scripts.
- **`static/css/input.css`**: The base configuration file for your CSS.

> [!IMPORTANT]
> **Path Consistency Warning**
> In `package.json`, ensure that the paths to `input.css` and `output.css` exactly match your project structure.
> If your static files are in a different location, you **MUST** update the paths in the `scripts` section of `package.json`.
>
> Example from `package.json`:
> ```json
> "dev": "tailwindcss -i ./static/css/input.css -o ./static/css/output.css --watch --minify"
> ```
> If these paths are incorrect, Tailwind will not generate your CSS.

## 2. Understanding `package.json`

The `package.json` file is the heart of the frontend configuration. Here's what's inside:

### Scripts
- **`start`**: Runs `npm run dev`.
- **`build`**: Cleans the old output and builds the production CSS.
- **`build:clean`**: Uses `rimraf` to delete the existing `output.css` to ensure a fresh build.
- **`build:tailwind`**: Compiles `input.css` into `output.css` and minifies it for production.
- **`dev`**: The main development command. It watches `input.css` and your template files for changes and rebuilds `output.css` in real-time.

### Dependencies
- **`tailwindcss`**: The utility-first CSS framework.
- **`flowbite`**: A component library built on top of Tailwind CSS.
- **`@tailwindcss/cli`**: The command-line interface for running Tailwind.
- **`rimraf`**: A cross-platform tool to delete files (used for cleaning builds).

## 3. Django Configuration

1.  **Create Static Directory**: Ensure a `static` directory exists in your project root.
2.  **Register in Settings**: In `settings.py`, configure the static files directories:
    ```python
    STATIC_URL = 'static/'
    STATICFILES_DIRS = [BASE_DIR / 'static']
    ```

## 4. CSS Configuration (`input.css`)

The `static/css/input.css` file is where you configure your base styles, including:
- Primary colors
- Text sizes
- Breakpoints
- Custom utilities

Paste your base configuration into this file. It serves as the source for generating the final CSS.

## 5. Git Configuration

Create a `.gitignore` file and add the following to exclude generated files and dependencies:
```
node_modules/
static/css/output.css
venv/
__pycache__/
*.pyc
db.sqlite3
.DS_Store
.env
```

## 6. Installation

Install the Node.js dependencies (Tailwind CSS and Flowbite) by running:

```bash
npm install
```

## 7. Development

To start the development process and watch for changes:

```bash
npm run dev
```

This command will:
1.  Watch `input.css` and your template files.
2.  Automatically generate `static/css/output.css`.

## 8. Usage

Your Django templates should link to the **generated** CSS file, not the input file:

```html
{% load static %}
<link href="{% static 'css/output.css' %}" rel="stylesheet">
```

The project reads the compiled styles from `output.css`.
