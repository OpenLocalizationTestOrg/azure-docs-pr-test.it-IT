---
title: applicazioni Azure Service Fabric aaaManage mediante Azure CLI 2.0
description: Informazioni su come toodeploy e rimuovere le applicazioni da un'infrastruttura di Azure del servizio cluster tramite l'interfaccia CLI di Azure 2.0.
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ae1ba19513978b0f95ffb65d5f1f7a21ed5f2894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a><span data-ttu-id="e1bea-103">Gestire un'applicazione di Azure Service Fabric usando l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e1bea-103">Manage an Azure Service Fabric application by using Azure CLI 2.0</span></span>

<span data-ttu-id="e1bea-104">Informazioni su come toocreate ed eliminare le applicazioni in esecuzione in un cluster di Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e1bea-104">Learn how toocreate and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1bea-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e1bea-105">Prerequisites</span></span>

* <span data-ttu-id="e1bea-106">Installare l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="e1bea-106">Install Azure CLI 2.0.</span></span> <span data-ttu-id="e1bea-107">Selezionare il cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e1bea-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="e1bea-108">Per altre informazioni, vedere [Azure Service Fabric e interfaccia della riga di comando di Azure 2.0](service-fabric-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="e1bea-108">For more information, see [Get started with Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span></span>

* <span data-ttu-id="e1bea-109">Disporre di un Service Fabric applicazione pacchetto pronto toobe distribuito.</span><span class="sxs-lookup"><span data-stu-id="e1bea-109">Have a Service Fabric application package ready toobe deployed.</span></span> <span data-ttu-id="e1bea-110">Per ulteriori informazioni su come tooauthor e un'applicazione, pacchetto conoscenza hello [il modello di applicazione di Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="e1bea-110">For more information about how tooauthor and package an application, read about hello [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="e1bea-111">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e1bea-111">Overview</span></span>

<span data-ttu-id="e1bea-112">toodeploy una nuova applicazione, completare questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="e1bea-112">toodeploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="e1bea-113">Caricare un archivio immagini di Service Fabric toohello di pacchetto di applicazione.</span><span class="sxs-lookup"><span data-stu-id="e1bea-113">Upload an application package toohello Service Fabric image store.</span></span>
2. <span data-ttu-id="e1bea-114">Eseguire il provisioning di un tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="e1bea-114">Provision an application type.</span></span>
3. <span data-ttu-id="e1bea-115">Specificare e creare un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e1bea-115">Specify and create an application.</span></span>
4. <span data-ttu-id="e1bea-116">Specificare e creare i servizi.</span><span class="sxs-lookup"><span data-stu-id="e1bea-116">Specify and create services.</span></span>

<span data-ttu-id="e1bea-117">tooremove un'applicazione esistente, completare questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="e1bea-117">tooremove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="e1bea-118">Eliminare un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e1bea-118">Delete hello application.</span></span>
2. <span data-ttu-id="e1bea-119">Hello annullamento del provisioning è associato il tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="e1bea-119">Unprovision hello associated application type.</span></span>
3. <span data-ttu-id="e1bea-120">Eliminare il contenuto di hello image store.</span><span class="sxs-lookup"><span data-stu-id="e1bea-120">Delete hello image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="e1bea-121">Distribuire un'applicazione nuova</span><span class="sxs-lookup"><span data-stu-id="e1bea-121">Deploy a new application</span></span>

<span data-ttu-id="e1bea-122">toodeploy una nuova applicazione hello completo seguenti attività.</span><span class="sxs-lookup"><span data-stu-id="e1bea-122">toodeploy a new application, complete hello following tasks.</span></span>

### <a name="upload-a-new-application-package-toohello-image-store"></a><span data-ttu-id="e1bea-123">Caricare un nuovo archivio di immagini toohello pacchetto applicazione</span><span class="sxs-lookup"><span data-stu-id="e1bea-123">Upload a new application package toohello image store</span></span>

<span data-ttu-id="e1bea-124">Prima di creare un'applicazione, caricare l'archivio immagini di hello applicazione pacchetto toohello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e1bea-124">Before you create an application, upload hello application package toohello Service Fabric image store.</span></span> 

<span data-ttu-id="e1bea-125">Ad esempio, se il pacchetto dell'applicazione è in hello `app_package_dir` directory, utilizzare hello seguenti directory hello tooupload di comandi:</span><span class="sxs-lookup"><span data-stu-id="e1bea-125">For example, if your application package is in hello `app_package_dir` directory, use hello following commands tooupload hello directory:</span></span>

```azurecli
az sf application upload --path ~/app_package_dir
```

<span data-ttu-id="e1bea-126">Per i pacchetti di applicazione di grandi dimensioni, è possibile specificare hello `--show-progress` opzione toodisplay lo stato di avanzamento hello del caricamento hello.</span><span class="sxs-lookup"><span data-stu-id="e1bea-126">For large application packages, you can specify hello `--show-progress` option toodisplay hello progress of hello upload.</span></span>

### <a name="provision-hello-application-type"></a><span data-ttu-id="e1bea-127">Tipo di provisioning dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="e1bea-127">Provision hello application type</span></span>

<span data-ttu-id="e1bea-128">Al termine di caricamento di hello, eseguire il provisioning di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e1bea-128">When hello upload is finished, provision hello application.</span></span> <span data-ttu-id="e1bea-129">applicazione hello tooprovision, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e1bea-129">tooprovision hello application, use hello following command:</span></span>

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="e1bea-130">valore per Hello `application-type-build-path` hello nome della directory hello in cui è caricato il pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e1bea-130">hello value for `application-type-build-path` is hello name of hello directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="e1bea-131">Creare un'applicazione da un tipo di applicazione</span><span class="sxs-lookup"><span data-stu-id="e1bea-131">Create an application from an application type</span></span>

<span data-ttu-id="e1bea-132">Dopo effettuare il provisioning di un'applicazione hello, utilizzare hello successivo comando tooname e creare l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="e1bea-132">After you provision hello application, use hello following command tooname and create your application:</span></span>

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="e1bea-133">`app-name`è il nome di hello che si desidera toouse per l'istanza dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e1bea-133">`app-name` is hello name that you want toouse for hello application instance.</span></span> <span data-ttu-id="e1bea-134">È possibile ottenere i parametri aggiuntivi hello definito in precedenza manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e1bea-134">You can get additional parameters from hello previously provisioned application manifest.</span></span>

<span data-ttu-id="e1bea-135">nome dell'applicazione Hello deve iniziare con il prefisso hello `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="e1bea-135">hello application name must start with hello prefix `fabric:/`.</span></span>

### <a name="create-services-for-hello-new-application"></a><span data-ttu-id="e1bea-136">Creazione di servizi per la nuova applicazione hello</span><span class="sxs-lookup"><span data-stu-id="e1bea-136">Create services for hello new application</span></span>

<span data-ttu-id="e1bea-137">Dopo aver creato un'applicazione, è possibile creare servizi da un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e1bea-137">After you have created an application, create services from hello application.</span></span> <span data-ttu-id="e1bea-138">Nell'esempio seguente di hello, è creare un nuovo servizio senza stato dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e1bea-138">In hello following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="e1bea-139">servizi di Hello che è possibile creare da un'applicazione vengono definiti in un manifesto del servizio nel pacchetto di applicazione definito in precedenza hello.</span><span class="sxs-lookup"><span data-stu-id="e1bea-139">hello services that you can create from an application are defined in a service manifest in hello previously provisioned application package.</span></span>

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="e1bea-140">Verificare l'integrità e la distribuzione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="e1bea-140">Verify application deployment and health</span></span>

<span data-ttu-id="e1bea-141">tooverify che un'applicazione e servizio siano state distribuite correttamente, verificare che il servizio e applicazione hello siano elencati:</span><span class="sxs-lookup"><span data-stu-id="e1bea-141">tooverify that an application and service were successfully deployed, check that hello application and service are listed:</span></span>

```azurecli
az sf application list
az sf service list --application-list TestApp
```

<span data-ttu-id="e1bea-142">tooverify che servizio hello è integro, utilizzare l'integrità di hello tooretrieve comandi simili del servizio hello e di un'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="e1bea-142">tooverify that hello service is healthy, use similar commands tooretrieve hello health of both hello service and hello application:</span></span>

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

<span data-ttu-id="e1bea-143">I servizi e le applicazioni integri devono avere il valore `HealthState` impostato su `Ok`.</span><span class="sxs-lookup"><span data-stu-id="e1bea-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="e1bea-144">Rimuovere un'applicazione esistente</span><span class="sxs-lookup"><span data-stu-id="e1bea-144">Remove an existing application</span></span>

<span data-ttu-id="e1bea-145">tooremove, un'applicazione hello completo seguenti attività.</span><span class="sxs-lookup"><span data-stu-id="e1bea-145">tooremove an application, complete hello following tasks.</span></span>

### <a name="delete-hello-application"></a><span data-ttu-id="e1bea-146">Eliminare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="e1bea-146">Delete hello application</span></span>

<span data-ttu-id="e1bea-147">applicazione hello toodelete, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e1bea-147">toodelete hello application, use hello following command:</span></span>

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a><span data-ttu-id="e1bea-148">Annullare il provisioning di tipo di applicazione hello</span><span class="sxs-lookup"><span data-stu-id="e1bea-148">Unprovision hello application type</span></span>

<span data-ttu-id="e1bea-149">Dopo l'eliminazione di un'applicazione hello, è possibile annullare il provisioning di tipo di applicazione hello se non è più necessario.</span><span class="sxs-lookup"><span data-stu-id="e1bea-149">After you delete hello application, you can unprovision hello application type if you no longer need it.</span></span> <span data-ttu-id="e1bea-150">tipo di applicazione hello toounprovision, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e1bea-150">toounprovision hello application type, use hello following command:</span></span>

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="e1bea-151">Hello tipo nome e tipo di versione deve corrispondere al nome hello e la versione nel manifesto di applicazione definito in precedenza hello.</span><span class="sxs-lookup"><span data-stu-id="e1bea-151">hello type name and type version must match hello name and version in hello previously provisioned application manifest.</span></span>

### <a name="delete-hello-application-package"></a><span data-ttu-id="e1bea-152">Eliminare il pacchetto di applicazione hello</span><span class="sxs-lookup"><span data-stu-id="e1bea-152">Delete hello application package</span></span>

<span data-ttu-id="e1bea-153">Dopo che si dispone di annullamento del provisioning di tipo di applicazione hello, è possibile eliminare il pacchetto di applicazione hello dall'archivio immagini hello se non è più necessario.</span><span class="sxs-lookup"><span data-stu-id="e1bea-153">After you have unprovisioned hello application type, you can delete hello application package from hello image store if you no longer need it.</span></span> <span data-ttu-id="e1bea-154">L'eliminazione di pacchetti di applicazioni consente di recuperare spazio su disco.</span><span class="sxs-lookup"><span data-stu-id="e1bea-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="e1bea-155">pacchetto di applicazione hello toodelete dall'archivio immagini hello, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e1bea-155">toodelete hello application package from hello image store, use hello following command:</span></span>

```azurecli
az sf application package-delete --content-path app_package_dir
```

<span data-ttu-id="e1bea-156">`content-path`deve essere hello nome della directory hello caricato durante la creazione di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e1bea-156">`content-path` must be hello name of hello directory that you uploaded when you created hello application.</span></span>

## <a name="related-articles"></a><span data-ttu-id="e1bea-157">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="e1bea-157">Related articles</span></span>

* [<span data-ttu-id="e1bea-158">Introduzione a Service Fabric e all'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e1bea-158">Get started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="e1bea-159">Introduzione all'interfaccia della riga di comando XPlat per Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e1bea-159">Get started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
