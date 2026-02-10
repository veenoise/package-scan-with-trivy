# Package Scan with Trivy

Automated vulnerability scanning for your repository using [Trivy](https://github.com/aquasecurity/trivy).

## Overview

This repository includes two GitHub Actions workflows that automatically scan your codebase for security vulnerabilities:
- **Table Output**: Console-friendly output for quick review
- **HTML Output**: Detailed reports converted to PDF and sent to Slack

## Features

- **Automated Scanning**: Runs on pushes and pull requests
- **Filesystem Scanning**: Scans the entire repository for vulnerabilities
- **Dual Output Formats**: Table for quick review, HTML for detailed reports
- **PDF Conversion**: Automatically converts HTML reports to PDF via N8N webhook
- **Slack Integration**: Sends PDF reports to Slack via webhook
- **Fail on Issues**: Exits with code 1 if vulnerabilities are found
- **Ignores Unfixed**: Only reports vulnerabilities that have available fixes
- **Severity Filtering**: Focuses on HIGH and CRITICAL vulnerabilities

## Workflows

### 1. Table Output (`scanner_table.yml`)

**Triggers:**
- Push to `main` or `develop` branches
- All pull requests

**Configuration:**
- **Format**: Table (console output)
- **Exit Code**: `1` (fails the build if vulnerabilities found)
- **Ignore Unfixed**: `true`
- **Scanners**: Vulnerability scanning only
- **Severity**: HIGH, CRITICAL

### 2. HTML Output (`scanner_html.yml`)

**Triggers:**
- Push to `main` or `develop` branches

**Configuration:**
- **Format**: HTML template
- **Exit Code**: `1` (fails the build if vulnerabilities found)
- **Ignore Unfixed**: `true`
- **Scanners**: Vulnerability scanning only
- **Severity**: HIGH, CRITICAL
- **Output**: `index.html`
- **Post-Processing**: Converts to PDF and sends to Slack

### Required Secrets

- `N8N_WEBHOOK`: N8N webhook URL for PDF conversion
- `BASIC_AUTH_TOKEN`: Basic authentication token for webhook

## Usage

Both workflows run automatically. No manual intervention required.

**To view scan results:**
- **Table Output**: Check the Actions tab for console output in workflow logs
- **HTML Output**: Review the PDF report delivered to Slack via N8N webhook

## How HTML Workflow Works

1. Trivy scans the repository filesystem for vulnerabilities
2. Generates an HTML report using Trivy's built-in template
3. Sends the HTML to N8N webhook for processing
4. N8N converts HTML to PDF using Gotenberg
5. PDF report is delivered to Slack
