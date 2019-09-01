# GCP

## BILLING >>>> Storing on BIGQUERY

You can capture and save your date on S3 and also Bigquery where you can also do some analytics if you want.

### CAPTURE BILLING DATA FROM BIGQUERY and Few more examples for Billing Report.
    SELECT *  
    FROM `cloud-training-prod-bucket.arch_infra.billing_data`

### Highest cost First 
    SELECT *  
    FROM `cloud-training-prod-bucket.arch_infra.billing_data`
    ORDER BY cost DESC
    
### Specific COST 

     SELECT product, resource_type, start_time, end_time,  
     cost, project_id, project_name, project_labels_key, currency, currency_conversion_rate,
     usage_amount, usage_unit
     FROM `cloud-training-prod-bucket.arch_infra.billing_data`
     WHERE (cost > 3)  

note here "3" is cost

### Next let’s find which product had the highest total number of records:

    SELECT product, COUNT(*)
    FROM `cloud-training-prod-bucket.arch_infra.billing_data`
    GROUP BY product
    LIMIT 200

###  let’s see which product most frequently cost more than a dollar:

    SELECT product, cost, COUNT(*)
    FROM `cloud-training-prod-bucket.arch_infra.billing_data`
    WHERE (cost > 1)
    GROUP BY cost, product
    LIMIT 200
    
    
    
    
## CLOUD STORAGE 
### Assiging Access

### Assign IAM roles to buckets:

        gsutil iam ch user:(user_email):(role1,role2) gs://(BUCKET)

### Remove IAM role from bucket:

        gsutil iam ch -d user:(user_email):(role1,role2) gs://(BUCKET)

### Remove all roles from bucket for given user:

        gsutil iam ch -d user:(user_email) gs://(BUCKET)

### Assign ACL roles to buckets and objects:

        gsutil acl ch -u (user_email):(O/R/W) gs://(BUCKET)

### Delete all ACLs:

        gsutil acl ch -d (user_email) gs://(BUCKET)

### Signed URLs

Create service account with key
        
        Upload to cloud shell (or add to current CLI environment)
        gsutil signurl -d (time_period (10m)) (keyfile.json) gs://(BUCKET)/(object)


 ## STACK DRIVER >>>>>>>>>>>>>>>>>>>>
