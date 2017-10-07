---
title: controllo delle versioni SDK aaaClient e server in App per dispositivi mobili e i servizi mobili | Documenti Microsoft
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
ms.openlocfilehash: 5874b7455ea407ca8c77fb1bd03d97d0767ebb47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a><span data-ttu-id="691b1-103">Controllo delle versioni client e server in App per dispositivi mobili e Servizi mobili</span><span class="sxs-lookup"><span data-stu-id="691b1-103">Client and server versioning in Mobile Apps and Mobile Services</span></span>
<span data-ttu-id="691b1-104">versione più recente di Hello di servizi mobili di Azure è hello **App per dispositivi mobili** funzionalità di servizio App di Azure.</span><span class="sxs-lookup"><span data-stu-id="691b1-104">hello latest version of Azure Mobile Services is hello **Mobile Apps** feature of Azure App Service.</span></span>

<span data-ttu-id="691b1-105">Hello client App per dispositivi mobili e server SDK originariamente sono basate su quelle di servizi mobili, ma sono *non* compatibili tra loro.</span><span class="sxs-lookup"><span data-stu-id="691b1-105">hello Mobile Apps client and server SDKs are originally based on those in Mobile Services, but they are *not* compatible with each other.</span></span>
<span data-ttu-id="691b1-106">È infatti necessario usare un SDK del client di *App per dispositivi mobili* con un SDK del server di *App per dispositivi mobili* e lo stesso vale per *Servizi mobili*.</span><span class="sxs-lookup"><span data-stu-id="691b1-106">That is, you must use a *Mobile Apps* client SDK with a *Mobile Apps* server SDK and similarly for *Mobile Services*.</span></span> <span data-ttu-id="691b1-107">Il presente contratto verrà applicato tramite un valore di intestazione speciale utilizzato dalle hello client e server SDK, `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="691b1-107">This contract is enforced through a special header value used by hello client and server SDKs, `ZUMO-API-VERSION`.</span></span>

<span data-ttu-id="691b1-108">Nota: ogni volta che questo documento si riferisce tooa *servizi mobili* back-end, non devono necessariamente toobe ospitati in servizi mobili.</span><span class="sxs-lookup"><span data-stu-id="691b1-108">Note: whenever this document refers tooa *Mobile Services* backend, it does not necessarily need toobe hosted on Mobile Services.</span></span> <span data-ttu-id="691b1-109">È ora possibile toomigrate toorun un servizio mobile nel servizio App senza alcuna modifica al codice, ma è comunque possibile utilizzare servizio hello *servizi mobili* versioni del SDK.</span><span class="sxs-lookup"><span data-stu-id="691b1-109">It is now possible toomigrate a mobile service toorun on App Service without any code changes, but hello service would still be using *Mobile Services*  SDK versions.</span></span>

<span data-ttu-id="691b1-110">toolearn altre informazioni sulla migrazione tooApp servizio senza alcuna modifica al codice, vedere l'articolo hello [tooAzure un servizio Mobile servizio App di eseguire la migrazione].</span><span class="sxs-lookup"><span data-stu-id="691b1-110">toolearn more about migrating tooApp Service without any code changes, see hello article [Migrate a Mobile Service tooAzure App Service].</span></span>

## <a name="header-specification"></a><span data-ttu-id="691b1-111">Specifica di intestazione</span><span class="sxs-lookup"><span data-stu-id="691b1-111">Header specification</span></span>
<span data-ttu-id="691b1-112">chiave Hello `ZUMO-API-VERSION` può essere specificato nell'intestazione HTTP hello o stringa di query hello.</span><span class="sxs-lookup"><span data-stu-id="691b1-112">hello key `ZUMO-API-VERSION` may be specified in either hello HTTP header or hello query string.</span></span> <span data-ttu-id="691b1-113">il valore di Hello è una stringa di versione in formato hello **x.y.z**.</span><span class="sxs-lookup"><span data-stu-id="691b1-113">hello value is a version string in hello form **x.y.z**.</span></span>

<span data-ttu-id="691b1-114">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="691b1-114">For example:</span></span>

<span data-ttu-id="691b1-115">GET https://service.azurewebsites.net/tables/TodoItem</span><span class="sxs-lookup"><span data-stu-id="691b1-115">GET https://service.azurewebsites.net/tables/TodoItem</span></span>

<span data-ttu-id="691b1-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span><span class="sxs-lookup"><span data-stu-id="691b1-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span></span>

<span data-ttu-id="691b1-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span><span class="sxs-lookup"><span data-stu-id="691b1-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span></span>

## <a name="opting-out-of-version-checking"></a><span data-ttu-id="691b1-118">Esclusione del controllo della versione</span><span class="sxs-lookup"><span data-stu-id="691b1-118">Opting out of version checking</span></span>
<span data-ttu-id="691b1-119">È possibile rifiutare esplicitamente la verifica della impostando un valore di versione **true** per l'impostazione di app hello **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="691b1-119">You can opt out of version checking by setting a value of **true** for hello app setting **MS_SkipVersionCheck**.</span></span> <span data-ttu-id="691b1-120">Specificare questo file Web. config o nella sezione impostazioni dell'applicazione del portale di Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="691b1-120">Specify this either in your web.config or in hello Application Settings section of hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="691b1-121">Esistono una serie di modifiche di comportamento tra servizi mobili e App per dispositivi mobili, in particolare nelle aree di hello di sincronizzazione non in linea, autenticazione e le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="691b1-121">There are a number of behavior changes between Mobile Services and Mobile Apps, particularly in hello areas of offline sync, authentication, and push notifications.</span></span> <span data-ttu-id="691b1-122">È solo necessario rifiutare esplicitamente versione controllo dopo tooensure test completo che queste modifiche del comportamento non interrompe l'esecuzione funzionalità dell'app.</span><span class="sxs-lookup"><span data-stu-id="691b1-122">You should only opt out of version checking after complete testing tooensure that these behavioral changes do not break your app's functionality.</span></span>
>
>

## <a name="summary-of-compatibility-for-all-versions"></a><span data-ttu-id="691b1-123">Riepilogo della compatibilità per tutte le versioni</span><span class="sxs-lookup"><span data-stu-id="691b1-123">Summary of compatibility for all versions</span></span>
<span data-ttu-id="691b1-124">Hello grafico mostra la compatibilità di hello tra tutti i tipi di client e server.</span><span class="sxs-lookup"><span data-stu-id="691b1-124">hello chart below shows hello compatibility between all client and server types.</span></span> <span data-ttu-id="691b1-125">Un back-end viene classificato come entrambi Mobile **servizi** o Mobile **app** basata su server hello SDK che utilizza.</span><span class="sxs-lookup"><span data-stu-id="691b1-125">A backend is classified as either Mobile **Services** or Mobile **Apps** based on hello server SDK that it uses.</span></span>

|  | <span data-ttu-id="691b1-126">**Servizi mobili**</span><span class="sxs-lookup"><span data-stu-id="691b1-126">**Mobile Services** Node.js or .NET</span></span> | <span data-ttu-id="691b1-127">**App per dispositivi mobili**</span><span class="sxs-lookup"><span data-stu-id="691b1-127">**Mobile Apps** Node.js or .NET</span></span> |
| --- | --- | --- |
| <span data-ttu-id="691b1-128">[Client di Servizi mobili]</span><span class="sxs-lookup"><span data-stu-id="691b1-128">[Mobile Services clients]</span></span> |<span data-ttu-id="691b1-129">OK</span><span class="sxs-lookup"><span data-stu-id="691b1-129">Ok</span></span> |<span data-ttu-id="691b1-130">Errore\*</span><span class="sxs-lookup"><span data-stu-id="691b1-130">Error\*</span></span> |
| <span data-ttu-id="691b1-131">[Client di App per dispositivi mobili]</span><span class="sxs-lookup"><span data-stu-id="691b1-131">[Mobile Apps clients]</span></span> |<span data-ttu-id="691b1-132">Errore\*</span><span class="sxs-lookup"><span data-stu-id="691b1-132">Error\*</span></span> |<span data-ttu-id="691b1-133">OK</span><span class="sxs-lookup"><span data-stu-id="691b1-133">Ok</span></span> |

<span data-ttu-id="691b1-134">\*Può essere controllato specificando **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="691b1-134">\*This can be controlled by specifying **MS_SkipVersionCheck**.</span></span>

<!-- IMPORTANT!  hello anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: hello fwlink toothis document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <span data-ttu-id="691b1-135"><a name="1.0.0"></a>Client e server di Servizi mobili</span><span class="sxs-lookup"><span data-stu-id="691b1-135"><a name="1.0.0"></a>Mobile Services client and server</span></span>
<span data-ttu-id="691b1-136">SDK per applicazioni client Hello in tabella hello riportata di seguito sono compatibili con **servizi mobili**.</span><span class="sxs-lookup"><span data-stu-id="691b1-136">hello client SDKs in hello table below are compatible with **Mobile Services**.</span></span>

<span data-ttu-id="691b1-137">Nota: hello SDK client Servizi mobili *non* per inviare un valore di intestazione `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="691b1-137">Note: hello Mobile Services client SDKs *do not* send a header value for `ZUMO-API-VERSION`.</span></span> <span data-ttu-id="691b1-138">Se il servizio di hello riceve questa intestazione o un valore di stringa di query, verrà restituito un errore, a meno che non si è scelto in modo esplicito come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="691b1-138">If hello service receives this header or query string value, an error will be returned, unless you have explicitly opted out as described above.</span></span>

