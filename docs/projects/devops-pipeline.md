# ⚙️ DevOps Pipeline Automation for Documentation

This project demonstrates a **comprehensive DevOps pipeline** that automates the build, linting, deployment, and publication of technical documentation.  
It leverages **GitLab CI/CD**, **Python scripts**, and integrates seamlessly with **Fluid Topics** to streamline documentation workflows.

---

## 🚀 Pipeline Overview

The pipeline is defined in `.gitlab-ci.yml` and includes several automated stages:

- **Lint** – Ensures code and documentation quality using Markdown linters and custom Python scripts.  
- **Build** – Installs dependencies and generates the documentation site using **MkDocs**.  
- **Deploy** – Prepares the built site for deployment and manages artifacts.  
- **Deploy to Fluid Topics** – Automates packaging and upload of documentation to **staging** and **production** environments.  
- **Translation** – Handles build and deployment steps for multi-language documentation.

---

## 🔑 Key Features

- **Modular Pipeline** – Uses includes and templates for reusability across multiple projects.  
- **Secure Credentials** – Environment variables store sensitive information like API keys.  
- **Flexible Triggers** – Supports both manual and automatic deployments.  
- **Artifact Management** – Maintains documentation site and ZIP files for review and deployment.  
- **External Integration** – Smooth interaction with Fluid Topics for publishing and staging.

---

## 🧱 Pipeline Stages and Jobs

### 1. Linting
- **lint-markdown**: Runs a reusable Markdown linter image to verify documentation quality.  
- **fluid-topics-linter**: Executes a custom Python linter (`ft-linter.py`) on the `docs` directory to enforce style rules.

### 2. Build
- **build_mkdocs**: Installs dependencies via **Poetry** and builds the documentation with MkDocs.  
- **build_mkdocs_offline**: Generates an offline version of the documentation for distribution.

### 3. Deploy
- **.deploy_mkdocs**: Moves the built site to the `public/` directory for deployment.  
- **review_app**: Creates a temporary review environment for each branch.  
- **pages**: Publishes the documentation site as a GitLab Pages artifact.

### 4. Deploy to Fluid Topics
Jobs defined in `ci-publish-jobs.yml` handle automated uploads:  
- **ft-staging** – Packages and uploads documentation to the Fluid Topics staging environment.  
- **ft-public** – Packages and uploads to the production environment (triggered only on the main branch).

---

## 🧰 Key Automation Scripts

### `metadata.py`
- Appends metadata from `ft/metadata.yml` to `mkdocs.yml`.  
- Comments out special `!ENV` blocks for compatibility.  
- Ensures metadata is not duplicated across builds.

### `upload_staging.py` & `upload.py`
- Packages `mkdocs.yml` and the `docs/` directory into a ZIP archive.  
- Uses environment variables for API keys and user credentials.  
- Uploads the ZIP file securely to Fluid Topics.  
- Separate scripts manage **staging** and **production** endpoints.

#### Example: Upload Script (Staging)
```python
import os
import requests
import zipfile

zip_archive = 'S7-connector.zip'
file_to_zip = 'mkdocs.yml'
folder_to_zip = 'docs/'
api_key = os.getenv('FT_PUBS')


🔐 Security & Best Practices

Secrets and credentials are fully managed via environment variables.

Production uploads are restricted to the main branch only.

Artifacts are configured to expire automatically to conserve storage.

Pipeline is modular, secure, and repeatable.

🌟 Benefits

Fully Automated Lifecycle – Lint, build, deploy, and publish documentation without manual intervention.

Translation-Ready – Integrates with multi-language documentation workflows.

Secure and Auditable – Tracks deployments and protects sensitive credentials.

Repeatable and Scalable – Modular design allows easy adaptation for new projects or repositories.
