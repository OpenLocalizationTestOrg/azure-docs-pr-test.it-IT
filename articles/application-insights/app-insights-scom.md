---
title: integrazione di aaaSCOM con Application Insights | Documenti Microsoft
description: Gli utenti di SCOM possono monitorare le prestazioni e diagnosticare i problemi con Application Insights. Dashboard completi, avvisi intelligenti, potenti strumenti di diagnostica e query di analisi.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: bwren
ms.openlocfilehash: ee9ad462610fd916098a0e292c5bd44f2a873c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a><span data-ttu-id="29e0d-104">Application Performance Monitoring con Application Insights per SCOM</span><span class="sxs-lookup"><span data-stu-id="29e0d-104">Application Performance Monitoring using Application Insights for SCOM</span></span>
<span data-ttu-id="29e0d-105">Se si utilizzano System Center Operations Manager (SCOM) toomanage i server, è possibile monitorare le prestazioni e diagnosticare i problemi di prestazioni con l'aiuto di hello di [Azure Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="29e0d-105">If you use System Center Operations Manager (SCOM) toomanage your servers, you can monitor performance and diagnose performance issues with hello help of [Azure Application Insights](app-insights-asp-net.md).</span></span> <span data-ttu-id="29e0d-106">Application Insights monitora le richieste in ingresso dell'applicazione Web, le chiamate REST e SQL in uscita, le eccezioni e le tracce dei log.</span><span class="sxs-lookup"><span data-stu-id="29e0d-106">Application Insights monitors your web application's incoming requests, outgoing REST and SQL calls, exceptions, and log traces.</span></span> <span data-ttu-id="29e0d-107">Fornisce i dashboard con grafici delle metriche e avvisi intelligenti, nonché funzionalità di ricerca diagnostica avanzate e query analitiche di questi dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="29e0d-107">It provides dashboards with metric charts and smart alerts, as well as powerful diagnostic search and analytical queries over this telemetry.</span></span> 

<span data-ttu-id="29e0d-108">È possibile attivare il monitoraggio di Application Insights tramite un Management Pack di SCOM.</span><span class="sxs-lookup"><span data-stu-id="29e0d-108">You can switch on Application Insights monitoring by using an SCOM management pack.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="29e0d-109">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="29e0d-109">Before you start</span></span>
<span data-ttu-id="29e0d-110">Si presuppone quanto segue:</span><span class="sxs-lookup"><span data-stu-id="29e0d-110">We assume:</span></span>

