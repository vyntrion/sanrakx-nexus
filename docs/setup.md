# Development Setup

## Prerequisites

-   Python 3.11+
-   Node.js LTS and npm
-   Git
-   A code editor

Check versions:

``` bash
python --version
node --version
npm --version
git --version
```

## Backend setup

From the repository root:

### Windows PowerShell

``` powershell
cd backend
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

If the environment is not created yet, install the initial packages:

``` powershell
python -m pip install fastapi "uvicorn[standard]" requests feedparser pytest
python -m pip freeze > requirements.txt
```

### Linux

``` bash
cd backend
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

Run from `backend/` once `app/main.py` exists:

``` bash
python -m uvicorn app.main:app --reload
```

Open `http://127.0.0.1:8000/docs` for interactive API documentation.

## Frontend setup

From the repository root:

``` bash
npm create vite@latest frontend -- --template react
cd frontend
npm install
npm install recharts
npm run dev
```

Install and configure Tailwind CSS using the official instructions for
the version selected by the project. Configure the frontend API base URL
and backend CORS origin.

## Environment

Copy `.env.example` to `.env` only if the implemented settings loader
supports it. Never commit `.env`.

## First verification

-   Backend health endpoint returns healthy.
-   `/docs` loads.
-   Frontend development server starts.
-   A synthetic event can be validated and stored.
-   A detection rule creates an alert with evidence.
-   The alert remains after a backend restart.

## Troubleshooting

-   **Python command not found:** install Python and ensure it is on
    PATH.
-   **Activation blocked in PowerShell:** use Command Prompt activation
    or follow your organization's approved shell policy.
-   **Port occupied:** choose another local port and update frontend
    configuration.
-   **CORS error:** set the exact local frontend origin in backend
    configuration.
-   **NVD request fails:** inspect status code, timeout, API quota, and
    source availability; preserve cached records.
