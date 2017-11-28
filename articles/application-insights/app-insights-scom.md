---
title: Integrazione di SCOM con Application Insights | Documentazione Microsoft
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
ms.openlocfilehash: 9c205465981fabdbb696cdc44f765532bbb992b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a><span data-ttu-id="e8430-104">Application Performance Monitoring con Application Insights per SCOM</span><span class="sxs-lookup"><span data-stu-id="e8430-104">Application Performance Monitoring using Application Insights for SCOM</span></span>
<span data-ttu-id="e8430-105">Se si usa System Center Operations Manager (SCOM) per gestire i server, è possibile monitorare le prestazioni e diagnosticare problemi di prestazioni con [Azure Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="e8430-105">If you use System Center Operations Manager (SCOM) to manage your servers, you can monitor performance and diagnose performance issues with the help of [Azure Application Insights](app-insights-asp-net.md).</span></span> <span data-ttu-id="e8430-106">Application Insights monitora le richieste in ingresso dell'applicazione Web, le chiamate REST e SQL in uscita, le eccezioni e le tracce dei log.</span><span class="sxs-lookup"><span data-stu-id="e8430-106">Application Insights monitors your web application's incoming requests, outgoing REST and SQL calls, exceptions, and log traces.</span></span> <span data-ttu-id="e8430-107">Fornisce i dashboard con grafici delle metriche e avvisi intelligenti, nonché funzionalità di ricerca diagnostica avanzate e query analitiche di questi dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="e8430-107">It provides dashboards with metric charts and smart alerts, as well as powerful diagnostic search and analytical queries over this telemetry.</span></span> 

<span data-ttu-id="e8430-108">È possibile attivare il monitoraggio di Application Insights tramite un Management Pack di SCOM.</span><span class="sxs-lookup"><span data-stu-id="e8430-108">You can switch on Application Insights monitoring by using an SCOM management pack.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="e8430-109">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="e8430-109">Before you start</span></span>
<span data-ttu-id="e8430-110">Si presuppone quanto segue:</span><span class="sxs-lookup"><span data-stu-id="e8430-110">We assume:</span></span>

* <span data-ttu-id="e8430-111">Si ha familiarità con SCOM e si usa SCOM 2012 R2 o 2016 per gestire i server Web IIS.</span><span class="sxs-lookup"><span data-stu-id="e8430-111">You're familiar with SCOM, and that you use SCOM 2012 R2 or 2016 to manage your IIS web servers.</span></span>
* <span data-ttu-id="e8430-112">È già stata installata nei server un'applicazione Web che si vuole monitorare con Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e8430-112">You have already installed on your servers a web application that you want to monitor with Application Insights.</span></span>
* <span data-ttu-id="e8430-113">La versione de framework applicazione è .NET 4.5 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="e8430-113">App framework version is .NET 4.5 or later.</span></span>
* <span data-ttu-id="e8430-114">Si ha accesso a una sottoscrizione in [Microsoft Azure](https://azure.com) e si può accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e8430-114">You have access to a subscription in [Microsoft Azure](https://azure.com) and can sign in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e8430-115">Se l'organizzazione ha una sottoscrizione, è possibile aggiungervi il proprio account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e8430-115">Your organization may have a subscription, and can add your Microsoft account to it.</span></span>

<span data-ttu-id="e8430-116">Il team di sviluppo può incorporare [Application Insights SDK](app-insights-asp-net.md) nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="e8430-116">(The development team might build the [Application Insights SDK](app-insights-asp-net.md) into the web app.</span></span> <span data-ttu-id="e8430-117">La strumentazione in fase di compilazione offre una maggiore flessibilità per la scrittura di dati di telemetria personalizzati.</span><span class="sxs-lookup"><span data-stu-id="e8430-117">This build-time instrumentation gives them greater flexibility in writing custom telemetry.</span></span> <span data-ttu-id="e8430-118">Se tuttavia questo aspetto non è significativo, è possibile seguire i passaggi descritti di seguito con o senza l'SDK incorporato.</span><span class="sxs-lookup"><span data-stu-id="e8430-118">However, it doesn't matter: you can follow the steps described here either with or without the SDK built in.)</span></span>

## <a name="one-time-install-application-insights-management-pack"></a><span data-ttu-id="e8430-119">(Una sola volta) Installare Management Pack per Application Insights</span><span class="sxs-lookup"><span data-stu-id="e8430-119">(One time) Install Application Insights management pack</span></span>
<span data-ttu-id="e8430-120">Nel computer in cui è in esecuzione Operations Manager seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e8430-120">On the machine where you run Operations Manager:</span></span>

1. <span data-ttu-id="e8430-121">Disinstallare eventuali versioni precedenti del management pack:</span><span class="sxs-lookup"><span data-stu-id="e8430-121">Uninstall any old version of the management pack:</span></span>
   1. <span data-ttu-id="e8430-122">In Operations Manager aprire Amministrazione, Management Pack.</span><span class="sxs-lookup"><span data-stu-id="e8430-122">In Operations Manager, open Administration, Management Packs.</span></span> 
   2. <span data-ttu-id="e8430-123">Eliminare la versione precedente.</span><span class="sxs-lookup"><span data-stu-id="e8430-123">Delete the old version.</span></span>
2. <span data-ttu-id="e8430-124">Scaricare e installare il management pack dal catalogo.</span><span class="sxs-lookup"><span data-stu-id="e8430-124">Download and install the management pack from the catalog.</span></span>
3. <span data-ttu-id="e8430-125">Riavviare Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="e8430-125">Restart Operations Manager.</span></span>

## <a name="create-a-management-pack"></a><span data-ttu-id="e8430-126">Creare un management pack</span><span class="sxs-lookup"><span data-stu-id="e8430-126">Create a management pack</span></span>
1. <span data-ttu-id="e8430-127">In Operations Manager aprire **Creazione**, **.NET... con Application Insights**, **Aggiunta guidata monitoraggio** e scegliere nuovamente **.NET... con Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="e8430-127">In Operations Manager, open **Authoring**, **.NET...with Application Insights**, **Add Monitoring Wizard**, and again choose **.NET...with Application Insights**.</span></span>
   
    ![](./media/app-insights-scom/020.png)
2. <span data-ttu-id="e8430-128">Assegnare un nome alla configurazione in base all'app.</span><span class="sxs-lookup"><span data-stu-id="e8430-128">Name the configuration after your app.</span></span> <span data-ttu-id="e8430-129">È necessario instrumentare un'applicazione alla volta.</span><span class="sxs-lookup"><span data-stu-id="e8430-129">(You have to instrument one app at a time.)</span></span>
   
    ![](./media/app-insights-scom/030.png)
3. <span data-ttu-id="e8430-130">Nella stessa pagina della procedura guidata, creare un nuovo management pack o selezionarne uno creato in precedenza per Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e8430-130">On the same wizard page, either create a new management pack, or select a pack that you created for Application Insights earlier.</span></span>
   
     <span data-ttu-id="e8430-131">[Management Pack](https://technet.microsoft.com/library/cc974491.aspx) per Application Insights è un modello da cui si crea un'istanza.</span><span class="sxs-lookup"><span data-stu-id="e8430-131">(The Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is a template, from which you create an instance.</span></span> <span data-ttu-id="e8430-132">È possibile riutilizzare la stessa istanza in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="e8430-132">You can reuse the same instance later.)</span></span>

    ![Nella scheda Proprietà generali, digitare il nome dell'app.](./media/app-insights-scom/040.png)

1. <span data-ttu-id="e8430-136">Scegliere un'app da monitorare.</span><span class="sxs-lookup"><span data-stu-id="e8430-136">Choose one app that you want to monitor.</span></span> <span data-ttu-id="e8430-137">La funzionalità di ricerca esegue la ricerca nelle app installate nei server.</span><span class="sxs-lookup"><span data-stu-id="e8430-137">The search feature searches among apps installed on your servers.</span></span>
   
    ![Nella scheda delle app da monitorare fare clic su Aggiungi, digitare parte del nome dell'app, fare clic su Cerca, scegliere l'app e quindi Aggiungi, OK.](./media/app-insights-scom/050.png)
   
    <span data-ttu-id="e8430-139">Il campo facoltativo Ambito monitoraggio può essere usato per specificare un subset di server, se non si vuole monitorare l'app in tutti i server.</span><span class="sxs-lookup"><span data-stu-id="e8430-139">The optional Monitoring scope field can be used to specify a subset of your servers, if you don't want to monitor the app in all servers.</span></span>
2. <span data-ttu-id="e8430-140">Nella pagina successiva della procedura guidata, è necessario fornire prima di tutto le credenziali per accedere a Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e8430-140">On the next wizard page, you must first provide your credentials to sign in to Microsoft Azure.</span></span>
   
    <span data-ttu-id="e8430-141">In questa pagina scegliere la risorsa di Application Insights in cui analizzare e visualizzare i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="e8430-141">On this page, you choose the Application Insights resource where you want the telemetry data to be analyzed and displayed.</span></span> 
   
   * <span data-ttu-id="e8430-142">Se l'applicazione è stata configurata per Application Insights durante lo sviluppo, selezionare la relativa risorsa esistente.</span><span class="sxs-lookup"><span data-stu-id="e8430-142">If the application was configured for Application Insights during development, select its existing resource.</span></span>
   * <span data-ttu-id="e8430-143">In caso contrario, creare una nuova risorsa denominata in base all'app.</span><span class="sxs-lookup"><span data-stu-id="e8430-143">Otherwise, create a new resource named for the app.</span></span> <span data-ttu-id="e8430-144">Se sono presenti altre app componenti dello stesso sistema, inserirle nello stesso gruppo di risorse, per gestire più facilmente l'accesso ai dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="e8430-144">If there are other apps that are components of the same system, put them in the same resource group, to make access to the telemetry easier to manage.</span></span>
     
     <span data-ttu-id="e8430-145">Queste impostazioni possono essere modificate in seguito.</span><span class="sxs-lookup"><span data-stu-id="e8430-145">You can change these settings later.</span></span>
     
     ![Nella scheda Impostazioni di Application Insights fare clic su 'accedi' e fornire le credenziali dell'account Microsoft per Azure.](./media/app-insights-scom/060.png)
3. <span data-ttu-id="e8430-148">Completare la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="e8430-148">Complete the wizard.</span></span>
   
    ![Fare clic su Crea](./media/app-insights-scom/070.png)

<span data-ttu-id="e8430-150">Ripetere questa procedura per ogni app da monitorare.</span><span class="sxs-lookup"><span data-stu-id="e8430-150">Repeat this procedure for each app that you want to monitor.</span></span>

<span data-ttu-id="e8430-151">Se è necessario modificare le impostazioni in un secondo momento, riaprire le proprietà del monitoraggio dalla finestra di creazione.</span><span class="sxs-lookup"><span data-stu-id="e8430-151">If you need to change settings later, re-open the properties of the monitor from the Authoring window.</span></span>

![Nella finestra di creazione selezionare Monitoraggio delle prestazioni delle applicazioni .NET con Application Insights, selezionare la funzionalità di monitoraggio e fare clic su Proprietà.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a><span data-ttu-id="e8430-153">Verificare il monitoraggio</span><span class="sxs-lookup"><span data-stu-id="e8430-153">Verify monitoring</span></span>
<span data-ttu-id="e8430-154">La funzionalità di monitoraggio installata cerca l'app in ogni server.</span><span class="sxs-lookup"><span data-stu-id="e8430-154">The monitor that you have installed searches for your app on every server.</span></span> <span data-ttu-id="e8430-155">Nel server in cui trova l'app configura Application Insights Status Monitor per monitorare l'app.</span><span class="sxs-lookup"><span data-stu-id="e8430-155">Where it finds the app, it configures Application Insights Status Monitor to monitor the app.</span></span> <span data-ttu-id="e8430-156">Se necessario, prima installa Status Monitor nel server.</span><span class="sxs-lookup"><span data-stu-id="e8430-156">If necessary, it first installs Status Monitor on the server.</span></span>

<span data-ttu-id="e8430-157">È possibile verificare quali istanze dell'app sono state trovate:</span><span class="sxs-lookup"><span data-stu-id="e8430-157">You can verify which instances of the app it has found:</span></span>

![In Monitoraggio aprire Application Insights](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a><span data-ttu-id="e8430-159">Visualizzare i dati di telemetria in Application Insights</span><span class="sxs-lookup"><span data-stu-id="e8430-159">View telemetry in Application Insights</span></span>
<span data-ttu-id="e8430-160">Nel [portale di Azure](https://portal.azure.com)individuare la risorsa per l'app.</span><span class="sxs-lookup"><span data-stu-id="e8430-160">In the [Azure portal](https://portal.azure.com), browse to the resource for your app.</span></span> <span data-ttu-id="e8430-161">Nell'app è possibile [visualizzare grafici che mostrano i dati di telemetria](app-insights-dashboards.md) .</span><span class="sxs-lookup"><span data-stu-id="e8430-161">You [see charts showing telemetry](app-insights-dashboards.md) from your app.</span></span> <span data-ttu-id="e8430-162">Se non vengono visualizzati nella pagina principale, fare clic su Flusso metriche attive.</span><span class="sxs-lookup"><span data-stu-id="e8430-162">(If it hasn't shown up on the main page yet, click Live Metrics Stream.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8430-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e8430-163">Next steps</span></span>
* <span data-ttu-id="e8430-164">[Configurare un dashboard](app-insights-dashboards.md) per riunire i grafici più importanti relativi al monitoraggio di questa e altre app.</span><span class="sxs-lookup"><span data-stu-id="e8430-164">[Set up a dashboard](app-insights-dashboards.md) to bring together the most important charts monitoring this and other apps.</span></span>
* [<span data-ttu-id="e8430-165">Informazioni sulle metriche</span><span class="sxs-lookup"><span data-stu-id="e8430-165">Learn about metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="e8430-166">Impostare gli avvisi in Application Insights</span><span class="sxs-lookup"><span data-stu-id="e8430-166">Set up alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="e8430-167">Rilevare, valutare e diagnosticare con Application Insights</span><span class="sxs-lookup"><span data-stu-id="e8430-167">Diagnosing performance issues</span></span>](app-insights-detect-triage-diagnose.md)
* [<span data-ttu-id="e8430-168">Query di Analisi avanzate</span><span class="sxs-lookup"><span data-stu-id="e8430-168">Powerful Analytics queries</span></span>](app-insights-analytics.md)
* [<span data-ttu-id="e8430-169">Test Web di disponibilità</span><span class="sxs-lookup"><span data-stu-id="e8430-169">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)

