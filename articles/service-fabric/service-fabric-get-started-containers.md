---
title: un'applicazione contenitore di Azure Service Fabric aaaCreate | Documenti Microsoft
description: Creare la prima applicazione contenitore Windows in Azure Service Fabric.  Creazione di un'immagine di Docker con un'applicazione Python, eseguire il push del Registro di sistema di hello immagine tooa contenitore, compilare e distribuire un'applicazione contenitore di Service Fabric.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/18/2017
ms.author: ryanwi
ms.openlocfilehash: b79d3a41eb2da5f7791266588fe9ea7becb0e58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-windows"></a><span data-ttu-id="c46b8-104">Creare la prima applicazione contenitore di Service Fabric in Windows</span><span class="sxs-lookup"><span data-stu-id="c46b8-104">Create your first Service Fabric container application on Windows</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c46b8-105">Windows</span><span class="sxs-lookup"><span data-stu-id="c46b8-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="c46b8-106">Linux</span><span class="sxs-lookup"><span data-stu-id="c46b8-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="c46b8-107">Esecuzione di un'applicazione esistente in un contenitore di Windows in un cluster di Service Fabric non richiede tutte le applicazioni tooyour le modifiche.</span><span class="sxs-lookup"><span data-stu-id="c46b8-107">Running an existing application in a Windows container on a Service Fabric cluster doesn't require any changes tooyour application.</span></span> <span data-ttu-id="c46b8-108">Questo articolo vengono illustrati la creazione di un'immagine Docker che contiene un Python [pallone](http://flask.pocoo.org/) distribuzione di cluster di Service Fabric tooa e l'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="c46b8-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it tooa Service Fabric cluster.</span></span>  <span data-ttu-id="c46b8-109">Si condividerà anche l'applicazione in contenitore tramite [Registro contenitori di Azure](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="c46b8-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="c46b8-110">L'articolo presuppone una conoscenza di base di Docker.</span><span class="sxs-lookup"><span data-stu-id="c46b8-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="c46b8-111">Per informazioni su Docker, lettura hello [Panoramica Docker](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="c46b8-111">You can learn about Docker by reading hello [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c46b8-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c46b8-112">Prerequisites</span></span>
<span data-ttu-id="c46b8-113">Un computer di sviluppo che esegue:</span><span class="sxs-lookup"><span data-stu-id="c46b8-113">A development computer running:</span></span>
* <span data-ttu-id="c46b8-114">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c46b8-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="c46b8-115">[SDK e strumenti di Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c46b8-115">[Service Fabric SDK and tools](service-fabric-get-started.md).</span></span>
*  <span data-ttu-id="c46b8-116">Docker per Windows.</span><span class="sxs-lookup"><span data-stu-id="c46b8-116">Docker for Windows.</span></span>  <span data-ttu-id="c46b8-117">[Scaricare Docker CE per Windows (stabile)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span><span class="sxs-lookup"><span data-stu-id="c46b8-117">[Get Docker CE for Windows (stable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span></span> <span data-ttu-id="c46b8-118">Dopo l'installazione e l'avvio di Docker, fare doppio clic sull'icona dell'area di notifica hello e selezionare **passare contenitori tooWindows**.</span><span class="sxs-lookup"><span data-stu-id="c46b8-118">After installing and starting Docker, right-click on hello tray icon and select **Switch tooWindows containers**.</span></span> <span data-ttu-id="c46b8-119">Si tratta di immagini Docker toorun obbligatorio basate su Windows.</span><span class="sxs-lookup"><span data-stu-id="c46b8-119">This is required toorun Docker images based on Windows.</span></span>

<span data-ttu-id="c46b8-120">Un cluster di Windows con tre o più nodi in esecuzione in Windows Server 2016 con Contenitori. A questo scopo, [creare un cluster](service-fabric-cluster-creation-via-portal.md) o [provare Service Fabric gratuitamente](https://aka.ms/tryservicefabric).</span><span class="sxs-lookup"><span data-stu-id="c46b8-120">A Windows cluster with three or more nodes running on Windows Server 2016 with Containers- [Create a cluster](service-fabric-cluster-creation-via-portal.md) or [try Service Fabric for free](https://aka.ms/tryservicefabric).</span></span>

<span data-ttu-id="c46b8-121">Un registro all'interno del registro contenitori di Azure. A questo scopo, [creare un registro contenitori](../container-registry/container-registry-get-started-portal.md) nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c46b8-121">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span>

## <a name="define-hello-docker-container"></a><span data-ttu-id="c46b8-122">Definire contenitore Docker hello</span><span class="sxs-lookup"><span data-stu-id="c46b8-122">Define hello Docker container</span></span>
<span data-ttu-id="c46b8-123">Creare un'immagine basata su hello [immagine Python](https://hub.docker.com/_/python/) si trova nell'Hub Docker.</span><span class="sxs-lookup"><span data-stu-id="c46b8-123">Build an image based on hello [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span>

<span data-ttu-id="c46b8-124">Definire il contenitore Docker in un Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="c46b8-124">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="c46b8-125">Hello Dockerfile contiene istruzioni per l'impostazione di ambiente hello all'interno del contenitore, il caricamento di un'applicazione hello desiderato toorun e il mapping delle porte.</span><span class="sxs-lookup"><span data-stu-id="c46b8-125">hello Dockerfile contains instructions for setting up hello environment inside your container, loading hello application you want toorun, and mapping ports.</span></span> <span data-ttu-id="c46b8-126">Hello Dockerfile è hello input toohello `docker build` comando che crea l'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-126">hello Dockerfile is hello input toohello `docker build` command, which creates hello image.</span></span>

<span data-ttu-id="c46b8-127">Creare una directory vuota e creare file hello *Dockerfile* (con alcuna estensione di file).</span><span class="sxs-lookup"><span data-stu-id="c46b8-127">Create an empty directory and create hello file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="c46b8-128">Aggiungere il seguente troppo di hello*Dockerfile* e salvare le modifiche:</span><span class="sxs-lookup"><span data-stu-id="c46b8-128">Add hello following too*Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-windowsservercore

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available toohello world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="c46b8-129">Hello lettura [riferimento a Dockerfile](https://docs.docker.com/engine/reference/builder/) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="c46b8-129">Read hello [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="c46b8-130">Creare un'applicazione Web semplice</span><span class="sxs-lookup"><span data-stu-id="c46b8-130">Create a simple web application</span></span>
<span data-ttu-id="c46b8-131">Creare un'applicazione Web Flask in ascolto sulla porta 80 che restituisce "Hello World!".</span><span class="sxs-lookup"><span data-stu-id="c46b8-131">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="c46b8-132">Nella stessa directory di hello, creare file hello *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="c46b8-132">In hello same directory, create hello file *requirements.txt*.</span></span>  <span data-ttu-id="c46b8-133">Aggiungere il seguente hello e salvare le modifiche:</span><span class="sxs-lookup"><span data-stu-id="c46b8-133">Add hello following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="c46b8-134">Creare anche hello *app.py* file e aggiungere hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="c46b8-134">Also create hello *app.py* file and add hello following:</span></span>

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():

    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

<a id="Build-Containers"></a>
## <a name="build-hello-image"></a><span data-ttu-id="c46b8-135">Creazione immagine hello</span><span class="sxs-lookup"><span data-stu-id="c46b8-135">Build hello image</span></span>
<span data-ttu-id="c46b8-136">Eseguire hello `docker build` toocreate hello comando che esegue l'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="c46b8-136">Run hello `docker build` command toocreate hello image that runs your web application.</span></span> <span data-ttu-id="c46b8-137">Aprire una finestra di PowerShell e passare toohello directory contenente hello Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="c46b8-137">Open a PowerShell window and navigate toohello directory containing hello Dockerfile.</span></span> <span data-ttu-id="c46b8-138">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c46b8-138">Run hello following command:</span></span>

```
docker build -t helloworldapp .
```

<span data-ttu-id="c46b8-139">Questo comando compilazioni hello nuova immagine con hello istruzioni del Dockerfile, denominazione (-t tag) immagine hello "helloworldapp".</span><span class="sxs-lookup"><span data-stu-id="c46b8-139">This command builds hello new image using hello instructions in your Dockerfile, naming (-t tagging) hello image "helloworldapp".</span></span> <span data-ttu-id="c46b8-140">La creazione di un'immagine effettua il pull immagine di base hello verso il basso dall'Hub Docker e crea una nuova immagine che consente di aggiungere l'applicazione sopra l'immagine di base hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-140">Building an image pulls hello base image down from Docker Hub and creates a new image that adds your application on top of hello base image.</span></span>  

<span data-ttu-id="c46b8-141">Al termine del comando di compilazione hello, eseguire hello `docker images` informazioni toosee hello nuova immagine di comando:</span><span class="sxs-lookup"><span data-stu-id="c46b8-141">Once hello build command completes, run hello `docker images` command toosee information on hello new image:</span></span>

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="c46b8-142">Eseguire un'applicazione hello in locale</span><span class="sxs-lookup"><span data-stu-id="c46b8-142">Run hello application locally</span></span>
<span data-ttu-id="c46b8-143">Verificare l'immagine localmente prima di pubblicarlo del Registro di sistema di hello contenitore.</span><span class="sxs-lookup"><span data-stu-id="c46b8-143">Verify your image locally before pushing it hello container registry.</span></span>  

<span data-ttu-id="c46b8-144">Eseguire un'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="c46b8-144">Run hello application:</span></span>

```
docker run -d --name my-web-site helloworldapp
```

<span data-ttu-id="c46b8-145">*nome* offre un toohello nome contenitore (invece di ID di contenitore hello) di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c46b8-145">*name* gives a name toohello running container (instead of hello container ID).</span></span>

<span data-ttu-id="c46b8-146">Una volta avviata contenitore hello, trovarne l'indirizzo IP in modo che sia possibile connettersi tooyour esecuzione contenitore da un browser:</span><span class="sxs-lookup"><span data-stu-id="c46b8-146">Once hello container starts, find its IP address so that you can connect tooyour running container from a browser:</span></span>
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

<span data-ttu-id="c46b8-147">Connettersi toohello esecuzione contenitore.</span><span class="sxs-lookup"><span data-stu-id="c46b8-147">Connect toohello running container.</span></span>  <span data-ttu-id="c46b8-148">Aprire un web browser che punta toohello l'indirizzo IP restituito, ad esempio "http://172.31.194.61".</span><span class="sxs-lookup"><span data-stu-id="c46b8-148">Open a web browser pointing toohello IP address returned, for example "http://172.31.194.61".</span></span> <span data-ttu-id="c46b8-149">Dovrebbe essere hello titolo "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="c46b8-149">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="c46b8-150">visualizzare nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-150">display in hello browser.</span></span>

<span data-ttu-id="c46b8-151">toostop nel contenitore, eseguire:</span><span class="sxs-lookup"><span data-stu-id="c46b8-151">toostop your container, run:</span></span>

```
docker stop my-web-site
```

<span data-ttu-id="c46b8-152">Eliminare il contenitore di hello dal computer di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="c46b8-152">Delete hello container from your development machine:</span></span>

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-hello-image-toohello-container-registry"></a><span data-ttu-id="c46b8-153">Eseguire il push del Registro di sistema di hello immagine toohello contenitore</span><span class="sxs-lookup"><span data-stu-id="c46b8-153">Push hello image toohello container registry</span></span>
<span data-ttu-id="c46b8-154">Dopo aver verificato che il contenitore hello viene eseguito nel computer di sviluppo, eseguire il push del Registro di sistema di hello immagine tooyour nel Registro di sistema contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="c46b8-154">After you verify that hello container runs on your development machine, push hello image tooyour registry in Azure Container Registry.</span></span>

<span data-ttu-id="c46b8-155">Eseguire ``docker login`` toolog nel Registro di sistema tooyour contenitore con il [le credenziali del Registro di sistema](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c46b8-155">Run ``docker login`` toolog in tooyour container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="c46b8-156">Hello seguente esempio passa hello ID e la password di Azure Active Directory [dell'entità servizio](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="c46b8-156">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="c46b8-157">Ad esempio, è stato assegnato un registro di sistema tooyour dell'entità servizio per uno scenario di automazione.</span><span class="sxs-lookup"><span data-stu-id="c46b8-157">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span> <span data-ttu-id="c46b8-158">In alternativa, è possibile eseguire l'accesso usando il nome utente e la password del registro.</span><span class="sxs-lookup"><span data-stu-id="c46b8-158">Or, you could login using your registry username and password.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="c46b8-159">Hello seguente comando crea un tag o l'alias dell'immagine di hello, con un registro di sistema tooyour il percorso completo.</span><span class="sxs-lookup"><span data-stu-id="c46b8-159">hello following command creates a tag, or alias, of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="c46b8-160">In questo esempio posizioni hello immagine hello ```samples``` disordine tooavoid dello spazio dei nomi nella directory radice del Registro di sistema hello hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-160">This example places hello image in hello ```samples``` namespace tooavoid clutter in hello root of hello registry.</span></span>

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="c46b8-161">Push del Registro di sistema di hello immagine tooyour contenitore:</span><span class="sxs-lookup"><span data-stu-id="c46b8-161">Push hello image tooyour container registry:</span></span>

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-hello-containerized-service-in-visual-studio"></a><span data-ttu-id="c46b8-162">Creare il servizio contenitore hello in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c46b8-162">Create hello containerized service in Visual Studio</span></span>
<span data-ttu-id="c46b8-163">Hello Service Fabric SDK e strumenti di forniscono un toohelp modello di servizio si crea un'applicazione nei contenitori.</span><span class="sxs-lookup"><span data-stu-id="c46b8-163">hello Service Fabric SDK and tools provide a service template toohelp you create a containerized application.</span></span>

1. <span data-ttu-id="c46b8-164">Avviare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c46b8-164">Start Visual Studio.</span></span>  <span data-ttu-id="c46b8-165">Selezionare **File** > **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="c46b8-165">Select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="c46b8-166">Selezionare l'**applicazione di Service Fabric**, denominarla "MyFirstContainer" e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c46b8-166">Select **Service Fabric application**, name it "MyFirstContainer", and click **OK**.</span></span>
3. <span data-ttu-id="c46b8-167">Selezionare **contenitore Guest** elenco hello di **i modelli di servizio**.</span><span class="sxs-lookup"><span data-stu-id="c46b8-167">Select **Guest Container** from hello list of **service templates**.</span></span>
4. <span data-ttu-id="c46b8-168">In **nome immagine** immettere "myregistry.azurecr.io/samples/helloworldapp", immagine hello è inserito tooyour repository del contenitore.</span><span class="sxs-lookup"><span data-stu-id="c46b8-168">In **Image Name** enter "myregistry.azurecr.io/samples/helloworldapp", hello image you pushed tooyour container repository.</span></span>
5. <span data-ttu-id="c46b8-169">Assegnare un nome al servizio e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c46b8-169">Give your service a name, and click **OK**.</span></span>

## <a name="configure-communication"></a><span data-ttu-id="c46b8-170">Configurare la comunicazione</span><span class="sxs-lookup"><span data-stu-id="c46b8-170">Configure communication</span></span>
<span data-ttu-id="c46b8-171">servizio Hello contenitore è necessario un endpoint per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="c46b8-171">hello containerized service needs an endpoint for communication.</span></span> <span data-ttu-id="c46b8-172">Aggiungere un `Endpoint` elemento con hello protocollo, porta e il file ServiceManifest.xml toohello del tipo.</span><span class="sxs-lookup"><span data-stu-id="c46b8-172">Add an `Endpoint` element with hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="c46b8-173">Per questo articolo, il servizio contenitore hello in ascolto sulla porta 8081.</span><span class="sxs-lookup"><span data-stu-id="c46b8-173">For this article, hello containerized service listens on port 8081.</span></span>  <span data-ttu-id="c46b8-174">In questo esempio viene usata una porta fissa 8081.</span><span class="sxs-lookup"><span data-stu-id="c46b8-174">In this example, a fixed port 8081 is used.</span></span>  <span data-ttu-id="c46b8-175">Se viene specificata alcuna porta, viene scelta una porta casuale dall'intervallo di porte applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-175">If no port is specified, a random port from hello application port range is chosen.</span></span>  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="c46b8-176">La definizione di un endpoint di Service Fabric pubblica hello toohello di endpoint del servizio di denominazione.</span><span class="sxs-lookup"><span data-stu-id="c46b8-176">By defining an endpoint, Service Fabric publishes hello endpoint toohello Naming service.</span></span>  <span data-ttu-id="c46b8-177">Altri servizi in esecuzione nel cluster hello è possono risolvere questo contenitore.</span><span class="sxs-lookup"><span data-stu-id="c46b8-177">Other services running in hello cluster can resolve this container.</span></span>  <span data-ttu-id="c46b8-178">È inoltre possibile eseguire la comunicazione di contenitore a utilizzando hello [proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="c46b8-178">You can also perform container-to-container communication using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span>  <span data-ttu-id="c46b8-179">La comunicazione viene eseguita, fornendo una porta di attesa di proxy inverso HTTP hello e il nome di hello dei servizi di hello che si desidera toocommunicate con come variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="c46b8-179">Communication is performed by providing hello reverse proxy HTTP listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="c46b8-180">Configurare e impostare variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="c46b8-180">Configure and set environment variables</span></span>
<span data-ttu-id="c46b8-181">Le variabili di ambiente possono essere specificate per ogni pacchetto di codice nel manifesto del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-181">Environment variables can be specified for each code package in hello service manifest.</span></span> <span data-ttu-id="c46b8-182">Questa funzionalità è disponibile per tutti i servizi, siano essi distribuiti come contenitori, processi o eseguibili guest.</span><span class="sxs-lookup"><span data-stu-id="c46b8-182">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="c46b8-183">È possibile eseguire l'override di variabile di ambiente, i valori in un'applicazione hello manifesto o specificarli durante la distribuzione come parametri dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c46b8-183">You can override environment variable values in hello application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="c46b8-184">Hello frammento XML del manifesto del servizio seguente viene illustrato un esempio di come le variabili di ambiente toospecify per un pacchetto di codice:</span><span class="sxs-lookup"><span data-stu-id="c46b8-184">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

<span data-ttu-id="c46b8-185">Queste variabili di ambiente possono essere sottoposto a override nel manifesto dell'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="c46b8-185">These environment variables can be overridden in hello application manifest:</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a><span data-ttu-id="c46b8-186">Configurare il mapping tra porta del contenitore e porta dell'host e l'individuazione da contenitore a contenitore</span><span class="sxs-lookup"><span data-stu-id="c46b8-186">Configure container port-to-host port mapping and container-to-container discovery</span></span>
<span data-ttu-id="c46b8-187">Configurare toocommunicate di porta usata un host con il contenitore di hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-187">Configure a host port used toocommunicate  with hello container.</span></span> <span data-ttu-id="c46b8-188">binding porta Hello esegue il mapping di porta hello su quale hello servizio è in attesa all'interno di hello contenitore tooa porta host hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-188">hello port binding maps hello port on which hello service is listening inside hello container tooa port on hello host.</span></span> <span data-ttu-id="c46b8-189">Aggiungere un `PortBinding` elemento `ContainerHostPolicies` elemento del file ApplicationManifest.xml hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-189">Add a `PortBinding` element in `ContainerHostPolicies` element of hello ApplicationManifest.xml file.</span></span>  <span data-ttu-id="c46b8-190">Per questo articolo, `ContainerPort` è 80 (contenitore hello espone la porta 80, come specificato in hello Dockerfile) e `EndpointRef` è "Guest1TypeEndpoint" (hello endpoint definiti in precedenza nel manifesto del servizio hello).</span><span class="sxs-lookup"><span data-stu-id="c46b8-190">For this article, `ContainerPort` is 80 (hello container exposes port 80, as specified in hello Dockerfile) and `EndpointRef` is "Guest1TypeEndpoint" (hello endpoint previously defined in hello service manifest).</span></span>  <span data-ttu-id="c46b8-191">Le richieste in ingresso toohello servizio sulla porta 8081 siano mappati tooport 80 sul contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-191">Incoming requests toohello service on port 8081 are mapped tooport 80 on hello container.</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a><span data-ttu-id="c46b8-192">Configurare l'autenticazione del registro contenitori</span><span class="sxs-lookup"><span data-stu-id="c46b8-192">Configure container registry authentication</span></span>
<span data-ttu-id="c46b8-193">Configurare l'autenticazione di contenitore del Registro di sistema aggiungendo `RepositoryCredentials` troppo`ContainerHostPolicies` di file ApplicationManifest XML hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-193">Configure container registry authentication by adding `RepositoryCredentials` too`ContainerHostPolicies` of hello ApplicationManifest.xml file.</span></span> <span data-ttu-id="c46b8-194">Aggiungere account hello e una password per hello myregistry.azurecr.io contenitore del Registro di sistema, che consente l'immagine contenitore dal repository hello hello servizio toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-194">Add hello account and password for hello myregistry.azurecr.io container registry, which allows hello service toodownload hello container image from hello repository.</span></span>

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

<span data-ttu-id="c46b8-195">È consigliabile crittografare la password di repository hello usando un certificato di crittografia che ha distribuito tooall i nodi del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-195">We recommend that you encrypt hello repository password by using an encipherment certificate that's deployed tooall nodes of hello cluster.</span></span> <span data-ttu-id="c46b8-196">Quando Service Fabric distribuisce hello il pacchetto toohello cluster, il certificato di crittografia hello è di testo crittografato hello toodecrypt utilizzato.</span><span class="sxs-lookup"><span data-stu-id="c46b8-196">When Service Fabric deploys hello service package toohello cluster, hello encipherment certificate is used toodecrypt hello cipher text.</span></span>  <span data-ttu-id="c46b8-197">cmdlet Invoke-ServiceFabricEncryptText Hello è testo crittografato hello di toocreate utilizzato per la password di hello, che viene aggiunto toohello file ApplicationManifest XML.</span><span class="sxs-lookup"><span data-stu-id="c46b8-197">hello Invoke-ServiceFabricEncryptText cmdlet is used toocreate hello cipher text for hello password, which is added toohello ApplicationManifest.xml file.</span></span>

<span data-ttu-id="c46b8-198">Hello lo script seguente crea un nuovo certificato autofirmato e li Esporta in file PFX tooa.</span><span class="sxs-lookup"><span data-stu-id="c46b8-198">hello following script creates a new self-signed certificate and exports it tooa PFX file.</span></span>  <span data-ttu-id="c46b8-199">certificato di Hello viene importato in un insieme di credenziali chiave esistente e quindi distribuiti toohello cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c46b8-199">hello certificate is imported into an existing key vault and then deployed toohello Service Fabric cluster.</span></span>

```powershell
# Variables.
$certpwd = ConvertTo-SecureString -String "Pa$$word321!" -Force -AsPlainText
$filepath = "C:\MyCertificates\dataenciphermentcert.pfx"
$subjectname = "dataencipherment"
$vaultname = "mykeyvault"
$certificateName = "dataenciphermentcert"
$groupname="myclustergroup"
$clustername = "mycluster"

$subscriptionId = "subscription ID"

Login-AzureRmAccount

Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Create a self signed cert, export tooPFX file.
New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject $subjectname -Provider 'Microsoft Enhanced Cryptographic Provider v1.0' `
| Export-PfxCertificate -FilePath $filepath -Password $certpwd

# Import hello certificate tooan existing key vault.  hello key vault must be enabled for deployment.
$cer = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name $certificateName -FilePath $filepath -Password $certpwd

Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $groupname -EnabledForDeployment

# Add hello certificate tooall hello VMs in hello cluster.
Add-AzureRmServiceFabricApplicationCertificate -ResourceGroupName $groupname -Name $clustername -SecretIdentifier $cer.SecretId
```
<span data-ttu-id="c46b8-200">Crittografare la password di hello utilizzando hello [Invoke ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c46b8-200">Encrypt hello password using hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.</span></span>

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

<span data-ttu-id="c46b8-201">Sostituire hello password con testo crittografato hello restituito da hello [Invoke ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet e impostare `PasswordEncrypted` troppo "true".</span><span class="sxs-lookup"><span data-stu-id="c46b8-201">Replace hello password with hello cipher text returned by hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet and set `PasswordEncrypted` too"true".</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-isolation-mode"></a><span data-ttu-id="c46b8-202">Configurare la modalità di isolamento</span><span class="sxs-lookup"><span data-stu-id="c46b8-202">Configure isolation mode</span></span>
<span data-ttu-id="c46b8-203">Windows supporta due modalità di isolamento per i contenitori: la modalità processo e la modalità Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="c46b8-203">Windows supports two isolation modes for containers: process and Hyper-V.</span></span> <span data-ttu-id="c46b8-204">In modalità di isolamento hello processo in esecuzione in tutti i contenitori di hello hello stesso host macchina condivisione hello kernel con host hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-204">With hello process isolation mode, all hello containers running on hello same host machine share hello kernel with hello host.</span></span> <span data-ttu-id="c46b8-205">Con la modalità di isolamento hello Hyper-V, sono isolate tra ogni contenitore di Hyper-V e host contenitore hello kernel hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-205">With hello Hyper-V isolation mode, hello kernels are isolated between each Hyper-V container and hello container host.</span></span> <span data-ttu-id="c46b8-206">viene specificata la modalità di isolamento Hello in hello `ContainerHostPolicies` elemento nel file manifesto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-206">hello isolation mode is specified in hello `ContainerHostPolicies` element in hello application manifest file.</span></span> <span data-ttu-id="c46b8-207">modalità di isolamento Hello che è possibile specificare sono `process`, `hyperv`, e `default`.</span><span class="sxs-lookup"><span data-stu-id="c46b8-207">hello isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="c46b8-208">modalità di isolamento predefinita Hello predefinite troppo`process` in Windows Server ospita e il valore predefinito troppo`hyperv` in host Windows 10.</span><span class="sxs-lookup"><span data-stu-id="c46b8-208">hello default isolation mode defaults too`process` on Windows Server hosts, and defaults too`hyperv` on Windows 10 hosts.</span></span> <span data-ttu-id="c46b8-209">Hello frammento di codice seguente viene illustrato come specificare la modalità di isolamento hello nel file manifesto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-209">hello following snippet shows how hello isolation mode is specified in hello application manifest file.</span></span>

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a><span data-ttu-id="c46b8-210">Configurare la governance delle risorse</span><span class="sxs-lookup"><span data-stu-id="c46b8-210">Configure resource governance</span></span>
<span data-ttu-id="c46b8-211">[Governance delle risorse](service-fabric-resource-governance.md) limita le risorse che hello contenitore è possono utilizzare nell'host di hello hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-211">[Resource governance](service-fabric-resource-governance.md) restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="c46b8-212">Hello `ResourceGovernancePolicy` elemento che è specificato nel manifesto dell'applicazione hello, viene utilizzato toodeclare i limiti delle risorse per un pacchetto di codice del servizio.</span><span class="sxs-lookup"><span data-stu-id="c46b8-212">hello `ResourceGovernancePolicy` element, which is specified in hello application manifest, is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="c46b8-213">I limiti delle risorse possono essere impostati per hello seguenti risorse: memoria, MemorySwap, CpuShares (peso relativo della CPU), MemoryReservationInMB, BlkioWeight (peso relativo BlockIO).</span><span class="sxs-lookup"><span data-stu-id="c46b8-213">Resource limits can be set for hello following resources: Memory, MemorySwap, CpuShares (CPU relative weight), MemoryReservationInMB, BlkioWeight (BlockIO relative weight).</span></span>  <span data-ttu-id="c46b8-214">In questo esempio, il pacchetto di servizio Guest1Pkg Ottiene un core nei nodi del cluster hello in cui viene inserito.</span><span class="sxs-lookup"><span data-stu-id="c46b8-214">In this example, service package Guest1Pkg gets one core on hello cluster nodes where it is placed.</span></span>  <span data-ttu-id="c46b8-215">I limiti di memoria sono assoluti, pertanto il pacchetto di codice hello è limitato too1024 MB di memoria (e una prenotazione soft garanzia di hello stesso).</span><span class="sxs-lookup"><span data-stu-id="c46b8-215">Memory limits are absolute, so hello code package is limited too1024 MB of memory (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="c46b8-216">Pacchetti di codice (contenitori o processi) non sono in grado di tooallocate più memoria rispetto a questo limite e il tentativo di toodo operazione genera un'eccezione di memoria insufficiente.</span><span class="sxs-lookup"><span data-stu-id="c46b8-216">Code packages (containers or processes) are not able tooallocate more memory than this limit, and attempting toodo so results in an out-of-memory exception.</span></span> <span data-ttu-id="c46b8-217">Per risorse limite imposizione toowork, tutti i pacchetti di codice all'interno di un pacchetto del servizio devono avere i limiti di memoria specificati.</span><span class="sxs-lookup"><span data-stu-id="c46b8-217">For resource limit enforcement toowork, all code packages within a service package should have memory limits specified.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-hello-container-application"></a><span data-ttu-id="c46b8-218">Distribuire un'applicazione contenitore hello</span><span class="sxs-lookup"><span data-stu-id="c46b8-218">Deploy hello container application</span></span>
<span data-ttu-id="c46b8-219">Salvare tutte le modifiche e compilare un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-219">Save all your changes and build hello application.</span></span> <span data-ttu-id="c46b8-220">toopublish l'applicazione, il pulsante destro del mouse su **MyFirstContainer** in Esplora soluzioni e selezionare **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="c46b8-220">toopublish your application, right-click on **MyFirstContainer** in Solution Explorer and select **Publish**.</span></span>

<span data-ttu-id="c46b8-221">In **Endpoint della connessione**, immettere l'endpoint di gestione di hello per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-221">In **Connection Endpoint**, enter hello management endpoint for hello cluster.</span></span>  <span data-ttu-id="c46b8-222">ad esempio "containercluster.westus2.cloudapp.azure.com:19000".</span><span class="sxs-lookup"><span data-stu-id="c46b8-222">For example, "containercluster.westus2.cloudapp.azure.com:19000".</span></span> <span data-ttu-id="c46b8-223">È possibile trovare una connessione client hello endpoint nel pannello della panoramica hello per il cluster in hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c46b8-223">You can find hello client connection endpoint in hello Overview blade for your cluster in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="c46b8-224">Fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="c46b8-224">Click **Publish**.</span></span>

<span data-ttu-id="c46b8-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) è uno strumento basato sul Web che permette di analizzare e gestire applicazioni e nodi in un cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c46b8-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a web-based tool for inspecting and managing applications and nodes in a Service Fabric cluster.</span></span> <span data-ttu-id="c46b8-226">Aprire un browser e passare toohttp://containercluster.westus2.cloudapp.azure.com:19080 Esplora/e seguono la distribuzione di applicazioni hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-226">Open a browser and navigate toohttp://containercluster.westus2.cloudapp.azure.com:19080/Explorer/ and follow hello application deployment.</span></span>  <span data-ttu-id="c46b8-227">un'applicazione Hello distribuisce ma non sono in stato di errore finché hello immagine viene scaricata nei nodi del cluster hello (che possono richiedere tempo, a seconda delle dimensioni dell'immagine hello): ![errore][1]</span><span class="sxs-lookup"><span data-stu-id="c46b8-227">hello application deploys but is in an error state until hello image is downloaded on hello cluster nodes (which can take some time, depending on hello image size): ![Error][1]</span></span>

<span data-ttu-id="c46b8-228">un'applicazione Hello è pronta quando è in ```Ready``` stato: ![pronto][2]</span><span class="sxs-lookup"><span data-stu-id="c46b8-228">hello application is ready when it's in ```Ready``` state: ![Ready][2]</span></span>

<span data-ttu-id="c46b8-229">Aprire un browser e passare toohttp://containercluster.westus2.cloudapp.azure.com:8081.</span><span class="sxs-lookup"><span data-stu-id="c46b8-229">Open a browser and navigate toohttp://containercluster.westus2.cloudapp.azure.com:8081.</span></span> <span data-ttu-id="c46b8-230">Dovrebbe essere hello titolo "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="c46b8-230">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="c46b8-231">visualizzare nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-231">display in hello browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="c46b8-232">Eseguire la pulizia</span><span class="sxs-lookup"><span data-stu-id="c46b8-232">Clean up</span></span>
<span data-ttu-id="c46b8-233">Continuare tooincur addebiti mentre hello cluster è in esecuzione, provare a [l'eliminazione del cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="c46b8-233">You continue tooincur charges while hello cluster is running, consider [deleting your cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span></span>  <span data-ttu-id="c46b8-234">I [party cluster](http://tryazureservicefabric.westus.cloudapp.azure.com/) vengono eliminati automaticamente dopo alcune ore.</span><span class="sxs-lookup"><span data-stu-id="c46b8-234">[Party clusters](http://tryazureservicefabric.westus.cloudapp.azure.com/) are automatically deleted after a few hours.</span></span>

<span data-ttu-id="c46b8-235">Dopo che si esegue il push del Registro di sistema di hello immagine toohello contenitore è possibile eliminare l'immagine locale hello dal computer di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="c46b8-235">After you push hello image toohello container registry you can delete hello local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="c46b8-236">Manifesti di esempio completi del servizio e dell'applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c46b8-236">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="c46b8-237">Ecco completa del servizio hello e i manifesti dell'applicazione utilizzate in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="c46b8-237">Here are hello complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="c46b8-238">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="c46b8-238">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Guest1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="Guest1Type" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->    
    <EnvironmentVariables>
      <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
      <EnvironmentVariable Name="BackendServiceName" Value=""/>
    </EnvironmentVariables>

  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which to
           listen. Please note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="c46b8-239">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="c46b8-239">ApplicationManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="MyFirstContainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Guest1_InstanceCount" DefaultValue="-1" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="FrontendService.Code">
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentOverrides>
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
      </ContainerHostPolicies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this
         application type is created. You can also create one or more instances of service type using the
         ServiceFabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Guest1">
      <StatelessService ServiceTypeName="Guest1Type" InstanceCount="[Guest1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="c46b8-240">Configurare l'intervallo di tempo prima della terminazione forzata del contenitore</span><span class="sxs-lookup"><span data-stu-id="c46b8-240">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="c46b8-241">È possibile configurare un intervallo di tempo per hello runtime toowait prima contenitore hello viene rimosso dopo hello eliminazione servizio (o un nodo di spostamento tooanother) è stata avviata.</span><span class="sxs-lookup"><span data-stu-id="c46b8-241">You can configure a time interval for hello runtime toowait before hello container is removed after hello service deletion (or a move tooanother node) has started.</span></span> <span data-ttu-id="c46b8-242">Intervallo di tempo hello configurazione invia hello `docker stop <time in seconds>` contenitore toohello di comando.</span><span class="sxs-lookup"><span data-stu-id="c46b8-242">Configuring hello time interval sends hello `docker stop <time in seconds>` command toohello container.</span></span>   <span data-ttu-id="c46b8-243">Per altri dettagli, vedere [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span><span class="sxs-lookup"><span data-stu-id="c46b8-243">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="c46b8-244">toowait intervallo di tempo Hello viene specificato sotto hello `Hosting` sezione.</span><span class="sxs-lookup"><span data-stu-id="c46b8-244">hello time interval toowait is specified under hello `Hosting` section.</span></span> <span data-ttu-id="c46b8-245">Hello seguente frammento di codice del manifesto del cluster viene illustrato come intervallo di attesa tooset hello:</span><span class="sxs-lookup"><span data-stu-id="c46b8-245">hello following cluster manifest snippet shows how tooset hello wait interval:</span></span>

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
<span data-ttu-id="c46b8-246">Hello intervallo di tempo predefinito è impostato too10 secondi.</span><span class="sxs-lookup"><span data-stu-id="c46b8-246">hello default time interval is set too10 seconds.</span></span> <span data-ttu-id="c46b8-247">Poiché questa configurazione è dinamica, una configurazione aggiornare solo in caso di timeout hello aggiornamenti cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-247">Since this configuration is dynamic, a config only upgrade on hello cluster updates hello timeout.</span></span> 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a><span data-ttu-id="c46b8-248">Configurare hello runtime tooremove immagini contenitore inutilizzati</span><span class="sxs-lookup"><span data-stu-id="c46b8-248">Configure hello runtime tooremove unused container images</span></span>

<span data-ttu-id="c46b8-249">È possibile configurare hello Service Fabric cluster tooremove immagini contenitore inutilizzati dal nodo hello.</span><span class="sxs-lookup"><span data-stu-id="c46b8-249">You can configure hello Service Fabric cluster tooremove unused container images from hello node.</span></span> <span data-ttu-id="c46b8-250">Questa configurazione consente toobe di spazio su disco liberare se sono presenti nel nodo hello troppi immagini contenitore.</span><span class="sxs-lookup"><span data-stu-id="c46b8-250">This configuration allows disk space toobe recaptured if too many container images are present on hello node.</span></span>  <span data-ttu-id="c46b8-251">tooenable questa funzionalità, l'aggiornamento hello `Hosting` sezione manifesto del cluster hello come illustrato nel seguente frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="c46b8-251">tooenable this feature, update hello `Hosting` section in hello cluster manifest as shown in hello following snippet:</span></span> 


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

<span data-ttu-id="c46b8-252">Per le immagini che non devono essere eliminate, è possibile specificarle in hello `ContainerImagesToSkip` parametro.</span><span class="sxs-lookup"><span data-stu-id="c46b8-252">For images that should not be deleted, you can specify them under hello `ContainerImagesToSkip` parameter.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="c46b8-253">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c46b8-253">Next steps</span></span>
* <span data-ttu-id="c46b8-254">Altre informazioni sull'esecuzione di [contenitori in Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c46b8-254">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="c46b8-255">Hello lettura [distribuire un'applicazione .NET in un contenitore](service-fabric-host-app-in-a-container.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c46b8-255">Read hello [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="c46b8-256">Informazioni su Service Fabric hello [del ciclo di vita dell'applicazione](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="c46b8-256">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="c46b8-257">Hello estrazione [esempi di codice di Service Fabric contenitore](https://github.com/Azure-Samples/service-fabric-dotnet-containers) su GitHub.</span><span class="sxs-lookup"><span data-stu-id="c46b8-257">Checkout hello [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
