# Send Email Notification GitHub Action

This repository contains a GitHub Action workflow to send an email notification whenever there is a new commit pushed to the `main` branch. This is achieved using the `dawidd6/action-send-mail@v2` action.

## Workflow Overview

The workflow defined in this repository performs the following steps:

1. **Checkout the code**: Retrieves the latest code from the repository.
2. **Send an email**: Sends an email notification about the new commit.

## Prerequisites

Before using this workflow, you need to set up the following secrets in your GitHub repository:

- `MAIL_SERVER_SMTP`: The SMTP server address for sending emails. (example: `smtp.example.com`)
- `MAIL_SERVER_PORT`: The port number for the SMTP server. (example: `587` (commonly used port for TLS))
- `EMAIL_USERNAME`: The username for your email account. (example: `your-email@example.com`)
- `EMAIL_PASSWORD`: The password for your email account. (example: `your-email-password`)
- `EMAIL_TO`: The recipient email addresses. (example: `your-email@example.com` or `first-email@example.com,second-email@example.com`)
- `EMAIL_FROM`: The sender email address. (example: `<your-email@example.com>`)

## How to Set Up

1. **Create a new GitHub repository** (or navigate to an existing one).
2. **Add the necessary secrets** to your repository. You can add secrets by navigating to `Settings > Secrets and variables > Actions > New repository secret` and adding each of the required secrets.

## Example Workflow File

Below is the example workflow file (`.github/workflows/send-email-notification.yml`) included in this repository:

```yaml
name: Send Email Notification

on:
  push:
    branches:
      - main # or 'master'

jobs:
  send_email:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Send email
        uses: dawidd6/action-send-mail@v3
        with:
          server_address: ${{ secrets.MAIL_SERVER_SMTP }}
          server_port: ${{ secrets.MAIL_SERVER_PORT }}
          username: ${{ secrets.EMAIL_USERNAME }}
          password: ${{ secrets.EMAIL_PASSWORD }}
          subject: "New Commit on Main"
          to: ${{ secrets.EMAIL_TO }}
          from: ${{ secrets.EMAIL_FROM }}
          body: "A new commit has been pushed!"
          secure: true # or false for no SSL
```

## How It Works

- **Trigger**: The workflow is triggered whenever a push is made to the `main` branch.
- **Checkout Code**: Uses the `actions/checkout@v3` action to check out the repository code.
- **Send Email**: Utilizes the `dawidd6/action-send-mail@v2` action to send an email notification with the provided details.

## Customization

You can customize the email content by modifying the `subject` and `body` fields in the workflow file. For example, you can include the commit message or author details in the email body.

```yaml
body: "A new commit has been pushed! Commit message: ${{ github.event.head_commit.message }}"
```

## Full documentation

For more information on this actions, refer to the [official documentation](https://github.com/dawidd6/action-send-mail).
