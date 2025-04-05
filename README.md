

```bash
#!/bin/bash

# Function to create S3 buckets for different departments
create_s3_buckets() {
    company="datawise"
    departments=("Marketing" "Sales" "HR" "Operations" "Media")

    for department in "${departments[@]}"; do
        bucket_name="${company}-${department}-Data-Bucket"

        # Check if the bucket already exists
        if aws s3api head-bucket --bucket "$bucket_name" &>/dev/null; then
            echo "S3 bucket '$bucket_name' already exists."
        else
            # Attempt to create the S3 bucket using AWS CLI
            aws s3api create-bucket --bucket "$bucket_name" --region your-region
            if [ $? -eq 0 ]; then
                echo "S3 bucket '$bucket_name' created successfully."
            else
                echo "Failed to create S3 bucket '$bucket_name'."
            fi
        fi
    done
}

# Call the function to create the S3 buckets
create_s3_buckets
```

### Key Elements in the Script:

1. **Function Definition:**
   - The `create_s3_buckets` function defines an array of departments and generates a unique S3 bucket name for each department.
   
2. **Check for Existing Buckets:**
   - The script uses `aws s3api head-bucket --bucket "$bucket_name"` to check if the S3 bucket already exists. If it does, a message is printed saying that the bucket exists. This prevents the script from trying to create a bucket that already exists, which would otherwise result in an error.

3. **Error Handling:**
   - The script uses `$?` to check the exit status of the `aws s3api create-bucket` command. If the command returns a success code (0), the bucket is created successfully, and a success message is printed. Otherwise, a failure message is displayed.

4. **Bucket Creation:**
   - If the bucket does not exist, the script proceeds with creating the S3 bucket using the `aws s3api create-bucket` command and checks the success of the operation.

### Summary:

- The script aims to create S3 buckets for different departments within a company, with error handling for scenarios where the bucket already exists.
- It ensures that unnecessary errors are prevented and provides clear feedback for both successful and failed operations.

This script demonstrates essential error-handling practices in shell scripting, particularly in the context of interacting with AWS services.
