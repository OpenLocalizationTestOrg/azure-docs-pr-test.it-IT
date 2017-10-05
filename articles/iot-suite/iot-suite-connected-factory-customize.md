---
title: Panoramica della soluzione di fabbrica connessa di Azure IoT Suite | Microsoft Docs
description: Informazioni su come personalizzare il comportamento della soluzione preconfigurata di fabbrica connessa.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: c#
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 90a6172dbd887ecda5a9f5d9082a4e136092bc10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="customize-how-the-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a><span data-ttu-id="753ed-103">Personalizzare la modalità di visualizzazione dei dati dai server OPC UA da parte della soluzione di fabbrica connessa</span><span class="sxs-lookup"><span data-stu-id="753ed-103">Customize how the connected factory solution displays data from your OPC UA servers</span></span>

## <a name="introduction"></a><span data-ttu-id="753ed-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="753ed-104">Introduction</span></span>

<span data-ttu-id="753ed-105">La soluzione di fabbrica connessa aggrega e visualizza dati dai server OPC UA connessi alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="753ed-105">The connected factory solution aggregates and displays data from the OPC UA servers connected to the solution.</span></span> <span data-ttu-id="753ed-106">È possibile individuare e inviare comandi ai server OPC UA nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="753ed-106">You can browse and send commands to the OPC UA servers in your solution.</span></span> <span data-ttu-id="753ed-107">Per altre informazioni su OPC UA, vedere le [domande frequenti sulla soluzione di connected factory](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="753ed-107">For more information about OPC UA, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

<span data-ttu-id="753ed-108">Gli esempi di dati aggregati nella soluzione includono i valori OEE (Overall Equipment Efficiency) e gli indicatori KPI visualizzabili nel dashboard a livello di fabbrica, linea e stazione.</span><span class="sxs-lookup"><span data-stu-id="753ed-108">Examples of aggregated data in the solution include the Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) that you can view in the dashboard at the factory, line, and station levels.</span></span> <span data-ttu-id="753ed-109">Lo screenshot seguente mostra i valori OEE e gli indicatori KPI per la stazione **Assemblaggio** nella **Linea di produzione 1** di uno stabilimento a **Monaco**:</span><span class="sxs-lookup"><span data-stu-id="753ed-109">The following screenshot shows the OEE and KPI values for the **Assembly** station, on **Production line 1**, in the **Munich** factory:</span></span>

![Esempio di valori OEE e indicatori KPI nella soluzione][img-oee-kpi]

<span data-ttu-id="753ed-111">Questa soluzione consente di visualizzare informazioni dettagliate su dati specifici dai server OPC UA, chiamati *stazioni*.</span><span class="sxs-lookup"><span data-stu-id="753ed-111">The solution enables you to view detailed information from specific data items from the OPC UA servers, called *stations*.</span></span> <span data-ttu-id="753ed-112">La schermata seguente mostra i tracciati del numero di articoli prodotti da una stazione specifica:</span><span class="sxs-lookup"><span data-stu-id="753ed-112">The following screenshot shows plots of the number of manufactured items from a specific station:</span></span>

![Tracciati del numero di articoli prodotti][img-manufactured-items]

<span data-ttu-id="753ed-114">Facendo clic su uno dei grafici è possibile esplorare ulteriormente i dati tramite Time Series Insights (TSI):</span><span class="sxs-lookup"><span data-stu-id="753ed-114">If you click one of the graphs, you can explore the data further using Time Series Insights (TSI):</span></span>

![Esplorare i dati con Time Series Insights][img-tsi]

<span data-ttu-id="753ed-116">L'articolo illustra:</span><span class="sxs-lookup"><span data-stu-id="753ed-116">This article describes:</span></span>

- <span data-ttu-id="753ed-117">Come i dati vengono resi disponibili per le diverse visualizzazioni nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="753ed-117">How the data is made available to the various views in the solution.</span></span>
- <span data-ttu-id="753ed-118">Come è possibile personalizzare il modo in cui la soluzione visualizza i dati.</span><span class="sxs-lookup"><span data-stu-id="753ed-118">How you can customize the way the solution displays the data.</span></span>

## <a name="data-sources"></a><span data-ttu-id="753ed-119">Origini dati</span><span class="sxs-lookup"><span data-stu-id="753ed-119">Data sources</span></span>

