---
title: Gestire le applicazioni di Azure Service Fabric con l'interfaccia della riga di comando di Azure 2.0
description: Informazioni su come distribuire e rimuovere le applicazioni da un cluster Azure Service Fabric usando l'interfaccia della riga di comando di Azure 2.0.
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: 5728339236e3819b301e428f9d7a8add08f02b3e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a><span data-ttu-id="57f68-103">Gestire un'applicazione di Azure Service Fabric usando l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="57f68-103">Manage an Azure Service Fabric application by using Azure CLI 2.0</span></span>

<span data-ttu-id="57f68-104">Informazioni su come creare ed eliminare applicazioni in esecuzione in un cluster Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="57f68-104">Learn how to create and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57f68-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="57f68-105">Prerequisites</span></span>

* <span data-ttu-id="57f68-106">Installare l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="57f68-106">Install Azure CLI 2.0.</span></span> <span data-ttu-id="57f68-107">Selezionare il cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="57f68-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="57f68-108">Per altre informazioni, vedere [Azure Service Fabric e interfaccia della riga di comando di Azure 2.0](service-fabric-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="57f68-108">For more information, see [Get started with Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span></span>

* <span data-ttu-id="57f68-109">È necessario avere un pacchetto dell'applicazione di Service Fabric pronto per essere distribuito.</span><span class="sxs-lookup"><span data-stu-id="57f68-109">Have a Service Fabric application package ready to be deployed.</span></span> <span data-ttu-id="57f68-110">Per altre informazioni su come creare un'applicazione e inserirla in un pacchetto, vedere l'articolo sul [modello di applicazione di Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="57f68-110">For more information about how to author and package an application, read about the [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="57f68-111">Panoramica</span><span class="sxs-lookup"><span data-stu-id="57f68-111">Overview</span></span>

<span data-ttu-id="57f68-112">Per distribuire una nuova applicazione, completare questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="57f68-112">To deploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="57f68-113">Caricare un pacchetto dell'applicazione nell'archivio immagini di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="57f68-113">Upload an application package to the Service Fabric image store.</span></span>
2. <span data-ttu-id="57f68-114">Eseguire il provisioning di un tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="57f68-114">Provision an application type.</span></span>
3. <span data-ttu-id="57f68-115">Specificare e creare un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="57f68-115">Specify and create an application.</span></span>
4. <span data-ttu-id="57f68-116">Specificare e creare i servizi.</span><span class="sxs-lookup"><span data-stu-id="57f68-116">Specify and create services.</span></span>

<span data-ttu-id="57f68-117">Per rimuovere un'applicazione esistente, completare questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="57f68-117">To remove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="57f68-118">Eliminare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="57f68-118">Delete the application.</span></span>
2. <span data-ttu-id="57f68-119">Annullare il provisioning del tipo di applicazione associato.</span><span class="sxs-lookup"><span data-stu-id="57f68-119">Unprovision the associated application type.</span></span>
3. <span data-ttu-id="57f68-120">Eliminare il contenuto dell'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="57f68-120">Delete the image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="57f68-121">Distribuire un'applicazione nuova</span><span class="sxs-lookup"><span data-stu-id="57f68-121">Deploy a new application</span></span>

<span data-ttu-id="57f68-122">Per distribuire una nuova applicazione, completare le operazioni descritte di seguito.</span><span class="sxs-lookup"><span data-stu-id="57f68-122">To deploy a new application, complete the following tasks.</span></span>

### <a name="upload-a-new-application-package-to-the-image-store"></a><span data-ttu-id="57f68-123">Caricare un nuovo pacchetto dell'applicazione nell'archivio immagini</span><span class="sxs-lookup"><span data-stu-id="57f68-123">Upload a new application package to the image store</span></span>

<span data-ttu-id="57f68-124">Prima di creare un'applicazione, caricare il pacchetto dell'applicazione nell'archivio immagini di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="57f68-124">Before you create an application, upload the application package to the Service Fabric image store.</span></span> 

