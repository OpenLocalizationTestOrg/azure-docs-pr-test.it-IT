---
title: toouse aaaHow con REST di Power BI Embedded | Documenti Microsoft
description: 'Informazioni su come toouse con REST di Power BI Embedded '
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 8bcef780-cca0-4f30-9a9b-9daa1a7ae865
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 02/06/2017
ms.author: asaxton
ms.openlocfilehash: 98057724e60ba868f9c93de8c50383569eb8852d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-power-bi-embedded-with-rest"></a><span data-ttu-id="424c6-103">Come toouse con REST di Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="424c6-103">How toouse Power BI Embedded with REST</span></span>

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a><span data-ttu-id="424c6-104">Power BI Embedded: che cos'è e a cosa serve</span><span class="sxs-lookup"><span data-stu-id="424c6-104">Power BI Embedded: What it is and what it's for</span></span>

<span data-ttu-id="424c6-105">Una panoramica di Power BI Embedded descritto ufficiale hello [sito Power BI Embedded](https://azure.microsoft.com/services/power-bi-embedded/), ma verrà esaminata rapidamente prima di passare in dettaglio hello per utilizzarlo con REST.</span><span class="sxs-lookup"><span data-stu-id="424c6-105">An overview of Power BI Embedded is described in hello official [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), but let's take a quick look before we get into hello details about using it with REST.</span></span>

<span data-ttu-id="424c6-106">È davvero semplice.</span><span class="sxs-lookup"><span data-stu-id="424c6-106">It's quite simple, really.</span></span> <span data-ttu-id="424c6-107">potrebbe essere visualizzazioni di dati dinamica hello toouse di [Power BI](https://powerbi.microsoft.com) nella propria applicazione.</span><span class="sxs-lookup"><span data-stu-id="424c6-107">you may want toouse hello dynamic data visualizations of [Power BI](https://powerbi.microsoft.com) in your own application.</span></span>

<span data-ttu-id="424c6-108">La maggior parte delle applicazioni personalizzate necessario dati hello toodeliver ai propri clienti, non necessariamente gli utenti nella propria organizzazione.</span><span class="sxs-lookup"><span data-stu-id="424c6-108">Most custom applications need toodeliver hello data for their own customers, not necessarily users in their own organization.</span></span> <span data-ttu-id="424c6-109">Ad esempio, se si sta offrendo alcuni servizi per la società e la società B, gli utenti nella società dovrebbero visualizzare solo dati per la propria società A. Vale a dire, multi-tenancy hello è necessaria per il recapito di hello.</span><span class="sxs-lookup"><span data-stu-id="424c6-109">For example, if you're delivering some service for both company A and company B, users in company A should only see data for their own company A. That is, hello multi-tenancy is needed for hello delivery.</span></span>

<span data-ttu-id="424c6-110">applicazione personalizzata Hello potrebbe anche essere offerta propri metodi di autenticazione, ad esempio l'autenticazione form, autenticazione di base, e così via...</span><span class="sxs-lookup"><span data-stu-id="424c6-110">hello custom application might also be offering its own authentication methods such as forms auth, basic auth, etc..</span></span> <span data-ttu-id="424c6-111">Quindi, hello incorporamento soluzione deve collaborare in modo sicuro con questo metodo di autenticazione esistente.</span><span class="sxs-lookup"><span data-stu-id="424c6-111">Then, hello embedding solution must collaborate with this existing authentication methods safely.</span></span> <span data-ttu-id="424c6-112">È inoltre necessario per gli utenti toobe in grado di toouse tali applicazioni di ISV senza hello acquisto aggiuntiva o licenze di una sottoscrizione di Power BI.</span><span class="sxs-lookup"><span data-stu-id="424c6-112">It's also necessary for users toobe able toouse those ISV applications without hello extra purchase or licensing of a Power BI subscription.</span></span>

 <span data-ttu-id="424c6-113">**Power BI Embedded** è progettato esattamente per questi tipi di scenari.</span><span class="sxs-lookup"><span data-stu-id="424c6-113">**Power BI Embedded** is designed for precisely these kinds of scenarios.</span></span> <span data-ttu-id="424c6-114">In tal caso, ora che è disponibile tale introduzione fuori modo hello, iniziamo in dettaglio</span><span class="sxs-lookup"><span data-stu-id="424c6-114">So, now that we have that quick introduction out of hello way, let's get into some details</span></span>

<span data-ttu-id="424c6-115">È possibile usare .NET hello \(c#) o Node.js SDK, tooeasily compilare l'applicazione con Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="424c6-115">You can use hello .NET \(C#) or Node.js SDK, tooeasily build your application with Power BI Embedded.</span></span> <span data-ttu-id="424c6-116">Tuttavia, in questo articolo verrà illustrato il flusso HTTP \(tra cui AuthN) di Power BI senza SDK.</span><span class="sxs-lookup"><span data-stu-id="424c6-116">But, in this article, we'll explain about HTTP flow \(incl. AuthN) of Power BI without SDKs.</span></span> <span data-ttu-id="424c6-117">Questo flusso, è possibile compilare l'applicazione **con qualsiasi linguaggio di programmazione**, e si possono comprendere eccessivamente le tracce di hello di Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="424c6-117">Understanding this flow, you can build your application **with any programming language**, and you can understand deeply hello essence of Power BI Embedded.</span></span>

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a><span data-ttu-id="424c6-118">Creare una raccolta di aree di lavoro di Power BI e ottenere la chiave di accesso \(provisioning)</span><span class="sxs-lookup"><span data-stu-id="424c6-118">Create Power BI workspace collection, and get access key \(Provisioning)</span></span>

<span data-ttu-id="424c6-119">Power BI incorporato è uno dei hello servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="424c6-119">Power BI Embedded is one of hello Azure services.</span></span> <span data-ttu-id="424c6-120">Solo hello ISV che usa il portale di Azure verrà addebitato i costi di utilizzo \(per la sessione utente di ogni ora), e gli utenti hello report hello viste non viene addebitato o persino richiede una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="424c6-120">Only hello ISV who uses Azure Portal is charged for usage fees \(per hourly user session), and hello user who views hello report isn't charged or even require an Azure subscription.</span></span>
<span data-ttu-id="424c6-121">Prima di iniziare lo sviluppo di applicazioni, è necessario creare hello **raccolta dell'area di lavoro di Power BI** tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="424c6-121">Before starting our application development, we must create hello **Power BI workspace collection** by using Azure Portal.</span></span>

<span data-ttu-id="424c6-122">Ogni area di lavoro di Power BI Embedded è l'area di lavoro di hello per ogni cliente (tenant) e possiamo aggiungere molte aree di lavoro in ogni raccolta di area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="424c6-122">Each workspace of Power BI Embedded is hello workspace for each customer (tenant), and we can add many workspaces in each workspace collection.</span></span> <span data-ttu-id="424c6-123">Hello stessa chiave di accesso viene utilizzato in ogni raccolta di area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="424c6-123">hello same access key is used in each workspace collection.</span></span> <span data-ttu-id="424c6-124">In concreto, raccolta di area di lavoro hello è il limite di sicurezza hello per Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="424c6-124">In-effect, hello workspace collection is hello security boundary for Power BI Embedded.</span></span>

![](media/power-bi-embedded-iframe/create-workspace.png)

<span data-ttu-id="424c6-125">Dopo il completamento di creazione della raccolta di hello dell'area di lavoro, copiare la chiave di accesso hello dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="424c6-125">When we finish creating hello workspace collection, copy hello access key from Azure Portal.</span></span>

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> <span data-ttu-id="424c6-126">È anche possibile eseguire il provisioning hello dell'area di lavoro raccolta e ottenere la chiave di accesso tramite l'API REST.</span><span class="sxs-lookup"><span data-stu-id="424c6-126">We can also provision hello workspace collection and get access key via REST API.</span></span> <span data-ttu-id="424c6-127">vedere, più toolearn [API del Provider di risorse di Power BI](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="424c6-127">toolearn more, see [Power BI Resource Provider APIs](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span></span>

## <a name="create-pbix-file-with-power-bi-desktop"></a><span data-ttu-id="424c6-128">Creare file con estensione pbix con Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="424c6-128">Create .pbix file with Power BI Desktop</span></span>

<span data-ttu-id="424c6-129">Successivamente, è necessario creare connessione dati hello e toobe report incorporato.</span><span class="sxs-lookup"><span data-stu-id="424c6-129">Next, we must create hello data connection and reports toobe embedded.</span></span>
<span data-ttu-id="424c6-130">Per questa attività, non è disponibile alcun codice o programmazione.</span><span class="sxs-lookup"><span data-stu-id="424c6-130">For this task, there’s no programming or code.</span></span> <span data-ttu-id="424c6-131">È sufficiente usare Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="424c6-131">We just use Power BI Desktop.</span></span>
<span data-ttu-id="424c6-132">In questo articolo non verranno esaminate tramite informazioni dettagliate hello toouse Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="424c6-132">In this article, we won't go through hello details about how toouse Power BI Desktop.</span></span> <span data-ttu-id="424c6-133">Per assistenza, vedere [Introduzione a Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="424c6-133">If you need some help here, see [Getting started with Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span></span> <span data-ttu-id="424c6-134">Per questo esempio, si userà solo hello [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span><span class="sxs-lookup"><span data-stu-id="424c6-134">For our example, we'll just use hello [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span></span>

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a><span data-ttu-id="424c6-135">Creare un'area di lavoro di Power BI</span><span class="sxs-lookup"><span data-stu-id="424c6-135">Create a Power BI workspace</span></span>

<span data-ttu-id="424c6-136">Ora che hello tutti il completamento del provisioning, iniziamo creazione dell'area di lavoro di un cliente nella raccolta di hello dell'area di lavoro tramite le API REST.</span><span class="sxs-lookup"><span data-stu-id="424c6-136">Now that hello provisioning is all done, let’s get started creating a customer’s workspace in hello workspace collection via REST APIs.</span></span> <span data-ttu-id="424c6-137">Hello seguente HTTP POST richiesta (REST) è creazione hello nuova area di lavoro dell'insieme di area di lavoro esistente.</span><span class="sxs-lookup"><span data-stu-id="424c6-137">hello following HTTP POST Request (REST) is creating hello new workspace in our existing workspace collection.</span></span> <span data-ttu-id="424c6-138">Si tratta di hello [API dell'area di lavoro POST](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="424c6-138">This is hello [POST Workspace API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span> <span data-ttu-id="424c6-139">In questo esempio, nome della raccolta dell'area di lavoro hello è **mypbiapp**.</span><span class="sxs-lookup"><span data-stu-id="424c6-139">In our example, hello workspace collection name is **mypbiapp**.</span></span> <span data-ttu-id="424c6-140">È sufficiente impostare chiave di accesso hello, che viene copiati in precedenza, come **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="424c6-140">We just set hello access key, which we previously copied, as **AppKey**.</span></span> <span data-ttu-id="424c6-141">L'autenticazione è molto semplice.</span><span class="sxs-lookup"><span data-stu-id="424c6-141">It’s very simple authentication!</span></span>

<span data-ttu-id="424c6-142">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="424c6-142">**HTTP Request**</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="424c6-143">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="424c6-143">**HTTP Response**</span></span>

```
HTTP/1.1 201 Created
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces
RequestId: 4220d385-2fb3-406b-8901-4ebe11a5f6da

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/$metadata#workspaces/$entity",
  "workspaceId": "32960a09-6366-4208-a8bb-9e0678cdbb9d",
  "workspaceCollectionName": "mypbiapp"
}
```

<span data-ttu-id="424c6-144">Hello restituito **Idareadilavoro** viene utilizzato per hello dopo le chiamate API successive.</span><span class="sxs-lookup"><span data-stu-id="424c6-144">hello returned **workspaceId** is used for hello following subsequent API calls.</span></span> <span data-ttu-id="424c6-145">L'applicazione deve mantenere questo valore.</span><span class="sxs-lookup"><span data-stu-id="424c6-145">Our application must retain this value.</span></span>

## <a name="import-pbix-file-into-hello-workspace"></a><span data-ttu-id="424c6-146">Importare i file con estensione pbix nell'area di lavoro hello</span><span class="sxs-lookup"><span data-stu-id="424c6-146">Import .pbix file into hello workspace</span></span>

<span data-ttu-id="424c6-147">Ogni report in un'area di lavoro corrisponde tooa singolo file di Power BI Desktop con un set di dati \(incluse le impostazioni di origine dati).</span><span class="sxs-lookup"><span data-stu-id="424c6-147">Each report in a workspace corresponds tooa single Power BI Desktop file with a dataset \(including datasource settings).</span></span> <span data-ttu-id="424c6-148">È possibile importare l'area toohello file pbix come illustrato nel seguente codice hello.</span><span class="sxs-lookup"><span data-stu-id="424c6-148">We can import our .pbix file toohello workspace as shown in hello code below.</span></span> <span data-ttu-id="424c6-149">Come si può notare, è possibile caricare file binario hello del file con estensione pbix usando multipart MIME in http.</span><span class="sxs-lookup"><span data-stu-id="424c6-149">As you can see, we can upload hello binary of .pbix file using MIME multipart in http.</span></span>

<span data-ttu-id="424c6-150">frammento dell'uri Hello **32960a09-6366-4208-a8bb-9e0678cdbb9d** è Idareadilavoro hello e parametro di query **datasetDisplayName** è toocreate nome set di dati di hello.</span><span class="sxs-lookup"><span data-stu-id="424c6-150">hello uri fragment **32960a09-6366-4208-a8bb-9e0678cdbb9d** is hello workspaceId, and query parameter **datasetDisplayName** is hello dataset name toocreate.</span></span> <span data-ttu-id="424c6-151">set di dati creato Hello contiene tutti i dati relativi elementi nel file con estensione pbix, ad esempio i dati importati, hello origine dati toohello di puntatore e così via...</span><span class="sxs-lookup"><span data-stu-id="424c6-151">hello created dataset holds all data related artifacts in .pbix file such as imported data, hello pointer toohello data source, etc..</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{hello content (binary) of .pbix file}
--A300testx--
```

<span data-ttu-id="424c6-152">Questa attività di importazione potrebbe richiedere qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="424c6-152">This import task might run for a while.</span></span> <span data-ttu-id="424c6-153">Al termine, l'applicazione può richiedere lo stato delle attività hello usando un id di importazione. In questo esempio, id di importazione hello è **4eec64dd-533b-47c3-a72c-6508ad854659**.</span><span class="sxs-lookup"><span data-stu-id="424c6-153">When complete, our application can ask hello task status using import id. In our example, hello import id is **4eec64dd-533b-47c3-a72c-6508ad854659**.</span></span>

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

<span data-ttu-id="424c6-154">esempio Hello richiede lo stato utilizzando questo id di importazione:</span><span class="sxs-lookup"><span data-stu-id="424c6-154">hello following is asking status using this import id:</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="424c6-155">Se l'attività hello non è stato completato, hello risposta HTTP potrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="424c6-155">If hello task isn't complete, hello HTTP response could be like this:</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: 614a13a5-4de7-43e8-83c9-9cd225535136

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Publishing",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "name": "mydataset01"
}
```

<span data-ttu-id="424c6-156">Se l'attività hello è stata completata, hello risposta HTTP può essere analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="424c6-156">If hello task is complete, hello HTTP response could be more like this:</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: eb2c5a85-4d7d-4cc2-b0aa-0bafee4b1606

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Succeeded",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "reports": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://app.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c"
    }
  ],
  "datasets": [
    {
      "id": "458e0451-7215-4029-80b3-9627bf3417b0",
      "name": "mydataset01",
      "tables": [
      ],
      "webUrl": "https://app.powerbi.com/datasets/458e0451-7215-4029-80b3-9627bf3417b0"
    }
  ],
  "name": "mydataset01"
}
```

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a><span data-ttu-id="424c6-157">Connettività dell'origine dati \(e multi-tenancy dei dati)</span><span class="sxs-lookup"><span data-stu-id="424c6-157">Data source connectivity \(and multi-tenancy of data)</span></span>

<span data-ttu-id="424c6-158">Quasi tutti gli elementi di hello in file con estensione pbix vengono importati l'area di lavoro, le credenziali di hello per le origini dati non sono.</span><span class="sxs-lookup"><span data-stu-id="424c6-158">While almost all of hello artifacts in .pbix file are imported into our workspace, hello  credentials for data sources are not.</span></span> <span data-ttu-id="424c6-159">Di conseguenza, quando si utilizza **modalità DirectQuery**, hello report incorporato non può essere visualizzato correttamente.</span><span class="sxs-lookup"><span data-stu-id="424c6-159">As a result, when using **DirectQuery mode**, hello embedded report cannot be shown correctly.</span></span> <span data-ttu-id="424c6-160">Ma, quando si usano **la modalità di importazione**, è possibile visualizzare report hello utilizzando i dati importati esistenti hello.</span><span class="sxs-lookup"><span data-stu-id="424c6-160">But, when using **Import mode**, we can view hello report using hello existing imported data.</span></span> <span data-ttu-id="424c6-161">In tal caso, è necessario impostare credenziali hello utilizzando hello tramite chiamate REST come segue.</span><span class="sxs-lookup"><span data-stu-id="424c6-161">In such a case, we must set hello credential using hello following steps via REST calls.</span></span>

<span data-ttu-id="424c6-162">Innanzitutto, è necessario ottenere hello gateway datasource.</span><span class="sxs-lookup"><span data-stu-id="424c6-162">First, we must get hello gateway datasource.</span></span> <span data-ttu-id="424c6-163">Sappiamo hello dataset **id** è hello in precedenza ha restituito un id.</span><span class="sxs-lookup"><span data-stu-id="424c6-163">We know hello dataset **id** is hello previously returned id.</span></span>

<span data-ttu-id="424c6-164">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="424c6-164">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="424c6-165">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="424c6-165">**HTTP Response**</span></span>

```
GET HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: 574b0b18-a6fa-46a6-826c-e65840cf6e15

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#gatewayDatasources",
  "value": [
    {
      "id": "5f7ee2e7-4851-44a1-8b75-3eb01309d0ea",
      "gatewayId": "ca17e77f-1b51-429b-b059-6b3e3e9685d1",
      "datasourceType": "Sql",
      "connectionDetails": "{\"server\":\"testserver.database.windows.net\",\"database\":\"testdb01\"}"
    }
  ]
}
```

<span data-ttu-id="424c6-166">Usando hello restituiti id gateway e l'id origine dati \(vedere hello precedente **gatewayId** e **id** in hello restituito), è possibile modificare le credenziali di hello dell'origine dati, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="424c6-166">Using hello returned gateway id and datasource id \(see hello previous **gatewayId** and **id** in hello returned result), we can change hello credential of this datasource as follows:</span></span>

<span data-ttu-id="424c6-167">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="424c6-167">**HTTP Request**</span></span>

```
PATCH https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/gateways/ca17e77f-1b51-429b-b059-6b3e3e9685d1/datasources/5f7ee2e7-4851-44a1-8b75-3eb01309d0ea
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "credentialType": "Basic",
  "basicCredentials": {
    "username": "demouser",
    "password": "P@ssw0rd"
  }
}
```

<span data-ttu-id="424c6-168">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="424c6-168">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

<span data-ttu-id="424c6-169">Nell'ambiente di produzione, è anche possibile impostare la stringa di connessione diversa hello per ogni area di lavoro tramite l'API REST.</span><span class="sxs-lookup"><span data-stu-id="424c6-169">In production, we can also set hello different connection string for each workspace using REST API.</span></span> <span data-ttu-id="424c6-170">\(ad esempio, è possibile separare hello database per ciascun cliente.)</span><span class="sxs-lookup"><span data-stu-id="424c6-170">\(i.e, we can separate hello database for each customers.)</span></span>

<span data-ttu-id="424c6-171">esempio Hello sta modificando la stringa di connessione hello dell'origine dati tramite REST.</span><span class="sxs-lookup"><span data-stu-id="424c6-171">hello following is changing hello connection string of datasource via REST.</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

<span data-ttu-id="424c6-172">In alternativa, è possibile utilizzare una sicurezza a livello di riga in Power BI Embedded ed è possibile separare i dati di hello per ciascun utente in un unico report.</span><span class="sxs-lookup"><span data-stu-id="424c6-172">Or, we can use Row Level Security in Power BI Embedded and we can separate hello data for each users in one report.</span></span> <span data-ttu-id="424c6-173">Di conseguenza, è possibile eseguire il provisioning di ogni report cliente con lo stesso file con estensione pbix \(interfaccia utente e così via) e origini dati diverse.</span><span class="sxs-lookup"><span data-stu-id="424c6-173">As a result, we can provision each customer report with same .pbix \(UI, etc.) and different data sources.</span></span>

> [!NOTE]
> <span data-ttu-id="424c6-174">Se si utilizza **la modalità di importazione** anziché **modalità DirectQuery**, non vi è Nessun modello toorefresh modo tramite l'API.</span><span class="sxs-lookup"><span data-stu-id="424c6-174">If you’re using **Import mode** instead of **DirectQuery mode**, there’s no way toorefresh models via API.</span></span> <span data-ttu-id="424c6-175">Inoltre, le origini dati locali mediante gateway di Power BI non sono ancora supportate in Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="424c6-175">And, on-premises datasources through Power BI gateway isn't yet supported in Power BI Embedded.</span></span> <span data-ttu-id="424c6-176">Tuttavia, è opportuno effettivamente tookeep sotto controllo hello [blog di Power BI](https://powerbi.microsoft.com/blog/) per le novità e Novità nelle future versioni.</span><span class="sxs-lookup"><span data-stu-id="424c6-176">However, you'll really want tookeep an eye on hello [Power BI blog](https://powerbi.microsoft.com/blog/) for what's new and what's coming in future releases.</span></span>

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a><span data-ttu-id="424c6-177">Autenticazione e hosting (incorporamento) dei report nella pagina Web</span><span class="sxs-lookup"><span data-stu-id="424c6-177">Authentication and hosting (embedding) reports in our web page</span></span>

<span data-ttu-id="424c6-178">In hello precedente API REST, è possibile usare la chiave di accesso hello **AppKey** stesso come intestazione di autorizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="424c6-178">In hello previous REST API, we can use hello access key **AppKey** itself as hello authorization header.</span></span> <span data-ttu-id="424c6-179">Poiché queste chiamate possono essere gestite sul lato server back-end di hello, è sicuro.</span><span class="sxs-lookup"><span data-stu-id="424c6-179">Because these calls can be handled on hello backend server side, it's safe.</span></span>

<span data-ttu-id="424c6-180">Ma, quando si incorporano report hello nella nostra pagina web, verrebbe gestito di questo tipo di informazioni di sicurezza utilizzando JavaScript \(front-end).</span><span class="sxs-lookup"><span data-stu-id="424c6-180">But, when we embed hello report in our web page, this kind of security information would be handled using JavaScript \(frontend).</span></span> <span data-ttu-id="424c6-181">Valore dell'intestazione di autorizzazione hello deve quindi essere protetto.</span><span class="sxs-lookup"><span data-stu-id="424c6-181">Then hello authorization header value must be secured.</span></span> <span data-ttu-id="424c6-182">Se un utente malintenzionato o un codice dannoso individua la chiave di accesso, la può usare per chiamare qualsiasi operazione.</span><span class="sxs-lookup"><span data-stu-id="424c6-182">If our access key is discovered by a malicious user or malicious code, they can call any operations using this key.</span></span>

<span data-ttu-id="424c6-183">Quando si incorporano report hello nella nostra pagina web, è necessario utilizzare token calcolata hello anziché chiave di accesso **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="424c6-183">When we embed hello report in our web page, we must use hello computed token instead of access key **AppKey**.</span></span> <span data-ttu-id="424c6-184">L'applicazione deve creare Token Web Json OAuth hello \(JWT) che include le attestazioni hello e firma digitale calcolata hello.</span><span class="sxs-lookup"><span data-stu-id="424c6-184">Our application must create hello OAuth Json Web Token \(JWT) which consists of hello claims and hello computed digital signature.</span></span> <span data-ttu-id="424c6-185">Come illustrato di seguito, questo token JTW OAuth è il token di stringa con codifica delimitato da punti.</span><span class="sxs-lookup"><span data-stu-id="424c6-185">As illustrated below, this OAuth JWT is dot-delimited encoded string tokens.</span></span>

![](media/power-bi-embedded-iframe/oauth-jwt.png)

<span data-ttu-id="424c6-186">In primo luogo, è necessario preparare hello valore di input, che viene firmato in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="424c6-186">First, we must prepare hello input value, which is signed later.</span></span> <span data-ttu-id="424c6-187">Questo valore è hello base64 codificati nell'url (rfc4648) stringa hello seguente json e queste sono delimitate da punto hello \(.) caratteri.</span><span class="sxs-lookup"><span data-stu-id="424c6-187">This value is hello base64 url encoded (rfc4648) string of hello following json, and these are delimited by hello dot \(.) character.</span></span> <span data-ttu-id="424c6-188">Successivamente, verrà illustrato come tooget hello id del report.</span><span class="sxs-lookup"><span data-stu-id="424c6-188">Later, we'll explain how tooget hello report id.</span></span>

> [!NOTE]
> <span data-ttu-id="424c6-189">Se si desidera toouse a livello di sicurezza di riga con Power BI incorporato, è necessario specificare anche **username** e **ruoli** nelle attestazioni hello.</span><span class="sxs-lookup"><span data-stu-id="424c6-189">If we want toouse Row Level Security (RLS) with Power BI Embedded, we must also specify **username** and **roles** in hello claims.</span></span>

```
{
  "typ":"JWT",
  "alg":"HS256"
}
```

```
{
  "wid":"{workspace id}",
  "rid":"{report id}",
  "wcn":"{workspace collection name}",
  "iss":"PowerBISDK",
  "ver":"0.2.0",
  "aud":"https://analysis.windows.net/powerbi/api",
  "nbf":{start time of token expiration},
  "exp":{end time of token expiration}
}
```

<span data-ttu-id="424c6-190">Successivamente, è necessario creare stringa con codificata base64 hello del codice HMAC \(firma hello) con l'algoritmo SHA256.</span><span class="sxs-lookup"><span data-stu-id="424c6-190">Next, we must create hello base64 encoded string of HMAC \(hello signature) with SHA256 algorithm.</span></span> <span data-ttu-id="424c6-191">Questo valore di input con segno è stringa precedente hello.</span><span class="sxs-lookup"><span data-stu-id="424c6-191">This signed input value is hello previous string.</span></span>

<span data-ttu-id="424c6-192">Ultimo, sarà necessario combinare valore di input hello e stringa di firma utilizzando periodo \(.) caratteri.</span><span class="sxs-lookup"><span data-stu-id="424c6-192">Last, we must combine hello input value and signature string using period \(.) character.</span></span> <span data-ttu-id="424c6-193">la stringa Hello completata è token app hello per hello incorporamento di report.</span><span class="sxs-lookup"><span data-stu-id="424c6-193">hello completed string is hello app token for hello report embedding.</span></span> <span data-ttu-id="424c6-194">Anche se il token di app hello viene individuato da un utente malintenzionato, è Impossibile ottenere chiave di accesso originale hello.</span><span class="sxs-lookup"><span data-stu-id="424c6-194">Even if hello app token is discovered by a malicious user, they cannot get hello original access key.</span></span> <span data-ttu-id="424c6-195">Questo token dell'applicazione scadrà rapidamente.</span><span class="sxs-lookup"><span data-stu-id="424c6-195">This app token will expire quickly.</span></span>

<span data-ttu-id="424c6-196">Ecco un esempio di codice PHP per questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="424c6-196">Here's a PHP example for these steps:</span></span>

```
<?php
// 1. power bi access key
$accesskey = "MpaUgrTv5e...";

// 2. construct input value
$token1 = "{" .
  "\"typ\":\"JWT\"," .
  "\"alg\":\"HS256\"" .
  "}";
$token2 = "{" .
  "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
  "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
  "\"wcn\":\"mypbiapp\"," . // workspace collection name
  "\"iss\":\"PowerBISDK\"," .
  "\"ver\":\"0.2.0\"," .
  "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
  "\"nbf\":" . date("U") . "," .
  "\"exp\":" . date("U" , strtotime("+1 hour")) .
  "}";
$inputval = rfc4648_base64_encode($token1) .
  "." .
  rfc4648_base64_encode($token2);

// 3. get encoded signature
$hash = hash_hmac("sha256",
    $inputval,
    $accesskey,
    true);
$sig = rfc4648_base64_encode($hash);

// 4. show result (which is hello apptoken)
$apptoken = $inputval . "." . $sig;
echo($apptoken);

// helper functions
function rfc4648_base64_encode($arg) {
  $res = $arg;
  $res = base64_encode($res);
  $res = str_replace("/", "_", $res);
  $res = str_replace("+", "-", $res);
  $res = rtrim($res, "=");
  return $res;
}
?>
```

## <a name="finally-embed-hello-report-into-hello-web-page"></a><span data-ttu-id="424c6-197">Infine, incorporare report hello pagina web hello</span><span class="sxs-lookup"><span data-stu-id="424c6-197">Finally, embed hello report into hello web page</span></span>

<span data-ttu-id="424c6-198">Per incorporare il report, è necessario ottenere hello incorporare url e report **id** utilizzando hello seguenti API REST.</span><span class="sxs-lookup"><span data-stu-id="424c6-198">For embedding our report, we must get hello embed url and report **id** using hello following REST API.</span></span>

<span data-ttu-id="424c6-199">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="424c6-199">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="424c6-200">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="424c6-200">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: d4099022-405b-49d3-b3b7-3c60cf675958

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#reports",
  "value": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c",
      "isFromPbix": false
    }
  ]
}
```

<span data-ttu-id="424c6-201">È possibile incorporare report hello nella nostra app web con token app precedente hello.</span><span class="sxs-lookup"><span data-stu-id="424c6-201">We can embed hello report in our web app using hello previous app token.</span></span>
<span data-ttu-id="424c6-202">Se si esamina il codice di esempio successivo hello, parte precedente hello è hello stesso esempio hello precedente.</span><span class="sxs-lookup"><span data-stu-id="424c6-202">If we look at hello next sample code, hello former part is hello same as hello previous example.</span></span> <span data-ttu-id="424c6-203">Nella parte di quest'ultimo hello, in questo esempio viene hello **embedUrl** \(vedere risultato precedente hello) in hello iframe, quindi esegue l'invio token app hello in iframe hello.</span><span class="sxs-lookup"><span data-stu-id="424c6-203">In hello latter part, this sample shows hello **embedUrl** \(see hello previous result) in hello iframe, and is posting hello app token into hello iframe.</span></span>

> [!NOTE]
> <span data-ttu-id="424c6-204">È necessario toochange hello report id valore tooone personalizzati.</span><span class="sxs-lookup"><span data-stu-id="424c6-204">You'll need toochange hello report id value tooone of your own.</span></span> <span data-ttu-id="424c6-205">Inoltre, a causa di bug tooa nel nostro sistema di gestione dei contenuti, hello iframe nell'esempio di codice hello lettura tag letteralmente.</span><span class="sxs-lookup"><span data-stu-id="424c6-205">Also, due tooa bug in our content management system, hello iframe tag in hello code sample is read literally.</span></span> <span data-ttu-id="424c6-206">Rimuovere testo hello delimitata da tag hello se si copia e incolla questo codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="424c6-206">Remove hello capped text from hello tag if you copy and paste this sample code.</span></span>

```
    <?php
    // 1. power bi access key
    $accesskey = "MpaUgrTv5e...";

    // 2. construct input value
    $token1 = "{" .
      "\"typ\":\"JWT\"," .
      "\"alg\":\"HS256\"" .
      "}";
    $token2 = "{" .
      "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
      "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
      "\"wcn\":\"mypbiapp\"," . // workspace collection name
      "\"iss\":\"PowerBISDK\"," .
      "\"ver\":\"0.2.0\"," .
      "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
      "\"nbf\":" . date("U") . "," .
      "\"exp\":" . date("U" , strtotime("+1 hour")) .
      "}";
    $inputval = rfc4648_base64_encode($token1) .
      "." .
      rfc4648_base64_encode($token2);

    // 3. get encoded signature value
    $hash = hash_hmac("sha256",
        $inputval,
        $accesskey,
        true);
    $sig = rfc4648_base64_encode($hash);

    // 4. get apptoken
    $apptoken = $inputval . "." . $sig;

    // helper functions
    function rfc4648_base64_encode($arg) {
      $res = $arg;
      $res = base64_encode($res);
      $res = str_replace("/", "_", $res);
      $res = str_replace("+", "-", $res);
      $res = rtrim($res, "=");
      return $res;
    }
    ?>
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Test page</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
      <button id="btnView">View Report !</button>
      <div id="divView">
        <**REMOVE THIS CAPPED TEXT IF COPIED** iframe id="ifrTile" width="100%" height="400"></iframe>
      </div>
      <script>
        (function () {
          document.getElementById('btnView').onclick = function() {
            var iframe = document.getElementById('ifrTile');
            iframe.src = 'https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c';
            iframe.onload = function() {
              var msgJson = {
                action: "loadReport",
                accessToken: "<?=$apptoken?>",
                height: 500,
                width: 722
              };
              var msgTxt = JSON.stringify(msgJson);
              iframe.contentWindow.postMessage(msgTxt, "*");
            };
          };
        }());
      </script>
    </body>
```

<span data-ttu-id="424c6-207">Ed ecco il risultato:</span><span class="sxs-lookup"><span data-stu-id="424c6-207">And here's our result:</span></span>

![](media/power-bi-embedded-iframe/view-report.png)

<span data-ttu-id="424c6-208">In questo momento, Power BI Embedded vengono visualizzati solo report hello in iframe hello.</span><span class="sxs-lookup"><span data-stu-id="424c6-208">At this time, Power BI Embedded only shows hello report in hello iframe.</span></span> <span data-ttu-id="424c6-209">Tuttavia, è consigliabile monitorare hello [Blog di Power BI](https://powerbi.microsoft.com/blog/).</span><span class="sxs-lookup"><span data-stu-id="424c6-209">But, keep an eye on hello [Power BI Blog](https://powerbi.microsoft.com/blog/).</span></span> <span data-ttu-id="424c6-210">Miglioramenti futuri utilizzi lato client nuova API che verranno possiamo inviare informazioni in iframe hello, nonché ottenere informazioni. Ci sono tanti aspetti interessanti.</span><span class="sxs-lookup"><span data-stu-id="424c6-210">Future improvements could use new client side APIs that will let us send information into hello iframe as well as get information out. Exciting stuff!</span></span>

## <a name="see-also"></a><span data-ttu-id="424c6-211">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="424c6-211">See also</span></span>
* [<span data-ttu-id="424c6-212">Autenticazione e autorizzazione con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="424c6-212">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)

<span data-ttu-id="424c6-213">Altre domande?</span><span class="sxs-lookup"><span data-stu-id="424c6-213">More questions?</span></span> [<span data-ttu-id="424c6-214">Provare a hello Community di Power BI</span><span class="sxs-lookup"><span data-stu-id="424c6-214">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

