## Workflow Overview

The workflow performs the following steps:

1. **Trigger**: The workflow is triggered when a pull request is closed on the `main` branch.
2. **Checkout Source Repository**: Checks out the source repository using the provided GitHub token.
3. **Install `yq`**: Installs the `yq` tool for parsing YAML files.
4. **Set Environment Variables from Config**: Reads the configuration from `.github/sync-config.yaml` and sets environment variables.
5. **Checkout Destination Repository**: Checks out the destination repository using the provided GitHub token.
6. **Configure Git**: Sets up Git configuration for committing and pushing changes.
7. **Create Sync Branch**: Creates a new sync branch in the destination repository.
8. **Create Exclusion File**: Creates an exclusion file based on the configuration to exclude certain directories and files from synchronization.
9. **Sync Source to Destination**: Synchronizes the source repository to the destination repository, excluding specified directories and files.
10. **Create Pull Request**: Creates a pull request in the destination repository with the synchronized changes.

## Configuration

The workflow relies on a configuration file located at `.github/sync-config.yaml` in the source repository. The configuration file should define the following:

- `repositories.source.name`: Name of the source repository.
- `repositories.destination.name`: Name of the destination repository.
- `repositories.destination.default_branch`: Default branch of the destination repository.
- `sync.default_branch_name`: Default branch name for synchronization.
- `exclude.directories`: List of directories to exclude from synchronization.
- `exclude.files`: List of files to exclude from synchronization.

Example configuration file:
```yaml
repositories:
  source:
    name: source-repo
  destination:
    name: destination-repo
    default_branch: main
sync:
  default_branch_name: sync-branch
exclude:
  directories:
    - dir1
    - dir2
  files:
    - file1.txt
    - file2.txt
Secrets
The workflow requires the following secrets to be set in the repository:

GH_PAT: A personal access token with permissions to access the source and destination repositories.
Usage
To use this workflow, ensure that the .github/sync-config.yaml file is configured correctly and the required secrets are set. Then, simply merge a pull request into the main branch of the source repository to trigger the synchronization process.

Contributing
If you have any suggestions or improvements for this workflow, please feel free to open an issue or submit a pull request.



