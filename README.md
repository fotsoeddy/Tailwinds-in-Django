# Django + Tailwind CSS Setup Guide

This guide explains how to set up Tailwind CSS and Flowbite in this Django project.

## 1. Initial Setup

The project starts with two key files:
- **`package.json`**: Contains the configuration for Tailwind CSS, Flowbite, and build scripts.
- **`static/css/input.css`**: The base configuration file for your CSS.

## 2. Django Configuration

1.  **Create Static Directory**: Ensure a `static` directory exists in your project root.
2.  **Register in Settings**: In `settings.py`, configure the static files directories:
    ```python
    STATIC_URL = 'static/'
    STATICFILES_DIRS = [BASE_DIR / 'static']
    ```

## 3. CSS Configuration (`input.css`)

The `static/css/input.css` file is where you configure your base styles, including:
- Primary colors
- Text sizes
- Breakpoints
- Custom utilities

Paste your base configuration into this file. It serves as the source for generating the final CSS.

## 4. Git Configuration

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

## 5. Installation

Install the Node.js dependencies (Tailwind CSS and Flowbite) by running:

```bash
npm install
```

## 6. Development

To start the development process and watch for changes:

```bash
npm run dev
```

This command will:
1.  Watch `input.css` and your template files.
2.  Automatically generate `static/css/output.css`.

## 7. Usage

Your Django templates should link to the **generated** CSS file, not the input file:

```html
{% load static %}
<link href="{% static 'css/output.css' %}" rel="stylesheet">
```

The project reads the compiled styles from `output.css`.
