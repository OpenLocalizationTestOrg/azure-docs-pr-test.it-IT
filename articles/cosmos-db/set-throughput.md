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
# <a name="set-throughput-for-azure-cosmos-db-containers"></a>Impostare la velocità effettiva per i contenitori di Azure Cosmos DB

È possibile impostare la velocità effettiva per i contenitori di DB Cosmos Azure nel portale di Azure hello o utilizzando hello client SDK. 

Hello nella tabella seguente sono elencate disponibili per i contenitori di velocità effettiva di hello:

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><strong>Contenitore a partizione singola</strong></p></td>
            <td valign="top"><p><strong>Contenitore partizionato</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>Velocità effettiva minima</p></td>
            <td valign="top"><p>400 unità richiesta al secondo</p></td>
            <td valign="top"><p>2.500 unità richiesta al secondo</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Velocità effettiva massima</p></td>
            <td valign="top"><p>10.000 unità richiesta al secondo</p></td>
            <td valign="top"><p>Senza limiti</p></td>
        </tr>
    </tbody>
</table>

## <a name="tooset-hello-throughput-by-using-hello-azure-portal"></a>velocità effettiva di hello tooset utilizzando hello portale di Azure

1. In una nuova finestra, aprire hello [portale di Azure](https://portal.azure.com).
2. Nella barra sinistra hello, fare clic su **Azure Cosmos DB**, oppure fare clic su **più servizi** nella parte inferiore di hello, quindi scorrere troppo**database**, quindi fare clic su **Azure Cosmos DB**.
3. Selezionare l'account Cosmos DB.
4. In nuova finestra hello, fare clic su **Esplora dati (anteprima)** nel menu di navigazione hello.
5. In nuova finestra hello, espandere il database e il contenitore e quindi fare clic su **scala & impostazioni**.
6. Nella finestra Nuovo hello digitare hello nuovo valore di velocità effettiva in hello **velocità effettiva** casella e quindi fare clic su **salvare**.

<a id="set-throughput-sdk"></a>

## <a name="tooset-hello-throughput-by-using-hello-documentdb-api-for-net"></a>velocità effettiva di hello tooset utilizzando hello API DocumentDB per .NET

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

## <a name="throughput-faq"></a>Domande frequenti sulla velocità effettiva

**È possibile impostare tooless la velocità effettiva di 400 UR/sec?**

400 UR/sec è la velocità effettiva minima a hello disponibile su raccolte con partizione singola DB Cosmos (2500 UR/sec è minimo per le raccolte partizionate hello). Richiesta di unità vengono impostate in intervalli di 100 UR/sec, ma la velocità effettiva non può essere impostata too100 UR/sec o qualsiasi valore minore di 400 UR/sec. Se si sta cercando di toodevelop un metodo conveniente e test Cosmos DB, è possibile utilizzare hello libero [Azure Cosmos DB emulatore](local-emulator.md), che è possibile distribuire senza alcun costo. 

**Impostazione througput utilizzando hello MongoDB API**

Non sussiste alcun della velocità effettiva di MongoDB API estensione tooset. Hello si consiglia di hello toouse API DocumentDB, come illustrato nella [tooset velocità effettiva di hello utilizzando hello API DocumentDB per .NET](#set-throughput-sdk).

## <a name="next-steps"></a>Passaggi successivi

toolearn ulteriori informazioni su provisioning e scalabilità pianeta corso con Cosmos DB, vedere [partizionamento e scalabilità con DB Cosmos](partition-data.md).
