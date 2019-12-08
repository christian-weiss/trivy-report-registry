# Install Trivy Report Registry (TRR)

## Prepare a webserver
Feel free to host your instance of Trivy Report Registry e.g. on a Google Cloud Platform (GCP) in the free-tier (always free).
All you need is to point an existing domain name to the IP of the GCP server. [How to setup a GCP server](GCP_setup.md) 

## Configure TRR
- Create a .env file:
    ```
    cp TEMPLATE.env .env
    ```
- Add your domain / subdomains and email adress to .env file
    ```
    vi .env
    ```

## Deploy TRR
Use ssh / sftp to upload files to your server:
- <projectRoot>/services/ => <vm>:/home/nameHere/trivy-report-registry/services/
- <projectRoot>/data/     => <vm>:/home/nameHere/trivy-report-registry/data/

## Start TRR
Start all TRR services with a single command:
    ```
    docker-compose up -d
    ```

## Integrate TRR with Docker Hub
To trigger Trivy all you need to do is to:
 + create a webhook at docker hub
   let IT point to: `https://trivy-report-registry.yourdomain.com/trigger` 
 + generate a report with trivy on your build pipeline
   ```
   trivy --format json --output report.json --input docker-image.tar
   # or
   trivy --format json --output report.json index.docker.io/jmalloc/echo-server
   ```
 + send trivy reports (json) to TRR  
   add this to your build script:
   ```
   curl -X POST -H "Content-Type: application/json" -d @vuln-report.json https://trivy-report-registry.yourdomain.com/incomming-report
   ```
   Replace `report.json` with the filename of your pre-generated trivy vulnerability report.
