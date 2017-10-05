---
title: Controllo delle versioni SDK di client e server in App per dispositivi mobili e Servizi mobili | Documentazione Microsoft
description: "Elenco degli SDK del client e compatibilità con versioni SDK del server per Servizi mobili e App per dispositivi mobili di Azure"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: f79e819b1547f81498ea213858faf3c75e374782
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a><span data-ttu-id="b449e-103">Controllo delle versioni client e server in App per dispositivi mobili e Servizi mobili</span><span class="sxs-lookup"><span data-stu-id="b449e-103">Client and server versioning in Mobile Apps and Mobile Services</span></span>
<span data-ttu-id="b449e-104">La versione più recente di Servizi mobili di Azure è la funzionalità **App per dispositivi mobili** del Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="b449e-104">The latest version of Azure Mobile Services is the **Mobile Apps** feature of Azure App Service.</span></span>

<span data-ttu-id="b449e-105">Gli SDK del client e del server di App per dispositivi mobili in origine si basano su quelle in Servizi mobili, ma *non* sono compatibili tra loro.</span><span class="sxs-lookup"><span data-stu-id="b449e-105">The Mobile Apps client and server SDKs are originally based on those in Mobile Services, but they are *not* compatible with each other.</span></span>
<span data-ttu-id="b449e-106">È infatti necessario usare un SDK del client di *App per dispositivi mobili* con un SDK del server di *App per dispositivi mobili* e lo stesso vale per *Servizi mobili*.</span><span class="sxs-lookup"><span data-stu-id="b449e-106">That is, you must use a *Mobile Apps* client SDK with a *Mobile Apps* server SDK and similarly for *Mobile Services*.</span></span> <span data-ttu-id="b449e-107">Questo contratto viene applicato tramite un valore di intestazione speciale utilizzato dagli SDK del client e del server, `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="b449e-107">This contract is enforced through a special header value used by the client and server SDKs, `ZUMO-API-VERSION`.</span></span>

<span data-ttu-id="b449e-108">Nota: ogni volta che in questo documento si fa riferimento a un back-end di *Servizi mobili* , esso non deve necessariamente essere ospitato su Servizi mobili.</span><span class="sxs-lookup"><span data-stu-id="b449e-108">Note: whenever this document refers to a *Mobile Services* backend, it does not necessarily need to be hosted on Mobile Services.</span></span> <span data-ttu-id="b449e-109">È ora possibile eseguire la migrazione di un servizio mobile per l'esecuzione nel servizio app senza apportare modifiche al codice, ma il servizio continuerà a usare le versioni SDK di *Servizi mobili*.</span><span class="sxs-lookup"><span data-stu-id="b449e-109">It is now possible to migrate a mobile service to run on App Service without any code changes, but the service would still be using *Mobile Services*  SDK versions.</span></span>

<span data-ttu-id="b449e-110">Per ulteriori informazioni sulla migrazione al servizio app senza apportare modifiche al codice, vedere l'articolo [Eseguire la migrazione di un servizio mobile al servizio app di Azure].</span><span class="sxs-lookup"><span data-stu-id="b449e-110">To learn more about migrating to App Service without any code changes, see the article [Migrate a Mobile Service to Azure App Service].</span></span>

## <a name="header-specification"></a><span data-ttu-id="b449e-111">Specifica di intestazione</span><span class="sxs-lookup"><span data-stu-id="b449e-111">Header specification</span></span>
<span data-ttu-id="b449e-112">La chiave `ZUMO-API-VERSION` può essere specificata nell'intestazione HTTP o nella stringa di query.</span><span class="sxs-lookup"><span data-stu-id="b449e-112">The key `ZUMO-API-VERSION` may be specified in either the HTTP header or the query string.</span></span> <span data-ttu-id="b449e-113">Il valore è una stringa di versione nel formato **x.y.z**.</span><span class="sxs-lookup"><span data-stu-id="b449e-113">The value is a version string in the form **x.y.z**.</span></span>

<span data-ttu-id="b449e-114">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b449e-114">For example:</span></span>

<span data-ttu-id="b449e-115">GET https://service.azurewebsites.net/tables/TodoItem</span><span class="sxs-lookup"><span data-stu-id="b449e-115">GET https://service.azurewebsites.net/tables/TodoItem</span></span>

<span data-ttu-id="b449e-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span><span class="sxs-lookup"><span data-stu-id="b449e-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span></span>

<span data-ttu-id="b449e-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span><span class="sxs-lookup"><span data-stu-id="b449e-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span></span>

## <a name="opting-out-of-version-checking"></a><span data-ttu-id="b449e-118">Esclusione del controllo della versione</span><span class="sxs-lookup"><span data-stu-id="b449e-118">Opting out of version checking</span></span>
<span data-ttu-id="b449e-119">È possibile rifiutare esplicitamente il controllo della versione impostando un valore **true** per l'impostazione dell'app **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="b449e-119">You can opt out of version checking by setting a value of **true** for the app setting **MS_SkipVersionCheck**.</span></span> <span data-ttu-id="b449e-120">Specificarlo nel file web.config o nella sezione Impostazioni applicazione del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b449e-120">Specify this either in your web.config or in the Application Settings section of the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="b449e-121">Esistono una serie di modifiche di comportamento tra Servizi mobili e App per dispositivi mobili, in particolare per quanto riguarda la sincronizzazione offline, l’autenticazione e le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="b449e-121">There are a number of behavior changes between Mobile Services and Mobile Apps, particularly in the areas of offline sync, authentication, and push notifications.</span></span> <span data-ttu-id="b449e-122">È consigliabile rifiutare esplicitamente solo il controllo della versione dopo aver completato un test per assicurarsi che queste modifiche del comportamento non interferiscano con le funzionalità dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b449e-122">You should only opt out of version checking after complete testing to ensure that these behavioral changes do not break your app's functionality.</span></span>
>
>

## <a name="summary-of-compatibility-for-all-versions"></a><span data-ttu-id="b449e-123">Riepilogo della compatibilità per tutte le versioni</span><span class="sxs-lookup"><span data-stu-id="b449e-123">Summary of compatibility for all versions</span></span>
<span data-ttu-id="b449e-124">Il grafico seguente illustra la compatibilità tra tutti i tipi di client e server.</span><span class="sxs-lookup"><span data-stu-id="b449e-124">The chart below shows the compatibility between all client and server types.</span></span> <span data-ttu-id="b449e-125">Un back-end viene classificato come **Servizi** mobili o **App** per dispositivi mobili in base all'SDK del server usato.</span><span class="sxs-lookup"><span data-stu-id="b449e-125">A backend is classified as either Mobile **Services** or Mobile **Apps** based on the server SDK that it uses.</span></span>

|  | <span data-ttu-id="b449e-126">**Servizi mobili** </span><span class="sxs-lookup"><span data-stu-id="b449e-126">**Mobile Services** Node.js or .NET</span></span> | <span data-ttu-id="b449e-127">**App per dispositivi mobili** </span><span class="sxs-lookup"><span data-stu-id="b449e-127">**Mobile Apps** Node.js or .NET</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b449e-128">[Client di Servizi mobili]</span><span class="sxs-lookup"><span data-stu-id="b449e-128">[Mobile Services clients]</span></span> |<span data-ttu-id="b449e-129">OK</span><span class="sxs-lookup"><span data-stu-id="b449e-129">Ok</span></span> |<span data-ttu-id="b449e-130">Errore\*</span><span class="sxs-lookup"><span data-stu-id="b449e-130">Error\*</span></span> |
| <span data-ttu-id="b449e-131">[Client di App per dispositivi mobili]</span><span class="sxs-lookup"><span data-stu-id="b449e-131">[Mobile Apps clients]</span></span> |<span data-ttu-id="b449e-132">Errore\*</span><span class="sxs-lookup"><span data-stu-id="b449e-132">Error\*</span></span> |<span data-ttu-id="b449e-133">OK</span><span class="sxs-lookup"><span data-stu-id="b449e-133">Ok</span></span> |

<span data-ttu-id="b449e-134">\*Può essere controllato specificando **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="b449e-134">\*This can be controlled by specifying **MS_SkipVersionCheck**.</span></span>

<!-- IMPORTANT!  The anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: the fwlink to this document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <span data-ttu-id="b449e-135"><a name="1.0.0"></a>Client e server di Servizi mobili</span><span class="sxs-lookup"><span data-stu-id="b449e-135"><a name="1.0.0"></a>Mobile Services client and server</span></span>
<span data-ttu-id="b449e-136">Gli SDK del client nella tabella seguente sono compatibili con **Servizi mobili**.</span><span class="sxs-lookup"><span data-stu-id="b449e-136">The client SDKs in the table below are compatible with **Mobile Services**.</span></span>

<span data-ttu-id="b449e-137">Nota: gli SDK del client di Servizi mobili *non* inviano un valore di intestazione per `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="b449e-137">Note: the Mobile Services client SDKs *do not* send a header value for `ZUMO-API-VERSION`.</span></span> <span data-ttu-id="b449e-138">Se il servizio riceve questo valore di intestazione o di stringa di query, verrà restituito un errore, a meno che non lo si abbia rifiutato in modo esplicito come descritto sopra.</span><span class="sxs-lookup"><span data-stu-id="b449e-138">If the service receives this header or query string value, an error will be returned, unless you have explicitly opted out as described above.</span></span>

