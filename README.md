# OpenMRS Patient Imaging module docker compose (Orthanc Integration)

## Overview

This project provides a Docker Compose setup for the OpenMRS 3.x Imaging frontend. It contains all the configuration files and libraries needed to run the application with Orthanc integration.

## Configure Your Local Orthanc Server

Update your orthanc setup by replacing and adding the following files:

- Replace/modify the existing `orthanc.json` in `/etc/orthanc` directory with the one from this project.

- Copy the Orthanc worklist script:

    ```bash
    cp orthancWorklist.py /etc/orthanc/
    ```
- Copy the Python plugin configuration:

    ```bash
    cp python.json /etc/orthanc/
    ``` 

## Orthanc Configuration in OpenMrS

To connect with Orthanc, add the following configuration:

- **URL**: `http://host.docker.internal:ORTHANC_PORT` 
  > **Note**: Not change `host.docker.internal`
- **Proxy URL**: `Your local orthanc URL`
- **User**: `orthanc`
- **Password**: `orthanc`

![Orthanc Configuration](/images/orthancConfiguration.png)


## Running the Container with Docker

- Start the Docker container:

    ```bash
    docker-compose up
    ```

    > **Note**  
    > - he installation process may take some time. You can monitor the progress of the setup by visiting
    > - In some cases, you may need to stop the container and restart it to complete the setup successfully.

    ```bash
    http://localhost/openmrs/initialsetup
    ```
    ![Installation](/images/installProcess.png)

- Remove the container

    ```bash
    docker-compose down    
    ```

## Running the Imaging Module

You have two options for running the Imaging module:

- Run via Docker (frontend image)

  > **Note** (Currently incomplete)

    - Start the frontend:

        ```bash
        http://localhost/openmrs/spa
        ```

    - Validate backend connection:

        ```bash
        http://localhost:8080/openmrs/spa
        ```

- Run the frontend locally (with Docker backend):
    To run the frontend on your local machine while using the OpenMRS backend running in Docker for development purposes, use:

    ```bash
    npm start -- --backend http://localhost:3030/
    ```

## Upload the imaging and necessay modules:
 Once the application is running, you will need to upload the required OpenMRS modules from the 'modules' folder within this project:

- imaging-1.1.2-SNAPSHOT.omod
- appui-1.18.0.omod
- uicommons-2.26.0.omod
- uiframework-4.0.0.omod
- appframework-2.18.0.omod

Link: http://localhost:8080/openmrs/admin/modules/module.list#markAllAsRead

![Upload moudles](/images/uploadModule.png)

## Links:
- Imaging frondend for OpenMRS3.x: https://github.com/sadrezhao/openmrs-esm-patient-imaging-app
- Imaging module (GUI+backend) for OpenMRS2.x: https://github.com/sadrezhao/openmrs-module-imaging
- Orthanc server: https://www.orthanc-server.com/download.php
- Imaging frontend (NPM release): https://www.npmjs.com/package/@zhaosadre/openmrs-esm-patient-imaging-app
- Imaging backend (release): https://github.com/sadrezhao/openmrs-module-imaging/releases


