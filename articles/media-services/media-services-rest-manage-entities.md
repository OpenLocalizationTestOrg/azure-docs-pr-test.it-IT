---
title: "Gestione di entità di Servizi multimediali con REST | Documentazione Microsoft"
description: "Informazioni su come gestire entità di Servizi multimediali con l'API REST."
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
ms.openlocfilehash: a336907b605da962f835b8057ac6071f480cd85e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="managing-media-services-entities-with-rest"></a><span data-ttu-id="5e6a5-103">Gestione di entità di Servizi multimediali con REST</span><span class="sxs-lookup"><span data-stu-id="5e6a5-103">Managing Media Services entities with REST</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5e6a5-104">REST</span><span class="sxs-lookup"><span data-stu-id="5e6a5-104">REST</span></span>](media-services-rest-manage-entities.md)
> * [<span data-ttu-id="5e6a5-105">.NET</span><span class="sxs-lookup"><span data-stu-id="5e6a5-105">.NET</span></span>](media-services-dotnet-manage-entities.md)
> 
> 

<span data-ttu-id="5e6a5-106">Servizi multimediali di Microsoft Azure è un servizio REST basato su OData versione 3.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-106">Microsoft Azure Media Services is a REST-based service built on OData v3.</span></span> <span data-ttu-id="5e6a5-107">È possibile aggiungere, interrogare, aggiornare ed eliminare entità come in qualsiasi altro servizio OData.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-107">You can add, query, update, and delete entities in much the same way as you can on any other OData service.</span></span> <span data-ttu-id="5e6a5-108">Verranno chiamate le eccezioni, quando necessario.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-108">Exceptions will be called out when applicable.</span></span> <span data-ttu-id="5e6a5-109">Per altre informazioni su OData, vedere la pagina relativa alla [documentazione del protocollo OData](http://www.odata.org/documentation/).</span><span class="sxs-lookup"><span data-stu-id="5e6a5-109">For more information on OData, see [Open Data Protocol documentation](http://www.odata.org/documentation/).</span></span>

<span data-ttu-id="5e6a5-110">Questo argomento illustra come gestire le entità di Servizi multimediali di Azure con REST.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-110">This topic shows you how to manage Azure Media Services entities with REST.</span></span>

>[!NOTE]
> <span data-ttu-id="5e6a5-111">A partire dal 1° aprile 2017, tutti i record di processo presenti nell'account e più vecchi di 90 giorni verranno eliminati automaticamente, insieme ai record attività associati, anche se il numero totale di record è inferiore alla quota massima.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-111">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if the total number of records is below the maximum quota.</span></span> <span data-ttu-id="5e6a5-112">Ad esempio, il 1° aprile 2017 qualsiasi record di processo nell'account precedente il 31 dicembre 2016 verrà automaticamente eliminato.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-112">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="5e6a5-113">Se è necessario archiviare le informazioni sul processo o sull'attività, è possibile usare il codice descritto in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-113">If you need to archive the job/task information, you can use the code described in this topic.</span></span>

## <a name="considerations"></a><span data-ttu-id="5e6a5-114">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="5e6a5-114">Considerations</span></span>  

<span data-ttu-id="5e6a5-115">Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-115">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="5e6a5-116">Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="5e6a5-116">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="5e6a5-117">Connettersi a Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="5e6a5-117">Connect to Media Services</span></span>

<span data-ttu-id="5e6a5-118">Per informazioni su come connettersi all'API AMS, vedere [Accedere all'API di Servizi multimediali di Azure con l'autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="5e6a5-118">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="5e6a5-119">Dopo avere stabilito la connessione a https://media.windows.net, si riceverà un reindirizzamento 301 che indica un altro URI di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-119">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="5e6a5-120">Le chiamate successive dovranno essere effettuate al nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-120">You must make subsequent calls to the new URI.</span></span>

## <a name="adding-entities"></a><span data-ttu-id="5e6a5-121">Aggiunta di entità</span><span class="sxs-lookup"><span data-stu-id="5e6a5-121">Adding entities</span></span>
<span data-ttu-id="5e6a5-122">Ogni entità in Servizi multimediali viene aggiunta a un set di entità, ad esempio asset, mediante una richiesta HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-122">Every entity in Media Services is added to an entity set, such as Assets, through a POST HTTP request.</span></span>

<span data-ttu-id="5e6a5-123">Il seguente esempio mostra come creare un'entità AccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-123">The following example shows how to create an AccessPolicy.</span></span>

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

## <a name="querying-entities"></a><span data-ttu-id="5e6a5-124">Query di entità</span><span class="sxs-lookup"><span data-stu-id="5e6a5-124">Querying entities</span></span>
<span data-ttu-id="5e6a5-125">L'interrogazione e la visualizzazione delle entità è un'operazione semplice che prevede solo una richiesta HTTP GET e operazioni OData facoltative.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-125">Querying and listing entities is straightforward and only involves a GET HTTP request and optional OData operations.</span></span>
<span data-ttu-id="5e6a5-126">Il seguente esempio recupera un elenco di tutte le entità MediaProcessor.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-126">The following example retrieves a list of all MediaProcessor entities.</span></span>

    GET https://media.windows.net/API/MediaProcessors HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="5e6a5-127">È inoltre possibile recuperare un'entità specifica o tutti gli insiemi di entità associati a un'entità specifica, come nei seguenti esempi:</span><span class="sxs-lookup"><span data-stu-id="5e6a5-127">You can also retrieve a specific entity or all entity sets associated with a specific entity, such as in the following examples:</span></span>

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