<span data-ttu-id="753ed-120">La soluzione di fabbrica connessa visualizza dati dai server OPC UA connessi alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="753ed-120">The connected factory solution displays data from the OPC UA servers connected to the solution.</span></span> <span data-ttu-id="753ed-121">L'installazione predefinita include diversi server OPC UA che eseguono una simulazione di fabbrica.</span><span class="sxs-lookup"><span data-stu-id="753ed-121">The default installation includes several OPC UA servers running a factory simulation.</span></span> <span data-ttu-id="753ed-122">È possibile aggiungere i propri server OPC UA che [si connettono tramite un gateway][lnk-connect-cf] alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="753ed-122">You can add your own OPC UA servers that [connect through a gateway][lnk-connect-cf] to your solution.</span></span>

<span data-ttu-id="753ed-123">È possibile anche esplorare gli elementi dei dati che un server OPC UA connesso può inviare alla soluzione nel dashboard:</span><span class="sxs-lookup"><span data-stu-id="753ed-123">You can browse the data items that a connected OPC UA server can send to your solution in the dashboard:</span></span>

1. <span data-ttu-id="753ed-124">Passare alla vista **Selezionare un server OPC UA**:</span><span class="sxs-lookup"><span data-stu-id="753ed-124">Navigate to the **Select an OPC UA server** view:</span></span>

    ![Passare alla vista Selezionare un server OPC UA][img-select-server]

1. <span data-ttu-id="753ed-126">Selezionare un server e fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="753ed-126">Select a server and click **Connect**.</span></span> <span data-ttu-id="753ed-127">Fare clic su **Procedi** quando viene visualizzato l'avviso di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="753ed-127">Click **Proceed** when the security warning appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="753ed-128">L'avviso viene visualizzato una sola volta per ciascun server e stabilisce una relazione di trust tra quest'ultimo e il dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="753ed-128">This warning only appears once for each server and establishes a trust relationship between the solution dashboard and the server.</span></span>

1. <span data-ttu-id="753ed-129">È ora possibile esplorare gli elementi dei dati che il server può inviare alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="753ed-129">You can now browse the data items that the server can send to the solution.</span></span> <span data-ttu-id="753ed-130">Gli elementi che vengono inviati alla soluzione hanno un segno di spunta verde:</span><span class="sxs-lookup"><span data-stu-id="753ed-130">Items that are being sent to the solution have a green check mark:</span></span>

    ![Elementi pubblicati][img-published]

1. <span data-ttu-id="753ed-132">Se si è un *amministratore* nella soluzione, è possibile scegliere di pubblicare un elemento di dati per renderlo disponibile nella soluzione di fabbrica connessa.</span><span class="sxs-lookup"><span data-stu-id="753ed-132">If you are an *Administrator* in the solution, you can choose to publish a data item to make it available in the connected factory solution.</span></span> <span data-ttu-id="753ed-133">L'amministratore può anche modificare il valore degli elementi di dati e chiamare i metodi nel server OPC UA.</span><span class="sxs-lookup"><span data-stu-id="753ed-133">As an Administrator, you can also change the value of data items and call methods in the OPC UA server.</span></span>

## <a name="map-the-data"></a><span data-ttu-id="753ed-134">Eseguire il mapping di dati</span><span class="sxs-lookup"><span data-stu-id="753ed-134">Map the data</span></span>

<span data-ttu-id="753ed-135">La soluzione di fabbrica connessa mappa e aggrega gli elementi di dati pubblicati dal server OPC UA alle varie viste nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="753ed-135">The connected factory solution maps and aggregates the published data items from the OPC UA server to the various views in the solution.</span></span> <span data-ttu-id="753ed-136">La soluzione di fabbrica connessa viene distribuita nell'account Azure dell'utente quando ne viene effettuato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="753ed-136">The connected factory solution deploys to your Azure account when you provision the solution.</span></span> <span data-ttu-id="753ed-137">Le informazioni di mapping sono contenute in un file JSON nella soluzione di fabbrica connessa Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="753ed-137">A JSON file in the Visual Studio connected factory solution stores this mapping information.</span></span> <span data-ttu-id="753ed-138">È possibile visualizzare e modificare questo file di configurazione JSON nella soluzione di fabbrica connessa Visual Studi.</span><span class="sxs-lookup"><span data-stu-id="753ed-138">You can view and modify this JSON configuration file in the connected factory Visual Studio solution.</span></span> <span data-ttu-id="753ed-139">È possibile ridistribuire la soluzione dopo aver apportato una modifica.</span><span class="sxs-lookup"><span data-stu-id="753ed-139">You can redeploy the solution after you make a change.</span></span>

