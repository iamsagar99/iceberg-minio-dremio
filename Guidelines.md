## First Create Docker Compose one by one:
-   docker-compose up notebook
-   docker-compose up minio
-   docker-compose up dremio   
-   docker-compose up nessie

### Notebook
- Get token url from the log and start
### Minio
- Read from log:
    -   S3API url at localhost:9000
    -   MinioUI at localhost:9001

### Nessie
-   Just start it

### dremio
-   http://localhost:9047/
-   steps to connect:
    1. Nessie Catalog:
        i. General 
            -   On data source add Nessie
            -   Give it some name like: nessie
            -   Nessie endpoint url: http://nessie:19120/api/v2
            -   Auth token none
        ii. Storage
            - First Open minio from localhost:9001 and create access keys
            - Give a s3 bucket name like warehouse/
            - Below there is connection properties , where need to fill following things:
                -     fs.s3a.path.style.access true
                -     dremio.s3.compat true
                -     fs.s3a.endpoint minio:9000
            - Don't need to encrypt in localhost
    Let's save then we can browse the catalog.

    2. Iceberg default catalog: 
        i. General 
            - Source Amazon s3 
            - give access keys
        ii. Advance options:
            Set the following true:
            - Enable asynchronous access when possible
            - Enable compatibility mode
            - Enable file status check
            Default CTAS format: Iceberg
            Root path: /
            fs.s3a.path.style.access true
            fs.s3a.endpoint minio:9000
    Let's save and connect.


 

            