<span data-ttu-id="5e6a5-128">Il seguente esempio restituisce solo la proprietà State di tutti i processi.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-128">The following example returns only the State property of all Jobs.</span></span>

    GET https://media.windows.net/API/Jobs?$select=State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="5e6a5-129">L'esempio seguente restituisce tutti gli oggetti JobTemplates con nome "SampleTemplate".</span><span class="sxs-lookup"><span data-stu-id="5e6a5-129">The following example returns all JobTemplates with the name "SampleTemplate."</span></span>

    GET https://media.windows.net/API/JobTemplates?$filter=startswith(Name,%20'SampleTemplate') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

> [!NOTE]
> <span data-ttu-id="5e6a5-130">L'operazione $expand non è supportata in Servizi multimediali così come i metodi LINQ non supportati descritti in Considerazioni su LINQ (WCF Data Services).</span><span class="sxs-lookup"><span data-stu-id="5e6a5-130">The $expand operation is not supported in Media Services as well as the unsupported LINQ methods described in LINQ Considerations (WCF Data Services).</span></span>
> 
> 

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="5e6a5-131">Enumerazione di grandi raccolte di entità</span><span class="sxs-lookup"><span data-stu-id="5e6a5-131">Enumerating through large collections of entities</span></span>
<span data-ttu-id="5e6a5-132">Quando si esegue una query di entità, è previsto un limite di 1000 entità restituite in una sola volta perché la versione 2 pubblica di REST limita i risultati della query a 1000 risultati.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-132">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results to 1000 results.</span></span> <span data-ttu-id="5e6a5-133">Usare gli elementi **skip** e **top** per enumerare raccolte di entità di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-133">Use **skip** and **top** to enumerate through the large collection of entities.</span></span> 

<span data-ttu-id="5e6a5-134">L'esempio seguente illustra come usare **skip** e **top** per ignorare i primi 2000 processi e ottenere i 1000 processi successivi.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-134">The following example shows how to use **skip** and **top** to skip the first 2000 jobs and get the next 1000 jobs.</span></span>  

    GET https://media.windows.net/api/Jobs()?$skip=2000&$top=1000 HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

## <a name="updating-entities"></a><span data-ttu-id="5e6a5-135">Aggiornamento di entità</span><span class="sxs-lookup"><span data-stu-id="5e6a5-135">Updating entities</span></span>
<span data-ttu-id="5e6a5-136">A seconda del tipo di entità e del relativo stato, è possibile aggiornare le proprietà corrispondenti mediante una richiesta HTTP PATCH, PUT o MERGE.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-136">Depending on the entity type and the state that it is in, you can update properties on that entity through a PATCH, PUT, or MERGE HTTP requests.</span></span> <span data-ttu-id="5e6a5-137">Per altre informazioni su queste operazioni, vedere [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="5e6a5-137">For more information about these operations, see [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="5e6a5-138">Il seguente esempio di codice illustra come aggiornare la proprietà Name in un'entità Asset.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-138">The following code example shows how to update the Name property on an Asset entity.</span></span>

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

## <a name="deleting-entities"></a><span data-ttu-id="5e6a5-139">Eliminazione di entità</span><span class="sxs-lookup"><span data-stu-id="5e6a5-139">Deleting entities</span></span>
<span data-ttu-id="5e6a5-140">Le entità possono essere eliminate in Servizi multimediali usando una richiesta HTTP DELETE.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-140">Entities can be deleted in Media Services by using a DELETE HTTP request.</span></span> <span data-ttu-id="5e6a5-141">A seconda dell'entità, l'ordine con cui vengono eliminate può essere importante.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-141">Depending on the entity, the order in which you delete entities may be important.</span></span> <span data-ttu-id="5e6a5-142">Entità come Asset ad esempio richiedono la revoca o eliminazione di tutti i localizzatori che fanno riferimento a tali entità prima dell'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-142">For example, entities such as Assets require that you revoke (or delete) all Locators that reference that particular Asset before deleting the Asset.</span></span>

<span data-ttu-id="5e6a5-143">Il seguente esempio illustra come eliminare un localizzatore usato per caricare un file nella risorsa di archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="5e6a5-143">The following example shows how to delete a Locator that was used to upload a file into blob storage.</span></span>

    DELETE https://media.windows.net/API/Locators('nb:lid:UUID:76dcc8e8-4230-463d-97b0-ce25c41b5c8d') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 0

## <a name="media-services-learning-paths"></a><span data-ttu-id="5e6a5-144">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="5e6a5-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5e6a5-145">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="5e6a5-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

