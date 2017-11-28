---
title: "entità di servizi multimediali aaaManaging con REST | Documenti Microsoft"
description: "Informazioni su come toomanage Media Services entità con l'API REST."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 95262a32-0f2a-4286-b9e2-1a1ca6399b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: bcdc5288e422ebc4e6f682a97da4e925ce237a79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-media-services-entities-with-rest"></a><span data-ttu-id="a2bf2-103">Gestione di entità di Servizi multimediali con REST</span><span class="sxs-lookup"><span data-stu-id="a2bf2-103">Managing Media Services entities with REST</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a2bf2-104">REST</span><span class="sxs-lookup"><span data-stu-id="a2bf2-104">REST</span></span>](media-services-rest-manage-entities.md)
> * [<span data-ttu-id="a2bf2-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a2bf2-105">.NET</span></span>](media-services-dotnet-manage-entities.md)
> 
> 

<span data-ttu-id="a2bf2-106">Servizi multimediali di Microsoft Azure è un servizio REST basato su OData versione 3.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-106">Microsoft Azure Media Services is a REST-based service built on OData v3.</span></span> <span data-ttu-id="a2bf2-107">È possibile aggiungere, query, aggiornamento ed eliminazione di entità nello hello stesso modo come in qualsiasi altro servizio OData.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-107">You can add, query, update, and delete entities in much hello same way as you can on any other OData service.</span></span> <span data-ttu-id="a2bf2-108">Verranno chiamate le eccezioni, quando necessario.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-108">Exceptions will be called out when applicable.</span></span> <span data-ttu-id="a2bf2-109">Per altre informazioni su OData, vedere la pagina relativa alla [documentazione del protocollo OData](http://www.odata.org/documentation/).</span><span class="sxs-lookup"><span data-stu-id="a2bf2-109">For more information on OData, see [Open Data Protocol documentation](http://www.odata.org/documentation/).</span></span>

<span data-ttu-id="a2bf2-110">In questo argomento illustra come entità di servizi multimediali di Azure toomanage con REST.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-110">This topic shows you how toomanage Azure Media Services entities with REST.</span></span>

>[!NOTE]
> <span data-ttu-id="a2bf2-111">A partire dal 1 aprile 2017, qualsiasi record di processo più vecchi di 90 giorni account vengono eliminate automaticamente, insieme ai relativi record di attività associato, anche se il numero di record hello sotto la quota massima di hello.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-111">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if hello total number of records is below hello maximum quota.</span></span> <span data-ttu-id="a2bf2-112">Ad esempio, il 1° aprile 2017 qualsiasi record di processo nell'account precedente il 31 dicembre 2016 verrà automaticamente eliminato.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-112">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="a2bf2-113">Se sono necessarie informazioni di processi/attività hello tooarchive, è possibile utilizzare codice hello descritte in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-113">If you need tooarchive hello job/task information, you can use hello code described in this topic.</span></span>

## <a name="considerations"></a><span data-ttu-id="a2bf2-114">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="a2bf2-114">Considerations</span></span>  

<span data-ttu-id="a2bf2-115">Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-115">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="a2bf2-116">Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a2bf2-116">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="a2bf2-117">Connessione dei servizi tooMedia</span><span class="sxs-lookup"><span data-stu-id="a2bf2-117">Connect tooMedia Services</span></span>

<span data-ttu-id="a2bf2-118">Per informazioni su come tooconnect toohello AMS API, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="a2bf2-118">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="a2bf2-119">Dopo avere stabilito la connessione toohttps://media.windows.net, si riceverà un reindirizzamento 301 specificando un altro URI di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-119">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="a2bf2-120">È necessario effettuare le chiamate successive toohello nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-120">You must make subsequent calls toohello new URI.</span></span>

## <a name="adding-entities"></a><span data-ttu-id="a2bf2-121">Aggiunta di entità</span><span class="sxs-lookup"><span data-stu-id="a2bf2-121">Adding entities</span></span>
<span data-ttu-id="a2bf2-122">Ogni entità in servizi multimediali viene aggiunto tooan set di entità, ad esempio asset, tramite una richiesta HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-122">Every entity in Media Services is added tooan entity set, such as Assets, through a POST HTTP request.</span></span>

<span data-ttu-id="a2bf2-123">Hello seguente esempio viene illustrato come toocreate un'entità AccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-123">hello following example shows how toocreate an AccessPolicy.</span></span>

    POST https://media.windows.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

## <a name="querying-entities"></a><span data-ttu-id="a2bf2-124">Query di entità</span><span class="sxs-lookup"><span data-stu-id="a2bf2-124">Querying entities</span></span>
<span data-ttu-id="a2bf2-125">L'interrogazione e la visualizzazione delle entità è un'operazione semplice che prevede solo una richiesta HTTP GET e operazioni OData facoltative.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-125">Querying and listing entities is straightforward and only involves a GET HTTP request and optional OData operations.</span></span>
<span data-ttu-id="a2bf2-126">Hello esempio seguente viene recuperato un elenco di tutte le entità MediaProcessor.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-126">hello following example retrieves a list of all MediaProcessor entities.</span></span>

    GET https://media.windows.net/API/MediaProcessors HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="a2bf2-127">È inoltre possibile recuperare un'entità specifica o tutti i set di entità associati a un'entità specifica, ad esempio in hello seguono esempi:</span><span class="sxs-lookup"><span data-stu-id="a2bf2-127">You can also retrieve a specific entity or all entity sets associated with a specific entity, such as in hello following examples:</span></span>

    GET https://media.windows.net/API/JobTemplates('nb:jtid:UUID:e81192f5-576f-b247-b781-70a790c20e7c') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336907474&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=OpuY0CeTylqFFcFaP4pKUVGesT4PGx4CP55zDf2zXnc%3d
    Host: media.windows.net

    GET https://media.windows.net/API/JobTemplates('nb:jtid:UUID:e81192f5-576f-b247-b781-70a790c20e7c')/TaskTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336907474&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=OpuY0CeTylqFFcFaP4pKUVGesT4PGx4CP55zDf2zXnc%3d
    Host: media.windows.net