<span data-ttu-id="753ed-140">È possibile usare il file di configurazione per:</span><span class="sxs-lookup"><span data-stu-id="753ed-140">You can use the configuration file to:</span></span>

- <span data-ttu-id="753ed-141">Modificare le stazioni, le linee di produzione e gli stabilimenti simulati esistenti.</span><span class="sxs-lookup"><span data-stu-id="753ed-141">Edit the existing simulated factories, production lines, and stations.</span></span>
- <span data-ttu-id="753ed-142">Eseguire il mapping di dati dai server OPC UA effettivi che si connettono alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="753ed-142">Map data from real OPC UA servers that you connect to the solution.</span></span>

<span data-ttu-id="753ed-143">Per clonare una copia della soluzione di fabbrica connessa Visual Studio, usare il comando git seguente:</span><span class="sxs-lookup"><span data-stu-id="753ed-143">To clone a copy of the connected factory Visual Studio solution, use the following git command:</span></span>

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

<span data-ttu-id="753ed-144">Il file **ContosoTopologyDescription.json** definisce il mapping dagli elementi di dati del server OPC UA alle visualizzazioni nel dashboard della soluzione di fabbrica connessa.</span><span class="sxs-lookup"><span data-stu-id="753ed-144">The file **ContosoTopologyDescription.json** defines the mapping from the OPC UA server data items to the views in the connected factory solution dashboard.</span></span> <span data-ttu-id="753ed-145">Il file di configurazione si trova nella cartella **Contoso\Topology** all'interno del progetto **WebApp** soluzione Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="753ed-145">You can find this configuration file in the **Contoso\Topology** folder in the **WebApp** project in the Visual Studio solution.</span></span>

<span data-ttu-id="753ed-146">Il contenuto del file JSON è organizzato come una gerarchia di nodi di stabilimento, linea di produzione e stazione,</span><span class="sxs-lookup"><span data-stu-id="753ed-146">The content of the JSON file is organized as a hierarchy of factory, production line, and station nodes.</span></span> <span data-ttu-id="753ed-147">la quale definisce la gerarchia di navigazione nel dashboard di fabbrica connessa.</span><span class="sxs-lookup"><span data-stu-id="753ed-147">This hierarchy defines the navigation hierarchy in the connected factory dashboard.</span></span> <span data-ttu-id="753ed-148">I valori in ogni nodo della gerarchia determinano le informazioni visualizzate nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="753ed-148">Values at each node of the hierarchy determine the information displayed in the dashboard.</span></span> <span data-ttu-id="753ed-149">Ad esempio, il file JSON contiene i valori seguenti per lo stabilimento di Monaco:</span><span class="sxs-lookup"><span data-stu-id="753ed-149">For example, the JSON file contains the following values for the Munich factory:</span></span>

```json
"Guid": "73B534AE-7C7E-4877-B826-F1C0EA339F65",
"Name": "Munich",
"Description": "Braking system",
"Location": {
    "City": "Munich",
    "Country": "Germany",
    "Latitude": 48.13641,
    "Longitude": 11.57754
},
"Image": "munich.jpg"
```

<span data-ttu-id="753ed-150">Nome, descrizione e posizione vengono visualizzati nel dashboard:</span><span class="sxs-lookup"><span data-stu-id="753ed-150">The name, description, and location appear on this view in the dashboard:</span></span>

![Dati di Monaco nel dashboard][img-munich]

<span data-ttu-id="753ed-152">Ogni stabilimento, linea di produzione e stazione ha una proprietà immagine.</span><span class="sxs-lookup"><span data-stu-id="753ed-152">Each factory, production line, and station have an image property.</span></span> <span data-ttu-id="753ed-153">Questi file JPEG si trovano nella cartella **Content\img** all'interno del progetto **WebApp**</span><span class="sxs-lookup"><span data-stu-id="753ed-153">You can find these JPEG files in the **Content\img** folder in the **WebApp** project.</span></span> <span data-ttu-id="753ed-154">e vengono visualizzati nel dashboard fabbrica connessa.</span><span class="sxs-lookup"><span data-stu-id="753ed-154">These image files display in the connected factory dashboard.</span></span>

