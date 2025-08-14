# IAM Policies for Instagram Automation System

This directory contains all the IAM policies needed for the AWS Instagram automation system.

## 🔧 Setup Instructions

### Step 1: Replace Placeholders

Before applying these policies, replace the following placeholders with your actual values:

| Placeholder | Replace With | Example |
|-------------|--------------|---------|
| `YOUR_PHOTOS_BUCKET_NAME` | Your S3 bucket name | `my-instagram-photos-bucket` |
| `YOUR_CAPTION_LAMBDA_FUNCTION_NAME` | Caption generation function name | `photo-caption-generator` |
| `YOUR_POSTING_LAMBDA_FUNCTION_NAME` | Posting function name | `instagram-zapier-bridge` |

### Step 2: Find and Replace

Use these commands to quickly replace placeholders:

**Linux/Mac:**
```bash
# Replace bucket name
sed -i 's/YOUR_PHOTOS_BUCKET_NAME/my-instagram-photos-bucket/g' *.json

# Replace function names
sed -i 's/YOUR_CAPTION_LAMBDA_FUNCTION_NAME/photo-caption-generator/g' *.json
sed -i 's/YOUR_POSTING_LAMBDA_FUNCTION_NAME/instagram-zapier-bridge/g' *.json