<span data-ttu-id="57f68-125">Ad esempio, se il pacchetto dell'applicazione è nella directory `app_package_dir`, usare i comandi seguenti per caricare la directory:</span><span class="sxs-lookup"><span data-stu-id="57f68-125">For example, if your application package is in the `app_package_dir` directory, use the following commands to upload the directory:</span></span>

```azurecli
az sf application upload --path ~/app_package_dir
```

<span data-ttu-id="57f68-126">Per i pacchetti di applicazione di grandi dimensioni è possibile specificare l'opzione `--show-progress` per visualizzare lo stato del caricamento.</span><span class="sxs-lookup"><span data-stu-id="57f68-126">For large application packages, you can specify the `--show-progress` option to display the progress of the upload.</span></span>

### <a name="provision-the-application-type"></a><span data-ttu-id="57f68-127">Eseguire il provisioning del tipo di applicazione</span><span class="sxs-lookup"><span data-stu-id="57f68-127">Provision the application type</span></span>

<span data-ttu-id="57f68-128">Al termine del caricamento eseguire il provisioning dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="57f68-128">When the upload is finished, provision the application.</span></span> <span data-ttu-id="57f68-129">Per eseguire il provisioning dell'applicazione, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="57f68-129">To provision the application, use the following command:</span></span>

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="57f68-130">Il valore per `application-type-build-path` è il nome della directory in cui è stato caricato il pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="57f68-130">The value for `application-type-build-path` is the name of the directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="57f68-131">Creare un'applicazione da un tipo di applicazione</span><span class="sxs-lookup"><span data-stu-id="57f68-131">Create an application from an application type</span></span>

<span data-ttu-id="57f68-132">Dopo il provisioning dell'applicazione, usare il comando seguente per assegnare un nome e creare l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="57f68-132">After you provision the application, use the following command to name and create your application:</span></span>

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="57f68-133">`app-name` è il nome da usare per l'istanza di applicazione.</span><span class="sxs-lookup"><span data-stu-id="57f68-133">`app-name` is the name that you want to use for the application instance.</span></span> <span data-ttu-id="57f68-134">È possibile ottenere parametri aggiuntivi dal manifesto dell'applicazione di cui è stato eseguito il provisioning.</span><span class="sxs-lookup"><span data-stu-id="57f68-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="57f68-135">Il nome dell'applicazione deve iniziare con il prefisso `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="57f68-135">The application name must start with the prefix `fabric:/`.</span></span>

### <a name="create-services-for-the-new-application"></a><span data-ttu-id="57f68-136">Creare i servizi per la nuova applicazione</span><span class="sxs-lookup"><span data-stu-id="57f68-136">Create services for the new application</span></span>

<span data-ttu-id="57f68-137">Dopo avere creato un'applicazione, creare i servizi dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="57f68-137">After you have created an application, create services from the application.</span></span> <span data-ttu-id="57f68-138">Nell'esempio seguente si crea dall'applicazione un nuovo servizio senza stato.</span><span class="sxs-lookup"><span data-stu-id="57f68-138">In the following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="57f68-139">I servizi che è possibile creare da un'applicazione sono definiti in un manifesto del servizio all'interno del pacchetto dell'applicazione di cui in precedenza è stato eseguito il provisioning.</span><span class="sxs-lookup"><span data-stu-id="57f68-139">The services that you can create from an application are defined in a service manifest in the previously provisioned application package.</span></span>

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="57f68-140">Verificare l'integrità e la distribuzione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="57f68-140">Verify application deployment and health</span></span>

<span data-ttu-id="57f68-141">Per verificare se un'applicazione e un servizio sono stati distribuiti in modo corretto, controllarne la presenza nei relativi elenchi:</span><span class="sxs-lookup"><span data-stu-id="57f68-141">To verify that an application and service were successfully deployed, check that the application and service are listed:</span></span>

