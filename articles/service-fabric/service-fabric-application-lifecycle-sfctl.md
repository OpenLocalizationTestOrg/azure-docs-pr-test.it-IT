---
title: Gestire le applicazioni di Azure Service Fabric usando l'interfaccia della riga di comando di Azure Service Fabric
description: Informazioni su come distribuire e rimuovere le applicazioni da un cluster Azure Service Fabric usando l'interfaccia della riga di comando di Azure Service Fabric.
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: c3a2eb3e6e54f952ef963bb2a0292d9ad7b53bc5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-service-fabric-cli"></a><span data-ttu-id="9e689-103">Gestire un'applicazione di Azure Service Fabric usando l'interfaccia della riga di comando di Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9e689-103">Manage an Azure Service Fabric application by using Azure Service Fabric CLI</span></span>

<span data-ttu-id="9e689-104">Informazioni su come creare ed eliminare applicazioni in esecuzione in un cluster Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9e689-104">Learn how to create and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e689-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9e689-105">Prerequisites</span></span>

* <span data-ttu-id="9e689-106">Installare l'interfaccia della riga di comando di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9e689-106">Install Service Fabric CLI.</span></span> <span data-ttu-id="9e689-107">Selezionare il cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9e689-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="9e689-108">Per altre informazioni, vedere [Introduzione all'interfaccia della riga di comando di Service Fabric](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9e689-108">For more information, see [Get started with Service Fabric CLI](service-fabric-cli.md).</span></span>

* <span data-ttu-id="9e689-109">È necessario avere un pacchetto dell'applicazione di Service Fabric pronto per essere distribuito.</span><span class="sxs-lookup"><span data-stu-id="9e689-109">Have a Service Fabric application package ready to be deployed.</span></span> <span data-ttu-id="9e689-110">Per altre informazioni su come creare un'applicazione e inserirla in un pacchetto, vedere l'articolo sul [modello di applicazione di Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="9e689-110">For more information about how to author and package an application, read about the [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="9e689-111">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9e689-111">Overview</span></span>

<span data-ttu-id="9e689-112">Per distribuire una nuova applicazione, completare questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="9e689-112">To deploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="9e689-113">Caricare un pacchetto dell'applicazione nell'archivio immagini di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9e689-113">Upload an application package to the Service Fabric image store.</span></span>
2. <span data-ttu-id="9e689-114">Eseguire il provisioning di un tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="9e689-114">Provision an application type.</span></span>
3. <span data-ttu-id="9e689-115">Specificare e creare un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9e689-115">Specify and create an application.</span></span>
4. <span data-ttu-id="9e689-116">Specificare e creare i servizi.</span><span class="sxs-lookup"><span data-stu-id="9e689-116">Specify and create services.</span></span>

<span data-ttu-id="9e689-117">Per rimuovere un'applicazione esistente, completare questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="9e689-117">To remove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="9e689-118">Eliminare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9e689-118">Delete the application.</span></span>
2. <span data-ttu-id="9e689-119">Annullare il provisioning del tipo di applicazione associato.</span><span class="sxs-lookup"><span data-stu-id="9e689-119">Unprovision the associated application type.</span></span>
3. <span data-ttu-id="9e689-120">Eliminare il contenuto dell'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="9e689-120">Delete the image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="9e689-121">Distribuire un'applicazione nuova</span><span class="sxs-lookup"><span data-stu-id="9e689-121">Deploy a new application</span></span>

<span data-ttu-id="9e689-122">Per distribuire una nuova applicazione, completare le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="9e689-122">To deploy a new application, complete the following tasks:</span></span>

### <a name="upload-a-new-application-package-to-the-image-store"></a><span data-ttu-id="9e689-123">Caricare un nuovo pacchetto dell'applicazione nell'archivio immagini</span><span class="sxs-lookup"><span data-stu-id="9e689-123">Upload a new application package to the image store</span></span>

<span data-ttu-id="9e689-124">Prima di creare un'applicazione, caricare il pacchetto dell'applicazione nell'archivio immagini di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9e689-124">Before you create an application, upload the application package to the Service Fabric image store.</span></span>

<span data-ttu-id="9e689-125">Ad esempio, se il pacchetto dell'applicazione è nella directory `app_package_dir`, usare i comandi seguenti per caricare la directory:</span><span class="sxs-lookup"><span data-stu-id="9e689-125">For example, if your application package is in the `app_package_dir` directory, use the following commands to upload the directory:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir
```

<span data-ttu-id="9e689-126">Per i pacchetti di applicazione di grandi dimensioni è possibile specificare l'opzione `--show-progress` per visualizzare lo stato del caricamento.</span><span class="sxs-lookup"><span data-stu-id="9e689-126">For large application packages, you can specify the `--show-progress` option to display the progress of the upload.</span></span>

### <a name="provision-the-application-type"></a><span data-ttu-id="9e689-127">Eseguire il provisioning del tipo di applicazione</span><span class="sxs-lookup"><span data-stu-id="9e689-127">Provision the application type</span></span>

<span data-ttu-id="9e689-128">Al termine del caricamento eseguire il provisioning dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9e689-128">When the upload is finished, provision the application.</span></span> <span data-ttu-id="9e689-129">Per eseguire il provisioning dell'applicazione, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9e689-129">To provision the application, use the following command:</span></span>

```azurecli
sfctl application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="9e689-130">Il valore per `application-type-build-path` è il nome della directory in cui è stato caricato il pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9e689-130">The value for `application-type-build-path` is the name of the directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="9e689-131">Creare un'applicazione da un tipo di applicazione</span><span class="sxs-lookup"><span data-stu-id="9e689-131">Create an application from an application type</span></span>

<span data-ttu-id="9e689-132">Dopo il provisioning dell'applicazione, usare il comando seguente per assegnare un nome e creare l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="9e689-132">After you provision the application, use the following command to name and create your application:</span></span>

```azurecli
sfctl application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="9e689-133">`app-name` è il nome da usare per l'istanza di applicazione.</span><span class="sxs-lookup"><span data-stu-id="9e689-133">`app-name` is the name that you want to use for the application instance.</span></span> <span data-ttu-id="9e689-134">È possibile ottenere parametri aggiuntivi dal manifesto dell'applicazione di cui è stato eseguito il provisioning.</span><span class="sxs-lookup"><span data-stu-id="9e689-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="9e689-135">Il nome dell'applicazione deve iniziare con il prefisso `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="9e689-135">The application name must start with the prefix `fabric:/`.</span></span>

### <a name="create-services-for-the-new-application"></a><span data-ttu-id="9e689-136">Creare i servizi per la nuova applicazione</span><span class="sxs-lookup"><span data-stu-id="9e689-136">Create services for the new application</span></span>

<span data-ttu-id="9e689-137">Dopo avere creato un'applicazione, creare i servizi dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9e689-137">After you have created an application, create services from the application.</span></span> <span data-ttu-id="9e689-138">Nell'esempio seguente si crea dall'applicazione un nuovo servizio senza stato.</span><span class="sxs-lookup"><span data-stu-id="9e689-138">In the following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="9e689-139">I servizi che è possibile creare da un'applicazione sono definiti in un manifesto del servizio all'interno del pacchetto dell'applicazione di cui in precedenza è stato eseguito il provisioning.</span><span class="sxs-lookup"><span data-stu-id="9e689-139">The services that you can create from an application are defined in a service manifest in the previously provisioned application package.</span></span>

```azurecli
sfctl service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="9e689-140">Verificare l'integrità e la distribuzione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="9e689-140">Verify application deployment and health</span></span>

<span data-ttu-id="9e689-141">Per verificare l'integrità completa, usare i seguenti comandi di integrità:</span><span class="sxs-lookup"><span data-stu-id="9e689-141">To verify everything is healthy, use the following health commands:</span></span>

```azurecli
sfctl application list
sfctl service list --application-id TestApp
```

<span data-ttu-id="9e689-142">Per verificare l'integrità del servizio, usare comandi simili per recuperare lo stato sia del servizio che dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="9e689-142">To verify that the service is healthy, use similar commands to retrieve the health of both the service and the application:</span></span>

```azurecli
sfctl application health --application-id TestApp
sfctl service health --service-id TestApp/TestSvc
```

<span data-ttu-id="9e689-143">I servizi e le applicazioni integri devono avere il valore `HealthState` impostato su `Ok`.</span><span class="sxs-lookup"><span data-stu-id="9e689-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="9e689-144">Rimuovere un'applicazione esistente</span><span class="sxs-lookup"><span data-stu-id="9e689-144">Remove an existing application</span></span>

<span data-ttu-id="9e689-145">Per rimuovere un'applicazione, completare le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="9e689-145">To remove an application, complete the following tasks:</span></span>

### <a name="delete-the-application"></a><span data-ttu-id="9e689-146">Eliminare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="9e689-146">Delete the application</span></span>

<span data-ttu-id="9e689-147">Per eliminare l'applicazione, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9e689-147">To delete the application, use the following command:</span></span>

```azurecli
sfctl application delete --application-id TestEdApp
```

### <a name="unprovision-the-application-type"></a><span data-ttu-id="9e689-148">Annullare il provisioning del tipo di applicazione</span><span class="sxs-lookup"><span data-stu-id="9e689-148">Unprovision the application type</span></span>

<span data-ttu-id="9e689-149">Dopo aver eliminato l'applicazione, è possibile annullare il provisioning del tipo di applicazione se non è più necessario.</span><span class="sxs-lookup"><span data-stu-id="9e689-149">After you delete the application, you can unprovision the application type if you no longer need it.</span></span> <span data-ttu-id="9e689-150">Per annullare il provisioning del tipo di applicazione, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9e689-150">To unprovision the application type, use the following command:</span></span>

```azurecli
sfctl application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="9e689-151">Il nome del tipo e la versione del tipo devono corrispondere al nome e alla versione indicati nel manifesto dell'applicazione di cui in precedenza è stato eseguito il provisioning.</span><span class="sxs-lookup"><span data-stu-id="9e689-151">The type name and type version must match the name and version in the previously provisioned application manifest.</span></span>

### <a name="delete-the-application-package"></a><span data-ttu-id="9e689-152">Eliminare il pacchetto dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="9e689-152">Delete the application package</span></span>

<span data-ttu-id="9e689-153">Dopo avere annullato il provisioning del tipo di applicazione, è possibile eliminare il pacchetto dell'applicazione dall'archivio immagini se non è più necessario.</span><span class="sxs-lookup"><span data-stu-id="9e689-153">After you have unprovisioned the application type, you can delete the application package from the image store if you no longer need it.</span></span> <span data-ttu-id="9e689-154">L'eliminazione di pacchetti di applicazioni consente di recuperare spazio su disco.</span><span class="sxs-lookup"><span data-stu-id="9e689-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="9e689-155">Per eliminare il pacchetto dell'applicazione dall'archivio immagini, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9e689-155">To delete the application package from the image store, use the following command:</span></span>

```azurecli
sfctl store delete --content-path app_package_dir
```

<span data-ttu-id="9e689-156">`content-path` deve essere il nome della directory caricata al momento della creazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9e689-156">`content-path` must be the name of the directory that you uploaded when you created the application.</span></span>

## <a name="upgrade-application"></a><span data-ttu-id="9e689-157">Aggiornare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="9e689-157">Upgrade application</span></span>

<span data-ttu-id="9e689-158">Dopo avere creato l'applicazione, è possibile ripetere lo stesso set di passaggi per eseguire il provisioning di una seconda versione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9e689-158">After creating your application, you can repeat the same set of steps to provision a second version of your application.</span></span> <span data-ttu-id="9e689-159">Con un aggiornamento dell'applicazione Service Fabric è possibile passare a eseguire la seconda versione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9e689-159">Then, with a Service Fabric application upgrade you can transition to running the second version of the application.</span></span> <span data-ttu-id="9e689-160">Per altre informazioni, vedere la documentazione su [Aggiornamento di un'applicazione di Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="9e689-160">For more information, see the documentation on [Service Fabric application upgrades](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="9e689-161">Per eseguire un aggiornamento, eseguire prima il provisioning della versione successiva dell'applicazione usando gli stessi comandi, come indicato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="9e689-161">To perform an upgrade, first provision the next version of the application using the same commands as before:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir_2
sfctl application provision --application-type-build-path app_package_dir_2
```

<span data-ttu-id="9e689-162">Si consiglia quindi di eseguire un aggiornamento automatico monitorato, avviare l'aggiornamento usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9e689-162">It is recommended then to perform a monitored automatic upgrade, launch the upgrade by running the following command:</span></span>

```azurecli
sfctl application upgrade --app-id TestApp --app-version 2.0.0 --parameters "{\"test\":\"value\"}" --mode Monitored
```

<span data-ttu-id="9e689-163">Gli aggiornamenti eseguono l'override dei parametri esistenti con il set specificato.</span><span class="sxs-lookup"><span data-stu-id="9e689-163">Upgrades override existing parameters with whatever set is specified.</span></span> <span data-ttu-id="9e689-164">I parametri dell'applicazione devono essere passati come argomenti al comando di aggiornamento, se necessario.</span><span class="sxs-lookup"><span data-stu-id="9e689-164">Application parameters should be passed as arguments to the upgrade command, if necessary.</span></span> <span data-ttu-id="9e689-165">I parametri dell'applicazione devono essere codificati come oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="9e689-165">Application parameters should be encoded as a JSON object.</span></span>

<span data-ttu-id="9e689-166">Per recuperare tutti i parametri specificati in precedenza, è possibile usare il comando `sfctl application info`.</span><span class="sxs-lookup"><span data-stu-id="9e689-166">To retrieve any parameters previously specified, you can use the `sfctl application info` command.</span></span>

<span data-ttu-id="9e689-167">Quando un aggiornamento dell'applicazione è in corso, è possibile recuperare lo stato tramite il comando `sfctl application upgrade-status`.</span><span class="sxs-lookup"><span data-stu-id="9e689-167">When an application upgrade is in progress, the status can be retrieved using the `sfctl application upgrade-status` command.</span></span>

<span data-ttu-id="9e689-168">Infine, se un aggiornamento è in corso e deve essere annullato, è possibile usare `sfctl application upgrade-rollback` per eseguire il rollback dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="9e689-168">Finally, if an upgrade is in progress and needs to be canceled, you can use the `sfctl application upgrade-rollback` to roll back the upgrade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e689-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9e689-169">Next steps</span></span>

* <span data-ttu-id="9e689-170">[Azure Service Fabric command line](service-fabric-cli.md) (Riga di comando di Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="9e689-170">[Service Fabric CLI basics](service-fabric-cli.md)</span></span>
* [<span data-ttu-id="9e689-171">Introduzione a Service Fabric in Linux</span><span class="sxs-lookup"><span data-stu-id="9e689-171">Getting started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
* <span data-ttu-id="9e689-172">[Service Fabric application upgrade](service-fabric-application-upgrade.md) (Aggiornamento di un'applicazione Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="9e689-172">[Launching a Service Fabric application upgrade](service-fabric-application-upgrade.md)</span></span>