<span data-ttu-id="a2bf2-128">Hello esempio seguente vengono restituite solo proprietà State hello di tutti i processi.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-128">hello following example returns only hello State property of all Jobs.</span></span>

    GET https://media.windows.net/API/Jobs?$select=State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="a2bf2-129">esempio Hello restituisce tutti gli oggetti JobTemplates con nome hello "SampleTemplate".</span><span class="sxs-lookup"><span data-stu-id="a2bf2-129">hello following example returns all JobTemplates with hello name "SampleTemplate."</span></span>

    GET https://media.windows.net/API/JobTemplates?$filter=startswith(Name,%20'SampleTemplate') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

> [!NOTE]
> <span data-ttu-id="a2bf2-130">operazione Hello $expand non è supportato in servizi multimediali, nonché hello metodi LINQ non supportati nelle considerazioni su LINQ (WCF Data Services).</span><span class="sxs-lookup"><span data-stu-id="a2bf2-130">hello $expand operation is not supported in Media Services as well as hello unsupported LINQ methods described in LINQ Considerations (WCF Data Services).</span></span>
> 
> 

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="a2bf2-131">Enumerazione di grandi raccolte di entità</span><span class="sxs-lookup"><span data-stu-id="a2bf2-131">Enumerating through large collections of entities</span></span>
<span data-ttu-id="a2bf2-132">Quando una query sulle entità, è previsto un limite di 1000 entità restituito in una sola volta perché v2 REST pubblici limita risultati too1000 risultati della query.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-132">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results too1000 results.</span></span> <span data-ttu-id="a2bf2-133">Utilizzare **ignorare** e **top** tooenumerate tramite una raccolta di entità di grandi dimensioni hello.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-133">Use **skip** and **top** tooenumerate through hello large collection of entities.</span></span> 

<span data-ttu-id="a2bf2-134">Hello seguente esempio viene illustrato come toouse **ignorare** e **top** tooskip hello innanzitutto 2000 processi e get hello accanto 1.000 processi.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-134">hello following example shows how toouse **skip** and **top** tooskip hello first 2000 jobs and get hello next 1000 jobs.</span></span>  

    GET https://media.windows.net/api/Jobs()?$skip=2000&$top=1000 HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

## <a name="updating-entities"></a><span data-ttu-id="a2bf2-135">Aggiornamento di entità</span><span class="sxs-lookup"><span data-stu-id="a2bf2-135">Updating entities</span></span>
<span data-ttu-id="a2bf2-136">A seconda di tipo di entità hello e dello stato di hello in esso contenuto, è possibile aggiornare le proprietà corrispondenti mediante una PATCH, richieste PUT o HTTP MERGE.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-136">Depending on hello entity type and hello state that it is in, you can update properties on that entity through a PATCH, PUT, or MERGE HTTP requests.</span></span> <span data-ttu-id="a2bf2-137">Per altre informazioni su queste operazioni, vedere [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2bf2-137">For more information about these operations, see [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="a2bf2-138">Hello esempio di codice seguente viene illustrato come tooupdate hello proprietà Name in un'entità Asset.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-138">hello following code example shows how tooupdate hello Name property on an Asset entity.</span></span>

    MERGE https://media.windows.net/API/Assets('nb:cid:UUID:80782407-3f87-4e60-a43e-5e4454232f60') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337083279&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=DMLQXWah4jO0icpfwyws5k%2b1aCDfz9KDGIGao20xk6g%3d
    Host: media.windows.net
    Content-Length: 21
    Expect: 100-continue

    {"Name" : "NewName" }

## <a name="deleting-entities"></a><span data-ttu-id="a2bf2-139">Eliminazione di entità</span><span class="sxs-lookup"><span data-stu-id="a2bf2-139">Deleting entities</span></span>
<span data-ttu-id="a2bf2-140">Le entità possono essere eliminate in Servizi multimediali usando una richiesta HTTP DELETE.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-140">Entities can be deleted in Media Services by using a DELETE HTTP request.</span></span> <span data-ttu-id="a2bf2-141">A seconda entità hello, ordine di hello in cui è stato eliminare entità può essere importante.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-141">Depending on hello entity, hello order in which you delete entities may be important.</span></span> <span data-ttu-id="a2bf2-142">Ad esempio, di richiedere che entità come asset revocare (o eliminare) tutti i localizzatori che fanno riferimento a tale Asset specifico prima di eliminare hello Asset.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-142">For example, entities such as Assets require that you revoke (or delete) all Locators that reference that particular Asset before deleting hello Asset.</span></span>

<span data-ttu-id="a2bf2-143">Hello seguente esempio viene illustrato come toodelete un localizzatore, che è stato utilizzato tooupload un file nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="a2bf2-143">hello following example shows how toodelete a Locator that was used tooupload a file into blob storage.</span></span>

    DELETE https://media.windows.net/API/Locators('nb:lid:UUID:76dcc8e8-4230-463d-97b0-ce25c41b5c8d') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 0

## <a name="media-services-learning-paths"></a><span data-ttu-id="a2bf2-144">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="a2bf2-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a2bf2-145">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="a2bf2-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

