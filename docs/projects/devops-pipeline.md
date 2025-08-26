# DevOps Pipeline Automation

This project demonstrates a comprehensive DevOps pipeline for automating the build, linting, deployment, and publication of technical documentation using GitLab CI/CD, Python scripts, and integration with Fluid Topics.

## Pipeline Overview

The pipeline is defined in `.gitlab-ci.yml` and consists of several stages:

- **Lint**: Ensures code and documentation quality using markdown linters and custom Python linters.
- **Build**: Installs dependencies and builds the documentation site using MkDocs.
- **Deploy**: Publishes the built site as artifacts and prepares it for deployment.
- **Deploy to Fluid Topics**: Automates the packaging and upload of documentation to Fluid Topics for both staging and production environments.
- **Translation**: Handles translation-related build and deployment steps.

### Key Features

- Modular pipeline using includes and templates for reusability.
- Environment variables for secure credentials and configuration.
- Manual and automatic deployment triggers.
- Artifact management for site and ZIP files.
- Integration with external documentation platforms (Fluid Topics).

### Pipeline Stages and Jobs

#### 1. Linting

- **lint-markdown**: Uses a reusable markdown linter image to check documentation quality.
- **fluid-topics-linter**: Runs a custom Python linter (`ft-linter.py`) on the `docs` directory.

#### 2. Build

- **build_mkdocs**: Installs dependencies with Poetry and builds the documentation using MkDocs.
- **build_mkdocs_offline**: Builds an offline version of the documentation.

#### 3. Deploy

- **.deploy_mkdocs**: Moves the built site to a `public/` directory for deployment.
- **review_app**: Creates a review environment for each branch.
- **pages**: Publishes the documentation site as a GitLab Pages artifact.

#### 4. Deploy to Fluid Topics

Jobs in `ci-publish-jobs.yml` automate the upload of documentation to Fluid Topics:

- **ft-staging**: Packages the documentation and uploads it to the Fluid Topics staging environment.
- **ft-public**: Packages and uploads to the production environment (runs only on the main branch).

### Key Automation Scripts

#### metadata.py

- Appends metadata from `ft/metadata.yml` to `mkdocs.yml`.
- Comments out special `!ENV` blocks for compatibility.
- Ensures metadata is not duplicated.

#### upload_staging.py & upload.py

- Package the documentation (`mkdocs.yml` and `docs/`) into a ZIP archive.
- Use environment variables for API keys and user info.
- Upload the ZIP to Fluid Topics via a secure API.
- Separate scripts for staging and production endpoints.

### Example: Upload Script (Staging)

```python
import os
import requests
import zipfile

zip_archive = 'S7-connector.zip'
file_to_zip = 'mkdocs.yml'
folder_to_zip = 'docs/'
api_key = os.getenv('FT_PUBS')
# ... (rest of the script)
```

### Security and Best Practices

- All secrets and credentials are managed via environment variables.
- Only the main branch can trigger production uploads.
- Artifacts are set to expire to save storage.

### Benefits

- Fully automated documentation lifecycle: lint, build, deploy, and publish.
- Easy integration with translation and review workflows.
- Secure, repeatable, and auditable process.
