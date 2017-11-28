---
title: aaaCustomize Azure IoT Suite connesso factory | Documenti Microsoft
description: "Una descrizione delle modalità di comportamento hello toocustomize di hello connessione factory preconfigurato soluzione."
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
ms.openlocfilehash: 53f2fef7a76b5d8e6ad023945a7812dc7fabd12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-how-hello-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a><span data-ttu-id="6276e-103">Personalizzare la modalità di connessione factory soluzione consente di visualizzare dati dai server OPC UA hello</span><span class="sxs-lookup"><span data-stu-id="6276e-103">Customize how hello connected factory solution displays data from your OPC UA servers</span></span>

## <a name="introduction"></a><span data-ttu-id="6276e-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="6276e-104">Introduction</span></span>

<span data-ttu-id="6276e-105">Hello factory connesso soluzione aggrega e visualizza i dati di hello OPC UA server connesso toohello soluzione.</span><span class="sxs-lookup"><span data-stu-id="6276e-105">hello connected factory solution aggregates and displays data from hello OPC UA servers connected toohello solution.</span></span> <span data-ttu-id="6276e-106">È possibile esplorare e inviare comandi toohello OPC UA server nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="6276e-106">You can browse and send commands toohello OPC UA servers in your solution.</span></span> <span data-ttu-id="6276e-107">Per ulteriori informazioni su OPC UA, vedere hello [connesso domande frequenti sulla factory](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="6276e-107">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

<span data-ttu-id="6276e-108">Sono esempi di dati aggregati in soluzione hello hello l'efficienza di apparecchiature complessivo (OEE) e indicatori di prestazioni chiave (KPI) che è possibile visualizzare nel dashboard di hello livello di factory hello, riga e di espansione.</span><span class="sxs-lookup"><span data-stu-id="6276e-108">Examples of aggregated data in hello solution include hello Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) that you can view in hello dashboard at hello factory, line, and station levels.</span></span> <span data-ttu-id="6276e-109">Hello schermata riportata di seguito vengono illustrati hello OEE e indicatori KPI valori per hello **Assembly** nella stazione **produzione riga 1**, in hello **Monaco** factory:</span><span class="sxs-lookup"><span data-stu-id="6276e-109">hello following screenshot shows hello OEE and KPI values for hello **Assembly** station, on **Production line 1**, in hello **Munich** factory:</span></span>

![Esempio di valori OEE e un indicatore KPI nella soluzione hello][img-oee-kpi]

<span data-ttu-id="6276e-111">Consente di Hello è tooview informazioni dagli elementi di dati specifico da hello Server OPC UA, detti *stazioni*.</span><span class="sxs-lookup"><span data-stu-id="6276e-111">hello solution enables you tooview detailed information from specific data items from hello OPC UA servers, called *stations*.</span></span> <span data-ttu-id="6276e-112">Hello schermata seguente mostra tracciati totale hello degli articoli a una stazione specifico:</span><span class="sxs-lookup"><span data-stu-id="6276e-112">hello following screenshot shows plots of hello number of manufactured items from a specific station:</span></span>

![Tracciati del numero di articoli prodotti][img-manufactured-items]

<span data-ttu-id="6276e-114">Se si fa clic su uno dei grafici hello, è possibile esplorare i dati di hello usando ora serie Insights (STI):</span><span class="sxs-lookup"><span data-stu-id="6276e-114">If you click one of hello graphs, you can explore hello data further using Time Series Insights (TSI):</span></span>

![Esplorare i dati con Time Series Insights][img-tsi]

<span data-ttu-id="6276e-116">L'articolo illustra:</span><span class="sxs-lookup"><span data-stu-id="6276e-116">This article describes:</span></span>

- <span data-ttu-id="6276e-117">Come dati hello vengono resa disponibile toohello diverse visualizzazioni in soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="6276e-117">How hello data is made available toohello various views in hello solution.</span></span>
- <span data-ttu-id="6276e-118">Come è possibile personalizzare soluzione hello hello Visualizza dati hello.</span><span class="sxs-lookup"><span data-stu-id="6276e-118">How you can customize hello way hello solution displays hello data.</span></span>

## <a name="data-sources"></a><span data-ttu-id="6276e-119">Origini dati</span><span class="sxs-lookup"><span data-stu-id="6276e-119">Data sources</span></span>

<span data-ttu-id="6276e-120">Hello factory connesso soluzione consente di visualizzare dati da hello OPC UA server collegati toohello soluzione.</span><span class="sxs-lookup"><span data-stu-id="6276e-120">hello connected factory solution displays data from hello OPC UA servers connected toohello solution.</span></span> <span data-ttu-id="6276e-121">installazione predefinita di Hello include diversi OPC UA che eseguono una simulazione di factory.</span><span class="sxs-lookup"><span data-stu-id="6276e-121">hello default installation includes several OPC UA servers running a factory simulation.</span></span> <span data-ttu-id="6276e-122">È possibile aggiungere i propri server OPC UA che [connettersi tramite un gateway] [ lnk-connect-cf] tooyour soluzione.</span><span class="sxs-lookup"><span data-stu-id="6276e-122">You can add your own OPC UA servers that [connect through a gateway][lnk-connect-cf] tooyour solution.</span></span>

<span data-ttu-id="6276e-123">È possibile esplorare gli elementi di dati hello che un server OPC UA connesso può inviare tooyour soluzione nel dashboard di hello:</span><span class="sxs-lookup"><span data-stu-id="6276e-123">You can browse hello data items that a connected OPC UA server can send tooyour solution in hello dashboard:</span></span>

1. <span data-ttu-id="6276e-124">Passare toohello **selezionare un server OPC UA** Vista:</span><span class="sxs-lookup"><span data-stu-id="6276e-124">Navigate toohello **Select an OPC UA server** view:</span></span>

    ![Passare toohello selezionare una visualizzazione di server UA OPC][img-select-server]

1. <span data-ttu-id="6276e-126">Selezionare un server e fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="6276e-126">Select a server and click **Connect**.</span></span> <span data-ttu-id="6276e-127">Fare clic su **procedere** quando viene visualizzata avviso di sicurezza hello.</span><span class="sxs-lookup"><span data-stu-id="6276e-127">Click **Proceed** when hello security warning appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6276e-128">Solo, questo avviso viene visualizzato una volta per ogni server e stabilisce una relazione di trust tra il dashboard di soluzione hello e server hello.</span><span class="sxs-lookup"><span data-stu-id="6276e-128">This warning only appears once for each server and establishes a trust relationship between hello solution dashboard and hello server.</span></span>

1. <span data-ttu-id="6276e-129">È ora Sfoglia hello gli elementi di dati hello server possono inviare toohello soluzione possibile.</span><span class="sxs-lookup"><span data-stu-id="6276e-129">You can now browse hello data items that hello server can send toohello solution.</span></span> <span data-ttu-id="6276e-130">Gli elementi che vengono inviati toohello soluzione hanno un segno di spunta verde:</span><span class="sxs-lookup"><span data-stu-id="6276e-130">Items that are being sent toohello solution have a green check mark:</span></span>

    ![Elementi pubblicati][img-published]

1. <span data-ttu-id="6276e-132">Se si è un *amministratore* nella soluzione hello, è possibile scegliere toopublish un toomake di elemento di dati è disponibile in hello connessa soluzione factory.</span><span class="sxs-lookup"><span data-stu-id="6276e-132">If you are an *Administrator* in hello solution, you can choose toopublish a data item toomake it available in hello connected factory solution.</span></span> <span data-ttu-id="6276e-133">Come amministratore, è anche possibile modificare il valore di hello di elementi di dati e chiamare metodi hello server UA OPC.</span><span class="sxs-lookup"><span data-stu-id="6276e-133">As an Administrator, you can also change hello value of data items and call methods in hello OPC UA server.</span></span>

## <a name="map-hello-data"></a><span data-ttu-id="6276e-134">Dati della mappa hello</span><span class="sxs-lookup"><span data-stu-id="6276e-134">Map hello data</span></span>

<span data-ttu-id="6276e-135">Hello connessi factory soluzione mappe e hello aggregazioni elementi di dati pubblicati da hello OPC UA server toohello diverse visualizzazioni soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="6276e-135">hello connected factory solution maps and aggregates hello published data items from hello OPC UA server toohello various views in hello solution.</span></span> <span data-ttu-id="6276e-136">Hello factory connesso soluzione distribuisce tooyour account Azure quando si esegue il provisioning di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="6276e-136">hello connected factory solution deploys tooyour Azure account when you provision hello solution.</span></span> <span data-ttu-id="6276e-137">Un file JSON di hello soluzione di Visual Studio connesso factory memorizza queste informazioni di mapping.</span><span class="sxs-lookup"><span data-stu-id="6276e-137">A JSON file in hello Visual Studio connected factory solution stores this mapping information.</span></span> <span data-ttu-id="6276e-138">È possibile visualizzare e modificare il file di configurazione JSON nella factory connesso hello soluzione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6276e-138">You can view and modify this JSON configuration file in hello connected factory Visual Studio solution.</span></span> <span data-ttu-id="6276e-139">Dopo aver apportato una modifica, è possibile ridistribuire la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="6276e-139">You can redeploy hello solution after you make a change.</span></span>

<span data-ttu-id="6276e-140">È possibile utilizzare file di configurazione hello:</span><span class="sxs-lookup"><span data-stu-id="6276e-140">You can use hello configuration file to:</span></span>

- <span data-ttu-id="6276e-141">Modificare factory simulato esistente hello, linee di produzione e le stazioni.</span><span class="sxs-lookup"><span data-stu-id="6276e-141">Edit hello existing simulated factories, production lines, and stations.</span></span>
- <span data-ttu-id="6276e-142">Eseguire il mapping di dati da Server OPC UA reali che si connette toohello soluzione.</span><span class="sxs-lookup"><span data-stu-id="6276e-142">Map data from real OPC UA servers that you connect toohello solution.</span></span>

<span data-ttu-id="6276e-143">una copia di hello tooclone connesso soluzione di Visual Studio factory, hello di utilizzare il comando di git seguente:</span><span class="sxs-lookup"><span data-stu-id="6276e-143">tooclone a copy of hello connected factory Visual Studio solution, use hello following git command:</span></span>

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

<span data-ttu-id="6276e-144">file Hello **ContosoTopologyDescription.json** definisce hello visualizzazioni del mapping di dati del server OPC UA hello elementi toohello nel dashboard di soluzione hello factory connesso.</span><span class="sxs-lookup"><span data-stu-id="6276e-144">hello file **ContosoTopologyDescription.json** defines hello mapping from hello OPC UA server data items toohello views in hello connected factory solution dashboard.</span></span> <span data-ttu-id="6276e-145">È possibile trovare questo file di configurazione in hello **Contoso\Topology** cartella hello **WebApp** progetto nella soluzione di Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="6276e-145">You can find this configuration file in hello **Contoso\Topology** folder in hello **WebApp** project in hello Visual Studio solution.</span></span>

<span data-ttu-id="6276e-146">organizzazione Hello del contenuto del file JSON hello come una gerarchia di nodi di stazione, linea di produzione e factory.</span><span class="sxs-lookup"><span data-stu-id="6276e-146">hello content of hello JSON file is organized as a hierarchy of factory, production line, and station nodes.</span></span> <span data-ttu-id="6276e-147">Questa gerarchia definisce la gerarchia di navigazione hello nel dashboard di hello factory connesso.</span><span class="sxs-lookup"><span data-stu-id="6276e-147">This hierarchy defines hello navigation hierarchy in hello connected factory dashboard.</span></span> <span data-ttu-id="6276e-148">I valori in ogni nodo della gerarchia hello determinano informazioni hello visualizzate nel dashboard di hello.</span><span class="sxs-lookup"><span data-stu-id="6276e-148">Values at each node of hello hierarchy determine hello information displayed in hello dashboard.</span></span> <span data-ttu-id="6276e-149">Ad esempio, file JSON hello contiene hello seguenti valori per hello factory Monaco:</span><span class="sxs-lookup"><span data-stu-id="6276e-149">For example, hello JSON file contains hello following values for hello Munich factory:</span></span>

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

<span data-ttu-id="6276e-150">percorso, la descrizione e nome hello vengono visualizzati in questa visualizzazione nel dashboard di hello:</span><span class="sxs-lookup"><span data-stu-id="6276e-150">hello name, description, and location appear on this view in hello dashboard:</span></span>

![Dati Monaco nel dashboard di hello][img-munich]

<span data-ttu-id="6276e-152">Ogni stabilimento, linea di produzione e stazione ha una proprietà immagine.</span><span class="sxs-lookup"><span data-stu-id="6276e-152">Each factory, production line, and station have an image property.</span></span> <span data-ttu-id="6276e-153">È possibile trovare questi file JPEG in hello **Content\img** cartella hello **WebApp** progetto.</span><span class="sxs-lookup"><span data-stu-id="6276e-153">You can find these JPEG files in hello **Content\img** folder in hello **WebApp** project.</span></span> <span data-ttu-id="6276e-154">Questi file di immagine visualizzano nel dashboard di factory connesso hello.</span><span class="sxs-lookup"><span data-stu-id="6276e-154">These image files display in hello connected factory dashboard.</span></span>

<span data-ttu-id="6276e-155">Ogni stazione include diverse proprietà dettagliate che definiscono i mapping di elementi di dati dalla hello OPC UA hello.</span><span class="sxs-lookup"><span data-stu-id="6276e-155">Each station includes several detailed properties that define hello mapping from hello OPC UA data items.</span></span> <span data-ttu-id="6276e-156">Queste proprietà sono descritte in hello le sezioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6276e-156">These properties are described in hello following sections:</span></span>

### <a name="opcuri"></a><span data-ttu-id="6276e-157">OpcUri</span><span class="sxs-lookup"><span data-stu-id="6276e-157">OpcUri</span></span>

<span data-ttu-id="6276e-158">Hello **OpcUri** valore è hello OPC UA Application URI che identifica in modo univoco hello server UA OPC.</span><span class="sxs-lookup"><span data-stu-id="6276e-158">hello **OpcUri** value is hello OPC UA Application URI that uniquely identifies hello OPC UA server.</span></span> <span data-ttu-id="6276e-159">Ad esempio, hello **OpcUri** stazione assembly hello nella riga di produzione 1 Monaco simile hello seguente valore: **urn: scada2194:ua:munich:productionline0:assemblystation**.</span><span class="sxs-lookup"><span data-stu-id="6276e-159">For example, hello **OpcUri** value for hello assembly station on production line 1 in Munich looks like hello following: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span></span>

<span data-ttu-id="6276e-160">È possibile visualizzare hello URI del server OPC UA hello connesso nel dashboard di soluzione hello:</span><span class="sxs-lookup"><span data-stu-id="6276e-160">You can view hello URIs of hello connected OPC UA servers in hello solution dashboard:</span></span>

![Visualizzare gli URI dei server OPC UA][img-server-uris]

### <a name="simulation"></a><span data-ttu-id="6276e-162">Simulazione</span><span class="sxs-lookup"><span data-stu-id="6276e-162">Simulation</span></span>

<span data-ttu-id="6276e-163">informazioni di hello Hello **simulazione** nodo è specifico toohello simulazione OPC UA che viene eseguito in hello Server OPC UA sottoposti a provisioning per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="6276e-163">hello information in hello **Simulation** node is specific toohello OPC UA simulation that runs in hello OPC UA servers that are provisioned by default.</span></span> <span data-ttu-id="6276e-164">Non vengono usate per un server OPC UA reale.</span><span class="sxs-lookup"><span data-stu-id="6276e-164">It is not used for a real OPC UA server.</span></span>

### <a name="kpi1-and-kpi2"></a><span data-ttu-id="6276e-165">Kpi1 e Kpi2</span><span class="sxs-lookup"><span data-stu-id="6276e-165">Kpi1 and Kpi2</span></span>

<span data-ttu-id="6276e-166">Questi nodi vengono descritti come dati di stazione hello contribuiscono toohello due valori di indicatore KPI nel dashboard di hello.</span><span class="sxs-lookup"><span data-stu-id="6276e-166">These nodes describe how data from hello station contributes toohello two KPI values in hello dashboard.</span></span> <span data-ttu-id="6276e-167">In una distribuzione predefinita, questi indicatori KPI rappresentano unità all'ora e kWh all'ora.</span><span class="sxs-lookup"><span data-stu-id="6276e-167">In a default deployment, these KPI values are units per hour and kWh per hour.</span></span> <span data-ttu-id="6276e-168">soluzione Hello calcola i valori di indicatore KPI a livello di hello una stazione e li aggrega alla linea di produzione hello e livelli di factory.</span><span class="sxs-lookup"><span data-stu-id="6276e-168">hello solution calculates KPI vales at hello level of a station and aggregates them at hello production line and factory levels.</span></span>

<span data-ttu-id="6276e-169">Ogni indicatore KPI ha un valore minimo, un valore massimo e un valore di destinazione</span><span class="sxs-lookup"><span data-stu-id="6276e-169">Each KPI has a minimum, maximum, and target value.</span></span> <span data-ttu-id="6276e-170">Ogni valore dell'indicatore KPI è inoltre possibile definire le azioni di allarme per hello connesso factory soluzione tooperform.</span><span class="sxs-lookup"><span data-stu-id="6276e-170">Each KPI value can also define alert actions for hello connected factory solution tooperform.</span></span> <span data-ttu-id="6276e-171">Hello frammento seguente mostra le definizioni KPI hello per stazione assembly hello nella riga di produzione 1 Monaco:</span><span class="sxs-lookup"><span data-stu-id="6276e-171">hello following snippet shows hello KPI definitions for hello assembly station on production line 1 in Munich:</span></span>

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

<span data-ttu-id="6276e-172">Hello seguente schermata Mostra dati KPI hello nel dashboard di hello.</span><span class="sxs-lookup"><span data-stu-id="6276e-172">hello following screenshot shows hello KPI data in hello dashboard.</span></span>

![Informazioni relative ai KPI nel dashboard di hello][lnk-kpi]

### <a name="opcnodes"></a><span data-ttu-id="6276e-174">OpcNodes</span><span class="sxs-lookup"><span data-stu-id="6276e-174">OpcNodes</span></span>

<span data-ttu-id="6276e-175">Hello **OpcNodes** nodi identificano gli elementi di dati pubblicati da hello server OPC UA hello e specificare come tooprocess tali dati.</span><span class="sxs-lookup"><span data-stu-id="6276e-175">hello **OpcNodes** nodes identify hello published data items from hello OPC UA server and specify how tooprocess that data.</span></span>

<span data-ttu-id="6276e-176">Hello **NodeId** valore identifica hello NodeID di UA OPC specifico da hello server UA OPC.</span><span class="sxs-lookup"><span data-stu-id="6276e-176">hello **NodeId** value identifies hello specific OPC UA NodeID from hello OPC UA server.</span></span> <span data-ttu-id="6276e-177">Hello primo nodo in una stazione di assembly hello per linea di produzione 1 Monaco ha un valore **ns = 2, i = 385**.</span><span class="sxs-lookup"><span data-stu-id="6276e-177">hello first node in hello assembly station for production line 1 in Munich has a value **ns=2;i=385**.</span></span> <span data-ttu-id="6276e-178">Oggetto **NodeId** valore specifica hello dati elemento tooread dal server OPC UA hello e hello **SymbolicName** fornisce un nome descrittivo toouse nel dashboard di hello per tali dati.</span><span class="sxs-lookup"><span data-stu-id="6276e-178">A **NodeId** value specifies hello data item tooread from hello OPC UA server, and hello **SymbolicName** provides a user-friendly name toouse in hello dashboard for that data.</span></span>

<span data-ttu-id="6276e-179">Altri valori associati a ogni nodo sono riepilogati nella seguente tabella hello:</span><span class="sxs-lookup"><span data-stu-id="6276e-179">Other values associated with each node are summarized in hello following table:</span></span>

| <span data-ttu-id="6276e-180">Valore</span><span class="sxs-lookup"><span data-stu-id="6276e-180">Value</span></span> | <span data-ttu-id="6276e-181">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6276e-181">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6276e-182">Pertinenza</span><span class="sxs-lookup"><span data-stu-id="6276e-182">Relevance</span></span>  | <span data-ttu-id="6276e-183">i valori di indicatore KPI e OEE Hello dati contribuiscono a.</span><span class="sxs-lookup"><span data-stu-id="6276e-183">hello KPI and OEE values this data contributes to.</span></span> |
| <span data-ttu-id="6276e-184">OpCode</span><span class="sxs-lookup"><span data-stu-id="6276e-184">OpCode</span></span>     | <span data-ttu-id="6276e-185">Come vengono aggregati i dati hello.</span><span class="sxs-lookup"><span data-stu-id="6276e-185">How hello data is aggregated.</span></span> |
| <span data-ttu-id="6276e-186">Unità</span><span class="sxs-lookup"><span data-stu-id="6276e-186">Units</span></span>      | <span data-ttu-id="6276e-187">Hello unità toouse nel dashboard di hello.</span><span class="sxs-lookup"><span data-stu-id="6276e-187">hello units toouse in hello dashboard.</span></span>  |
| <span data-ttu-id="6276e-188">Visible</span><span class="sxs-lookup"><span data-stu-id="6276e-188">Visible</span></span>    | <span data-ttu-id="6276e-189">Se toodisplay questo valore nelle dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="6276e-189">Whether toodisplay this value in hello dashboard.</span></span> <span data-ttu-id="6276e-190">Alcuni valori vengono usati nei calcoli, ma non visualizzati.</span><span class="sxs-lookup"><span data-stu-id="6276e-190">Some values are used in calculations but not displayed.</span></span>  |
| <span data-ttu-id="6276e-191">Massima</span><span class="sxs-lookup"><span data-stu-id="6276e-191">Maximum</span></span>    | <span data-ttu-id="6276e-192">valore massimo Hello che attiva un avviso nel dashboard di hello.</span><span class="sxs-lookup"><span data-stu-id="6276e-192">hello maximum value that triggers an alert in hello dashboard.</span></span> |
| <span data-ttu-id="6276e-193">MaximumAlertActions</span><span class="sxs-lookup"><span data-stu-id="6276e-193">MaximumAlertActions</span></span> | <span data-ttu-id="6276e-194">Tootake un'azione nell'avviso tooan di risposta.</span><span class="sxs-lookup"><span data-stu-id="6276e-194">An action tootake in response tooan alert.</span></span> <span data-ttu-id="6276e-195">Ad esempio, inviare una stazione tooa di comando.</span><span class="sxs-lookup"><span data-stu-id="6276e-195">For example, send a command tooa station.</span></span> |
| <span data-ttu-id="6276e-196">ConstValue</span><span class="sxs-lookup"><span data-stu-id="6276e-196">ConstValue</span></span> | <span data-ttu-id="6276e-197">Un valore costante usato in un calcolo.</span><span class="sxs-lookup"><span data-stu-id="6276e-197">A constant value used in a calculation.</span></span> |

## <a name="deploy-hello-changes"></a><span data-ttu-id="6276e-198">Distribuire le modifiche di hello</span><span class="sxs-lookup"><span data-stu-id="6276e-198">Deploy hello changes</span></span>

<span data-ttu-id="6276e-199">Dopo avere apportato modifiche toohello **ContosoTopologyDescription.json** file, è necessario ridistribuire hello connesso factory soluzione tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="6276e-199">When you have finished making changes toohello **ContosoTopologyDescription.json** file, you must redeploy hello connected factory solution tooyour Azure account.</span></span>

<span data-ttu-id="6276e-200">Hello **azure iot-connessione-factory** repository include un **build.ps1** script di PowerShell, è possibile utilizzare toorebuild e distribuire la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="6276e-200">hello **azure-iot-connected-factory** repository includes a **build.ps1** PowerShell script you can use toorebuild and deploy hello solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6276e-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6276e-201">Next Steps</span></span>

<span data-ttu-id="6276e-202">Ulteriori informazioni sulla soluzione factory preconfigurato hello connesso da lettura hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="6276e-202">Learn more about hello connected factory preconfigured solution by reading hello following articles:</span></span>

* <span data-ttu-id="6276e-203">[Procedura dettagliata per la soluzione preconfigurata di connected factory][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="6276e-203">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="6276e-204">[Distribuire un gateway per fabbrica connessa][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="6276e-204">[Deploy a gateway for connected factory][lnk-connect-cf]</span></span>
* <span data-ttu-id="6276e-205">[Autorizzazioni nel sito azureiotsuite.com hello][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="6276e-205">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="6276e-206">Domande frequenti sulla soluzione di connected factory</span><span class="sxs-lookup"><span data-stu-id="6276e-206">Connected factory FAQ</span></span>](iot-suite-faq-cf.md)
* <span data-ttu-id="6276e-207">[Domande frequenti][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="6276e-207">[FAQ][lnk-faq]</span></span>


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