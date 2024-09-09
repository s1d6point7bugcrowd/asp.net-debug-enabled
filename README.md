## Vulnerability Explanation

### ASPX Debug Mode

ASPX (Active Server Pages Extended) is a web application framework developed by Microsoft for building dynamic websites. When **debug mode** is enabled in ASPX applications, detailed error messages and stack traces are displayed to help developers identify issues during development.

### Security Risk

When debug mode is left enabled in production environments, it can unintentionally leak sensitive information. This includes:

- **Stack Traces**: Detailed call stacks that show the internal structure of the application.
- **Compilation Errors**: Information about the underlying code, which could expose business logic or security mechanisms.
- **Server Configuration Details**: Internal configuration details like server paths, libraries, and other software dependencies.

An attacker could exploit these details to further investigate the system, identify vulnerabilities, or craft targeted attacks.

### Why This Happens

Developers often use debug mode during development to catch and resolve bugs. However, if debug mode is accidentally left enabled when the application is deployed, it exposes internal workings to anyone who can access the application. This can result in:

- **Information Disclosure**: Attackers can gain insights into how the application operates, what technologies are being used, and any potential weaknesses in the code.
- **Sensitive Data Exposure**: Error messages and traces could leak sensitive data such as usernames, passwords, or other internal system information.

### How This Template Helps

This Nuclei template is designed to detect when an ASPX application has debug mode enabled. It sends a crafted request to the target, mimicking a scenario where debug information would be returned. The template then looks for common debug-specific indicators, such as:

- `Debug`
- `Stack Trace`
- `ASP.NET`
- `Compilation`

By running this template, security researchers and bug bounty hunters can identify ASPX applications that are leaking sensitive information due to debug mode being enabled, allowing them to report the issue for remediation.








# ASPX Debug Mode Enabled Detection - Nuclei Template

## Overview

This repository contains a custom Nuclei template designed to detect when **ASPX debug mode** is enabled on a target web application. The template sends a specific request to the target and checks for debug-related information in the response, such as stack traces or compilation details, which are often leaked when debug mode is active.

## Usage

### Requirements
- **Nuclei**: Ensure you have Nuclei installed. You can download it from [Project Discovery](https://github.com/projectdiscovery/nuclei).

### Running the Template

To run the template against a target URL, use the following command:

```bash
nuclei -u <target_url> -t /path/to/aspx-debug-mode-enabled.yaml
