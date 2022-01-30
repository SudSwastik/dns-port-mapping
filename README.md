# Map Domain/Sub-Domain To A Random IP:Port To Make it Lsiten on Port 80/443


### Installation

> Create a VM in GCP

```
$ gcloud compute instances create <name> --project=<Project-id> --zone=us-central1-a --machine-type=e2-micro --network-interface=network-tier=PREMIUM,subnet=default --maintenance-policy=MIGRATE --service-account=<service-account> --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --tags=http-server,https-server --create-disk=auto-delete=yes,boot=yes,device-name=nginx-ssl,image=projects/debian-cloud/global/images/debian-10-buster-v20211209,mode=rw,size=10,type=projects/round-water-262008/zones/us-central1-a/diskTypes/pd-balanced --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any
```

> Login To VM and Install nginx

```
$ sudo apt update
$ sudo apt install nginx
```

> Create an A record with domain or subdomain pointing to ip of VM

> Modify the nginx configuration to create multiple server block to listen on domain and sub domain and point to it to the actual ip:port of your service. 

```
$ sudo nginx -t
$ sudo systemctl reload nginx
```