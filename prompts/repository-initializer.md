---
name: repository-initializer
description: "Create a new repository from the Liatrio Open Source Template and automatically customize it"
tags:
  - initialization
  - onboarding
  - repository-creation
arguments:
  - name: project_name
    description: "Name for the new project repository (e.g., 'my-awesome-project')"
    required: true
  - name: project_description
    description: "One-sentence description of the project"
    required: true
  - name: local_parent_folder
    description: "Local directory path where the new repository should be cloned (e.g., '/home/user/projects')"
    required: true
  - name: github_organization
    description: "GitHub organization or username where the repository should be created (defaults to 'liatrio-labs' if not specified)"
    required: false
  - name: primary_language
    description: "Primary language or framework (Node.js, Python, Go, Ruby, etc.) for workflow customization"
    required: false
  - name: additional_details
    description: "Optional additional customization goals or requirements"
    required: false
meta:
  category: repository-management
  allowed-tools: Terminal, Read, Write, Edit
  note: "Automates the complete template initialization and customization workflow"
---

# Repository Initializer Prompt

## Your Goal

Create a new repository from the Liatrio Open Source Template and automatically customize it for the user's project.

## Required Inputs

If any of these inputs are not provided, prompt the user before proceeding:

- **project_name** (required): Name for the new project repository
- **project_description** (required): One-sentence description of the project
- **local_parent_folder** (required): Local directory path where the repository should be cloned
- **primary_language** (optional): Primary language or framework (Node.js, Python, Go, Ruby, etc.)
- **additional_details** (optional): Any additional customization goals or requirements

## Workflow

### Step 1: Create Repository from Template

1. **Create the repository** using GitHub CLI:

   ```bash
   gh repo create <org>/<project_name> --template liatrio-labs/open-source-project-template --private --description "<project_description>"
   ```

   **Note**: Replace `<org>` with the GitHub organization or username where the repository should be created. If not specified, use the `liatrio-labs` organization.

2. **Clone the repository** to the specified local parent folder:

   ```bash
   cd <local_parent_folder>
   gh repo clone <org>/<project_name>
   cd <project_name>
   ```

### Step 2: Run Customization Prompt

After cloning, automatically run the customization prompt:

1. **Read the customization prompt** from `prompts/repository-template-customizer.md` in the cloned repository
2. **Execute the customization workflow** using the provided inputs:
   - `target_repository`: Use `$(pwd)` (current directory - the cloned repo)
   - `project_name`: Use the provided project name
   - `project_description`: Use the provided project description
   - `primary_language`: Use the provided primary language (if specified)
   - `customization_goals`: Use any additional details provided

3. **Follow all instructions** in the customization prompt to complete the setup

## Output

After completion, inform the user:

- Repository created and cloned successfully
- Customization completed
- Next steps (e.g., "Review the customization-plan.md file, make initial commits, and run the audit prompt")

## Error Handling

If any step fails:

- **Repository creation fails**: Check GitHub CLI authentication (`gh auth status`) and permissions
- **Clone fails**: Verify the repository was created and the local parent folder path is valid
- **Customization fails**: Report the specific error and provide guidance on manual remediation
