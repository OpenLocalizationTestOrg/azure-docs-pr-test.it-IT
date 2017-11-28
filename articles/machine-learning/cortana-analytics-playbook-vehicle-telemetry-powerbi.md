---
title: "aaaPower BI Dashboard di integrità veicolo e gestire abitudini - Azure | Documenti Microsoft"
description: "Utilizzare funzionalità di hello di insights di predittiva e in tempo reale toogain Intelligence Cortana sull'integrità del veicolo e abitudini di Guida."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: bradsev
ms.openlocfilehash: 0bd054d943387ecad7301236eebae22458173aba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a><span data-ttu-id="f13d3-103">Istruzioni di configurazione del dashboard di Power BI per il modello di soluzione per l'analisi dei dati di telemetria del veicolo</span><span class="sxs-lookup"><span data-stu-id="f13d3-103">Vehicle telemetry analytics solution template Power BI Dashboard setup instructions</span></span>
<span data-ttu-id="f13d3-104">Questo **menu** capitoli toohello questo playbook è collegato.</span><span class="sxs-lookup"><span data-stu-id="f13d3-104">This **menu** links toohello chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="f13d3-105">Hello soluzione Analitica telemetria veicolo illustra come società di assicurazioni, produttori di automobili e settore automobilistico trae possono sfruttare le funzionalità di hello di Cortana Intelligence toogain predittive e in tempo reale informazioni dettagliate sui integrità veicolo e Guida miglioramenti di toodrive abitudini nell'area di hello del cliente verifica, R & D e campagne di marketing.</span><span class="sxs-lookup"><span data-stu-id="f13d3-105">hello Vehicle Telemetry Analytics solution showcases how car dealerships, automobile manufacturers and insurance companies can leverage hello capabilities of Cortana Intelligence toogain real-time and predictive insights on vehicle health and driving habits toodrive improvements in hello area of customer experience, R&D and marketing campaigns.</span></span> <span data-ttu-id="f13d3-106">Questo documento contiene istruzioni dettagliate su come configurare i report di Power BI hello e dashboard dopo aver distribuita la soluzione hello nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f13d3-106">This document contains step by step instructions on how you can configure hello Power BI reports and dashboard once hello solution is deployed in your subscription.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f13d3-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f13d3-107">Prerequisites</span></span>
1. <span data-ttu-id="f13d3-108">Distribuire hello [telemetria Analitica](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) soluzione</span><span class="sxs-lookup"><span data-stu-id="f13d3-108">Deploy hello [Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solution</span></span>  
2. [<span data-ttu-id="f13d3-109">Installare Microsoft Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="f13d3-109">Install Microsoft Power BI Desktop</span></span>](http://www.microsoft.com/download/details.aspx?id=45331)
3. <span data-ttu-id="f13d3-110">Una [sottoscrizione di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f13d3-110">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="f13d3-111">Se non si dispone di una sottoscrizione Azure, iniziare con una sottoscrizione gratuita di Azure.</span><span class="sxs-lookup"><span data-stu-id="f13d3-111">If you don't have an Azure subscription, get started with Azure free subscription</span></span>
4. <span data-ttu-id="f13d3-112">Account di Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="f13d3-112">Microsoft Power BI account</span></span>

## <a name="cortana-intelligence-suite-components"></a><span data-ttu-id="f13d3-113">Componenti di Cortana Intelligence Suite</span><span class="sxs-lookup"><span data-stu-id="f13d3-113">Cortana Intelligence Suite Components</span></span>
<span data-ttu-id="f13d3-114">Come parte del modello di soluzione hello veicolo telemetria Analitica, hello seguenti Intelligence Cortana services viene distribuito nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f13d3-114">As part of hello Vehicle Telemetry Analytics solution template, hello following Cortana Intelligence services are deployed in your subscription.</span></span>

* <span data-ttu-id="f13d3-115">**Hub eventi** per l'inserimento di milioni di eventi di telemetria del veicolo in Azure.</span><span class="sxs-lookup"><span data-stu-id="f13d3-115">**Event Hub** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="f13d3-116">**Analisi di flusso** per ottenere informazioni dettagliate in tempo reale sul funzionamento del veicolo e salvare i dati in modo permanente nello spazio di archiviazione a lungo termine per un'analisi batch avanzata.</span><span class="sxs-lookup"><span data-stu-id="f13d3-116">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="f13d3-117">**Machine Learning** per il rilevamento di anomalie in tempo reale e approfondimenti predittiva toogain di elaborazione batch.</span><span class="sxs-lookup"><span data-stu-id="f13d3-117">**Machine Learning** for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="f13d3-118">**HDInsight** tootransform sfruttate dati su larga scala</span><span class="sxs-lookup"><span data-stu-id="f13d3-118">**HDInsight** is leveraged tootransform data at scale</span></span>
* <span data-ttu-id="f13d3-119">**Data Factory** gestisce l'orchestrazione, pianificazione, la gestione delle risorse e il monitoraggio della pipeline di elaborazione batch hello.</span><span class="sxs-lookup"><span data-stu-id="f13d3-119">**Data Factory** handles orchestration, scheduling, resource management and monitoring of hello batch processing pipeline.</span></span>

<span data-ttu-id="f13d3-120">**Power BI** offre alla soluzione un dashboard completo per la visualizzazione di dati in tempo reale e di analisi predittiva.</span><span class="sxs-lookup"><span data-stu-id="f13d3-120">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="f13d3-121">soluzione Hello utilizza due origini dati diverse: **simulato segnali veicolo e set di dati diagnostici** e **catalogo veicolo**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-121">hello solution uses two different data sources: **Simulated vehicle signals and diagnostic dataset** and **vehicle catalog**.</span></span>

<span data-ttu-id="f13d3-122">Nella soluzione è incluso un simulatore di dati telematici relativi al veicolo.</span><span class="sxs-lookup"><span data-stu-id="f13d3-122">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="f13d3-123">Genera informazioni di diagnostica ed segnala stato toohello corrispondente del veicolo hello e modello determinante in un determinato punto nel tempo.</span><span class="sxs-lookup"><span data-stu-id="f13d3-123">It emits diagnostic information and signals corresponding toohello state of hello vehicle and driving pattern at a given point in time.</span></span> 

<span data-ttu-id="f13d3-124">Hello veicolo catalogo è un mapping riferimento set di dati contenente VPN toomodel</span><span class="sxs-lookup"><span data-stu-id="f13d3-124">hello Vehicle Catalog is a reference dataset containing VIN toomodel mapping</span></span>

## <a name="power-bi-dashboard-preparation"></a><span data-ttu-id="f13d3-125">Preparazione del dashboard di Power BI</span><span class="sxs-lookup"><span data-stu-id="f13d3-125">Power BI Dashboard Preparation</span></span>
### <a name="setup-power-bi-real-time-dashboard"></a><span data-ttu-id="f13d3-126">Configurare il dashboard in tempo reale di Power BI</span><span class="sxs-lookup"><span data-stu-id="f13d3-126">Setup Power BI Real-Time Dashboard</span></span>

<span data-ttu-id="f13d3-127">**Avviare un'applicazione hello dashboard in tempo reale** al termine della distribuzione di hello, è necessario seguire le istruzioni di operazione manuale hello</span><span class="sxs-lookup"><span data-stu-id="f13d3-127">**Start hello real-time dashboard application** Once hello deployment is completed, you should follow hello Manual Operation Instructions</span></span>

* <span data-ttu-id="f13d3-128">Scaricare l'applicazione dashboard in tempo reale RealtimeDashboardApp.zip e decomprimere il file.</span><span class="sxs-lookup"><span data-stu-id="f13d3-128">Download real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span></span>
*  <span data-ttu-id="f13d3-129">Nella cartella decompresso hello, aprire file di configurazione app 'RealtimeDashboardApp.exe.config', sostituire appSettings per le connessioni di servizio hub eventi, l'archiviazione Blob e ML con i valori hello in istruzioni di operazione manuale hello e salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="f13d3-129">In hello unzipped folder, open app config file 'RealtimeDashboardApp.exe.config', replace appSettings for Eventhub, Blob Storage, and ML service connections with hello values in hello Manual Operation Instructions, and save your changes.</span></span>
* <span data-ttu-id="f13d3-130">Eseguire l'applicazione RealtimeDashboardApp.exe.</span><span class="sxs-lookup"><span data-stu-id="f13d3-130">Run application RealtimeDashboardApp.exe.</span></span> <span data-ttu-id="f13d3-131">Una finestra di dialogo di accesso popup, fornire le credenziali di Power BI valide e fare clic su hello **Accept** pulsante.</span><span class="sxs-lookup"><span data-stu-id="f13d3-131">A login window will pop up, provide your valid PowerBI credentials and click hello **Accept** button.</span></span> <span data-ttu-id="f13d3-132">Quindi l'applicazione hello inizierà toorun.</span><span class="sxs-lookup"><span data-stu-id="f13d3-132">Then hello app will start toorun.</span></span>

   ![Accedi tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Autorizzazioni per il dashboard di Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* <span data-ttu-id="f13d3-135">Sito Web tooPowerBI account di accesso e creare dashboard in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="f13d3-135">Login tooPowerBI website, and create real-time dashboard.</span></span>

<span data-ttu-id="f13d3-136">A questo punto, si è pronti tooconfigure dashboard di Power BI hello con le visualizzazioni dettagliate toogain in tempo reale e abitudini predittive informazioni essenziali quanto a integrità veicolo e la Guida.</span><span class="sxs-lookup"><span data-stu-id="f13d3-136">Now, you are ready tooconfigure hello Power BI dashboard with rich visualizations toogain real-time and predictive insights on vehicle health and driving habits.</span></span> <span data-ttu-id="f13d3-137">Sono necessari circa 45 minuti tooan ora toocreate hello tutti i report e configurare hello dashboard.</span><span class="sxs-lookup"><span data-stu-id="f13d3-137">It takes about 45 minutes tooan hour toocreate all hello reports and configure hello dashboard.</span></span> 

### <a name="configure-power-bi-reports"></a><span data-ttu-id="f13d3-138">Configurare i report di Power BI</span><span class="sxs-lookup"><span data-stu-id="f13d3-138">Configure Power BI reports</span></span>
<span data-ttu-id="f13d3-139">i report in tempo reale di Hello e dashboard hello richiedere circa 30 a 45 minuti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="f13d3-139">hello real-time reports and hello dashboard take about 30-45 minutes toocomplete.</span></span> <span data-ttu-id="f13d3-140">Sfoglia troppo[http://powerbi.com](http://powerbi.com) e account di accesso.</span><span class="sxs-lookup"><span data-stu-id="f13d3-140">Browse too[http://powerbi.com](http://powerbi.com) and login.</span></span>

![Accedi tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

<span data-ttu-id="f13d3-142">Viene generato un nuovo set di dati in Power BI.</span><span class="sxs-lookup"><span data-stu-id="f13d3-142">A new dataset is generated in Power BI.</span></span> <span data-ttu-id="f13d3-143">Fare clic su hello **ConnectedCarsRealtime** set di dati.</span><span class="sxs-lookup"><span data-stu-id="f13d3-143">Click hello **ConnectedCarsRealtime** dataset.</span></span>

![Selezionare il set di dati in tempo reale delle automobili connesse](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

<span data-ttu-id="f13d3-145">Salvare hello report vuoto utilizzando **Ctrl + s**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-145">Save hello blank report using **Ctrl + s**.</span></span>

![Salvare il report vuoto](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

<span data-ttu-id="f13d3-147">Specificare il nome del report *Analisi dei dati di telemetria del veicolo in tempo reale - Report*.</span><span class="sxs-lookup"><span data-stu-id="f13d3-147">Provide report name *Vehicle Telemetry Analytics Real-time - Reports*.</span></span>

![Specificare il nome del report](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a><span data-ttu-id="f13d3-149">Report in tempo reale</span><span class="sxs-lookup"><span data-stu-id="f13d3-149">Real-time reports</span></span>
<span data-ttu-id="f13d3-150">Questa soluzione include tre report in tempo reale:</span><span class="sxs-lookup"><span data-stu-id="f13d3-150">There are three real-time reports in this solution:</span></span>

1. <span data-ttu-id="f13d3-151">Veicoli operativi</span><span class="sxs-lookup"><span data-stu-id="f13d3-151">Vehicles in operation</span></span>
2. <span data-ttu-id="f13d3-152">Veicoli che richiedono manutenzione</span><span class="sxs-lookup"><span data-stu-id="f13d3-152">Vehicles Requiring Maintenance</span></span>
3. <span data-ttu-id="f13d3-153">Statistiche sull'integrità dei veicoli</span><span class="sxs-lookup"><span data-stu-id="f13d3-153">Vehicles Health Statistics</span></span>

<span data-ttu-id="f13d3-154">È possibile scegliere tooconfigure tutti i report in tempo reale tre hello o arrestarsi dopo qualsiasi fase e procedere toohello successiva sezione di configurazione dei report di batch hello.</span><span class="sxs-lookup"><span data-stu-id="f13d3-154">You can choose tooconfigure all hello three real-time reports or stop after any stage and proceed toohello next section of configuring hello batch reports.</span></span> <span data-ttu-id="f13d3-155">È consigliabile toocreate tutti hello tre riporta informazioni dettagliate completo toovisualize hello del percorso in tempo reale di hello di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="f13d3-155">We recommend you toocreate all hello three reports toovisualize hello full insights of hello real-time path of hello solution.</span></span>  

### <a name="1-vehicles-in-operation"></a><span data-ttu-id="f13d3-156">1. Veicoli operativi</span><span class="sxs-lookup"><span data-stu-id="f13d3-156">1. Vehicles in operation</span></span>
<span data-ttu-id="f13d3-157">Fare doppio clic su **pagina 1** e rinominarlo troppo "Veicoli nell'operazione"</span><span class="sxs-lookup"><span data-stu-id="f13d3-157">Double-click **Page 1** and rename it too“Vehicles in operation”</span></span>  
    <span data-ttu-id="f13d3-158">![Automobili connesse: veicoli operativi](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span><span class="sxs-lookup"><span data-stu-id="f13d3-158">![Connected Cars - Vehicles in operation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span></span>  

<span data-ttu-id="f13d3-159">Selezionare il campo **vin** da **Fields** e scegliere **"Card"** come tipo di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="f13d3-159">Select **vin** field from **Fields** and choose visualization type as **“Card”**.</span></span>  

<span data-ttu-id="f13d3-160">Viene creata una visualizzazione di tipo scheda come illustrato nella figura.</span><span class="sxs-lookup"><span data-stu-id="f13d3-160">Card visualization is created as shown in figure.</span></span>  
    ![Automobili connesse: seleziona vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

<span data-ttu-id="f13d3-162">Fare clic su nuova visualizzazione tooadd area vuota hello.</span><span class="sxs-lookup"><span data-stu-id="f13d3-162">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="f13d3-163">Selezionare **Città** e **vin** dai campi.</span><span class="sxs-lookup"><span data-stu-id="f13d3-163">Select **City** and **vin** from fields.</span></span> <span data-ttu-id="f13d3-164">Modificare anche le visualizzazione**"Mappa"**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-164">Change visualization too**“Map”**.</span></span> <span data-ttu-id="f13d3-165">Trascinare **vin** nell'area valori.</span><span class="sxs-lookup"><span data-stu-id="f13d3-165">Drag **vin** in values area.</span></span> <span data-ttu-id="f13d3-166">Trascinare **Città** dai campi troppo**legenda** area.</span><span class="sxs-lookup"><span data-stu-id="f13d3-166">Drag **city** from fields too**Legend** area.</span></span>   
    <span data-ttu-id="f13d3-167">![Automobili connesse: visualizzazione scheda](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span><span class="sxs-lookup"><span data-stu-id="f13d3-167">![Connected Cars - Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span></span>

<span data-ttu-id="f13d3-168">Selezionare **formato** sezione **visualizzazioni**, fare clic su **titolo** e modificare hello **testo** troppo**"veicoli operazione in base alla città"**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-168">Select **format** section from **Visualizations**, click **Title** and change hello **Text** too**“Vehicles in operation by city”**.</span></span>  
    <span data-ttu-id="f13d3-169">![Automobili connesse: veicoli operativi in base alla città](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span><span class="sxs-lookup"><span data-stu-id="f13d3-169">![Connected Cars - Vehicles in operation by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span></span>   

<span data-ttu-id="f13d3-170">La visualizzazione finale è simile a quella illustrata nella figura.</span><span class="sxs-lookup"><span data-stu-id="f13d3-170">Final visualization looks as shown in figure.</span></span>    
    ![Automobili connesse: visualizzazione finale](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

<span data-ttu-id="f13d3-172">Fare clic su nuova visualizzazione tooadd area vuota hello.</span><span class="sxs-lookup"><span data-stu-id="f13d3-172">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="f13d3-173">Selezionare **Città** e **VPN**, modificare il tipo di visualizzazione anche**istogramma a colonne raggruppate**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-173">Select **City** and **vin**, change visualization type too**Clustered Column Chart**.</span></span> <span data-ttu-id="f13d3-174">Verificare che il campo **Città** sia nell'**area Asse** e **vin** nell'**area Valore**</span><span class="sxs-lookup"><span data-stu-id="f13d3-174">Ensure **City** field in **Axis area** and **vin** in **Value area**</span></span>  

<span data-ttu-id="f13d3-175">Ordinare il grafico in base a **"Count of vin"**</span><span class="sxs-lookup"><span data-stu-id="f13d3-175">Sort chart by **“Count of vin”**</span></span>  
    <span data-ttu-id="f13d3-176">![Automobili connesse: conteggio di vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span><span class="sxs-lookup"><span data-stu-id="f13d3-176">![Connected Cars - Count of vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span></span>  

<span data-ttu-id="f13d3-177">Il grafico cambia **titolo** troppo**"Veicoli nell'operazione in base alla città"**</span><span class="sxs-lookup"><span data-stu-id="f13d3-177">Change chart **Title** too**“Vehicles in operation by city”**</span></span>  

<span data-ttu-id="f13d3-178">Fare clic su hello **formato** sezione, quindi selezionare **colori dati**, fare clic su hello **"On"** troppo**Mostra tutto**</span><span class="sxs-lookup"><span data-stu-id="f13d3-178">Click hello **Format** section, then select **Data Colors**,  Click hello **“On”** too**Show All**</span></span>  
    <span data-ttu-id="f13d3-179">![Automobili connesse: mostra tutti i colori dei dati](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span><span class="sxs-lookup"><span data-stu-id="f13d3-179">![Connected Cars - Show all Data Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span></span>  

<span data-ttu-id="f13d3-180">Modificare il colore di hello di singole città facendo clic sull'icona di colore.</span><span class="sxs-lookup"><span data-stu-id="f13d3-180">Change hello color of individual city by clicking on color icon.</span></span>  
    ![Automobili connesse: modifica colori](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

<span data-ttu-id="f13d3-182">Fare clic su nuova visualizzazione tooadd area vuota hello.</span><span class="sxs-lookup"><span data-stu-id="f13d3-182">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="f13d3-183">Dalle visualizzazioni selezionare **Istogramma a colonne raggruppate**, trascinare il campo **città** nell'area **Asse**, **Modello** nell'area **Legenda** e **vin** nell'area **Valore**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-183">Select **Clustered Column Chart** visualization from visualizations, drag **city** field in **Axis** area, **Model** in **Legend** area and **vin** in **Value** area.</span></span>  
    <span data-ttu-id="f13d3-184">![Automobili connesse: istogramma a colonne raggruppate](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span><span class="sxs-lookup"><span data-stu-id="f13d3-184">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span></span>  
    <span data-ttu-id="f13d3-185">![Automobili connesse: rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span><span class="sxs-lookup"><span data-stu-id="f13d3-185">![Connected Cars - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span></span>

<span data-ttu-id="f13d3-186">Ridisporre la visualizzazione nella pagina come illustrato nella figura.</span><span class="sxs-lookup"><span data-stu-id="f13d3-186">Rearrange all visualization on this page as shown in figure.</span></span>  
    ![Automobili connesse: visualizzazioni](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

<span data-ttu-id="f13d3-188">Report in tempo reale di hello "Veicoli nell'operazione" è stata configurata.</span><span class="sxs-lookup"><span data-stu-id="f13d3-188">You have successfully configured hello “Vehicles in operation” real-time report.</span></span> <span data-ttu-id="f13d3-189">È possibile procedere toocreate hello successivo in tempo reale report o interrompere la procedura e configurare hello dashboard.</span><span class="sxs-lookup"><span data-stu-id="f13d3-189">You can proceed toocreate hello next real-time report or stop here and configure hello dashboard.</span></span> 

### <a name="2-vehicles-requiring-maintenance"></a><span data-ttu-id="f13d3-190">2. Veicoli che richiedono manutenzione</span><span class="sxs-lookup"><span data-stu-id="f13d3-190">2. Vehicles Requiring Maintenance</span></span>
<span data-ttu-id="f13d3-191">Fare clic su ![Aggiungi](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd un nuovo report, rinominare troppo**"Veicoli che richiedono manutenzione"**</span><span class="sxs-lookup"><span data-stu-id="f13d3-191">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd a new report, rename it too**“Vehicles Requiring Maintenance”**</span></span>

![Automobili connesse: veicoli che richiedono manutenzione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

<span data-ttu-id="f13d3-193">Selezionare **VPN** campo e modificare il tipo di visualizzazione troppo**scheda**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-193">Select **vin** field and change visualization type too**Card**.</span></span>  
    <span data-ttu-id="f13d3-194">![Automobili connesse: visualizzazione scheda vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span><span class="sxs-lookup"><span data-stu-id="f13d3-194">![Connected Cars - Vin Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span></span>  

<span data-ttu-id="f13d3-195">Abbiamo un campo denominato "MaintenanceLabel" nel set di dati hello.</span><span class="sxs-lookup"><span data-stu-id="f13d3-195">We have a field named “MaintenanceLabel” In hello dataset.</span></span> <span data-ttu-id="f13d3-196">Questo campo può avere un valore pari a "0" o "1".</span><span class="sxs-lookup"><span data-stu-id="f13d3-196">This field can have a value of “0” or “1”.”</span></span> <span data-ttu-id="f13d3-197">Viene impostato dal modello di Azure Machine Learning hello effettuato il provisioning come parte della soluzione e integrato con il percorso di hello in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="f13d3-197">It is set by hello Azure Machine Learning model provisioned as part of solution and integrated with hello real-time path.</span></span> <span data-ttu-id="f13d3-198">il valore di Hello "1" indica che un veicolo richiede attività di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="f13d3-198">hello value “1” indicates a vehicle requires maintenance.</span></span> 

<span data-ttu-id="f13d3-199">tooadd un **a livello di pagina** filtro per la visualizzazione dei dati veicoli, che richiedono manutenzione:</span><span class="sxs-lookup"><span data-stu-id="f13d3-199">tooadd a **Page Level** filter for showing vehicles data, which are requiring maintenance:</span></span> 

1. <span data-ttu-id="f13d3-200">Hello trascinare **"MaintenanceLabel"** campo in **filtri a livello di pagina**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-200">Drag hello **“MaintenanceLabel”** field into **Page Level Filters**.</span></span>  
   <span data-ttu-id="f13d3-201">![Automobili connesse: filtri del livello di pagina](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span><span class="sxs-lookup"><span data-stu-id="f13d3-201">![Connected Cars - Page Level Filters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span></span>  
2. <span data-ttu-id="f13d3-202">Fare clic sul menu **Basic Filtering** presente in basso nella schermata del filtro MaintenanceLabel in Page Level Filter.</span><span class="sxs-lookup"><span data-stu-id="f13d3-202">Click **Basic Filtering** menu present at bottom of MaintenanceLabel Page Level Filter.</span></span>  
   <span data-ttu-id="f13d3-203">![Automobili connesse: filtro base](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span><span class="sxs-lookup"><span data-stu-id="f13d3-203">![Connected Cars - Basic Filtering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span></span>  
3. <span data-ttu-id="f13d3-204">Impostare il valore di filtro troppo**"1"**  </span><span class="sxs-lookup"><span data-stu-id="f13d3-204">Set its filter value too**“1”**  </span></span>  
   <span data-ttu-id="f13d3-205">![Automobili connesse: valore di filtro](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span><span class="sxs-lookup"><span data-stu-id="f13d3-205">![Connected Cars - Filter Value](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span></span>  

<span data-ttu-id="f13d3-206">Fare clic su nuova visualizzazione tooadd area vuota hello.</span><span class="sxs-lookup"><span data-stu-id="f13d3-206">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="f13d3-207">Dalle visualizzazioni selezionare **Istogramma a colonne raggruppate**</span><span class="sxs-lookup"><span data-stu-id="f13d3-207">Select **Clustered Column Chart** from visualizations</span></span>  
<span data-ttu-id="f13d3-208">![Automobili connesse: visualizzazione scheda vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span><span class="sxs-lookup"><span data-stu-id="f13d3-208">![Connected Cars - Vind Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span></span>  
<span data-ttu-id="f13d3-209">![Automobili connesse: istogramma a colonne raggruppate](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span><span class="sxs-lookup"><span data-stu-id="f13d3-209">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span></span>

<span data-ttu-id="f13d3-210">Campo trascinare **modello** in **asse** area **VPN** troppo**valore** area.</span><span class="sxs-lookup"><span data-stu-id="f13d3-210">Drag field **Model** into **Axis** area, **Vin** too**Value** area.</span></span> <span data-ttu-id="f13d3-211">Ordinare quindi la visualizzazione in base a **Count of vin**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-211">Then sort visualization by **Count of vin**.</span></span>  <span data-ttu-id="f13d3-212">Il grafico cambia **titolo** troppo**"Veicoli richiesta dal modello di manutenzione"**</span><span class="sxs-lookup"><span data-stu-id="f13d3-212">Change chart **Title** too**“Vehicles requiring maintenance by model”**</span></span>  

<span data-ttu-id="f13d3-213">Trascinare i campi **vin** in **Saturazione colore** presente nella sezione **Campi** ![Campi](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) della scheda **Visualizzazione**</span><span class="sxs-lookup"><span data-stu-id="f13d3-213">Drag **vin** fields into **Color Saturation** present at **Fields** ![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of **Visualization** tab</span></span>  
<span data-ttu-id="f13d3-214">![Automobili connesse: saturazione dei colori](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span><span class="sxs-lookup"><span data-stu-id="f13d3-214">![Connected Cars - Color Saturation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span></span>  

<span data-ttu-id="f13d3-215">Modificare **Colori dati** nelle visualizzazioni dalla sezione **Formato**</span><span class="sxs-lookup"><span data-stu-id="f13d3-215">Change **Data Colors** in visualizations from **Format** section</span></span>  
<span data-ttu-id="f13d3-216">Cambiare il colore minimo in: **F2C812**</span><span class="sxs-lookup"><span data-stu-id="f13d3-216">Change Minimum color to: **F2C812**</span></span>  
<span data-ttu-id="f13d3-217">Cambiare il colore minimo in: **FF6300**</span><span class="sxs-lookup"><span data-stu-id="f13d3-217">Change Maximum color to: **FF6300**</span></span>  
<span data-ttu-id="f13d3-218">![Automobili connesse: modifiche dei colori](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span><span class="sxs-lookup"><span data-stu-id="f13d3-218">![Connected Cars - Color Changes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span></span>  
<span data-ttu-id="f13d3-219">![Automobili connesse: nuovi colori di visualizzazione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span><span class="sxs-lookup"><span data-stu-id="f13d3-219">![Connected Cars - New Visualization Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span></span>  

<span data-ttu-id="f13d3-220">Fare clic su nuova visualizzazione tooadd area vuota hello.</span><span class="sxs-lookup"><span data-stu-id="f13d3-220">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="f13d3-221">Selezionare **Istogramma a colonne raggruppate** dalle visualizzazioni, trascinare il campo **vin** nell'area **Valore** e il campo **Città** nell'area **Asse**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-221">Select **Clustered column chart** from visualizations, drag **vin** field into **Value** area, drag **City** field into **Axis** area.</span></span> <span data-ttu-id="f13d3-222">Ordinare il grafico in base a **"Count of vin"**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-222">Sort chart by **“Count of vin”**.</span></span> <span data-ttu-id="f13d3-223">Il grafico cambia **titolo** troppo**"Veicoli che richiedono manutenzione in base alla città"** </span><span class="sxs-lookup"><span data-stu-id="f13d3-223">Change chart **Title** too**“Vehicles requiring maintenance by city”** </span></span>  
<span data-ttu-id="f13d3-224">![Automobili connesse: veicoli che richiedono manutenzione in base alla città](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span><span class="sxs-lookup"><span data-stu-id="f13d3-224">![Connected Cars - Vehicles requiring maintenance by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span></span>  

<span data-ttu-id="f13d3-225">Fare clic su nuova visualizzazione tooadd area vuota hello.</span><span class="sxs-lookup"><span data-stu-id="f13d3-225">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="f13d3-226">Selezionare **scheda con più righe** visualizzazione da visualizzazioni, trascinare **modello** e **VPN** in hello **campi** area.</span><span class="sxs-lookup"><span data-stu-id="f13d3-226">Select **Multi-Row Card** visualization from visualizations, drag **Model** and **vin** into hello **Fields** area.</span></span>  
<span data-ttu-id="f13d3-227">![Automobili connesse: scheda con più righe](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span><span class="sxs-lookup"><span data-stu-id="f13d3-227">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span></span>    

<span data-ttu-id="f13d3-228">Report finale hello ridisposizione tutti di visualizzazione hello, simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f13d3-228">Rearranging all of hello visualization, hello final report looks as follows:</span></span>  
![Automobili connesse: scheda con più righe](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

<span data-ttu-id="f13d3-230">È stato configurato correttamente i report in tempo reale di hello "Veicoli che richiedono manutenzione".</span><span class="sxs-lookup"><span data-stu-id="f13d3-230">You have successfully configured hello “Vehicles Requiring Maintenance” real-time report.</span></span> <span data-ttu-id="f13d3-231">È possibile procedere toocreate hello successivo in tempo reale report o interrompere la procedura e configurare hello dashboard.</span><span class="sxs-lookup"><span data-stu-id="f13d3-231">You can proceed toocreate hello next real-time report or stop here and configure hello dashboard.</span></span> 

### <a name="3-vehicles-health-statistics"></a><span data-ttu-id="f13d3-232">3. Statistiche sull'integrità dei veicoli</span><span class="sxs-lookup"><span data-stu-id="f13d3-232">3. Vehicles Health Statistics</span></span>
<span data-ttu-id="f13d3-233">Fare clic su ![Aggiungi](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd nuovo report, rinominarla troppo**"Veicoli delle statistiche di integrità"**</span><span class="sxs-lookup"><span data-stu-id="f13d3-233">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd new report, rename it too**“Vehicles Health Statistics”**</span></span>  

<span data-ttu-id="f13d3-234">Selezionare **misuratore** visualizzazione da visualizzazioni, quindi trascinare hello **velocità** campo in **, valore minimo, massimo valore** aree.</span><span class="sxs-lookup"><span data-stu-id="f13d3-234">Select **Gauge** visualization from visualizations, then drag hello **Speed** field into **Value, Minimum Value, Maximum Value** areas.</span></span>  
<span data-ttu-id="f13d3-235">![Automobili connesse: scheda con più righe](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span><span class="sxs-lookup"><span data-stu-id="f13d3-235">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span></span>  

<span data-ttu-id="f13d3-236">Modificare l'aggregazione predefinita hello di **velocità** in **valore area** troppo**medio**</span><span class="sxs-lookup"><span data-stu-id="f13d3-236">Change hello default aggregation of **speed** in **Value area** too**Average**</span></span> 

<span data-ttu-id="f13d3-237">Modificare l'aggregazione predefinita hello di **velocità** in **area minima** troppo**minimo**</span><span class="sxs-lookup"><span data-stu-id="f13d3-237">Change hello default aggregation of **speed** in **Minimum area** too**Minimum**</span></span>

<span data-ttu-id="f13d3-238">Modificare l'aggregazione predefinita hello di **velocità** in **area massima** troppo**massimo**</span><span class="sxs-lookup"><span data-stu-id="f13d3-238">Change hello default aggregation of **speed** in **Maximum area** too**Maximum**</span></span>

![Automobili connesse: scheda con più righe](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

<span data-ttu-id="f13d3-240">Rinominare hello **misuratore titolo** troppo**"Velocità media"**</span><span class="sxs-lookup"><span data-stu-id="f13d3-240">Rename hello **Gauge Title** too**“Average speed”**</span></span> 

![Automobili connesse: misuratore](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

<span data-ttu-id="f13d3-242">Fare clic su nuova visualizzazione tooadd area vuota hello.</span><span class="sxs-lookup"><span data-stu-id="f13d3-242">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="f13d3-243">Allo stesso modo, aggiungere un **Misuratore** per **media olio motore**, **media carburante** e **media temperatura motore**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-243">Similarly add a **Gauge** for **average engine oil**, **average fuel**, and **average engine temperate**.</span></span>  

<span data-ttu-id="f13d3-244">Modificare l'aggregazione predefinita hello di campi in ogni misuratore in base di sopra di passaggi **"Velocità media"** del misuratore.</span><span class="sxs-lookup"><span data-stu-id="f13d3-244">Change hello default aggregation of fields in each gauge as per above steps in **“Average speed”** gauge.</span></span>

![Automobili connesse: misuratori](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

<span data-ttu-id="f13d3-246">Fare clic su nuova visualizzazione tooadd area vuota hello.</span><span class="sxs-lookup"><span data-stu-id="f13d3-246">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="f13d3-247">Selezionare **riga e istogramma a colonne raggruppate** visualizzazioni, quindi trascinare **Città** campo in **asse condiviso**, trascinare **velocità**, **campi tirepressure ed engineoil** in **i valori di colonna** area, modificare il tipo di aggregazione troppo**Media**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-247">Select **Line and Clustered Column Chart** from visualizations, then drag **City** field into **Shared Axis**, drag **speed**, **tirepressure and engineoil fields** into **Column Values** area, change their aggregation type too**Average**.</span></span> 

<span data-ttu-id="f13d3-248">Hello trascinare **engineTemperature** campo in **valori riga** area, modificare il tipo di aggregazione di hello troppo**Media**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-248">Drag hello **engineTemperature** field into **Line Values** area, change hello  aggregation type too**Average**.</span></span> 

![Automobili connesse: campi di visualizzazione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

<span data-ttu-id="f13d3-250">Grafico hello modifica **titolo** troppo**"Media velocità, pressione tire, olio motore e temperatura del motore"**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-250">Change hello chart **Title** too**“Average speed, tire pressure, engine oil and engine temperature”**.</span></span>  

![Automobili connesse: campi di visualizzazione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

<span data-ttu-id="f13d3-252">Fare clic su nuova visualizzazione tooadd area vuota hello.</span><span class="sxs-lookup"><span data-stu-id="f13d3-252">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="f13d3-253">Selezionare **Treemap** visualizzazione da visualizzazioni, trascinare hello **modello** campo in hello **gruppo** area e trascinare hello  **MaintenanceProbability** in hello **valori** area.</span><span class="sxs-lookup"><span data-stu-id="f13d3-253">Select **Treemap** visualization from visualizations, drag hello **Model** field into hello **Group** area, and drag hello field **MaintenanceProbability** into hello **Values** area.</span></span>

<span data-ttu-id="f13d3-254">Grafico hello modifica **titolo** troppo**"Modelli veicolo che richiedono manutenzione"**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-254">Change hello chart **Title** too**“Vehicle models requiring maintenance”**.</span></span>

![Automobili connesse: modifica titolo del grafico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

<span data-ttu-id="f13d3-256">Fare clic su nuova visualizzazione tooadd area vuota hello.</span><span class="sxs-lookup"><span data-stu-id="f13d3-256">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="f13d3-257">Selezionare **barre del grafico in pila 100%** dalla visualizzazione, trascinare hello **Città** campo in hello **asse** area e trascinare hello **MaintenanceProbability**, **RecallProbability** campi hello **valore** area.</span><span class="sxs-lookup"><span data-stu-id="f13d3-257">Select **100% Stacked Bar Chart** from visualization, drag hello **city** field into hello **Axis** area, and drag hello **MaintenanceProbability**, **RecallProbability** fields into hello **Value** area.</span></span>

![Automobili connesse: aggiungi nuova visualizzazione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

<span data-ttu-id="f13d3-259">Fare clic su **formato**selezionare **colori dati**e set hello **MaintenanceProbability** toohello valore di colore **"F2C80F"**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-259">Click **Format**, select **Data Colors**, and set hello **MaintenanceProbability** color toohello value **“F2C80F”**.</span></span>

<span data-ttu-id="f13d3-260">Hello modifica **titolo** di hello grafico troppo**"Probabilità del veicolo manutenzione e richiamare by City"**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-260">Change hello **Title** of hello chart too**“Probability of Vehicle Maintenance & Recall by City”**.</span></span>

![Automobili connesse: aggiungi nuova visualizzazione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

<span data-ttu-id="f13d3-262">Fare clic su nuova visualizzazione tooadd area vuota hello.</span><span class="sxs-lookup"><span data-stu-id="f13d3-262">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="f13d3-263">Selezionare **grafico ad Area** dalla visualizzazione da visualizzazioni, trascinare hello **modello** campo in hello **asse** area e trascinare hello **engineOil, tirepressure, velocità e MaintenanceProbability** campi hello **valori** area.</span><span class="sxs-lookup"><span data-stu-id="f13d3-263">Select **Area Chart** from visualization from visualizations, drag hello **Model** field into hello **Axis** area, and drag hello **engineOil, tirepressure, speed and MaintenanceProbability** fields into hello **Values** area.</span></span> <span data-ttu-id="f13d3-264">Modificare il tipo di aggregazione troppo**"Medio"**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-264">Change their aggregation type too**“Average”**.</span></span> 

![Automobili connesse: modifica tipo di aggregazione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

<span data-ttu-id="f13d3-266">Modificare il titolo di hello del grafico hello troppo**"Media olio motore, tire probabilità pressione, velocità e la manutenzione dal modello"**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-266">Change hello title of hello chart too**“Average engine oil, tire pressure, speed and maintenance probability by model”**.</span></span>

![Automobili connesse: modifica titolo del grafico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

<span data-ttu-id="f13d3-268">Fare clic su nuova visualizzazione tooadd area vuota hello:</span><span class="sxs-lookup"><span data-stu-id="f13d3-268">Click hello blank area tooadd new visualization:</span></span>

1. <span data-ttu-id="f13d3-269">Nelle visualizzazioni selezionare **Scatter Chart** .</span><span class="sxs-lookup"><span data-stu-id="f13d3-269">Select **Scatter Chart** visualization from visualizations.</span></span>
2. <span data-ttu-id="f13d3-270">Hello trascinare **modello** campo in hello **dettagli** e **legenda** area.</span><span class="sxs-lookup"><span data-stu-id="f13d3-270">Drag hello **Model** field into hello **Details** and **Legend** area.</span></span>
3. <span data-ttu-id="f13d3-271">Hello trascinare **carburante** campo in hello **asse x** area, modificare anche le aggregazioni hello**Media**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-271">Drag hello **fuel** field into hello **X-Axis** area, change hello aggregation too**Average**.</span></span>
4. <span data-ttu-id="f13d3-272">Trascinare **engineTemparature** in **area asse y**, modificare anche le aggregazioni hello**medio**</span><span class="sxs-lookup"><span data-stu-id="f13d3-272">Drag **engineTemparature** into **Y-Axis area**, change hello aggregation too**Average**</span></span>
5. <span data-ttu-id="f13d3-273">Hello trascinare **VPN** campo in hello **dimensioni** area.</span><span class="sxs-lookup"><span data-stu-id="f13d3-273">Drag hello **vin** field into hello **Size** area.</span></span>

![Automobili connesse: aggiungi nuova visualizzazione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

<span data-ttu-id="f13d3-275">Grafico hello modifica **titolo** troppo**"Medie di carburante, temperatura motore dal modello"**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-275">Change hello chart **Title** too**“Averages of Fuel, Engine Temperature by Model”**.</span></span>

![Automobili connesse: modifica titolo del grafico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

<span data-ttu-id="f13d3-277">report finale Hello apparirà come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="f13d3-277">hello final report will look like as shown below.</span></span>

![Automobili connesse: report finale](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-hello-reports-toohello-real-time-dashboard"></a><span data-ttu-id="f13d3-279">Visualizzazioni di pin di dashboard in tempo reale di hello report toohello</span><span class="sxs-lookup"><span data-stu-id="f13d3-279">Pin visualizations from hello reports toohello real-time dashboard</span></span>
<span data-ttu-id="f13d3-280">Creare un dashboard vuoto da facendo clic sull'icona di addizione hello tooDashboards successivo.</span><span class="sxs-lookup"><span data-stu-id="f13d3-280">Create a blank dashboard by clicking on hello plus icon next tooDashboards.</span></span> <span data-ttu-id="f13d3-281">È possibile denominarlo "Dashboard di analisi dei dati di telemetria di veicolo".</span><span class="sxs-lookup"><span data-stu-id="f13d3-281">You can name it “Vehicle Telemetry Analytics Dashboard”</span></span>

![Automobili connesse: dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

<span data-ttu-id="f13d3-283">Visualizzazione di hello pin da hello sopra dashboard toohello di report.</span><span class="sxs-lookup"><span data-stu-id="f13d3-283">Pin hello visualization from hello above reports toohello dashboard.</span></span> 

![Automobili connesse: dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

<span data-ttu-id="f13d3-285">Quando tutti hello tre report vengono creati e hello corrispondente visualizzazioni dashboard toohello bloccati, dashboard Hello dovrebbe apparire come segue.</span><span class="sxs-lookup"><span data-stu-id="f13d3-285">hello dashboard should look as follows when all hello three reports are created and hello corresponding visualizations are pinned toohello dashboard.</span></span> <span data-ttu-id="f13d3-286">Se non è stato creato tutti i report di hello, il dashboard potrebbe essere diverso.</span><span class="sxs-lookup"><span data-stu-id="f13d3-286">If you have not created all hello reports, your dashboard could look different.</span></span> 

![Automobili connesse: dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

<span data-ttu-id="f13d3-288">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="f13d3-288">Congratulations!</span></span> <span data-ttu-id="f13d3-289">Dashboard in tempo reale hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="f13d3-289">You have successfully created hello real-time dashboard.</span></span> <span data-ttu-id="f13d3-290">Mentre si continua a tooexecute CarEventGenerator.exe e RealtimeDashboardApp.exe, vedrai aggiornamenti in tempo reale nel dashboard di hello.</span><span class="sxs-lookup"><span data-stu-id="f13d3-290">As you continue tooexecute CarEventGenerator.exe and RealtimeDashboardApp.exe, you should see live updates on hello dashboard.</span></span> <span data-ttu-id="f13d3-291">Occorrere hello di toocomplete too15 circa 10 minuti alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="f13d3-291">It should take about 10 too15 minutes toocomplete hello following steps.</span></span>

## <a name="setup-power-bi-batch-processing-dashboard"></a><span data-ttu-id="f13d3-292">Configurare il dashboard di elaborazione batch di PowerBI</span><span class="sxs-lookup"><span data-stu-id="f13d3-292">Setup Power BI batch processing dashboard</span></span>
> [!NOTE]
> <span data-ttu-id="f13d3-293">Accetta circa due ore (da hello corretto completamento di distribuzione hello) per il batch di tooend fine hello esecuzione toofinish della pipeline di elaborazione e l'elaborazione di un valore di anno di dati generati.</span><span class="sxs-lookup"><span data-stu-id="f13d3-293">It takes about two hours (from hello successful completion of hello deployment) for hello end tooend batch processing pipeline toofinish execution and process a year worth of generated data.</span></span> <span data-ttu-id="f13d3-294">Pertanto si consiglia di attendere hello toofinish prima di procedere con passaggi successivi hello di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="f13d3-294">So wait for hello processing toofinish before proceeding with hello next steps.</span></span> 
> 
> 

<span data-ttu-id="f13d3-295">**Scaricare il file della finestra di progettazione di Power BI hello**</span><span class="sxs-lookup"><span data-stu-id="f13d3-295">**Download hello Power BI designer file**</span></span>

* <span data-ttu-id="f13d3-296">Un file della finestra di progettazione di Power BI configurati in precedenza è incluso come parte della distribuzione hello istruzioni operazione manuale</span><span class="sxs-lookup"><span data-stu-id="f13d3-296">A pre-configured Power BI designer file is included as part of hello deployment Manual Operation Instructions</span></span>
* <span data-ttu-id="f13d3-297">Cercare 2.</span><span class="sxs-lookup"><span data-stu-id="f13d3-297">Look for 2.</span></span> <span data-ttu-id="f13d3-298">Dashboard di elaborazione batch di installazione Power BI è possibile scaricare il modello di Power BI hello per l'elaborazione batch dashboard denominate **ConnectedCarsPbiReport.pbix**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-298">Setup PowerBI batch processing dashboard You can download hello PowerBI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span></span>
* <span data-ttu-id="f13d3-299">Salvare in locale</span><span class="sxs-lookup"><span data-stu-id="f13d3-299">Save locally</span></span>

<span data-ttu-id="f13d3-300">**Configurare i report di Power BI**</span><span class="sxs-lookup"><span data-stu-id="f13d3-300">**Configure Power BI reports**</span></span>

* <span data-ttu-id="f13d3-301">File di progettazione aprire hello '**ConnectedCarsPbiReport.pbix**' con Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="f13d3-301">Open hello designer file ‘**ConnectedCarsPbiReport.pbix**’ using Power BI Desktop.</span></span> <span data-ttu-id="f13d3-302">Se non si dispone, installa hello Power BI Desktop dal [installare Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="f13d3-302">If you do not already have, install hello Power BI Desktop from [Power BI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span></span> 
* <span data-ttu-id="f13d3-303">Fare clic su hello **modifica query**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-303">Click hello **Edit Queries**.</span></span>

![Modificare la query di Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* <span data-ttu-id="f13d3-305">Fare doppio clic su hello **origine**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-305">Double-click hello **Source**.</span></span>

![Impostare l'origine di Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* <span data-ttu-id="f13d3-307">Aggiornare la stringa di connessione Server con hello Azure SQL server in cui è stato eseguito il provisioning come parte della distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="f13d3-307">Update Server connection string with hello Azure SQL server that got provisioned as part of hello deployment.</span></span>  <span data-ttu-id="f13d3-308">Cerca in istruzioni di operazione manuale hello in</span><span class="sxs-lookup"><span data-stu-id="f13d3-308">Look in hello Manual Operation Instructions under</span></span> 

    4. <span data-ttu-id="f13d3-309">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="f13d3-309">Azure SQL Database</span></span>
    
    * <span data-ttu-id="f13d3-310">Server: somethingsrv.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="f13d3-310">Server: somethingsrv.database.windows.net</span></span>
    * <span data-ttu-id="f13d3-311">Database: connectedcar</span><span class="sxs-lookup"><span data-stu-id="f13d3-311">Database: connectedcar</span></span>
    * <span data-ttu-id="f13d3-312">Nome utente: nome utente</span><span class="sxs-lookup"><span data-stu-id="f13d3-312">Username: username</span></span>
    * <span data-ttu-id="f13d3-313">Password: è possibile gestire la password di SQL Server dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f13d3-313">Password: You can manage your SQL server password from Azure portal</span></span>

* <span data-ttu-id="f13d3-314">Lasciare **Database** come *connectedcar*.</span><span class="sxs-lookup"><span data-stu-id="f13d3-314">Leave **Database** as *connectedcar*.</span></span>

![Impostare il database Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* <span data-ttu-id="f13d3-316">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-316">Click **OK**.</span></span>
* <span data-ttu-id="f13d3-317">Si noterà **credenziale Windows** scheda selezionata per impostazione predefinita, modificarla troppo**le credenziali del Database** facendo clic su **Database** scheda nella parte destra.</span><span class="sxs-lookup"><span data-stu-id="f13d3-317">You will see **Windows credential** tab selected by default, change it too**Database credentials** by clicking on **Database** tab at right.</span></span>
* <span data-ttu-id="f13d3-318">Fornire hello **Username** e **Password** di Database SQL di Azure che è stato specificato durante il programma di installazione di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f13d3-318">Provide hello **Username** and **Password** of your Azure SQL Database that was specified during its deployment setup.</span></span>

![Ottenere le credenziali del database](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* <span data-ttu-id="f13d3-320">Fare clic su **Connetti**</span><span class="sxs-lookup"><span data-stu-id="f13d3-320">Click **Connect**</span></span>
* <span data-ttu-id="f13d3-321">Ripetere hello sopra i passaggi per ogni query hello tre rimanenti presenti nel riquadro destro e quindi aggiornare i dettagli di connessione origine dati hello.</span><span class="sxs-lookup"><span data-stu-id="f13d3-321">Repeat hello above steps for each of hello three remaining queries present at right pane, and then update hello data source connection details.</span></span>
* <span data-ttu-id="f13d3-322">Fare clic su **Chiudi e carica**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-322">Click **Close and Load**.</span></span> <span data-ttu-id="f13d3-323">Set di file di dati di Power BI Desktop sono tabelle di Database di Azure tooSQL connesso.</span><span class="sxs-lookup"><span data-stu-id="f13d3-323">Power BI Desktop file datasets are connected tooSQL Azure Database tables.</span></span>
* <span data-ttu-id="f13d3-324">**Chiudi** per chiudere il file Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="f13d3-324">**Close** Power BI Desktop file.</span></span>

![Chiudere Power BI Desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* <span data-ttu-id="f13d3-326">Fare clic su **salvare** pulsante modifiche hello toosave.</span><span class="sxs-lookup"><span data-stu-id="f13d3-326">Click **Save** button toosave hello changes.</span></span> 

<span data-ttu-id="f13d3-327">È stato configurato tutti i report di hello toohello percorso di elaborazione batch nella soluzione hello corrispondente.</span><span class="sxs-lookup"><span data-stu-id="f13d3-327">You have now configured all hello reports corresponding toohello batch processing path in hello solution.</span></span> 

## <a name="upload-toopowerbicom"></a><span data-ttu-id="f13d3-328">Caricare troppo*powerbi.com*</span><span class="sxs-lookup"><span data-stu-id="f13d3-328">Upload too*powerbi.com*</span></span>
1. <span data-ttu-id="f13d3-329">Passare portale web di Power BI toohello http://powerbi.com e account di accesso.</span><span class="sxs-lookup"><span data-stu-id="f13d3-329">Navigate toohello Power BI web portal at http://powerbi.com and login.</span></span>
2. <span data-ttu-id="f13d3-330">Fare clic su **Recupera dati**</span><span class="sxs-lookup"><span data-stu-id="f13d3-330">Click **Get Data**</span></span>  
3. <span data-ttu-id="f13d3-331">Caricare il File di Power BI Desktop hello.</span><span class="sxs-lookup"><span data-stu-id="f13d3-331">Upload hello Power BI Desktop File.</span></span>  
4. <span data-ttu-id="f13d3-332">tooupload, fare clic su **recupera dati -> ottenere file -> file locale**</span><span class="sxs-lookup"><span data-stu-id="f13d3-332">tooupload, click **Get Data -> Files Get -> Local file**</span></span>  
5. <span data-ttu-id="f13d3-333">Passare toohello **"**ConnectedCarsPbiReport.pbix**"**</span><span class="sxs-lookup"><span data-stu-id="f13d3-333">Navigate toohello **“**ConnectedCarsPbiReport.pbix**”**</span></span>  
6. <span data-ttu-id="f13d3-334">Una volta caricato il file hello, sarà tooyour indietro spostarsi area di lavoro di Power BI.</span><span class="sxs-lookup"><span data-stu-id="f13d3-334">Once hello file is uploaded, you will be navigated back tooyour Power BI work space.</span></span>  

<span data-ttu-id="f13d3-335">Verranno creati automaticamente un set di dati, un report e un dashboard vuoto.</span><span class="sxs-lookup"><span data-stu-id="f13d3-335">A dataset, report and a blank dashboard will be created for you.</span></span>  

<span data-ttu-id="f13d3-336">PIN grafici tooa nuovo dashboard chiamato **veicolo telemetria Analitica Dashboard** in **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="f13d3-336">Pin charts tooa new dashboard called **Vehicle Telemetry Analytics Dashboard** in **Power BI**.</span></span> <span data-ttu-id="f13d3-337">Fare clic su dashboard di hello vuoto creato in precedenza e quindi passare toohello **report** fare clic su sezione hello appena caricato report.</span><span class="sxs-lookup"><span data-stu-id="f13d3-337">Click hello blank dashboard created above and then navigate toohello **Reports** section click hello newly uploaded report.</span></span>  

![Vehicle Telemetry Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

<span data-ttu-id="f13d3-339">**Nota hello report ha sei pagine:**</span><span class="sxs-lookup"><span data-stu-id="f13d3-339">**Note hello report has six pages:**</span></span>  
<span data-ttu-id="f13d3-340">Pagina 1: Densità veicolo</span><span class="sxs-lookup"><span data-stu-id="f13d3-340">Page 1: Vehicle density</span></span>  
<span data-ttu-id="f13d3-341">Pagina 2: Integrità veicolo in tempo reale</span><span class="sxs-lookup"><span data-stu-id="f13d3-341">Page 2: Real-time vehicle health</span></span>  
<span data-ttu-id="f13d3-342">Pagina 3: Veicoli guidati in modo aggressivo</span><span class="sxs-lookup"><span data-stu-id="f13d3-342">Page 3: Aggressively Driven Vehicles</span></span>   
<span data-ttu-id="f13d3-343">Pagina 4: Veicoli richiamati</span><span class="sxs-lookup"><span data-stu-id="f13d3-343">Page 4: Recalled vehicles</span></span>  
<span data-ttu-id="f13d3-344">Pagina 5: Veicoli con consumo di carburante efficiente</span><span class="sxs-lookup"><span data-stu-id="f13d3-344">Page 5: Fuel Efficiently Driven Vehicles</span></span>  
<span data-ttu-id="f13d3-345">Pagina 6: Logo di Contoso</span><span class="sxs-lookup"><span data-stu-id="f13d3-345">Page 6: Contoso Logo</span></span>  

![Connected Cars Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

<span data-ttu-id="f13d3-347">**Dalla pagina 3**, aggiungere il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="f13d3-347">**From Page 3**, pin hello following:</span></span>  

1. <span data-ttu-id="f13d3-348">Count of vin</span><span class="sxs-lookup"><span data-stu-id="f13d3-348">Count of VIN</span></span>  
   ![Connected Cars Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. <span data-ttu-id="f13d3-350">Veicoli guidati in modo aggressivo in base al modello: grafico a cascata </span><span class="sxs-lookup"><span data-stu-id="f13d3-350">Aggressively driven vehicles by model – Waterfall chart</span></span>  
   ![Telemetria veicolo: aggiungi grafici 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

<span data-ttu-id="f13d3-352">**Dalla pagina 5**, aggiungere il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="f13d3-352">**From Page 5**, pin hello following:</span></span> 

1. <span data-ttu-id="f13d3-353">Count of vin</span><span class="sxs-lookup"><span data-stu-id="f13d3-353">Count of vin</span></span>    
   ![Telemetria veicolo: aggiungi grafici 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. <span data-ttu-id="f13d3-355">Veicoli guidati con un consumo efficiente del carburante in base al modello: istogramma a colonne raggruppate </span><span class="sxs-lookup"><span data-stu-id="f13d3-355">Fuel efficient vehicles by model: Clustered column chart</span></span>  
   ![Telemetria veicolo: aggiungi grafici 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

<span data-ttu-id="f13d3-357">**Dalla pagina 4**, aggiungere il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="f13d3-357">**From Page 4**, pin hello following:</span></span>  

1. <span data-ttu-id="f13d3-358">Count of vin</span><span class="sxs-lookup"><span data-stu-id="f13d3-358">Count of vin</span></span>  
   ![Telemetria veicolo: aggiungi grafici 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. <span data-ttu-id="f13d3-360">Veicoli richiamati in base alla città e al modello: grafico ad albero </span><span class="sxs-lookup"><span data-stu-id="f13d3-360">Recalled vehicles by city, model: Treemap</span></span>  
   ![Telemetria veicolo: aggiungi grafici 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

<span data-ttu-id="f13d3-362">**Dalla pagina 6**, aggiungere il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="f13d3-362">**From Page 6**, pin hello following:</span></span>  

1. <span data-ttu-id="f13d3-363">Logo Contoso Motors </span><span class="sxs-lookup"><span data-stu-id="f13d3-363">Contoso Motors logo</span></span>  
   ![Telemetria veicolo: aggiungi grafici 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

<span data-ttu-id="f13d3-365">**Organizzare il dashboard di hello**</span><span class="sxs-lookup"><span data-stu-id="f13d3-365">**Organize hello dashboard**</span></span>  

1. <span data-ttu-id="f13d3-366">Passare toohello dashboard</span><span class="sxs-lookup"><span data-stu-id="f13d3-366">Navigate toohello dashboard</span></span>
2. <span data-ttu-id="f13d3-367">Passare il mouse su ogni grafico e rinominarlo in base a denominazione hello fornito nell'immagine di un dashboard completo hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="f13d3-367">Hover over each chart and rename it based on hello naming provided in hello complete dashboard image below.</span></span> <span data-ttu-id="f13d3-368">Spostare anche i grafici di hello intorno toolook come dashboard hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="f13d3-368">Also move hello charts around toolook like hello dashboard below.</span></span>  
   ![Telemetria veicolo: organizza dashboard 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Vehicle Telemetry Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. <span data-ttu-id="f13d3-371">Se è stato creato tutti i report di hello, come indicato in questo documento, hello finale dashboard completato dovrebbe essere simile hello seguente illustrazione.</span><span class="sxs-lookup"><span data-stu-id="f13d3-371">If you have created all hello reports as mentioned in this document, hello final completed dashboard should look like hello following figure.</span></span> 

![Telemetria veicolo: organizza dashboard 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

<span data-ttu-id="f13d3-373">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="f13d3-373">Congratulations!</span></span> <span data-ttu-id="f13d3-374">Sono stati creati correttamente i report di hello e hello toogain dashboard in tempo reale, predittiva e abitudini di insights di batch su integrità veicolo e la Guida.</span><span class="sxs-lookup"><span data-stu-id="f13d3-374">You have successfully created hello reports and hello dashboard toogain real-time, predictive and batch insights on vehicle health and driving habits.</span></span>  
