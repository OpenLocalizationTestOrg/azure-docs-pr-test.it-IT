---
title: livelli di prestazioni aaaDocumentDB API | Documenti Microsoft
description: "Informazioni su come livelli di prestazioni di DocumentDB API consentono di velocità effettiva tooreserve in base al contenitore."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 7dc21c71-47e2-4e06-aa21-e84af52866f4
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 716bc11ae238dbb0feebf004ed8d5f8a7515ec6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="retiring-hello-s1-s2-and-s3-performance-levels"></a>Ritiro di livelli di prestazioni S1, S2 e S3 hello

> [!IMPORTANT] 
> Hello S1, S2 e S3 livelli di prestazioni descritti in questo articolo verranno ritirati e non sono più disponibili per i nuovi account API DocumentDB.
>

In questo articolo viene fornita una panoramica dei livelli di prestazioni S1, S2 e S3 e viene illustrato come le raccolte di hello che usano questi livelli di prestazioni saranno le raccolte con partizione toosingle migrati sul 1 ° agosto 2017. Dopo aver letto questo articolo, sarà in grado di tooanswer hello seguenti domande:

- [Perché sono le prestazioni di S1, S2 e S3 hello livelli ritirati?](#why-retired)
- [Come raccolte con partizione singola e le raccolte partizionate confrontare toohello S1, S2, livelli di prestazioni S3?](#compare)
- [Cosa è necessario tooensure toodo ininterrotta accedere ai dati toomy?](#uninterrupted-access)
- [Come cambierà la raccolta dopo la migrazione di hello?](#collection-change)
- [Come la fatturazione cambieranno dopo che sono le raccolte con partizione toosingle migrati?](#billing-change)
- [Come bisogna comportarsi se sono necessari più di 10 GB di spazio di archiviazione?](#more-storage-needed)
- [È possibile modificare tra livelli di prestazioni di S1, S2 e S3 hello prima 1 agosto 2017?](#change-before)
- [Come è possibile sapere quando sarà stata eseguita la migrazione di una raccolta?](#when-migrated)
- [Come la migrazione da hello S1, S2, S3 prestazioni livelli toosingle le raccolte con partizione in modo personalizzato?](#migrate-diy)
- [Quali sono le conseguenze per i clienti EA?](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-hello-s1-s2-and-s3-performance-levels-being-retired"></a>Perché sono le prestazioni di S1, S2 e S3 hello livelli ritirati?

livelli di prestazioni S1, S2 e S3 Hello non non offrono hello una flessibilità che offre le raccolte di API DocumentDB. Con hello S1, S2, livelli di prestazioni S3 entrambi hello velocità effettiva e capacità di archiviazione sono state già impostate e non ha inviato l'elasticità. DB Cosmos Azure offre ora hello possibilità toocustomize la velocità effettiva e l'archiviazione, offrendo maggiore flessibilità in tooscale il possibilità in base alle esigenze.

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-toohello-s1-s2-s3-performance-levels"></a>Come raccolte con partizione singola e le raccolte partizionate confrontare toohello S1, S2, livelli di prestazioni S3?

Hello nella tabella seguente confronta hello velocità effettiva e l'archiviazione opzioni disponibili nelle raccolte con partizione singola, le raccolte partizionate e S1, S2, livelli di prestazioni S3. Di seguito è riportato un esempio per l'area Stati Uniti orientali 2:

|   |Raccolta partizionata|Raccolta a partizione singola|S1|S2|S3|
|---|---|---|---|---|---|
|Velocità effettiva massima|Illimitato|10.000 UR/sec|250 UR/sec|1000 UR/sec|2500 UR/sec|
|Velocità effettiva minima|2500 UR/sec|400 UR/sec|250 UR/sec|1000 UR/sec|2500 UR/sec|
|Spazio di archiviazione massimo|Illimitato|10 GB|10 GB|10 GB|10 GB|
|Prezzo (ogni mese)|Velocità effettiva: $ 6/100 UR/sec<br><br>Spazio di archiviazione: $ 0,25/GB|Velocità effettiva: $ 6/100 UR/sec<br><br>Spazio di archiviazione: $ 0,25/GB|$ 25 USD|$ 50 USD|$ 100 USD|

Per i clienti EA, è consigliabile fare riferimento a [Quali sono le conseguenze per i clienti EA?](#ea-customer)

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-toodo-tooensure-uninterrupted-access-toomy-data"></a>Cosa è necessario tooensure toodo ininterrotta accedere ai dati toomy?

Nothing, Cosmos DB gestisce migrazione hello automaticamente. Se si dispone di una raccolta S1, S2 o S3, la raccolta corrente sarà migrato tooa singola partizione raccolta 31 luglio 2017. 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-hello-migration"></a>Come cambierà la raccolta dopo la migrazione di hello?

Se si dispone di una raccolta di S1, sarà migrato tooa singola partizione insieme con velocità effettiva di 400 UR/sec. 400 UR/sec è la velocità effettiva più bassa a hello disponibile con le raccolte con partizione singola. Tuttavia, il costo di hello di 400 UR/sec in una raccolta di singola partizione è di circa hello come se sono stati paga con la raccolta di S1 hello e 250 UR/sec: in modo non di pagamento per hello extra 150 tooyou disponibili di UR/sec.

Se si dispone di una raccolta di S2, sarà migrato tooa singola partizione insieme con 1 K UR/sec. Non verrà visualizzato alcun livello di velocità effettiva tooyour di modifica.

Se si dispone di una raccolta di S3, sarà migrato tooa singola partizione insieme con 2.5 K UR/sec. Non verrà visualizzato alcun livello di velocità effettiva tooyour di modifica.

In ognuno di questi casi, dopo la migrazione, la raccolta di è che saranno in grado di toocustomize il livello di velocità effettiva o applicarvi la scalabilità verticale come utenti tooyour di bassa latenza accesso tooprovide necessari. livello di velocità effettiva hello toochange dopo la raccolta ha eseguito la migrazione, aprire semplicemente l'account DB Cosmos in hello portale di Azure, fare clic su scala, scegliere la raccolta e quindi modificare il livello di velocità effettiva di hello, come illustrato nella seguente schermata hello:

![La velocità effettiva tooscale in hello portale di Azure](./media/performance-levels/portal-scale-throughput.png)

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-im-migrated-toohello-single-partition-collections"></a>Come la fatturazione cambieranno dopo che sono raccolte con partizione singola toohello migrati?

Presupponendo che si hanno 10 raccolte S1, 1 GB di spazio di archiviazione per ogni, nell'area Stati Uniti orientali hello, e si esegue la migrazione di queste 10 S1 raccolte too10 raccolte con partizione singola 400 UR/sec (livello minimo di hello). La fattura sarà simile al seguente se si mantengono le raccolte con partizione singola 10 hello per un intero mese:

![Come S1 prezzi per le 10 raccolte Confronta too10 raccolte con prezzi per un insieme di singola partizione](./media/performance-levels/s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a>Come bisogna comportarsi se sono necessari più di 10 GB di spazio di archiviazione?

Se si dispone di una raccolta con un livello di prestazioni S1, S2 o S3 o dispone di una raccolta di sola partizione, ognuno dei quali dispone di 10 GB di spazio di archiviazione disponibile, è possibile utilizzare hello migrazione dei dati DB Cosmos strumento toomigrate tooa i dati partizionati insieme con virtualmente archiviazione illimitata. Per informazioni sui vantaggi di hello di una raccolta partizionata, vedere [partizionamento e la scalabilità in Azure Cosmos DB](documentdb-partition-data.md). Per informazioni su come toomigrate le S1, S2, S3 o raccolta tooa partizionata raccolta singola partizione, vedere [la migrazione da una singola partizione toopartitioned raccolte](documentdb-partition-data.md#migrating-from-single-partition). 

<a name="change-before"></a>

## <a name="can-i-change-between-hello-s1-s2-and-s3-performance-levels-before-august-1-2017"></a>È possibile modificare tra livelli di prestazioni di S1, S2 e S3 hello prima 1 agosto 2017?

Solo gli account esistenti con le prestazioni S1, S2 e S3 verranno in grado di toochange e modificare i livelli di livello delle prestazioni tramite il portale di hello o a livello di codice. Entro il 1 ° agosto 2017 S1, S2, hello e livelli di prestazioni S3 non saranno disponibili. Se si modifica dalla raccolta di sola partizione tooa S1, S3 o S3, è possibile restituire toohello livelli di prestazioni S1, S2 o S3.

<a name="when-migrated"></a>

## <a name="how-will-i-know-when-my-collection-has-migrated"></a>Come è possibile sapere quando sarà stata eseguita la migrazione di una raccolta?

migrazione di Hello verificherà su 31 luglio 2017. Se si dispone di una raccolta che utilizza hello S1, S2 o S3 livelli di prestazioni, il team di DB Cosmos hello contatterà l'utente tramite posta elettronica prima della migrazione hello. Al termine della migrazione hello, su 1 agosto 2017, verrà visualizzato hello portale di Azure che viene utilizzata la raccolta di prezzo Standard.

![Il modo tooconfirm la raccolta di cui eseguire la migrazione piano tariffario Standard toohello](./media/performance-levels/portal-standard-pricing-applied.png)

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-hello-s1-s2-s3-performance-levels-toosingle-partition-collections-on-my-own"></a>Come la migrazione da hello S1, S2, S3 prestazioni livelli toosingle le raccolte con partizione in modo personalizzato?

È possibile migrare da hello S1, S2, e le raccolte con partizione toosingle hello portale di Azure utilizzando i livelli di prestazioni S3 o a livello di codice. È possibile farlo nel proprio prima toobenefit 1 agosto dalle opzioni flessibili di velocità effettiva di hello disponibili con le raccolte con partizione singola o su 31 luglio 2017 trasferiremo le raccolte per l'utente.

**raccolte con partizione toosingle toomigrate utilizzando hello portale di Azure**

1. In hello [ **portale di Azure**](https://portal.azure.com), fare clic su **Azure Cosmos DB**, quindi selezionare hello Cosmos DB account toomodify. 
 
    Se **Azure Cosmos DB** non è in hello Jumpbar, fare clic su >, scorrere troppo**database**selezionare **Azure Cosmos DB**, quindi selezionare l'account DocumentDB hello.  

2. Menu risorse hello in **contenitori**, fare clic su **scala**selezionare hello raccolta toomodify dall'elenco a discesa hello e quindi fare clic su **tariffario**. Gli account che usano la velocità effettiva predefinita hanno un piano tariffario S1, S2 o S3.  In hello **scegliere il piano tariffario** pannello, fare clic su **Standard** toochange definito toouser velocità effettiva, quindi fare clic su **selezionare** toosave la modifica.

    ![Cattura di schermata del pannello impostazioni hello che mostra dove toochange hello il valore di velocità effettiva](./media/performance-levels/change-performance-set-thoughput.png)

3. In hello **scala** blade, hello **tariffario** è stato modificato anche**Standard** hello e **velocità effettiva (UR/sec)** viene visualizzata con un valore predefinito di 400. Velocità effettiva di hello set compreso tra 400 e 10.000 [unità richieste](request-units.md)al secondo (UR/sec). Hello **fattura mensile stimato** nella parte inferiore di hello di hello pagina Aggiorna automaticamente tooprovide una stima del costo mensile hello. 

    >[!IMPORTANT] 
    > Dopo aver salvato le modifiche e spostare piano tariffario Standard toohello, è possibile eseguire il rollback toohello livelli di prestazioni S1, S2 o S3.

4. Fare clic su **salvare** toosave le modifiche.

    Se è necessaria una velocità effettiva maggiore di 10.000 UR/sec o uno spazio di archiviazione maggiore di 10 GB è possibile creare una raccolta partizionata. toomigrate una raccolta partizionata tooa raccolta singola partizione, vedere [la migrazione da una singola partizione toopartitioned raccolte](documentdb-partition-data.md#migrating-from-single-partition).

    > [!NOTE]
    > Minuti too2 potrebbe richiedere la modifica da tooStandard S1, S2 o S3.
    > 
    > 

**utilizzando le raccolte con partizione toosingle toomigrate hello .NET SDK**

Un'altra opzione per la modifica dei livelli di prestazioni degli insiemi è tramite SDK. Questa sezione sono disponibili solo se si modificano prestazioni di una raccolta di livello utilizzando il nostro [API .NET di DocumentDB](documentdb-sdk-dotnet.md), ma il processo di hello è simile per altri SDK di questo.

Di seguito è riportato un frammento di codice per la modifica hello insieme velocità effettiva too5, 000 unità di richiesta al secondo:
    
```C#
    //Fetch hello resource toobe updated
    Offer offer = client.CreateOfferQuery()
                      .Where(r => r.ResourceLink == collection.SelfLink)    
                      .AsEnumerable()
                      .SingleOrDefault();

    // Set hello throughput too5000 request units per second
    offer = new OfferV2(offer, 5000);

    //Now persist these changes toohello database by replacing hello original resource
    await client.ReplaceOfferAsync(offer);
```

Visitare [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) tooview ulteriori esempi e ulteriori informazioni sui metodi offerta:

* [**ReadOfferAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [**ReadOffersFeedAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [**ReplaceOfferAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [**CreateOfferQuery**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a>Quali sono le conseguenze per i clienti EA?

I clienti EA saranno prezzo protetto fino al fine di hello del contratto corrente.

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni sui prezzi e la gestione dei dati con Azure Cosmos DB, è esplorare queste risorse:

1.  [Partizionamento dei dati in Cosmos DB](documentdb-partition-data.md). Comprendere la differenza hello tra contenitore singola partizione e contenitori partizionati, nonché suggerimenti sull'implementazione di un esempio di strategia partizionamento tooscale senza problemi.
2.  [Prezzi di Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/). Informazioni sui costi di hello del provisioning di velocità effettiva e l'utilizzo di archiviazione.
3.  [Unità richiesta](request-units.md). Comprendere il consumo di hello di velocità effettiva per i tipi di operazione diversa, ad esempio lettura, scrittura, Query.