<span data-ttu-id="753ed-155">Ogni stazione include diverse proprietà dettagliate che definiscono il mapping dagli elementi di dati OPC UA.</span><span class="sxs-lookup"><span data-stu-id="753ed-155">Each station includes several detailed properties that define the mapping from the OPC UA data items.</span></span> <span data-ttu-id="753ed-156">Queste proprietà sono descritte nelle sezioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="753ed-156">These properties are described in the following sections:</span></span>

### <a name="opcuri"></a><span data-ttu-id="753ed-157">OpcUri</span><span class="sxs-lookup"><span data-stu-id="753ed-157">OpcUri</span></span>

<span data-ttu-id="753ed-158">Il valore **OpcUri** è l'URI dell'applicazione OPC UA che identifica in modo univoco il server OPC UA.</span><span class="sxs-lookup"><span data-stu-id="753ed-158">The **OpcUri** value is the OPC UA Application URI that uniquely identifies the OPC UA server.</span></span> <span data-ttu-id="753ed-159">Ad esempio, il valore **OpcUri** per la stazione di assemblaggio nella linea di produzione 1 a Monaco ha l'aspetto seguente: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span><span class="sxs-lookup"><span data-stu-id="753ed-159">For example, the **OpcUri** value for the assembly station on production line 1 in Munich looks like the following: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span></span>

<span data-ttu-id="753ed-160">È possibile visualizzare gli URI dei server OPC UA connessi nel dashboard della soluzione:</span><span class="sxs-lookup"><span data-stu-id="753ed-160">You can view the URIs of the connected OPC UA servers in the solution dashboard:</span></span>

![Visualizzare gli URI dei server OPC UA][img-server-uris]

### <a name="simulation"></a><span data-ttu-id="753ed-162">Simulazione</span><span class="sxs-lookup"><span data-stu-id="753ed-162">Simulation</span></span>

<span data-ttu-id="753ed-163">Le informazioni contenute nel nodo **Simulazione** si riferiscono in modo specifico alla simulazione OPC UA eseguita nei server OPC UA di cui è stato eseguito il provisioning per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="753ed-163">The information in the **Simulation** node is specific to the OPC UA simulation that runs in the OPC UA servers that are provisioned by default.</span></span> <span data-ttu-id="753ed-164">Non vengono usate per un server OPC UA reale.</span><span class="sxs-lookup"><span data-stu-id="753ed-164">It is not used for a real OPC UA server.</span></span>

### <a name="kpi1-and-kpi2"></a><span data-ttu-id="753ed-165">Kpi1 e Kpi2</span><span class="sxs-lookup"><span data-stu-id="753ed-165">Kpi1 and Kpi2</span></span>

<span data-ttu-id="753ed-166">Questi nodi descrivono il contributo dei dati dalla stazione ai due indicatori KPI nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="753ed-166">These nodes describe how data from the station contributes to the two KPI values in the dashboard.</span></span> <span data-ttu-id="753ed-167">In una distribuzione predefinita, questi indicatori KPI rappresentano unità all'ora e kWh all'ora.</span><span class="sxs-lookup"><span data-stu-id="753ed-167">In a default deployment, these KPI values are units per hour and kWh per hour.</span></span> <span data-ttu-id="753ed-168">La soluzione calcola i valori degli indicatori KPI a livello di stazione e li aggrega ai livelli di linea di produzione e di stabilimento.</span><span class="sxs-lookup"><span data-stu-id="753ed-168">The solution calculates KPI vales at the level of a station and aggregates them at the production line and factory levels.</span></span>

<span data-ttu-id="753ed-169">Ogni indicatore KPI ha un valore minimo, un valore massimo e un valore di destinazione</span><span class="sxs-lookup"><span data-stu-id="753ed-169">Each KPI has a minimum, maximum, and target value.</span></span> <span data-ttu-id="753ed-170">e può anche definire azioni di avviso che devono essere eseguite dalla soluzione di fabbrica connessa.</span><span class="sxs-lookup"><span data-stu-id="753ed-170">Each KPI value can also define alert actions for the connected factory solution to perform.</span></span> <span data-ttu-id="753ed-171">Il frammento di codice seguente mostra le definizioni degli indicatori KPI per la stazione di assemblaggio nella linea di produzione 1 a Monaco:</span><span class="sxs-lookup"><span data-stu-id="753ed-171">The following snippet shows the KPI definitions for the assembly station on production line 1 in Munich:</span></span>

