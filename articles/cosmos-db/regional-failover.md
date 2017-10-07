---
title: il failover in Azure Cosmos DB aaaRegional | Documenti Microsoft
description: "Informazioni sulla modalità di funzionamento di failover manuali e automatici con Azure Cosmos DB."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 446e2580-ff49-4485-8e53-ae34e08d997f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2fdc7b0e8958d129ab027e4b11193b12961ddae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-regional-failover-for-business-continuity-in-azure-cosmos-db"></a>Failover a livello di area automatici per la continuità aziendale in Azure Cosmos DB
DB Cosmos Azure semplifica la distribuzione globale di hello dei dati offrendo completamente gestiti, [account database multiarea](distribute-data-globally.md) che forniscono deselezionare i compromessi tra la coerenza, disponibilità e prestazioni, tutti con corrispondente garanzia. Account COSMOS DB offrono un'elevata disponibilità, le latenze ms cifra, [livelli di coerenza ben definiti](consistency-levels.md), il failover regionale trasparente con le API multihosting e velocità effettiva di scala hello possibilità tooelastically e archiviazione tutto il mondo hello. 

COSMOS DB supporta entrambi esplicita e failover basata su criteri che consentono di comportamento del sistema di end-to-end hello toocontrol nell'evento hello di errori. Questo articolo analizza i seguenti aspetti:

* Come funzionano i failover manuali in Cosmos DB?
* Come funzionano i failover automatici in Cosmos DB e che cosa accade quando un data center smette di funzionare?
* In che modo è possibile usare i failover manuali in architetture applicative?

In questo video di Azure Friday, con Scott Hanselman e Karthik Raman, Principal Engineering Manager, sono disponibili altre informazioni sui failover regionali.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

## <a id="ConfigureMultiRegionApplications"></a>Configurazione di applicazioni in più aree
Approfondiremo modalità di failover, verranno esaminate come è possibile configurare un vantaggio tootake applicazione disponibilità multiarea ed essere resilienti in faccia hello dei failover regionale.

* In primo luogo, distribuire l'applicazione in più aree
* accesso a bassa latenza tooensure da ogni area in cui l'applicazione viene distribuita, configurare hello corrispondente [elenco delle aree preferito](https://msdn.microsoft.com/library/microsoft.azure.documents.client.connectionpolicy.preferredlocations.aspx#P:Microsoft.Azure.Documents.Client.ConnectionPolicy.PreferredLocations) per ogni area attraverso una delle hello supportata SDK.

Hello seguente mostra come tooinitialize un'applicazione con più aree. In questo caso, hello account Azure Cosmos DB `contoso.documents.azure.com` è configurato con due aree: Europa settentrionale e Stati Uniti occidentali. 

* un'applicazione Hello viene distribuita nell'area Stati Uniti occidentali hello (tramite servizi di App di Azure, ad esempio) 
* Configurato con `West US` come area geografica preferita prima hello per una latenza bassa legge
* Configurato con `North Europe` come area geografica preferita secondo hello (per la disponibilità elevata durante gli errori locali)

In hello API DocumentDB, questa configurazione è simile a quello seguente frammento di codice hello:

```cs
ConnectionPolicy usConnectionPolicy = new ConnectionPolicy 
{ 
    ConnectionMode = ConnectionMode.Direct,
    ConnectionProtocol = Protocol.Tcp
};

usConnectionPolicy.PreferredLocations.Add(LocationNames.WestUS);
usConnectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

DocumentClient usClient = new DocumentClient(
    new Uri("https://contosodb.documents.azure.com"),
    "memf7qfF89n6KL9vcb7rIQl6tfgZsRt5gY5dh3BIjesarJanYIcg2Edn9uPOUIVwgkAugOb2zUdCR2h0PTtMrA==",
    usConnectionPolicy);
```

