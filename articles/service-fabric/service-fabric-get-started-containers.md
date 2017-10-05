---
title: Creare un'applicazione contenitore di Azure Service Fabric | Microsoft Docs
description: Creare la prima applicazione contenitore Windows in Azure Service Fabric.  Creare un'immagine Docker con un'applicazione Python, effettuare il push dell'immagine in un registro contenitori e compilare e distribuire un'applicazione contenitore di Service Fabric.
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
ms.openlocfilehash: 025bde02b3f342ec3399d51819d1fa8a91f11374
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-service-fabric-container-application-on-windows"></a><span data-ttu-id="7751a-104">Creare la prima applicazione contenitore di Service Fabric in Windows</span><span class="sxs-lookup"><span data-stu-id="7751a-104">Create your first Service Fabric container application on Windows</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7751a-105">Windows</span><span class="sxs-lookup"><span data-stu-id="7751a-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="7751a-106">Linux</span><span class="sxs-lookup"><span data-stu-id="7751a-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="7751a-107">Per eseguire un'applicazione esistente in un contenitore Windows in un cluster di Service Fabric non è necessario apportare modifiche all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7751a-107">Running an existing application in a Windows container on a Service Fabric cluster doesn't require any changes to your application.</span></span> <span data-ttu-id="7751a-108">Questo articolo illustra come creare un'immagine Docker contenente un'applicazione Web Python [Flask](http://flask.pocoo.org/) e come distribuirla in un cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7751a-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it to a Service Fabric cluster.</span></span>  <span data-ttu-id="7751a-109">Si condividerà anche l'applicazione in contenitore tramite [Registro contenitori di Azure](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="7751a-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="7751a-110">L'articolo presuppone una conoscenza di base di Docker.</span><span class="sxs-lookup"><span data-stu-id="7751a-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="7751a-111">Per informazioni su Docker, vedere [Docker overview](https://docs.docker.com/engine/understanding-docker/) (Panoramica su Docker).</span><span class="sxs-lookup"><span data-stu-id="7751a-111">You can learn about Docker by reading the [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7751a-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7751a-112">Prerequisites</span></span>
<span data-ttu-id="7751a-113">Un computer di sviluppo che esegue:</span><span class="sxs-lookup"><span data-stu-id="7751a-113">A development computer running:</span></span>
* <span data-ttu-id="7751a-114">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="7751a-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="7751a-115">[SDK e strumenti di Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7751a-115">[Service Fabric SDK and tools](service-fabric-get-started.md).</span></span>
*  <span data-ttu-id="7751a-116">Docker per Windows.</span><span class="sxs-lookup"><span data-stu-id="7751a-116">Docker for Windows.</span></span>  <span data-ttu-id="7751a-117">[Scaricare Docker CE per Windows (stabile)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span><span class="sxs-lookup"><span data-stu-id="7751a-117">[Get Docker CE for Windows (stable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span></span> <span data-ttu-id="7751a-118">Dopo aver installato e avviato Docker, fare clic con il pulsante destro del mouse sull'icona nell'area di notifica e selezionare **Switch to Windows containers** (Passa ai contenitori Windows).</span><span class="sxs-lookup"><span data-stu-id="7751a-118">After installing and starting Docker, right-click on the tray icon and select **Switch to Windows containers**.</span></span> <span data-ttu-id="7751a-119">Questa operazione è necessaria per eseguire le immagini Docker basate su Windows.</span><span class="sxs-lookup"><span data-stu-id="7751a-119">This is required to run Docker images based on Windows.</span></span>

<span data-ttu-id="7751a-120">Un cluster di Windows con tre o più nodi in esecuzione in Windows Server 2016 con Contenitori. A questo scopo, [creare un cluster](service-fabric-cluster-creation-via-portal.md) o [provare Service Fabric gratuitamente](https://aka.ms/tryservicefabric).</span><span class="sxs-lookup"><span data-stu-id="7751a-120">A Windows cluster with three or more nodes running on Windows Server 2016 with Containers- [Create a cluster](service-fabric-cluster-creation-via-portal.md) or [try Service Fabric for free](https://aka.ms/tryservicefabric).</span></span>

<span data-ttu-id="7751a-121">Un registro all'interno del registro contenitori di Azure. A questo scopo, [creare un registro contenitori](../container-registry/container-registry-get-started-portal.md) nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7751a-121">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span>

## <a name="define-the-docker-container"></a><span data-ttu-id="7751a-122">Definire il contenitore Docker</span><span class="sxs-lookup"><span data-stu-id="7751a-122">Define the Docker container</span></span>
<span data-ttu-id="7751a-123">Compilare un'immagine in base all'[immagine Python](https://hub.docker.com/_/python/) disponibile nell'hub Docker.</span><span class="sxs-lookup"><span data-stu-id="7751a-123">Build an image based on the [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span>

<span data-ttu-id="7751a-124">Definire il contenitore Docker in un Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="7751a-124">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="7751a-125">Il Dockerfile contiene istruzioni per la configurazione dell'ambiente all'interno del contenitore, il caricamento dell'applicazione da eseguire e il mapping delle porte.</span><span class="sxs-lookup"><span data-stu-id="7751a-125">The Dockerfile contains instructions for setting up the environment inside your container, loading the application you want to run, and mapping ports.</span></span> <span data-ttu-id="7751a-126">Il file Dockerfile rappresenta l'input per il comando `docker build` che crea l'immagine.</span><span class="sxs-lookup"><span data-stu-id="7751a-126">The Dockerfile is the input to the `docker build` command, which creates the image.</span></span>

<span data-ttu-id="7751a-127">Creare una directory vuota e il file *Dockerfile* (senza estensione file).</span><span class="sxs-lookup"><span data-stu-id="7751a-127">Create an empty directory and create the file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="7751a-128">Aggiungere quanto segue a *Dockerfile* e salvare le modifiche:</span><span class="sxs-lookup"><span data-stu-id="7751a-128">Add the following to *Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-windowsservercore

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="7751a-129">Per altre informazioni, vedere [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) (Informazioni di riferimento su Dockerfile).</span><span class="sxs-lookup"><span data-stu-id="7751a-129">Read the [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="7751a-130">Creare un'applicazione Web semplice</span><span class="sxs-lookup"><span data-stu-id="7751a-130">Create a simple web application</span></span>
<span data-ttu-id="7751a-131">Creare un'applicazione Web Flask in ascolto sulla porta 80 che restituisce "Hello World!".</span><span class="sxs-lookup"><span data-stu-id="7751a-131">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="7751a-132">Nella stessa directory creare il file *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="7751a-132">In the same directory, create the file *requirements.txt*.</span></span>  <span data-ttu-id="7751a-133">Aggiungere quanto segue e salvare le modifiche:</span><span class="sxs-lookup"><span data-stu-id="7751a-133">Add the following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="7751a-134">Creare anche il file *app.py* e aggiungere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="7751a-134">Also create the *app.py* file and add the following:</span></span>

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
## <a name="build-the-image"></a><span data-ttu-id="7751a-135">Compilare l'immagine</span><span class="sxs-lookup"><span data-stu-id="7751a-135">Build the image</span></span>
<span data-ttu-id="7751a-136">Eseguire il comando `docker build` per creare l'immagine che esegue l'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="7751a-136">Run the `docker build` command to create the image that runs your web application.</span></span> <span data-ttu-id="7751a-137">Aprire una finestra di PowerShell e passare alla directory contenente il Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="7751a-137">Open a PowerShell window and navigate to the directory containing the Dockerfile.</span></span> <span data-ttu-id="7751a-138">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7751a-138">Run the following command:</span></span>

```
docker build -t helloworldapp .
```

<span data-ttu-id="7751a-139">Questo comando compila la nuova immagine usando le istruzioni contenute nel file Dockerfile e denomina l'immagine "helloworldapp" , ovvero le assegna un tag -t.</span><span class="sxs-lookup"><span data-stu-id="7751a-139">This command builds the new image using the instructions in your Dockerfile, naming (-t tagging) the image "helloworldapp".</span></span> <span data-ttu-id="7751a-140">La compilazione di un'immagine determina il pull dell'immagine di base dall'hub Docker e la creazione di una nuova immagine che aggiunge l'applicazione sopra l'immagine di base.</span><span class="sxs-lookup"><span data-stu-id="7751a-140">Building an image pulls the base image down from Docker Hub and creates a new image that adds your application on top of the base image.</span></span>  

<span data-ttu-id="7751a-141">Al termine dell'esecuzione del comando di compilazione, eseguire il comando `docker images` per visualizzare le informazioni sulla nuova immagine:</span><span class="sxs-lookup"><span data-stu-id="7751a-141">Once the build command completes, run the `docker images` command to see information on the new image:</span></span>

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-the-application-locally"></a><span data-ttu-id="7751a-142">Eseguire l'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="7751a-142">Run the application locally</span></span>
<span data-ttu-id="7751a-143">Verifica l'immagine in locale prima di effettuarne il push nel registro contenitori.</span><span class="sxs-lookup"><span data-stu-id="7751a-143">Verify your image locally before pushing it the container registry.</span></span>  

<span data-ttu-id="7751a-144">Eseguire l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="7751a-144">Run the application:</span></span>

```
docker run -d --name my-web-site helloworldapp
```

<span data-ttu-id="7751a-145">*name* assegna un nome al contenitore in esecuzione, anziché l'ID contenitore.</span><span class="sxs-lookup"><span data-stu-id="7751a-145">*name* gives a name to the running container (instead of the container ID).</span></span>

<span data-ttu-id="7751a-146">Dopo aver avviato il contenitore, trovare il relativo indirizzo IP per consentire la connessione al contenitore in esecuzione da un browser:</span><span class="sxs-lookup"><span data-stu-id="7751a-146">Once the container starts, find its IP address so that you can connect to your running container from a browser:</span></span>
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

<span data-ttu-id="7751a-147">Connettersi al contenitore in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7751a-147">Connect to the running container.</span></span>  <span data-ttu-id="7751a-148">Aprire un Web browser puntando all'indirizzo IP restituito, ad esempio "http://172.31.194.61".</span><span class="sxs-lookup"><span data-stu-id="7751a-148">Open a web browser pointing to the IP address returned, for example "http://172.31.194.61".</span></span> <span data-ttu-id="7751a-149">Verrà visualizzata l'intestazione "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="7751a-149">You should see the heading "Hello World!"</span></span> <span data-ttu-id="7751a-150">nel browser.</span><span class="sxs-lookup"><span data-stu-id="7751a-150">display in the browser.</span></span>

<span data-ttu-id="7751a-151">Per arrestare il contenitore, eseguire:</span><span class="sxs-lookup"><span data-stu-id="7751a-151">To stop your container, run:</span></span>

```
docker stop my-web-site
```

<span data-ttu-id="7751a-152">Per eliminare il contenitore dal computer di sviluppo, eseguire:</span><span class="sxs-lookup"><span data-stu-id="7751a-152">Delete the container from your development machine:</span></span>

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-the-image-to-the-container-registry"></a><span data-ttu-id="7751a-153">Effettuare il push dell'immagine nel registro contenitori</span><span class="sxs-lookup"><span data-stu-id="7751a-153">Push the image to the container registry</span></span>
<span data-ttu-id="7751a-154">Dopo aver verificato l'esecuzione del contenitore nel computer di sviluppo, effettuare il push dell'immagine nel registro all'interno del registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="7751a-154">After you verify that the container runs on your development machine, push the image to your registry in Azure Container Registry.</span></span>

<span data-ttu-id="7751a-155">Eseguire ``docker login`` per accedere al registro di contenitori con le [credenziali del registro](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7751a-155">Run ``docker login`` to log in to your container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="7751a-156">L'esempio seguente passa l'ID e la password di un'[entità servizio](../active-directory/active-directory-application-objects.md) di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7751a-156">The following example passes the ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="7751a-157">Ad esempio, è possibile che sia stata assegnata un'entità servizio al registro per uno scenario di automazione.</span><span class="sxs-lookup"><span data-stu-id="7751a-157">For example, you might have assigned a service principal to your registry for an automation scenario.</span></span> <span data-ttu-id="7751a-158">In alternativa, è possibile eseguire l'accesso usando il nome utente e la password del registro.</span><span class="sxs-lookup"><span data-stu-id="7751a-158">Or, you could login using your registry username and password.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="7751a-159">Il comando seguente crea un tag, o alias, dell'immagine, con un percorso completo del registro.</span><span class="sxs-lookup"><span data-stu-id="7751a-159">The following command creates a tag, or alias, of the image, with a fully qualified path to your registry.</span></span> <span data-ttu-id="7751a-160">Questo esempio inserisce l'immagine dello spazio dei nomi ```samples``` per evitare confusione nella radice del registro.</span><span class="sxs-lookup"><span data-stu-id="7751a-160">This example places the image in the ```samples``` namespace to avoid clutter in the root of the registry.</span></span>

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="7751a-161">Effettuare il push dell'immagine nel registro contenitori:</span><span class="sxs-lookup"><span data-stu-id="7751a-161">Push the image to your container registry:</span></span>

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-the-containerized-service-in-visual-studio"></a><span data-ttu-id="7751a-162">Creare il servizio in contenitori in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7751a-162">Create the containerized service in Visual Studio</span></span>
<span data-ttu-id="7751a-163">L'SDK e gli strumenti di Service Fabric offrono un modello di servizio che consente di creare un'applicazione in contenitori.</span><span class="sxs-lookup"><span data-stu-id="7751a-163">The Service Fabric SDK and tools provide a service template to help you create a containerized application.</span></span>

1. <span data-ttu-id="7751a-164">Avviare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7751a-164">Start Visual Studio.</span></span>  <span data-ttu-id="7751a-165">Selezionare **File** > **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="7751a-165">Select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="7751a-166">Selezionare l'**applicazione di Service Fabric**, denominarla "MyFirstContainer" e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="7751a-166">Select **Service Fabric application**, name it "MyFirstContainer", and click **OK**.</span></span>
3. <span data-ttu-id="7751a-167">Scegliere **Contenitore guest** dall'elenco dei **modelli di servizio**.</span><span class="sxs-lookup"><span data-stu-id="7751a-167">Select **Guest Container** from the list of **service templates**.</span></span>
4. <span data-ttu-id="7751a-168">In **Nome immagine** immettere "myregistry.azurecr.io/samples/helloworldapp", vale a dire l'immagine di cui è stato effettuato il push nel repository dei contenitori.</span><span class="sxs-lookup"><span data-stu-id="7751a-168">In **Image Name** enter "myregistry.azurecr.io/samples/helloworldapp", the image you pushed to your container repository.</span></span>
5. <span data-ttu-id="7751a-169">Assegnare un nome al servizio e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="7751a-169">Give your service a name, and click **OK**.</span></span>

## <a name="configure-communication"></a><span data-ttu-id="7751a-170">Configurare la comunicazione</span><span class="sxs-lookup"><span data-stu-id="7751a-170">Configure communication</span></span>
<span data-ttu-id="7751a-171">Il servizio in contenitori richiede un endpoint per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="7751a-171">The containerized service needs an endpoint for communication.</span></span> <span data-ttu-id="7751a-172">Aggiungere un elemento `Endpoint` con il protocollo, la porta e il tipo al file ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="7751a-172">Add an `Endpoint` element with the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="7751a-173">Per questo articolo, il servizio in contenitori è in ascolto sulla porta 8081.</span><span class="sxs-lookup"><span data-stu-id="7751a-173">For this article, the containerized service listens on port 8081.</span></span>  <span data-ttu-id="7751a-174">In questo esempio viene usata una porta fissa 8081.</span><span class="sxs-lookup"><span data-stu-id="7751a-174">In this example, a fixed port 8081 is used.</span></span>  <span data-ttu-id="7751a-175">Se non vengono specificate porte, verrà scelta una porta casuale dall'intervallo di porte dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7751a-175">If no port is specified, a random port from the application port range is chosen.</span></span>  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="7751a-176">Definendo un endpoint, Service Fabric pubblica l'endpoint nel servizio Naming.</span><span class="sxs-lookup"><span data-stu-id="7751a-176">By defining an endpoint, Service Fabric publishes the endpoint to the Naming service.</span></span>  <span data-ttu-id="7751a-177">Altri servizi in esecuzione nel cluster possono risolvere questo contenitore.</span><span class="sxs-lookup"><span data-stu-id="7751a-177">Other services running in the cluster can resolve this container.</span></span>  <span data-ttu-id="7751a-178">È anche possibile eseguire la comunicazione da contenitore a contenitore usando il [proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="7751a-178">You can also perform container-to-container communication using the [reverse proxy](service-fabric-reverseproxy.md).</span></span>  <span data-ttu-id="7751a-179">La comunicazione avviene specificando la porta di ascolto HTTP del proxy inverso e il nome dei servizi con cui si vuole comunicare come variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="7751a-179">Communication is performed by providing the reverse proxy HTTP listening port and the name of the services that you want to communicate with as environment variables.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="7751a-180">Configurare e impostare variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="7751a-180">Configure and set environment variables</span></span>
<span data-ttu-id="7751a-181">È possibile specificare variabili di ambiente per ogni pacchetto di codice nel manifesto del servizio.</span><span class="sxs-lookup"><span data-stu-id="7751a-181">Environment variables can be specified for each code package in the service manifest.</span></span> <span data-ttu-id="7751a-182">Questa funzionalità è disponibile per tutti i servizi, siano essi distribuiti come contenitori, processi o eseguibili guest.</span><span class="sxs-lookup"><span data-stu-id="7751a-182">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="7751a-183">È possibile sostituire i valori delle variabili di ambiente nel manifesto dell'applicazione oppure specificarli durante la distribuzione come parametri dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7751a-183">You can override environment variable values in the application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="7751a-184">Il frammento XML del manifesto del servizio seguente offre un esempio di come specificare le variabili di ambiente per un pacchetto di codice:</span><span class="sxs-lookup"><span data-stu-id="7751a-184">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

<span data-ttu-id="7751a-185">È possibile eseguire l'override di queste variabili di ambiente nel manifesto dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="7751a-185">These environment variables can be overridden in the application manifest:</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a><span data-ttu-id="7751a-186">Configurare il mapping tra porta del contenitore e porta dell'host e l'individuazione da contenitore a contenitore</span><span class="sxs-lookup"><span data-stu-id="7751a-186">Configure container port-to-host port mapping and container-to-container discovery</span></span>
<span data-ttu-id="7751a-187">Configurare una porta dell'host per la comunicazione con il contenitore.</span><span class="sxs-lookup"><span data-stu-id="7751a-187">Configure a host port used to communicate  with the container.</span></span> <span data-ttu-id="7751a-188">Il binding di porta esegue il mapping tra la porta su cui il servizio è in ascolto nel contenitore e una porta nell'host.</span><span class="sxs-lookup"><span data-stu-id="7751a-188">The port binding maps the port on which the service is listening inside the container to a port on the host.</span></span> <span data-ttu-id="7751a-189">Aggiungere un elemento `PortBinding` nell'elemento `ContainerHostPolicies` del file ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="7751a-189">Add a `PortBinding` element in `ContainerHostPolicies` element of the ApplicationManifest.xml file.</span></span>  <span data-ttu-id="7751a-190">Per questo articolo, il valore di `ContainerPort` è 80, vale a dire che il contenitore espone la porta 80, come specificato nel Dockerfile, e il valore di `EndpointRef` è "Guest1TypeEndpoint", ovvero l'endpoint definito in precedenza nel manifesto del servizio.</span><span class="sxs-lookup"><span data-stu-id="7751a-190">For this article, `ContainerPort` is 80 (the container exposes port 80, as specified in the Dockerfile) and `EndpointRef` is "Guest1TypeEndpoint" (the endpoint previously defined in the service manifest).</span></span>  <span data-ttu-id="7751a-191">Per le richieste in ingresso per il servizio sulla porta 8081 viene eseguito il mapping alla porta 80 del contenitore.</span><span class="sxs-lookup"><span data-stu-id="7751a-191">Incoming requests to the service on port 8081 are mapped to port 80 on the container.</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a><span data-ttu-id="7751a-192">Configurare l'autenticazione del registro contenitori</span><span class="sxs-lookup"><span data-stu-id="7751a-192">Configure container registry authentication</span></span>
<span data-ttu-id="7751a-193">Configurare l'autenticazione del registro contenitori aggiungendo `RepositoryCredentials` a `ContainerHostPolicies` nel file ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="7751a-193">Configure container registry authentication by adding `RepositoryCredentials` to `ContainerHostPolicies` of the ApplicationManifest.xml file.</span></span> <span data-ttu-id="7751a-194">Aggiungere l'account e la password per il contenitore myregistry.azurecr.io, per consentire al servizio di scaricare l'immagine del contenitore dal repository.</span><span class="sxs-lookup"><span data-stu-id="7751a-194">Add the account and password for the myregistry.azurecr.io container registry, which allows the service to download the container image from the repository.</span></span>

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

<span data-ttu-id="7751a-195">È consigliabile crittografare la password del repository con un certificato di crittografia distribuito in tutti i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="7751a-195">We recommend that you encrypt the repository password by using an encipherment certificate that's deployed to all nodes of the cluster.</span></span> <span data-ttu-id="7751a-196">Quando Service Fabric distribuisce il pacchetto del servizio nel cluster, il certificato di crittografia viene usato per decrittografare il testo crittografato.</span><span class="sxs-lookup"><span data-stu-id="7751a-196">When Service Fabric deploys the service package to the cluster, the encipherment certificate is used to decrypt the cipher text.</span></span>  <span data-ttu-id="7751a-197">Il cmdlet Invoke-ServiceFabricEncryptText viene usato per creare il testo crittografato della password, che viene aggiunto al file ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="7751a-197">The Invoke-ServiceFabricEncryptText cmdlet is used to create the cipher text for the password, which is added to the ApplicationManifest.xml file.</span></span>

<span data-ttu-id="7751a-198">Lo script seguente crea un nuovo certificato autofirmato e lo esporta in un file PFX.</span><span class="sxs-lookup"><span data-stu-id="7751a-198">The following script creates a new self-signed certificate and exports it to a PFX file.</span></span>  <span data-ttu-id="7751a-199">Il certificato viene importato in un insieme di credenziali delle chiavi esistente e quindi distribuito nel cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7751a-199">The certificate is imported into an existing key vault and then deployed to the Service Fabric cluster.</span></span>

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

# Create a self signed cert, export to PFX file.
New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject $subjectname -Provider 'Microsoft Enhanced Cryptographic Provider v1.0' `
| Export-PfxCertificate -FilePath $filepath -Password $certpwd

# Import the certificate to an existing key vault.  The key vault must be enabled for deployment.
$cer = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name $certificateName -FilePath $filepath -Password $certpwd

Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $groupname -EnabledForDeployment

# Add the certificate to all the VMs in the cluster.
Add-AzureRmServiceFabricApplicationCertificate -ResourceGroupName $groupname -Name $clustername -SecretIdentifier $cer.SecretId
```
<span data-ttu-id="7751a-200">Crittografare la password usando il cmdlet [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="7751a-200">Encrypt the password using the [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.</span></span>

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

<span data-ttu-id="7751a-201">Sostituire la password con il testo crittografato restituito dal cmdlet [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) e impostare `PasswordEncrypted` su "true".</span><span class="sxs-lookup"><span data-stu-id="7751a-201">Replace the password with the cipher text returned by the [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet and set `PasswordEncrypted` to "true".</span></span>

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

## <a name="configure-isolation-mode"></a><span data-ttu-id="7751a-202">Configurare la modalità di isolamento</span><span class="sxs-lookup"><span data-stu-id="7751a-202">Configure isolation mode</span></span>
<span data-ttu-id="7751a-203">Windows supporta due modalità di isolamento per i contenitori: la modalità processo e la modalità Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="7751a-203">Windows supports two isolation modes for containers: process and Hyper-V.</span></span> <span data-ttu-id="7751a-204">Nella modalità di isolamento del processo tutti i contenitori in esecuzione nello stesso computer host condividono il kernel con l'host.</span><span class="sxs-lookup"><span data-stu-id="7751a-204">With the process isolation mode, all the containers running on the same host machine share the kernel with the host.</span></span> <span data-ttu-id="7751a-205">Nella modalità di isolamento Hyper-V i kernel sono isolati tra i singoli contenitori Hyper-V e il contenitore host.</span><span class="sxs-lookup"><span data-stu-id="7751a-205">With the Hyper-V isolation mode, the kernels are isolated between each Hyper-V container and the container host.</span></span> <span data-ttu-id="7751a-206">La modalità di isolamento è specificata nell'elemento `ContainerHostPolicies` nel file manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7751a-206">The isolation mode is specified in the `ContainerHostPolicies` element in the application manifest file.</span></span> <span data-ttu-id="7751a-207">Le modalità di isolamento specificabili sono `process`, `hyperv` e `default`.</span><span class="sxs-lookup"><span data-stu-id="7751a-207">The isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="7751a-208">La modalità di isolamento assume come impostazione predefinita `process` negli host Windows Server e `hyperv` negli host Windows 10.</span><span class="sxs-lookup"><span data-stu-id="7751a-208">The default isolation mode defaults to `process` on Windows Server hosts, and defaults to `hyperv` on Windows 10 hosts.</span></span> <span data-ttu-id="7751a-209">Il frammento seguente indica come è specificata la modalità di isolamento nel file manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7751a-209">The following snippet shows how the isolation mode is specified in the application manifest file.</span></span>

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a><span data-ttu-id="7751a-210">Configurare la governance delle risorse</span><span class="sxs-lookup"><span data-stu-id="7751a-210">Configure resource governance</span></span>
<span data-ttu-id="7751a-211">La [governance delle risorse](service-fabric-resource-governance.md) limita le risorse che possono essere usate dal contenitore nell'host.</span><span class="sxs-lookup"><span data-stu-id="7751a-211">[Resource governance](service-fabric-resource-governance.md) restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="7751a-212">L'elemento `ResourceGovernancePolicy`, specificato nel manifesto dell'applicazione, viene usato per dichiarare limiti di risorse per il pacchetto di codice di un servizio.</span><span class="sxs-lookup"><span data-stu-id="7751a-212">The `ResourceGovernancePolicy` element, which is specified in the application manifest, is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="7751a-213">È possibile impostare limiti per le risorse seguenti: Memory, MemorySwap, CpuShares (peso relativo CPU), MemoryReservationInMB, BlkioWeight (peso relativo BlockIO).</span><span class="sxs-lookup"><span data-stu-id="7751a-213">Resource limits can be set for the following resources: Memory, MemorySwap, CpuShares (CPU relative weight), MemoryReservationInMB, BlkioWeight (BlockIO relative weight).</span></span>  <span data-ttu-id="7751a-214">In questo esempio, il pacchetto del servizio Guest1Pkg ottiene un core nei nodi del cluster in cui è posizionato.</span><span class="sxs-lookup"><span data-stu-id="7751a-214">In this example, service package Guest1Pkg gets one core on the cluster nodes where it is placed.</span></span>  <span data-ttu-id="7751a-215">I limiti di memoria sono assoluti, quindi i pacchetti di codice sono limitati a 1024 MB di memoria, con prenotazione a garanzia flessibile.</span><span class="sxs-lookup"><span data-stu-id="7751a-215">Memory limits are absolute, so the code package is limited to 1024 MB of memory (and a soft-guarantee reservation of the same).</span></span> <span data-ttu-id="7751a-216">I pacchetti di codice (contenitori o pacchetti) non sono in grado di allocare una quantità di memoria superiore a questo limite. Un'operazione di questo tipo genererebbe un'eccezione di memoria esaurita.</span><span class="sxs-lookup"><span data-stu-id="7751a-216">Code packages (containers or processes) are not able to allocate more memory than this limit, and attempting to do so results in an out-of-memory exception.</span></span> <span data-ttu-id="7751a-217">Perché l'imposizione di un limite di risorse funzioni, è necessario che tutti i pacchetti di codice inclusi in un pacchetto del servizio abbiano limiti di memoria specificati.</span><span class="sxs-lookup"><span data-stu-id="7751a-217">For resource limit enforcement to work, all code packages within a service package should have memory limits specified.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-the-container-application"></a><span data-ttu-id="7751a-218">Distribuire l'applicazione del contenitore</span><span class="sxs-lookup"><span data-stu-id="7751a-218">Deploy the container application</span></span>
<span data-ttu-id="7751a-219">Salvare tutte le modifiche e compilare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7751a-219">Save all your changes and build the application.</span></span> <span data-ttu-id="7751a-220">Per pubblicare l'applicazione, fare clic con il pulsante destro del mouse su **MyFirstContainer** in Esplora soluzioni e scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="7751a-220">To publish your application, right-click on **MyFirstContainer** in Solution Explorer and select **Publish**.</span></span>

<span data-ttu-id="7751a-221">In **Endpoint connessione** immettere l'endpoint di gestione per il cluster,</span><span class="sxs-lookup"><span data-stu-id="7751a-221">In **Connection Endpoint**, enter the management endpoint for the cluster.</span></span>  <span data-ttu-id="7751a-222">ad esempio "containercluster.westus2.cloudapp.azure.com:19000".</span><span class="sxs-lookup"><span data-stu-id="7751a-222">For example, "containercluster.westus2.cloudapp.azure.com:19000".</span></span> <span data-ttu-id="7751a-223">L'endpoint di connessione del client è disponibile nel pannello Panoramica per il cluster nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7751a-223">You can find the client connection endpoint in the Overview blade for your cluster in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="7751a-224">Fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="7751a-224">Click **Publish**.</span></span>

<span data-ttu-id="7751a-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) è uno strumento basato sul Web che permette di analizzare e gestire applicazioni e nodi in un cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7751a-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a web-based tool for inspecting and managing applications and nodes in a Service Fabric cluster.</span></span> <span data-ttu-id="7751a-226">Aprire un browser Web e passare a http://containercluster.westus2.cloudapp.azure.com:19080/Explorer/ per seguire la distribuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7751a-226">Open a browser and navigate to http://containercluster.westus2.cloudapp.azure.com:19080/Explorer/ and follow the application deployment.</span></span>  <span data-ttu-id="7751a-227">L'applicazione viene distribuita, ma rimane in stato di errore fino a quando l'immagine non viene scaricata nei nodi del cluster. L'operazione può richiedere del tempo, a seconda delle dimensioni dell'immagine: ![Errore][1]</span><span class="sxs-lookup"><span data-stu-id="7751a-227">The application deploys but is in an error state until the image is downloaded on the cluster nodes (which can take some time, depending on the image size): ![Error][1]</span></span>

<span data-ttu-id="7751a-228">L'applicazione è pronta quando è in stato ```Ready```: ![Pronto][2]</span><span class="sxs-lookup"><span data-stu-id="7751a-228">The application is ready when it's in ```Ready``` state: ![Ready][2]</span></span>

<span data-ttu-id="7751a-229">Aprire un browser Web e passare a http://containercluster.westus2.cloudapp.azure.com:8081.</span><span class="sxs-lookup"><span data-stu-id="7751a-229">Open a browser and navigate to http://containercluster.westus2.cloudapp.azure.com:8081.</span></span> <span data-ttu-id="7751a-230">Verrà visualizzata l'intestazione "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="7751a-230">You should see the heading "Hello World!"</span></span> <span data-ttu-id="7751a-231">nel browser.</span><span class="sxs-lookup"><span data-stu-id="7751a-231">display in the browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="7751a-232">Eseguire la pulizia</span><span class="sxs-lookup"><span data-stu-id="7751a-232">Clean up</span></span>
<span data-ttu-id="7751a-233">Mentre il cluster è in esecuzione, continuano a essere addebitati i relativi costi. È quindi consigliabile [eliminare il cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="7751a-233">You continue to incur charges while the cluster is running, consider [deleting your cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span></span>  <span data-ttu-id="7751a-234">I [party cluster](http://tryazureservicefabric.westus.cloudapp.azure.com/) vengono eliminati automaticamente dopo alcune ore.</span><span class="sxs-lookup"><span data-stu-id="7751a-234">[Party clusters](http://tryazureservicefabric.westus.cloudapp.azure.com/) are automatically deleted after a few hours.</span></span>

<span data-ttu-id="7751a-235">Dopo aver effettuato il push dell'immagine nel registro contenitori, è possibile eliminare l'immagine locale dal computer di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="7751a-235">After you push the image to the container registry you can delete the local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="7751a-236">Manifesti di esempio completi del servizio e dell'applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7751a-236">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="7751a-237">Di seguito sono riportati i manifesti completi del servizio e dell'applicazione usati in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="7751a-237">Here are the complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="7751a-238">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="7751a-238">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Guest1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType.
         The UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="Guest1Type" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers to Service Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables to your container: -->    
    <EnvironmentVariables>
      <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
      <EnvironmentVariable Name="BackendServiceName" Value=""/>
    </EnvironmentVariables>

  </CodePackage>

  <!-- Config package is the contents of the Config directoy under PackageRoot that contains an
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to
           listen. Please note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="7751a-239">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="7751a-239">ApplicationManifest.xml</span></span>
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
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion
       should match the Name and Version attributes of the ServiceManifest element defined in the
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
    <!-- The section below creates instances of service types, when an instance of this
         application type is created. You can also create one or more instances of service type using the
         ServiceFabric PowerShell module.

         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
    <Service Name="Guest1">
      <StatelessService ServiceTypeName="Guest1Type" InstanceCount="[Guest1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="7751a-240">Configurare l'intervallo di tempo prima della terminazione forzata del contenitore</span><span class="sxs-lookup"><span data-stu-id="7751a-240">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="7751a-241">È possibile configurare un intervallo di tempo di attesa del runtime prima che il contenitore venga rimosso dopo l'avvio dell'eliminazione del servizio (o di un passaggio a un altro nodo).</span><span class="sxs-lookup"><span data-stu-id="7751a-241">You can configure a time interval for the runtime to wait before the container is removed after the service deletion (or a move to another node) has started.</span></span> <span data-ttu-id="7751a-242">Configurando l'intervallo di tempo, viene inviato il comando `docker stop <time in seconds>` al contenitore.</span><span class="sxs-lookup"><span data-stu-id="7751a-242">Configuring the time interval sends the `docker stop <time in seconds>` command to the container.</span></span>   <span data-ttu-id="7751a-243">Per altri dettagli, vedere [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span><span class="sxs-lookup"><span data-stu-id="7751a-243">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="7751a-244">L'intervallo di tempo per l'attesa viene specificato nella sezione `Hosting`.</span><span class="sxs-lookup"><span data-stu-id="7751a-244">The time interval to wait is specified under the `Hosting` section.</span></span> <span data-ttu-id="7751a-245">Il frammento di manifesto del cluster seguente illustra come impostare l'intervallo di attesa:</span><span class="sxs-lookup"><span data-stu-id="7751a-245">The following cluster manifest snippet shows how to set the wait interval:</span></span>

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
<span data-ttu-id="7751a-246">L'intervallo di tempo predefinito è impostato su 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="7751a-246">The default time interval is set to 10 seconds.</span></span> <span data-ttu-id="7751a-247">Poiché questa configurazione è dinamica, un aggiornamento della sola configurazione nel cluster aggiorna il timeout.</span><span class="sxs-lookup"><span data-stu-id="7751a-247">Since this configuration is dynamic, a config only upgrade on the cluster updates the timeout.</span></span> 


## <a name="configure-the-runtime-to-remove-unused-container-images"></a><span data-ttu-id="7751a-248">Configurare il runtime per rimuovere le immagini del contenitore non usate</span><span class="sxs-lookup"><span data-stu-id="7751a-248">Configure the runtime to remove unused container images</span></span>

<span data-ttu-id="7751a-249">È possibile configurate il cluster di Service Fabric per rimuovere le immagini del contenitore non usate dal nodo.</span><span class="sxs-lookup"><span data-stu-id="7751a-249">You can configure the Service Fabric cluster to remove unused container images from the node.</span></span> <span data-ttu-id="7751a-250">Questa configurazione consente di riacquisire spazio su disco se nel nodo sono presenti troppe immagini del contenitore.</span><span class="sxs-lookup"><span data-stu-id="7751a-250">This configuration allows disk space to be recaptured if too many container images are present on the node.</span></span>  <span data-ttu-id="7751a-251">Per abilitare questa funzionalità, aggiornare la sezione `Hosting` nel manifesto del cluster, come illustrato nel frammento seguente:</span><span class="sxs-lookup"><span data-stu-id="7751a-251">To enable this feature, update the `Hosting` section in the cluster manifest as shown in the following snippet:</span></span> 


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

<span data-ttu-id="7751a-252">Le immagini che non devono essere eliminate possono essere specificate nel parametro `ContainerImagesToSkip`.</span><span class="sxs-lookup"><span data-stu-id="7751a-252">For images that should not be deleted, you can specify them under the `ContainerImagesToSkip` parameter.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="7751a-253">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7751a-253">Next steps</span></span>
* <span data-ttu-id="7751a-254">Altre informazioni sull'esecuzione di [contenitori in Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7751a-254">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="7751a-255">Vedere l'esercitazione [Distribuire un'applicazione .NET in un contenitore](service-fabric-host-app-in-a-container.md).</span><span class="sxs-lookup"><span data-stu-id="7751a-255">Read the [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="7751a-256">Altre informazioni sul [ciclo di vita dell'applicazione](service-fabric-application-lifecycle.md) di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7751a-256">Learn about the Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="7751a-257">Vedere gli [esempi di codice del contenitore di Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-containers) in GitHub.</span><span class="sxs-lookup"><span data-stu-id="7751a-257">Checkout the [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
