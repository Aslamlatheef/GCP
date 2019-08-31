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
    
 ## STACK DRIVER >>>>>>>>>>>>>>>>>>>>