un'applicazione Hello viene distribuita nell'area Europa settentrionale hello con ordine hello delle regioni Preferiti invertita. Vale a dire area Europa settentrionale hello specificato prima per letture a bassa latenza. Quindi, area Stati Uniti occidentali hello viene specificato come area geografica preferita secondo hello per la disponibilità elevata durante errori internazionali.

Hello diagramma dell'architettura di esempio mostra una distribuzione di applicazioni con più aree in cui Cosmos DB e un'applicazione hello configurato toobe disponibile in quattro aree geografiche Azure.  

![Distribuzione globale di un'applicazione con Azure Cosmos DB](./media/regional-failover/app-deployment.png)

A questo punto, si esaminerà come hello Cosmos DB servizio gestisce internazionali errori tramite i failover automatici. 

## <a id="AutomaticFailovers"></a>Failover automatici
Nell'evento raro di hello di un'interruzione dell'alimentazione locale Azure o di interruzione del data center, DB Cosmos attiva automaticamente i failover di tutti gli account DB Cosmos con una presenza nell'area di hello interessata. 

**Cosa accade se si verifica un'interruzione del servizio in un'area di lettura?**

Account COSMOS DB con un'area di lettura in una delle aree di hello interessato vengono automaticamente disconnessi dal loro area di scrittura e contrassegnato come offline. Hello Cosmos DB SDK implementano un protocollo di individuazione internazionali che consenta loro tooautomatically rilevare quando è disponibile un'area e reindirizzamento leggere chiamate toohello Avanti area disponibile nell'elenco di area geografica preferita hello. Se nessuna delle aree di hello in hello preferito area elenco è disponibile, chiama automaticamente il fallback toohello area di scrittura corrente. Non sono necessarie modifiche nel failover delle applicazioni codice toohandle internazionali. Durante l'intero processo, garanzie di coerenza continuano toobe rispettata dal DB Cosmos.

![Errori di un'area di lettura in Azure Cosmos DB](./media/regional-failover/read-region-failures.png)

Una volta l'area interessata hello ripristino in caso di interruzione hello, tutti gli account Cosmos DB hello interessato nell'area di hello vengono automaticamente ripristinati dal servizio hello. Account COSMOS DB contenente un'area di lettura nell'area di hello interessato verrà quindi automaticamente la sincronizzazione con l'area di scrittura corrente e attivare online. Hello Cosmos DB SDK individuare disponibilità hello della nuova area hello e valutare se hello area deve essere selezionata come area lettura di hello corrente basato sull'elenco di area geografica preferita hello configurata da un'applicazione hello. Letture successive vengono reindirizzate toohello area ripristinato senza richiedere alcun codice di applicazione di modifiche tooyour.

**Cosa accade se si verifica un'interruzione del servizio in un'area di scrittura?**

Se l'area interessata hello è l'area di scrittura per un determinato account Cosmos DB corrente hello, quindi area hello verrà automaticamente contrassegnato come offline. Quindi, un'area alternativa viene promossa quando hello scrive area ogni conto Cosmos DB interessato. È possibile controllare completamente hello area selezione affinché gli account Cosmos DB tramite il portale di Azure hello o [a livello di codice](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_FailoverPriorityChange). 

![Priorità di failover per Azure Cosmos DB](./media/regional-failover/failover-priorities.png)

Durante i failover automatico, DB Cosmos sceglie automaticamente l'area di scrittura successiva hello per un determinato database Cosmos account in base a hello specificato l'ordine di priorità. 

![Errori di un'area di scrittura in Azure Cosmos DB](./media/regional-failover/write-region-failures.png)

Una volta l'area interessata hello ripristino in caso di interruzione hello, tutti gli account Cosmos DB hello interessato nell'area di hello vengono automaticamente ripristinati dal servizio hello. 

* Account COSMOS DB con la loro regione di scrittura precedente nell'area interessata hello viene mantenuta in modalità offline con disponibilità lettura anche dopo il ripristino di hello dell'area di hello. 
* È possibile eseguire query toocompute questa area non replicate scritture durante un'interruzione di hello mediante il confronto con dati di hello disponibili nell'area di scrittura corrente hello. In base alle esigenze di hello dell'applicazione, è possibile eseguire la risoluzione di tipo merge e/o dei conflitti e scrivere set finale di hello dell'area di scrittura delle modifiche toohello indietro corrente. 
* Dopo aver completato l'unione delle modifiche, è possibile riportare area interessata hello online rimuovendo e nuova aggiunta account di hello area tooyour DB Cosmos. Una volta area hello viene aggiunto nuovamente, è possibile configurarlo come area di scrittura hello eseguendo un failover manuale tramite hello portale di Azure o [a livello di codice](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate).

## <a id="ManualFailovers"></a>Failover manuali

I failover tooautomatic, hello corrente inoltre scrivere area di un account DB Cosmos specificato può essere modificato manualmente in modo dinamico tooone di hello aree di lettura esistente. Failover manuale può essere avviato tramite il portale di Azure hello o [a livello di codice](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate). 

Verificare che i failover manuali **zero la perdita di dati** e **zero disponibilità** perdita e normalmente hello precedente lo stato della scrittura trasferimento scrivere area toohello uno nuovo per hello specificati account DB Cosmos. Come failover automatico, hello Cosmos DB SDK automaticamente gli handle di scrittura area cambia durante i failover manuali e assicura che le chiamate sono automaticamente reindirizzato toohello nuova area di scrittura. Nessuna modifica di codice o nella configurazione è necessari i failover toomanage applicazione. 

![Failover manuali in Azure Cosmos DB](./media/regional-failover/manual-failovers.png)

Alcuni degli scenari comuni di hello in cui il failover manuale può essere utile sono:

**Seguire il modello di orologio hello**: se le applicazioni dispongono di modelli di traffico stimabile basate sull'ora hello del giorno hello, è possibile modificare periodicamente hello scrittura stato toohello più attivo area geografica basata sull'ora del giorno hello.

**Aggiornamento del servizio**: determinata distribuzione dell'applicazione distribuita a livello globale può comportare il reindirizzamento area toodifferent traffico tramite Gestione traffico durante l'aggiornamento pianificato del servizio. Tale ora la distribuzione di applicazioni è possibile utilizzare il failover manuale tookeep hello scrittura stato toohello area in cui sta toobe active traffico durante l'intervallo di aggiornamento servizio hello.

**Continuità aziendale e ripristino di emergenza, BCDR, e Disponibilità elevata e ripristino di emergenza, HADR**: la maggior parte delle applicazioni aziendali include test di continuità aziendale come parte del processo di sviluppo e rilascio. BCDR e HADR di testing è spesso un passaggio importante di certificazioni di conformità e garantisce la disponibilità del servizio in caso di hello delle interruzioni internazionali. È possibile testare conformità BCDR hello delle applicazioni che utilizzano DB Cosmos per l'archiviazione di attivare un failover manuale di account DB Cosmos e/o aggiungendo e rimuovendo un'area in modo dinamico.

In questo articolo è stata esaminata la modalità manuale e automatico lavoro failover nel database Cosmos e come è possibile configurare il DB Cosmos account e le applicazioni toobe disponibili a livello globale. Con supporto della replica globale Cosmos DB, è possibile migliorare la latenza end-to-end e verificare che siano a disponibilità elevata anche in caso di hello di errori di area. 

## <a id="NextSteps"></a>Passaggi successivi
* Informazioni su come Cosmos DB supporta la [distribuzione globale](distribute-data-globally.md)
* Informazioni sulla [coerenza globale con Azure Cosmos DB](consistency-levels.md)
* Sviluppare in più aree usando l'[API DocumentDB](../cosmos-db/tutorial-global-distribution-documentdb.md) di Azure Cosmos DB
* Informazioni su come toobuild [architetture multiarea writer](multi-region-writers.md) con Azure DocumentDB

