---
title: "Effettuare il provisioning della velocità effettiva per Azure Cosmos DB | Microsoft Docs"
description: "Informazioni su come configurare la velocità effettiva di provisioning per i container, le raccolte, i grafici e le tabelle di Azure Cosmos DB."
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
ms.openlocfilehash: d541bb19ba7e5ecb44c9fe91b1e232d4d9c2170e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a><span data-ttu-id="85714-103">Impostare la velocità effettiva per i contenitori di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="85714-103">Set throughput for Azure Cosmos DB containers</span></span>

<span data-ttu-id="85714-104">È possibile impostare la velocità effettiva per i contenitori di Azure Cosmos DB nel portale di Azure oppure usando gli SDK client.</span><span class="sxs-lookup"><span data-stu-id="85714-104">You can set throughput for your Azure Cosmos DB containers in the Azure portal or by using the client SDKs.</span></span> 

<span data-ttu-id="85714-105">La tabella seguente elenca la velocità effettiva disponibile per i contenitori:</span><span class="sxs-lookup"><span data-stu-id="85714-105">The following table lists the throughput available for containers:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="85714-106"><strong>Contenitore a partizione singola</strong></span><span class="sxs-lookup"><span data-stu-id="85714-106"><strong>Single Partition Container</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85714-107"><strong>Contenitore partizionato</strong></span><span class="sxs-lookup"><span data-stu-id="85714-107"><strong>Partitioned Container</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="85714-108">Velocità effettiva minima</span><span class="sxs-lookup"><span data-stu-id="85714-108">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85714-109">400 unità richiesta al secondo</span><span class="sxs-lookup"><span data-stu-id="85714-109">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85714-110">2.500 unità richiesta al secondo</span><span class="sxs-lookup"><span data-stu-id="85714-110">2,500 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="85714-111">Velocità effettiva massima</span><span class="sxs-lookup"><span data-stu-id="85714-111">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85714-112">10.000 unità richiesta al secondo</span><span class="sxs-lookup"><span data-stu-id="85714-112">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85714-113">Senza limiti</span><span class="sxs-lookup"><span data-stu-id="85714-113">Unlimited</span></span></p></td>
        </tr>
    </tbody>
</table>

## <a name="to-set-the-throughput-by-using-the-azure-portal"></a><span data-ttu-id="85714-114">Per impostare la velocità effettiva tramite il Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="85714-114">To set the throughput by using the Azure portal</span></span>

1. <span data-ttu-id="85714-115">In una nuova finestra accedere al [Portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="85714-115">In a new window, open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="85714-116">Fare clic su **Azure Cosmos DB** nella barra a sinistra oppure fare clic su **Altri servizi** nella parte inferiore, scorrere fino a **Database**, quindi fare clic su **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="85714-116">On the left bar, click **Azure Cosmos DB**, or click **More Services** at the bottom, then scroll to **Databases**, and then click **Azure Cosmos DB**.</span></span>
3. <span data-ttu-id="85714-117">Selezionare l'account Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="85714-117">Select your Cosmos DB account.</span></span>
4. <span data-ttu-id="85714-118">Nella nuova finestra fare clic su **Esplora dati (anteprima)** dal menu di spostamento.</span><span class="sxs-lookup"><span data-stu-id="85714-118">In the new window, click **Data Explorer (Preview)** in the navigation menu.</span></span>
5. <span data-ttu-id="85714-119">Nella nuova finestra espandere il database e il contenitore e quindi fare clic su **Scale & Settings** (Scalabilità e impostazioni).</span><span class="sxs-lookup"><span data-stu-id="85714-119">In the new window, expand your database and container and then click **Scale & Settings**.</span></span>
6. <span data-ttu-id="85714-120">Nella nuova finestra digitare il nuovo valore per la velocità effettiva nella casella **Velocità effettiva** e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="85714-120">In the new window, type the new throughput value in the **Throughput** box, and then click **Save**.</span></span>

<a id="set-throughput-sdk"></a>

## <a name="to-set-the-throughput-by-using-the-documentdb-api-for-net"></a><span data-ttu-id="85714-121">Per configurare la velocità effettiva usando l'API DocumentDB per .NET</span><span class="sxs-lookup"><span data-stu-id="85714-121">To set the throughput by using the DocumentDB API for .NET</span></span>

```C#
//Fetch the resource to be updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set the throughput to the new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a><span data-ttu-id="85714-122">Domande frequenti sulla velocità effettiva</span><span class="sxs-lookup"><span data-stu-id="85714-122">Throughput FAQ</span></span>

<span data-ttu-id="85714-123">**È possibile impostare la velocità effettiva a meno di 400 UR/sec?**</span><span class="sxs-lookup"><span data-stu-id="85714-123">**Can I set my throughput to less than 400 RU/s?**</span></span>

<span data-ttu-id="85714-124">Il valore di 400 UR/sec è la velocità effettiva minima disponibile nelle raccolte di partizioni singole di Cosmos DB. 2500 UR/sec è il valore minimo per le raccolte partizionate.</span><span class="sxs-lookup"><span data-stu-id="85714-124">400 RU/s is the minimum throughput available on Cosmos DB single partition collections (2500 RU/s is the minimum for partitioned collections).</span></span> <span data-ttu-id="85714-125">Le unità richieste sono impostate in intervalli di 100 UR/sec, ma la velocità effettiva non può essere impostata su 100 UR/sec o su qualsiasi valore inferiore a 400 UR/sec.</span><span class="sxs-lookup"><span data-stu-id="85714-125">Request units are set in 100 RU/s intervals, but throughput cannot be set to 100 RU/s or any value smaller than 400 RU/s.</span></span> <span data-ttu-id="85714-126">Se si cerca un metodo conveniente per sviluppare e testare Cosmos DB, è possibile usare la versione gratuita dell'[emulatore di Azure Cosmos DB](local-emulator.md), distribuibile in locale senza alcun costo aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="85714-126">If you're looking for a cost effective method to develop and test Cosmos DB, you can use the free [Azure Cosmos DB Emulator](local-emulator.md), which you can deploy locally at no cost.</span></span> 

<span data-ttu-id="85714-127">**Come configurare la velocità effettiva tramite l'API MongoDB**</span><span class="sxs-lookup"><span data-stu-id="85714-127">**How do I set througput using the MongoDB API?**</span></span>

<span data-ttu-id="85714-128">Non è disponibile alcuna estensione dell'API MongoDB per la configurazione della velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="85714-128">There's no MongoDB API extension to set throughput.</span></span> <span data-ttu-id="85714-129">È consigliabile usare l'API DocumentDB, come mostrato in [Per configurare la velocità effettiva usando l'API DocumentDB per .NET](#set-throughput-sdk).</span><span class="sxs-lookup"><span data-stu-id="85714-129">The recommendation is to use the DocumentDB API, as shown in [To set the throughput by using the DocumentDB API for .NET](#set-throughput-sdk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="85714-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="85714-130">Next steps</span></span>

<span data-ttu-id="85714-131">Per altre informazioni sul provisioning e sulla diffusione su scala globale di Cosmos DB, vedere [Partizionamento e scalabilità con Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="85714-131">To learn more about provisioning and going planet-scale with Cosmos DB, see [Partitioning and scaling with Cosmos DB](partition-data.md).</span></span>
