# Simple Task Manager

A simple web application built with Python and Flask.

## About the Project

Simple Task Manager is a beginner-friendly Flask web application. It provides a home page and a health-check endpoint to verify that the application is running correctly.

## Technologies Used

- Python 3.12
- Flask
- Pytest
- Gunicorn
- GitHub Actions
- Render

## Project Structure

```text
simple-task-manager/
│
├── .github/
│   └── workflows/
│       └── python-ci.yml
│
├── app.py
├── test_app.py
├── requirements.txt
└── README.md
```

## Installation

1. Clone the repository:

```bash
git clone https://github.com/Burulai0406/simple-task-manager.git
```

2. Open the project directory:

```bash
cd simple-task-manager
```

3. Install dependencies:

```bash
pip install -r requirements.txt
```

## Run Locally

Start the Flask application:

```bash
python app.py
```

Open your browser:

http://127.0.0.1:5000/

## API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | Home page |
| GET | `/health` | Health check |

### Health Check Response

```json
{
  "status": "healthy"
}
```

## Run Tests

Run automated tests using pytest:

```bash
pytest -p no:cacheprovider -v
```

## Continuous Integration (CI)

GitHub Actions automatically runs tests when code is pushed to the `main` branch or when a pull request targets `main`.

The workflow:

1. Checks out the repository.
2. Sets up Python 3.12.
3. Installs dependencies.
4. Runs automated tests using pytest.

## Deployment

The application is deployed on Render.

Live application:

https://simple-task-manager-4sgd.onrender.com

Health endpoint:

https://simple-task-manager-4sgd.onrender.com/health

Automatic deployment is configured to deploy only after CI checks pass.

## Author

Burulai Mamatusmanova

GitHub: https://github.com/Burulai0406
