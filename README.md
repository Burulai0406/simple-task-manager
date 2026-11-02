# Part 10. Application Deployment to a PaaS Platform

## 1. Introduction

The goal of this task was to deploy a web application to a Platform as a Service (PaaS) provider and configure automatic deployment with CI protection.

For this assignment, I selected **Render** as the PaaS platform and deployed my Python Flask application, Simple Task Manager.

The main objectives were:

- Deploy the application to a public HTTPS URL.
- Make sure the `/health` endpoint works correctly.
- Configure automatic deployment after pushing changes to the `main` branch.
- Ensure that deployment happens only when Continuous Integration (CI) checks pass.
- Test the configuration using a commit with a failing test and verify that it is not deployed.

## 2. Project Information

**Project name:** Simple Task Manager

**Programming language:** Python 3.12

**Framework:** Flask

**Testing framework:** Pytest

**Production server:** Gunicorn

**Source code repository:**

https://github.com/Burulai0406/simple-task-manager

**Deployment platform:** Render

**Live application:**

https://simple-task-manager-4sgd.onrender.com

## 3. Application Deployment

I deployed my Flask application to Render.

The application has two main endpoints:

- `GET /` — displays the home page.
- `GET /health` — checks whether the application is running correctly.

The application is publicly accessible through HTTPS.

### Home Page

URL:

https://simple-task-manager-4sgd.onrender.com/

Expected response:

```text
Welcome to Simple Task Manager!
```

### Health Check

URL:

https://simple-task-manager-4sgd.onrender.com/health

Expected JSON response:

```json
{
  "status": "healthy"
}
```

Both endpoints were successfully tested in a web browser.

## 4. Continuous Integration (CI)

I configured GitHub Actions to automatically run tests whenever code is pushed to the `main` branch or when a pull request targets the `main` branch.

The workflow is defined in:

`.github/workflows/python-ci.yml`

The CI pipeline performs the following steps:

1. Checks out the repository.
2. Sets up Python 3.12.
3. Installs project dependencies from `requirements.txt`.
4. Runs automated tests using Pytest.

The test command is:

```bash
pytest -p no:cacheprovider -v
```

The project contains two main tests:

- `test_home()` checks the home page response.
- `test_health()` checks the health endpoint response.

If all tests pass, the GitHub Actions workflow finishes successfully. If a test fails, the workflow reports a failure.

## 5. Automatic Deployment Configuration

I configured automatic deployment in the Render dashboard.

The configuration is located at:

**Render Dashboard → Service Settings → Build & Deploy → Auto-Deploy**

I selected the following option:

**After CI Checks Pass**

This setting ensures that Render waits for the CI checks to complete successfully before starting a new deployment.

The expected behavior is:

- If CI checks pass, Render automatically deploys the new commit.
- If CI checks fail, Render does not deploy that commit.

I found this configuration in the official Render documentation:

https://render.com/docs/deploys

## 6. Testing CI Deployment Protection

To verify that the configuration works correctly, I used a commit containing a failing test.

### 6.1. Failed Test Commit

Commit:

`15653e96fe4866b28c5fd9326d62312eae2a58fd`

Short commit hash:

`15653e9`

GitHub Actions workflow:

https://github.com/Burulai0406/simple-task-manager/actions/runs/41005861270

Result:

**Failure**

The workflow failed because the automated tests did not pass. The process finished with exit code 2.

This demonstrated that the CI pipeline correctly detected the failing test.

### 6.2. Successful Test Commit

After the test failure, I used a corrected version of the tests.

Commit:

`eb275e84c7cfc47fae9ca6e63a262037d2eea3bf`

Short commit hash:

`eb275e8`

GitHub Actions workflow:

https://github.com/Burulai0406/simple-task-manager/actions/runs/41006435739

Result:

**Success**

All tests passed successfully.

### 6.3. Deployment Verification

I checked the deployment history in the Render dashboard and compared it with the GitHub Actions workflow history.

The failed commits `15653e9` and `33eb05c` were not present in the displayed Render deployment history.

The successful commits were deployed:

- `eb275e8` — Fix test indentation.
- `473d166` — Create README.md.
- `bf024b5` — Update README.md.

This comparison demonstrated the expected CI-protected deployment behavior: successful commits were deployed, while the failed commits were not deployed.

## 7. Final Result

All main requirements of the assignment were completed:

1. The application was deployed to Render.
2. The application is publicly accessible through HTTPS.
3. The `/health` endpoint returns the expected healthy status.
4. GitHub Actions automatically runs tests after pushes to `main`.
5. Render Auto-Deploy was configured using the **After CI Checks Pass** option.
6. A failing test commit was used to verify CI failure.
7. Successful commits were automatically deployed.

## 8. Conclusion

During this assignment, I learned how to deploy a Python Flask application to a PaaS platform using Render.

I also learned how to configure a Continuous Integration pipeline with GitHub Actions and connect it to automatic deployment.

The most important part of this task was configuring deployment protection. By selecting **After CI Checks Pass**, I configured Render to wait for successful CI checks before deploying new changes.

This assignment helped me understand the relationship between GitHub, GitHub Actions, CI pipelines, and PaaS deployment.

**Project repository:**  
https://github.com/Burulai0406/simple-task-manager

**Live application:**  
https://simple-task-manager-4sgd.onrender.com
