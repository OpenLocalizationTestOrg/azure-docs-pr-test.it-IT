---
title: Microsoft Dynamics CRM e Azure Application Insights | Documentazione Microsoft
description: Ottenere i dati di telemetria da Microsoft Dynamics CRM Online tramite Application Insights. Procedura dettagliate relative a installazione, recupero dei dati, visualizzazione ed esportazione.
services: application-insights
documentationcenter: 
author: mazharmicrosoft
manager: carmonm
ms.assetid: 04c66338-687e-49e5-9975-be935f98f156
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: bwren
ms.openlocfilehash: a9593d5f198e05db80451a599428a296ed02e781
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a><span data-ttu-id="70f5d-104">Procedura dettagliata: Abilitazione della telemetria per Microsoft Dynamics CRM Online tramite Application Insights</span><span class="sxs-lookup"><span data-stu-id="70f5d-104">Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights</span></span>
<span data-ttu-id="70f5d-105">Questo articolo descrive come ottenere i dati di telemetria da [Microsoft Dynamics CRM Online](https://www.dynamics.com/) usando [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="70f5d-105">This article shows you how to get telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span></span> <span data-ttu-id="70f5d-106">Verrà illustrato il processo completo che prevede l'aggiunta di uno script di Application Insights all'applicazione, l'acquisizione dei dati e la visualizzazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="70f5d-106">We’ll walk through the complete process of adding Application Insights script to your application, capturing data, and data visualization.</span></span>

> [!NOTE]
> <span data-ttu-id="70f5d-107">[Esplorare la soluzione di esempio](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="70f5d-107">[Browse the sample solution](https://dynamicsandappinsights.codeplex.com/).</span></span>
> 
> 

## <a name="add-application-insights-to-new-or-existing-crm-online-instance"></a><span data-ttu-id="70f5d-108">Aggiungere Application Insights a un'istanza di CRM Online nuova o esistente</span><span class="sxs-lookup"><span data-stu-id="70f5d-108">Add Application Insights to new or existing CRM Online instance</span></span>
<span data-ttu-id="70f5d-109">Per monitorare l'applicazione, è necessario aggiungere un SDK di Application Insights all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="70f5d-109">To monitor your application, you add an Application Insights SDK to your application.</span></span> <span data-ttu-id="70f5d-110">L'SDK invia dati di telemetria al [portale di Application Insights](https://portal.azure.com), dove è possibile usare potenti strumenti di analisi e diagnostica o esportare i dati nell'archivio.</span><span class="sxs-lookup"><span data-stu-id="70f5d-110">The SDK sends telemetry to the [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export the data to storage.</span></span>

### <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="70f5d-111">Creare una risorsa di Application Insights in Azure</span><span class="sxs-lookup"><span data-stu-id="70f5d-111">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="70f5d-112">Ottenere un [account in Microsoft Azure](http://azure.com/pricing).</span><span class="sxs-lookup"><span data-stu-id="70f5d-112">Get [an account in Microsoft Azure](http://azure.com/pricing).</span></span> 
2. <span data-ttu-id="70f5d-113">Accedere al [portale di Azure](https://portal.azure.com) e aggiungere una nuova risorsa di Application Insights,</span><span class="sxs-lookup"><span data-stu-id="70f5d-113">Sign into the [Azure portal](https://portal.azure.com) and add a new Application Insights resource.</span></span> <span data-ttu-id="70f5d-114">in cui i dati verranno elaborati e visualizzati.</span><span class="sxs-lookup"><span data-stu-id="70f5d-114">This is where your data will be processed and displayed.</span></span>
   
    ![Clic su +, Servizi per gli sviluppatori, Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    <span data-ttu-id="70f5d-116">Scegliere ASP.NET come tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="70f5d-116">Choose ASP.NET as the application type.</span></span>
3. <span data-ttu-id="70f5d-117">Aprire la pagina introduttiva e "Monitoraggio e diagnosi dell'applicazione lato client".</span><span class="sxs-lookup"><span data-stu-id="70f5d-117">Open the Getting Started page and open "Monitor and diagnose client side".</span></span>
   
    ![Frammento di codice per l'inserimento nella pagina Web](./media/app-insights-sample-mscrm/03.png)

<span data-ttu-id="70f5d-119">**Mantenere aperta la pagina del codice** mentre si esegue il passaggio successivo in un'altra finestra del browser.</span><span class="sxs-lookup"><span data-stu-id="70f5d-119">**Keep the code page open** while you do the next step in another browser window.</span></span> <span data-ttu-id="70f5d-120">È necessario tenere il codice a portata di mano.</span><span class="sxs-lookup"><span data-stu-id="70f5d-120">You'll need the code soon.</span></span> 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a><span data-ttu-id="70f5d-121">Creare una risorsa Web JavaScript in Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="70f5d-121">Create a JavaScript web resource in Microsoft Dynamics CRM</span></span>
1. <span data-ttu-id="70f5d-122">Aprire l'istanza di CRM Online ed eseguire l'accesso con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="70f5d-122">Open your CRM Online instance and login with administrator privileges.</span></span>
2. <span data-ttu-id="70f5d-123">In Microsoft Dynamics CRM fare clic su Impostazioni, su Personalizzazioni e su Personalizza il Sistema</span><span class="sxs-lookup"><span data-stu-id="70f5d-123">Open Microsoft Dynamics CRM Settings, Customizations, Customize the System</span></span>
   
    ![Impostazioni di Microsoft Dynamics CRM](./media/app-insights-sample-mscrm/04.png)
   
    ![Impostazioni > Personalizzazioni](./media/app-insights-sample-mscrm/05.png)

    ![Personalizzare l'opzione del sistema](./media/app-insights-sample-mscrm/06.png)

1. <span data-ttu-id="70f5d-127">Creare una risorsa JavaScript.</span><span class="sxs-lookup"><span data-stu-id="70f5d-127">Create a JavaScript resource.</span></span>
   
    ![Finestra di dialogo Nuova risorsa Web](./media/app-insights-sample-mscrm/07.png)
   
    <span data-ttu-id="70f5d-129">Assegnarle un nome, selezionare **Script (JScript)** e aprire l'editor di testo.</span><span class="sxs-lookup"><span data-stu-id="70f5d-129">Give it a name, select **Script (JScript)** and open the text editor.</span></span>
   
    ![Aprire l'editor di testo](./media/app-insights-sample-mscrm/08.png)
2. <span data-ttu-id="70f5d-131">Copiare il codice da Application Insights.</span><span class="sxs-lookup"><span data-stu-id="70f5d-131">Copy the code from Application Insights.</span></span> <span data-ttu-id="70f5d-132">Durante la copia assicurarsi di ignorare i tag di script.</span><span class="sxs-lookup"><span data-stu-id="70f5d-132">While copying make sure to ignore script tags.</span></span> <span data-ttu-id="70f5d-133">Fare riferimento alla schermata illustrata di seguito:</span><span class="sxs-lookup"><span data-stu-id="70f5d-133">Refer below screenshot:</span></span>
   
    ![Impostare la chiave di strumentazione](./media/app-insights-sample-mscrm/09.png)
   
    <span data-ttu-id="70f5d-135">Il codice contiene la chiave di strumentazione che identifica la risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="70f5d-135">The code includes the instrumentation key that identifies your Application insights resource.</span></span>
3. <span data-ttu-id="70f5d-136">Fare clic su Salva e quindi su Pubblica.</span><span class="sxs-lookup"><span data-stu-id="70f5d-136">Save and publish.</span></span>
   
    ![Fare clic su Salva e quindi su Pubblica](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a><span data-ttu-id="70f5d-138">Form strumentazione</span><span class="sxs-lookup"><span data-stu-id="70f5d-138">Instrument Forms</span></span>
1. <span data-ttu-id="70f5d-139">In Microsoft CRM Online aprire il form Account</span><span class="sxs-lookup"><span data-stu-id="70f5d-139">In Microsoft CRM Online, open the Account form</span></span>
   
    ![Modulo account](./media/app-insights-sample-mscrm/11.png)
2. <span data-ttu-id="70f5d-141">Aprire il form Proprietà</span><span class="sxs-lookup"><span data-stu-id="70f5d-141">Open the form Properties</span></span>
   
    ![Proprietà del modulo](./media/app-insights-sample-mscrm/12.png)
3. <span data-ttu-id="70f5d-143">Aggiungere la risorsa Web JavaScript creata in precedenza</span><span class="sxs-lookup"><span data-stu-id="70f5d-143">Add the JavaScript web resource that you created</span></span>
   
    ![Menu Aggiungi](./media/app-insights-sample-mscrm/13.png)
   
    ![Aggiungere la risorsa Web](./media/app-insights-sample-mscrm/14.png)
4. <span data-ttu-id="70f5d-146">Salvare e pubblicare le personalizzazioni dei form.</span><span class="sxs-lookup"><span data-stu-id="70f5d-146">Save and publish your form customizations.</span></span>

## <a name="metrics-captured"></a><span data-ttu-id="70f5d-147">Metriche acquisite</span><span class="sxs-lookup"><span data-stu-id="70f5d-147">Metrics captured</span></span>
<span data-ttu-id="70f5d-148">È stata configurata l'acquisizione dei dati telemetria per il form.</span><span class="sxs-lookup"><span data-stu-id="70f5d-148">You have now set up telemetry capture for the form.</span></span> <span data-ttu-id="70f5d-149">A ogni utilizzo, i dati verranno inviati alla risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="70f5d-149">Whenever it is used, data will be sent to your Application Insights resource.</span></span>

<span data-ttu-id="70f5d-150">Ecco alcuni esempi dei dati che verranno visualizzati.</span><span class="sxs-lookup"><span data-stu-id="70f5d-150">Here are samples of the data that you'll see.</span></span>

#### <a name="application-health"></a><span data-ttu-id="70f5d-151">Integrità dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="70f5d-151">Application health</span></span>
![Tempo di caricamento pagina di esempio](./media/app-insights-sample-mscrm/15.png)

![Grafico delle visualizzazioni pagina di esempio](./media/app-insights-sample-mscrm/16.png)

<span data-ttu-id="70f5d-154">Eccezioni del browser:</span><span class="sxs-lookup"><span data-stu-id="70f5d-154">Browser exceptions:</span></span>

![Grafico delle eccezioni del browser](./media/app-insights-sample-mscrm/17.png)

<span data-ttu-id="70f5d-156">Fare clic sul grafico per ottenere altri dettagli:</span><span class="sxs-lookup"><span data-stu-id="70f5d-156">Click the chart to get more detail:</span></span>

![Elenco delle eccezioni](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a><span data-ttu-id="70f5d-158">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="70f5d-158">Usage</span></span>
![Utenti, sessioni e visualizzazioni pagine](./media/app-insights-sample-mscrm/19.png)

![Grafici della sessione](./media/app-insights-sample-mscrm/20.png)

![Versioni del browser](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a><span data-ttu-id="70f5d-162">Browser</span><span class="sxs-lookup"><span data-stu-id="70f5d-162">Browsers</span></span>
![Scomposizione del tempo di caricamento della pagina](./media/app-insights-sample-mscrm/22.png)

![Conteggio delle sessioni in base alla versione del browser](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a><span data-ttu-id="70f5d-165">Georilevazione</span><span class="sxs-lookup"><span data-stu-id="70f5d-165">Geolocation</span></span>
![Conteggio delle sessioni in base al paese](./media/app-insights-sample-mscrm/24.png)

![Sessioni e utenti in base al paese](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a><span data-ttu-id="70f5d-168">Richieste visualizzazione pagina interna</span><span class="sxs-lookup"><span data-stu-id="70f5d-168">Inside page view request</span></span>
![Riepilogo della visualizzazione pagina](./media/app-insights-sample-mscrm/26.png)

![Cercare negli eventi della visualizzazione pagina](./media/app-insights-sample-mscrm/27.png)

![Visualizzazioni pagina simili](./media/app-insights-sample-mscrm/28.png)

![Proprietà delle visualizzazioni di pagina](./media/app-insights-sample-mscrm/29.png)

![Pagine per sessione](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a><span data-ttu-id="70f5d-174">Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="70f5d-174">Sample code</span></span>
<span data-ttu-id="70f5d-175">[Sfoglia il codice di esempio](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="70f5d-175">[Browse the sample code](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="power-bi"></a><span data-ttu-id="70f5d-176">Power BI</span><span class="sxs-lookup"><span data-stu-id="70f5d-176">Power BI</span></span>
<span data-ttu-id="70f5d-177">Per eseguire analisi più approfondite, è possibile [esportare i dati in Microsoft Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="70f5d-177">You can do even deeper analysis if you [export the data to Microsoft Power BI](app-insights-export-power-bi.md).</span></span>

## <a name="sample-microsoft-dynamics-crm-solution"></a><span data-ttu-id="70f5d-178">Soluzione di esempio Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="70f5d-178">Sample Microsoft Dynamics CRM Solution</span></span>
<span data-ttu-id="70f5d-179">[Ecco la soluzione di esempio implementata in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="70f5d-179">[Here is the sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="learn-more"></a><span data-ttu-id="70f5d-180">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="70f5d-180">Learn more</span></span>
* [<span data-ttu-id="70f5d-181">Informazioni su Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="70f5d-181">What is Application Insights?</span></span>](app-insights-overview.md)
* [<span data-ttu-id="70f5d-182">Application Insights per pagine Web</span><span class="sxs-lookup"><span data-stu-id="70f5d-182">Application Insights for web pages</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="70f5d-183">Altri esempi e procedure dettagliate</span><span class="sxs-lookup"><span data-stu-id="70f5d-183">More samples and walkthroughs</span></span>](app-insights-code-samples.md)
