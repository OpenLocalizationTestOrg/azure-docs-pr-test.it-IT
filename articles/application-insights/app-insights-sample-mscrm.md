---
title: aaaMicrosoft Dynamics CRM e Azure Application Insights | Documenti Microsoft
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
ms.openlocfilehash: a39398060d6553fb18a26c101f085b7d87443636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a><span data-ttu-id="dff69-104">Procedura dettagliata: Abilitazione della telemetria per Microsoft Dynamics CRM Online tramite Application Insights</span><span class="sxs-lookup"><span data-stu-id="dff69-104">Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights</span></span>
<span data-ttu-id="dff69-105">In questo articolo illustra come i dati di telemetria tooget [Microsoft Dynamics CRM Online](https://www.dynamics.com/) utilizzando [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="dff69-105">This article shows you how tooget telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span></span> <span data-ttu-id="dff69-106">Verranno esaminati procedura completa di hello di aggiunta di Application Insights script tooyour applicazione, l'acquisizione di dati e visualizzazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="dff69-106">We’ll walk through hello complete process of adding Application Insights script tooyour application, capturing data, and data visualization.</span></span>

> [!NOTE]
> <span data-ttu-id="dff69-107">[Selezionare la soluzione di esempio hello](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="dff69-107">[Browse hello sample solution](https://dynamicsandappinsights.codeplex.com/).</span></span>
> 
> 

## <a name="add-application-insights-toonew-or-existing-crm-online-instance"></a><span data-ttu-id="dff69-108">Aggiungere Application Insights toonew o istanza esistente di CRM Online</span><span class="sxs-lookup"><span data-stu-id="dff69-108">Add Application Insights toonew or existing CRM Online instance</span></span>
<span data-ttu-id="dff69-109">toomonitor l'applicazione, si aggiunge un'applicazione tooyour Application Insights SDK.</span><span class="sxs-lookup"><span data-stu-id="dff69-109">toomonitor your application, you add an Application Insights SDK tooyour application.</span></span> <span data-ttu-id="dff69-110">Hello SDK invia dati di telemetria toohello [portale Application Insights](https://portal.azure.com), in cui è possibile utilizzare l'analisi potenti e strumenti di diagnostica o esportazione toostorage dati hello.</span><span class="sxs-lookup"><span data-stu-id="dff69-110">hello SDK sends telemetry toohello [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export hello data toostorage.</span></span>

### <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="dff69-111">Creare una risorsa di Application Insights in Azure</span><span class="sxs-lookup"><span data-stu-id="dff69-111">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="dff69-112">Ottenere un [account in Microsoft Azure](http://azure.com/pricing).</span><span class="sxs-lookup"><span data-stu-id="dff69-112">Get [an account in Microsoft Azure](http://azure.com/pricing).</span></span> 
2. <span data-ttu-id="dff69-113">Sign in hello [portale di Azure](https://portal.azure.com) e aggiungere una nuova risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="dff69-113">Sign into hello [Azure portal](https://portal.azure.com) and add a new Application Insights resource.</span></span> <span data-ttu-id="dff69-114">in cui i dati verranno elaborati e visualizzati.</span><span class="sxs-lookup"><span data-stu-id="dff69-114">This is where your data will be processed and displayed.</span></span>
   
    ![Clic su +, Servizi per gli sviluppatori, Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    <span data-ttu-id="dff69-116">Scegliere ASP.NET come tipo di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="dff69-116">Choose ASP.NET as hello application type.</span></span>
3. <span data-ttu-id="dff69-117">Aprire una pagina della Guida introduttiva hello "monitoraggio e diagnosi lato client".</span><span class="sxs-lookup"><span data-stu-id="dff69-117">Open hello Getting Started page and open "Monitor and diagnose client side".</span></span>
   
    ![Frammento di codice per l'inserimento nella pagina Web](./media/app-insights-sample-mscrm/03.png)

<span data-ttu-id="dff69-119">**Tenere aperto codici hello** mentre si hello il passaggio successivo in un'altra finestra del browser.</span><span class="sxs-lookup"><span data-stu-id="dff69-119">**Keep hello code page open** while you do hello next step in another browser window.</span></span> <span data-ttu-id="dff69-120">È necessario codice hello presto.</span><span class="sxs-lookup"><span data-stu-id="dff69-120">You'll need hello code soon.</span></span> 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a><span data-ttu-id="dff69-121">Creare una risorsa Web JavaScript in Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="dff69-121">Create a JavaScript web resource in Microsoft Dynamics CRM</span></span>
1. <span data-ttu-id="dff69-122">Aprire l'istanza di CRM Online ed eseguire l'accesso con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="dff69-122">Open your CRM Online instance and login with administrator privileges.</span></span>
2. <span data-ttu-id="dff69-123">Aprire Microsoft Dynamics CRM impostazioni, le personalizzazioni, Personalizza hello sistema</span><span class="sxs-lookup"><span data-stu-id="dff69-123">Open Microsoft Dynamics CRM Settings, Customizations, Customize hello System</span></span>
   
    ![Impostazioni di Microsoft Dynamics CRM](./media/app-insights-sample-mscrm/04.png)
   
    ![Impostazioni > Personalizzazioni](./media/app-insights-sample-mscrm/05.png)

    ![Personalizzare l'opzione di sistema hello](./media/app-insights-sample-mscrm/06.png)

1. <span data-ttu-id="dff69-127">Creare una risorsa JavaScript.</span><span class="sxs-lookup"><span data-stu-id="dff69-127">Create a JavaScript resource.</span></span>
   
    ![Finestra di dialogo Nuova risorsa Web](./media/app-insights-sample-mscrm/07.png)
   
    <span data-ttu-id="dff69-129">Assegnare un nome, seleziona **Script (JScript)** e hello Apri editor di testo.</span><span class="sxs-lookup"><span data-stu-id="dff69-129">Give it a name, select **Script (JScript)** and open hello text editor.</span></span>
   
    ![Editor di testo hello aperto](./media/app-insights-sample-mscrm/08.png)
2. <span data-ttu-id="dff69-131">Copiare il codice hello da Application Insights.</span><span class="sxs-lookup"><span data-stu-id="dff69-131">Copy hello code from Application Insights.</span></span> <span data-ttu-id="dff69-132">Durante la copia di rendere tooignore che tag di script.</span><span class="sxs-lookup"><span data-stu-id="dff69-132">While copying make sure tooignore script tags.</span></span> <span data-ttu-id="dff69-133">Fare riferimento alla schermata illustrata di seguito:</span><span class="sxs-lookup"><span data-stu-id="dff69-133">Refer below screenshot:</span></span>
   
    ![Impostare la chiave di strumentazione](./media/app-insights-sample-mscrm/09.png)
   
    <span data-ttu-id="dff69-135">codice Hello include una chiave di strumentazione hello che identifica la risorsa di Application insights.</span><span class="sxs-lookup"><span data-stu-id="dff69-135">hello code includes hello instrumentation key that identifies your Application insights resource.</span></span>
3. <span data-ttu-id="dff69-136">Fare clic su Salva e quindi su Pubblica.</span><span class="sxs-lookup"><span data-stu-id="dff69-136">Save and publish.</span></span>
   
    ![Fare clic su Salva e quindi su Pubblica](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a><span data-ttu-id="dff69-138">Form strumentazione</span><span class="sxs-lookup"><span data-stu-id="dff69-138">Instrument Forms</span></span>
1. <span data-ttu-id="dff69-139">In Microsoft CRM Online, aprire il form dell'Account hello</span><span class="sxs-lookup"><span data-stu-id="dff69-139">In Microsoft CRM Online, open hello Account form</span></span>
   
    ![Modulo account](./media/app-insights-sample-mscrm/11.png)
2. <span data-ttu-id="dff69-141">Aprire il form hello proprietà</span><span class="sxs-lookup"><span data-stu-id="dff69-141">Open hello form Properties</span></span>
   
    ![Proprietà del modulo](./media/app-insights-sample-mscrm/12.png)
3. <span data-ttu-id="dff69-143">Aggiungere hello risorsa web JavaScript che è stato creato</span><span class="sxs-lookup"><span data-stu-id="dff69-143">Add hello JavaScript web resource that you created</span></span>
   
    ![Menu Aggiungi](./media/app-insights-sample-mscrm/13.png)
   
    ![Aggiungere una risorsa web hello](./media/app-insights-sample-mscrm/14.png)
4. <span data-ttu-id="dff69-146">Salvare e pubblicare le personalizzazioni dei form.</span><span class="sxs-lookup"><span data-stu-id="dff69-146">Save and publish your form customizations.</span></span>

## <a name="metrics-captured"></a><span data-ttu-id="dff69-147">Metriche acquisite</span><span class="sxs-lookup"><span data-stu-id="dff69-147">Metrics captured</span></span>
<span data-ttu-id="dff69-148">Ora impostati acquisizione della telemetria per form hello.</span><span class="sxs-lookup"><span data-stu-id="dff69-148">You have now set up telemetry capture for hello form.</span></span> <span data-ttu-id="dff69-149">Ogni volta che viene utilizzato, verranno inviati dati tooyour risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="dff69-149">Whenever it is used, data will be sent tooyour Application Insights resource.</span></span>

<span data-ttu-id="dff69-150">Di seguito sono esempi di dati hello che verrà visualizzato.</span><span class="sxs-lookup"><span data-stu-id="dff69-150">Here are samples of hello data that you'll see.</span></span>

#### <a name="application-health"></a><span data-ttu-id="dff69-151">Integrità dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="dff69-151">Application health</span></span>
![Tempo di caricamento pagina di esempio](./media/app-insights-sample-mscrm/15.png)

![Grafico delle visualizzazioni pagina di esempio](./media/app-insights-sample-mscrm/16.png)

<span data-ttu-id="dff69-154">Eccezioni del browser:</span><span class="sxs-lookup"><span data-stu-id="dff69-154">Browser exceptions:</span></span>

![Grafico delle eccezioni del browser](./media/app-insights-sample-mscrm/17.png)

<span data-ttu-id="dff69-156">Fare clic su hello grafico tooget dettaglio:</span><span class="sxs-lookup"><span data-stu-id="dff69-156">Click hello chart tooget more detail:</span></span>

![Elenco delle eccezioni](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a><span data-ttu-id="dff69-158">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="dff69-158">Usage</span></span>
![Utenti, sessioni e visualizzazioni pagine](./media/app-insights-sample-mscrm/19.png)

![Grafici della sessione](./media/app-insights-sample-mscrm/20.png)

![Versioni del browser](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a><span data-ttu-id="dff69-162">Browser</span><span class="sxs-lookup"><span data-stu-id="dff69-162">Browsers</span></span>
![Scomposizione del tempo di caricamento della pagina](./media/app-insights-sample-mscrm/22.png)

![Conteggio delle sessioni in base alla versione del browser](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a><span data-ttu-id="dff69-165">Georilevazione</span><span class="sxs-lookup"><span data-stu-id="dff69-165">Geolocation</span></span>
![Conteggio delle sessioni in base al paese](./media/app-insights-sample-mscrm/24.png)

![Sessioni e utenti in base al paese](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a><span data-ttu-id="dff69-168">Richieste visualizzazione pagina interna</span><span class="sxs-lookup"><span data-stu-id="dff69-168">Inside page view request</span></span>
![Riepilogo della visualizzazione pagina](./media/app-insights-sample-mscrm/26.png)

![Cercare negli eventi della visualizzazione pagina](./media/app-insights-sample-mscrm/27.png)

![Visualizzazioni pagina simili](./media/app-insights-sample-mscrm/28.png)

![Proprietà delle visualizzazioni di pagina](./media/app-insights-sample-mscrm/29.png)

![Pagine per sessione](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a><span data-ttu-id="dff69-174">Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="dff69-174">Sample code</span></span>
<span data-ttu-id="dff69-175">[Esaminare il codice di esempio hello](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="dff69-175">[Browse hello sample code](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="power-bi"></a><span data-ttu-id="dff69-176">Power BI</span><span class="sxs-lookup"><span data-stu-id="dff69-176">Power BI</span></span>
<span data-ttu-id="dff69-177">È possibile eseguire anche un'analisi più approfondita, se si [esportare hello dati tooMicrosoft Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="dff69-177">You can do even deeper analysis if you [export hello data tooMicrosoft Power BI](app-insights-export-power-bi.md).</span></span>

## <a name="sample-microsoft-dynamics-crm-solution"></a><span data-ttu-id="dff69-178">Soluzione di esempio Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="dff69-178">Sample Microsoft Dynamics CRM Solution</span></span>
<span data-ttu-id="dff69-179">[Di seguito viene implementata in Microsoft Dynamics CRM soluzione di esempio hello](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="dff69-179">[Here is hello sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="learn-more"></a><span data-ttu-id="dff69-180">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="dff69-180">Learn more</span></span>
* [<span data-ttu-id="dff69-181">Informazioni su Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="dff69-181">What is Application Insights?</span></span>](app-insights-overview.md)
* [<span data-ttu-id="dff69-182">Application Insights per pagine Web</span><span class="sxs-lookup"><span data-stu-id="dff69-182">Application Insights for web pages</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="dff69-183">Altri esempi e procedure dettagliate</span><span class="sxs-lookup"><span data-stu-id="dff69-183">More samples and walkthroughs</span></span>](app-insights-code-samples.md)
