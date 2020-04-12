## GCP COMMAND LINE

### GCP VNET CREATION

```gcloud compute networks create privatenet --subnet-mode=custom```

#### Subnet

```gcloud compute networks subnets create privatesubnet-us --network=privatenet --region=us-central1 --range=172.16.0.0/24```

***Private Subnet US***

```gcloud compute networks subnets create privatesubnet-us --network=privatenet --region=us-central1 --range=172.16.0.0/24```

*** Private Subnet EU ***

```gcloud compute networks subnets create privatesubnet-eu --network=privatenet --region=europe-west1 --range=172.20.0.0/20```

*** LIST VPC ****

```gcloud compute networks list```

*** SORT BY VNET AND SUBNET ***

```gcloud compute networks subnets list --sort-by=NETWORK```

*** DELETION ***

```gcloud compute networks delete <name of vnet> ```