### <span data-ttu-id="691b1-139"><a name="MobileServicesClients"></a> SDK del client di *Servizi* mobili</span><span class="sxs-lookup"><span data-stu-id="691b1-139"><a name="MobileServicesClients"></a> Mobile *Services* client SDKs</span></span>
| <span data-ttu-id="691b1-140">Piattaforma client</span><span class="sxs-lookup"><span data-stu-id="691b1-140">Client platform</span></span> | <span data-ttu-id="691b1-141">Versione</span><span class="sxs-lookup"><span data-stu-id="691b1-141">Version</span></span> | <span data-ttu-id="691b1-142">Valore dell'intestazione della versione</span><span class="sxs-lookup"><span data-stu-id="691b1-142">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="691b1-143">Client gestito (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="691b1-143">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="691b1-144">1.3.2</span><span class="sxs-lookup"><span data-stu-id="691b1-144">1.3.2</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |<span data-ttu-id="691b1-145">n/d</span><span class="sxs-lookup"><span data-stu-id="691b1-145">n/a</span></span> |
| <span data-ttu-id="691b1-146">iOS</span><span class="sxs-lookup"><span data-stu-id="691b1-146">iOS</span></span> |[<span data-ttu-id="691b1-147">2.2.2</span><span class="sxs-lookup"><span data-stu-id="691b1-147">2.2.2</span></span>](http://aka.ms/gc6fex) |<span data-ttu-id="691b1-148">n/d</span><span class="sxs-lookup"><span data-stu-id="691b1-148">n/a</span></span> |
| <span data-ttu-id="691b1-149">Android</span><span class="sxs-lookup"><span data-stu-id="691b1-149">Android</span></span> |[<span data-ttu-id="691b1-150">2.0.3</span><span class="sxs-lookup"><span data-stu-id="691b1-150">2.0.3</span></span>](https://go.microsoft.com/fwLink/?LinkID=280126) |<span data-ttu-id="691b1-151">n/d</span><span class="sxs-lookup"><span data-stu-id="691b1-151">n/a</span></span> |
| <span data-ttu-id="691b1-152">HTML</span><span class="sxs-lookup"><span data-stu-id="691b1-152">HTML</span></span> |[<span data-ttu-id="691b1-153">1.2.7</span><span class="sxs-lookup"><span data-stu-id="691b1-153">1.2.7</span></span>](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |<span data-ttu-id="691b1-154">n/d</span><span class="sxs-lookup"><span data-stu-id="691b1-154">n/a</span></span> |

### <a name="mobile-services-server-sdks"></a><span data-ttu-id="691b1-155">SDK del server di *Servizi* mobili</span><span class="sxs-lookup"><span data-stu-id="691b1-155">Mobile *Services* server SDKs</span></span>
| <span data-ttu-id="691b1-156">Piattaforma server</span><span class="sxs-lookup"><span data-stu-id="691b1-156">Server platform</span></span> | <span data-ttu-id="691b1-157">Versione</span><span class="sxs-lookup"><span data-stu-id="691b1-157">Version</span></span> | <span data-ttu-id="691b1-158">Intestazione della versione accettata</span><span class="sxs-lookup"><span data-stu-id="691b1-158">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="691b1-159">.NET</span><span class="sxs-lookup"><span data-stu-id="691b1-159">.NET</span></span> |[<span data-ttu-id="691b1-160">WindowsAzure.MobileServices.Backend.* Versione 1.0.x</span><span class="sxs-lookup"><span data-stu-id="691b1-160">WindowsAzure.MobileServices.Backend.* Version 1.0.x</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |<span data-ttu-id="691b1-161">* * Nessuna intestazione di versione * *</span><span class="sxs-lookup"><span data-stu-id="691b1-161">**No version header **</span></span> |
| <span data-ttu-id="691b1-162">Node.js</span><span class="sxs-lookup"><span data-stu-id="691b1-162">Node.js</span></span> |<span data-ttu-id="691b1-163">(Presto disponibile)</span><span class="sxs-lookup"><span data-stu-id="691b1-163">(coming soon)</span></span> |<span data-ttu-id="691b1-164">**Nessuna intestazione di versione**</span><span class="sxs-lookup"><span data-stu-id="691b1-164">**No version header**</span></span> |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a><span data-ttu-id="691b1-165">Comportamento dei back-end di Servizi mobili</span><span class="sxs-lookup"><span data-stu-id="691b1-165">Behavior of Mobile Services backends</span></span>
| <span data-ttu-id="691b1-166">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="691b1-166">ZUMO-API-VERSION</span></span> | <span data-ttu-id="691b1-167">Valore di MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="691b1-167">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="691b1-168">Response</span><span class="sxs-lookup"><span data-stu-id="691b1-168">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="691b1-169">Non specificato</span><span class="sxs-lookup"><span data-stu-id="691b1-169">Not specified</span></span> |<span data-ttu-id="691b1-170">Qualsiasi</span><span class="sxs-lookup"><span data-stu-id="691b1-170">Any</span></span> |<span data-ttu-id="691b1-171">200 - OK</span><span class="sxs-lookup"><span data-stu-id="691b1-171">200 - OK</span></span> |
| <span data-ttu-id="691b1-172">Qualsiasi valore</span><span class="sxs-lookup"><span data-stu-id="691b1-172">Any value</span></span> |<span data-ttu-id="691b1-173">True</span><span class="sxs-lookup"><span data-stu-id="691b1-173">True</span></span> |<span data-ttu-id="691b1-174">200 - OK</span><span class="sxs-lookup"><span data-stu-id="691b1-174">200 - OK</span></span> |
| <span data-ttu-id="691b1-175">Qualsiasi valore</span><span class="sxs-lookup"><span data-stu-id="691b1-175">Any value</span></span> |<span data-ttu-id="691b1-176">False/Non specificato</span><span class="sxs-lookup"><span data-stu-id="691b1-176">False/Not Specified</span></span> |<span data-ttu-id="691b1-177">400 - Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="691b1-177">400 - Bad Request</span></span> |

## <span data-ttu-id="691b1-178"><a name="2.0.0"></a>Client e server di App per dispositivi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="691b1-178"><a name="2.0.0"></a>Azure Mobile Apps client and server</span></span>
### <span data-ttu-id="691b1-179"><a name="MobileAppsClients"></a> SDK del client di *App* per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="691b1-179"><a name="MobileAppsClients"></a> Mobile *Apps* client SDKs</span></span>
<span data-ttu-id="691b1-180">Il controllo della versione è stato introdotto a partire da hello seguenti versioni del client hello SDK per **App mobili di Azure**:</span><span class="sxs-lookup"><span data-stu-id="691b1-180">Version checking was introduced starting with hello following versions of hello client SDK for **Azure Mobile Apps**:</span></span>

| <span data-ttu-id="691b1-181">Piattaforma client</span><span class="sxs-lookup"><span data-stu-id="691b1-181">Client platform</span></span> | <span data-ttu-id="691b1-182">Versione</span><span class="sxs-lookup"><span data-stu-id="691b1-182">Version</span></span> | <span data-ttu-id="691b1-183">Valore dell'intestazione della versione</span><span class="sxs-lookup"><span data-stu-id="691b1-183">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="691b1-184">Client gestito (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="691b1-184">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="691b1-185">2.0.0</span><span class="sxs-lookup"><span data-stu-id="691b1-185">2.0.0</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |<span data-ttu-id="691b1-186">2.0.0</span><span class="sxs-lookup"><span data-stu-id="691b1-186">2.0.0</span></span> |
| <span data-ttu-id="691b1-187">iOS</span><span class="sxs-lookup"><span data-stu-id="691b1-187">iOS</span></span> |[<span data-ttu-id="691b1-188">3.0.0</span><span class="sxs-lookup"><span data-stu-id="691b1-188">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=529823) |<span data-ttu-id="691b1-189">2.0.0</span><span class="sxs-lookup"><span data-stu-id="691b1-189">2.0.0</span></span> |
| <span data-ttu-id="691b1-190">Android</span><span class="sxs-lookup"><span data-stu-id="691b1-190">Android</span></span> |[<span data-ttu-id="691b1-191">3.0.0</span><span class="sxs-lookup"><span data-stu-id="691b1-191">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |<span data-ttu-id="691b1-192">3.0.0</span><span class="sxs-lookup"><span data-stu-id="691b1-192">3.0.0</span></span> |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a><span data-ttu-id="691b1-193">SDK del server di *App* per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="691b1-193">Mobile *Apps* server SDKs</span></span>
<span data-ttu-id="691b1-194">Il controllo della versione è incluso nelle seguenti versioni dell’SDK del server:</span><span class="sxs-lookup"><span data-stu-id="691b1-194">Version checking is included in following server SDK versions:</span></span>

| <span data-ttu-id="691b1-195">Piattaforma server</span><span class="sxs-lookup"><span data-stu-id="691b1-195">Server platform</span></span> | <span data-ttu-id="691b1-196">SDK</span><span class="sxs-lookup"><span data-stu-id="691b1-196">SDK</span></span> | <span data-ttu-id="691b1-197">Intestazione della versione accettata</span><span class="sxs-lookup"><span data-stu-id="691b1-197">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="691b1-198">.NET</span><span class="sxs-lookup"><span data-stu-id="691b1-198">.NET</span></span> |[<span data-ttu-id="691b1-199">Microsoft.Azure.Mobile.Server</span><span class="sxs-lookup"><span data-stu-id="691b1-199">Microsoft.Azure.Mobile.Server</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |<span data-ttu-id="691b1-200">2.0.0</span><span class="sxs-lookup"><span data-stu-id="691b1-200">2.0.0</span></span> |
| <span data-ttu-id="691b1-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="691b1-201">Node.js</span></span> |[<span data-ttu-id="691b1-202">azure-mobile-apps)</span><span class="sxs-lookup"><span data-stu-id="691b1-202">azure-mobile-apps)</span></span>](https://www.npmjs.com/package/azure-mobile-apps) |<span data-ttu-id="691b1-203">2.0.0</span><span class="sxs-lookup"><span data-stu-id="691b1-203">2.0.0</span></span> |

### <a name="behavior-of-mobile-apps-backends"></a><span data-ttu-id="691b1-204">Comportamento dei back-end di app per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="691b1-204">Behavior of Mobile Apps backends</span></span>
| <span data-ttu-id="691b1-205">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="691b1-205">ZUMO-API-VERSION</span></span> | <span data-ttu-id="691b1-206">Valore di MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="691b1-206">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="691b1-207">Response</span><span class="sxs-lookup"><span data-stu-id="691b1-207">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="691b1-208">x.y.z o Null</span><span class="sxs-lookup"><span data-stu-id="691b1-208">x.y.z or Null</span></span> |<span data-ttu-id="691b1-209">True</span><span class="sxs-lookup"><span data-stu-id="691b1-209">True</span></span> |<span data-ttu-id="691b1-210">200 - OK</span><span class="sxs-lookup"><span data-stu-id="691b1-210">200 - OK</span></span> |
| <span data-ttu-id="691b1-211">Null</span><span class="sxs-lookup"><span data-stu-id="691b1-211">Null</span></span> |<span data-ttu-id="691b1-212">False/Non specificato</span><span class="sxs-lookup"><span data-stu-id="691b1-212">False/Not Specified</span></span> |<span data-ttu-id="691b1-213">400 - Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="691b1-213">400 - Bad Request</span></span> |
| <span data-ttu-id="691b1-214">1.x.y</span><span class="sxs-lookup"><span data-stu-id="691b1-214">1.x.y</span></span> |<span data-ttu-id="691b1-215">False/Non specificato</span><span class="sxs-lookup"><span data-stu-id="691b1-215">False/Not Specified</span></span> |<span data-ttu-id="691b1-216">400 - Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="691b1-216">400 - Bad Request</span></span> |
| <span data-ttu-id="691b1-217">2.0.0-2.x.y</span><span class="sxs-lookup"><span data-stu-id="691b1-217">2.0.0-2.x.y</span></span> |<span data-ttu-id="691b1-218">False/Non specificato</span><span class="sxs-lookup"><span data-stu-id="691b1-218">False/Not Specified</span></span> |<span data-ttu-id="691b1-219">200 - OK</span><span class="sxs-lookup"><span data-stu-id="691b1-219">200 - OK</span></span> |
| <span data-ttu-id="691b1-220">3.0.0-3.x.y</span><span class="sxs-lookup"><span data-stu-id="691b1-220">3.0.0-3.x.y</span></span> |<span data-ttu-id="691b1-221">False/Non specificato</span><span class="sxs-lookup"><span data-stu-id="691b1-221">False/Not Specified</span></span> |<span data-ttu-id="691b1-222">400 - Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="691b1-222">400 - Bad Request</span></span> |

## <a name="next-steps"></a><span data-ttu-id="691b1-223">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="691b1-223">Next Steps</span></span>
* <span data-ttu-id="691b1-224">[tooAzure un servizio Mobile servizio App di eseguire la migrazione]</span><span class="sxs-lookup"><span data-stu-id="691b1-224">[Migrate a Mobile Service tooAzure App Service]</span></span>

[Client di Servizi mobili]: #MobileServicesClients
[Client di App per dispositivi mobili]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[tooAzure un servizio Mobile servizio App di eseguire la migrazione]: app-service-mobile-migrating-from-mobile-services.md
