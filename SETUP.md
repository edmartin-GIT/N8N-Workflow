# LinkedIn Weekly Post Automation - Setup Guide

## Workflow Overview

**Schedule (Wed 10AM)** → **Google Sheets** → **Filter Unposted** → **Pick First** → **Gemini AI** → **Prepare Data** → **Generate Image** → **LinkedIn Post** → **Update Sheet**

## Google Sheets Structure

Create a Google Sheet with these columns:

| Topic | Details | Status | PostedDate |
|-------|---------|--------|------------|
| AI in Healthcare | How AI is transforming patient care | | |
| Remote Work Tips | Best practices for remote teams | | |
| Cloud Migration | Steps to migrate to the cloud | posted | 2026-03-28 10:00 |

- **Topic** (required): The main subject for the LinkedIn post
- **Details** (optional): Additional context to guide Gemini
- **Status**: Leave empty for pending topics; the workflow sets it to `posted`
- **PostedDate**: Automatically filled after posting

## Credentials to Configure

After importing the workflow into n8n, update these credentials:

1. **Google Sheets OAuth2** - For reading topics and updating status
2. **Google Gemini API** - For generating post content
3. **Napkin AI API Key** (HTTP Header Auth) - For image generation
4. **LinkedIn OAuth2** - For creating the post

## Import Instructions

1. Open your n8n instance
2. Go to **Workflows** → **Import from File**
3. Select `linkedin-weekly-post-workflow.json`
4. Update each node with your credentials and Google Sheet URL
5. In the **Read Topics from Google Sheets** node, set your Sheet URL
6. In the **Create LinkedIn Post** node, set your LinkedIn Person URN
7. In the **Generate Image** node, update the API URL/auth for your image service
8. Activate the workflow

## Notes

- The workflow filters out rows where `Status = posted`, so each topic is only used once
- The **Limit** node ensures only one post per execution
- Adjust the Gemini prompt in the "Generate Post with Gemini" node to match your tone/style
- The image generation node is configured as an HTTP Request — update URL and body format to match your chosen image API (Napkin AI, DALL-E, Midjourney API, etc.)
