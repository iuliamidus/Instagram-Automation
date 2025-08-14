# Lambda Test Events

## S3 Upload Test Event
File: `s3-upload-event.json`
- Tests the photo caption generation Lambda
- Simulates S3 upload trigger
- **Update the bucket name and image key** to match your actual S3 objects

## EventBridge Hourly Test Event  
File: `eventbridge-hourly-trigger.json`
- Tests the Instagram posting Lambda
- Simulates EventBridge hourly trigger
- **Update account ID** to match your AWS account

## How to Use

### In AWS Lambda Console:
1. Go to your Lambda function
2. Test tab → Create new test event
3. Copy JSON from the appropriate file
4. Update bucket/image names to match your data
5. Save and test

### With AWS CLI:
```bash
aws lambda invoke \
  --function-name photo-caption-generator \
  --payload file://s3-upload-event.json \
  response.json

## Method 2: Add Them in AWS Lambda Console

**For Caption Generation Lambda:**
1. Go to Lambda → your caption function → Test tab
2. Create new test event:
   - **Event name**: `S3-Upload-Test`
   - **Template**: Amazon S3 Put
   - **Or paste the JSON above**
3. **Important**: Update the bucket name and image key to real values
4. Save and test

**For Posting Lambda:**
1. Go to Lambda → your posting function → Test tab  
2. Create new test event:
   - **Event name**: `EventBridge-Hourly-Test`
   - **Template**: Amazon EventBridge (CloudWatch Events)
   - **Or paste the JSON above**
3. Save and test

## Method 3: Quick GitHub Upload

**Create this folder structure in your repo:**
