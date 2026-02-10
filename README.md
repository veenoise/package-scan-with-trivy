# Package Scan with Trivy

Automated vulnerability scanning for your repository using [Trivy](https://github.com/aquasecurity/trivy).

## Overview

This repository includes a GitHub Actions workflow that automatically scans your codebase for security vulnerabilities on every push and pull request.

## Features

- **Automated Scanning**: Runs on pushes to `main` and `develop` branches, and on all pull requests
- **Filesystem Scanning**: Scans the entire repository for vulnerabilities
- **Fail on Issues**: Exits with code 1 if vulnerabilities are found
- **Ignores Unfixed**: Only reports vulnerabilities that have available fixes

## Workflow Configuration

The scan runs on:
- Push to `main` branch
- Push to `develop` branch  
- All pull requests

### Scan Settings

- **Scan Type**: Filesystem (`fs`)
- **Format**: Table output
- **Exit Code**: `1` (fails the build if vulnerabilities found)
- **Ignore Unfixed**: `true` (only reports fixable vulnerabilities)

## Usage

The workflow runs automatically. No manual intervention required.

To view scan results, check the Actions tab in your GitHub repository after each push or pull request.