```json
"Kpi1": {
  "Minimum": 150,
  "Target": 300,
  "Maximum": 600
},
"Kpi2": {
  "Minimum": 50,
  "Target": 100,
  "Maximum": 200,
  "MinimumAlertActions": [
    {
      "Type": "None"
    }
  ]
}
```

<span data-ttu-id="753ed-172">Lo screenshot seguente mostra i dati KPI nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="753ed-172">The following screenshot shows the KPI data in the dashboard.</span></span>

![Informazioni relative ai KPI nel dashboard][lnk-kpi]

### <a name="opcnodes"></a><span data-ttu-id="753ed-174">OpcNodes</span><span class="sxs-lookup"><span data-stu-id="753ed-174">OpcNodes</span></span>

<span data-ttu-id="753ed-175">I nodi **OpcNodes** identificano gli elementi dei dati pubblicati dal server OPC UA e ne specificano le modalità di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="753ed-175">The **OpcNodes** nodes identify the published data items from the OPC UA server and specify how to process that data.</span></span>

<span data-ttu-id="753ed-176">Il valore **NodeId** identifica il NodeID OPC UA specifico dal server OPC UA.</span><span class="sxs-lookup"><span data-stu-id="753ed-176">The **NodeId** value identifies the specific OPC UA NodeID from the OPC UA server.</span></span> <span data-ttu-id="753ed-177">Il primo nodo nella stazione di assemblaggio per la linea di produzione 1 a Monaco ha un valore **ns=2;i=385**.</span><span class="sxs-lookup"><span data-stu-id="753ed-177">The first node in the assembly station for production line 1 in Munich has a value **ns=2;i=385**.</span></span> <span data-ttu-id="753ed-178">Il valore **NodeId** specifica l'elemento dati da leggere dal server OPC UA, mentre il valore **SymbolicName** fornisce un nome descrittivo da usare nel dashboard per tali dati.</span><span class="sxs-lookup"><span data-stu-id="753ed-178">A **NodeId** value specifies the data item to read from the OPC UA server, and the **SymbolicName** provides a user-friendly name to use in the dashboard for that data.</span></span>

<span data-ttu-id="753ed-179">Altri valori associati a ogni nodo sono riepilogati nella tabella riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="753ed-179">Other values associated with each node are summarized in the following table:</span></span>

| <span data-ttu-id="753ed-180">Valore</span><span class="sxs-lookup"><span data-stu-id="753ed-180">Value</span></span> | <span data-ttu-id="753ed-181">Descrizione</span><span class="sxs-lookup"><span data-stu-id="753ed-181">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="753ed-182">Pertinenza</span><span class="sxs-lookup"><span data-stu-id="753ed-182">Relevance</span></span>  | <span data-ttu-id="753ed-183">Gli indicatori KPI e i valori OEE cui contribuiscono questi dati.</span><span class="sxs-lookup"><span data-stu-id="753ed-183">The KPI and OEE values this data contributes to.</span></span> |
| <span data-ttu-id="753ed-184">OpCode</span><span class="sxs-lookup"><span data-stu-id="753ed-184">OpCode</span></span>     | <span data-ttu-id="753ed-185">Il modo in cui i dati vengono aggregati.</span><span class="sxs-lookup"><span data-stu-id="753ed-185">How the data is aggregated.</span></span> |
| <span data-ttu-id="753ed-186">Unità</span><span class="sxs-lookup"><span data-stu-id="753ed-186">Units</span></span>      | <span data-ttu-id="753ed-187">Le unità da usare nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="753ed-187">The units to use in the dashboard.</span></span>  |
| <span data-ttu-id="753ed-188">Visible</span><span class="sxs-lookup"><span data-stu-id="753ed-188">Visible</span></span>    | <span data-ttu-id="753ed-189">Indica se il valore viene visualizzato nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="753ed-189">Whether to display this value in the dashboard.</span></span> <span data-ttu-id="753ed-190">Alcuni valori vengono usati nei calcoli, ma non visualizzati.</span><span class="sxs-lookup"><span data-stu-id="753ed-190">Some values are used in calculations but not displayed.</span></span>  |
| <span data-ttu-id="753ed-191">Massima</span><span class="sxs-lookup"><span data-stu-id="753ed-191">Maximum</span></span>    | <span data-ttu-id="753ed-192">Il valore massimo che attiva un avviso nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="753ed-192">The maximum value that triggers an alert in the dashboard.</span></span> |
| <span data-ttu-id="753ed-193">MaximumAlertActions</span><span class="sxs-lookup"><span data-stu-id="753ed-193">MaximumAlertActions</span></span> | <span data-ttu-id="753ed-194">Azione da intraprendere in risposta a un avviso.</span><span class="sxs-lookup"><span data-stu-id="753ed-194">An action to take in response to an alert.</span></span> <span data-ttu-id="753ed-195">Ad esempio, l'invio di un comando a una stazione.</span><span class="sxs-lookup"><span data-stu-id="753ed-195">For example, send a command to a station.</span></span> |
| <span data-ttu-id="753ed-196">ConstValue</span><span class="sxs-lookup"><span data-stu-id="753ed-196">ConstValue</span></span> | <span data-ttu-id="753ed-197">Un valore costante usato in un calcolo.</span><span class="sxs-lookup"><span data-stu-id="753ed-197">A constant value used in a calculation.</span></span> |

