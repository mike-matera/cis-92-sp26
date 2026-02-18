
gcloud config set project your-project-id


gcloud compute instances create my-debian-vm  \
    --machine-type=e2-small \
    --image-family=debian-12 \
    --image-project=debian-cloud \
    --zone=us-central1-a \
    --tags=http-server 

gcloud compute firewall-rules create allow-http-https-on-tagged-servers \
    --network=default \
    --allow=tcp:80,tcp:443 \
    --target-tags=http-server \
    --source-ranges=0.0.0.0/0 \
    --description="Allow incoming HTTP and HTTPS traffic to servers with the http-server tag" \
    --direction=INGRESS

gcloud compute ssh my-debian-vm --zone=us-central1-a

gcloud compute instances delete my-debian-vm --zone=us-central1-a

gcloud compute firewall-rules delete allow-http-https-on-tagged-servers

