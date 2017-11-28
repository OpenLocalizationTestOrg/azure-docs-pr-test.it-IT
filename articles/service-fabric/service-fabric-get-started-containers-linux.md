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
# <a name="create-your-first-service-fabric-container-application-on-linux"></a><span data-ttu-id="1b62a-104">Creare la prima applicazione contenitore di Service Fabric in Linux</span><span class="sxs-lookup"><span data-stu-id="1b62a-104">Create your first Service Fabric container application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1b62a-105">Windows</span><span class="sxs-lookup"><span data-stu-id="1b62a-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="1b62a-106">Linux</span><span class="sxs-lookup"><span data-stu-id="1b62a-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="1b62a-107">Esecuzione di un'applicazione esistente in un contenitore di Linux in un cluster di Service Fabric non richiede tutte le applicazioni tooyour le modifiche.</span><span class="sxs-lookup"><span data-stu-id="1b62a-107">Running an existing application in a Linux container on a Service Fabric cluster doesn't require any changes tooyour application.</span></span> <span data-ttu-id="1b62a-108">Questo articolo vengono illustrati la creazione di un'immagine Docker che contiene un Python [pallone](http://flask.pocoo.org/) distribuzione di cluster di Service Fabric tooa e l'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="1b62a-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it tooa Service Fabric cluster.</span></span>  <span data-ttu-id="1b62a-109">Si condividerà anche l'applicazione in contenitore tramite [Registro contenitori di Azure](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="1b62a-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="1b62a-110">L'articolo presuppone una conoscenza di base di Docker.</span><span class="sxs-lookup"><span data-stu-id="1b62a-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="1b62a-111">Per informazioni su Docker, lettura hello [Panoramica Docker](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="1b62a-111">You can learn about Docker by reading hello [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b62a-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1b62a-112">Prerequisites</span></span>
* <span data-ttu-id="1b62a-113">Un computer di sviluppo che esegue:</span><span class="sxs-lookup"><span data-stu-id="1b62a-113">A development computer running:</span></span>
  * <span data-ttu-id="1b62a-114">[SDK e strumenti di Service Fabric](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1b62a-114">[Service Fabric SDK and tools](service-fabric-get-started-linux.md).</span></span>
  * <span data-ttu-id="1b62a-115">[Docker CE per Linux](https://docs.docker.com/engine/installation/#prior-releases).</span><span class="sxs-lookup"><span data-stu-id="1b62a-115">[Docker CE for Linux](https://docs.docker.com/engine/installation/#prior-releases).</span></span> 
  * [<span data-ttu-id="1b62a-116">Interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1b62a-116">Service Fabric CLI</span></span>](service-fabric-cli.md)

* <span data-ttu-id="1b62a-117">Un registro all'interno del registro contenitori di Azure. A questo scopo, [creare un registro contenitori](../container-registry/container-registry-get-started-portal.md) nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b62a-117">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span> 

## <a name="define-hello-docker-container"></a><span data-ttu-id="1b62a-118">Definire contenitore Docker hello</span><span class="sxs-lookup"><span data-stu-id="1b62a-118">Define hello Docker container</span></span>
<span data-ttu-id="1b62a-119">Creare un'immagine basata su hello [immagine Python](https://hub.docker.com/_/python/) si trova nell'Hub Docker.</span><span class="sxs-lookup"><span data-stu-id="1b62a-119">Build an image based on hello [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span> 

<span data-ttu-id="1b62a-120">Definire il contenitore Docker in un Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="1b62a-120">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="1b62a-121">Hello Dockerfile contiene istruzioni per l'impostazione di ambiente hello all'interno del contenitore, il caricamento di un'applicazione hello desiderato toorun e il mapping delle porte.</span><span class="sxs-lookup"><span data-stu-id="1b62a-121">hello Dockerfile contains instructions for setting up hello environment inside your container, loading hello application you want toorun, and mapping ports.</span></span> <span data-ttu-id="1b62a-122">Hello Dockerfile è hello input toohello `docker build` comando che crea l'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="1b62a-122">hello Dockerfile is hello input toohello `docker build` command, which creates hello image.</span></span> 

<span data-ttu-id="1b62a-123">Creare una directory vuota e creare file hello *Dockerfile* (con alcuna estensione di file).</span><span class="sxs-lookup"><span data-stu-id="1b62a-123">Create an empty directory and create hello file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="1b62a-124">Aggiungere il seguente troppo di hello*Dockerfile* e salvare le modifiche:</span><span class="sxs-lookup"><span data-stu-id="1b62a-124">Add hello following too*Dockerfile* and save your changes:</span></span>

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

<span data-ttu-id="1b62a-125">Hello lettura [riferimento a Dockerfile](https://docs.docker.com/engine/reference/builder/) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="1b62a-125">Read hello [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="1b62a-126">Creare un'applicazione Web semplice</span><span class="sxs-lookup"><span data-stu-id="1b62a-126">Create a simple web application</span></span>
<span data-ttu-id="1b62a-127">Creare un'applicazione Web Flask in ascolto sulla porta 80 che restituisce "Hello World!".</span><span class="sxs-lookup"><span data-stu-id="1b62a-127">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="1b62a-128">Nella stessa directory di hello, creare file hello *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="1b62a-128">In hello same directory, create hello file *requirements.txt*.</span></span>  <span data-ttu-id="1b62a-129">Aggiungere il seguente hello e salvare le modifiche:</span><span class="sxs-lookup"><span data-stu-id="1b62a-129">Add hello following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="1b62a-130">Creare anche hello *app.py* file e aggiungere hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="1b62a-130">Also create hello *app.py* file and add hello following:</span></span>

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-hello-image"></a><span data-ttu-id="1b62a-131">Creazione immagine hello</span><span class="sxs-lookup"><span data-stu-id="1b62a-131">Build hello image</span></span>
<span data-ttu-id="1b62a-132">Eseguire hello `docker build` toocreate hello comando che esegue l'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="1b62a-132">Run hello `docker build` command toocreate hello image that runs your web application.</span></span> <span data-ttu-id="1b62a-133">Aprire una finestra di PowerShell e passare troppo*c:\temp\helloworldapp*.</span><span class="sxs-lookup"><span data-stu-id="1b62a-133">Open a PowerShell window and navigate too*c:\temp\helloworldapp*.</span></span> <span data-ttu-id="1b62a-134">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1b62a-134">Run hello following command:</span></span>

```bash
docker build -t helloworldapp .
```

<span data-ttu-id="1b62a-135">Questo comando compilazioni hello nuova immagine con hello istruzioni del Dockerfile, denominazione (-t tag) immagine hello "helloworldapp".</span><span class="sxs-lookup"><span data-stu-id="1b62a-135">This command builds hello new image using hello instructions in your Dockerfile, naming (-t tagging) hello image "helloworldapp".</span></span> <span data-ttu-id="1b62a-136">La creazione di un'immagine effettua il pull immagine di base hello verso il basso dall'Hub Docker e crea una nuova immagine che consente di aggiungere l'applicazione sopra l'immagine di base hello.</span><span class="sxs-lookup"><span data-stu-id="1b62a-136">Building an image pulls hello base image down from Docker Hub and creates a new image that adds your application on top of hello base image.</span></span>  

<span data-ttu-id="1b62a-137">Al termine del comando di compilazione hello, eseguire hello `docker images` informazioni toosee hello nuova immagine di comando:</span><span class="sxs-lookup"><span data-stu-id="1b62a-137">Once hello build command completes, run hello `docker images` command toosee information on hello new image:</span></span>

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="1b62a-138">Eseguire un'applicazione hello in locale</span><span class="sxs-lookup"><span data-stu-id="1b62a-138">Run hello application locally</span></span>
<span data-ttu-id="1b62a-139">Verificare che l'applicazione nei contenitori viene eseguita in locale prima di pubblicarlo del Registro di sistema di hello contenitore.</span><span class="sxs-lookup"><span data-stu-id="1b62a-139">Verify that your containerized application runs locally before pushing it hello container registry.</span></span>  

<span data-ttu-id="1b62a-140">Eseguire un'applicazione hello, mapping del contenitore di computer porta 4000 toohello esposte porta 80:</span><span class="sxs-lookup"><span data-stu-id="1b62a-140">Run hello application, mapping your computer's port 4000 toohello container's exposed port 80:</span></span>

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

<span data-ttu-id="1b62a-141">*nome* offre un toohello nome contenitore (invece di ID di contenitore hello) di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1b62a-141">*name* gives a name toohello running container (instead of hello container ID).</span></span>

<span data-ttu-id="1b62a-142">Connettersi toohello esecuzione contenitore.</span><span class="sxs-lookup"><span data-stu-id="1b62a-142">Connect toohello running container.</span></span>  <span data-ttu-id="1b62a-143">Aprire un web browser che punta toohello l'indirizzo IP restituito nella porta 4000, ad esempio "http://localhost:4000".</span><span class="sxs-lookup"><span data-stu-id="1b62a-143">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="1b62a-144">Dovrebbe essere hello titolo "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="1b62a-144">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="1b62a-145">visualizzare nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="1b62a-145">display in hello browser.</span></span>

![Hello World!][hello-world]

<span data-ttu-id="1b62a-147">toostop nel contenitore, eseguire:</span><span class="sxs-lookup"><span data-stu-id="1b62a-147">toostop your container, run:</span></span>

```bash
docker stop my-web-site
```

<span data-ttu-id="1b62a-148">Eliminare il contenitore di hello dal computer di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="1b62a-148">Delete hello container from your development machine:</span></span>

```bash
docker rm my-web-site
```

## <a name="push-hello-image-toohello-container-registry"></a><span data-ttu-id="1b62a-149">Eseguire il push del Registro di sistema di hello immagine toohello contenitore</span><span class="sxs-lookup"><span data-stu-id="1b62a-149">Push hello image toohello container registry</span></span>
<span data-ttu-id="1b62a-150">Dopo aver verificato che l'applicazione hello viene eseguito in Docker, eseguire il push del Registro di sistema di hello immagine tooyour nel Registro di sistema contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b62a-150">After you verify that hello application runs in Docker, push hello image tooyour registry in Azure Container Registry.</span></span>

<span data-ttu-id="1b62a-151">Eseguire `docker login` toolog nel Registro di sistema tooyour contenitore con il [le credenziali del Registro di sistema](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1b62a-151">Run `docker login` toolog in tooyour container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="1b62a-152">Hello seguente esempio passa hello ID e la password di Azure Active Directory [dell'entità servizio](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="1b62a-152">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="1b62a-153">Ad esempio, è stato assegnato un registro di sistema tooyour dell'entità servizio per uno scenario di automazione.</span><span class="sxs-lookup"><span data-stu-id="1b62a-153">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span>  <span data-ttu-id="1b62a-154">In alternativa, è possibile eseguire l'accesso usando il nome utente e la password del registro.</span><span class="sxs-lookup"><span data-stu-id="1b62a-154">Or, you could login using your registry username and password.</span></span>

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="1b62a-155">Hello seguente comando crea un tag o l'alias dell'immagine di hello, con un registro di sistema tooyour il percorso completo.</span><span class="sxs-lookup"><span data-stu-id="1b62a-155">hello following command creates a tag, or alias, of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="1b62a-156">In questo esempio posizioni hello immagine hello `samples` disordine tooavoid dello spazio dei nomi nella directory radice del Registro di sistema hello hello.</span><span class="sxs-lookup"><span data-stu-id="1b62a-156">This example places hello image in hello `samples` namespace tooavoid clutter in hello root of hello registry.</span></span>

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="1b62a-157">Push del Registro di sistema di hello immagine tooyour contenitore:</span><span class="sxs-lookup"><span data-stu-id="1b62a-157">Push hello image tooyour container registry:</span></span>

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-hello-docker-image-with-yeoman"></a><span data-ttu-id="1b62a-158">Immagine di Docker hello del pacchetto con Yeoman</span><span class="sxs-lookup"><span data-stu-id="1b62a-158">Package hello Docker image with Yeoman</span></span>
<span data-ttu-id="1b62a-159">Hello Service Fabric SDK per Linux include un [Yeoman](http://yeoman.io/) generatore che rende facile toocreate l'applicazione e aggiungere un'immagine contenitore.</span><span class="sxs-lookup"><span data-stu-id="1b62a-159">hello Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy toocreate your application and add a container image.</span></span> <span data-ttu-id="1b62a-160">Consente di usare Yeoman toocreate chiamata un'applicazione con un singolo contenitore Docker *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="1b62a-160">Let's use Yeoman toocreate an application with a single Docker container called *SimpleContainerApp*.</span></span>

<span data-ttu-id="1b62a-161">toocreate un'applicazione contenitore di Service Fabric, aprire una finestra terminale ed eseguire `yo azuresfcontainer`.</span><span class="sxs-lookup"><span data-stu-id="1b62a-161">toocreate a Service Fabric container application, open a terminal window and run `yo azuresfcontainer`.</span></span>  

<span data-ttu-id="1b62a-162">Assegnare un nome all'applicazione, ad esempio "mycontainer".</span><span class="sxs-lookup"><span data-stu-id="1b62a-162">Name your application (for example, "mycontainer").</span></span> 

<span data-ttu-id="1b62a-163">Specificare hello URL di immagine contenitore hello nel Registro di sistema contenitore (ad esempio, "").</span><span class="sxs-lookup"><span data-stu-id="1b62a-163">Provide hello URL for hello container image in a container registry (for example, "").</span></span> 

<span data-ttu-id="1b62a-164">Questa immagine presenta un carico di lavoro del punto di ingresso definito, pertanto è necessario tooexplicitly specificare inpui comandi (comandi eseguiti all'interno di hello contenitore, in modo che i contenitori di hello in esecuzione dopo l'avvio).</span><span class="sxs-lookup"><span data-stu-id="1b62a-164">This image has a workload entry-point defined, so need tooexplicitly specify input commands (commands run inside hello container, which will keep hello container running after startup).</span></span> 

<span data-ttu-id="1b62a-165">Specificare "1" come numero di istanze.</span><span class="sxs-lookup"><span data-stu-id="1b62a-165">Specify an instance count of "1".</span></span>

![Generatore Yeoman di Service Fabric per i contenitori][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a><span data-ttu-id="1b62a-167">Configurare il mapping delle porte e l'autenticazione per il repository del contenitore</span><span class="sxs-lookup"><span data-stu-id="1b62a-167">Configure port mapping and container repository authentication</span></span>
<span data-ttu-id="1b62a-168">Il servizio in contenitore richiede un endpoint per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="1b62a-168">Your containerized service needs an endpoint for communication.</span></span>  <span data-ttu-id="1b62a-169">A questo punto aggiungere hello protocollo, porta e tipo tooan `Endpoint` nel file ServiceManifest.xml hello.</span><span class="sxs-lookup"><span data-stu-id="1b62a-169">Now add hello protocol, port, and type tooan `Endpoint` in hello ServiceManifest.xml file.</span></span> <span data-ttu-id="1b62a-170">Per questo articolo, il servizio contenitore hello in ascolto sulla porta 4000:</span><span class="sxs-lookup"><span data-stu-id="1b62a-170">For this article, hello containerized service listens on port 4000:</span></span> 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
<span data-ttu-id="1b62a-171">Fornendo hello `UriScheme` automaticamente registri hello endpoint del contenitore con hello servizio dei nomi dell'infrastruttura di servizio per l'individuazione.</span><span class="sxs-lookup"><span data-stu-id="1b62a-171">Providing hello `UriScheme` automatically registers hello container endpoint with hello Service Fabric Naming service for discoverability.</span></span> <span data-ttu-id="1b62a-172">Un file di esempio ServiceManifest.xml completo viene fornito alla fine di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="1b62a-172">A full ServiceManifest.xml example file is provided at hello end of this article.</span></span> 

<span data-ttu-id="1b62a-173">Configurare il mapping di porta del contenitore per ospitare porta hello specificando un `PortBinding` criteri in `ContainerHostPolicies` di file ApplicationManifest XML hello.</span><span class="sxs-lookup"><span data-stu-id="1b62a-173">Configure hello container port-to-host port mapping by specifying a `PortBinding` policy in `ContainerHostPolicies` of hello ApplicationManifest.xml file.</span></span>  <span data-ttu-id="1b62a-174">Per questo articolo, `ContainerPort` è 80 (contenitore hello espone la porta 80, come specificato in hello Dockerfile) e `EndpointRef` è "myserviceTypeEndpoint" (endpoint hello definiti nel manifesto del servizio hello).</span><span class="sxs-lookup"><span data-stu-id="1b62a-174">For this article, `ContainerPort` is 80 (hello container exposes port 80, as specified in hello Dockerfile) and `EndpointRef` is "myserviceTypeEndpoint" (hello endpoint defined in hello service manifest).</span></span>  <span data-ttu-id="1b62a-175">Le richieste in ingresso del servizio sulla porta 4000 toohello sono mappati tooport 80 sul contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="1b62a-175">Incoming requests toohello service on port 4000 are mapped tooport 80 on hello container.</span></span>  <span data-ttu-id="1b62a-176">Se il contenitore deve tooauthenticate con un repository privato, quindi aggiungere `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="1b62a-176">If your container needs tooauthenticate with a private repository, then add `RepositoryCredentials`.</span></span>  <span data-ttu-id="1b62a-177">Per questo articolo, aggiungere il nome di account hello e la password del Registro di sistema di hello myregistry.azurecr.io contenitore.</span><span class="sxs-lookup"><span data-stu-id="1b62a-177">For this article, add hello account name and password for hello myregistry.azurecr.io container registry.</span></span> 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-hello-service-fabric-application"></a><span data-ttu-id="1b62a-178">Compilazione e del pacchetto dell'applicazione di Service Fabric hello</span><span class="sxs-lookup"><span data-stu-id="1b62a-178">Build and package hello Service Fabric application</span></span>
<span data-ttu-id="1b62a-179">modelli di servizio dell'infrastruttura Yeoman Hello includono uno script di compilazione per [Gradle](https://gradle.org/), che è possibile utilizzare un'applicazione hello toobuild da hello terminal.</span><span class="sxs-lookup"><span data-stu-id="1b62a-179">hello Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use toobuild hello application from hello terminal.</span></span> <span data-ttu-id="1b62a-180">toobuild e pacchetto applicazione hello, eseguire hello seguente:</span><span class="sxs-lookup"><span data-stu-id="1b62a-180">toobuild and package hello application, run hello following:</span></span>

```bash
cd mycontainer
gradle
```

## <a name="deploy-hello-application"></a><span data-ttu-id="1b62a-181">Distribuire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="1b62a-181">Deploy hello application</span></span>
<span data-ttu-id="1b62a-182">Una volta creata l'applicazione hello, è possibile distribuire cluster locale di toohello utilizzando hello servizio infrastruttura CLI.</span><span class="sxs-lookup"><span data-stu-id="1b62a-182">Once hello application is built, you can deploy it toohello local cluster using hello Service Fabric CLI.</span></span>

<span data-ttu-id="1b62a-183">Connettere il cluster di Service Fabric locale toohello.</span><span class="sxs-lookup"><span data-stu-id="1b62a-183">Connect toohello local Service Fabric cluster.</span></span>

```bash
sfctl cluster select --endpoint http://localhost:19080
```

<span data-ttu-id="1b62a-184">Hello utilizzare lo script di installazione fornite in hello modello toocopy applicazione hello pacchetto archivio immagini toohello del cluster, registrare il tipo di applicazione hello e creare un'istanza di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1b62a-184">Use hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

```bash
./install.sh
```

<span data-ttu-id="1b62a-185">Aprire un browser e passare tooService Fabric Explorer in http://localhost:19080/Esplora (sostituire localhost con indirizzo IP privato di hello di hello VM se utilizza Vagrant su Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="1b62a-185">Open a browser and navigate tooService Fabric Explorer at http://localhost:19080/Explorer (replace localhost with hello private IP of hello VM if using Vagrant on Mac OS X).</span></span> <span data-ttu-id="1b62a-186">Espandere il nodo di applicazioni hello e si noti che è ora disponibile una voce per il tipo di applicazione e un altro per hello prima istanza di quel tipo.</span><span class="sxs-lookup"><span data-stu-id="1b62a-186">Expand hello Applications node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

<span data-ttu-id="1b62a-187">Connettersi toohello esecuzione contenitore.</span><span class="sxs-lookup"><span data-stu-id="1b62a-187">Connect toohello running container.</span></span>  <span data-ttu-id="1b62a-188">Aprire un web browser che punta toohello l'indirizzo IP restituito nella porta 4000, ad esempio "http://localhost:4000".</span><span class="sxs-lookup"><span data-stu-id="1b62a-188">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="1b62a-189">Dovrebbe essere hello titolo "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="1b62a-189">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="1b62a-190">visualizzare nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="1b62a-190">display in hello browser.</span></span>

![Hello World!][hello-world]

## <a name="clean-up"></a><span data-ttu-id="1b62a-192">Eseguire la pulizia</span><span class="sxs-lookup"><span data-stu-id="1b62a-192">Clean up</span></span>
<span data-ttu-id="1b62a-193">Utilizza script di disinstallazione hello fornito nell'istanza dell'applicazione hello hello modello toodelete dal cluster di sviluppo locale hello e annullare la registrazione del tipo di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1b62a-193">Use hello uninstall script provided in hello template toodelete hello application instance from hello local development cluster and unregister hello application type.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="1b62a-194">Dopo che si esegue il push del Registro di sistema di hello immagine toohello contenitore è possibile eliminare l'immagine locale hello dal computer di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="1b62a-194">After you push hello image toohello container registry you can delete hello local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="1b62a-195">Manifesti di esempio completi del servizio e dell'applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1b62a-195">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="1b62a-196">Ecco completa del servizio hello e i manifesti dell'applicazione utilizzate in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="1b62a-196">Here are hello complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="1b62a-197">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="1b62a-197">ServiceManifest.xml</span></span>
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
### <a name="applicationmanifestxml"></a><span data-ttu-id="1b62a-198">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="1b62a-198">ApplicationManifest.xml</span></span>
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
## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="1b62a-199">Aggiunta di ulteriori servizi tooan esistente dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="1b62a-199">Adding more services tooan existing application</span></span>

<span data-ttu-id="1b62a-200">eseguire un altro contenitore servizio tooan applicazione già creata mediante yeoman, tooadd hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1b62a-200">tooadd another container service tooan application already created using yeoman, perform hello following steps:</span></span>

1. <span data-ttu-id="1b62a-201">Cambiare directory toohello principale di un'applicazione hello esistente.</span><span class="sxs-lookup"><span data-stu-id="1b62a-201">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="1b62a-202">Ad esempio, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` è un'applicazione hello creata da Yeoman.</span><span class="sxs-lookup"><span data-stu-id="1b62a-202">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="1b62a-203">Eseguire `yo azuresfcontainer:AddService`</span><span class="sxs-lookup"><span data-stu-id="1b62a-203">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="1b62a-204">Configurare l'intervallo di tempo prima della terminazione forzata del contenitore</span><span class="sxs-lookup"><span data-stu-id="1b62a-204">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="1b62a-205">È possibile configurare un intervallo di tempo per hello runtime toowait prima contenitore hello viene rimosso dopo hello eliminazione servizio (o un nodo di spostamento tooanother) è stata avviata.</span><span class="sxs-lookup"><span data-stu-id="1b62a-205">You can configure a time interval for hello runtime toowait before hello container is removed after hello service deletion (or a move tooanother node) has started.</span></span> <span data-ttu-id="1b62a-206">Intervallo di tempo hello configurazione invia hello `docker stop <time in seconds>` contenitore toohello di comando.</span><span class="sxs-lookup"><span data-stu-id="1b62a-206">Configuring hello time interval sends hello `docker stop <time in seconds>` command toohello container.</span></span>   <span data-ttu-id="1b62a-207">Per altri dettagli, vedere [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span><span class="sxs-lookup"><span data-stu-id="1b62a-207">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="1b62a-208">toowait intervallo di tempo Hello viene specificato sotto hello `Hosting` sezione.</span><span class="sxs-lookup"><span data-stu-id="1b62a-208">hello time interval toowait is specified under hello `Hosting` section.</span></span> <span data-ttu-id="1b62a-209">Hello seguente frammento di codice del manifesto del cluster viene illustrato come intervallo di attesa tooset hello:</span><span class="sxs-lookup"><span data-stu-id="1b62a-209">hello following cluster manifest snippet shows how tooset hello wait interval:</span></span>

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
<span data-ttu-id="1b62a-210">Hello intervallo di tempo predefinito è impostato too10 secondi.</span><span class="sxs-lookup"><span data-stu-id="1b62a-210">hello default time interval is set too10 seconds.</span></span> <span data-ttu-id="1b62a-211">Poiché questa configurazione è dinamica, una configurazione aggiornare solo in caso di timeout hello aggiornamenti cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1b62a-211">Since this configuration is dynamic, a config only upgrade on hello cluster updates hello timeout.</span></span> 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a><span data-ttu-id="1b62a-212">Configurare hello runtime tooremove immagini contenitore inutilizzati</span><span class="sxs-lookup"><span data-stu-id="1b62a-212">Configure hello runtime tooremove unused container images</span></span>

<span data-ttu-id="1b62a-213">È possibile configurare hello Service Fabric cluster tooremove immagini contenitore inutilizzati dal nodo hello.</span><span class="sxs-lookup"><span data-stu-id="1b62a-213">You can configure hello Service Fabric cluster tooremove unused container images from hello node.</span></span> <span data-ttu-id="1b62a-214">Questa configurazione consente toobe di spazio su disco liberare se sono presenti nel nodo hello troppi immagini contenitore.</span><span class="sxs-lookup"><span data-stu-id="1b62a-214">This configuration allows disk space toobe recaptured if too many container images are present on hello node.</span></span>  <span data-ttu-id="1b62a-215">tooenable questa funzionalità, l'aggiornamento hello `Hosting` sezione manifesto del cluster hello come illustrato nel seguente frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="1b62a-215">tooenable this feature, update hello `Hosting` section in hello cluster manifest as shown in hello following snippet:</span></span> 


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

<span data-ttu-id="1b62a-216">Per le immagini che non devono essere eliminate, è possibile specificarle in hello `ContainerImagesToSkip` parametro.</span><span class="sxs-lookup"><span data-stu-id="1b62a-216">For images that should not be deleted, you can specify them under hello `ContainerImagesToSkip` parameter.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="1b62a-217">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1b62a-217">Next steps</span></span>
* <span data-ttu-id="1b62a-218">Altre informazioni sull'esecuzione di [contenitori in Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1b62a-218">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="1b62a-219">Hello lettura [distribuire un'applicazione .NET in un contenitore](service-fabric-host-app-in-a-container.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="1b62a-219">Read hello [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="1b62a-220">Informazioni su Service Fabric hello [del ciclo di vita dell'applicazione](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="1b62a-220">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="1b62a-221">Hello estrazione [esempi di codice di Service Fabric contenitore](https://github.com/Azure-Samples/service-fabric-dotnet-containers) su GitHub.</span><span class="sxs-lookup"><span data-stu-id="1b62a-221">Checkout hello [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
