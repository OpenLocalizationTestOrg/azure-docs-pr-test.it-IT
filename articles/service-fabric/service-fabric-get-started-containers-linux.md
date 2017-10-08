---
title: un'applicazione contenitore di Azure Service Fabric in Linux aaaCreate | Documenti Microsoft
description: Creare la prima applicazione contenitore Linux in Azure Service Fabric.  Creazione di un'immagine di Docker con l'applicazione, eseguire il push del Registro di sistema di hello immagine tooa contenitore, compilare e distribuire un'applicazione contenitore di Service Fabric.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 348dbcbaa1a534fb2808450e4c2d5f9acc7c7b35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-linux"></a>Creare la prima applicazione contenitore di Service Fabric in Linux
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started-containers.md)
> * [Linux](service-fabric-get-started-containers-linux.md)

Esecuzione di un'applicazione esistente in un contenitore di Linux in un cluster di Service Fabric non richiede tutte le applicazioni tooyour le modifiche. Questo articolo vengono illustrati la creazione di un'immagine Docker che contiene un Python [pallone](http://flask.pocoo.org/) distribuzione di cluster di Service Fabric tooa e l'applicazione web.  Si condividerà anche l'applicazione in contenitore tramite [Registro contenitori di Azure](/azure/container-registry/).  L'articolo presuppone una conoscenza di base di Docker. Per informazioni su Docker, lettura hello [Panoramica Docker](https://docs.docker.com/engine/understanding-docker/).

## <a name="prerequisites"></a>Prerequisiti
* Un computer di sviluppo che esegue:
  * [SDK e strumenti di Service Fabric](service-fabric-get-started-linux.md).
  * [Docker CE per Linux](https://docs.docker.com/engine/installation/#prior-releases). 
  * [Interfaccia della riga di comando di Service Fabric](service-fabric-cli.md)

* Un registro all'interno del registro contenitori di Azure. A questo scopo, [creare un registro contenitori](../container-registry/container-registry-get-started-portal.md) nella sottoscrizione di Azure. 

## <a name="define-hello-docker-container"></a>Definire contenitore Docker hello
Creare un'immagine basata su hello [immagine Python](https://hub.docker.com/_/python/) si trova nell'Hub Docker. 

Definire il contenitore Docker in un Dockerfile. Hello Dockerfile contiene istruzioni per l'impostazione di ambiente hello all'interno del contenitore, il caricamento di un'applicazione hello desiderato toorun e il mapping delle porte. Hello Dockerfile è hello input toohello `docker build` comando che crea l'immagine di hello. 

Creare una directory vuota e creare file hello *Dockerfile* (con alcuna estensione di file). Aggiungere il seguente troppo di hello*Dockerfile* e salvare le modifiche:

```
# Use an official Python runtime as a base image
FROM python:2.7-slim

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

Hello lettura [riferimento a Dockerfile](https://docs.docker.com/engine/reference/builder/) per ulteriori informazioni.

## <a name="create-a-simple-web-application"></a>Creare un'applicazione Web semplice
Creare un'applicazione Web Flask in ascolto sulla porta 80 che restituisce "Hello World!".  Nella stessa directory di hello, creare file hello *requirements.txt*.  Aggiungere il seguente hello e salvare le modifiche:
```
Flask
```

Creare anche hello *app.py* file e aggiungere hello seguenti:

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-hello-image"></a>Creazione immagine hello
Eseguire hello `docker build` toocreate hello comando che esegue l'applicazione web. Aprire una finestra di PowerShell e passare troppo*c:\temp\helloworldapp*. Eseguire hello comando seguente:

```bash
docker build -t helloworldapp .
```

Questo comando compilazioni hello nuova immagine con hello istruzioni del Dockerfile, denominazione (-t tag) immagine hello "helloworldapp". La creazione di un'immagine effettua il pull immagine di base hello verso il basso dall'Hub Docker e crea una nuova immagine che consente di aggiungere l'applicazione sopra l'immagine di base hello.  

Al termine del comando di compilazione hello, eseguire hello `docker images` informazioni toosee hello nuova immagine di comando:

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-hello-application-locally"></a>Eseguire un'applicazione hello in locale
Verificare che l'applicazione nei contenitori viene eseguita in locale prima di pubblicarlo del Registro di sistema di hello contenitore.  

Eseguire un'applicazione hello, mapping del contenitore di computer porta 4000 toohello esposte porta 80:

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

*nome* offre un toohello nome contenitore (invece di ID di contenitore hello) di esecuzione.

Connettersi toohello esecuzione contenitore.  Aprire un web browser che punta toohello l'indirizzo IP restituito nella porta 4000, ad esempio "http://localhost:4000". Dovrebbe essere hello titolo "Hello World!" visualizzare nel browser hello.

![Hello World!][hello-world]

toostop nel contenitore, eseguire:

```bash
docker stop my-web-site
```

Eliminare il contenitore di hello dal computer di sviluppo:

```bash
docker rm my-web-site
```

## <a name="push-hello-image-toohello-container-registry"></a>Eseguire il push del Registro di sistema di hello immagine toohello contenitore
Dopo aver verificato che l'applicazione hello viene eseguito in Docker, eseguire il push del Registro di sistema di hello immagine tooyour nel Registro di sistema contenitore di Azure.

Eseguire `docker login` toolog nel Registro di sistema tooyour contenitore con il [le credenziali del Registro di sistema](../container-registry/container-registry-authentication.md).

Hello seguente esempio passa hello ID e la password di Azure Active Directory [dell'entità servizio](../active-directory/active-directory-application-objects.md). Ad esempio, è stato assegnato un registro di sistema tooyour dell'entità servizio per uno scenario di automazione.  In alternativa, è possibile eseguire l'accesso usando il nome utente e la password del registro.

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Hello seguente comando crea un tag o l'alias dell'immagine di hello, con un registro di sistema tooyour il percorso completo. In questo esempio posizioni hello immagine hello `samples` disordine tooavoid dello spazio dei nomi nella directory radice del Registro di sistema hello hello.

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

Push del Registro di sistema di hello immagine tooyour contenitore:

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-hello-docker-image-with-yeoman"></a>Immagine di Docker hello del pacchetto con Yeoman
Hello Service Fabric SDK per Linux include un [Yeoman](http://yeoman.io/) generatore che rende facile toocreate l'applicazione e aggiungere un'immagine contenitore. Consente di usare Yeoman toocreate chiamata un'applicazione con un singolo contenitore Docker *SimpleContainerApp*.

toocreate un'applicazione contenitore di Service Fabric, aprire una finestra terminale ed eseguire `yo azuresfcontainer`.  

Assegnare un nome all'applicazione, ad esempio "mycontainer". 

Specificare hello URL di immagine contenitore hello nel Registro di sistema contenitore (ad esempio, ""). 

Questa immagine presenta un carico di lavoro del punto di ingresso definito, pertanto è necessario tooexplicitly specificare inpui comandi (comandi eseguiti all'interno di hello contenitore, in modo che i contenitori di hello in esecuzione dopo l'avvio). 

Specificare "1" come numero di istanze.

![Generatore Yeoman di Service Fabric per i contenitori][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a>Configurare il mapping delle porte e l'autenticazione per il repository del contenitore
Il servizio in contenitore richiede un endpoint per la comunicazione.  A questo punto aggiungere hello protocollo, porta e tipo tooan `Endpoint` nel file ServiceManifest.xml hello. Per questo articolo, il servizio contenitore hello in ascolto sulla porta 4000: 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
Fornendo hello `UriScheme` automaticamente registri hello endpoint del contenitore con hello servizio dei nomi dell'infrastruttura di servizio per l'individuazione. Un file di esempio ServiceManifest.xml completo viene fornito alla fine di hello di questo articolo. 

Configurare il mapping di porta del contenitore per ospitare porta hello specificando un `PortBinding` criteri in `ContainerHostPolicies` di file ApplicationManifest XML hello.  Per questo articolo, `ContainerPort` è 80 (contenitore hello espone la porta 80, come specificato in hello Dockerfile) e `EndpointRef` è "myserviceTypeEndpoint" (endpoint hello definiti nel manifesto del servizio hello).  Le richieste in ingresso del servizio sulla porta 4000 toohello sono mappati tooport 80 sul contenitore hello.  Se il contenitore deve tooauthenticate con un repository privato, quindi aggiungere `RepositoryCredentials`.  Per questo articolo, aggiungere il nome di account hello e la password del Registro di sistema di hello myregistry.azurecr.io contenitore. 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-hello-service-fabric-application"></a>Compilazione e del pacchetto dell'applicazione di Service Fabric hello
modelli di servizio dell'infrastruttura Yeoman Hello includono uno script di compilazione per [Gradle](https://gradle.org/), che è possibile utilizzare un'applicazione hello toobuild da hello terminal. toobuild e pacchetto applicazione hello, eseguire hello seguente:

```bash
cd mycontainer
gradle
```

## <a name="deploy-hello-application"></a>Distribuire un'applicazione hello
Una volta creata l'applicazione hello, è possibile distribuire cluster locale di toohello utilizzando hello servizio infrastruttura CLI.

Connettere il cluster di Service Fabric locale toohello.

```bash
sfctl cluster select --endpoint http://localhost:19080
```

Hello utilizzare lo script di installazione fornite in hello modello toocopy applicazione hello pacchetto archivio immagini toohello del cluster, registrare il tipo di applicazione hello e creare un'istanza di un'applicazione hello.

```bash
./install.sh
```

Aprire un browser e passare tooService Fabric Explorer in http://localhost:19080/Esplora (sostituire localhost con indirizzo IP privato di hello di hello VM se utilizza Vagrant su Mac OS X). Espandere il nodo di applicazioni hello e si noti che è ora disponibile una voce per il tipo di applicazione e un altro per hello prima istanza di quel tipo.

Connettersi toohello esecuzione contenitore.  Aprire un web browser che punta toohello l'indirizzo IP restituito nella porta 4000, ad esempio "http://localhost:4000". Dovrebbe essere hello titolo "Hello World!" visualizzare nel browser hello.

![Hello World!][hello-world]

## <a name="clean-up"></a>Eseguire la pulizia
Utilizza script di disinstallazione hello fornito nell'istanza dell'applicazione hello hello modello toodelete dal cluster di sviluppo locale hello e annullare la registrazione del tipo di applicazione hello.

```bash
./uninstall.sh
```

Dopo che si esegue il push del Registro di sistema di hello immagine toohello contenitore è possibile eliminare l'immagine locale hello dal computer di sviluppo:

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a>Manifesti di esempio completi del servizio e dell'applicazione di Service Fabric
Ecco completa del servizio hello e i manifesti dell'applicazione utilizzate in questo articolo.

### <a name="servicemanifestxml"></a>ServiceManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="myservicePkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="myserviceType" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers 
      tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
        <Commands></Commands>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->
    
    <EnvironmentVariables>
      <!--
      <EnvironmentVariable Name="VariableName" Value="VariableValue"/>
      -->
    </EnvironmentVariables>
    
  </CodePackage>

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a>ApplicationManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="mycontainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion 
       should match hello Name and Version attributes of hello ServiceManifest element defined in hello 
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="myservicePkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
      </ContainerHostPolicies>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using hello 
         ServiceFabric PowerShell module.
         
         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="myservice">
      <!-- On a local development cluster, set InstanceCount too1.  On a multi-node production 
      cluster, set InstanceCount too-1 for hello container service toorun on every node in 
      hello cluster.
      -->
      <StatelessService ServiceTypeName="myserviceType" InstanceCount="1">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```
## <a name="adding-more-services-tooan-existing-application"></a>Aggiunta di ulteriori servizi tooan esistente dell'applicazione

eseguire un altro contenitore servizio tooan applicazione già creata mediante yeoman, tooadd hello i passaggi seguenti:

1. Cambiare directory toohello principale di un'applicazione hello esistente.  Ad esempio, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` è un'applicazione hello creata da Yeoman.
2. Eseguire `yo azuresfcontainer:AddService`

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a>Configurare l'intervallo di tempo prima della terminazione forzata del contenitore

È possibile configurare un intervallo di tempo per hello runtime toowait prima contenitore hello viene rimosso dopo hello eliminazione servizio (o un nodo di spostamento tooanother) è stata avviata. Intervallo di tempo hello configurazione invia hello `docker stop <time in seconds>` contenitore toohello di comando.   Per altri dettagli, vedere [docker stop](https://docs.docker.com/engine/reference/commandline/stop/). toowait intervallo di tempo Hello viene specificato sotto hello `Hosting` sezione. Hello seguente frammento di codice del manifesto del cluster viene illustrato come intervallo di attesa tooset hello:

```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "ContainerDeactivationTimeout": "10",
          ...
          }
        ]
}
```
Hello intervallo di tempo predefinito è impostato too10 secondi. Poiché questa configurazione è dinamica, una configurazione aggiornare solo in caso di timeout hello aggiornamenti cluster hello. 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a>Configurare hello runtime tooremove immagini contenitore inutilizzati

È possibile configurare hello Service Fabric cluster tooremove immagini contenitore inutilizzati dal nodo hello. Questa configurazione consente toobe di spazio su disco liberare se sono presenti nel nodo hello troppi immagini contenitore.  tooenable questa funzionalità, l'aggiornamento hello `Hosting` sezione manifesto del cluster hello come illustrato nel seguente frammento di codice hello: 


```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "PruneContainerImages": “True”,
            "ContainerImagesToSkip": "microsoft/windowsservercore|microsoft/nanoserver|…",
          ...
          }
        ]
} 
```

Per le immagini che non devono essere eliminate, è possibile specificarle in hello `ContainerImagesToSkip` parametro. 


## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni sull'esecuzione di [contenitori in Service Fabric](service-fabric-containers-overview.md).
* Hello lettura [distribuire un'applicazione .NET in un contenitore](service-fabric-host-app-in-a-container.md) esercitazione.
* Informazioni su Service Fabric hello [del ciclo di vita dell'applicazione](service-fabric-application-lifecycle.md).
* Hello estrazione [esempi di codice di Service Fabric contenitore](https://github.com/Azure-Samples/service-fabric-dotnet-containers) su GitHub.

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
