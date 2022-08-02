# Azure Container Apps

Permite ejecutar microservicios y aplicaciones contenedorizadas en una plataforma sin servidor, no tiene en cuenta el entorno de ejecución o el modelo de programación. Con Container Apps, puede puede sacar provecho de las ventajas de ejecutar contenedores y, al mismo tiempo, olvidarse de administrar la infraestructura en la nube y orquestadores de contenedores complejos.

![image](https://user-images.githubusercontent.com/17581842/179627943-0f43598b-e6cb-4fd5-89de-12a155109e50.png)

# Características

- [Ejecutar varias revisiones](https://docs.microsoft.com/es-mx/azure/container-apps/application-lifecycle-management) del contenedor y administrar el ciclo de vida de la aplicación del contenedor.

- [Escalar automáticamente](https://docs.microsoft.com/es-mx/azure/container-apps/scale-app) las aplicaciones en función de cualquier desencadenador de escalado compatible con KEDA. La mayoría de las aplicaciones se pueden escalar a cero 1.

- [Habilitar la entrada HTTPS](https://docs.microsoft.com/es-mx/azure/container-apps/ingress?tabs=bash) sin tener que administrar otra infraestructura de Azure.

- [Dividir el tráfico](https://docs.microsoft.com/es-mx/azure/container-apps/revisions) entre varias versiones de una aplicación.

- [Usar la entrada interna](https://docs.microsoft.com/es-mx/azure/container-apps/connect-apps?tabs=bash) y la detección de servicios para proteger los puntos de conexión solo internos con la detección de servicios basada en DNS integrada.

- [Crear microservicios con Dapr](https://docs.microsoft.com/es-mx/azure/container-apps/microservices) y acceder a su amplio conjunto de API.

- [Ejecutar contenedores desde cualquier registro](https://docs.microsoft.com/es-mx/azure/container-apps/containers), público o privado, incluidos Docker Hub y Azure Container Registry (ACR).

- [Usar la extensión CLI de Azure o plantillas de ARM](https://docs.microsoft.com/es-mx/azure/container-apps/get-started?tabs=bash) para administrar las aplicaciones.

- [Proporcionar una red virtual existente](https://docs.microsoft.com/es-mx/azure/container-apps/vnet-custom?tabs=bash&pivots=azure-portal) al crear un entorno para las aplicaciones de contenedor.

- [Administrar secretos de forma segura](https://docs.microsoft.com/es-mx/azure/container-apps/manage-secrets?tabs=arm-template) directamente en una aplicación.

- [Ver los registros de aplicaciones](https://docs.microsoft.com/es-mx/azure/container-apps/monitor?tabs=bash) mediante Azure Log Analytics.

# Arquitectura

Conectividad privada a través de la infraestructura de red virtual.

![AzureContainerApps (2)](https://user-images.githubusercontent.com/17581842/179628279-0648eb25-5b03-4b47-91aa-a008eb29a0b8.png)


# Despliegue

## Red Virtual

```bash
az network vnet create --name VN-CONTAINER-APP --address-prefix 10.0.0.0/16 --resource-group SORDONEZR --subnet-name default
```

![image](https://user-images.githubusercontent.com/17581842/179633862-5050c6b9-1417-47e8-83a3-52ce20908b7f.png)

## Sub Red

```bash
az network vnet subnet create -n SN-CONTAINER-APP --vnet-name VN-CONTAINER-APP -g SORDONEZR --address-prefixes "10.0.0.0/23"
```

![image](https://user-images.githubusercontent.com/17581842/179634108-c7ea6019-94be-44de-8257-2075d9619bfd.png)

## Área de trabajo de Log Analytics

```bash
az monitor log-analytics workspace create -g SORDONEZR -n workspacecontainerapp -l eastus
```
![image](https://user-images.githubusercontent.com/17581842/179634583-b67886b6-2596-458f-8e30-6ccb6d436f76.png)

## Registro de contenedor

![image](https://user-images.githubusercontent.com/17581842/179634654-47b09896-fa31-489a-9ace-499fa6872621.png)

## Zona DNS privada

![image](https://user-images.githubusercontent.com/17581842/182390595-37b170b5-e40a-48c8-b419-8579236acde8.png)

![image](https://user-images.githubusercontent.com/17581842/179634763-3c1ecd42-4579-4726-9c27-565a11e2b642.png)

![image](https://user-images.githubusercontent.com/17581842/179634811-6633c767-8dc7-4622-817c-42f55f3c8297.png)


![image](https://user-images.githubusercontent.com/17581842/179631367-fb3e88f7-c308-4cdb-a1d2-70cbb0382570.png)

Se puede crear el área de trabajo de Log Analytics previamente y seleccionarla o crearla desde el asistente.

![image](https://user-images.githubusercontent.com/17581842/179631463-b696ae8b-2f38-4be0-a398-09677652674b.png)

Se puede crear la red virtual previamente y seleccionarla o crearla desde el asistente.

![image](https://user-images.githubusercontent.com/17581842/179631678-809d708b-9d53-4122-8c85-6a90599de7e9.png)

Una vez creado el entorno ya podemos crear aplicaciones y asociarlas al mismo.

![image](https://user-images.githubusercontent.com/17581842/179632290-3d6aca85-fc87-4a6a-bf65-826fbacacfef.png)

![image](https://user-images.githubusercontent.com/17581842/179632459-19626134-6691-4c79-9d55-dc315159527d.png)

![image](https://user-images.githubusercontent.com/17581842/179632587-973202cc-a278-42a9-9b09-0f538a376a5e.png)

## Realizando pruebas en una maquina virtual que se integra a la red virtual

![image](https://user-images.githubusercontent.com/17581842/179635126-f2eb7a3f-8e81-4ffc-9c7f-533c0fb1ed82.png)

![image](https://user-images.githubusercontent.com/17581842/179635013-0b4bc60e-e6ae-4c81-84d6-1c359dfbb512.png)

![image](https://user-images.githubusercontent.com/17581842/179635067-cebd9ab4-8cc4-4a92-b538-197f59aa96aa.png)


# Integracion con GitHub CI/CD

![image](https://user-images.githubusercontent.com/17581842/179635455-36555f56-a2b2-43cc-8796-1106b430c7e3.png)

## Workflow

```yml

name: Trigger auto deployment for containerapp

# When this action will be executed
on:
  # Automatically trigger it when detected changes in repo
  push:
    branches: 
      [ main ]
    paths:
    - '**'
    - '.github/workflows/containerapp-AutoDeployTrigger-cbafa6ac-44be-42d6-bb0f-225327d5c843.yml'

  # Allow mannually trigger 
  workflow_dispatch:      

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout to the branch
        uses: actions/checkout@v2

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v1

      - name: Log in to container registry
        uses: docker/login-action@v1
        with:
          registry: crsordonezr.azurecr.io
          username: ${{ secrets.CONTAINERAPP_REGISTRY_USERNAME }}
          password: ${{ secrets.CONTAINERAPP_REGISTRY_PASSWORD }}

      - name: Build and push container image to registry
        uses: docker/build-push-action@v2
        with:
          push: true
          tags: crsordonezr.azurecr.io/containerapp:${{ github.sha }}
          file: ./Dockerfile
          context: ./


  deploy:
    runs-on: ubuntu-latest
    needs: build
    
    steps:
      - name: Azure Login
        uses: azure/login@v1
        with:
          creds: ${{ secrets.CONTAINERAPP_AZURE_CREDENTIALS }}


      - name: Deploy to containerapp
        uses: azure/CLI@v1
        with:
          inlineScript: |
            az config set extension.use_dynamic_install=yes_without_prompt
            az containerapp registry set -n containerapp -g SORDONEZR --server crsordonezr.azurecr.io --username  ${{ secrets.CONTAINERAPP_REGISTRY_USERNAME }} --password ${{ secrets.CONTAINERAPP_REGISTRY_PASSWORD }}
            az containerapp update -n containerapp -g SORDONEZR --image crsordonezr.azurecr.io/containerapp:${{ github.sha }}

```
![image](https://user-images.githubusercontent.com/17581842/179636141-98af181a-59a8-4936-a11a-6060d7449588.png)


