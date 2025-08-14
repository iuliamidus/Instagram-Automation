# Complete Setup Guide - AWS Instagram Automation

This guide walks you through setting up the entire automated Instagram posting system from scratch.

## 📋 Prerequisites

Before starting, ensure you have:

- **AWS Account** with administrative access
- **Instagram Business Account** (converted from personal)
- **Zapier Account** (free tier sufficient)
- **Basic AWS CLI** installed and configured (optional but recommended)
- **Photos ready** (JPEG format, under 5MB each)

### Required AWS Service Access
- ✅ AWS Lambda
- ✅ Amazon S3
- ✅ Amazon DynamoDB
- ✅ Amazon Bedrock (with Claude 3 model access)
- ✅ Amazon EventBridge
- ✅ AWS IAM

## 🚀 Step-by-Step Setup

### Phase 1: AWS Infrastructure Setup

#### Step 1: Create S3 Bucket

1. **Go to S3 Console**
   - AWS Console → S3 → Create bucket
   - **Bucket name**: `your-instagram-photos-[random-string]`
   - **Region**: Choose your preferred region (e.g., `us-east-1`, `eu-west-2`)
   - **Public access**: We'll configure this later

2. **Configure Bucket for Public Read**
   - Go to bucket → Permissions tab
   - **Block public access**: Edit → Uncheck "Block all public access" → Confirm
   - **Bucket policy**: Add the policy from `/aws-infrastructure/iam-policies/s3-bucket-policy.json`
   - Replace `YOUR_PHOTOS_BUCKET_NAME` with your actual bucket name

#### Step 2: Create DynamoDB Table

1. **Go to DynamoDB Console**
   - AWS Console → DynamoDB → Tables → Create table
   - **Table name**: `instagram-post-queue`
   - **Primary key**: `image_key` (String)
   - **Settings**: Use default provisioned capacity

2. **Verify Table Structure**
   - The table will auto-create columns as data is inserted
   - Expected schema: `image_key`, `status`, `caption`, `bucket`, `created_at`, `scheduled_time`

#### Step 3: Enable Bedrock Model Access

1. **Go to Bedrock Console**
   - AWS Console → Amazon Bedrock → Model access
   - **Request access** to "Claude 3 Sonnet" model
   - **Wait for approval** (usually instant)
   - **Note the model ID**: `anthropic.claude-3-sonnet-20240229-v1:0`

#### Step 4: Create IAM Roles and Policies

1. **Create Caption Generation Lambda Role**
   ```bash
   aws iam create-role \
     --role-name InstagramCaptionLambdaRole \
     --assume-role-policy-document file://aws-infrastructure/iam-policies/lambda-trust-policy.json
