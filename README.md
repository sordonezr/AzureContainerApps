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

![image](https://user-images.githubusercontent.com/17581842/179631367-fb3e88f7-c308-4cdb-a1d2-70cbb0382570.png)

Se puede crear el área de trabajo de Log Analytics previamente y seleccionarla o crearla desde el asistente.

![image](https://user-images.githubusercontent.com/17581842/179631463-b696ae8b-2f38-4be0-a398-09677652674b.png)

Se puede crear la red virtual previamente y seleccionarla o crearla desde el asistente.

![image](https://user-images.githubusercontent.com/17581842/179631678-809d708b-9d53-4122-8c85-6a90599de7e9.png)

Una vez creado el entorno ya podemos crear aplicaciones y asociarlas al mismo.

![image](https://user-images.githubusercontent.com/17581842/179632290-3d6aca85-fc87-4a6a-bf65-826fbacacfef.png)

![image](https://user-images.githubusercontent.com/17581842/179632459-19626134-6691-4c79-9d55-dc315159527d.png)

![image](https://user-images.githubusercontent.com/17581842/179632587-973202cc-a278-42a9-9b09-0f538a376a5e.png)




# Integración de red virtual con Azure Container Apps
