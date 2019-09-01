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
    
## CLOUD STORAGE  >>>>>>>>>>>>>>>>>>>
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

### Check current versioning policy:

        gsutil versioning get gs://&lt;BUCKET&gt;

### Enable Object Versioning:

        gsutil versioning set on gs://&lt;BUCKET&gt;

### Check full object details in bucket:

        gsutil ls -a gs://&lt;BUCKET&gt;

### Download current lifecycle policy to local machine to edit:

        gsutil lifecycle get gs://&lt;BUCKET&gt; > filename.json

### Set new lifecycle policy after making above edits:

        gsutil lifecycle set filename.json gs://&lt;BUCKET&gt;


## DISK MANAGEMENT

### Create disk:

    gcloud compute disks create &lt;DISK_NAME&gt; --type=&lt;DISK_TYPE&gt; --size=&lt;SIZE&gt; --zone=&lt;ZONE&gt;

### Resize disk:

    gcloud compute disks resize &lt;disk_name&gt; --size=&lt;size&gt; --zone=&lt;zone&gt;

### Attach disk:

    gcloud compute instances attach-disk &lt;instance&gt; --disk=&lt;disk_name&gt; --zone=&lt;zone&gt;

## Formatting and Mounting DISK for LINUX in GCP >>>
### View available disks:

    sudo lsblk
### Format attached disk:

    sudo mkfs.ext4 -m 0 -F -E lazy_itable_init=0,lazy_journal_init=0,discard /dev/sdb
### Create mount directory:

    sudo mkdir -p /mnt/disks/disk2
### Mount disk:

    sudo mount -o discard,defaults /dev/sdb /mnt/disks/disk2

### Set read/write permissions:

    sudo chmod a+w /mnt/disks/
    Resize existing Linux disk
    
### Identify the disk to resize:

    sudo lsblk

### Resize (grow) the partition:

    sudo growpart /dev/sda 1

### Extend file system to use added space:

    sudo resize2fs /dev/sda1
### Verify file system is resized:

    df -h 



 ## STACK DRIVER >>>>>>>>>>>>>>>>>>>>
