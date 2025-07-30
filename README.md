# My Jenkins Templates

A collection of Jenkinsfile templates for CI/CD automation of various project types. All templates are fully parameterized and designed to work with Jenkins running on HTTPS with unique tokens for each job.

## 📋 Available Templates

### 1. 🐳 Docker Container (`docker-container/`)

Template for building a single Docker container from a GitHub repository.

**Parameters:**

-   `CONT_NAME` - Container name (required)
-   `GITHUB_REPO_URL` - GitHub repository URL (required)

**Stages:**

-   ✅ Parameter validation
-   📁 Project directory creation
-   📥 Repository cloning
-   🔒 Security scan with Snyk
-   🏗️ Docker image building

### 2. 🐳🐳 Docker Multi-Containers (`docker-multi-containers/`)

Template for running multi-container applications with docker-compose.

**Parameters:**

-   `CONT_NAME` - Container name (required)
-   `GITHUB_REPO_URL` - GitHub repository URL (required)

**Stages:**

-   ✅ Parameter validation
-   📁 Project directory creation
-   📥 Repository cloning
-   🔒 Security scan with Snyk
-   📖 Reading configuration from docker-compose.yml
-   🔍 Software version check
-   🚀 Docker containers deployment
-   🛡️ OWASP ZAP security scan
-   🧹 Cleanup of unused Docker images

### 3. ⚛️ Docker Next.js (`docker-next/`)

Template specifically designed for Next.js applications in Docker containers.

**Parameters:**

-   `CONT_NAME` - Container name (required)
-   `GITHUB_REPO_URL` - GitHub repository URL (required)

**Stages:**

-   ✅ Parameter validation
-   📁 Project directory creation
-   📥 Repository cloning
-   🔒 Security scan with Snyk
-   🔍 Software version check
-   🚀 Docker containers deployment
-   🧹 Cleanup of unused Docker images

### 4. 🟢 Node.js App (`node-app/`)

Template for running Node.js applications with NGINX configuration.

**Parameters:**

-   `GITHUB_URL` - GitHub repository URL
-   `REPO_NAME` - Repository name
-   `SERV_PORT` - Application server port

**Stages:**

-   📥 Repository cloning
-   🔧 Environment variables loading
-   🔍 Software version check
-   📦 Dependencies installation
-   ⚙️ NGINX configuration
-   🚀 Project deployment

### 5. ✅ Parameter Validation (`validate-params/`)

Utility template for validating required parameters across all pipelines.

**Parameters:**

-   `CONT_NAME` - Container name (required)
-   `GITHUB_REPO_URL` - GitHub repository URL (required)

**Stages:**

-   ✅ Parameter validation

## 🔧 Requirements

### Jenkins

-   Jenkins with HTTPS enabled
-   Unique tokens for each job
-   Installed plugins:
    -   Git Plugin
    -   Docker Plugin
    -   NodeJS Plugin
    -   Pipeline Plugin

### Tools on Jenkins

-   Docker
-   Docker Compose
-   Node.js 20
-   Snyk CLI
-   OWASP ZAP (for security scans)
-   NGINX (for Node.js applications)

## 🚀 Usage

### 1. Create a new Jenkins job

1. Go to Jenkins → New Item
2. Select "Pipeline"
3. Enter job name (e.g., "Docker-Build-Pipeline")

**Note:** This job will serve as a template for multiple projects - each can use the same job with different parameters.

### 2. Configure Pipeline

1. In the "Pipeline" section, select "Pipeline script from SCM"
2. Select "Git" as SCM
3. Enter the URL of this repository (with Jenkinsfile templates)
4. Set branch to `main`
5. In "Script Path" enter the path to the selected template (e.g., `docker-container/Jenkinsfile`)

**Note:** The pipeline will run from the target repository (passed via `GITHUB_REPO_URL` or `GITHUB_URL` parameter), but the Jenkinsfile script will be fetched from this repository with templates.

### 3. Add parameters

In the "Build Triggers" → "This project is parameterized" section, add the required parameters:

**For Docker templates:**

-   `CONT_NAME` (String Parameter)
-   `GITHUB_REPO_URL` (String Parameter)

**For Node.js App:**

-   `GITHUB_URL` (String Parameter)
-   `REPO_NAME` (String Parameter)
-   `SERV_PORT` (String Parameter)

### 4. Run the job

1. Click "Build with Parameters"
2. Enter parameter values (including the target repository URL)
3. Click "Build"

**Alternatively:** Configure a webhook in the target repository to automatically trigger the pipeline with appropriate parameters.

## 🔒 Security

All templates include built-in security scans:

-   **Snyk** - dependency, Docker image, and IaC configuration scanning
-   **OWASP ZAP** - web application penetration testing (docker-multi-containers only)

## 📁 Repository Structure

```
my-jenkins-templates/
├── docker-container/
│   └── Jenkinsfile          # Single Docker container
├── docker-multi-containers/
│   └── Jenkinsfile          # Multi-container application
├── docker-next/
│   └── Jenkinsfile          # Next.js application
├── node-app/
│   └── Jenkinsfile          # Node.js application with NGINX
├── validate-params/
│   └── Jenkinsfile          # Parameter validation utility
└── README.md
```

## 🎯 Key Features

- **Consistent Formatting**: All Jenkinsfile templates follow standardized formatting with proper indentation and structure
- **Parameter Validation**: Built-in validation ensures required parameters are provided
- **Security Integration**: Comprehensive security scanning with Snyk and OWASP ZAP
- **Multi-Environment Support**: Templates work across different deployment scenarios
- **Clean Code Practices**: Well-structured and maintainable pipeline code

## 🔄 Updates

Templates are regularly updated with the latest CI/CD practices and security tools. Check regularly for available updates.

## 🤝 Support

For issues or questions regarding the templates, create an issue in this repository or contact the DevOps team.

---

**Note:** Ensure that Jenkins has appropriate permissions to clone repositories and run Docker containers.
