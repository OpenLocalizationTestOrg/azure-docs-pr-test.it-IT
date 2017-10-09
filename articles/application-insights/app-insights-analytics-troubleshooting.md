---
title: aaaTroubleshoot Analitica in Azure Application Insights | Documenti Microsoft
description: 'Problemi con Application Insights Analytics? Inizia da qui. '
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/11/2016
ms.author: bwren
ms.openlocfilehash: e3be2fbc0237440d3b8a736484434a9f276296c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a><span data-ttu-id="c9bca-104">Risoluzione dei problemi di Analytics in Application Insights</span><span class="sxs-lookup"><span data-stu-id="c9bca-104">Troubleshoot Analytics in Application Insights</span></span>
<span data-ttu-id="c9bca-105">Problemi con [Application Insights Analytics](app-insights-analytics.md)?</span><span class="sxs-lookup"><span data-stu-id="c9bca-105">Problems with [Application Insights Analytics](app-insights-analytics.md)?</span></span> <span data-ttu-id="c9bca-106">Inizia da qui.</span><span class="sxs-lookup"><span data-stu-id="c9bca-106">Start here.</span></span> <span data-ttu-id="c9bca-107">Analitica è hello potente strumento di ricerca di Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c9bca-107">Analytics is hello powerful search tool of Azure Application Insights.</span></span>

## <a name="limits"></a><span data-ttu-id="c9bca-108">Limiti</span><span class="sxs-lookup"><span data-stu-id="c9bca-108">Limits</span></span>
* <span data-ttu-id="c9bca-109">Al momento, i risultati della query sono toojust limitato più di una settimana di dati passati.</span><span class="sxs-lookup"><span data-stu-id="c9bca-109">At present, query results are limited toojust over a week of past data.</span></span>
* <span data-ttu-id="c9bca-110">Browser su cui eseguiamo i test: versioni più recenti di Chrome, Edge e Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="c9bca-110">Browsers we test on: latest editions of Chrome, Edge, and Internet Explorer.</span></span>

## <a name="known-incompatible-browser-extensions"></a><span data-ttu-id="c9bca-111">Estensioni del browser dall'incompatibilità nota</span><span class="sxs-lookup"><span data-stu-id="c9bca-111">Known incompatible browser extensions</span></span>
* <span data-ttu-id="c9bca-112">Ghostery</span><span class="sxs-lookup"><span data-stu-id="c9bca-112">Ghostery</span></span>

<span data-ttu-id="c9bca-113">Disabilitare l'estensione hello o utilizzare un browser diverso.</span><span class="sxs-lookup"><span data-stu-id="c9bca-113">Disable hello extension or use a different browser.</span></span>

## <span data-ttu-id="c9bca-114"><a name="e-a"></a> "Errore imprevisto"</span><span class="sxs-lookup"><span data-stu-id="c9bca-114"><a name="e-a"></a> "Unexpected error"</span></span>
![Schermata di errore imprevisto](./media/app-insights-analytics-troubleshooting/010.png)

<span data-ttu-id="c9bca-116">Si è verificato un errore interno durante il runtime del portale: eccezione non gestita.</span><span class="sxs-lookup"><span data-stu-id="c9bca-116">Internal error occurred during portal runtime – unhandled exception.</span></span>

* <span data-ttu-id="c9bca-117">Eseguire la pulizia della cache del browser hello.</span><span class="sxs-lookup"><span data-stu-id="c9bca-117">Clean hello browser's cache.</span></span> 

## <span data-ttu-id="c9bca-118"><a name="e-b"></a>403.... riprovare tooreload</span><span class="sxs-lookup"><span data-stu-id="c9bca-118"><a name="e-b"></a>403 ... please try tooreload</span></span>
![403.... riprovare tooreload](./media/app-insights-analytics-troubleshooting/020.png)

<span data-ttu-id="c9bca-120">Si è verificato un errore correlato all'autenticazione (durante l'autenticazione o durante la generazione del token di accesso).</span><span class="sxs-lookup"><span data-stu-id="c9bca-120">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="c9bca-121">portale Hello può in alcun modo troppo ripristinare senza modificare le impostazioni del browser.</span><span class="sxs-lookup"><span data-stu-id="c9bca-121">hello portal may have no way too recover without changing browser settings.</span></span>

* <span data-ttu-id="c9bca-122">Verificare [sono abilitati i cookie di terze parti](#cookies) nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="c9bca-122">Verify [third party cookies are enabled](#cookies) in hello browser.</span></span> 

## <span data-ttu-id="c9bca-123"><a name="authentication"></a>403 ... verificare l'area di sicurezza</span><span class="sxs-lookup"><span data-stu-id="c9bca-123"><a name="authentication"></a>403 ... verify security zone</span></span>
![403 ... verify security zone](./media/app-insights-analytics-troubleshooting/030.png)

<span data-ttu-id="c9bca-125">Si è verificato un errore correlato all'autenticazione (durante l'autenticazione o durante la generazione del token di accesso).</span><span class="sxs-lookup"><span data-stu-id="c9bca-125">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="c9bca-126">portale Hello può in alcun modo troppo ripristinare senza modificare le impostazioni del browser.</span><span class="sxs-lookup"><span data-stu-id="c9bca-126">hello portal may have no way too recover without changing browser settings.</span></span>

