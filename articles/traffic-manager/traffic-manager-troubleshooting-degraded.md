---
title: stato aaaTroubleshooting ridotto per gestione traffico di Azure
description: Come i profili di gestione traffico tootroubleshoot quando viene illustrato come dello stato danneggiato.
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
ms.assetid: 8af0433d-e61b-4761-adcc-7bc9b8142fc6
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: kumud
ms.openlocfilehash: fd95697781472b52e98d856e66beb7b89dfeaf23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a><span data-ttu-id="dcab9-103">Risoluzione dei problemi relativi allo stato Danneggiato di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="dcab9-103">Troubleshooting degraded state on Azure Traffic Manager</span></span>

<span data-ttu-id="dcab9-104">In questo articolo viene descritto come tootroubleshoot un profilo di Traffic Manager di Azure che viene visualizzato uno stato danneggiato.</span><span class="sxs-lookup"><span data-stu-id="dcab9-104">This article describes how tootroubleshoot an Azure Traffic Manager profile that is showing a degraded status.</span></span> <span data-ttu-id="dcab9-105">Per questo scenario, è consigliabile che sia stato configurato un profilo di gestione traffico verso toosome dei servizi ospitati cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="dcab9-105">For this scenario, consider that you have configured a Traffic Manager profile pointing toosome of your cloudapp.net hosted services.</span></span> <span data-ttu-id="dcab9-106">Se l'integrità di hello di gestione del traffico consente di visualizzare un **danneggiato** potrebbe essere stato, quindi lo stato di hello di uno o più endpoint **danneggiato**:</span><span class="sxs-lookup"><span data-stu-id="dcab9-106">If hello health of your Traffic Manager displays a **Degraded** status, then hello status of one or more endpoints may be **Degraded**:</span></span>

