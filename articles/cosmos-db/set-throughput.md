---
title: "velocità effettiva aaaProvision per Azure Cosmos DB | Documenti Microsoft"
description: "Informazioni su come tooset il provisioning di velocità effettiva per containsers, raccolte, grafici e tabelle di Azure Cosmos DB."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f98def7f-f012-4592-be03-f6fa185e1b1e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: mimig
ms.openlocfilehash: c143f4aace466b7109168a50e2eb80ddeca6400e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a><span data-ttu-id="9e3f2-103">Impostare la velocità effettiva per i contenitori di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9e3f2-103">Set throughput for Azure Cosmos DB containers</span></span>

<span data-ttu-id="9e3f2-104">È possibile impostare la velocità effettiva per i contenitori di DB Cosmos Azure nel portale di Azure hello o utilizzando hello client SDK.</span><span class="sxs-lookup"><span data-stu-id="9e3f2-104">You can set throughput for your Azure Cosmos DB containers in hello Azure portal or by using hello client SDKs.</span></span> 

<span data-ttu-id="9e3f2-105">Hello nella tabella seguente sono elencate disponibili per i contenitori di velocità effettiva di hello:</span><span class="sxs-lookup"><span data-stu-id="9e3f2-105">hello following table lists hello throughput available for containers:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="9e3f2-106"><strong>Contenitore a partizione singola</strong></span><span class="sxs-lookup"><span data-stu-id="9e3f2-106"><strong>Single Partition Container</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9e3f2-107"><strong>Contenitore partizionato</strong></span><span class="sxs-lookup"><span data-stu-id="9e3f2-107"><strong>Partitioned Container</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="9e3f2-108">Velocità effettiva minima</span><span class="sxs-lookup"><span data-stu-id="9e3f2-108">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9e3f2-109">400 unità richiesta al secondo</span><span class="sxs-lookup"><span data-stu-id="9e3f2-109">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9e3f2-110">2.500 unità richiesta al secondo</span><span class="sxs-lookup"><span data-stu-id="9e3f2-110">2,500 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="9e3f2-111">Velocità effettiva massima</span><span class="sxs-lookup"><span data-stu-id="9e3f2-111">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9e3f2-112">10.000 unità richiesta al secondo</span><span class="sxs-lookup"><span data-stu-id="9e3f2-112">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9e3f2-113">Senza limiti</span><span class="sxs-lookup"><span data-stu-id="9e3f2-113">Unlimited</span></span></p></td>
        </tr>
    </tbody>
</table>

## <a name="tooset-hello-throughput-by-using-hello-azure-portal"></a><span data-ttu-id="9e3f2-114">velocità effettiva di hello tooset utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9e3f2-114">tooset hello throughput by using hello Azure portal</span></span>

1. <span data-ttu-id="9e3f2-115">In una nuova finestra, aprire hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9e3f2-115">In a new window, open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9e3f2-116">Nella barra sinistra hello, fare clic su **Azure Cosmos DB**, oppure fare clic su **più servizi** nella parte inferiore di hello, quindi scorrere troppo**database**, quindi fare clic su **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="9e3f2-116">On hello left bar, click **Azure Cosmos DB**, or click **More Services** at hello bottom, then scroll too**Databases**, and then click **Azure Cosmos DB**.</span></span>
3. <span data-ttu-id="9e3f2-117">Selezionare l'account Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9e3f2-117">Select your Cosmos DB account.</span></span>
4. <span data-ttu-id="9e3f2-118">In nuova finestra hello, fare clic su **Esplora dati (anteprima)** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="9e3f2-118">In hello new window, click **Data Explorer (Preview)** in hello navigation menu.</span></span>
5. <span data-ttu-id="9e3f2-119">In nuova finestra hello, espandere il database e il contenitore e quindi fare clic su **scala & impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="9e3f2-119">In hello new window, expand your database and container and then click **Scale & Settings**.</span></span>
6. <span data-ttu-id="9e3f2-120">Nella finestra Nuovo hello digitare hello nuovo valore di velocità effettiva in hello **velocità effettiva** casella e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="9e3f2-120">In hello new window, type hello new throughput value in hello **Throughput** box, and then click **Save**.</span></span>