```azurecli
az sf application list
az sf service list --application-list TestApp
```

<span data-ttu-id="57f68-142">Per verificare l'integrità del servizio, usare comandi simili per recuperare lo stato sia del servizio che dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="57f68-142">To verify that the service is healthy, use similar commands to retrieve the health of both the service and the application:</span></span>

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

<span data-ttu-id="57f68-143">I servizi e le applicazioni integri devono avere il valore `HealthState` impostato su `Ok`.</span><span class="sxs-lookup"><span data-stu-id="57f68-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="57f68-144">Rimuovere un'applicazione esistente</span><span class="sxs-lookup"><span data-stu-id="57f68-144">Remove an existing application</span></span>

<span data-ttu-id="57f68-145">Per rimuovere un'applicazione, completare le operazioni descritte di seguito.</span><span class="sxs-lookup"><span data-stu-id="57f68-145">To remove an application, complete the following tasks.</span></span>

### <a name="delete-the-application"></a><span data-ttu-id="57f68-146">Eliminare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="57f68-146">Delete the application</span></span>

<span data-ttu-id="57f68-147">Per eliminare l'applicazione, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="57f68-147">To delete the application, use the following command:</span></span>

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-the-application-type"></a><span data-ttu-id="57f68-148">Annullare il provisioning del tipo di applicazione</span><span class="sxs-lookup"><span data-stu-id="57f68-148">Unprovision the application type</span></span>

<span data-ttu-id="57f68-149">Dopo aver eliminato l'applicazione, è possibile annullare il provisioning del tipo di applicazione se non è più necessario.</span><span class="sxs-lookup"><span data-stu-id="57f68-149">After you delete the application, you can unprovision the application type if you no longer need it.</span></span> <span data-ttu-id="57f68-150">Per annullare il provisioning del tipo di applicazione, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="57f68-150">To unprovision the application type, use the following command:</span></span>

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="57f68-151">Il nome del tipo e la versione del tipo devono corrispondere al nome e alla versione indicati nel manifesto dell'applicazione di cui in precedenza è stato eseguito il provisioning.</span><span class="sxs-lookup"><span data-stu-id="57f68-151">The type name and type version must match the name and version in the previously provisioned application manifest.</span></span>

### <a name="delete-the-application-package"></a><span data-ttu-id="57f68-152">Eliminare il pacchetto dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="57f68-152">Delete the application package</span></span>

<span data-ttu-id="57f68-153">Dopo avere annullato il provisioning del tipo di applicazione, è possibile eliminare il pacchetto dell'applicazione dall'archivio immagini se non è più necessario.</span><span class="sxs-lookup"><span data-stu-id="57f68-153">After you have unprovisioned the application type, you can delete the application package from the image store if you no longer need it.</span></span> <span data-ttu-id="57f68-154">L'eliminazione di pacchetti di applicazioni consente di recuperare spazio su disco.</span><span class="sxs-lookup"><span data-stu-id="57f68-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="57f68-155">Per eliminare il pacchetto dell'applicazione dall'archivio immagini, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="57f68-155">To delete the application package from the image store, use the following command:</span></span>

```azurecli
az sf application package-delete --content-path app_package_dir
```

<span data-ttu-id="57f68-156">`content-path` deve essere il nome della directory caricata al momento della creazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="57f68-156">`content-path` must be the name of the directory that you uploaded when you created the application.</span></span>

## <a name="related-articles"></a><span data-ttu-id="57f68-157">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="57f68-157">Related articles</span></span>

* [<span data-ttu-id="57f68-158">Introduzione a Service Fabric e all'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="57f68-158">Get started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="57f68-159">Introduzione all'interfaccia della riga di comando XPlat per Service Fabric</span><span class="sxs-lookup"><span data-stu-id="57f68-159">Get started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
