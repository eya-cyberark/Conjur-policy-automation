# GitHub Action Pipeline for Managing Conjur Policies

This GitHub Action automates the process of **loading and managing Conjur policies**, ensuring that changes made to policy files in your repository are automatically applied to your Conjur instance.

### Overview

This GitHub Action streamlines the management of Conjur policies by automatically loading policy files into Conjur whenever changes are made to your repository. The action triggers on `push` events to the `main` branch or when a pull request targeting the `main` branch is created, ensuring that policy updates are consistently applied without manual intervention.

The action interacts with Conjur’s API to authenticate via an API key and apply policy changes, including the creation or modification of resources like hosts and access control lists (ACLs).

### Key Features

- **Automated Policy Management**: Automatically applies policy updates to Conjur whenever policy files are modified in the repository.
- **API Authentication**: Securely authenticates with Conjur using an API key stored in GitHub Secrets.
- **Policy Application**: The action automatically applies changes based on the modified policy files in the commit.

### Prerequisites

To use this GitHub Action, ensure the following prerequisites are met:

- **Conjur API Key**: Store your Conjur API key in GitHub Secrets as `CONJUR_API_KEY`.
- **Conjur URL**: Provide the URL for your Conjur instance (Cloud, Enterprise, or OSS).
- **Policy Repository**: Your repository should include the policy files that will be applied to Conjur.

### Secrets and Configuration

Ensure the following GitHub Secrets are configured in your repository:

1. **`CONJUR_API_KEY`** (GitHub Secret)
   - The API key used to authenticate with your Conjur instance.

### Folder and File Conventions

Policy files should be organized and named according to the following conventions:

#### Folder Structure

Organize your policy files by either application or policy branch:

- **By Application**:

```
root
  |- APP1234
    |- 01_host.yml
    |- 02_acls.yml
```


- **By Policy Branch**:

```
root
  |- apps
    |- 01_app1234.yml
  |- acls
    |- 02_app1234.yml 
```

#### File Naming Conventions

- **`01_`**: Files with this prefix are used for creating host resources in Conjur.
- **`02_`**: Files with this prefix are used for granting ACL access to hosts.
- **`d_`**: Files with this prefix are used for deleting hosts or other resources.

### Workflow Trigger

The GitHub Action is triggered on both **push** and **pull request** events targeting the `main` branch. The action follows these steps:

1. **Install Dependencies**: Installs required dependencies like `curl` for interacting with the Conjur API.
2. **Authenticate to Conjur**: Authenticates using the stored API key and retrieves a token for API interaction.
3. **Apply Policy Updates**: Applies any policy updates based on the modified files in the commit.

### Policy Management Flow

1. **Commit Changes**: Modify the appropriate policy files in your repository.
2. **Push Changes**: Push the changes to the `main` branch or create a pull request targeting `main`.
3. **Automatic Trigger**: The GitHub Action automatically triggers when changes are detected.
4. **Authentication and Policy Update**: The action authenticates to Conjur and applies the changes from the modified policy files.
5. **Validation**: Verify that the policies have been successfully applied in Conjur.

### Conclusion

This GitHub Action automates the process of managing Conjur policies, allowing policy updates to be seamlessly applied whenever changes are made to the repository. By incorporating this action into your CI/CD pipeline, you ensure that Conjur policies remain up-to-date without manual intervention, improving both automation and security.