1. <span data-ttu-id="c9bca-127">Verificare [sono abilitati i cookie di terze parti](#cookies) nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="c9bca-127">Verify [third party cookies are enabled](#cookies) in hello browser.</span></span> 
2. <span data-ttu-id="c9bca-128">È stato usato un preferito, un segnalibro o un collegamento salvato tooopen hello Analitica portale?</span><span class="sxs-lookup"><span data-stu-id="c9bca-128">Did you use a favorite, bookmark or saved link tooopen hello Analytics portal?</span></span> <span data-ttu-id="c9bca-129">È eseguito l'accesso con credenziali diverse da quello utilizzato al momento del salvataggio collegamento hello?</span><span class="sxs-lookup"><span data-stu-id="c9bca-129">Are you signed in with different credentials than you used when you saved hello link?</span></span>
3. <span data-ttu-id="c9bca-130">Provare a utilizzare una finestra del browser privata/in incognito (dopo aver chiuso tutte le finestre di questo tipo).</span><span class="sxs-lookup"><span data-stu-id="c9bca-130">Try using an in-private/incognito browser window (after closing all such windows).</span></span> <span data-ttu-id="c9bca-131">È necessario tooprovide le credenziali.</span><span class="sxs-lookup"><span data-stu-id="c9bca-131">You'll have tooprovide your credentials.</span></span> 
4. <span data-ttu-id="c9bca-132">Aprire un'altra finestra del browser (comune) e andare troppo[Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c9bca-132">Open another (ordinary) browser window and go too[Azure](https://portal.azure.com).</span></span> <span data-ttu-id="c9bca-133">Uscire, Aprire il collegamento e accedere con le credenziali corrette hello.</span><span class="sxs-lookup"><span data-stu-id="c9bca-133">Sign out. Then open your link and sign in with hello correct credentials.</span></span>
5. <span data-ttu-id="c9bca-134">Gli utenti di Edge e Internet Explorer possono ricevere questo errore anche quando le impostazioni delle zone attendibili non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="c9bca-134">Edge and Internet Explorer users can also get this error when trusted zone settings are not supported.</span></span>
   
    <span data-ttu-id="c9bca-135">Verificare sia [portale Analitica](https://analytics.applicationinsights.io) e [portale di Azure Active Directory](https://portal.azure.com) in hello stessa area di protezione:</span><span class="sxs-lookup"><span data-stu-id="c9bca-135">Verify both [Analytics portal](https://analytics.applicationinsights.io) and [Azure Active Directory portal](https://portal.azure.com) are in hello same security zone:</span></span>
   
   * <span data-ttu-id="c9bca-136">In Internet Explorer aprire **Opzioni Internet**, **Sicurezza**, **Siti attendibili**, **Siti**:</span><span class="sxs-lookup"><span data-stu-id="c9bca-136">In Internet Explorer, open **Internet Options**, **Security**, **Trusted sites**, **Sites**:</span></span>
     
     ![Finestra di dialogo Opzioni Internet, l'aggiunta di un sito tooTrusted siti](./media/app-insights-analytics-troubleshooting/033.png)
     
     <span data-ttu-id="c9bca-138">Nell'elenco di siti Web hello, se uno qualsiasi dei hello URL seguenti sono incluso, assicurarsi che tale hello ad altri utenti sono inoltre inclusi:</span><span class="sxs-lookup"><span data-stu-id="c9bca-138">In hello Websites list, if any of hello following URLs are included, make sure that hello others are included also:</span></span>
     
     <span data-ttu-id="c9bca-139">https://analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="c9bca-139">https://analytics.applicationinsights.io</span></span><br/>
     <span data-ttu-id="c9bca-140">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="c9bca-140">https://login.microsoftonline.com</span></span><br/>
     <span data-ttu-id="c9bca-141">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="c9bca-141">https://login.windows.net</span></span>

## <span data-ttu-id="c9bca-142"><a name="e-d"></a>404 ... Resource not found</span><span class="sxs-lookup"><span data-stu-id="c9bca-142"><a name="e-d"></a>404 ... Resource not found</span></span>
![404 ... resource not found](./media/app-insights-analytics-troubleshooting/040.png)

<span data-ttu-id="c9bca-144">Una risorsa dell'applicazione è stata eliminata da Application Insights e non è più disponibile.</span><span class="sxs-lookup"><span data-stu-id="c9bca-144">Application resource was deleted from Application Insights and isn’t available anymore.</span></span> <span data-ttu-id="c9bca-145">Questa situazione può verificarsi se è stato salvato nella pagina hello URL toohello Analitica.</span><span class="sxs-lookup"><span data-stu-id="c9bca-145">This can happen if you saved hello URL toohello Analytics page.</span></span>

## <span data-ttu-id="c9bca-146"><a name="e-e"></a>403 ... No authorization</span><span class="sxs-lookup"><span data-stu-id="c9bca-146"><a name="e-e"></a>403 ... No authorization</span></span>
![403 ... not authorized](./media/app-insights-analytics-troubleshooting/050.png)

<span data-ttu-id="c9bca-148">Non si dispone dell'autorizzazione tooopen questa applicazione in Analitica.</span><span class="sxs-lookup"><span data-stu-id="c9bca-148">You don't have permission tooopen this application in Analytics.</span></span>

* <span data-ttu-id="c9bca-149">Sono stati ottenuti hello collegamento da un altro utente?</span><span class="sxs-lookup"><span data-stu-id="c9bca-149">Did you get hello link from someone else?</span></span> <span data-ttu-id="c9bca-150">Chiedere che la hello toomake [lettori o collaboratori per questo gruppo di risorse](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="c9bca-150">Ask them toomake sure you are in hello [readers or contributors for this resource group](app-insights-resources-roles-access-control.md).</span></span>
* <span data-ttu-id="c9bca-151">È stato salvato il collegamento hello utilizzando credenziali diverse?</span><span class="sxs-lookup"><span data-stu-id="c9bca-151">Did you save hello link using different credentials?</span></span> <span data-ttu-id="c9bca-152">Aprire hello [portale di Azure](https://portal.azure.com), disconnettersi e quindi provare questo collegamento, fornendo le credenziali corrette hello.</span><span class="sxs-lookup"><span data-stu-id="c9bca-152">Open hello [Azure portal](https://portal.azure.com), sign out, and then try this link again, providing hello correct credentials.</span></span>

## <span data-ttu-id="c9bca-153"><a name="html-storage"></a>403 ... HTML5 Storage</span><span class="sxs-lookup"><span data-stu-id="c9bca-153"><a name="html-storage"></a>403 ... HTML5 Storage</span></span>
<span data-ttu-id="c9bca-154">Il portale utilizza HTML5 localStorage e sessionStorage.</span><span class="sxs-lookup"><span data-stu-id="c9bca-154">Our portal uses HTML5 localStorage and sessionStorage.</span></span>

* <span data-ttu-id="c9bca-155">Chrome: Impostazioni, Privacy, Impostazioni contenuti.</span><span class="sxs-lookup"><span data-stu-id="c9bca-155">Chrome: Settings, privacy, content settings.</span></span>
* <span data-ttu-id="c9bca-156">Internet Explorer: Opzioni Internet, scheda Avanzate, Sicurezza, Abilita archiviazione DOM</span><span class="sxs-lookup"><span data-stu-id="c9bca-156">Internet Explorer: Internet Options, Advanced tab, Security, Enable DOM Storage</span></span>

![403... provare archiviazione tooenable HTML5](./media/app-insights-analytics-troubleshooting/060.png)

## <span data-ttu-id="c9bca-158"><a name="e-g"></a>404 ... Sottoscrizione non trovata</span><span class="sxs-lookup"><span data-stu-id="c9bca-158"><a name="e-g"></a>404 ... Subscription not found</span></span>
![404 ... Sottoscrizione non trovata](./media/app-insights-analytics-troubleshooting/070.png)

<span data-ttu-id="c9bca-160">Hello URL è valido.</span><span class="sxs-lookup"><span data-stu-id="c9bca-160">hello URL is invalid.</span></span> 

* <span data-ttu-id="c9bca-161">Aprire una risorsa applicazione hello in [portale Application Insights](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c9bca-161">Open hello app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="c9bca-162">Quindi sul pulsante hello Analitica.</span><span class="sxs-lookup"><span data-stu-id="c9bca-162">Then use hello Analytics button.</span></span>

## <span data-ttu-id="c9bca-163"><a name="e-h"></a>404 ... la pagina non esiste</span><span class="sxs-lookup"><span data-stu-id="c9bca-163"><a name="e-h"></a>404 ... page doesn't exist</span></span>
![404 ... Page does not exist](./media/app-insights-analytics-troubleshooting/080.png)

<span data-ttu-id="c9bca-165">Hello URL è valido.</span><span class="sxs-lookup"><span data-stu-id="c9bca-165">hello URL is invalid.</span></span>

* <span data-ttu-id="c9bca-166">Aprire una risorsa applicazione hello in [portale Application Insights](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c9bca-166">Open hello app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="c9bca-167">Quindi sul pulsante hello Analitica.</span><span class="sxs-lookup"><span data-stu-id="c9bca-167">Then use hello Analytics button.</span></span>

## <span data-ttu-id="c9bca-168"><a name="cookies"></a>Abilitare i cookie di terze parti</span><span class="sxs-lookup"><span data-stu-id="c9bca-168"><a name="cookies"></a>Enable third-party cookies</span></span>
  <span data-ttu-id="c9bca-169">Vedere [come toodisable terze parti cookie](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), ma è necessario troppo**abilitare** li.</span><span class="sxs-lookup"><span data-stu-id="c9bca-169">See [how toodisable third party cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), but notice we need too**enable** them.</span></span>


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

