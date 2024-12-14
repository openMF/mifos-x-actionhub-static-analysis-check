# KMP Static Analysis Check GitHub Action

## Overview

This GitHub Action performs comprehensive static analysis checks on a Kotlin Multiplatform (KMP)
project. It ensures code quality, formatting, and dependency management through multiple
verification steps.

```yaml
- name: Static Analysis Check
  uses: openMF/kmp-static-analysis-check-action@v1.0.0
```

## Prerequisites

- Kotlin Multiplatform project
- Gradle build system
- Java 17

## Requirements

- Configured Gradle project
- Spotless plugin
- Detekt plugin
- Dependency Guard plugin

## Workflow Steps

### 1. Java Environment Setup

- Uses Zulu OpenJDK distribution
- Configures Java 17 development environment

### 2. Gradle Configuration

- Sets up Gradle build system
- Configures caching for improved build performance

### 3. Gradle Dependency Caching

- Caches Gradle dependencies and build outputs
- Uses runner OS and Gradle configuration hash as cache key
- Speeds up subsequent build processes

### 4. Build Logic Check

- Runs configuration checks on build logic
- Command: `./gradlew check -p build-logic`

### 5. Code Formatting Verification

- Uses Spotless to check code formatting
- Command: `./gradlew spotlessCheck`
- Flags:
    - `--no-configuration-cache`
    - `--no-daemon`

### 6. Static Code Analysis

- Runs Detekt for static code analysis
- Command: `./gradlew detekt`

### 7. Dependency Verification

- Checks project dependencies
- Command: `./gradlew dependencyGuard`

### 8. Detekt Reports Upload

- Uploads Detekt analysis reports as artifacts
- Conditional upload based on Detekt check success
- Stores reports in `**/build/reports/detekt/detekt.md`

## Example Usage

```yaml
name: Static Analysis
on: [ push, pull_request ]

jobs:
  static-analysis:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Static Analysis Check
        uses: openMF/kmp-static-analysis-check-action@v1.0.0
```

## Benefits

- Ensures code quality
- Maintains consistent code formatting
- Identifies potential code smells and vulnerabilities
- Manages dependency integrity
- Provides detailed analysis reports
