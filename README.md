# Deployment Using CI/CD Pipeline

A hands-on demonstration of a modern CI/CD pipeline using **GitHub Actions** and Python.

The project demonstrates how a software change can move from source control through automated validation and, as the project evolves, toward automated deployment.

## Project Objective

The objective of this project is to demonstrate practical understanding of modern software delivery and CI/CD practices, including:

- Source control with Git and GitHub
- Continuous Integration (CI)
- Automated testing
- GitHub Actions workflows
- Dependency management
- Automated build and validation
- Containerization with Docker
- Deployment automation
- Environment management
- Security and quality checks
- Deployment governance and rollback strategies

## Current Implementation

The current version implements the **Continuous Integration (CI)** portion of the pipeline.

Whenever code is pushed to the `main` branch or a pull request targets `main`, GitHub Actions automatically:

1. Checks out the source code
2. Sets up the Python environment
3. Installs project dependencies
4. Runs automated tests
5. Reports the pipeline result

### Current CI Flow

```text
Developer
    |
    v
GitHub Repository
    |
    v
GitHub Actions
    |
    +--> Checkout Code
    |
    +--> Setup Python
    |
    +--> Install Dependencies
    |
    +--> Run Automated Tests
    |
    v
Success / Failure
