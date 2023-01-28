# s3-transfer
for transfer of s3-data

Two AWS accounts(One for source S3 bucket and another for destination S3 bucket)
Create an IAM user in destination AWS account (see this doc to create IAM user for AWS account).
Configure AWS CLI in local machine with previously created IAM user credentials (see this doc to configure AWS CLI).


Step 1: Get the 12 digit destination AWS account number
Sign in to destination AWS account. Go to Support → Support center and copy account number from there.

Step 2: Setup source S3 bucket
Sign in to source AWS account. Create a bucket in S3(To create bucket, follow this doc). Attach the following policy to the bucket(To attach bucket policy, follow this doc). Upload some test files which are meant to be copied automatically to the destination bucket.

Step 3: Setup destination S3 bucket
Sign in to destination AWS account. Create a bucket in S3(To create bucket, follow this doc).

Step 4: Attach policy to IAM user in destination AWS account
Attach the following policy to the IAM user created previously in the destination AWS account (see this doc to add policy to IAM user).

Step 5: Sync S3 objects to destination
If above steps are completed, we can copy S3 bucket objects from source account to destination account by using the following AWS CLI command.

aws s3 sync s3://SOURCE-BUCKET-NAME s3://DESTINATION-BUCKET-NAME --source-region SOURCE-REGION-NAME --region DESTINATION-REGION-NAME


The above command should be executed with destination AWS IAM user account credentials only otherwise the copied objects in destination S3 bucket will still have the source account permissions and won’t be accessible by destination account users.



NOTE:  #Always use "s3:GetObjectTagging" option otherwise it will through an error "An error occurred (AccessDenied) when calling the GetObjectTagging operation: Access Denied
