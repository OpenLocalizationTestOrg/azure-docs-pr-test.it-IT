---
title: Risolvere i problemi di Analytics in Azure Application Insights | Documentazione Microsoft
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
ms.openlocfilehash: 02df117908fc1790e8cfb9ec0a7218c1b8be856c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a><span data-ttu-id="d066f-104">Risoluzione dei problemi di Analytics in Application Insights</span><span class="sxs-lookup"><span data-stu-id="d066f-104">Troubleshoot Analytics in Application Insights</span></span>
<span data-ttu-id="d066f-105">Problemi con [Application Insights Analytics](app-insights-analytics.md)?</span><span class="sxs-lookup"><span data-stu-id="d066f-105">Problems with [Application Insights Analytics](app-insights-analytics.md)?</span></span> <span data-ttu-id="d066f-106">Inizia da qui.</span><span class="sxs-lookup"><span data-stu-id="d066f-106">Start here.</span></span> <span data-ttu-id="d066f-107">Analytics è l'efficace strumento di ricerca incluso in Application Insights di Azure.</span><span class="sxs-lookup"><span data-stu-id="d066f-107">Analytics is the powerful search tool of Azure Application Insights.</span></span>

## <a name="limits"></a><span data-ttu-id="d066f-108">Limiti</span><span class="sxs-lookup"><span data-stu-id="d066f-108">Limits</span></span>
* <span data-ttu-id="d066f-109">Attualmente sono disponibili i risultati delle query per una settimana di dati.</span><span class="sxs-lookup"><span data-stu-id="d066f-109">At present, query results are limited to just over a week of past data.</span></span>
* <span data-ttu-id="d066f-110">Browser su cui eseguiamo i test: versioni più recenti di Chrome, Edge e Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="d066f-110">Browsers we test on: latest editions of Chrome, Edge, and Internet Explorer.</span></span>

## <a name="known-incompatible-browser-extensions"></a><span data-ttu-id="d066f-111">Estensioni del browser dall'incompatibilità nota</span><span class="sxs-lookup"><span data-stu-id="d066f-111">Known incompatible browser extensions</span></span>
* <span data-ttu-id="d066f-112">Ghostery</span><span class="sxs-lookup"><span data-stu-id="d066f-112">Ghostery</span></span>

<span data-ttu-id="d066f-113">Disabilitare l'estensione o utilizzare un altro browser.</span><span class="sxs-lookup"><span data-stu-id="d066f-113">Disable the extension or use a different browser.</span></span>

## <span data-ttu-id="d066f-114"><a name="e-a"></a> "Errore imprevisto"</span><span class="sxs-lookup"><span data-stu-id="d066f-114"><a name="e-a"></a> "Unexpected error"</span></span>
![Schermata di errore imprevisto](./media/app-insights-analytics-troubleshooting/010.png)

<span data-ttu-id="d066f-116">Si è verificato un errore interno durante il runtime del portale: eccezione non gestita.</span><span class="sxs-lookup"><span data-stu-id="d066f-116">Internal error occurred during portal runtime – unhandled exception.</span></span>

* <span data-ttu-id="d066f-117">Svuotare la cache del browser.</span><span class="sxs-lookup"><span data-stu-id="d066f-117">Clean the browser's cache.</span></span> 

## <span data-ttu-id="d066f-118"><a name="e-b"></a>403 ... provare a ricaricare la pagina</span><span class="sxs-lookup"><span data-stu-id="d066f-118"><a name="e-b"></a>403 ... please try to reload</span></span>
![403 ... please try to reload](./media/app-insights-analytics-troubleshooting/020.png)

<span data-ttu-id="d066f-120">Si è verificato un errore correlato all'autenticazione (durante l'autenticazione o durante la generazione del token di accesso).</span><span class="sxs-lookup"><span data-stu-id="d066f-120">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="d066f-121">Potrebbe non essere possibile ripristinare il portale senza modificare le impostazioni del browser.</span><span class="sxs-lookup"><span data-stu-id="d066f-121">The portal may have no way to  recover without changing browser settings.</span></span>

* <span data-ttu-id="d066f-122">Verificare che nel browser siano attivati i [cookie di terze parti](#cookies) .</span><span class="sxs-lookup"><span data-stu-id="d066f-122">Verify [third party cookies are enabled](#cookies) in the browser.</span></span> 

## <span data-ttu-id="d066f-123"><a name="authentication"></a>403 ... verificare l'area di sicurezza</span><span class="sxs-lookup"><span data-stu-id="d066f-123"><a name="authentication"></a>403 ... verify security zone</span></span>
![403 ... verify security zone](./media/app-insights-analytics-troubleshooting/030.png)

<span data-ttu-id="d066f-125">Si è verificato un errore correlato all'autenticazione (durante l'autenticazione o durante la generazione del token di accesso).</span><span class="sxs-lookup"><span data-stu-id="d066f-125">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="d066f-126">Potrebbe non essere possibile ripristinare il portale senza modificare le impostazioni del browser.</span><span class="sxs-lookup"><span data-stu-id="d066f-126">The portal may have no way to  recover without changing browser settings.</span></span>

