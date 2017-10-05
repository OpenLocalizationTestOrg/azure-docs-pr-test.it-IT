---
title: "Come usare l'API di gestione dei servizi (Python) - Guida alle funzionalità"
description: "Informazioni su come eseguire attività comuni di gestione dei servizi a livello di codice da Python."
services: cloud-services
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: 61538ec0-1536-4a7e-ae89-95967fe35d73
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/30/2017
ms.author: lmazuel
ms.openlocfilehash: 13249ba9a4b317a3154776b411ce0bb1f316b3bb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-management-from-python"></a><span data-ttu-id="1b266-103">Come usare la gestione dei servizi da Python</span><span class="sxs-lookup"><span data-stu-id="1b266-103">How to use Service Management from Python</span></span>
<span data-ttu-id="1b266-104">La guida descrive come eseguire attività comuni di gestione dei servizi a livello di codice da Python.</span><span class="sxs-lookup"><span data-stu-id="1b266-104">This guide shows you how to programmatically perform common service management tasks from Python.</span></span> <span data-ttu-id="1b266-105">La classe **ServiceManagementService** disponibile in [Azure SDK per Python](https://github.com/Azure/azure-sdk-for-python) supporta l'accesso a livello di codice alla maggior parte delle funzionalità di gestione dei servizi disponibili tramite il [portale di Azure classico][management-portal] (ad esempio **creazione, aggiornamento ed eliminazione dei servizi cloud, distribuzioni, servizi di gestione dati e macchine virtuali**).</span><span class="sxs-lookup"><span data-stu-id="1b266-105">The **ServiceManagementService** class in the [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) supports programmatic access to much of the service management-related functionality that is available in the [Azure classic portal][management-portal] (such as **creating, updating, and deleting cloud services, deployments, data management services, and virtual machines**).</span></span> <span data-ttu-id="1b266-106">Questa funzionalità può rivelarsi utile nella creazione di applicazioni che richiedono accesso a livello di codice alla gestione dei servizi.</span><span class="sxs-lookup"><span data-stu-id="1b266-106">This functionality can be useful in building applications that need programmatic access to service management.</span></span>

## <span data-ttu-id="1b266-107"><a name="WhatIs"> </a>Informazioni sulla gestione dei servizi</span><span class="sxs-lookup"><span data-stu-id="1b266-107"><a name="WhatIs"> </a>What is Service Management</span></span>
<span data-ttu-id="1b266-108">L'API di gestione dei servizi fornisce l'accesso a livello di codice alla maggior parte delle funzionalità di gestione dei servizi disponibili tramite il [portale di Azure classico][management-portal].</span><span class="sxs-lookup"><span data-stu-id="1b266-108">The Service Management API provides programmatic access to much of the service management functionality available through the [Azure classic portal][management-portal].</span></span> <span data-ttu-id="1b266-109">Azure SDK per Python consente di gestire i servizi cloud e gli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1b266-109">The Azure SDK for Python allows you to manage your cloud services and storage accounts.</span></span>

<span data-ttu-id="1b266-110">Per usare l'API Gestione dei servizi, è necessario [creare un account Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1b266-110">To use the Service Management API, you need to [create an Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="1b266-111"><a name="Concepts"> </a>Concetti</span><span class="sxs-lookup"><span data-stu-id="1b266-111"><a name="Concepts"> </a>Concepts</span></span>
<span data-ttu-id="1b266-112">Azure SDK per Python include l'[API di Gestione servizi di Azure][svc-mgmt-rest-api], ovvero un'API REST.</span><span class="sxs-lookup"><span data-stu-id="1b266-112">The Azure SDK for Python wraps the [Azure Service Management API][svc-mgmt-rest-api], which is a REST API.</span></span> <span data-ttu-id="1b266-113">Tutte le operazioni dell'API vengono eseguite tramite SSL e autenticate reciprocamente con certificati X.509 v3.</span><span class="sxs-lookup"><span data-stu-id="1b266-113">All API operations are performed over SSL and mutually authenticated using X.509 v3 certificates.</span></span> <span data-ttu-id="1b266-114">Il servizio di gestione è accessibile da un servizio in esecuzione in Azure o direttamente tramite Internet da qualsiasi applicazione in grado di inviare una richiesta HTTPS e ricevere una risposta HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1b266-114">The management service may be accessed from within a service running in Azure, or directly over the Internet from any application that can send an HTTPS request and receive an HTTPS response.</span></span>

## <span data-ttu-id="1b266-115"><a name="Installation"> </a>Installazione</span><span class="sxs-lookup"><span data-stu-id="1b266-115"><a name="Installation"> </a>Installation</span></span>
<span data-ttu-id="1b266-116">Tutte le funzionalità descritte in questo articolo sono disponibili nel pacchetto `azure-servicemanagement-legacy` che è possibile installare tramite pip.</span><span class="sxs-lookup"><span data-stu-id="1b266-116">All the features described in this article are available in the `azure-servicemanagement-legacy` package, which you can install using pip.</span></span> <span data-ttu-id="1b266-117">Per altre informazioni sull'installazione, ad esempio se non si ha familiarità con Python, vedere l'articolo relativo all'[installazione di Python e Azure SDK](../python-how-to-install.md)</span><span class="sxs-lookup"><span data-stu-id="1b266-117">For more information about installation (for example, if you are new to Python), see this article: [Installing Python and the Azure SDK](../python-how-to-install.md)</span></span>

## <span data-ttu-id="1b266-118"><a name="Connect"> </a>Procedura: Connettersi alla gestione dei servizi</span><span class="sxs-lookup"><span data-stu-id="1b266-118"><a name="Connect"> </a>How to: Connect to service management</span></span>
<span data-ttu-id="1b266-119">Per connettersi all'endpoint di gestione dei servizi, sono necessari un ID sottoscrizione di Azure e un certificato di gestione valido.</span><span class="sxs-lookup"><span data-stu-id="1b266-119">To connect to the Service Management endpoint, you need your Azure subscription ID and a valid management certificate.</span></span> <span data-ttu-id="1b266-120">È possibile ottenere l'ID sottoscrizione tramite il [portale di Azure classico][management-portal].</span><span class="sxs-lookup"><span data-stu-id="1b266-120">You can obtain your subscription ID through the [Azure classic portal][management-portal].</span></span>

> [!NOTE]
> <span data-ttu-id="1b266-121">È ora possibile usare i certificati creati con OpenSSL per l'esecuzione in Windows.</span><span class="sxs-lookup"><span data-stu-id="1b266-121">It is now possible to use certificates created with OpenSSL when running on Windows.</span></span>  <span data-ttu-id="1b266-122">È necessario Python 2.7.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="1b266-122">It requires Python 2.7.4 or later.</span></span> <span data-ttu-id="1b266-123">Per gli utenti è consigliabile usare i certificati OpenSSL anziché pfx, perché il supporto per i certificati pfx verrà probabilmente rimosso in futuro.</span><span class="sxs-lookup"><span data-stu-id="1b266-123">We recommend users to use OpenSSL instead of .pfx, since support for .pfx certificates will likely be removed in the future.</span></span>
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a><span data-ttu-id="1b266-124">Certificati di gestione in Windows/Mac/Linux (OpenSSL)</span><span class="sxs-lookup"><span data-stu-id="1b266-124">Management certificates on Windows/Mac/Linux (OpenSSL)</span></span>
<span data-ttu-id="1b266-125">Per creare il certificato di gestione, è possibile utilizzare [OpenSSL](http://www.openssl.org/) .</span><span class="sxs-lookup"><span data-stu-id="1b266-125">You can use [OpenSSL](http://www.openssl.org/) to create your management certificate.</span></span>  <span data-ttu-id="1b266-126">È in realtà necessario creare due certificati, uno per il server (un file `.cer`) e uno per il client (un file `.pem`).</span><span class="sxs-lookup"><span data-stu-id="1b266-126">You actually need to create two certificates, one for the server (a `.cer` file) and one for the client (a `.pem` file).</span></span> <span data-ttu-id="1b266-127">Per creare il file `.pem` , eseguire:</span><span class="sxs-lookup"><span data-stu-id="1b266-127">To create the `.pem` file, execute:</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="1b266-128">Per creare il certificato `.cer` , eseguire:</span><span class="sxs-lookup"><span data-stu-id="1b266-128">To create the `.cer` certificate, execute:</span></span>

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

<span data-ttu-id="1b266-129">Per altre informazioni sui certificati di Azure, vedere [Panoramica sui certificati per i servizi cloud di Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="1b266-129">For more information about Azure certificates, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="1b266-130">Per una descrizione completa dei parametri OpenSSL, vedere la documentazione disponibile all'indirizzo [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span><span class="sxs-lookup"><span data-stu-id="1b266-130">For a complete description of OpenSSL parameters, see the documentation at [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span></span>

<span data-ttu-id="1b266-131">Dopo avere creato questi file è necessario caricare il file `.cer` in Azure selezionando l'opzione "Carica" della scheda "Impostazioni" del [portale di Azure classico][management-portal] ed è anche necessario prendere nota del percorso di salvataggio del file `.pem`.</span><span class="sxs-lookup"><span data-stu-id="1b266-131">After you have created these files, you need to upload the `.cer` file to Azure via the "Upload" action of the "Settings" tab of the [Azure classic portal][management-portal], and you need to make note of where you saved the `.pem` file.</span></span>

<span data-ttu-id="1b266-132">Dopo aver ottenuto l'ID sottoscrizione, aver creato un certificato e aver caricato il file `.cer` in Azure è possibile connettersi all'endpoint di gestione di Azure passando l'ID sottoscrizione e il percorso del file `.pem` a **ServiceManagementService**:</span><span class="sxs-lookup"><span data-stu-id="1b266-132">After you have obtained your subscription ID, created a certificate, and uploaded the `.cer` file to Azure, you can connect to the Azure management endpoint by passing the subscription id and the path to the `.pem` file to **ServiceManagementService**:</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="1b266-133">Nell'esempio precedente `sms` è un oggetto **ServiceManagementService** .</span><span class="sxs-lookup"><span data-stu-id="1b266-133">In the preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="1b266-134">La classe **ServiceManagementService** è la classe principale usata per gestire i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b266-134">The **ServiceManagementService** class is the primary class used to manage Azure services.</span></span>

### <a name="management-certificates-on-windows-makecert"></a><span data-ttu-id="1b266-135">Certificati di gestione in Windows (MakeCert)</span><span class="sxs-lookup"><span data-stu-id="1b266-135">Management certificates on Windows (MakeCert)</span></span>
<span data-ttu-id="1b266-136">È possibile creare nel computer un certificato di gestione autofirmato usando `makecert.exe`.</span><span class="sxs-lookup"><span data-stu-id="1b266-136">You can create a self-signed management certificate on your machine using `makecert.exe`.</span></span>  <span data-ttu-id="1b266-137">Aprire un **prompt dei comandi di Visual Studio** come **amministratore** e usare il comando seguente, sostituendo *AzureCertificate* con il nome del certificato da usare.</span><span class="sxs-lookup"><span data-stu-id="1b266-137">Open a **Visual Studio command prompt** as an **administrator** and use the following command, replacing *AzureCertificate* with the certificate name you would like to use.</span></span>

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

<span data-ttu-id="1b266-138">Il comando consente di creare il file `.cer` e di installarlo nell'archivio certificati **Personale** .</span><span class="sxs-lookup"><span data-stu-id="1b266-138">The command creates the `.cer` file, and installs it in the **Personal** certificate store.</span></span> <span data-ttu-id="1b266-139">Per altre informazioni, vedere [Panoramica sui certificati per i servizi cloud di Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="1b266-139">For more information, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span>

<span data-ttu-id="1b266-140">Dopo avere creato il certificato è necessario caricare il file `.cer` in Azure selezionando l'opzione "Carica" della scheda "Impostazioni" del [portale di Azure classico][management-portal].</span><span class="sxs-lookup"><span data-stu-id="1b266-140">After you have created the certificate, you need to upload the `.cer` file to Azure via the "Upload" action of the "Settings" tab of the [Azure classic portal][management-portal].</span></span>

<span data-ttu-id="1b266-141">Dopo aver ottenuto l'ID sottoscrizione, aver creato un certificato e aver caricato il file `.cer` in Azure, è possibile connettersi all'endpoint di gestione di Azure passando l'ID sottoscrizione e il percorso del certificato nell'archivio certificati **personale** a **ServiceManagementService**. Anche in questo caso, sostituire *AzureCertificate* con il nome del proprio certificato:</span><span class="sxs-lookup"><span data-stu-id="1b266-141">After you have obtained your subscription ID, created a certificate, and uploaded the `.cer` file to Azure, you can connect to the Azure management endpoint by passing the subscription id and the location of the certificate in your **Personal** certificate store to **ServiceManagementService** (again, replace *AzureCertificate* with the name of your certificate):</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="1b266-142">Nell'esempio precedente `sms` è un oggetto **ServiceManagementService** .</span><span class="sxs-lookup"><span data-stu-id="1b266-142">In the preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="1b266-143">La classe **ServiceManagementService** è la classe principale usata per gestire i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b266-143">The **ServiceManagementService** class is the primary class used to manage Azure services.</span></span>

## <span data-ttu-id="1b266-144"><a name="ListAvailableLocations"> </a>Procedura: Creare un elenco delle località disponibili</span><span class="sxs-lookup"><span data-stu-id="1b266-144"><a name="ListAvailableLocations"> </a>How to: List available locations</span></span>
<span data-ttu-id="1b266-145">Per elencare le località disponibili per i servizi di hosting, usare il metodo **list\_locations**:</span><span class="sxs-lookup"><span data-stu-id="1b266-145">To list the locations that are available for hosting services, use the **list\_locations** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

<span data-ttu-id="1b266-146">Quando si crea un servizio cloud o un servizio di archiviazione, è necessario fornire una località valida.</span><span class="sxs-lookup"><span data-stu-id="1b266-146">When you create a cloud service or storage service you need to provide a valid location.</span></span> <span data-ttu-id="1b266-147">Il metodo **list\_locations** restituisce sempre un elenco aggiornato delle località attualmente disponibili.</span><span class="sxs-lookup"><span data-stu-id="1b266-147">The **list\_locations** method always returns an up-to-date list of the currently available locations.</span></span> <span data-ttu-id="1b266-148">Al momento della stesura di questo articolo, le località disponibili sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="1b266-148">As of this writing, the available locations are:</span></span>

* <span data-ttu-id="1b266-149">Europa occidentale</span><span class="sxs-lookup"><span data-stu-id="1b266-149">West Europe</span></span>
* <span data-ttu-id="1b266-150">Europa settentrionale</span><span class="sxs-lookup"><span data-stu-id="1b266-150">North Europe</span></span>
* <span data-ttu-id="1b266-151">Asia sudorientale</span><span class="sxs-lookup"><span data-stu-id="1b266-151">Southeast Asia</span></span>
* <span data-ttu-id="1b266-152">Asia orientale</span><span class="sxs-lookup"><span data-stu-id="1b266-152">East Asia</span></span>
* <span data-ttu-id="1b266-153">Stati Uniti centrali</span><span class="sxs-lookup"><span data-stu-id="1b266-153">Central US</span></span>
* <span data-ttu-id="1b266-154">Stati Uniti centro-settentrionali</span><span class="sxs-lookup"><span data-stu-id="1b266-154">North Central US</span></span>
* <span data-ttu-id="1b266-155">Stati Uniti centro-meridionali</span><span class="sxs-lookup"><span data-stu-id="1b266-155">South Central US</span></span>
* <span data-ttu-id="1b266-156">Stati Uniti occidentali</span><span class="sxs-lookup"><span data-stu-id="1b266-156">West US</span></span>
* <span data-ttu-id="1b266-157">Stati Uniti orientali</span><span class="sxs-lookup"><span data-stu-id="1b266-157">East US</span></span>
* <span data-ttu-id="1b266-158">Giappone orientale</span><span class="sxs-lookup"><span data-stu-id="1b266-158">Japan East</span></span>
* <span data-ttu-id="1b266-159">Giappone occidentale</span><span class="sxs-lookup"><span data-stu-id="1b266-159">Japan West</span></span>
* <span data-ttu-id="1b266-160">Brasile meridionale</span><span class="sxs-lookup"><span data-stu-id="1b266-160">Brazil South</span></span>
* <span data-ttu-id="1b266-161">Australia orientale</span><span class="sxs-lookup"><span data-stu-id="1b266-161">Australia East</span></span>
* <span data-ttu-id="1b266-162">Australia sudorientale</span><span class="sxs-lookup"><span data-stu-id="1b266-162">Australia Southeast</span></span>

## <span data-ttu-id="1b266-163"><a name="CreateCloudService"> </a>Procedura: Creare un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="1b266-163"><a name="CreateCloudService"> </a>How to: Create a cloud service</span></span>
<span data-ttu-id="1b266-164">Quando si crea un'applicazione e la si esegue in Azure, la combinazione del codice e della configurazione costituisce il cosiddetto [servizio cloud][cloud service] di Azure (noto come *servizio ospitato* in versioni precedenti di Azure).</span><span class="sxs-lookup"><span data-stu-id="1b266-164">When you create an application and run it in Azure, the code and configuration together are called an Azure [cloud service][cloud service] (known as a *hosted service* in earlier Azure releases).</span></span> <span data-ttu-id="1b266-165">Il metodo **create\_hosted\_service** consente di creare un nuovo servizio ospitato specificando un nome di servizio ospitato che deve essere univoco in Azure, un'etichetta con codifica Base64 automatica, una descrizione e una località.</span><span class="sxs-lookup"><span data-stu-id="1b266-165">The **create\_hosted\_service** method allows you to create a new hosted service by providing a hosted service name (which must be unique in Azure), a label (automatically encoded to base64), a description, and a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

<span data-ttu-id="1b266-166">Per elencare tutti i servizi ospitati per la sottoscrizione, è possibile usare il metodo **list\_hosted\_services**:</span><span class="sxs-lookup"><span data-stu-id="1b266-166">You can list all the hosted services for your subscription with the **list\_hosted\_services** method:</span></span>

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

<span data-ttu-id="1b266-167">Per ottenere eventuali informazioni su un particolare servizio ospitato, passare il nome del servizio ospitato al metodo **get\_hosted\_service\_properties**:</span><span class="sxs-lookup"><span data-stu-id="1b266-167">If you want to get information about a particular hosted service, you can do so by passing the hosted service name to the **get\_hosted\_service\_properties** method:</span></span>

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

<span data-ttu-id="1b266-168">Dopo aver creato un servizio cloud è possibile distribuire il codice al servizio con il metodo **create\_deployment**.</span><span class="sxs-lookup"><span data-stu-id="1b266-168">After you have created a cloud service, you can deploy your code to the service with the **create\_deployment** method.</span></span>

## <span data-ttu-id="1b266-169"><a name="DeleteCloudService"> </a>Procedura: Eliminare un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="1b266-169"><a name="DeleteCloudService"> </a>How to: Delete a cloud service</span></span>
<span data-ttu-id="1b266-170">È possibile eliminare un servizio cloud passando il nome del servizio al metodo **delete\_hosted\_service**:</span><span class="sxs-lookup"><span data-stu-id="1b266-170">You can delete a cloud service by passing the service name to the **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service('myhostedservice')

<span data-ttu-id="1b266-171">Prima di eliminare un servizio è necessario eliminare tutte le distribuzioni del servizio.</span><span class="sxs-lookup"><span data-stu-id="1b266-171">Before you can delete a service, all deployments for the service must first be deleted.</span></span> <span data-ttu-id="1b266-172">Per informazioni dettagliate, vedere [Procedura: Eliminare una distribuzione](#DeleteDeployment) .</span><span class="sxs-lookup"><span data-stu-id="1b266-172">(See [How to: Delete a deployment](#DeleteDeployment) for details.)</span></span>

## <span data-ttu-id="1b266-173"><a name="DeleteDeployment"> </a>Procedura: Eliminare una distribuzione</span><span class="sxs-lookup"><span data-stu-id="1b266-173"><a name="DeleteDeployment"> </a>How to: Delete a deployment</span></span>
<span data-ttu-id="1b266-174">Per eliminare una distribuzione, usare il metodo **delete\_deployment**.</span><span class="sxs-lookup"><span data-stu-id="1b266-174">To delete a deployment, use the **delete\_deployment** method.</span></span> <span data-ttu-id="1b266-175">L'esempio seguente mostra come eliminare una distribuzione denominata `v1`.</span><span class="sxs-lookup"><span data-stu-id="1b266-175">The following example shows how to delete a deployment named `v1`.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <span data-ttu-id="1b266-176"><a name="CreateStorageService"> </a>Procedura: Creare un servizio di archiviazione</span><span class="sxs-lookup"><span data-stu-id="1b266-176"><a name="CreateStorageService"> </a>How to: Create a storage service</span></span>
<span data-ttu-id="1b266-177">Un [servizio di archiviazione](../storage/common/storage-create-storage-account.md) offre l'accesso ai [BLOB](../storage/blobs/storage-python-how-to-use-blob-storage.md), alle [tabelle](../cosmos-db/table-storage-how-to-use-python.md) e alle [code](../storage/queues/storage-python-how-to-use-queue-storage.md) di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b266-177">A [storage service](../storage/common/storage-create-storage-account.md) gives you access to Azure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [Tables](../cosmos-db/table-storage-how-to-use-python.md), and [Queues](../storage/queues/storage-python-how-to-use-queue-storage.md).</span></span> <span data-ttu-id="1b266-178">Per creare un servizio di archiviazione, è necessario assegnare al servizio un nome di lunghezza compresa tra 3 e 24 caratteri minuscoli e univoco in Azure, nonché una descrizione, un'etichetta fino a 100 caratteri con codifica in Base64 automatica e una località.</span><span class="sxs-lookup"><span data-stu-id="1b266-178">To create a storage service, you need a name for the service (between 3 and 24 lowercase characters and unique within Azure), a description, a label (up to 100 characters, automatically encoded to base64), and a location.</span></span> <span data-ttu-id="1b266-179">Nell'esempio seguente viene illustrato come creare un servizio di archiviazione specificando una località.</span><span class="sxs-lookup"><span data-stu-id="1b266-179">The following example shows how to create a storage service by specifying a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mystorageaccount'
    label = 'mystorageaccount'
    location = 'West US'
    desc = 'My storage account description.'

    result = sms.create_storage_account(name, desc, label, location=location)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="1b266-180">Si noti nell'esempio precedente che è possibile recuperare lo stato dell'operazione **create\_storage\_account** passando il risultato restituito da **create\_storage\_account** al metodo **get\_operation\_status**.</span><span class="sxs-lookup"><span data-stu-id="1b266-180">Note in the preceding example that the status of the **create\_storage\_account** operation can be retrieved by passing the result returned by **create\_storage\_account** to the **get\_operation\_status** method.</span></span>  

<span data-ttu-id="1b266-181">È possibile elencare gli account di archiviazione e le relative proprietà con il metodo **list\_storage\_accounts**:</span><span class="sxs-lookup"><span data-stu-id="1b266-181">You can list your storage accounts and their properties with the **list\_storage\_accounts** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <span data-ttu-id="1b266-182"><a name="DeleteStorageService"> </a>Procedura: Eliminare un servizio di archiviazione</span><span class="sxs-lookup"><span data-stu-id="1b266-182"><a name="DeleteStorageService"> </a>How to: Delete a storage service</span></span>
<span data-ttu-id="1b266-183">È possibile eliminare un servizio di archiviazione passando il relativo nome al metodo **delete\_storage\_account**.</span><span class="sxs-lookup"><span data-stu-id="1b266-183">You can delete a storage service by passing the storage service name to the **delete\_storage\_account** method.</span></span> <span data-ttu-id="1b266-184">L'eliminazione di un servizio di archiviazione comporta l'eliminazione di tutti i dati archiviati nel servizio: BLOB, tabelle e code.</span><span class="sxs-lookup"><span data-stu-id="1b266-184">Deleting a storage service deletes all data stored in the service (blobs, tables, and queues).</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <span data-ttu-id="1b266-185"><a name="ListOperatingSystems"> </a>Procedura: Elencare i sistemi operativi disponibili</span><span class="sxs-lookup"><span data-stu-id="1b266-185"><a name="ListOperatingSystems"> </a>How to: List available operating systems</span></span>
<span data-ttu-id="1b266-186">Per elencare i sistemi operativi disponibili per i servizi di hosting, usare il metodo **list\_operating\_systems**:</span><span class="sxs-lookup"><span data-stu-id="1b266-186">To list the operating systems that are available for hosting services, use the **list\_operating\_systems** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

<span data-ttu-id="1b266-187">In alternativa, è possibile usare il metodo **list\_operating\_system\_families** che consente di raggruppare i sistemi operativi in base alla famiglia:</span><span class="sxs-lookup"><span data-stu-id="1b266-187">Alternatively, you can use the **list\_operating\_system\_families** method, which groups the operating systems by family:</span></span>

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <span data-ttu-id="1b266-188"><a name="CreateVMImage"> </a>Procedura: Creare un'immagine del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="1b266-188"><a name="CreateVMImage"> </a>How to: Create an operating system image</span></span>
<span data-ttu-id="1b266-189">Per aggiungere un'immagine del sistema operativo all'archivio di immagini, usare il metodo **add\_os\_image**:</span><span class="sxs-lookup"><span data-stu-id="1b266-189">To add an operating system image to the image repository, use the **add\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mycentos'
    label = 'mycentos'
    os = 'Linux' # Linux or Windows
    media_link = 'url_to_storage_blob_for_source_image_vhd'

    result = sms.add_os_image(label, media_link, name, os)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="1b266-190">Per elencare le immagini del sistema operativo disponibili, usare il metodo **list\_os\_images**.</span><span class="sxs-lookup"><span data-stu-id="1b266-190">To list the operating system images that are available, use the **list\_os\_images** method.</span></span> <span data-ttu-id="1b266-191">Sono incluse tutte le immagini di piattaforma e utente:</span><span class="sxs-lookup"><span data-stu-id="1b266-191">It includes all platform images and user images:</span></span>

    result = sms.list_os_images()

    for image in result:
        print('Name: ' + image.name)
        print('Label: ' + image.label)
        print('OS: ' + image.os)
        print('Category: ' + image.category)
        print('Description: ' + image.description)
        print('Location: ' + image.location)
        print('Media link: ' + image.media_link)
        print('')

## <span data-ttu-id="1b266-192"><a name="DeleteVMImage"> </a>Procedura: Eliminare un'immagine del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="1b266-192"><a name="DeleteVMImage"> </a>How to: Delete an operating system image</span></span>
<span data-ttu-id="1b266-193">Per eliminare un'immagine dell'utente, usare il metodo **delete\_os\_image**:</span><span class="sxs-lookup"><span data-stu-id="1b266-193">To delete a user image, use the **delete\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <span data-ttu-id="1b266-194"><a name="CreateVM"> </a>Procedura: Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="1b266-194"><a name="CreateVM"> </a>How to: Create a virtual machine</span></span>
<span data-ttu-id="1b266-195">Per creare una macchina virtuale, è necessario creare un [servizio cloud](#CreateCloudService)</span><span class="sxs-lookup"><span data-stu-id="1b266-195">To create a virtual machine, you first need to create a [cloud service](#CreateCloudService).</span></span>  <span data-ttu-id="1b266-196">prima di creare la distribuzione della macchina virtuale tramite il metodo **create\_virtual\_machine\_deployment**:</span><span class="sxs-lookup"><span data-stu-id="1b266-196">Then create the virtual machine deployment using the **create\_virtual\_machine\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set the location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where the VM disk
    # will be created
    media_link = 'url_to_target_storage_blob_for_vm_hd'

    # Linux VM configuration, you can use WindowsConfigurationSet
    # for a Windows VM instead
    linux_config = LinuxConfigurationSet('myhostname', 'myuser', 'mypassword', True)

    os_hd = OSVirtualHardDisk(image_name, media_link)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=os_hd,
        role_size='Small')

## <span data-ttu-id="1b266-197"><a name="DeleteVM"> </a>Procedura: Eliminare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="1b266-197"><a name="DeleteVM"> </a>How to: Delete a virtual machine</span></span>
<span data-ttu-id="1b266-198">Per eliminare una macchina virtuale, è prima necessario eliminare la distribuzione tramite il metodo **delete\_deployment**:</span><span class="sxs-lookup"><span data-stu-id="1b266-198">To delete a virtual machine, you first delete the deployment using the **delete\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

<span data-ttu-id="1b266-199">Sarà quindi possibile eliminare il servizio cloud usando il metodo **delete\_hosted\_service**:</span><span class="sxs-lookup"><span data-stu-id="1b266-199">The cloud service can then be deleted using the **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a><span data-ttu-id="1b266-200">Procedura: Creare una macchina virtuale da un'immagine di macchina virtuale acquisita</span><span class="sxs-lookup"><span data-stu-id="1b266-200">How To: Create a Virtual Machine from a Captured Virtual Machine Image</span></span>
<span data-ttu-id="1b266-201">Per acquisire un'immagine di macchina virtuale, è prima necessario chiamare il metodo **capture\_vm\_image**:</span><span class="sxs-lookup"><span data-stu-id="1b266-201">To capture a VM image, you first call the **capture\_vm\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace the below three parameters with actual values
    hosted_service_name = 'hs1'
    deployment_name = 'dep1'
    vm_name = 'vm1'

    image_name = vm_name + 'image'
    image = CaptureRoleAsVMImage    ('Specialized',
        image_name,
        image_name + 'label',
        image_name + 'description',
        'english',
        'mygroup')

    result = sms.capture_vm_image(
            hosted_service_name,
            deployment_name,
            vm_name,
            image
        )

<span data-ttu-id="1b266-202">Per verificare quindi di aver acquisito l'immagine correttamente, usare l'API **list\_vm\_images** e accertarsi che l'immagine venga visualizzata nei risultati:</span><span class="sxs-lookup"><span data-stu-id="1b266-202">Next, to make sure that you have successfully captured the image, use the **list\_vm\_images** api, and make sure your image is displayed in the results:</span></span>

    images = sms.list_vm_images()

<span data-ttu-id="1b266-203">Per creare infine la macchina virtuale con l'immagine acquisita, usare il metodo **create\_virtual\_machine\_deployment** come fatto in precedenza, ma questa volta passare vm_image_name.</span><span class="sxs-lookup"><span data-stu-id="1b266-203">To finally create the virtual machine using the captured image, use the **create\_virtual\_machine\_deployment** method as before, but this time pass in the vm_image_name instead</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set the location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=None,
        role_size='Small',
        vm_image_name = image_name)

<span data-ttu-id="1b266-204">Per altre informazioni su come acquisire una macchina virtuale Linux, vedere [Come acquisire una macchina virtuale Linux](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1b266-204">To learn more about how to capture a Linux Virtual Machine, see [How to Capture a Linux Virtual Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="1b266-205">Per altre informazioni su come acquisire una macchina virtuale Windows, vedere [Come acquisire una macchina virtuale Windows](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1b266-205">To learn more about how to capture a Windows Virtual Machine, see [How to Capture a Windows Virtual Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="1b266-206"><a name="What's Next"> </a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1b266-206"><a name="What's Next"> </a>Next Steps</span></span>
<span data-ttu-id="1b266-207">A questo punto, dopo aver appreso le nozioni di base della gestione dei servizi, è possibile accedere alla [documentazione completa di riferimento all'API per Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) ed eseguire facilmente le complesse attività di gestione dell'applicazione Python.</span><span class="sxs-lookup"><span data-stu-id="1b266-207">Now that you've learned the basics of service management, you can access the [Complete API reference documentation for the Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) and perform complex tasks easily to manage your python application.</span></span>

<span data-ttu-id="1b266-208">Per ulteriori informazioni, vedere il [Centro per sviluppatori di Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="1b266-208">For more information, see the [Python Developer Center](/develop/python/).</span></span>

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect to service management]: #Connect
[How to: List available locations]: #ListAvailableLocations
[How to: Create a cloud service]: #CreateCloudService
[How to: Delete a cloud service]: #DeleteCloudService
[How to: Create a deployment]: #CreateDeployment
[How to: Update a deployment]: #UpdateDeployment
[How to: Move deployments between staging and production]: #MoveDeployments
[How to: Delete a deployment]: #DeleteDeployment
[How to: Create a storage service]: #CreateStorageService
[How to: Delete a storage service]: #DeleteStorageService
[How to: List available operating systems]: #ListOperatingSystems
[How to: Create an operating system image]: #CreateVMImage
[How to: Delete an operating system image]: #DeleteVMImage
[How to: Create a virtual machine]: #CreateVM
[How to: Delete a virtual machine]: #DeleteVM
[Next Steps]: #NextSteps
[management-portal]: https://manage.windowsazure.com/
[svc-mgmt-rest-api]: http://msdn.microsoft.com/library/windowsazure/ee460799.aspx


[cloud service]:/services/cloud-services/
