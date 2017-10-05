---
title: Creare un'applicazione contenitore di Azure Service Fabric in Linux | Microsoft Docs
description: Creare la prima applicazione contenitore Linux in Azure Service Fabric.  Compilare un'immagine Docker con l'applicazione, eseguire il push dell'immagine in un registro contenitori e compilare e distribuire un'applicazione contenitore di Service Fabric.
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
ms.openlocfilehash: 8355478cb2fff3a63bc4a9b359ec8e2b132c80f6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-service-fabric-container-application-on-linux"></a><span data-ttu-id="e1167-104">Creare la prima applicazione contenitore di Service Fabric in Linux</span><span class="sxs-lookup"><span data-stu-id="e1167-104">Create your first Service Fabric container application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e1167-105">Windows</span><span class="sxs-lookup"><span data-stu-id="e1167-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="e1167-106">Linux</span><span class="sxs-lookup"><span data-stu-id="e1167-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="e1167-107">Per eseguire un'applicazione esistente in un contenitore Linux in un cluster di Service Fabric non è necessario apportare modifiche all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e1167-107">Running an existing application in a Linux container on a Service Fabric cluster doesn't require any changes to your application.</span></span> <span data-ttu-id="e1167-108">Questo articolo illustra come creare un'immagine Docker contenente un'applicazione Web Python [Flask](http://flask.pocoo.org/) e come distribuirla in un cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e1167-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it to a Service Fabric cluster.</span></span>  <span data-ttu-id="e1167-109">Si condividerà anche l'applicazione in contenitore tramite [Registro contenitori di Azure](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="e1167-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="e1167-110">L'articolo presuppone una conoscenza di base di Docker.</span><span class="sxs-lookup"><span data-stu-id="e1167-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="e1167-111">Per informazioni su Docker, vedere [Docker overview](https://docs.docker.com/engine/understanding-docker/) (Panoramica su Docker).</span><span class="sxs-lookup"><span data-stu-id="e1167-111">You can learn about Docker by reading the [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1167-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e1167-112">Prerequisites</span></span>
* <span data-ttu-id="e1167-113">Un computer di sviluppo che esegue:</span><span class="sxs-lookup"><span data-stu-id="e1167-113">A development computer running:</span></span>
  * <span data-ttu-id="e1167-114">[SDK e strumenti di Service Fabric](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e1167-114">[Service Fabric SDK and tools](service-fabric-get-started-linux.md).</span></span>
  * <span data-ttu-id="e1167-115">[Docker CE per Linux](https://docs.docker.com/engine/installation/#prior-releases).</span><span class="sxs-lookup"><span data-stu-id="e1167-115">[Docker CE for Linux](https://docs.docker.com/engine/installation/#prior-releases).</span></span> 
  * [<span data-ttu-id="e1167-116">Interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e1167-116">Service Fabric CLI</span></span>](service-fabric-cli.md)

* <span data-ttu-id="e1167-117">Un registro all'interno del registro contenitori di Azure. A questo scopo, [creare un registro contenitori](../container-registry/container-registry-get-started-portal.md) nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1167-117">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span> 

## <a name="define-the-docker-container"></a><span data-ttu-id="e1167-118">Definire il contenitore Docker</span><span class="sxs-lookup"><span data-stu-id="e1167-118">Define the Docker container</span></span>
<span data-ttu-id="e1167-119">Compilare un'immagine in base all'[immagine Python](https://hub.docker.com/_/python/) disponibile nell'hub Docker.</span><span class="sxs-lookup"><span data-stu-id="e1167-119">Build an image based on the [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span> 

<span data-ttu-id="e1167-120">Definire il contenitore Docker in un Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="e1167-120">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="e1167-121">Il Dockerfile contiene istruzioni per la configurazione dell'ambiente all'interno del contenitore, il caricamento dell'applicazione da eseguire e il mapping delle porte.</span><span class="sxs-lookup"><span data-stu-id="e1167-121">The Dockerfile contains instructions for setting up the environment inside your container, loading the application you want to run, and mapping ports.</span></span> <span data-ttu-id="e1167-122">Il file Dockerfile rappresenta l'input per il comando `docker build` che crea l'immagine.</span><span class="sxs-lookup"><span data-stu-id="e1167-122">The Dockerfile is the input to the `docker build` command, which creates the image.</span></span> 

<span data-ttu-id="e1167-123">Creare una directory vuota e il file *Dockerfile* (senza estensione file).</span><span class="sxs-lookup"><span data-stu-id="e1167-123">Create an empty directory and create the file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="e1167-124">Aggiungere quanto segue a *Dockerfile* e salvare le modifiche:</span><span class="sxs-lookup"><span data-stu-id="e1167-124">Add the following to *Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-slim

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="e1167-125">Per altre informazioni, vedere [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) (Informazioni di riferimento su Dockerfile).</span><span class="sxs-lookup"><span data-stu-id="e1167-125">Read the [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="e1167-126">Creare un'applicazione Web semplice</span><span class="sxs-lookup"><span data-stu-id="e1167-126">Create a simple web application</span></span>
<span data-ttu-id="e1167-127">Creare un'applicazione Web Flask in ascolto sulla porta 80 che restituisce "Hello World!".</span><span class="sxs-lookup"><span data-stu-id="e1167-127">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="e1167-128">Nella stessa directory creare il file *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="e1167-128">In the same directory, create the file *requirements.txt*.</span></span>  <span data-ttu-id="e1167-129">Aggiungere quanto segue e salvare le modifiche:</span><span class="sxs-lookup"><span data-stu-id="e1167-129">Add the following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="e1167-130">Creare anche il file *app.py* e aggiungere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="e1167-130">Also create the *app.py* file and add the following:</span></span>

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-the-image"></a><span data-ttu-id="e1167-131">Compilare l'immagine</span><span class="sxs-lookup"><span data-stu-id="e1167-131">Build the image</span></span>
<span data-ttu-id="e1167-132">Eseguire il comando `docker build` per creare l'immagine che esegue l'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="e1167-132">Run the `docker build` command to create the image that runs your web application.</span></span> <span data-ttu-id="e1167-133">Aprire una finestra di PowerShell e passare a *c:\temp\helloworldapp*.</span><span class="sxs-lookup"><span data-stu-id="e1167-133">Open a PowerShell window and navigate to *c:\temp\helloworldapp*.</span></span> <span data-ttu-id="e1167-134">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e1167-134">Run the following command:</span></span>

```bash
docker build -t helloworldapp .
```

<span data-ttu-id="e1167-135">Questo comando compila la nuova immagine usando le istruzioni contenute nel file Dockerfile e denomina l'immagine "helloworldapp" , ovvero le assegna un tag -t.</span><span class="sxs-lookup"><span data-stu-id="e1167-135">This command builds the new image using the instructions in your Dockerfile, naming (-t tagging) the image "helloworldapp".</span></span> <span data-ttu-id="e1167-136">La compilazione di un'immagine determina il pull dell'immagine di base dall'hub Docker e la creazione di una nuova immagine che aggiunge l'applicazione sopra l'immagine di base.</span><span class="sxs-lookup"><span data-stu-id="e1167-136">Building an image pulls the base image down from Docker Hub and creates a new image that adds your application on top of the base image.</span></span>  

<span data-ttu-id="e1167-137">Al termine dell'esecuzione del comando di compilazione, eseguire il comando `docker images` per visualizzare le informazioni sulla nuova immagine:</span><span class="sxs-lookup"><span data-stu-id="e1167-137">Once the build command completes, run the `docker images` command to see information on the new image:</span></span>

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-the-application-locally"></a><span data-ttu-id="e1167-138">Eseguire l'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="e1167-138">Run the application locally</span></span>
<span data-ttu-id="e1167-139">Verificare l'esecuzione dell'applicazione in contenitore in locale prima di eseguirne il push nel registro contenitori.</span><span class="sxs-lookup"><span data-stu-id="e1167-139">Verify that your containerized application runs locally before pushing it the container registry.</span></span>  

<span data-ttu-id="e1167-140">Eseguire l'applicazione, effettuando il mapping della porta 4000 del computer alla porta 80 esposta dal contenitore:</span><span class="sxs-lookup"><span data-stu-id="e1167-140">Run the application, mapping your computer's port 4000 to the container's exposed port 80:</span></span>

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

<span data-ttu-id="e1167-141">*name* assegna un nome al contenitore in esecuzione, anziché l'ID contenitore.</span><span class="sxs-lookup"><span data-stu-id="e1167-141">*name* gives a name to the running container (instead of the container ID).</span></span>

<span data-ttu-id="e1167-142">Connettersi al contenitore in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e1167-142">Connect to the running container.</span></span>  <span data-ttu-id="e1167-143">Aprire un Web browser puntando all'indirizzo IP restituito sulla porta 4000, ad esempio "http://localhost:4000".</span><span class="sxs-lookup"><span data-stu-id="e1167-143">Open a web browser pointing to the IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="e1167-144">Verrà visualizzata l'intestazione "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="e1167-144">You should see the heading "Hello World!"</span></span> <span data-ttu-id="e1167-145">nel browser.</span><span class="sxs-lookup"><span data-stu-id="e1167-145">display in the browser.</span></span>

![Hello World!][hello-world]

<span data-ttu-id="e1167-147">Per arrestare il contenitore, eseguire:</span><span class="sxs-lookup"><span data-stu-id="e1167-147">To stop your container, run:</span></span>

```bash
docker stop my-web-site
```

<span data-ttu-id="e1167-148">Per eliminare il contenitore dal computer di sviluppo, eseguire:</span><span class="sxs-lookup"><span data-stu-id="e1167-148">Delete the container from your development machine:</span></span>

```bash
docker rm my-web-site
```

## <a name="push-the-image-to-the-container-registry"></a><span data-ttu-id="e1167-149">Effettuare il push dell'immagine nel registro contenitori</span><span class="sxs-lookup"><span data-stu-id="e1167-149">Push the image to the container registry</span></span>
<span data-ttu-id="e1167-150">Dopo aver verificato l'esecuzione dell'applicazione in Docker, eseguire il push dell'immagine nel registro all'interno di Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1167-150">After you verify that the application runs in Docker, push the image to your registry in Azure Container Registry.</span></span>

<span data-ttu-id="e1167-151">Eseguire `docker login` per accedere al registro di contenitori con le [credenziali del registro](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e1167-151">Run `docker login` to log in to your container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="e1167-152">L'esempio seguente passa l'ID e la password di un'[entità servizio](../active-directory/active-directory-application-objects.md) di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e1167-152">The following example passes the ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="e1167-153">Ad esempio, è possibile che sia stata assegnata un'entità servizio al registro per uno scenario di automazione.</span><span class="sxs-lookup"><span data-stu-id="e1167-153">For example, you might have assigned a service principal to your registry for an automation scenario.</span></span>  <span data-ttu-id="e1167-154">In alternativa, è possibile eseguire l'accesso usando il nome utente e la password del registro.</span><span class="sxs-lookup"><span data-stu-id="e1167-154">Or, you could login using your registry username and password.</span></span>

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="e1167-155">Il comando seguente crea un tag, o alias, dell'immagine, con un percorso completo del registro.</span><span class="sxs-lookup"><span data-stu-id="e1167-155">The following command creates a tag, or alias, of the image, with a fully qualified path to your registry.</span></span> <span data-ttu-id="e1167-156">Questo esempio inserisce l'immagine dello spazio dei nomi `samples` per evitare confusione nella radice del registro.</span><span class="sxs-lookup"><span data-stu-id="e1167-156">This example places the image in the `samples` namespace to avoid clutter in the root of the registry.</span></span>

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="e1167-157">Effettuare il push dell'immagine nel registro contenitori:</span><span class="sxs-lookup"><span data-stu-id="e1167-157">Push the image to your container registry:</span></span>

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-the-docker-image-with-yeoman"></a><span data-ttu-id="e1167-158">Creare il pacchetto dell'immagine Docker con Yeoman</span><span class="sxs-lookup"><span data-stu-id="e1167-158">Package the Docker image with Yeoman</span></span>
<span data-ttu-id="e1167-159">Service Fabric SDK per Linux include un generatore [Yeoman](http://yeoman.io/) che semplifica la creazione dell'applicazione e l'aggiunta di un'immagine contenitore.</span><span class="sxs-lookup"><span data-stu-id="e1167-159">The Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy to create your application and add a container image.</span></span> <span data-ttu-id="e1167-160">È possibile usare Yeoman per creare un'applicazione con un singolo contenitore Docker denominato *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="e1167-160">Let's use Yeoman to create an application with a single Docker container called *SimpleContainerApp*.</span></span>

<span data-ttu-id="e1167-161">Per creare un'applicazione contenitore di Service Fabric, aprire una finestra del terminale ed eseguire `yo azuresfcontainer`.</span><span class="sxs-lookup"><span data-stu-id="e1167-161">To create a Service Fabric container application, open a terminal window and run `yo azuresfcontainer`.</span></span>  

<span data-ttu-id="e1167-162">Assegnare un nome all'applicazione, ad esempio "mycontainer".</span><span class="sxs-lookup"><span data-stu-id="e1167-162">Name your application (for example, "mycontainer").</span></span> 

<span data-ttu-id="e1167-163">Specificare l'URL dell'immagine del contenitore in un registro contenitori, ad esempio "".</span><span class="sxs-lookup"><span data-stu-id="e1167-163">Provide the URL for the container image in a container registry (for example, "").</span></span> 

<span data-ttu-id="e1167-164">Dato che per l'immagine è stato definito un punto di ingresso del carico di lavoro, è necessario specificare in modo esplicito i comandi di input, che vengono eseguiti all'interno del contenitore in modo che la relativa esecuzione continui dopo l'avvio.</span><span class="sxs-lookup"><span data-stu-id="e1167-164">This image has a workload entry-point defined, so need to explicitly specify input commands (commands run inside the container, which will keep the container running after startup).</span></span> 

<span data-ttu-id="e1167-165">Specificare "1" come numero di istanze.</span><span class="sxs-lookup"><span data-stu-id="e1167-165">Specify an instance count of "1".</span></span>

![Generatore Yeoman di Service Fabric per i contenitori][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a><span data-ttu-id="e1167-167">Configurare il mapping delle porte e l'autenticazione per il repository del contenitore</span><span class="sxs-lookup"><span data-stu-id="e1167-167">Configure port mapping and container repository authentication</span></span>
<span data-ttu-id="e1167-168">Il servizio in contenitore richiede un endpoint per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="e1167-168">Your containerized service needs an endpoint for communication.</span></span>  <span data-ttu-id="e1167-169">Aggiungere il protocollo, la porta e il tipo a un `Endpoint` nel file ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="e1167-169">Now add the protocol, port, and type to an `Endpoint` in the ServiceManifest.xml file.</span></span> <span data-ttu-id="e1167-170">Per questo articolo, il servizio in contenitore è in ascolto sulla porta 4000:</span><span class="sxs-lookup"><span data-stu-id="e1167-170">For this article, the containerized service listens on port 4000:</span></span> 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
<span data-ttu-id="e1167-171">Se si specifica `UriScheme`, l'endpoint del contenitore viene registrato automaticamente con Service Fabric Naming Service per l'individuazione.</span><span class="sxs-lookup"><span data-stu-id="e1167-171">Providing the `UriScheme` automatically registers the container endpoint with the Service Fabric Naming service for discoverability.</span></span> <span data-ttu-id="e1167-172">Alla fine di questo articolo viene fornito un file di esempio completo di ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="e1167-172">A full ServiceManifest.xml example file is provided at the end of this article.</span></span> 

<span data-ttu-id="e1167-173">Configurare il mapping tra la porta del contenitore e la porta dell'host specificando i criteri `PortBinding` in `ContainerHostPolicies` nel file ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="e1167-173">Configure the container port-to-host port mapping by specifying a `PortBinding` policy in `ContainerHostPolicies` of the ApplicationManifest.xml file.</span></span>  <span data-ttu-id="e1167-174">Per questo articolo, il valore di `ContainerPort` è 80, dato che il contenitore espone la porta 80, come specificato nel Dockerfile, e il valore di `EndpointRef` è "myserviceTypeEndpoint", ossia l'endpoint definito nel manifesto del servizio.</span><span class="sxs-lookup"><span data-stu-id="e1167-174">For this article, `ContainerPort` is 80 (the container exposes port 80, as specified in the Dockerfile) and `EndpointRef` is "myserviceTypeEndpoint" (the endpoint defined in the service manifest).</span></span>  <span data-ttu-id="e1167-175">Per le richieste in ingresso per il servizio sulla porta 4000 viene eseguito il mapping alla porta 80 del contenitore.</span><span class="sxs-lookup"><span data-stu-id="e1167-175">Incoming requests to the service on port 4000 are mapped to port 80 on the container.</span></span>  <span data-ttu-id="e1167-176">Se il contenitore deve eseguire l'autenticazione con un repository privato, aggiungere `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="e1167-176">If your container needs to authenticate with a private repository, then add `RepositoryCredentials`.</span></span>  <span data-ttu-id="e1167-177">Per questo articolo, aggiungere il nome e la password dell'account per il registro contenitori myregistry.azurecr.io.</span><span class="sxs-lookup"><span data-stu-id="e1167-177">For this article, add the account name and password for the myregistry.azurecr.io container registry.</span></span> 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-the-service-fabric-application"></a><span data-ttu-id="e1167-178">Compilare l'applicazione di Service Fabric e creare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="e1167-178">Build and package the Service Fabric application</span></span>
<span data-ttu-id="e1167-179">I modelli Yeoman di Service Fabric includono uno script di compilazione per [Gradle](https://gradle.org/), che può essere usato per compilare l'applicazione dal terminale.</span><span class="sxs-lookup"><span data-stu-id="e1167-179">The Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use to build the application from the terminal.</span></span> <span data-ttu-id="e1167-180">Per compilare l'applicazione e creare il pacchetto, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="e1167-180">To build and package the application, run the following:</span></span>

```bash
cd mycontainer
gradle
```

## <a name="deploy-the-application"></a><span data-ttu-id="e1167-181">Distribuire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="e1167-181">Deploy the application</span></span>
<span data-ttu-id="e1167-182">Dopo aver compilato l'applicazione, è possibile distribuirla nel cluster locale tramite l'interfaccia della riga di comando di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e1167-182">Once the application is built, you can deploy it to the local cluster using the Service Fabric CLI.</span></span>

<span data-ttu-id="e1167-183">Connettersi al cluster locale di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e1167-183">Connect to the local Service Fabric cluster.</span></span>

```bash
sfctl cluster select --endpoint http://localhost:19080
```

<span data-ttu-id="e1167-184">Usare lo script di installazione messo a disposizione nel modello per copiare il pacchetto dell'applicazione nell'archivio immagini del cluster, registrare il tipo di applicazione e creare un'istanza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e1167-184">Use the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

```bash
./install.sh
```

<span data-ttu-id="e1167-185">Aprire un browser e passare a Service Fabric Explorer all'indirizzo http://localhost:19080/Explorer. Sostituire localhost con l'indirizzo IP privato della macchina virtuale se si usa Vagrant in Mac OS X.</span><span class="sxs-lookup"><span data-stu-id="e1167-185">Open a browser and navigate to Service Fabric Explorer at http://localhost:19080/Explorer (replace localhost with the private IP of the VM if using Vagrant on Mac OS X).</span></span> <span data-ttu-id="e1167-186">Espandere il nodo delle applicazioni, nel quale sarà ora presente una voce per il tipo di applicazione e un'altra per la prima istanza del tipo.</span><span class="sxs-lookup"><span data-stu-id="e1167-186">Expand the Applications node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>

<span data-ttu-id="e1167-187">Connettersi al contenitore in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e1167-187">Connect to the running container.</span></span>  <span data-ttu-id="e1167-188">Aprire un Web browser puntando all'indirizzo IP restituito sulla porta 4000, ad esempio "http://localhost:4000".</span><span class="sxs-lookup"><span data-stu-id="e1167-188">Open a web browser pointing to the IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="e1167-189">Verrà visualizzata l'intestazione "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="e1167-189">You should see the heading "Hello World!"</span></span> <span data-ttu-id="e1167-190">nel browser.</span><span class="sxs-lookup"><span data-stu-id="e1167-190">display in the browser.</span></span>

![Hello World!][hello-world]

## <a name="clean-up"></a><span data-ttu-id="e1167-192">Eseguire la pulizia</span><span class="sxs-lookup"><span data-stu-id="e1167-192">Clean up</span></span>
<span data-ttu-id="e1167-193">Usare lo script di disinstallazione incluso nel modello per eliminare l'istanza dell'applicazione dal cluster di sviluppo locale e annullare la registrazione del tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="e1167-193">Use the uninstall script provided in the template to delete the application instance from the local development cluster and unregister the application type.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="e1167-194">Dopo aver effettuato il push dell'immagine nel registro contenitori, è possibile eliminare l'immagine locale dal computer di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="e1167-194">After you push the image to the container registry you can delete the local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="e1167-195">Manifesti di esempio completi del servizio e dell'applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e1167-195">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="e1167-196">Di seguito sono riportati i manifesti completi del servizio e dell'applicazione usati in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="e1167-196">Here are the complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="e1167-197">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="e1167-197">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="myservicePkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType.
         The UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="myserviceType" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers 
      to Service Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
        <Commands></Commands>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables to your container: -->
    
    <EnvironmentVariables>
      <!--
      <EnvironmentVariable Name="VariableName" Value="VariableValue"/>
      -->
    </EnvironmentVariables>
    
  </CodePackage>

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="e1167-198">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="e1167-198">ApplicationManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="mycontainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion 
       should match the Name and Version attributes of the ServiceManifest element defined in the 
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
    <!-- The section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using the 
         ServiceFabric PowerShell module.
         
         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
    <Service Name="myservice">
      <!-- On a local development cluster, set InstanceCount to 1.  On a multi-node production 
      cluster, set InstanceCount to -1 for the container service to run on every node in 
      the cluster.
      -->
      <StatelessService ServiceTypeName="myserviceType" InstanceCount="1">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```
## <a name="adding-more-services-to-an-existing-application"></a><span data-ttu-id="e1167-199">Aggiunta di altri servizi a un'applicazione esistente</span><span class="sxs-lookup"><span data-stu-id="e1167-199">Adding more services to an existing application</span></span>

<span data-ttu-id="e1167-200">Per aggiungere un altro servizio contenitore a un'applicazione già creata usando yeoman, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e1167-200">To add another container service to an application already created using yeoman, perform the following steps:</span></span>

1. <span data-ttu-id="e1167-201">Modificare la directory impostandola sulla radice dell'applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="e1167-201">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="e1167-202">Ad esempio, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` è l'applicazione creata da Yeoman.</span><span class="sxs-lookup"><span data-stu-id="e1167-202">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="e1167-203">Eseguire `yo azuresfcontainer:AddService`</span><span class="sxs-lookup"><span data-stu-id="e1167-203">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="e1167-204">Configurare l'intervallo di tempo prima della terminazione forzata del contenitore</span><span class="sxs-lookup"><span data-stu-id="e1167-204">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="e1167-205">È possibile configurare un intervallo di tempo di attesa del runtime prima che il contenitore venga rimosso dopo l'avvio dell'eliminazione del servizio (o di un passaggio a un altro nodo).</span><span class="sxs-lookup"><span data-stu-id="e1167-205">You can configure a time interval for the runtime to wait before the container is removed after the service deletion (or a move to another node) has started.</span></span> <span data-ttu-id="e1167-206">Configurando l'intervallo di tempo, viene inviato il comando `docker stop <time in seconds>` al contenitore.</span><span class="sxs-lookup"><span data-stu-id="e1167-206">Configuring the time interval sends the `docker stop <time in seconds>` command to the container.</span></span>   <span data-ttu-id="e1167-207">Per altri dettagli, vedere [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span><span class="sxs-lookup"><span data-stu-id="e1167-207">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="e1167-208">L'intervallo di tempo per l'attesa viene specificato nella sezione `Hosting`.</span><span class="sxs-lookup"><span data-stu-id="e1167-208">The time interval to wait is specified under the `Hosting` section.</span></span> <span data-ttu-id="e1167-209">Il frammento di manifesto del cluster seguente illustra come impostare l'intervallo di attesa:</span><span class="sxs-lookup"><span data-stu-id="e1167-209">The following cluster manifest snippet shows how to set the wait interval:</span></span>

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
<span data-ttu-id="e1167-210">L'intervallo di tempo predefinito è impostato su 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="e1167-210">The default time interval is set to 10 seconds.</span></span> <span data-ttu-id="e1167-211">Poiché questa configurazione è dinamica, un aggiornamento della sola configurazione nel cluster aggiorna il timeout.</span><span class="sxs-lookup"><span data-stu-id="e1167-211">Since this configuration is dynamic, a config only upgrade on the cluster updates the timeout.</span></span> 


## <a name="configure-the-runtime-to-remove-unused-container-images"></a><span data-ttu-id="e1167-212">Configurare il runtime per rimuovere le immagini del contenitore non usate</span><span class="sxs-lookup"><span data-stu-id="e1167-212">Configure the runtime to remove unused container images</span></span>

<span data-ttu-id="e1167-213">È possibile configurate il cluster di Service Fabric per rimuovere le immagini del contenitore non usate dal nodo.</span><span class="sxs-lookup"><span data-stu-id="e1167-213">You can configure the Service Fabric cluster to remove unused container images from the node.</span></span> <span data-ttu-id="e1167-214">Questa configurazione consente di riacquisire spazio su disco se nel nodo sono presenti troppe immagini del contenitore.</span><span class="sxs-lookup"><span data-stu-id="e1167-214">This configuration allows disk space to be recaptured if too many container images are present on the node.</span></span>  <span data-ttu-id="e1167-215">Per abilitare questa funzionalità, aggiornare la sezione `Hosting` nel manifesto del cluster, come illustrato nel frammento seguente:</span><span class="sxs-lookup"><span data-stu-id="e1167-215">To enable this feature, update the `Hosting` section in the cluster manifest as shown in the following snippet:</span></span> 


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

<span data-ttu-id="e1167-216">Le immagini che non devono essere eliminate possono essere specificate nel parametro `ContainerImagesToSkip`.</span><span class="sxs-lookup"><span data-stu-id="e1167-216">For images that should not be deleted, you can specify them under the `ContainerImagesToSkip` parameter.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="e1167-217">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e1167-217">Next steps</span></span>
* <span data-ttu-id="e1167-218">Altre informazioni sull'esecuzione di [contenitori in Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e1167-218">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="e1167-219">Vedere l'esercitazione [Distribuire un'applicazione .NET in un contenitore](service-fabric-host-app-in-a-container.md).</span><span class="sxs-lookup"><span data-stu-id="e1167-219">Read the [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="e1167-220">Altre informazioni sul [ciclo di vita dell'applicazione](service-fabric-application-lifecycle.md) di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e1167-220">Learn about the Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="e1167-221">Vedere gli [esempi di codice del contenitore di Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-containers) in GitHub.</span><span class="sxs-lookup"><span data-stu-id="e1167-221">Checkout the [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