1. <span data-ttu-id="d066f-127">Verificare che nel browser siano attivati i [cookie di terze parti](#cookies) .</span><span class="sxs-lookup"><span data-stu-id="d066f-127">Verify [third party cookies are enabled](#cookies) in the browser.</span></span> 
2. <span data-ttu-id="d066f-128">Il portale Analytics è stato aperto utilizzando preferiti, segnalibri o un collegamento salvato?</span><span class="sxs-lookup"><span data-stu-id="d066f-128">Did you use a favorite, bookmark or saved link to open the Analytics portal?</span></span> <span data-ttu-id="d066f-129">L'accesso è stato eseguito con credenziali diverse da quelle utilizzate quando è stato salvato il collegamento?</span><span class="sxs-lookup"><span data-stu-id="d066f-129">Are you signed in with different credentials than you used when you saved the link?</span></span>
3. <span data-ttu-id="d066f-130">Provare a utilizzare una finestra del browser privata/in incognito (dopo aver chiuso tutte le finestre di questo tipo).</span><span class="sxs-lookup"><span data-stu-id="d066f-130">Try using an in-private/incognito browser window (after closing all such windows).</span></span> <span data-ttu-id="d066f-131">Sarà necessario fornire le credenziali.</span><span class="sxs-lookup"><span data-stu-id="d066f-131">You'll have to provide your credentials.</span></span> 
4. <span data-ttu-id="d066f-132">Aprire un'altra finestra del browser (normale) e accedere ad [Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d066f-132">Open another (ordinary) browser window and go to [Azure](https://portal.azure.com).</span></span> <span data-ttu-id="d066f-133">Uscire, quindi aprire il collegamento ed effettuare l'accesso con le credenziali corrette.</span><span class="sxs-lookup"><span data-stu-id="d066f-133">Sign out. Then open your link and sign in with the correct credentials.</span></span>
5. <span data-ttu-id="d066f-134">Gli utenti di Edge e Internet Explorer possono ricevere questo errore anche quando le impostazioni delle zone attendibili non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="d066f-134">Edge and Internet Explorer users can also get this error when trusted zone settings are not supported.</span></span>
   
    <span data-ttu-id="d066f-135">Verificare che il [portale di Analytics](https://analytics.applicationinsights.io) e il [portale di Azure Active Directory](https://portal.azure.com) si trovino nella stessa area di sicurezza:</span><span class="sxs-lookup"><span data-stu-id="d066f-135">Verify both [Analytics portal](https://analytics.applicationinsights.io) and [Azure Active Directory portal](https://portal.azure.com) are in the same security zone:</span></span>
   
   * <span data-ttu-id="d066f-136">In Internet Explorer aprire **Opzioni Internet**, **Sicurezza**, **Siti attendibili**, **Siti**:</span><span class="sxs-lookup"><span data-stu-id="d066f-136">In Internet Explorer, open **Internet Options**, **Security**, **Trusted sites**, **Sites**:</span></span>
     
     ![Finestra di dialogo Opzioni Internet, aggiungere un sito all'elenco dei siti attendibili](./media/app-insights-analytics-troubleshooting/033.png)
     
     <span data-ttu-id="d066f-138">Se nell'elenco dei siti Web compaiono i seguenti URL, controllare che siano inclusi anche gli altri:</span><span class="sxs-lookup"><span data-stu-id="d066f-138">In the Websites list, if any of the following URLs are included, make sure that the others are included also:</span></span>
     
     <span data-ttu-id="d066f-139">https://analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d066f-139">https://analytics.applicationinsights.io</span></span><br/>
     <span data-ttu-id="d066f-140">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d066f-140">https://login.microsoftonline.com</span></span><br/>
     <span data-ttu-id="d066f-141">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="d066f-141">https://login.windows.net</span></span>

## <span data-ttu-id="d066f-142"><a name="e-d"></a>404 ... Resource not found</span><span class="sxs-lookup"><span data-stu-id="d066f-142"><a name="e-d"></a>404 ... Resource not found</span></span>
![404 ... resource not found](./media/app-insights-analytics-troubleshooting/040.png)

<span data-ttu-id="d066f-144">Una risorsa dell'applicazione è stata eliminata da Application Insights e non è più disponibile.</span><span class="sxs-lookup"><span data-stu-id="d066f-144">Application resource was deleted from Application Insights and isn’t available anymore.</span></span> <span data-ttu-id="d066f-145">Questa situazione può verificarsi se è stato salvato l'URL alla pagina di Analytics.</span><span class="sxs-lookup"><span data-stu-id="d066f-145">This can happen if you saved the URL to the Analytics page.</span></span>

## <span data-ttu-id="d066f-146"><a name="e-e"></a>403 ... No authorization</span><span class="sxs-lookup"><span data-stu-id="d066f-146"><a name="e-e"></a>403 ... No authorization</span></span>
![403 ... not authorized](./media/app-insights-analytics-troubleshooting/050.png)

<span data-ttu-id="d066f-148">Non si dispone dell'autorizzazione ad aprire questa applicazione in Analytics.</span><span class="sxs-lookup"><span data-stu-id="d066f-148">You don't have permission to open this application in Analytics.</span></span>

* <span data-ttu-id="d066f-149">Se il collegamento è stato fornito da un altro utente,</span><span class="sxs-lookup"><span data-stu-id="d066f-149">Did you get the link from someone else?</span></span> <span data-ttu-id="d066f-150">Chiedere la conferma che l'utente destinatario sia un [lettore o collaboratore di questo gruppo di risorse](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="d066f-150">Ask them to make sure you are in the [readers or contributors for this resource group](app-insights-resources-roles-access-control.md).</span></span>
* <span data-ttu-id="d066f-151">Se il collegamento è stato salvato con credenziali diverse,</span><span class="sxs-lookup"><span data-stu-id="d066f-151">Did you save the link using different credentials?</span></span> <span data-ttu-id="d066f-152">Aprire il [portale di Azure](https://portal.azure.com), disconnettersi e riprovare a usare questo collegamento, inserendo le credenziali corrette.</span><span class="sxs-lookup"><span data-stu-id="d066f-152">Open the [Azure portal](https://portal.azure.com), sign out, and then try this link again, providing the correct credentials.</span></span>

## <span data-ttu-id="d066f-153"><a name="html-storage"></a>403 ... HTML5 Storage</span><span class="sxs-lookup"><span data-stu-id="d066f-153"><a name="html-storage"></a>403 ... HTML5 Storage</span></span>
<span data-ttu-id="d066f-154">Il portale utilizza HTML5 localStorage e sessionStorage.</span><span class="sxs-lookup"><span data-stu-id="d066f-154">Our portal uses HTML5 localStorage and sessionStorage.</span></span>

* <span data-ttu-id="d066f-155">Chrome: Impostazioni, Privacy, Impostazioni contenuti.</span><span class="sxs-lookup"><span data-stu-id="d066f-155">Chrome: Settings, privacy, content settings.</span></span>
* <span data-ttu-id="d066f-156">Internet Explorer: Opzioni Internet, scheda Avanzate, Sicurezza, Abilita archiviazione DOM</span><span class="sxs-lookup"><span data-stu-id="d066f-156">Internet Explorer: Internet Options, Advanced tab, Security, Enable DOM Storage</span></span>

![403 ... try to enable HTML5 storage](./media/app-insights-analytics-troubleshooting/060.png)

## <span data-ttu-id="d066f-158"><a name="e-g"></a>404 ... Sottoscrizione non trovata</span><span class="sxs-lookup"><span data-stu-id="d066f-158"><a name="e-g"></a>404 ... Subscription not found</span></span>
![404 ... Sottoscrizione non trovata](./media/app-insights-analytics-troubleshooting/070.png)

<span data-ttu-id="d066f-160">L'URL non è valido.</span><span class="sxs-lookup"><span data-stu-id="d066f-160">The URL is invalid.</span></span> 

* <span data-ttu-id="d066f-161">Aprire la risorsa dell'app nel [portale di Application Insights](https://portal.azure.com),</span><span class="sxs-lookup"><span data-stu-id="d066f-161">Open the app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="d066f-162">quindi utilizzare il pulsante di analisi.</span><span class="sxs-lookup"><span data-stu-id="d066f-162">Then use the Analytics button.</span></span>

## <span data-ttu-id="d066f-163"><a name="e-h"></a>404 ... la pagina non esiste</span><span class="sxs-lookup"><span data-stu-id="d066f-163"><a name="e-h"></a>404 ... page doesn't exist</span></span>
![404 ... Page does not exist](./media/app-insights-analytics-troubleshooting/080.png)

<span data-ttu-id="d066f-165">L'URL non è valido.</span><span class="sxs-lookup"><span data-stu-id="d066f-165">The URL is invalid.</span></span>

* <span data-ttu-id="d066f-166">Aprire la risorsa dell'app nel [portale di Application Insights](https://portal.azure.com),</span><span class="sxs-lookup"><span data-stu-id="d066f-166">Open the app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="d066f-167">quindi utilizzare il pulsante di analisi.</span><span class="sxs-lookup"><span data-stu-id="d066f-167">Then use the Analytics button.</span></span>

## <span data-ttu-id="d066f-168"><a name="cookies"></a>Abilitare i cookie di terze parti</span><span class="sxs-lookup"><span data-stu-id="d066f-168"><a name="cookies"></a>Enable third-party cookies</span></span>
  <span data-ttu-id="d066f-169">Vedere [come disabilitare il cookie di terze parti](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), tenendo conto che in questo caso è necessario **abilitarli** .</span><span class="sxs-lookup"><span data-stu-id="d066f-169">See [how to disable third party cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), but notice we need to **enable** them.</span></span>


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

