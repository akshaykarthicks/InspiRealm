## 🚀 Deployment on Render.com

This project is configured for seamless deployment on [Render.com](https://render.com/). Below are the steps and details of all deployment-specific changes.

### 1. Deployment-Specific Files & Changes

- **`render.yaml`**  
  This file defines the infrastructure and services for Render deployment, including the web service, build and start commands, and environment variables.

- **`core/core/settings.py`**  
  - Ensure `ALLOWED_HOSTS` includes Render's domain.
  - Static files settings are configured for production.

- **Environment Variables**  
  - Set `DJANGO_SECRET_KEY`, `DEBUG`, and any other sensitive settings in Render's dashboard (not in code).

### 2. Step-by-Step Deployment Instructions

#### a. Connect Your Repository

1. Sign in to [Render.com](https://render.com/).
2. Click **"New Web Service"** and connect your GitHub/GitLab repository.

#### b. Configure the Service

- **Environment:** Python 3.x
- **Build Command:**  
  ```
  pip install -r requirements.txt
  python manage.py collectstatic --noinput
  python manage.py migrate
  ```
- **Start Command:**  
  ```
  gunicorn core.wsgi:application
  ```
- **Environment Variables:**  
  Add the following in the Render dashboard:
  - `DJANGO_SETTINGS_MODULE=core.settings`
  - `DJANGO_SECRET_KEY=your-secret-key`
  - `DEBUG=False`
  - Any other required variables

#### c. Static & Media Files

- Render automatically serves static files if configured in `settings.py`.
- Make sure `collectstatic` runs in the build command.

#### d. Post-Deployment

- After the first deploy, you may need to run migrations manually:
  ```
  python manage.py migrate
  ```
- Check logs in the Render dashboard for errors.

### 3. Summary of Deployment Changes

- Added `render.yaml` for Render infrastructure.
- Updated `settings.py` for production (ALLOWED_HOSTS, static files).
- Deployment commands and environment variables are set up for Render.
- No code changes required for local development.

---

**Your project is now ready for production deployment on Render.com!**  
If you need to update deployment settings, edit `render.yaml` or environment variables in the Render dashboard.
