---
title: "aaaHow toouse hello API gestione dei servizi (Python) - Guida alle funzionalità"
description: "Informazioni su come eseguire attività comuni di gestione del servizio di tooprogrammatically da Python."
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
ms.openlocfilehash: b59622203470e1586484cec4033515edb39ca4d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-management-from-python"></a><span data-ttu-id="b54ca-103">La gestione dei servizi da Python toouse</span><span class="sxs-lookup"><span data-stu-id="b54ca-103">How toouse Service Management from Python</span></span>
<span data-ttu-id="b54ca-104">Questa guida viene illustrato come eseguire attività comuni di gestione del servizio di tooprogrammatically da Python.</span><span class="sxs-lookup"><span data-stu-id="b54ca-104">This guide shows you how tooprogrammatically perform common service management tasks from Python.</span></span> <span data-ttu-id="b54ca-105">Hello **ServiceManagementService** classe hello [Azure SDK per Python](https://github.com/Azure/azure-sdk-for-python) supporta l'accesso programmatico toomuch di hello-relative alla gestione delle funzionalità del servizio che è disponibile in hello [Portale di azure classico] [ management-portal] (ad esempio **creazione, aggiornamento ed eliminazione di servizi cloud, le distribuzioni, servizi di gestione dati e le macchine virtuali**).</span><span class="sxs-lookup"><span data-stu-id="b54ca-105">hello **ServiceManagementService** class in hello [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) supports programmatic access toomuch of hello service management-related functionality that is available in hello [Azure classic portal][management-portal] (such as **creating, updating, and deleting cloud services, deployments, data management services, and virtual machines**).</span></span> <span data-ttu-id="b54ca-106">Questa funzionalità può essere utile per la creazione di applicazioni che richiedono la gestione di accesso a livello di codice tooservice.</span><span class="sxs-lookup"><span data-stu-id="b54ca-106">This functionality can be useful in building applications that need programmatic access tooservice management.</span></span>

## <span data-ttu-id="b54ca-107"><a name="WhatIs"></a>Informazioni sulla gestione dei servizi</span><span class="sxs-lookup"><span data-stu-id="b54ca-107"><a name="WhatIs"> </a>What is Service Management</span></span>
<span data-ttu-id="b54ca-108">Hello API del servizio di gestione fornisce l'accesso programmatico toomuch di funzionalità di Gestione servizio hello disponibili tramite hello [portale di Azure classico][management-portal].</span><span class="sxs-lookup"><span data-stu-id="b54ca-108">hello Service Management API provides programmatic access toomuch of hello service management functionality available through hello [Azure classic portal][management-portal].</span></span> <span data-ttu-id="b54ca-109">Hello Azure SDK per Python consente toomanage i servizi cloud e account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b54ca-109">hello Azure SDK for Python allows you toomanage your cloud services and storage accounts.</span></span>

<span data-ttu-id="b54ca-110">API di gestione del servizio hello toouse, è necessario troppo[creare un account Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b54ca-110">toouse hello Service Management API, you need too[create an Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="b54ca-111"><a name="Concepts"></a>Concetti</span><span class="sxs-lookup"><span data-stu-id="b54ca-111"><a name="Concepts"> </a>Concepts</span></span>
<span data-ttu-id="b54ca-112">esegue il wrapping di Hello Azure SDK per Python hello [API di gestione del servizio di Azure][svc-mgmt-rest-api], che è un'API REST.</span><span class="sxs-lookup"><span data-stu-id="b54ca-112">hello Azure SDK for Python wraps hello [Azure Service Management API][svc-mgmt-rest-api], which is a REST API.</span></span> <span data-ttu-id="b54ca-113">Tutte le operazioni dell'API vengono eseguite tramite SSL e autenticate reciprocamente con certificati X.509 v3.</span><span class="sxs-lookup"><span data-stu-id="b54ca-113">All API operations are performed over SSL and mutually authenticated using X.509 v3 certificates.</span></span> <span data-ttu-id="b54ca-114">il servizio di gestione di Hello sono accessibili da un servizio in esecuzione in Azure o direttamente su hello Internet da qualsiasi applicazione in grado di inviare una richiesta HTTPS e ricevere una risposta HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b54ca-114">hello management service may be accessed from within a service running in Azure, or directly over hello Internet from any application that can send an HTTPS request and receive an HTTPS response.</span></span>

## <span data-ttu-id="b54ca-115"><a name="Installation"> </a>Installazione</span><span class="sxs-lookup"><span data-stu-id="b54ca-115"><a name="Installation"> </a>Installation</span></span>
<span data-ttu-id="b54ca-116">Tutte le funzionalità di hello descritte in questo articolo sono disponibili in hello `azure-servicemanagement-legacy` pacchetto, è possibile installare l'uso di pip.</span><span class="sxs-lookup"><span data-stu-id="b54ca-116">All hello features described in this article are available in hello `azure-servicemanagement-legacy` package, which you can install using pip.</span></span> <span data-ttu-id="b54ca-117">Per ulteriori informazioni sull'installazione (ad esempio, se si è tooPython nuova), vedere questo articolo: [l'installazione di Python e hello Azure SDK](../python-how-to-install.md)</span><span class="sxs-lookup"><span data-stu-id="b54ca-117">For more information about installation (for example, if you are new tooPython), see this article: [Installing Python and hello Azure SDK](../python-how-to-install.md)</span></span>

## <span data-ttu-id="b54ca-118"><a name="Connect"></a>Procedura: connettersi a gestione tooservice</span><span class="sxs-lookup"><span data-stu-id="b54ca-118"><a name="Connect"> </a>How to: Connect tooservice management</span></span>
<span data-ttu-id="b54ca-119">endpoint di gestione dei servizi toohello tooconnect, è necessario l'ID sottoscrizione Azure e un certificato di gestione valido.</span><span class="sxs-lookup"><span data-stu-id="b54ca-119">tooconnect toohello Service Management endpoint, you need your Azure subscription ID and a valid management certificate.</span></span> <span data-ttu-id="b54ca-120">È possibile ottenere l'ID sottoscrizione tramite hello [portale di Azure classico][management-portal].</span><span class="sxs-lookup"><span data-stu-id="b54ca-120">You can obtain your subscription ID through hello [Azure classic portal][management-portal].</span></span>

> [!NOTE]
> <span data-ttu-id="b54ca-121">È ora possibile toouse certificati creati con OpenSSL durante l'esecuzione in Windows.</span><span class="sxs-lookup"><span data-stu-id="b54ca-121">It is now possible toouse certificates created with OpenSSL when running on Windows.</span></span>  <span data-ttu-id="b54ca-122">È necessario Python 2.7.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="b54ca-122">It requires Python 2.7.4 or later.</span></span> <span data-ttu-id="b54ca-123">Gli utenti toouse OpenSSL anziché con estensione pfx, è consigliabile poiché il supporto per certificati verranno probabilmente rimossa in futuro hello pfx.</span><span class="sxs-lookup"><span data-stu-id="b54ca-123">We recommend users toouse OpenSSL instead of .pfx, since support for .pfx certificates will likely be removed in hello future.</span></span>
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a><span data-ttu-id="b54ca-124">Certificati di gestione in Windows/Mac/Linux (OpenSSL)</span><span class="sxs-lookup"><span data-stu-id="b54ca-124">Management certificates on Windows/Mac/Linux (OpenSSL)</span></span>
<span data-ttu-id="b54ca-125">È possibile utilizzare [OpenSSL](http://www.openssl.org/) toocreate il certificato di gestione.</span><span class="sxs-lookup"><span data-stu-id="b54ca-125">You can use [OpenSSL](http://www.openssl.org/) toocreate your management certificate.</span></span>  <span data-ttu-id="b54ca-126">È necessario effettivamente toocreate due certificati, uno per il server di hello (un `.cer` file) e uno per i client hello (un `.pem` file).</span><span class="sxs-lookup"><span data-stu-id="b54ca-126">You actually need toocreate two certificates, one for hello server (a `.cer` file) and one for hello client (a `.pem` file).</span></span> <span data-ttu-id="b54ca-127">hello toocreate `.pem` file, eseguire:</span><span class="sxs-lookup"><span data-stu-id="b54ca-127">toocreate hello `.pem` file, execute:</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="b54ca-128">hello toocreate `.cer` certificati, eseguire:</span><span class="sxs-lookup"><span data-stu-id="b54ca-128">toocreate hello `.cer` certificate, execute:</span></span>

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

<span data-ttu-id="b54ca-129">Per altre informazioni sui certificati di Azure, vedere [Panoramica sui certificati per i servizi cloud di Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="b54ca-129">For more information about Azure certificates, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="b54ca-130">Per una descrizione completa di OpenSSL parametri, vedere la documentazione di hello in [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span><span class="sxs-lookup"><span data-stu-id="b54ca-130">For a complete description of OpenSSL parameters, see hello documentation at [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span></span>

<span data-ttu-id="b54ca-131">Dopo aver creato questi file, è necessario hello tooupload `.cer` file tooAzure tramite l'azione "Carica" hello della scheda "Impostazioni" hello di hello [portale di Azure classico][management-portal], ed è necessario annotare toomake in cui è stato salvato hello `.pem` file.</span><span class="sxs-lookup"><span data-stu-id="b54ca-131">After you have created these files, you need tooupload hello `.cer` file tooAzure via hello "Upload" action of hello "Settings" tab of hello [Azure classic portal][management-portal], and you need toomake note of where you saved hello `.pem` file.</span></span>

<span data-ttu-id="b54ca-132">Dopo aver ottenuto l'ID sottoscrizione, un certificato creato e caricato hello `.cer` tooAzure file, è possibile connettere l'endpoint di gestione di Azure di toohello passando l'id sottoscrizione hello e hello percorso toohello `.pem` file troppo**ServiceManagementService**:</span><span class="sxs-lookup"><span data-stu-id="b54ca-132">After you have obtained your subscription ID, created a certificate, and uploaded hello `.cer` file tooAzure, you can connect toohello Azure management endpoint by passing hello subscription id and hello path toohello `.pem` file too**ServiceManagementService**:</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="b54ca-133">Nell'esempio sopra riportato, hello `sms` è un **ServiceManagementService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="b54ca-133">In hello preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="b54ca-134">Hello **ServiceManagementService** classe è hello classe primaria utilizzata toomanage servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="b54ca-134">hello **ServiceManagementService** class is hello primary class used toomanage Azure services.</span></span>

### <a name="management-certificates-on-windows-makecert"></a><span data-ttu-id="b54ca-135">Certificati di gestione in Windows (MakeCert)</span><span class="sxs-lookup"><span data-stu-id="b54ca-135">Management certificates on Windows (MakeCert)</span></span>
<span data-ttu-id="b54ca-136">È possibile creare nel computer un certificato di gestione autofirmato usando `makecert.exe`.</span><span class="sxs-lookup"><span data-stu-id="b54ca-136">You can create a self-signed management certificate on your machine using `makecert.exe`.</span></span>  <span data-ttu-id="b54ca-137">Aprire un **prompt dei comandi di Visual Studio** come un **amministratore** e utilizzare hello comando seguente, sostituendo *AzureCertificate* con nome certificato hello desiderato toouse.</span><span class="sxs-lookup"><span data-stu-id="b54ca-137">Open a **Visual Studio command prompt** as an **administrator** and use hello following command, replacing *AzureCertificate* with hello certificate name you would like toouse.</span></span>

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

<span data-ttu-id="b54ca-138">comando Hello crea hello `.cer` file e lo installa nell'hello **personale** archivio certificati.</span><span class="sxs-lookup"><span data-stu-id="b54ca-138">hello command creates hello `.cer` file, and installs it in hello **Personal** certificate store.</span></span> <span data-ttu-id="b54ca-139">Per altre informazioni, vedere [Panoramica sui certificati per i servizi cloud di Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="b54ca-139">For more information, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span>

<span data-ttu-id="b54ca-140">Dopo aver creato il certificato di hello, è necessario hello tooupload `.cer` file tooAzure tramite l'azione "Carica" hello della scheda "Impostazioni" hello di hello [portale di Azure classico][management-portal].</span><span class="sxs-lookup"><span data-stu-id="b54ca-140">After you have created hello certificate, you need tooupload hello `.cer` file tooAzure via hello "Upload" action of hello "Settings" tab of hello [Azure classic portal][management-portal].</span></span>

<span data-ttu-id="b54ca-141">Dopo aver ottenuto l'ID sottoscrizione, un certificato creato e caricato hello `.cer` tooAzure file, è possibile connettere endpoint di gestione di Azure toohello passando il idsottoscrizionehelloeilpercorsodihellodelcertificatohello**Personale** archivio certificati troppo**ServiceManagementService** (nuovamente, sostituire *AzureCertificate* con nome hello del certificato):</span><span class="sxs-lookup"><span data-stu-id="b54ca-141">After you have obtained your subscription ID, created a certificate, and uploaded hello `.cer` file tooAzure, you can connect toohello Azure management endpoint by passing hello subscription id and hello location of hello certificate in your **Personal** certificate store too**ServiceManagementService** (again, replace *AzureCertificate* with hello name of your certificate):</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="b54ca-142">Nell'esempio sopra riportato, hello `sms` è un **ServiceManagementService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="b54ca-142">In hello preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="b54ca-143">Hello **ServiceManagementService** classe è hello classe primaria utilizzata toomanage servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="b54ca-143">hello **ServiceManagementService** class is hello primary class used toomanage Azure services.</span></span>

## <span data-ttu-id="b54ca-144"><a name="ListAvailableLocations"></a>Procedura: Creare un elenco delle località disponibili</span><span class="sxs-lookup"><span data-stu-id="b54ca-144"><a name="ListAvailableLocations"> </a>How to: List available locations</span></span>
<span data-ttu-id="b54ca-145">percorsi di hello toolist disponibili per l'hosting dei servizi, utilizzare hello **elenco\_percorsi** metodo:</span><span class="sxs-lookup"><span data-stu-id="b54ca-145">toolist hello locations that are available for hosting services, use hello **list\_locations** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

<span data-ttu-id="b54ca-146">Quando si crea un servizio cloud o un servizio di archiviazione è necessario tooprovide un percorso valido.</span><span class="sxs-lookup"><span data-stu-id="b54ca-146">When you create a cloud service or storage service you need tooprovide a valid location.</span></span> <span data-ttu-id="b54ca-147">Hello **elenco\_percorsi** metodo restituisce sempre un elenco aggiornato dei percorsi di hello attualmente disponibile.</span><span class="sxs-lookup"><span data-stu-id="b54ca-147">hello **list\_locations** method always returns an up-to-date list of hello currently available locations.</span></span> <span data-ttu-id="b54ca-148">In questo modo, le posizioni disponibili hello sono:</span><span class="sxs-lookup"><span data-stu-id="b54ca-148">As of this writing, hello available locations are:</span></span>

* <span data-ttu-id="b54ca-149">Europa occidentale</span><span class="sxs-lookup"><span data-stu-id="b54ca-149">West Europe</span></span>
* <span data-ttu-id="b54ca-150">Europa settentrionale</span><span class="sxs-lookup"><span data-stu-id="b54ca-150">North Europe</span></span>
* <span data-ttu-id="b54ca-151">Asia sudorientale</span><span class="sxs-lookup"><span data-stu-id="b54ca-151">Southeast Asia</span></span>
* <span data-ttu-id="b54ca-152">Asia orientale</span><span class="sxs-lookup"><span data-stu-id="b54ca-152">East Asia</span></span>
* <span data-ttu-id="b54ca-153">Stati Uniti centrali</span><span class="sxs-lookup"><span data-stu-id="b54ca-153">Central US</span></span>
* <span data-ttu-id="b54ca-154">Stati Uniti centro-settentrionali</span><span class="sxs-lookup"><span data-stu-id="b54ca-154">North Central US</span></span>
* <span data-ttu-id="b54ca-155">Stati Uniti centro-meridionali</span><span class="sxs-lookup"><span data-stu-id="b54ca-155">South Central US</span></span>
* <span data-ttu-id="b54ca-156">Stati Uniti occidentali</span><span class="sxs-lookup"><span data-stu-id="b54ca-156">West US</span></span>
* <span data-ttu-id="b54ca-157">Stati Uniti orientali</span><span class="sxs-lookup"><span data-stu-id="b54ca-157">East US</span></span>
* <span data-ttu-id="b54ca-158">Giappone orientale</span><span class="sxs-lookup"><span data-stu-id="b54ca-158">Japan East</span></span>
* <span data-ttu-id="b54ca-159">Giappone occidentale</span><span class="sxs-lookup"><span data-stu-id="b54ca-159">Japan West</span></span>
* <span data-ttu-id="b54ca-160">Brasile meridionale</span><span class="sxs-lookup"><span data-stu-id="b54ca-160">Brazil South</span></span>
* <span data-ttu-id="b54ca-161">Australia orientale</span><span class="sxs-lookup"><span data-stu-id="b54ca-161">Australia East</span></span>
* <span data-ttu-id="b54ca-162">Australia sudorientale</span><span class="sxs-lookup"><span data-stu-id="b54ca-162">Australia Southeast</span></span>

## <span data-ttu-id="b54ca-163"><a name="CreateCloudService"></a>Procedura: Creare un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="b54ca-163"><a name="CreateCloudService"> </a>How to: Create a cloud service</span></span>
<span data-ttu-id="b54ca-164">Quando si crea un'applicazione ed eseguirla in Azure, il codice hello e la configurazione vengono chiamati di Azure [servizio cloud] [ cloud service] (noto come un *servizio ospitato* in precedenza Versioni di Azure).</span><span class="sxs-lookup"><span data-stu-id="b54ca-164">When you create an application and run it in Azure, hello code and configuration together are called an Azure [cloud service][cloud service] (known as a *hosted service* in earlier Azure releases).</span></span> <span data-ttu-id="b54ca-165">Hello **creare\_ospitato\_servizio** metodo consente toocreate un nuovo servizio ospitato, fornendo un nome di servizio ospitato (che deve essere univoco in Azure), un'etichetta (toobase64 codificato automaticamente), un descrizione e un percorso.</span><span class="sxs-lookup"><span data-stu-id="b54ca-165">hello **create\_hosted\_service** method allows you toocreate a new hosted service by providing a hosted service name (which must be unique in Azure), a label (automatically encoded toobase64), a description, and a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

<span data-ttu-id="b54ca-166">È possibile elencare tutti i servizi ospitato hello per la sottoscrizione con hello **elenco\_ospitato\_servizi** metodo:</span><span class="sxs-lookup"><span data-stu-id="b54ca-166">You can list all hello hosted services for your subscription with hello **list\_hosted\_services** method:</span></span>

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

<span data-ttu-id="b54ca-167">Se si desiderano tooget informazioni relative a un servizio ospitato particolare, è possibile farlo passando hello ospitato servizio nome toohello **ottenere\_ospitato\_servizio\_proprietà** metodo:</span><span class="sxs-lookup"><span data-stu-id="b54ca-167">If you want tooget information about a particular hosted service, you can do so by passing hello hosted service name toohello **get\_hosted\_service\_properties** method:</span></span>

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

<span data-ttu-id="b54ca-168">Dopo aver creato un servizio cloud, è possibile distribuire il servizio toohello codice con hello **creare\_distribuzione** metodo.</span><span class="sxs-lookup"><span data-stu-id="b54ca-168">After you have created a cloud service, you can deploy your code toohello service with hello **create\_deployment** method.</span></span>

## <span data-ttu-id="b54ca-169"><a name="DeleteCloudService"></a>Procedura: Eliminare un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="b54ca-169"><a name="DeleteCloudService"> </a>How to: Delete a cloud service</span></span>
<span data-ttu-id="b54ca-170">È possibile eliminare un servizio cloud passando hello servizio nome toohello **eliminare\_ospitato\_servizio** metodo:</span><span class="sxs-lookup"><span data-stu-id="b54ca-170">You can delete a cloud service by passing hello service name toohello **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service('myhostedservice')

<span data-ttu-id="b54ca-171">Prima di poter eliminare un servizio, è necessario eliminare innanzitutto tutte le distribuzioni per il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="b54ca-171">Before you can delete a service, all deployments for hello service must first be deleted.</span></span> <span data-ttu-id="b54ca-172">Per informazioni dettagliate, vedere [Procedura: Eliminare una distribuzione](#DeleteDeployment) .</span><span class="sxs-lookup"><span data-stu-id="b54ca-172">(See [How to: Delete a deployment](#DeleteDeployment) for details.)</span></span>

## <span data-ttu-id="b54ca-173"><a name="DeleteDeployment"></a>Procedura: Eliminare una distribuzione</span><span class="sxs-lookup"><span data-stu-id="b54ca-173"><a name="DeleteDeployment"> </a>How to: Delete a deployment</span></span>
<span data-ttu-id="b54ca-174">toodelete una distribuzione, utilizzare hello **eliminare\_distribuzione** metodo.</span><span class="sxs-lookup"><span data-stu-id="b54ca-174">toodelete a deployment, use hello **delete\_deployment** method.</span></span> <span data-ttu-id="b54ca-175">Hello esempio seguente viene illustrato come toodelete una distribuzione denominata `v1`.</span><span class="sxs-lookup"><span data-stu-id="b54ca-175">hello following example shows how toodelete a deployment named `v1`.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <span data-ttu-id="b54ca-176"><a name="CreateStorageService"> </a>Procedura: Creare un servizio di archiviazione</span><span class="sxs-lookup"><span data-stu-id="b54ca-176"><a name="CreateStorageService"> </a>How to: Create a storage service</span></span>
<span data-ttu-id="b54ca-177">Oggetto [servizio di archiviazione](../storage/common/storage-create-storage-account.md) fornisce l'accesso tooAzure [BLOB](../storage/blobs/storage-python-how-to-use-blob-storage.md), [tabelle](../cosmos-db/table-storage-how-to-use-python.md), e [code](../storage/queues/storage-python-how-to-use-queue-storage.md).</span><span class="sxs-lookup"><span data-stu-id="b54ca-177">A [storage service](../storage/common/storage-create-storage-account.md) gives you access tooAzure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [Tables](../cosmos-db/table-storage-how-to-use-python.md), and [Queues](../storage/queues/storage-python-how-to-use-queue-storage.md).</span></span> <span data-ttu-id="b54ca-178">toocreate un servizio di archiviazione, è necessario un nome per il servizio di hello (compreso tra 3 e 24 caratteri minuscoli e univoco all'interno di Azure), una descrizione, un'etichetta (i caratteri too100, toobase64 automaticamente con codifica) e un percorso.</span><span class="sxs-lookup"><span data-stu-id="b54ca-178">toocreate a storage service, you need a name for hello service (between 3 and 24 lowercase characters and unique within Azure), a description, a label (up too100 characters, automatically encoded toobase64), and a location.</span></span> <span data-ttu-id="b54ca-179">Hello di esempio seguente viene illustrato come toocreate uno spazio di archiviazione del servizio, specificando un percorso.</span><span class="sxs-lookup"><span data-stu-id="b54ca-179">hello following example shows how toocreate a storage service by specifying a location.</span></span>

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

<span data-ttu-id="b54ca-180">Si noti in hello sopra riportato lo stato di hello hello **creare\_archiviazione\_account** operazione può essere recuperata passando hello risultato **creare\_archiviazione \_account** toohello **ottenere\_operazione\_stato** metodo.</span><span class="sxs-lookup"><span data-stu-id="b54ca-180">Note in hello preceding example that hello status of hello **create\_storage\_account** operation can be retrieved by passing hello result returned by **create\_storage\_account** toohello **get\_operation\_status** method.</span></span>  

<span data-ttu-id="b54ca-181">È possibile elencare gli account di archiviazione e le relative proprietà con hello **elenco\_archiviazione\_account** metodo:</span><span class="sxs-lookup"><span data-stu-id="b54ca-181">You can list your storage accounts and their properties with hello **list\_storage\_accounts** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <span data-ttu-id="b54ca-182"><a name="DeleteStorageService"></a>Procedura: Eliminare un servizio di archiviazione</span><span class="sxs-lookup"><span data-stu-id="b54ca-182"><a name="DeleteStorageService"> </a>How to: Delete a storage service</span></span>
<span data-ttu-id="b54ca-183">È possibile eliminare un servizio di archiviazione passando hello archiviazione servizio nome toohello **eliminare\_archiviazione\_account** metodo.</span><span class="sxs-lookup"><span data-stu-id="b54ca-183">You can delete a storage service by passing hello storage service name toohello **delete\_storage\_account** method.</span></span> <span data-ttu-id="b54ca-184">Se si elimina un servizio di archiviazione, tutti i dati archiviati nel servizio hello (BLOB, tabelle e code).</span><span class="sxs-lookup"><span data-stu-id="b54ca-184">Deleting a storage service deletes all data stored in hello service (blobs, tables, and queues).</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <span data-ttu-id="b54ca-185"><a name="ListOperatingSystems"></a>Procedura: Elencare i sistemi operativi disponibili</span><span class="sxs-lookup"><span data-stu-id="b54ca-185"><a name="ListOperatingSystems"> </a>How to: List available operating systems</span></span>
<span data-ttu-id="b54ca-186">sistemi operativi toolist hello disponibili per l'hosting dei servizi, utilizzare hello **elenco\_operativo\_sistemi** metodo:</span><span class="sxs-lookup"><span data-stu-id="b54ca-186">toolist hello operating systems that are available for hosting services, use hello **list\_operating\_systems** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

<span data-ttu-id="b54ca-187">In alternativa, è possibile utilizzare hello **elenco\_operativo\_sistema\_famiglie** metodo, che raggruppa i sistemi operativi hello dalla famiglia di:</span><span class="sxs-lookup"><span data-stu-id="b54ca-187">Alternatively, you can use hello **list\_operating\_system\_families** method, which groups hello operating systems by family:</span></span>

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <span data-ttu-id="b54ca-188"><a name="CreateVMImage"></a>Procedura: Creare un'immagine del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="b54ca-188"><a name="CreateVMImage"> </a>How to: Create an operating system image</span></span>
<span data-ttu-id="b54ca-189">un archivio di immagini del sistema operativo immagine toohello, tooadd utilizzare hello **aggiungere\_os\_immagine** metodo:</span><span class="sxs-lookup"><span data-stu-id="b54ca-189">tooadd an operating system image toohello image repository, use hello **add\_os\_image** method:</span></span>

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

<span data-ttu-id="b54ca-190">immagini del sistema operativo hello toolist disponibili, utilizzare hello **elenco\_os\_immagini** metodo.</span><span class="sxs-lookup"><span data-stu-id="b54ca-190">toolist hello operating system images that are available, use hello **list\_os\_images** method.</span></span> <span data-ttu-id="b54ca-191">Sono incluse tutte le immagini di piattaforma e utente:</span><span class="sxs-lookup"><span data-stu-id="b54ca-191">It includes all platform images and user images:</span></span>

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

## <span data-ttu-id="b54ca-192"><a name="DeleteVMImage"></a>Procedura: Eliminare un'immagine del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="b54ca-192"><a name="DeleteVMImage"> </a>How to: Delete an operating system image</span></span>
<span data-ttu-id="b54ca-193">toodelete un'immagine utente, utilizzare hello **eliminare\_os\_immagine** metodo:</span><span class="sxs-lookup"><span data-stu-id="b54ca-193">toodelete a user image, use hello **delete\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <span data-ttu-id="b54ca-194"><a name="CreateVM"> </a>Procedura: Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b54ca-194"><a name="CreateVM"> </a>How to: Create a virtual machine</span></span>
<span data-ttu-id="b54ca-195">toocreate una macchina virtuale, è innanzitutto necessario toocreate un [servizio cloud](#CreateCloudService).</span><span class="sxs-lookup"><span data-stu-id="b54ca-195">toocreate a virtual machine, you first need toocreate a [cloud service](#CreateCloudService).</span></span>  <span data-ttu-id="b54ca-196">Creare quindi distribuzione della macchina virtuale hello utilizzando hello **creare\_virtuale\_macchina\_distribuzione** metodo:</span><span class="sxs-lookup"><span data-stu-id="b54ca-196">Then create hello virtual machine deployment using hello **create\_virtual\_machine\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where hello VM disk
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

## <span data-ttu-id="b54ca-197"><a name="DeleteVM"></a>Procedura: Eliminare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b54ca-197"><a name="DeleteVM"> </a>How to: Delete a virtual machine</span></span>
<span data-ttu-id="b54ca-198">toodelete una macchina virtuale, prima di tutto eliminare hello distribuzione mediante hello **eliminare\_distribuzione** metodo:</span><span class="sxs-lookup"><span data-stu-id="b54ca-198">toodelete a virtual machine, you first delete hello deployment using hello **delete\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

<span data-ttu-id="b54ca-199">è quindi possibile eliminare il servizio di cloud Hello utilizzando hello **eliminare\_ospitato\_servizio** metodo:</span><span class="sxs-lookup"><span data-stu-id="b54ca-199">hello cloud service can then be deleted using hello **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a><span data-ttu-id="b54ca-200">Procedura: Creare una macchina virtuale da un'immagine di macchina virtuale acquisita</span><span class="sxs-lookup"><span data-stu-id="b54ca-200">How To: Create a Virtual Machine from a Captured Virtual Machine Image</span></span>
<span data-ttu-id="b54ca-201">toocapture un'immagine di macchina virtuale, chiamare prima hello **acquisire\_vm\_immagine** metodo:</span><span class="sxs-lookup"><span data-stu-id="b54ca-201">toocapture a VM image, you first call hello **capture\_vm\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace hello below three parameters with actual values
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

<span data-ttu-id="b54ca-202">Successivamente, toomake certi che è stato acquisizione immagine hello, utilizzare hello **elenco\_vm\_immagini** api e assicurarsi che l'immagine viene visualizzata nei risultati di hello:</span><span class="sxs-lookup"><span data-stu-id="b54ca-202">Next, toomake sure that you have successfully captured hello image, use hello **list\_vm\_images** api, and make sure your image is displayed in hello results:</span></span>

    images = sms.list_vm_images()

<span data-ttu-id="b54ca-203">toofinally creare una macchina virtuale hello utilizzando l'immagine acquisita hello, utilizzare hello **creare\_virtuale\_macchina\_distribuzione** come prima, ma questa volta passare vm_image_name hello invece</span><span class="sxs-lookup"><span data-stu-id="b54ca-203">toofinally create hello virtual machine using hello captured image, use hello **create\_virtual\_machine\_deployment** method as before, but this time pass in hello vm_image_name instead</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
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

<span data-ttu-id="b54ca-204">altre informazioni sulle toolearn toocapture una macchina virtuale Linux, vedere [come tooCapture una macchina virtuale di Linux.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="b54ca-204">toolearn more about how toocapture a Linux Virtual Machine, see [How tooCapture a Linux Virtual Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="b54ca-205">altre informazioni sulle toolearn toocapture una macchina virtuale di Windows, vedere [come tooCapture una macchina virtuale di Windows.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="b54ca-205">toolearn more about how toocapture a Windows Virtual Machine, see [How tooCapture a Windows Virtual Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="b54ca-206"><a name="What's Next"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b54ca-206"><a name="What's Next"> </a>Next Steps</span></span>
<span data-ttu-id="b54ca-207">Dopo aver appreso hello passaggi di base di gestione dei servizi, è possibile accedere hello [documentazione di riferimento API completa per hello Azure SDK Python](http://azure-sdk-for-python.readthedocs.org/) ed eseguire complesso è attività facilmente toomanage applicazione python.</span><span class="sxs-lookup"><span data-stu-id="b54ca-207">Now that you've learned hello basics of service management, you can access hello [Complete API reference documentation for hello Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) and perform complex tasks easily toomanage your python application.</span></span>

<span data-ttu-id="b54ca-208">Per ulteriori informazioni, vedere hello [Centro per sviluppatori Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="b54ca-208">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect tooservice management]: #Connect
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