## <a name="deploy-the-changes"></a><span data-ttu-id="753ed-198">Distribuire le modifiche</span><span class="sxs-lookup"><span data-stu-id="753ed-198">Deploy the changes</span></span>

<span data-ttu-id="753ed-199">Dopo avere apportato modifiche al file **ContosoTopologyDescription.json**, è necessario ridistribuire la soluzione di fabbrica connessa nel proprio account Azure.</span><span class="sxs-lookup"><span data-stu-id="753ed-199">When you have finished making changes to the **ContosoTopologyDescription.json** file, you must redeploy the connected factory solution to your Azure account.</span></span>

<span data-ttu-id="753ed-200">Il repository **azure-iot-connected-factory** include uno script PowerShell **build.ps1** che è possibile usare per ricompilare e distribuire la soluzione.</span><span class="sxs-lookup"><span data-stu-id="753ed-200">The **azure-iot-connected-factory** repository includes a **build.ps1** PowerShell script you can use to rebuild and deploy the solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="753ed-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="753ed-201">Next Steps</span></span>

<span data-ttu-id="753ed-202">Altre informazioni sulla soluzione preconfigurata di fabbrica connessa sono disponibili nei seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="753ed-202">Learn more about the connected factory preconfigured solution by reading the following articles:</span></span>

* <span data-ttu-id="753ed-203">[Procedura dettagliata per la soluzione preconfigurata di connected factory][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="753ed-203">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="753ed-204">[Distribuire un gateway per fabbrica connessa][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="753ed-204">[Deploy a gateway for connected factory][lnk-connect-cf]</span></span>
* <span data-ttu-id="753ed-205">[Autorizzazioni per il sito azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="753ed-205">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="753ed-206">Domande frequenti sulla soluzione di connected factory</span><span class="sxs-lookup"><span data-stu-id="753ed-206">Connected factory FAQ</span></span>](iot-suite-faq-cf.md)
* <span data-ttu-id="753ed-207">[Domande frequenti][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="753ed-207">[FAQ][lnk-faq]</span></span>


[img-oee-kpi]: ./media/iot-suite-connected-factory-customize/oeenadkpi.png
[img-manufactured-items]: ./media/iot-suite-connected-factory-customize/manufactured.png
[img-tsi]: ./media/iot-suite-connected-factory-customize/tsi.png
[img-select-server]: ./media/iot-suite-connected-factory-customize/selectserver.png
[img-published]: ./media/iot-suite-connected-factory-customize/published.png
[img-munich]: ./media/iot-suite-connected-factory-customize/munich.png
[img-server-uris]: ./media/iot-suite-connected-factory-customize/serveruris.png
[lnk-kpi]: ./media/iot-suite-connected-factory-customize/kpidisplay.png

[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md