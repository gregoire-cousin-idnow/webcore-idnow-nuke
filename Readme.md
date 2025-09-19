# AWS Nuke - One Command Cleanup

This repository provides a simple way to run [aws-nuke](https://github.com/ekristen/aws-nuke) with a pre-configured configuration file to safely clean up AWS resources.

---

## Prerequisites

- macOS with [aws-nuke](https://github.com/ekristen/aws-nuke) installed:
  ```bash
  brew install aws-nuke
  ```
- AWS credentials configured in your environment

---

## One-Command AWS Cleanup

Run the following command to clean up your AWS resources:

```bash
# Set your AWS credentials
export AWS_ACCESS_KEY_ID=<your-access-key>
export AWS_SECRET_ACCESS_KEY=<your-secret-key>
export AWS_REGION=eu-west-3

# Run aws-nuke with remote config (with timeout and multiple attempts)
for i in 1 2 3; do echo "Running aws-nuke attempt $i..."; timeout 300 aws-nuke run --config <(curl -sSL https://raw.githubusercontent.com/gregoire-cousin-idnow/webcore-idnow-nuke/main/config.yaml) --no-dry-run --force || true; done
```

This single command:
1. Sets up your AWS credentials
2. Downloads the configuration file directly from GitHub
3. Runs aws-nuke with a 5-minute timeout
4. Makes 3 attempts to ensure thorough cleanup
5. Uses the `|| true` to continue even if an attempt fails