### <span data-ttu-id="b449e-139"><a name="MobileServicesClients"></a> SDK del client di *Servizi* mobili</span><span class="sxs-lookup"><span data-stu-id="b449e-139"><a name="MobileServicesClients"></a> Mobile *Services* client SDKs</span></span>
| <span data-ttu-id="b449e-140">Piattaforma client</span><span class="sxs-lookup"><span data-stu-id="b449e-140">Client platform</span></span> | <span data-ttu-id="b449e-141">Versione</span><span class="sxs-lookup"><span data-stu-id="b449e-141">Version</span></span> | <span data-ttu-id="b449e-142">Valore dell'intestazione della versione</span><span class="sxs-lookup"><span data-stu-id="b449e-142">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b449e-143">Client gestito (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="b449e-143">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="b449e-144">1.3.2</span><span class="sxs-lookup"><span data-stu-id="b449e-144">1.3.2</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |<span data-ttu-id="b449e-145">n/d</span><span class="sxs-lookup"><span data-stu-id="b449e-145">n/a</span></span> |
| <span data-ttu-id="b449e-146">iOS</span><span class="sxs-lookup"><span data-stu-id="b449e-146">iOS</span></span> |[<span data-ttu-id="b449e-147">2.2.2</span><span class="sxs-lookup"><span data-stu-id="b449e-147">2.2.2</span></span>](http://aka.ms/gc6fex) |<span data-ttu-id="b449e-148">n/d</span><span class="sxs-lookup"><span data-stu-id="b449e-148">n/a</span></span> |
| <span data-ttu-id="b449e-149">Android</span><span class="sxs-lookup"><span data-stu-id="b449e-149">Android</span></span> |[<span data-ttu-id="b449e-150">2.0.3</span><span class="sxs-lookup"><span data-stu-id="b449e-150">2.0.3</span></span>](https://go.microsoft.com/fwLink/?LinkID=280126) |<span data-ttu-id="b449e-151">n/d</span><span class="sxs-lookup"><span data-stu-id="b449e-151">n/a</span></span> |
| <span data-ttu-id="b449e-152">HTML</span><span class="sxs-lookup"><span data-stu-id="b449e-152">HTML</span></span> |[<span data-ttu-id="b449e-153">1.2.7</span><span class="sxs-lookup"><span data-stu-id="b449e-153">1.2.7</span></span>](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |<span data-ttu-id="b449e-154">n/d</span><span class="sxs-lookup"><span data-stu-id="b449e-154">n/a</span></span> |

### <a name="mobile-services-server-sdks"></a><span data-ttu-id="b449e-155">SDK del server di *Servizi* mobili</span><span class="sxs-lookup"><span data-stu-id="b449e-155">Mobile *Services* server SDKs</span></span>
| <span data-ttu-id="b449e-156">Piattaforma server</span><span class="sxs-lookup"><span data-stu-id="b449e-156">Server platform</span></span> | <span data-ttu-id="b449e-157">Versione</span><span class="sxs-lookup"><span data-stu-id="b449e-157">Version</span></span> | <span data-ttu-id="b449e-158">Intestazione della versione accettata</span><span class="sxs-lookup"><span data-stu-id="b449e-158">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b449e-159">.NET</span><span class="sxs-lookup"><span data-stu-id="b449e-159">.NET</span></span> |[<span data-ttu-id="b449e-160">WindowsAzure.MobileServices.Backend.* Versione 1.0.x</span><span class="sxs-lookup"><span data-stu-id="b449e-160">WindowsAzure.MobileServices.Backend.* Version 1.0.x</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |<span data-ttu-id="b449e-161">* * Nessuna intestazione di versione * *</span><span class="sxs-lookup"><span data-stu-id="b449e-161">**No version header **</span></span> |
| <span data-ttu-id="b449e-162">Node.js</span><span class="sxs-lookup"><span data-stu-id="b449e-162">Node.js</span></span> |<span data-ttu-id="b449e-163">(Presto disponibile)</span><span class="sxs-lookup"><span data-stu-id="b449e-163">(coming soon)</span></span> |<span data-ttu-id="b449e-164">**Nessuna intestazione di versione**</span><span class="sxs-lookup"><span data-stu-id="b449e-164">**No version header**</span></span> |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a><span data-ttu-id="b449e-165">Comportamento dei back-end di Servizi mobili</span><span class="sxs-lookup"><span data-stu-id="b449e-165">Behavior of Mobile Services backends</span></span>
| <span data-ttu-id="b449e-166">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="b449e-166">ZUMO-API-VERSION</span></span> | <span data-ttu-id="b449e-167">Valore di MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="b449e-167">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="b449e-168">Response</span><span class="sxs-lookup"><span data-stu-id="b449e-168">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b449e-169">Non specificato</span><span class="sxs-lookup"><span data-stu-id="b449e-169">Not specified</span></span> |<span data-ttu-id="b449e-170">Qualsiasi</span><span class="sxs-lookup"><span data-stu-id="b449e-170">Any</span></span> |<span data-ttu-id="b449e-171">200 - OK</span><span class="sxs-lookup"><span data-stu-id="b449e-171">200 - OK</span></span> |
| <span data-ttu-id="b449e-172">Qualsiasi valore</span><span class="sxs-lookup"><span data-stu-id="b449e-172">Any value</span></span> |<span data-ttu-id="b449e-173">True</span><span class="sxs-lookup"><span data-stu-id="b449e-173">True</span></span> |<span data-ttu-id="b449e-174">200 - OK</span><span class="sxs-lookup"><span data-stu-id="b449e-174">200 - OK</span></span> |
| <span data-ttu-id="b449e-175">Qualsiasi valore</span><span class="sxs-lookup"><span data-stu-id="b449e-175">Any value</span></span> |<span data-ttu-id="b449e-176">False/Non specificato</span><span class="sxs-lookup"><span data-stu-id="b449e-176">False/Not Specified</span></span> |<span data-ttu-id="b449e-177">400 - Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="b449e-177">400 - Bad Request</span></span> |

## <span data-ttu-id="b449e-178"><a name="2.0.0"></a>Client e server di App per dispositivi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="b449e-178"><a name="2.0.0"></a>Azure Mobile Apps client and server</span></span>
### <span data-ttu-id="b449e-179"><a name="MobileAppsClients"></a> SDK del client di *App* per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="b449e-179"><a name="MobileAppsClients"></a> Mobile *Apps* client SDKs</span></span>
<span data-ttu-id="b449e-180">Il controllo della versione è stata introdotta a partire dalle seguenti versioni dell’SDK del client per **App per dispositivi mobili di Azure**:</span><span class="sxs-lookup"><span data-stu-id="b449e-180">Version checking was introduced starting with the following versions of the client SDK for **Azure Mobile Apps**:</span></span>

| <span data-ttu-id="b449e-181">Piattaforma client</span><span class="sxs-lookup"><span data-stu-id="b449e-181">Client platform</span></span> | <span data-ttu-id="b449e-182">Versione</span><span class="sxs-lookup"><span data-stu-id="b449e-182">Version</span></span> | <span data-ttu-id="b449e-183">Valore dell'intestazione della versione</span><span class="sxs-lookup"><span data-stu-id="b449e-183">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b449e-184">Client gestito (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="b449e-184">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="b449e-185">2.0.0</span><span class="sxs-lookup"><span data-stu-id="b449e-185">2.0.0</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |<span data-ttu-id="b449e-186">2.0.0</span><span class="sxs-lookup"><span data-stu-id="b449e-186">2.0.0</span></span> |
| <span data-ttu-id="b449e-187">iOS</span><span class="sxs-lookup"><span data-stu-id="b449e-187">iOS</span></span> |[<span data-ttu-id="b449e-188">3.0.0</span><span class="sxs-lookup"><span data-stu-id="b449e-188">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=529823) |<span data-ttu-id="b449e-189">2.0.0</span><span class="sxs-lookup"><span data-stu-id="b449e-189">2.0.0</span></span> |
| <span data-ttu-id="b449e-190">Android</span><span class="sxs-lookup"><span data-stu-id="b449e-190">Android</span></span> |[<span data-ttu-id="b449e-191">3.0.0</span><span class="sxs-lookup"><span data-stu-id="b449e-191">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |<span data-ttu-id="b449e-192">3.0.0</span><span class="sxs-lookup"><span data-stu-id="b449e-192">3.0.0</span></span> |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a><span data-ttu-id="b449e-193">SDK del server di *App* per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="b449e-193">Mobile *Apps* server SDKs</span></span>
<span data-ttu-id="b449e-194">Il controllo della versione è incluso nelle seguenti versioni dell’SDK del server:</span><span class="sxs-lookup"><span data-stu-id="b449e-194">Version checking is included in following server SDK versions:</span></span>

| <span data-ttu-id="b449e-195">Piattaforma server</span><span class="sxs-lookup"><span data-stu-id="b449e-195">Server platform</span></span> | <span data-ttu-id="b449e-196">SDK</span><span class="sxs-lookup"><span data-stu-id="b449e-196">SDK</span></span> | <span data-ttu-id="b449e-197">Intestazione della versione accettata</span><span class="sxs-lookup"><span data-stu-id="b449e-197">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b449e-198">.NET</span><span class="sxs-lookup"><span data-stu-id="b449e-198">.NET</span></span> |[<span data-ttu-id="b449e-199">Microsoft.Azure.Mobile.Server</span><span class="sxs-lookup"><span data-stu-id="b449e-199">Microsoft.Azure.Mobile.Server</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |<span data-ttu-id="b449e-200">2.0.0</span><span class="sxs-lookup"><span data-stu-id="b449e-200">2.0.0</span></span> |
| <span data-ttu-id="b449e-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="b449e-201">Node.js</span></span> |[<span data-ttu-id="b449e-202">azure-mobile-apps)</span><span class="sxs-lookup"><span data-stu-id="b449e-202">azure-mobile-apps)</span></span>](https://www.npmjs.com/package/azure-mobile-apps) |<span data-ttu-id="b449e-203">2.0.0</span><span class="sxs-lookup"><span data-stu-id="b449e-203">2.0.0</span></span> |

### <a name="behavior-of-mobile-apps-backends"></a><span data-ttu-id="b449e-204">Comportamento dei back-end di app per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="b449e-204">Behavior of Mobile Apps backends</span></span>
| <span data-ttu-id="b449e-205">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="b449e-205">ZUMO-API-VERSION</span></span> | <span data-ttu-id="b449e-206">Valore di MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="b449e-206">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="b449e-207">Response</span><span class="sxs-lookup"><span data-stu-id="b449e-207">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b449e-208">x.y.z o Null</span><span class="sxs-lookup"><span data-stu-id="b449e-208">x.y.z or Null</span></span> |<span data-ttu-id="b449e-209">True</span><span class="sxs-lookup"><span data-stu-id="b449e-209">True</span></span> |<span data-ttu-id="b449e-210">200 - OK</span><span class="sxs-lookup"><span data-stu-id="b449e-210">200 - OK</span></span> |
| <span data-ttu-id="b449e-211">Null</span><span class="sxs-lookup"><span data-stu-id="b449e-211">Null</span></span> |<span data-ttu-id="b449e-212">False/Non specificato</span><span class="sxs-lookup"><span data-stu-id="b449e-212">False/Not Specified</span></span> |<span data-ttu-id="b449e-213">400 - Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="b449e-213">400 - Bad Request</span></span> |
| <span data-ttu-id="b449e-214">1.x.y</span><span class="sxs-lookup"><span data-stu-id="b449e-214">1.x.y</span></span> |<span data-ttu-id="b449e-215">False/Non specificato</span><span class="sxs-lookup"><span data-stu-id="b449e-215">False/Not Specified</span></span> |<span data-ttu-id="b449e-216">400 - Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="b449e-216">400 - Bad Request</span></span> |
| <span data-ttu-id="b449e-217">2.0.0-2.x.y</span><span class="sxs-lookup"><span data-stu-id="b449e-217">2.0.0-2.x.y</span></span> |<span data-ttu-id="b449e-218">False/Non specificato</span><span class="sxs-lookup"><span data-stu-id="b449e-218">False/Not Specified</span></span> |<span data-ttu-id="b449e-219">200 - OK</span><span class="sxs-lookup"><span data-stu-id="b449e-219">200 - OK</span></span> |
| <span data-ttu-id="b449e-220">3.0.0-3.x.y</span><span class="sxs-lookup"><span data-stu-id="b449e-220">3.0.0-3.x.y</span></span> |<span data-ttu-id="b449e-221">False/Non specificato</span><span class="sxs-lookup"><span data-stu-id="b449e-221">False/Not Specified</span></span> |<span data-ttu-id="b449e-222">400 - Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="b449e-222">400 - Bad Request</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b449e-223">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b449e-223">Next Steps</span></span>
* <span data-ttu-id="b449e-224">[Eseguire la migrazione di un servizio mobile al servizio app di Azure]</span><span class="sxs-lookup"><span data-stu-id="b449e-224">[Migrate a Mobile Service to Azure App Service]</span></span>

<span data-ttu-id="b449e-225">[Client di Servizi mobili]: #MobileServicesClients</span><span class="sxs-lookup"><span data-stu-id="b449e-225">[Mobile Services clients]: #MobileServicesClients</span></span>
<span data-ttu-id="b449e-226">[Client di App per dispositivi mobili]: #MobileAppsClients</span><span class="sxs-lookup"><span data-stu-id="b449e-226">[Mobile Apps clients]: #MobileAppsClients</span></span>


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
<span data-ttu-id="b449e-227">[Eseguire la migrazione di un servizio mobile al servizio app di Azure]: app-service-mobile-migrating-from-mobile-services.md</span><span class="sxs-lookup"><span data-stu-id="b449e-227">[Migrate a Mobile Service to Azure App Service]: app-service-mobile-migrating-from-mobile-services.md</span></span>