* <span data-ttu-id="29e0d-111">Si ha familiarità con SCOM e usare SCOM 2012 R2 o 2016 toomanage di IIS server web.</span><span class="sxs-lookup"><span data-stu-id="29e0d-111">You're familiar with SCOM, and that you use SCOM 2012 R2 or 2016 toomanage your IIS web servers.</span></span>
* <span data-ttu-id="29e0d-112">Già installati nei server di un'applicazione web che si desidera toomonitor con Application Insights.</span><span class="sxs-lookup"><span data-stu-id="29e0d-112">You have already installed on your servers a web application that you want toomonitor with Application Insights.</span></span>
* <span data-ttu-id="29e0d-113">La versione de framework applicazione è .NET 4.5 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="29e0d-113">App framework version is .NET 4.5 or later.</span></span>
* <span data-ttu-id="29e0d-114">Si dispone di accesso tooa sottoscrizione [Microsoft Azure](https://azure.com) e può firmare in toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="29e0d-114">You have access tooa subscription in [Microsoft Azure](https://azure.com) and can sign in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="29e0d-115">L'organizzazione dispone di una sottoscrizione e può aggiungere la tooit account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="29e0d-115">Your organization may have a subscription, and can add your Microsoft account tooit.</span></span>

<span data-ttu-id="29e0d-116">(il team di sviluppo hello venga compilato hello [Application Insights SDK](app-insights-asp-net.md) in hello web app.</span><span class="sxs-lookup"><span data-stu-id="29e0d-116">(hello development team might build hello [Application Insights SDK](app-insights-asp-net.md) into hello web app.</span></span> <span data-ttu-id="29e0d-117">La strumentazione in fase di compilazione offre una maggiore flessibilità per la scrittura di dati di telemetria personalizzati.</span><span class="sxs-lookup"><span data-stu-id="29e0d-117">This build-time instrumentation gives them greater flexibility in writing custom telemetry.</span></span> <span data-ttu-id="29e0d-118">Tuttavia, non è importante: è possibile seguire i passaggi di hello descritti qui, con o senza hello SDK incorporata.)</span><span class="sxs-lookup"><span data-stu-id="29e0d-118">However, it doesn't matter: you can follow hello steps described here either with or without hello SDK built in.)</span></span>

## <a name="one-time-install-application-insights-management-pack"></a><span data-ttu-id="29e0d-119">(Una sola volta) Installare Management Pack per Application Insights</span><span class="sxs-lookup"><span data-stu-id="29e0d-119">(One time) Install Application Insights management pack</span></span>
<span data-ttu-id="29e0d-120">Nel computer di hello in cui si esegue Operations Manager:</span><span class="sxs-lookup"><span data-stu-id="29e0d-120">On hello machine where you run Operations Manager:</span></span>

1. <span data-ttu-id="29e0d-121">Disinstallare qualsiasi versione precedente del management pack di hello:</span><span class="sxs-lookup"><span data-stu-id="29e0d-121">Uninstall any old version of hello management pack:</span></span>
   1. <span data-ttu-id="29e0d-122">In Operations Manager aprire Amministrazione, Management Pack.</span><span class="sxs-lookup"><span data-stu-id="29e0d-122">In Operations Manager, open Administration, Management Packs.</span></span> 
   2. <span data-ttu-id="29e0d-123">Eliminare la versione precedente di hello.</span><span class="sxs-lookup"><span data-stu-id="29e0d-123">Delete hello old version.</span></span>
2. <span data-ttu-id="29e0d-124">Scaricare e installare hello management pack dal catalogo hello.</span><span class="sxs-lookup"><span data-stu-id="29e0d-124">Download and install hello management pack from hello catalog.</span></span>
3. <span data-ttu-id="29e0d-125">Riavviare Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="29e0d-125">Restart Operations Manager.</span></span>

## <a name="create-a-management-pack"></a><span data-ttu-id="29e0d-126">Creare un management pack</span><span class="sxs-lookup"><span data-stu-id="29e0d-126">Create a management pack</span></span>
1. <span data-ttu-id="29e0d-127">In Operations Manager aprire **Creazione**, **.NET... con Application Insights**, **Aggiunta guidata monitoraggio** e scegliere nuovamente **.NET... con Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="29e0d-127">In Operations Manager, open **Authoring**, **.NET...with Application Insights**, **Add Monitoring Wizard**, and again choose **.NET...with Application Insights**.</span></span>
   
    ![](./media/app-insights-scom/020.png)
2. <span data-ttu-id="29e0d-128">Configurazione del nome hello dopo l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="29e0d-128">Name hello configuration after your app.</span></span> <span data-ttu-id="29e0d-129">(Hai tooinstrument un'app alla volta.)</span><span class="sxs-lookup"><span data-stu-id="29e0d-129">(You have tooinstrument one app at a time.)</span></span>
   
    ![](./media/app-insights-scom/030.png)
3. <span data-ttu-id="29e0d-130">Hello nella stessa pagina della procedura guidata, creare un nuovo management pack o selezionare un pacchetto creato in precedenza per Application Insights.</span><span class="sxs-lookup"><span data-stu-id="29e0d-130">On hello same wizard page, either create a new management pack, or select a pack that you created for Application Insights earlier.</span></span>
   
     <span data-ttu-id="29e0d-131">(hello Application Insights [management pack di](https://technet.microsoft.com/library/cc974491.aspx) è un modello, da cui si crea un'istanza.</span><span class="sxs-lookup"><span data-stu-id="29e0d-131">(hello Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is a template, from which you create an instance.</span></span> <span data-ttu-id="29e0d-132">È possibile riutilizzare hello stessa istanza in un secondo momento.)</span><span class="sxs-lookup"><span data-stu-id="29e0d-132">You can reuse hello same instance later.)</span></span>

    ![Nella scheda proprietà generali di hello, digitare il nome di hello dell'applicazione hello.](./media/app-insights-scom/040.png)

1. <span data-ttu-id="29e0d-136">Scegliere un'app che si desidera toomonitor.</span><span class="sxs-lookup"><span data-stu-id="29e0d-136">Choose one app that you want toomonitor.</span></span> <span data-ttu-id="29e0d-137">funzionalità di ricerca Hello Cerca tra le app installate nel server.</span><span class="sxs-lookup"><span data-stu-id="29e0d-137">hello search feature searches among apps installed on your servers.</span></span>
   
    ![Nella scheda da tooMonitor, fare clic su Aggiungi, digitare parte del nome dell'applicazione hello, fare clic su Cerca, scegliere OK hello app, quindi scegliere Aggiungi,](./media/app-insights-scom/050.png)
   
    <span data-ttu-id="29e0d-139">Hello facoltativo monitoraggio ambito campo può essere utilizzato toospecify un sottoinsieme di server, se non si desidera app hello toomonitor in tutti i server.</span><span class="sxs-lookup"><span data-stu-id="29e0d-139">hello optional Monitoring scope field can be used toospecify a subset of your servers, if you don't want toomonitor hello app in all servers.</span></span>
2. <span data-ttu-id="29e0d-140">Nella pagina della procedura guidata Avanti hello, è necessario specificare innanzitutto toosign le credenziali in tooMicrosoft Azure.</span><span class="sxs-lookup"><span data-stu-id="29e0d-140">On hello next wizard page, you must first provide your credentials toosign in tooMicrosoft Azure.</span></span>
   
    <span data-ttu-id="29e0d-141">In questa pagina è scegliere una risorsa di Application Insights hello in cui si desidera hello toobe dati di telemetria analizzati e visualizzati.</span><span class="sxs-lookup"><span data-stu-id="29e0d-141">On this page, you choose hello Application Insights resource where you want hello telemetry data toobe analyzed and displayed.</span></span> 
   
   * <span data-ttu-id="29e0d-142">Se un'applicazione hello è stata configurata per Application Insights durante lo sviluppo, selezionare la risorsa esistente.</span><span class="sxs-lookup"><span data-stu-id="29e0d-142">If hello application was configured for Application Insights during development, select its existing resource.</span></span>
   * <span data-ttu-id="29e0d-143">In caso contrario, creare una nuova risorsa denominata per l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="29e0d-143">Otherwise, create a new resource named for hello app.</span></span> <span data-ttu-id="29e0d-144">Se sono presenti altre applicazioni che sono componenti di hello sistema stesso, inserirli in hello stesso gruppo di risorse, toomake accesso toohello telemetria più facile toomanage.</span><span class="sxs-lookup"><span data-stu-id="29e0d-144">If there are other apps that are components of hello same system, put them in hello same resource group, toomake access toohello telemetry easier toomanage.</span></span>
     
     <span data-ttu-id="29e0d-145">Queste impostazioni possono essere modificate in seguito.</span><span class="sxs-lookup"><span data-stu-id="29e0d-145">You can change these settings later.</span></span>
     
     ![Nella scheda Impostazioni di Application Insights fare clic su 'accedi' e fornire le credenziali dell'account Microsoft per Azure.](./media/app-insights-scom/060.png)
3. <span data-ttu-id="29e0d-148">Creazione guidata hello completo.</span><span class="sxs-lookup"><span data-stu-id="29e0d-148">Complete hello wizard.</span></span>
   
    ![Fare clic su Crea](./media/app-insights-scom/070.png)

<span data-ttu-id="29e0d-150">Ripetere questa procedura per ogni app che si desidera toomonitor.</span><span class="sxs-lookup"><span data-stu-id="29e0d-150">Repeat this procedure for each app that you want toomonitor.</span></span>

<span data-ttu-id="29e0d-151">Se è necessario toochange impostazioni in un secondo momento, è necessario aprire nuovamente proprietà hello del monitoraggio di hello dalla finestra di creazione e modifica di hello.</span><span class="sxs-lookup"><span data-stu-id="29e0d-151">If you need toochange settings later, re-open hello properties of hello monitor from hello Authoring window.</span></span>

![Nella finestra di creazione selezionare Monitoraggio delle prestazioni delle applicazioni .NET con Application Insights, selezionare la funzionalità di monitoraggio e fare clic su Proprietà.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a><span data-ttu-id="29e0d-153">Verificare il monitoraggio</span><span class="sxs-lookup"><span data-stu-id="29e0d-153">Verify monitoring</span></span>
<span data-ttu-id="29e0d-154">monitoraggio di Hello di avere installato Cerca l'app in ogni server.</span><span class="sxs-lookup"><span data-stu-id="29e0d-154">hello monitor that you have installed searches for your app on every server.</span></span> <span data-ttu-id="29e0d-155">In cui trova app hello, configura Application Insights Status Monitor toomonitor hello app.</span><span class="sxs-lookup"><span data-stu-id="29e0d-155">Where it finds hello app, it configures Application Insights Status Monitor toomonitor hello app.</span></span> <span data-ttu-id="29e0d-156">Se necessario, innanzitutto Status Monitor viene installato nel server di hello.</span><span class="sxs-lookup"><span data-stu-id="29e0d-156">If necessary, it first installs Status Monitor on hello server.</span></span>

<span data-ttu-id="29e0d-157">È possibile verificare quali istanze di applicazione hello che è stato individuato:</span><span class="sxs-lookup"><span data-stu-id="29e0d-157">You can verify which instances of hello app it has found:</span></span>

![In Monitoraggio aprire Application Insights](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a><span data-ttu-id="29e0d-159">Visualizzare i dati di telemetria in Application Insights</span><span class="sxs-lookup"><span data-stu-id="29e0d-159">View telemetry in Application Insights</span></span>
<span data-ttu-id="29e0d-160">In hello [portale di Azure](https://portal.azure.com), Sfoglia risorsa toohello per l'app.</span><span class="sxs-lookup"><span data-stu-id="29e0d-160">In hello [Azure portal](https://portal.azure.com), browse toohello resource for your app.</span></span> <span data-ttu-id="29e0d-161">Nell'app è possibile [visualizzare grafici che mostrano i dati di telemetria](app-insights-dashboards.md) .</span><span class="sxs-lookup"><span data-stu-id="29e0d-161">You [see charts showing telemetry](app-insights-dashboards.md) from your app.</span></span> <span data-ttu-id="29e0d-162">(Se non vengono visualizzate nella pagina principale di hello ancora, fare clic su flusso di metriche in tempo reale).</span><span class="sxs-lookup"><span data-stu-id="29e0d-162">(If it hasn't shown up on hello main page yet, click Live Metrics Stream.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="29e0d-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="29e0d-163">Next steps</span></span>
* <span data-ttu-id="29e0d-164">[Impostare un dashboard](app-insights-dashboards.md) grafici più importanti insieme hello toobring monitoraggio questa e altre app.</span><span class="sxs-lookup"><span data-stu-id="29e0d-164">[Set up a dashboard](app-insights-dashboards.md) toobring together hello most important charts monitoring this and other apps.</span></span>
* [<span data-ttu-id="29e0d-165">Informazioni sulle metriche</span><span class="sxs-lookup"><span data-stu-id="29e0d-165">Learn about metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="29e0d-166">Impostare gli avvisi in Application Insights</span><span class="sxs-lookup"><span data-stu-id="29e0d-166">Set up alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="29e0d-167">Rilevare, valutare e diagnosticare con Application Insights</span><span class="sxs-lookup"><span data-stu-id="29e0d-167">Diagnosing performance issues</span></span>](app-insights-detect-triage-diagnose.md)
* [<span data-ttu-id="29e0d-168">Query di Analisi avanzate</span><span class="sxs-lookup"><span data-stu-id="29e0d-168">Powerful Analytics queries</span></span>](app-insights-analytics.md)
* [<span data-ttu-id="29e0d-169">Test Web di disponibilità</span><span class="sxs-lookup"><span data-stu-id="29e0d-169">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)