![Stato degli endpoint Danneggiato](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

<span data-ttu-id="dcab9-108">Se l'integrità di hello di gestione del traffico consente di visualizzare un **inattivo** stato, entrambi gli endpoint possono essere **disabilitato**:</span><span class="sxs-lookup"><span data-stu-id="dcab9-108">If hello health of your Traffic Manager displays an **Inactive** status, then both end points may be **Disabled**:</span></span>

![Stato Inattivo di Gestione traffico](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a><span data-ttu-id="dcab9-110">Informazioni sui probe di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="dcab9-110">Understanding Traffic Manager probes</span></span>

* <span data-ttu-id="dcab9-111">Gestione traffico considera un toobe endpoint ONLINE solo quando probe hello riceve una risposta HTTP 200 eseguire il backup dal percorso di sondaggio hello.</span><span class="sxs-lookup"><span data-stu-id="dcab9-111">Traffic Manager considers an endpoint toobe ONLINE only when hello probe receives an HTTP 200 response back from hello probe path.</span></span> <span data-ttu-id="dcab9-112">Qualsiasi risposta diversa da 200 viene considerata un errore.</span><span class="sxs-lookup"><span data-stu-id="dcab9-112">Any other non-200 response is a failure.</span></span>
* <span data-ttu-id="dcab9-113">Un reindirizzamento 30 x ha esito negativo, anche se hello reindirizzato URL restituisce 200.</span><span class="sxs-lookup"><span data-stu-id="dcab9-113">A 30x redirect fails, even if hello redirected URL returns a 200.</span></span>
* <span data-ttu-id="dcab9-114">Per i probe HTTPS, gli errori di certificati vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="dcab9-114">For HTTPs probes, certificate errors are ignored.</span></span>
* <span data-ttu-id="dcab9-115">contenuto effettivo di Hello del percorso di sondaggio hello non è rilevante, purché viene restituito un messaggio 200.</span><span class="sxs-lookup"><span data-stu-id="dcab9-115">hello actual content of hello probe path doesn't matter, as long as a 200 is returned.</span></span> <span data-ttu-id="dcab9-116">Ricerca di un tipo di URL toosome statico contenuto "/ favicon.ico" è una tecnica comune.</span><span class="sxs-lookup"><span data-stu-id="dcab9-116">Probing a URL toosome static content like "/favicon.ico" is a common technique.</span></span> <span data-ttu-id="dcab9-117">Contenuto dinamico, ad esempio le pagine ASP hello, non sempre restituisca 200, anche quando un'applicazione hello è integra.</span><span class="sxs-lookup"><span data-stu-id="dcab9-117">Dynamic content, like hello ASP pages, may not always return 200, even when hello application is healthy.</span></span>
* <span data-ttu-id="dcab9-118">Una procedura consigliata è tooset hello Probe toosomething percorso dotato di sufficiente toodetermine logica che hello del sito è verso l'alto o verso il basso.</span><span class="sxs-lookup"><span data-stu-id="dcab9-118">A best practice is tooset hello Probe path toosomething that has enough logic toodetermine that hello site is up or down.</span></span> <span data-ttu-id="dcab9-119">In hello delle esempio precedente, impostando hello percorso too"/favicon.ico", si desidera utilizzare solo tale w3wp.exe test sta rispondendo.</span><span class="sxs-lookup"><span data-stu-id="dcab9-119">In hello previous example, by setting hello path too"/favicon.ico", you are only testing that w3wp.exe is responding.</span></span> <span data-ttu-id="dcab9-120">Questo probe non indica necessariamente che l'applicazione Web è integra.</span><span class="sxs-lookup"><span data-stu-id="dcab9-120">This probe may not indicate that your web application is healthy.</span></span> <span data-ttu-id="dcab9-121">Un'opzione migliore può essere tooset tooa un percorso, ad esempio "/ Probe.aspx" che dispone dello stato di hello toodetermine logica del sito hello.</span><span class="sxs-lookup"><span data-stu-id="dcab9-121">A better option would be tooset a path tooa something such as "/Probe.aspx" that has logic toodetermine hello health of hello site.</span></span> <span data-ttu-id="dcab9-122">Ad esempio, è possibile utilizzare utilizzo tooCPU di contatori delle prestazioni o misura hello numero di richieste non riuscite.</span><span class="sxs-lookup"><span data-stu-id="dcab9-122">For example, you could use performance counters tooCPU utilization or measure hello number of failed requests.</span></span> <span data-ttu-id="dcab9-123">Oppure è possibile tentare le risorse del database tooaccess o toomake stato sessione assicurarsi che l'applicazione web hello funzioni.</span><span class="sxs-lookup"><span data-stu-id="dcab9-123">Or you could attempt tooaccess database resources or session state toomake sure that hello web application is working.</span></span>
* <span data-ttu-id="dcab9-124">Se tutti gli endpoint in un profilo sono danneggiati, quindi considera tutti gli endpoint di gestione traffico come integri e instrada il traffico tooall endpoint.</span><span class="sxs-lookup"><span data-stu-id="dcab9-124">If all endpoints in a profile are degraded, then Traffic Manager treats all endpoints as healthy and routes traffic tooall endpoints.</span></span> <span data-ttu-id="dcab9-125">Questo comportamento assicura che i problemi con hello meccanismo di probe non causino un'interruzione completa del servizio.</span><span class="sxs-lookup"><span data-stu-id="dcab9-125">This behavior ensures that problems with hello probing mechanism do not result in a complete outage of your service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="dcab9-126">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="dcab9-126">Troubleshooting</span></span>

<span data-ttu-id="dcab9-127">tootroubleshoot un errore probe, è necessario uno strumento che viene restituito il codice di stato HTTP hello dall'URL del probe hello.</span><span class="sxs-lookup"><span data-stu-id="dcab9-127">tootroubleshoot a probe failure, you need a tool that shows hello HTTP status code return from hello probe URL.</span></span> <span data-ttu-id="dcab9-128">Sono disponibili numerosi strumenti disponibili che mostrano hello risposta HTTP non elaborato.</span><span class="sxs-lookup"><span data-stu-id="dcab9-128">There are many tools available that show you hello raw HTTP response.</span></span>

* [<span data-ttu-id="dcab9-129">Fiddler</span><span class="sxs-lookup"><span data-stu-id="dcab9-129">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="dcab9-130">curl</span><span class="sxs-lookup"><span data-stu-id="dcab9-130">curl</span></span>](https://curl.haxx.se/)
* [<span data-ttu-id="dcab9-131">wget</span><span class="sxs-lookup"><span data-stu-id="dcab9-131">wget</span></span>](http://gnuwin32.sourceforge.net/packages/wget.htm)

<span data-ttu-id="dcab9-132">Inoltre, è possibile utilizzare scheda di rete hello di hello F12 strumenti di debug nelle risposte HTTP hello tooview di Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="dcab9-132">Also, you can use hello Network tab of hello F12 Debugging Tools in Internet Explorer tooview hello HTTP responses.</span></span>

<span data-ttu-id="dcab9-133">Per questo esempio si desidera risposta hello toosee l'URL del probe: http://watestsdp2008r2.cloudapp.net:80/Probe.</span><span class="sxs-lookup"><span data-stu-id="dcab9-133">For this example we want toosee hello response from our probe URL: http://watestsdp2008r2.cloudapp.net:80/Probe.</span></span> <span data-ttu-id="dcab9-134">Hello esempio PowerShell seguente illustra il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="dcab9-134">hello following PowerShell example illustrates hello problem.</span></span>

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

<span data-ttu-id="dcab9-135">Output di esempio:</span><span class="sxs-lookup"><span data-stu-id="dcab9-135">Example output:</span></span>

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

<span data-ttu-id="dcab9-136">Si noti che è pervenuta una risposta di reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="dcab9-136">Notice that we received a redirect response.</span></span> <span data-ttu-id="dcab9-137">Come indicato in precedenza, qualsiasi StatusCode diverso da 200 viene considerato un errore.</span><span class="sxs-lookup"><span data-stu-id="dcab9-137">As stated previously, any StatusCode other than 200 is considered a failure.</span></span> <span data-ttu-id="dcab9-138">Modifiche di Traffic Manager hello tooOffline lo stato di endpoint.</span><span class="sxs-lookup"><span data-stu-id="dcab9-138">Traffic Manager changes hello endpoint status tooOffline.</span></span> <span data-ttu-id="dcab9-139">problema di hello tooresolve, controllo hello sito Web configuration tooensure che hello StatusCode corretto può essere restituiti dal percorso di sondaggio hello.</span><span class="sxs-lookup"><span data-stu-id="dcab9-139">tooresolve hello problem, check hello website configuration tooensure that hello proper StatusCode can be returned from hello probe path.</span></span> <span data-ttu-id="dcab9-140">Riconfigurare hello Traffic Manager toopoint tooa percorso di sondaggio che restituisce un messaggio 200.</span><span class="sxs-lookup"><span data-stu-id="dcab9-140">Reconfigure hello Traffic Manager probe toopoint tooa path that returns a 200.</span></span>

<span data-ttu-id="dcab9-141">Se il probe utilizza hello il protocollo HTTPS, potrebbe essere toodisable certificato verifica degli errori SSL/TLS di tooavoid durante il test.</span><span class="sxs-lookup"><span data-stu-id="dcab9-141">If your probe is using hello HTTPS protocol, you may need toodisable certificate checking tooavoid SSL/TLS errors during your test.</span></span> <span data-ttu-id="dcab9-142">Hello istruzioni di PowerShell seguente disabilita la convalida dei certificati per la sessione corrente di PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="dcab9-142">hello following PowerShell statements disable certificate validation for hello current PowerShell session:</span></span>

```powershell
add-type @"
using System.Net;
using System.Security.Cryptography.X509Certificates;
public class TrustAllCertsPolicy : ICertificatePolicy {
    public bool CheckValidationResult(
    ServicePoint srvPoint, X509Certificate certificate,
    WebRequest request, int certificateProblem) {
    return true;
    }
}
"@
[System.Net.ServicePointManager]::CertificatePolicy = New-Object TrustAllCertsPolicy
```

## <a name="next-steps"></a><span data-ttu-id="dcab9-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dcab9-143">Next Steps</span></span>

[<span data-ttu-id="dcab9-144">Informazioni sui metodi di routing di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="dcab9-144">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="dcab9-145">Gestione traffico di Azure</span><span class="sxs-lookup"><span data-stu-id="dcab9-145">What is Traffic Manager</span></span>](traffic-manager-overview.md)

[<span data-ttu-id="dcab9-146">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="dcab9-146">Cloud Services</span></span>](http://go.microsoft.com/fwlink/?LinkId=314074)

[<span data-ttu-id="dcab9-147">App Web di Azure</span><span class="sxs-lookup"><span data-stu-id="dcab9-147">Azure Web Apps</span></span>](https://azure.microsoft.com/documentation/services/app-service/web/)

[<span data-ttu-id="dcab9-148">Operazioni per Gestione traffico (informazioni di riferimento API REST)</span><span class="sxs-lookup"><span data-stu-id="dcab9-148">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

<span data-ttu-id="dcab9-149">[Cmdlet di Gestione traffico di Azure][1]</span><span class="sxs-lookup"><span data-stu-id="dcab9-149">[Azure Traffic Manager Cmdlets][1]</span></span>

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
