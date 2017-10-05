---
title: "Dashboard di Power BI sull'integrità dei veicoli e sulle abitudini di guida - Azure | Documentazione Microsoft"
description: "Usare le funzionalità di Cortana Intelligence per ottenere informazioni dettagliate predittive e in tempo reale sullo stato di integrità del veicolo e sulle abitudini di guida."
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
ms.openlocfilehash: f880aceb1657ffdfe909b73f175b9673d9ab02cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a><span data-ttu-id="1b877-103">Istruzioni di configurazione del dashboard di Power BI per il modello di soluzione per l'analisi dei dati di telemetria del veicolo</span><span class="sxs-lookup"><span data-stu-id="1b877-103">Vehicle telemetry analytics solution template Power BI Dashboard setup instructions</span></span>
<span data-ttu-id="1b877-104">Questo **menu** contiene i collegamenti alle sezioni dello studio.</span><span class="sxs-lookup"><span data-stu-id="1b877-104">This **menu** links to the chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="1b877-105">La soluzione per l'analisi dei dati di telemetria del veicolo illustra come le concessionarie d'auto, i produttori di automobili e le compagnie di assicurazione possano sfruttare le funzionalità di Cortana Intelligence per ottenere informazioni dettagliate predittive e in tempo reale sullo stato di integrità del veicolo e sulle abitudini di guida in modo da apportare miglioramenti nelle aree dell'esperienza cliente, di ricerca e sviluppo e delle campagne di marketing.</span><span class="sxs-lookup"><span data-stu-id="1b877-105">The Vehicle Telemetry Analytics solution showcases how car dealerships, automobile manufacturers and insurance companies can leverage the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits to drive improvements in the area of customer experience, R&D and marketing campaigns.</span></span> <span data-ttu-id="1b877-106">Questo documento contiene istruzioni dettagliate su come configurare i report e il dashboard di Power BI dopo la distribuzione della soluzione nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="1b877-106">This document contains step by step instructions on how you can configure the Power BI reports and dashboard once the solution is deployed in your subscription.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1b877-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1b877-107">Prerequisites</span></span>
1. <span data-ttu-id="1b877-108">Distribuire la soluzione per l'[analisi dei dati di telemetria](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90)</span><span class="sxs-lookup"><span data-stu-id="1b877-108">Deploy the [Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solution</span></span>  
2. [<span data-ttu-id="1b877-109">Installare Microsoft Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="1b877-109">Install Microsoft Power BI Desktop</span></span>](http://www.microsoft.com/download/details.aspx?id=45331)
3. <span data-ttu-id="1b877-110">Una [sottoscrizione di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1b877-110">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="1b877-111">Se non si dispone di una sottoscrizione Azure, iniziare con una sottoscrizione gratuita di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b877-111">If you don't have an Azure subscription, get started with Azure free subscription</span></span>
4. <span data-ttu-id="1b877-112">Account di Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="1b877-112">Microsoft Power BI account</span></span>

## <a name="cortana-intelligence-suite-components"></a><span data-ttu-id="1b877-113">Componenti di Cortana Intelligence Suite</span><span class="sxs-lookup"><span data-stu-id="1b877-113">Cortana Intelligence Suite Components</span></span>
<span data-ttu-id="1b877-114">Come parte del modello di soluzione per l'analisi dei dati di telemetria del veicolo, nella sottoscrizione vengono distribuiti i servizi di Cortana Intelligence seguenti.</span><span class="sxs-lookup"><span data-stu-id="1b877-114">As part of the Vehicle Telemetry Analytics solution template, the following Cortana Intelligence services are deployed in your subscription.</span></span>

* <span data-ttu-id="1b877-115">**Hub eventi** per l'inserimento di milioni di eventi di telemetria del veicolo in Azure.</span><span class="sxs-lookup"><span data-stu-id="1b877-115">**Event Hub** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="1b877-116">**Analisi di flusso** per ottenere informazioni dettagliate in tempo reale sul funzionamento del veicolo e salvare i dati in modo permanente nello spazio di archiviazione a lungo termine per un'analisi batch avanzata.</span><span class="sxs-lookup"><span data-stu-id="1b877-116">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="1b877-117">**Machine Learning** per il rilevamento di anomalie in tempo reale e l'elaborazione batch per ottenere informazioni predittive.</span><span class="sxs-lookup"><span data-stu-id="1b877-117">**Machine Learning** for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="1b877-118">**HDInsight** per trasformare i dati su larga scala</span><span class="sxs-lookup"><span data-stu-id="1b877-118">**HDInsight** is leveraged to transform data at scale</span></span>
* <span data-ttu-id="1b877-119">**Data Factory** gestisce l'orchestrazione, la pianificazione, la gestione delle risorse e il monitoraggio della pipeline di elaborazione batch.</span><span class="sxs-lookup"><span data-stu-id="1b877-119">**Data Factory** handles orchestration, scheduling, resource management and monitoring of the batch processing pipeline.</span></span>

<span data-ttu-id="1b877-120">**Power BI** offre alla soluzione un dashboard completo per la visualizzazione di dati in tempo reale e di analisi predittiva.</span><span class="sxs-lookup"><span data-stu-id="1b877-120">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="1b877-121">La soluzione usa due origini dati diverse: **segnali del veicolo e set di dati di diagnostica simulati** e **catalogo dei veicoli**.</span><span class="sxs-lookup"><span data-stu-id="1b877-121">The solution uses two different data sources: **Simulated vehicle signals and diagnostic dataset** and **vehicle catalog**.</span></span>

<span data-ttu-id="1b877-122">Nella soluzione è incluso un simulatore di dati telematici relativi al veicolo.</span><span class="sxs-lookup"><span data-stu-id="1b877-122">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="1b877-123">Il simulatore genera informazioni di diagnostica e segnali corrispondenti allo stato del veicolo e allo schema di guida in un determinato momento.</span><span class="sxs-lookup"><span data-stu-id="1b877-123">It emits diagnostic information and signals corresponding to the state of the vehicle and driving pattern at a given point in time.</span></span> 

<span data-ttu-id="1b877-124">Il catalogo del veicolo è un set di dati di riferimento contenente il numero di identificazione del veicolo per il mapping del modello.</span><span class="sxs-lookup"><span data-stu-id="1b877-124">The Vehicle Catalog is a reference dataset containing VIN to model mapping</span></span>

## <a name="power-bi-dashboard-preparation"></a><span data-ttu-id="1b877-125">Preparazione del dashboard di Power BI</span><span class="sxs-lookup"><span data-stu-id="1b877-125">Power BI Dashboard Preparation</span></span>
### <a name="setup-power-bi-real-time-dashboard"></a><span data-ttu-id="1b877-126">Configurare il dashboard in tempo reale di Power BI</span><span class="sxs-lookup"><span data-stu-id="1b877-126">Setup Power BI Real-Time Dashboard</span></span>

<span data-ttu-id="1b877-127">**Avviare l'applicazione dashboard in tempo reale** Dopo aver completato la distribuzione, è necessario seguire le istruzioni di funzionamento manuale</span><span class="sxs-lookup"><span data-stu-id="1b877-127">**Start the real-time dashboard application** Once the deployment is completed, you should follow the Manual Operation Instructions</span></span>

* <span data-ttu-id="1b877-128">Scaricare l'applicazione dashboard in tempo reale RealtimeDashboardApp.zip e decomprimere il file.</span><span class="sxs-lookup"><span data-stu-id="1b877-128">Download real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span></span>
*  <span data-ttu-id="1b877-129">Nella cartella non compressa, aprire il file di configurazione app 'RealtimeDashboardApp.exe.config', sostituire appSettings per hub eventi, archiviazione BLOB e connessioni al servizio ML con i valori indicati nelle istruzioni di funzionamento manuale e salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="1b877-129">In the unzipped folder, open app config file 'RealtimeDashboardApp.exe.config', replace appSettings for Eventhub, Blob Storage, and ML service connections with the values in the Manual Operation Instructions, and save your changes.</span></span>
* <span data-ttu-id="1b877-130">Eseguire l'applicazione RealtimeDashboardApp.exe.</span><span class="sxs-lookup"><span data-stu-id="1b877-130">Run application RealtimeDashboardApp.exe.</span></span> <span data-ttu-id="1b877-131">Specificare le credenziali di Power BI valide nella finestra di accesso visualizzata e fare clic sul pulsante **Accetto**.</span><span class="sxs-lookup"><span data-stu-id="1b877-131">A login window will pop up, provide your valid PowerBI credentials and click the **Accept** button.</span></span> <span data-ttu-id="1b877-132">Viene avviata l'esecuzione dell'app.</span><span class="sxs-lookup"><span data-stu-id="1b877-132">Then the app will start to run.</span></span>

   ![Accedere a Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Autorizzazioni per il dashboard di Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* <span data-ttu-id="1b877-135">Accedere al sito Web di Power BI e creare dashboard in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="1b877-135">Login to PowerBI website, and create real-time dashboard.</span></span>

<span data-ttu-id="1b877-136">A questo punto si è pronti per configurare il dashboard di Power BI con visualizzazioni avanzate, per ottenere informazioni dettagliate predittive e in tempo reale sull'integrità del veicolo e sulle abitudini di guida.</span><span class="sxs-lookup"><span data-stu-id="1b877-136">Now, you are ready to configure the Power BI dashboard with rich visualizations to gain real-time and predictive insights on vehicle health and driving habits.</span></span> <span data-ttu-id="1b877-137">Per creare tutti i report e configurare il dashboard, sono necessari da circa 45 minuti a un'ora.</span><span class="sxs-lookup"><span data-stu-id="1b877-137">It takes about 45 minutes to an hour to create all the reports and configure the dashboard.</span></span> 

### <a name="configure-power-bi-reports"></a><span data-ttu-id="1b877-138">Configurare i report di Power BI</span><span class="sxs-lookup"><span data-stu-id="1b877-138">Configure Power BI reports</span></span>
<span data-ttu-id="1b877-139">Il completamento dei report in tempo reale e del dashboard richiede circa 30-45 minuti.</span><span class="sxs-lookup"><span data-stu-id="1b877-139">The real-time reports and the dashboard take about 30-45 minutes to complete.</span></span> <span data-ttu-id="1b877-140">Passare a [http://powerbi.com](http://powerbi.com) e accedere.</span><span class="sxs-lookup"><span data-stu-id="1b877-140">Browse to [http://powerbi.com](http://powerbi.com) and login.</span></span>

![Accedere a Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

<span data-ttu-id="1b877-142">Viene generato un nuovo set di dati in Power BI.</span><span class="sxs-lookup"><span data-stu-id="1b877-142">A new dataset is generated in Power BI.</span></span> <span data-ttu-id="1b877-143">Fare clic sul set di dati **ConnectedCarsRealtime**.</span><span class="sxs-lookup"><span data-stu-id="1b877-143">Click the **ConnectedCarsRealtime** dataset.</span></span>

![Selezionare il set di dati in tempo reale delle automobili connesse](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

<span data-ttu-id="1b877-145">Salvare il report vuoto premendo **CTRL+S**.</span><span class="sxs-lookup"><span data-stu-id="1b877-145">Save the blank report using **Ctrl + s**.</span></span>

![Salvare il report vuoto](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

<span data-ttu-id="1b877-147">Specificare il nome del report *Analisi dei dati di telemetria del veicolo in tempo reale - Report*.</span><span class="sxs-lookup"><span data-stu-id="1b877-147">Provide report name *Vehicle Telemetry Analytics Real-time - Reports*.</span></span>

![Specificare il nome del report](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a><span data-ttu-id="1b877-149">Report in tempo reale</span><span class="sxs-lookup"><span data-stu-id="1b877-149">Real-time reports</span></span>
<span data-ttu-id="1b877-150">Questa soluzione include tre report in tempo reale:</span><span class="sxs-lookup"><span data-stu-id="1b877-150">There are three real-time reports in this solution:</span></span>

1. <span data-ttu-id="1b877-151">Veicoli operativi</span><span class="sxs-lookup"><span data-stu-id="1b877-151">Vehicles in operation</span></span>
2. <span data-ttu-id="1b877-152">Veicoli che richiedono manutenzione</span><span class="sxs-lookup"><span data-stu-id="1b877-152">Vehicles Requiring Maintenance</span></span>
3. <span data-ttu-id="1b877-153">Statistiche sull'integrità dei veicoli</span><span class="sxs-lookup"><span data-stu-id="1b877-153">Vehicles Health Statistics</span></span>

<span data-ttu-id="1b877-154">È possibile scegliere di configurare tutti e tre i report in tempo reale o interrompere la procedura dopo ogni fase e passare alla successiva sezione di configurazione dei report in batch.</span><span class="sxs-lookup"><span data-stu-id="1b877-154">You can choose to configure all the three real-time reports or stop after any stage and proceed to the next section of configuring the batch reports.</span></span> <span data-ttu-id="1b877-155">È consigliabile creare tutti e tre i report per visualizzare le informazioni dettagliate complete del percorso in tempo reale della soluzione.</span><span class="sxs-lookup"><span data-stu-id="1b877-155">We recommend you to create all the three reports to visualize the full insights of the real-time path of the solution.</span></span>  

### <a name="1-vehicles-in-operation"></a><span data-ttu-id="1b877-156">1. Veicoli operativi</span><span class="sxs-lookup"><span data-stu-id="1b877-156">1. Vehicles in operation</span></span>
<span data-ttu-id="1b877-157">Fare doppio clic su **Pagina 1** e rinominarla "Veicoli operativi"</span><span class="sxs-lookup"><span data-stu-id="1b877-157">Double-click **Page 1** and rename it to “Vehicles in operation”</span></span>  
    <span data-ttu-id="1b877-158">![Automobili connesse: veicoli operativi](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span><span class="sxs-lookup"><span data-stu-id="1b877-158">![Connected Cars - Vehicles in operation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span></span>  

<span data-ttu-id="1b877-159">Selezionare il campo **vin** da **Fields** e scegliere **"Card"** come tipo di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="1b877-159">Select **vin** field from **Fields** and choose visualization type as **“Card”**.</span></span>  

<span data-ttu-id="1b877-160">Viene creata una visualizzazione di tipo scheda come illustrato nella figura.</span><span class="sxs-lookup"><span data-stu-id="1b877-160">Card visualization is created as shown in figure.</span></span>  
    ![Automobili connesse: seleziona vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

<span data-ttu-id="1b877-162">Fare clic sull'area vuota per aggiungere una nuova visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="1b877-162">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="1b877-163">Selezionare **Città** e **vin** dai campi.</span><span class="sxs-lookup"><span data-stu-id="1b877-163">Select **City** and **vin** from fields.</span></span> <span data-ttu-id="1b877-164">Cambiare la visualizzazione in **"Map"**.</span><span class="sxs-lookup"><span data-stu-id="1b877-164">Change visualization to **“Map”**.</span></span> <span data-ttu-id="1b877-165">Trascinare **vin** nell'area valori.</span><span class="sxs-lookup"><span data-stu-id="1b877-165">Drag **vin** in values area.</span></span> <span data-ttu-id="1b877-166">Trascinare **città** dai campi nell'area **Legenda**.</span><span class="sxs-lookup"><span data-stu-id="1b877-166">Drag **city** from fields to **Legend** area.</span></span>   
    <span data-ttu-id="1b877-167">![Automobili connesse: visualizzazione scheda](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span><span class="sxs-lookup"><span data-stu-id="1b877-167">![Connected Cars - Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span></span>

<span data-ttu-id="1b877-168">Selezionare la sezione **Formato** da **Visualizzazioni**, fare clic su **Titolo** e modificare il **testo** in **"Veicoli operativi in base alla città"**.</span><span class="sxs-lookup"><span data-stu-id="1b877-168">Select **format** section from **Visualizations**, click **Title** and change the **Text** to **“Vehicles in operation by city”**.</span></span>  
    <span data-ttu-id="1b877-169">![Automobili connesse: veicoli operativi in base alla città](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span><span class="sxs-lookup"><span data-stu-id="1b877-169">![Connected Cars - Vehicles in operation by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span></span>   

<span data-ttu-id="1b877-170">La visualizzazione finale è simile a quella illustrata nella figura.</span><span class="sxs-lookup"><span data-stu-id="1b877-170">Final visualization looks as shown in figure.</span></span>    
    ![Automobili connesse: visualizzazione finale](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

<span data-ttu-id="1b877-172">Fare clic sull'area vuota per aggiungere una nuova visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="1b877-172">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="1b877-173">Selezionare **Città** e **vin**, modificare il tipo di visualizzazione in **Istogramma a colonne raggruppate**.</span><span class="sxs-lookup"><span data-stu-id="1b877-173">Select **City** and **vin**, change visualization type to **Clustered Column Chart**.</span></span> <span data-ttu-id="1b877-174">Verificare che il campo **Città** sia nell'**area Asse** e **vin** nell'**area Valore**</span><span class="sxs-lookup"><span data-stu-id="1b877-174">Ensure **City** field in **Axis area** and **vin** in **Value area**</span></span>  

<span data-ttu-id="1b877-175">Ordinare il grafico in base a **"Count of vin"**</span><span class="sxs-lookup"><span data-stu-id="1b877-175">Sort chart by **“Count of vin”**</span></span>  
    <span data-ttu-id="1b877-176">![Automobili connesse: conteggio di vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span><span class="sxs-lookup"><span data-stu-id="1b877-176">![Connected Cars - Count of vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span></span>  

<span data-ttu-id="1b877-177">Modificare il campo **Titolo** del grafico in **"Veicoli operativi per città"**</span><span class="sxs-lookup"><span data-stu-id="1b877-177">Change chart **Title** to **“Vehicles in operation by city”**</span></span>  

<span data-ttu-id="1b877-178">Fare clic sulla sezione **Formato**, quindi selezionare **Colori dati** e in **Mostra tutto** fare clic su **"Attiva"**</span><span class="sxs-lookup"><span data-stu-id="1b877-178">Click the **Format** section, then select **Data Colors**,  Click the **“On”** to **Show All**</span></span>  
    <span data-ttu-id="1b877-179">![Automobili connesse: mostra tutti i colori dei dati](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span><span class="sxs-lookup"><span data-stu-id="1b877-179">![Connected Cars - Show all Data Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span></span>  

<span data-ttu-id="1b877-180">Modificare il colore delle singole città facendo clic sull'icona del colore.</span><span class="sxs-lookup"><span data-stu-id="1b877-180">Change the color of individual city by clicking on color icon.</span></span>  
    ![Automobili connesse: modifica colori](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

<span data-ttu-id="1b877-182">Fare clic sull'area vuota per aggiungere una nuova visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="1b877-182">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="1b877-183">Dalle visualizzazioni selezionare **Istogramma a colonne raggruppate**, trascinare il campo **città** nell'area **Asse**, **Modello** nell'area **Legenda** e **vin** nell'area **Valore**.</span><span class="sxs-lookup"><span data-stu-id="1b877-183">Select **Clustered Column Chart** visualization from visualizations, drag **city** field in **Axis** area, **Model** in **Legend** area and **vin** in **Value** area.</span></span>  
    <span data-ttu-id="1b877-184">![Automobili connesse: istogramma a colonne raggruppate](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span><span class="sxs-lookup"><span data-stu-id="1b877-184">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span></span>  
    <span data-ttu-id="1b877-185">![Automobili connesse: rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span><span class="sxs-lookup"><span data-stu-id="1b877-185">![Connected Cars - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span></span>

<span data-ttu-id="1b877-186">Ridisporre la visualizzazione nella pagina come illustrato nella figura.</span><span class="sxs-lookup"><span data-stu-id="1b877-186">Rearrange all visualization on this page as shown in figure.</span></span>  
    ![Automobili connesse: visualizzazioni](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

<span data-ttu-id="1b877-188">Il report in tempo reale "Veicoli operativi" è stato configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="1b877-188">You have successfully configured the “Vehicles in operation” real-time report.</span></span> <span data-ttu-id="1b877-189">È possibile procedere per creare il report in tempo reale successivo o interrompere la procedura e configurare il dashboard.</span><span class="sxs-lookup"><span data-stu-id="1b877-189">You can proceed to create the next real-time report or stop here and configure the dashboard.</span></span> 

### <a name="2-vehicles-requiring-maintenance"></a><span data-ttu-id="1b877-190">2. Veicoli che richiedono manutenzione</span><span class="sxs-lookup"><span data-stu-id="1b877-190">2. Vehicles Requiring Maintenance</span></span>
<span data-ttu-id="1b877-191">Fare clic su ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) per aggiungere un nuovo report e rinominarlo **"Veicoli che richiedono manutenzione"**</span><span class="sxs-lookup"><span data-stu-id="1b877-191">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add a new report, rename it to **“Vehicles Requiring Maintenance”**</span></span>

![Automobili connesse: veicoli che richiedono manutenzione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

<span data-ttu-id="1b877-193">Selezionare il campo **vin** e modificare il tipo di visualizzazione in **Scheda**.</span><span class="sxs-lookup"><span data-stu-id="1b877-193">Select **vin** field and change visualization type to **Card**.</span></span>  
    <span data-ttu-id="1b877-194">![Automobili connesse: visualizzazione scheda vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span><span class="sxs-lookup"><span data-stu-id="1b877-194">![Connected Cars - Vin Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span></span>  

<span data-ttu-id="1b877-195">Nel set di dati è presente un campo denominato "MaintenanceLabel".</span><span class="sxs-lookup"><span data-stu-id="1b877-195">We have a field named “MaintenanceLabel” In the dataset.</span></span> <span data-ttu-id="1b877-196">Questo campo può avere un valore pari a "0" o "1".</span><span class="sxs-lookup"><span data-stu-id="1b877-196">This field can have a value of “0” or “1”.”</span></span> <span data-ttu-id="1b877-197">È impostato dal modello di Azure Machine Learning fornito come parte della soluzione e integrato nel percorso in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="1b877-197">It is set by the Azure Machine Learning model provisioned as part of solution and integrated with the real-time path.</span></span> <span data-ttu-id="1b877-198">Il valore "1" indica che un veicolo richiede manutenzione.</span><span class="sxs-lookup"><span data-stu-id="1b877-198">The value “1” indicates a vehicle requires maintenance.</span></span> 

<span data-ttu-id="1b877-199">Per aggiungere il filtro **Page Level** e visualizzare i dati relativi ai veicoli che richiedono manutenzione:</span><span class="sxs-lookup"><span data-stu-id="1b877-199">To add a **Page Level** filter for showing vehicles data, which are requiring maintenance:</span></span> 

1. <span data-ttu-id="1b877-200">Trascinare il campo **"MaintenanceLabel"** in **Filtri a livello di pagina**.</span><span class="sxs-lookup"><span data-stu-id="1b877-200">Drag the **“MaintenanceLabel”** field into **Page Level Filters**.</span></span>  
   <span data-ttu-id="1b877-201">![Automobili connesse: filtri del livello di pagina](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span><span class="sxs-lookup"><span data-stu-id="1b877-201">![Connected Cars - Page Level Filters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span></span>  
2. <span data-ttu-id="1b877-202">Fare clic sul menu **Basic Filtering** presente in basso nella schermata del filtro MaintenanceLabel in Page Level Filter.</span><span class="sxs-lookup"><span data-stu-id="1b877-202">Click **Basic Filtering** menu present at bottom of MaintenanceLabel Page Level Filter.</span></span>  
   <span data-ttu-id="1b877-203">![Automobili connesse: filtro base](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span><span class="sxs-lookup"><span data-stu-id="1b877-203">![Connected Cars - Basic Filtering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span></span>  
3. <span data-ttu-id="1b877-204">Impostare il valore del filtro su **"1"**  </span><span class="sxs-lookup"><span data-stu-id="1b877-204">Set its filter value to **“1”**  </span></span>  
   <span data-ttu-id="1b877-205">![Automobili connesse: valore di filtro](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span><span class="sxs-lookup"><span data-stu-id="1b877-205">![Connected Cars - Filter Value](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span></span>  

<span data-ttu-id="1b877-206">Fare clic sull'area vuota per aggiungere una nuova visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="1b877-206">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="1b877-207">Dalle visualizzazioni selezionare **Istogramma a colonne raggruppate**</span><span class="sxs-lookup"><span data-stu-id="1b877-207">Select **Clustered Column Chart** from visualizations</span></span>  
<span data-ttu-id="1b877-208">![Automobili connesse: visualizzazione scheda vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span><span class="sxs-lookup"><span data-stu-id="1b877-208">![Connected Cars - Vind Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span></span>  
<span data-ttu-id="1b877-209">![Automobili connesse: istogramma a colonne raggruppate](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span><span class="sxs-lookup"><span data-stu-id="1b877-209">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span></span>

<span data-ttu-id="1b877-210">Trascinare il campo **Modello** nell'area **Asse** e **vin** nell'area **Valore**.</span><span class="sxs-lookup"><span data-stu-id="1b877-210">Drag field **Model** into **Axis** area, **Vin** to **Value** area.</span></span> <span data-ttu-id="1b877-211">Ordinare quindi la visualizzazione in base a **Count of vin**.</span><span class="sxs-lookup"><span data-stu-id="1b877-211">Then sort visualization by **Count of vin**.</span></span>  <span data-ttu-id="1b877-212">Modificare il campo **Titolo** del grafico in **"Veicoli che richiedono manutenzione in base al modello"**</span><span class="sxs-lookup"><span data-stu-id="1b877-212">Change chart **Title** to **“Vehicles requiring maintenance by model”**</span></span>  

<span data-ttu-id="1b877-213">Trascinare i campi **vin** in **Saturazione colore** presente nella sezione **Campi** ![Campi](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) della scheda **Visualizzazione**</span><span class="sxs-lookup"><span data-stu-id="1b877-213">Drag **vin** fields into **Color Saturation** present at **Fields** ![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of **Visualization** tab</span></span>  
<span data-ttu-id="1b877-214">![Automobili connesse: saturazione dei colori](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span><span class="sxs-lookup"><span data-stu-id="1b877-214">![Connected Cars - Color Saturation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span></span>  

<span data-ttu-id="1b877-215">Modificare **Colori dati** nelle visualizzazioni dalla sezione **Formato**</span><span class="sxs-lookup"><span data-stu-id="1b877-215">Change **Data Colors** in visualizations from **Format** section</span></span>  
<span data-ttu-id="1b877-216">Cambiare il colore minimo in: **F2C812**</span><span class="sxs-lookup"><span data-stu-id="1b877-216">Change Minimum color to: **F2C812**</span></span>  
<span data-ttu-id="1b877-217">Cambiare il colore minimo in: **FF6300**</span><span class="sxs-lookup"><span data-stu-id="1b877-217">Change Maximum color to: **FF6300**</span></span>  
<span data-ttu-id="1b877-218">![Automobili connesse: modifiche dei colori](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span><span class="sxs-lookup"><span data-stu-id="1b877-218">![Connected Cars - Color Changes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span></span>  
<span data-ttu-id="1b877-219">![Automobili connesse: nuovi colori di visualizzazione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span><span class="sxs-lookup"><span data-stu-id="1b877-219">![Connected Cars - New Visualization Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span></span>  

<span data-ttu-id="1b877-220">Fare clic sull'area vuota per aggiungere una nuova visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="1b877-220">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="1b877-221">Selezionare **Istogramma a colonne raggruppate** dalle visualizzazioni, trascinare il campo **vin** nell'area **Valore** e il campo **Città** nell'area **Asse**.</span><span class="sxs-lookup"><span data-stu-id="1b877-221">Select **Clustered column chart** from visualizations, drag **vin** field into **Value** area, drag **City** field into **Axis** area.</span></span> <span data-ttu-id="1b877-222">Ordinare il grafico in base a **"Count of vin"**.</span><span class="sxs-lookup"><span data-stu-id="1b877-222">Sort chart by **“Count of vin”**.</span></span> <span data-ttu-id="1b877-223">Modificare il campo **Titolo** del grafico in **"Veicoli che richiedono manutenzione in base alla città"** </span><span class="sxs-lookup"><span data-stu-id="1b877-223">Change chart **Title** to **“Vehicles requiring maintenance by city”** </span></span>  
<span data-ttu-id="1b877-224">![Automobili connesse: veicoli che richiedono manutenzione in base alla città](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span><span class="sxs-lookup"><span data-stu-id="1b877-224">![Connected Cars - Vehicles requiring maintenance by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span></span>  

<span data-ttu-id="1b877-225">Fare clic sull'area vuota per aggiungere una nuova visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="1b877-225">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="1b877-226">Selezionare la visualizzazione **Scheda con più righe** dalle visualizzazioni, trascinare **Modello** e **vin** nell'area **Campi**.</span><span class="sxs-lookup"><span data-stu-id="1b877-226">Select **Multi-Row Card** visualization from visualizations, drag **Model** and **vin** into the **Fields** area.</span></span>  
<span data-ttu-id="1b877-227">![Automobili connesse: scheda con più righe](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span><span class="sxs-lookup"><span data-stu-id="1b877-227">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span></span>    

<span data-ttu-id="1b877-228">Ridisponendo tutte le visualizzazioni, il report finale avrà l'aspetto seguente: </span><span class="sxs-lookup"><span data-stu-id="1b877-228">Rearranging all of the visualization, the final report looks as follows:</span></span>  
![Automobili connesse: scheda con più righe](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

<span data-ttu-id="1b877-230">Il report in tempo reale "Veicoli che richiedono manutenzione" è stato configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="1b877-230">You have successfully configured the “Vehicles Requiring Maintenance” real-time report.</span></span> <span data-ttu-id="1b877-231">È possibile procedere per creare il report in tempo reale successivo o interrompere la procedura e configurare il dashboard.</span><span class="sxs-lookup"><span data-stu-id="1b877-231">You can proceed to create the next real-time report or stop here and configure the dashboard.</span></span> 

### <a name="3-vehicles-health-statistics"></a><span data-ttu-id="1b877-232">3. Statistiche sull'integrità dei veicoli</span><span class="sxs-lookup"><span data-stu-id="1b877-232">3. Vehicles Health Statistics</span></span>
<span data-ttu-id="1b877-233">Fare clic su ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) per aggiungere un nuovo report e rinominarlo **"Statistiche sull'integrità dei veicoli"**</span><span class="sxs-lookup"><span data-stu-id="1b877-233">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add new report, rename it to **“Vehicles Health Statistics”**</span></span>  

<span data-ttu-id="1b877-234">Selezionare la visualizzazione **Misuratore** dalle visualizzazioni, quindi trascinare il campo **Velocità** nelle aree **Valore, Valore minimo, Valore massimo**.</span><span class="sxs-lookup"><span data-stu-id="1b877-234">Select **Gauge** visualization from visualizations, then drag the **Speed** field into **Value, Minimum Value, Maximum Value** areas.</span></span>  
<span data-ttu-id="1b877-235">![Automobili connesse: scheda con più righe](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span><span class="sxs-lookup"><span data-stu-id="1b877-235">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span></span>  

<span data-ttu-id="1b877-236">Modificare l'aggregazione predefinita di **velocità** nell'area **Valore** su **Media**</span><span class="sxs-lookup"><span data-stu-id="1b877-236">Change the default aggregation of **speed** in **Value area** to **Average**</span></span> 

<span data-ttu-id="1b877-237">Modificare l'aggregazione predefinita di **velocità** nell'area **Valore minimo** su **Minima**</span><span class="sxs-lookup"><span data-stu-id="1b877-237">Change the default aggregation of **speed** in **Minimum area** to **Minimum**</span></span>

<span data-ttu-id="1b877-238">Modificare l'aggregazione predefinita di **velocità** nell'area **Valore massimo** su **Massima**</span><span class="sxs-lookup"><span data-stu-id="1b877-238">Change the default aggregation of **speed** in **Maximum area** to **Maximum**</span></span>

![Automobili connesse: scheda con più righe](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

<span data-ttu-id="1b877-240">Rinominare il campo **Titolo misuratore** in **"Velocità media"**</span><span class="sxs-lookup"><span data-stu-id="1b877-240">Rename the **Gauge Title** to **“Average speed”**</span></span> 

![Automobili connesse: misuratore](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

<span data-ttu-id="1b877-242">Fare clic sull'area vuota per aggiungere una nuova visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="1b877-242">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="1b877-243">Allo stesso modo, aggiungere un **Misuratore** per **media olio motore**, **media carburante** e **media temperatura motore**.</span><span class="sxs-lookup"><span data-stu-id="1b877-243">Similarly add a **Gauge** for **average engine oil**, **average fuel**, and **average engine temperate**.</span></span>  

<span data-ttu-id="1b877-244">Modificare l'aggregazione predefinita dei campi in ogni misuratore come indicato nei passaggi precedenti per il misuratore **"Velocità media"**.</span><span class="sxs-lookup"><span data-stu-id="1b877-244">Change the default aggregation of fields in each gauge as per above steps in **“Average speed”** gauge.</span></span>

![Automobili connesse: misuratori](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

<span data-ttu-id="1b877-246">Fare clic sull'area vuota per aggiungere una nuova visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="1b877-246">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="1b877-247">Selezionare **Grafico a linee e istogramma a colonne raggruppate** dalle visualizzazioni, quindi trascinare il campo **Città** in **Asse condiviso**, trascinare i campi **velocità**, **pressione gomme ed olio motore** nell'area **Valori colonna**, modificare il tipo di aggregazione in **Media**.</span><span class="sxs-lookup"><span data-stu-id="1b877-247">Select **Line and Clustered Column Chart** from visualizations, then drag **City** field into **Shared Axis**, drag **speed**, **tirepressure and engineoil fields** into **Column Values** area, change their aggregation type to **Average**.</span></span> 

<span data-ttu-id="1b877-248">Trascinare il campo **Temperatura motore** nell'area **Valori riga** e modificare il tipo di aggregazione in **Media**.</span><span class="sxs-lookup"><span data-stu-id="1b877-248">Drag the **engineTemperature** field into **Line Values** area, change the  aggregation type to **Average**.</span></span> 

![Automobili connesse: campi di visualizzazione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

<span data-ttu-id="1b877-250">Modificare il campo **Titolo** del grafico in **"Media velocità, pressione pneumatici, temperatura dell'olio e del motore"**.</span><span class="sxs-lookup"><span data-stu-id="1b877-250">Change the chart **Title** to **“Average speed, tire pressure, engine oil and engine temperature”**.</span></span>  

![Automobili connesse: campi di visualizzazione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

<span data-ttu-id="1b877-252">Fare clic sull'area vuota per aggiungere una nuova visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="1b877-252">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="1b877-253">Nelle visualizzazioni selezionare **Treemap**, trascinare il campo **Modello** nell'area **Gruppo** e il campo **MaintenanceProbability** nell'area **Valori**.</span><span class="sxs-lookup"><span data-stu-id="1b877-253">Select **Treemap** visualization from visualizations, drag the **Model** field into the **Group** area, and drag the field **MaintenanceProbability** into the **Values** area.</span></span>

<span data-ttu-id="1b877-254">Modificare il campo **Titolo** del grafico in **"Modelli di veicolo che richiedono manutenzione"**.</span><span class="sxs-lookup"><span data-stu-id="1b877-254">Change the chart **Title** to **“Vehicle models requiring maintenance”**.</span></span>

![Automobili connesse: modifica titolo del grafico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

<span data-ttu-id="1b877-256">Fare clic sull'area vuota per aggiungere una nuova visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="1b877-256">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="1b877-257">Nella visualizzazione selezionare **Grafico a barre in pila 100%**, trascinare il campo **città** nell'area **Asse** e i campi **MaintenanceProbability** e **RecallProbability** nell'area **Valore**.</span><span class="sxs-lookup"><span data-stu-id="1b877-257">Select **100% Stacked Bar Chart** from visualization, drag the **city** field into the **Axis** area, and drag the **MaintenanceProbability**, **RecallProbability** fields into the **Value** area.</span></span>

![Automobili connesse: aggiungi nuova visualizzazione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

<span data-ttu-id="1b877-259">Fare clic su **Formato**, selezionare **Colori dati** e impostare il colore di **MaintenanceProbability** sul valore **"F2C80F"**.</span><span class="sxs-lookup"><span data-stu-id="1b877-259">Click **Format**, select **Data Colors**, and set the **MaintenanceProbability** color to the value **“F2C80F”**.</span></span>

<span data-ttu-id="1b877-260">Modificare il campo **Titolo** del grafico in **"Probabilità di manutenzione e richiamo del veicolo in base alla città"**.</span><span class="sxs-lookup"><span data-stu-id="1b877-260">Change the **Title** of the chart to **“Probability of Vehicle Maintenance & Recall by City”**.</span></span>

![Automobili connesse: aggiungi nuova visualizzazione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

<span data-ttu-id="1b877-262">Fare clic sull'area vuota per aggiungere una nuova visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="1b877-262">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="1b877-263">Nelle visualizzazioni selezionare **Grafico ad area**, trascinare il campo **Modello** nell'area **Asse** e i campi **engineOil, tirepressure, speed e MaintenanceProbability** nell'area **Valori**.</span><span class="sxs-lookup"><span data-stu-id="1b877-263">Select **Area Chart** from visualization from visualizations, drag the **Model** field into the **Axis** area, and drag the **engineOil, tirepressure, speed and MaintenanceProbability** fields into the **Values** area.</span></span> <span data-ttu-id="1b877-264">Modificare il tipo di aggregazione in **"Average"**.</span><span class="sxs-lookup"><span data-stu-id="1b877-264">Change their aggregation type to **“Average”**.</span></span> 

![Automobili connesse: modifica tipo di aggregazione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

<span data-ttu-id="1b877-266">Modificare il titolo del grafico in **"Media per olio motore, pressione pneumatici, velocità e probabilità di manutenzione in base al modello"**.</span><span class="sxs-lookup"><span data-stu-id="1b877-266">Change the title of the chart to **“Average engine oil, tire pressure, speed and maintenance probability by model”**.</span></span>

![Automobili connesse: modifica titolo del grafico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

<span data-ttu-id="1b877-268">Fare clic sull'area vuota per aggiungere una nuova visualizzazione:</span><span class="sxs-lookup"><span data-stu-id="1b877-268">Click the blank area to add new visualization:</span></span>

1. <span data-ttu-id="1b877-269">Nelle visualizzazioni selezionare **Scatter Chart** .</span><span class="sxs-lookup"><span data-stu-id="1b877-269">Select **Scatter Chart** visualization from visualizations.</span></span>
2. <span data-ttu-id="1b877-270">Trascinare il campo **Modello** nelle aree **Dettagli** e **Legenda**.</span><span class="sxs-lookup"><span data-stu-id="1b877-270">Drag the **Model** field into the **Details** and **Legend** area.</span></span>
3. <span data-ttu-id="1b877-271">Trascinare il campo **carburante** nell'area **Asse X** e modificare l'aggregazione in **Media**.</span><span class="sxs-lookup"><span data-stu-id="1b877-271">Drag the **fuel** field into the **X-Axis** area, change the aggregation to **Average**.</span></span>
4. <span data-ttu-id="1b877-272">Trascinare il campo **engineTemperature** nell'area **Asse Y** e modificare l'aggregazione in **Media**</span><span class="sxs-lookup"><span data-stu-id="1b877-272">Drag **engineTemparature** into **Y-Axis area**, change the aggregation to **Average**</span></span>
5. <span data-ttu-id="1b877-273">Trascinare il campo **vin** nell'area **Dimensioni**.</span><span class="sxs-lookup"><span data-stu-id="1b877-273">Drag the **vin** field into the **Size** area.</span></span>

![Automobili connesse: aggiungi nuova visualizzazione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

<span data-ttu-id="1b877-275">Modificare il campo **Titolo** del grafico in **"Medie per carburante e temperatura del motore in base al modello"**.</span><span class="sxs-lookup"><span data-stu-id="1b877-275">Change the chart **Title** to **“Averages of Fuel, Engine Temperature by Model”**.</span></span>

![Automobili connesse: modifica titolo del grafico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

<span data-ttu-id="1b877-277">Il report finale avrà un aspetto simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="1b877-277">The final report will look like as shown below.</span></span>

![Automobili connesse: report finale](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-the-reports-to-the-real-time-dashboard"></a><span data-ttu-id="1b877-279">Aggiungere visualizzazioni dai report al dashboard in tempo reale</span><span class="sxs-lookup"><span data-stu-id="1b877-279">Pin visualizations from the reports to the real-time dashboard</span></span>
<span data-ttu-id="1b877-280">Creare un dashboard vuoto facendo clic sull'icona del segno più accanto a Dashboard.</span><span class="sxs-lookup"><span data-stu-id="1b877-280">Create a blank dashboard by clicking on the plus icon next to Dashboards.</span></span> <span data-ttu-id="1b877-281">È possibile denominarlo "Dashboard di analisi dei dati di telemetria di veicolo".</span><span class="sxs-lookup"><span data-stu-id="1b877-281">You can name it “Vehicle Telemetry Analytics Dashboard”</span></span>

![Automobili connesse: dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

<span data-ttu-id="1b877-283">Aggiungere la visualizzazione dei report precedenti al dashboard.</span><span class="sxs-lookup"><span data-stu-id="1b877-283">Pin the visualization from the above reports to the dashboard.</span></span> 

![Automobili connesse: dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

<span data-ttu-id="1b877-285">Il dashboard dovrebbe avere l'aspetto illustrato di seguito una volta creati tutti e tre i report e aggiunte le visualizzazioni corrispondenti al dashboard.</span><span class="sxs-lookup"><span data-stu-id="1b877-285">The dashboard should look as follows when all the three reports are created and the corresponding visualizations are pinned to the dashboard.</span></span> <span data-ttu-id="1b877-286">Se non sono stati creati tutti i report, il dashboard potrebbe apparire diverso.</span><span class="sxs-lookup"><span data-stu-id="1b877-286">If you have not created all the reports, your dashboard could look different.</span></span> 

![Automobili connesse: dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

<span data-ttu-id="1b877-288">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="1b877-288">Congratulations!</span></span> <span data-ttu-id="1b877-289">Il dashboard in tempo reale è stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="1b877-289">You have successfully created the real-time dashboard.</span></span> <span data-ttu-id="1b877-290">Continuando a eseguire CarEventGenerator.exe e RealtimeDashboardApp.exe, gli aggiornamenti saranno visualizzati in tempo reale nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="1b877-290">As you continue to execute CarEventGenerator.exe and RealtimeDashboardApp.exe, you should see live updates on the dashboard.</span></span> <span data-ttu-id="1b877-291">Il completamento dei passaggi seguenti dovrebbe richiedere circa 10-15 minuti .</span><span class="sxs-lookup"><span data-stu-id="1b877-291">It should take about 10 to 15 minutes to complete the following steps.</span></span>

## <a name="setup-power-bi-batch-processing-dashboard"></a><span data-ttu-id="1b877-292">Configurare il dashboard di elaborazione batch di PowerBI</span><span class="sxs-lookup"><span data-stu-id="1b877-292">Setup Power BI batch processing dashboard</span></span>
> [!NOTE]
> <span data-ttu-id="1b877-293">Occorrono circa due ore dal completamento della distribuzione perché la pipeline di elaborazione batch end-to-end completi l'esecuzione ed elabori un anno di dati generati.</span><span class="sxs-lookup"><span data-stu-id="1b877-293">It takes about two hours (from the successful completion of the deployment) for the end to end batch processing pipeline to finish execution and process a year worth of generated data.</span></span> <span data-ttu-id="1b877-294">Quindi, attendere il completamento prima di procedere con i passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="1b877-294">So wait for the processing to finish before proceeding with the next steps.</span></span> 
> 
> 

<span data-ttu-id="1b877-295">**Scaricare il file di progettazione Power BI**</span><span class="sxs-lookup"><span data-stu-id="1b877-295">**Download the Power BI designer file**</span></span>

* <span data-ttu-id="1b877-296">Un file di progettazione Power BI preconfigurato è incluso con le istruzioni di funzionamento manuale della distribuzione</span><span class="sxs-lookup"><span data-stu-id="1b877-296">A pre-configured Power BI designer file is included as part of the deployment Manual Operation Instructions</span></span>
* <span data-ttu-id="1b877-297">Cercare 2.</span><span class="sxs-lookup"><span data-stu-id="1b877-297">Look for 2.</span></span> <span data-ttu-id="1b877-298">Impostare il dashboard di elaborazione batch Power BI È possibile scaricare il modello di Power BI per il dashboard di elaborazione batch denominato **ConnectedCarsPbiReport.pbix**.</span><span class="sxs-lookup"><span data-stu-id="1b877-298">Setup PowerBI batch processing dashboard You can download the PowerBI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span></span>
* <span data-ttu-id="1b877-299">Salvare in locale</span><span class="sxs-lookup"><span data-stu-id="1b877-299">Save locally</span></span>

<span data-ttu-id="1b877-300">**Configurare i report di Power BI**</span><span class="sxs-lookup"><span data-stu-id="1b877-300">**Configure Power BI reports**</span></span>

* <span data-ttu-id="1b877-301">Aprire il file di progettazione '**ConnectedCarsPbiReport.pbix**' tramite Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="1b877-301">Open the designer file ‘**ConnectedCarsPbiReport.pbix**’ using Power BI Desktop.</span></span> <span data-ttu-id="1b877-302">Se non lo si è ancora fatto, installare Power BI Desktop da [Installazione Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="1b877-302">If you do not already have, install the Power BI Desktop from [Power BI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span></span> 
* <span data-ttu-id="1b877-303">Fare clic su **Modifica query**.</span><span class="sxs-lookup"><span data-stu-id="1b877-303">Click the **Edit Queries**.</span></span>

![Modificare la query di Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* <span data-ttu-id="1b877-305">Fare doppio clic sull'**origine**.</span><span class="sxs-lookup"><span data-stu-id="1b877-305">Double-click the **Source**.</span></span>

![Impostare l'origine di Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* <span data-ttu-id="1b877-307">Aggiornare la stringa di connessione del server con il server di Azure SQL di cui è stato effettuato il provisioning come parte della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="1b877-307">Update Server connection string with the Azure SQL server that got provisioned as part of the deployment.</span></span>  <span data-ttu-id="1b877-308">Esaminare le istruzioni di funzionamento manuale in</span><span class="sxs-lookup"><span data-stu-id="1b877-308">Look in the Manual Operation Instructions under</span></span> 

    4. <span data-ttu-id="1b877-309">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="1b877-309">Azure SQL Database</span></span>
    
    * <span data-ttu-id="1b877-310">Server: somethingsrv.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="1b877-310">Server: somethingsrv.database.windows.net</span></span>
    * <span data-ttu-id="1b877-311">Database: connectedcar</span><span class="sxs-lookup"><span data-stu-id="1b877-311">Database: connectedcar</span></span>
    * <span data-ttu-id="1b877-312">Nome utente: nome utente</span><span class="sxs-lookup"><span data-stu-id="1b877-312">Username: username</span></span>
    * <span data-ttu-id="1b877-313">Password: è possibile gestire la password di SQL Server dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1b877-313">Password: You can manage your SQL server password from Azure portal</span></span>

* <span data-ttu-id="1b877-314">Lasciare **Database** come *connectedcar*.</span><span class="sxs-lookup"><span data-stu-id="1b877-314">Leave **Database** as *connectedcar*.</span></span>

![Impostare il database Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* <span data-ttu-id="1b877-316">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b877-316">Click **OK**.</span></span>
* <span data-ttu-id="1b877-317">La scheda **Credenziali di Windows** è selezionata per impostazione predefinita. Modificarla in **Credenziali di database** facendo clic sulla scheda **Database** a destra.</span><span class="sxs-lookup"><span data-stu-id="1b877-317">You will see **Windows credential** tab selected by default, change it to **Database credentials** by clicking on **Database** tab at right.</span></span>
* <span data-ttu-id="1b877-318">Specificare **Nome utente** e **Password** del database SQL di Azure specificato durante la relativa configurazione della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="1b877-318">Provide the **Username** and **Password** of your Azure SQL Database that was specified during its deployment setup.</span></span>

![Ottenere le credenziali del database](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* <span data-ttu-id="1b877-320">Fare clic su **Connetti**</span><span class="sxs-lookup"><span data-stu-id="1b877-320">Click **Connect**</span></span>
* <span data-ttu-id="1b877-321">Ripetere i passaggi precedenti per ciascuna delle tre query rimanenti presenti nel riquadro destro, quindi aggiornare i dettagli di connessione dell'origine dati.</span><span class="sxs-lookup"><span data-stu-id="1b877-321">Repeat the above steps for each of the three remaining queries present at right pane, and then update the data source connection details.</span></span>
* <span data-ttu-id="1b877-322">Fare clic su **Chiudi e carica**.</span><span class="sxs-lookup"><span data-stu-id="1b877-322">Click **Close and Load**.</span></span> <span data-ttu-id="1b877-323">I set di dati del file di Power BI Desktop sono connessi alle tabelle del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b877-323">Power BI Desktop file datasets are connected to SQL Azure Database tables.</span></span>
* <span data-ttu-id="1b877-324">**Chiudi** per chiudere il file Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="1b877-324">**Close** Power BI Desktop file.</span></span>

![Chiudere Power BI Desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* <span data-ttu-id="1b877-326">Fare clic sul pulsante **Salva** per salvare le modifiche apportate.</span><span class="sxs-lookup"><span data-stu-id="1b877-326">Click **Save** button to save the changes.</span></span> 

<span data-ttu-id="1b877-327">Sono stati configurati tutti i report corrispondenti al percorso di elaborazione batch nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="1b877-327">You have now configured all the reports corresponding to the batch processing path in the solution.</span></span> 

## <a name="upload-to-powerbicom"></a><span data-ttu-id="1b877-328">Caricare in *powerbi.com*</span><span class="sxs-lookup"><span data-stu-id="1b877-328">Upload to *powerbi.com*</span></span>
1. <span data-ttu-id="1b877-329">Passare al portale Web di Power BI all'indirizzo http://powerbi.com e accedere.</span><span class="sxs-lookup"><span data-stu-id="1b877-329">Navigate to the Power BI web portal at http://powerbi.com and login.</span></span>
2. <span data-ttu-id="1b877-330">Fare clic su **Recupera dati**</span><span class="sxs-lookup"><span data-stu-id="1b877-330">Click **Get Data**</span></span>  
3. <span data-ttu-id="1b877-331">Caricare il file di Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="1b877-331">Upload the Power BI Desktop File.</span></span>  
4. <span data-ttu-id="1b877-332">Per caricarlo, fare clic su **Recupera dati -> Recupera File -> File locale**</span><span class="sxs-lookup"><span data-stu-id="1b877-332">To upload, click **Get Data -> Files Get -> Local file**</span></span>  
5. <span data-ttu-id="1b877-333">Individuare il file **"**ConnectedCarsPbiReport.pbix**"**</span><span class="sxs-lookup"><span data-stu-id="1b877-333">Navigate to the **“**ConnectedCarsPbiReport.pbix**”**</span></span>  
6. <span data-ttu-id="1b877-334">Una volta caricato il file, si verrà reindirizzati nuovamente all'area di lavoro di PowerBI.</span><span class="sxs-lookup"><span data-stu-id="1b877-334">Once the file is uploaded, you will be navigated back to your Power BI work space.</span></span>  

<span data-ttu-id="1b877-335">Verranno creati automaticamente un set di dati, un report e un dashboard vuoto.</span><span class="sxs-lookup"><span data-stu-id="1b877-335">A dataset, report and a blank dashboard will be created for you.</span></span>  

<span data-ttu-id="1b877-336">Aggiungere grafici a un nuovo dashboard denominato **Vehicle Telemetry Analytics Dashboard**  (Dashboard di analisi dei dati di telemetria del veicolo) in **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="1b877-336">Pin charts to a new dashboard called **Vehicle Telemetry Analytics Dashboard** in **Power BI**.</span></span> <span data-ttu-id="1b877-337">Fare clic sul dashboard vuoto creato in precedenza, quindi passare alla sezione **Report** e fare clic sul report appena caricato.</span><span class="sxs-lookup"><span data-stu-id="1b877-337">Click the blank dashboard created above and then navigate to the **Reports** section click the newly uploaded report.</span></span>  

![Vehicle Telemetry Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

<span data-ttu-id="1b877-339">**Il report include sei pagine:**</span><span class="sxs-lookup"><span data-stu-id="1b877-339">**Note the report has six pages:**</span></span>  
<span data-ttu-id="1b877-340">Pagina 1: Densità veicolo</span><span class="sxs-lookup"><span data-stu-id="1b877-340">Page 1: Vehicle density</span></span>  
<span data-ttu-id="1b877-341">Pagina 2: Integrità veicolo in tempo reale</span><span class="sxs-lookup"><span data-stu-id="1b877-341">Page 2: Real-time vehicle health</span></span>  
<span data-ttu-id="1b877-342">Pagina 3: Veicoli guidati in modo aggressivo</span><span class="sxs-lookup"><span data-stu-id="1b877-342">Page 3: Aggressively Driven Vehicles</span></span>   
<span data-ttu-id="1b877-343">Pagina 4: Veicoli richiamati</span><span class="sxs-lookup"><span data-stu-id="1b877-343">Page 4: Recalled vehicles</span></span>  
<span data-ttu-id="1b877-344">Pagina 5: Veicoli con consumo di carburante efficiente</span><span class="sxs-lookup"><span data-stu-id="1b877-344">Page 5: Fuel Efficiently Driven Vehicles</span></span>  
<span data-ttu-id="1b877-345">Pagina 6: Logo di Contoso</span><span class="sxs-lookup"><span data-stu-id="1b877-345">Page 6: Contoso Logo</span></span>  

![Connected Cars Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

<span data-ttu-id="1b877-347">**Dalla pagina 3**aggiungere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="1b877-347">**From Page 3**, pin the following:</span></span>  

1. <span data-ttu-id="1b877-348">Count of vin</span><span class="sxs-lookup"><span data-stu-id="1b877-348">Count of VIN</span></span>  
   ![Connected Cars Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. <span data-ttu-id="1b877-350">Veicoli guidati in modo aggressivo in base al modello: grafico a cascata </span><span class="sxs-lookup"><span data-stu-id="1b877-350">Aggressively driven vehicles by model – Waterfall chart</span></span>  
   ![Telemetria veicolo: aggiungi grafici 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

<span data-ttu-id="1b877-352">**Dalla pagina 5**aggiungere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="1b877-352">**From Page 5**, pin the following:</span></span> 

1. <span data-ttu-id="1b877-353">Count of vin</span><span class="sxs-lookup"><span data-stu-id="1b877-353">Count of vin</span></span>    
   ![Telemetria veicolo: aggiungi grafici 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. <span data-ttu-id="1b877-355">Veicoli guidati con un consumo efficiente del carburante in base al modello: istogramma a colonne raggruppate </span><span class="sxs-lookup"><span data-stu-id="1b877-355">Fuel efficient vehicles by model: Clustered column chart</span></span>  
   ![Telemetria veicolo: aggiungi grafici 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

<span data-ttu-id="1b877-357">**Dalla pagina 4**aggiungere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="1b877-357">**From Page 4**, pin the following:</span></span>  

1. <span data-ttu-id="1b877-358">Count of vin</span><span class="sxs-lookup"><span data-stu-id="1b877-358">Count of vin</span></span>  
   ![Telemetria veicolo: aggiungi grafici 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. <span data-ttu-id="1b877-360">Veicoli richiamati in base alla città e al modello: grafico ad albero </span><span class="sxs-lookup"><span data-stu-id="1b877-360">Recalled vehicles by city, model: Treemap</span></span>  
   ![Telemetria veicolo: aggiungi grafici 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

<span data-ttu-id="1b877-362">**Dalla pagina 6**aggiungere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="1b877-362">**From Page 6**, pin the following:</span></span>  

1. <span data-ttu-id="1b877-363">Logo Contoso Motors </span><span class="sxs-lookup"><span data-stu-id="1b877-363">Contoso Motors logo</span></span>  
   ![Telemetria veicolo: aggiungi grafici 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

<span data-ttu-id="1b877-365">**Organizzare il dashboard**</span><span class="sxs-lookup"><span data-stu-id="1b877-365">**Organize the dashboard**</span></span>  

1. <span data-ttu-id="1b877-366">Passare al dashboard</span><span class="sxs-lookup"><span data-stu-id="1b877-366">Navigate to the dashboard</span></span>
2. <span data-ttu-id="1b877-367">Passare il mouse su ciascun grafico e rinominarlo in base alla denominazione specificata nell'immagine seguente del dashboard completo.</span><span class="sxs-lookup"><span data-stu-id="1b877-367">Hover over each chart and rename it based on the naming provided in the complete dashboard image below.</span></span> <span data-ttu-id="1b877-368">Spostare anche i grafici come illustrato nel dashboard seguente.</span><span class="sxs-lookup"><span data-stu-id="1b877-368">Also move the charts around to look like the dashboard below.</span></span>  
   ![Telemetria veicolo: organizza dashboard 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Vehicle Telemetry Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. <span data-ttu-id="1b877-371">Se tutti i report sono stati creati come indicato in questo documento, il dashboard finale completato dovrebbe avere un aspetto simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="1b877-371">If you have created all the reports as mentioned in this document, the final completed dashboard should look like the following figure.</span></span> 

![Telemetria veicolo: organizza dashboard 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

<span data-ttu-id="1b877-373">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="1b877-373">Congratulations!</span></span> <span data-ttu-id="1b877-374">Sono stati creati il report e il dashboard per ottenere in tempo reale informazioni dettagliate in batch e predittive sullo stato di integrità dei veicoli e sulle abitudini di guida.</span><span class="sxs-lookup"><span data-stu-id="1b877-374">You have successfully created the reports and the dashboard to gain real-time, predictive and batch insights on vehicle health and driving habits.</span></span>  
