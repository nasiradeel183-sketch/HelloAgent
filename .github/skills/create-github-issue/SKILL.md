---
name: create-github-issue
description: Creates a new GitHub issue as either a feature request or bug report using the GitHub MCP tool. For feature requests: problem space, description, why, success measures. For bug reports: version info, environment, reproduction steps, priority. USE FOR: creating issues, filing bug reports, submitting feature requests, opening GitHub issues.
---

# Create GitHub Issue Skill

## Overview
This skill helps you create well-structured GitHub issues using the MCP GitHub tool. It supports two issue types: **Feature Requests** and **Bug Reports**, each with specific required fields.

## When to Use
- Creating a **bug report** with reproduction steps and version information
- Submitting a **feature request** with problem space and success criteria
- Filing issues in a GitHub repository
- Opening GitHub issues programmatically

## Issue Types

### Feature Request
A feature request should include:
- **Problem Space**: What problem does this solve? What's the current limitation?
- **Description**: Clear description of the requested feature
- **Why**: Why is this feature needed? What's the business value or user impact?
- **Success Measures**: How do we know the feature is successful? What are the acceptance criteria?

### Bug Report
A bug report should include:
- **Version Info**: Version of the software where the bug occurs
- **Environment**: Relevant environment details (OS, browser, etc.)
- **Reproduction Steps**: Step-by-step instructions to reproduce the bug
- **Expected Behavior**: What should happen
- **Actual Behavior**: What actually happens
- **Priority**: High, Medium, or Low (based on impact and frequency)

## Skill Flow

1. **Determine issue type**: Feature Request or Bug Report (ask if not provided)
2. **Collect required fields**: Gather all information specific to the issue type
3. **Validate completeness**: Ask follow-ups for any missing required fields
4. **Compose issue body**: Build markdown-formatted issue body with sections and bullet lists
5. **Create via MCP**: Use the GitHub MCP tool to create the issue
6. **Confirm**: Return the issue URL and issue number to the user

## Usage Examples

### Example 1: Create a Feature Request
```
@create-github-issue
Type: Feature Request
Repository: owner/repo
Title: Add dark mode support
Problem Space: Users working in low-light environments need a dark mode option
Description: Implement a dark mode theme that applies across the entire UI
Why: Improves user experience for night-time users and reduces eye strain
Success Measures: 
  - Dark mode toggle in settings
  - All UI components properly themed
  - Theme preference persists across sessions
```

### Example 2: Create a Bug Report
```
@create-github-issue
Type: Bug Report
Repository: owner/repo
Title: Login fails with special characters in password
Version Info: v2.1.0
Environment: Windows 10, Chrome 120
Reproduction Steps:
  1. Go to login page
  2. Enter username
  3. Enter password containing @ symbol
  4. Click submit
Expected Behavior: Login should succeed
Actual Behavior: Error message "Invalid credentials"
Priority: High
```

## MCP Tool Integration

This skill uses the `@github` MCP tool to create issues:
- Authenticates using your GITHUB_TOKEN environment variable
- Creates the issue in the specified repository
- Returns the issue URL and issue number
- Does NOT use PowerShell commands

Example MCP call format:
```
@github createIssue
{
  "owner": "OWNER",
  "repo": "REPO",
  "title": "ISSUE TITLE",
  "body": "<COMPOSED MARKDOWN BODY>",
  "labels": ["bug" | "enhancement", ...]
}
```

## Requirements
- Repository must be in format: `owner/repo`
- You must have write access to the repository
- GitHub MCP tool must be configured with valid GITHUB_TOKEN
- All required fields for the issue type must be provided

## Notes
- The skill will ask clarifying questions for missing fields rather than guessing
- Issue creation uses the authenticated user's account
- Support for labels: bug, enhancement, documentation, question, etc.