<a id="set-throughput-sdk"></a>

## <a name="tooset-hello-throughput-by-using-hello-documentdb-api-for-net"></a><span data-ttu-id="9e3f2-121">velocità effettiva di hello tooset utilizzando hello API DocumentDB per .NET</span><span class="sxs-lookup"><span data-stu-id="9e3f2-121">tooset hello throughput by using hello DocumentDB API for .NET</span></span>

```C#
//Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput toohello new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a><span data-ttu-id="9e3f2-122">Domande frequenti sulla velocità effettiva</span><span class="sxs-lookup"><span data-stu-id="9e3f2-122">Throughput FAQ</span></span>

<span data-ttu-id="9e3f2-123">**È possibile impostare tooless la velocità effettiva di 400 UR/sec?**</span><span class="sxs-lookup"><span data-stu-id="9e3f2-123">**Can I set my throughput tooless than 400 RU/s?**</span></span>

<span data-ttu-id="9e3f2-124">400 UR/sec è la velocità effettiva minima a hello disponibile su raccolte con partizione singola DB Cosmos (2500 UR/sec è minimo per le raccolte partizionate hello).</span><span class="sxs-lookup"><span data-stu-id="9e3f2-124">400 RU/s is hello minimum throughput available on Cosmos DB single partition collections (2500 RU/s is hello minimum for partitioned collections).</span></span> <span data-ttu-id="9e3f2-125">Richiesta di unità vengono impostate in intervalli di 100 UR/sec, ma la velocità effettiva non può essere impostata too100 UR/sec o qualsiasi valore minore di 400 UR/sec.</span><span class="sxs-lookup"><span data-stu-id="9e3f2-125">Request units are set in 100 RU/s intervals, but throughput cannot be set too100 RU/s or any value smaller than 400 RU/s.</span></span> <span data-ttu-id="9e3f2-126">Se si sta cercando di toodevelop un metodo conveniente e test Cosmos DB, è possibile utilizzare hello libero [Azure Cosmos DB emulatore](local-emulator.md), che è possibile distribuire senza alcun costo.</span><span class="sxs-lookup"><span data-stu-id="9e3f2-126">If you're looking for a cost effective method toodevelop and test Cosmos DB, you can use hello free [Azure Cosmos DB Emulator](local-emulator.md), which you can deploy locally at no cost.</span></span> 

<span data-ttu-id="9e3f2-127">**Impostazione througput utilizzando hello MongoDB API**</span><span class="sxs-lookup"><span data-stu-id="9e3f2-127">**How do I set througput using hello MongoDB API?**</span></span>

<span data-ttu-id="9e3f2-128">Non sussiste alcun della velocità effettiva di MongoDB API estensione tooset.</span><span class="sxs-lookup"><span data-stu-id="9e3f2-128">There's no MongoDB API extension tooset throughput.</span></span> <span data-ttu-id="9e3f2-129">Hello si consiglia di hello toouse API DocumentDB, come illustrato nella [tooset velocità effettiva di hello utilizzando hello API DocumentDB per .NET](#set-throughput-sdk).</span><span class="sxs-lookup"><span data-stu-id="9e3f2-129">hello recommendation is toouse hello DocumentDB API, as shown in [tooset hello throughput by using hello DocumentDB API for .NET](#set-throughput-sdk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e3f2-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9e3f2-130">Next steps</span></span>

<span data-ttu-id="9e3f2-131">toolearn ulteriori informazioni su provisioning e scalabilità pianeta corso con Cosmos DB, vedere [partizionamento e scalabilità con DB Cosmos](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="9e3f2-131">toolearn more about provisioning and going planet-scale with Cosmos DB, see [Partitioning and scaling with Cosmos DB](partition-data.md).</span></span>
