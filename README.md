# Netflix Clone - Jenkins CI/CD with SonarQube, Trivy, OWASP, Grafana, and Prometheus

## Table of Contents

- [Introduction](#introduction)
- [Setup](#setup)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [Jenkins CI/CD](#jenkins-cicd)
- [Integration with SonarQube](#integration-with-sonarqube)
- [Security Scanning with Trivy and OWASP](#security-scanning-with-trivy-and-owasp)
- [Monitoring with Grafana and Prometheus](#monitoring-with-grafana-and-prometheus)
- [Contributing](#contributing)
- [License](#license)

## Introduction

This repository contains a Netflix clone application deployed on Amazon EC2 using Jenkins for Continuous Integration and Continuous Deployment (CI/CD). The project is integrated with SonarQube for code quality analysis, Trivy for container security scanning, and OWASP for web application security. Additionally, Grafana and Prometheus are integrated for monitoring the application's performance and health.

## Setup

### Prerequisites

Before you begin, make sure you have the following prerequisites:

- [Amazon EC2](https://aws.amazon.com/ec2/) instance with appropriate permissions
- [Jenkins](https://www.jenkins.io/) installed and configured on your EC2 instance
- [SonarQube](https://www.sonarqube.org/) server up and running
- [Trivy](https://github.com/aquasecurity/trivy) installed for container scanning
- [OWASP ZAP](https://www.zaproxy.org/) for web application security scanning
- [Grafana](https://grafana.com/) and [Prometheus](https://prometheus.io/) installed and configured

### Installation

1. Clone the repository to your local machine:

   ```bash
   git clone https://github.com/your-username/netflix-clone.git
   ```

2. Navigate to the project directory:

   ```bash
   cd netflix-clone
   ```

3. Deploy the application on your EC2 instance.

## Jenkins CI/CD

The Jenkins pipeline is configured to automate the build, test, and deployment processes. The `Jenkinsfile` contains the stages for each phase of the CI/CD pipeline. Make sure to configure your Jenkins server to trigger the pipeline on code changes.

## Integration with SonarQube

SonarQube is used to perform static code analysis and assess code quality. Configure your Jenkins server to integrate with SonarQube by providing the SonarQube server URL and authentication credentials. The results of the code analysis will be available on the SonarQube dashboard.

## Security Scanning with Trivy and OWASP

Trivy is utilized for scanning container images for vulnerabilities, and OWASP ZAP is used for web application security testing. Make sure to run Trivy before deploying the application and OWASP ZAP during the testing phase. The scan results should be reviewed to address any security issues.

## Monitoring with Grafana and Prometheus

Grafana and Prometheus are integrated to monitor the performance and health of the application. Configure the Prometheus server to scrape metrics from your application, and then set up Grafana to visualize the metrics. Import the provided Grafana dashboard for a comprehensive view of your application's metrics.

## Contributing

If you find any issues or have suggestions for improvement, feel free to open an issue or create a pull request. Your contributions are welcome!
