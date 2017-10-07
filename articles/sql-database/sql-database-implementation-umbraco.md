---
title: aaaAzure SQL Database Azure Case Study - Umbraco | Documenti Microsoft
description: Informazioni su come Umbraco Usa il provisioning di Database SQL tooquickly e scalare un servizio per migliaia di tenant nel cloud hello
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5243d31e-3241-4cb0-9470-ad488ff28572
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 93e39e509831a5ff90f129d9537ece0b0dafef0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="umbraco-uses-azure-sql-database-tooquickly-provision-and-scale-services-for-thousands-of-tenants-in-hello-cloud"></a>Umbraco viene utilizzato il provisioning di Database SQL di Azure tooquickly e scalare un servizio per migliaia di tenant nel cloud hello
![Logo di Umbraco](./media/sql-database-implementation-umbraco/umbracologo.png)

Umbraco è un sistema di gestione del contenuto di open source più diffuso (CMS) che può eseguire alcuna operazione da siti di piccole dimensioni campagna o brochure toocomplex applicazioni per aziende classificate Fortune 500 e siti Web di supporto globale. 

> "È disponibile una vasta community di sviluppatori che utilizzano il sistema di hello, con più di 100.000 sviluppatori nei forum e più di 350.000 nei siti che sono in tempo reale, in esecuzione Umbraco".
> 
> - Morten Christensen, responsabile tecnico, Umbraco
> 
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-Case-Study-Umbraco/player]
> 
> 

distribuzioni dei clienti, toosimplify Umbraco aggiunto Umbraco-as-a-Service (UaaS): un'offerta di software-as-a-service (SaaS) che elimina la necessità di hello per le distribuzioni locali, offre scalabilità predefinite e rimuove gestione overhead abilitando gli sviluppatori toofocus gestione innovazione piuttosto che come soluzione di prodotto. Umbraco è in grado di tooprovide tutti questi vantaggi basandosi sulle hello del modello flessibile platform-as-a-service (PaaS) offerto da Microsoft Azure.

UaaS consente ai clienti di SaaS toouse Umbraco CMS funzionalità che precedentemente erano presenti fuori la copertura. Per questi clienti viene eseguito il provisioning di un ambiente CMS di lavoro con un database di produzione. I clienti possono sommarsi tootwo database aggiuntivi per lo sviluppo e di ambienti, a seconda dei requisiti di gestione temporanea. Quando è necessario un nuovo ambiente, al cliente viene assegnato automaticamente un database tramite un processo automatizzato. Hello nuovo database è pronto, in secondi, in quanto database hello è già stato già eseguito il provisioning Umbraco da un pool elastico Azure dei database disponibili (vedere la figura 1).

![Ciclo di vita del provisioning Umbraco](./media/sql-database-implementation-umbraco/figure1.png)

Figura 1. Ciclo di vita del provisioning per Umbraco-as-a-Service (UaaS)

## <a name="azure-elastic-pools-and-automation-simplify-deployments"></a>Automazione e pool elastici di Azure per semplificare le distribuzioni
Con il database SQL di Azure e altri servizi di Azure, i clienti Umbraco possono eseguire autonomamente il provisioning dei propri ambienti e Umbraco può monitorare e gestire facilmente i database come parte di un flusso di lavoro intuitivo:

1. Eseguire il provisioning
   
   Umbraco gestisce 200 database disponibili, il cui provisioning è stato eseguito preventivamente da pool elastici. Quando un nuovo cliente si iscrive per UaaS, Umbraco fornisce cliente hello con un nuovo ambiente CMS quasi in tempo reale mediante assegnazione di un database dal pool di disponibilità hello.
   
   Quando un pool di disponibilità raggiunge la soglia, viene creato un nuovo pool elastico e i nuovi database sono pre-provisioning toobe assegnato toocustomers in base alle esigenze.
   
   L'implementazione è completamente automatizzata tramite le librerie di gestione in C# e le code del bus di servizio.
2. Uso
   
   I clienti utilizzare uno toothree ambienti (per la produzione, gestione temporanea e/o sviluppo), ognuno con il proprio database. Database del cliente sono in pool elastici, che consente di Umbraco tooprovide scalabilità senza dover eseguire il provisioning tooover efficiente.
   
   ![Panoramica del progetto Umbraco](./media/sql-database-implementation-umbraco/figure2.png)
   
   ![Dettagli del progetto Umbraco](./media/sql-database-implementation-umbraco/figure3.png)
   
   Figura 2. Sito Web di clienti con Umbraco-as-a-Service (UaaS) che mostra una panoramica e i dettagli del progetto
   
   Database SQL di Azure Usa unità di transazione Database (Dtu) toorepresent hello potenza relativa necessario per le transazioni di database reali. Per i clienti UaaS, i database in genere funzionano in Dtu circa 10, ma ciascuno con hello elasticità tooscale su richiesta. I clienti possono quindi disporre delle risorse necessarie, anche durante le ore di punta. Durante un recente evento sportivo domenica, ad esempio, un cliente UaaS verificato picchi di database di Dtu too100 per durata hello di gioco hello. Azure pool elastici consentito a Umbraco toosupport che richiedono elevata senza un calo delle prestazioni.
3. Monitorare
   
   Umbraco Monitor attività con i dashboard nel portale di Azure con gli avvisi di posta elettronica personalizzati hello del database.
4. Ripristino di emergenza
   
   Azure offre due opzioni di ripristino di emergenza (DR): la replica geografica attiva e il ripristino geografico. opzione di ripristino di emergenza che una società deve selezionare Hello dipende relativo [gli obiettivi di continuità aziendale](sql-database-business-continuity.md).
   
   replica geografica attiva offre livello più veloce di hello della risposta nell'evento hello del tempo di inattività. Usando la replica geografica attiva, è possibile creare backup toofour database secondari leggibili in aree diverse, ed è quindi possibile avviare tooany failover dei database secondari hello nell'evento hello di un errore.
   
   Umbraco non richieda la replica geografica, ma si usufruire del ripristino a livello geografico Azure toohelp verificare tempi di inattività minimo nell'evento hello di interruzione. il ripristino geografico si basa sui backup di database nell'archiviazione di Azure con ridondanza geografica. Che consente agli utenti toorestore da una copia di backup quando è presente un'interruzione del servizio nell'area primaria hello.
5. Deprovisioning
   
   Quando viene eliminato l'ambiente di un progetto, tutti i database associati (di sviluppo, di gestione temporanea o live) vengono rimossi durante la pulizia della coda del bus di servizio. Questo processo automatizzato ripristini hello pool elastico la disponibilità dei database del database inutilizzati tooUmbraco, rendendoli disponibili per il provisioning future mantenendo l'utilizzo massimo.

## <a name="elastic-pools-allow-uaas-tooscale-with-ease"></a>Pool elastici consentire UaaS tooscale con facilità
Sfruttare i pool elastici Azure, Umbraco possibile ottimizzare le prestazioni per i clienti senza tooover - o effettuare il provisioning insufficiente. Umbraco è attualmente circa 3.000 database tra i pool elastici 19, con hello possibilità tooeasily scalabilità come necessari tooaccommodate uno qualsiasi dei 325,000 clienti esistenti o nuovi clienti che sono pronti toodeploy un CMS nel cloud hello.

In realtà, in base tooMorten Christensen, Technical Lead presso Umbraco, "UaaS sono ora verificati aumento delle dimensioni di circa 30 nuovi clienti al giorno. I clienti lieti praticità hello di essere in grado di tooprovision nuovi progetti in secondi, pubblicare aggiornamenti tootheir in tempo reale di siti da un ambiente di sviluppo mediante 'installazione di un solo clic' immediatamente e apportare modifiche altrettanto rapidamente se vengono individuati errori . "

Se un cliente non ha più necessità di un secondo e/o un terzo ambiente, è possibile rimuovere semplicemente questi ambienti. Che consente di liberare risorse che possono essere utilizzate per altri clienti come parte del pool elastico la disponibilità dei database Umbraco hello.

![Architettura di distribuzione Umbraco](./media/sql-database-implementation-umbraco/figure4.png)

Figura 3. Architettura per la distribuzione di UaaS in Microsoft Azure

## <a name="hello-path-from-datacenter-toocloud"></a>percorso di Hello dalla toocloud datacenter
Quando gli sviluppatori di Umbraco hello inizialmente resa hello decisione toomove tooa modello SaaS, sapevano che devono toobuild un modo economico e scalabile servizio hello.

> "I pool elastici sono perfetti per l'offerta SaaS perché consentono di aumentare o ridurre la capacità in base alle esigenze. Il provisioning è semplice e grazie alla configurazione è possibile ottimizzare il livello di utilizzo".
> 
> - Morten Christensen, responsabile tecnico, Umbraco
> 
> 

"Desideravamo toospend tempo sulla risoluzione dei problemi dei clienti, non gestire l'infrastruttura. Desideravamo toomake è più facile per tooget nostri clienti hello maggior valore, "afferma Niels Hartvig, fondatore di Umbraco. "È considerato inizialmente hello server effettuata di hosting, ma la pianificazione della capacità avrebbe un incubo". Non a caso, Umbraco non impiega amministratori di database, aspetto che evidenzia l'uso di UaaS come proposta di valore chiave.

Un obiettivo importante per gli sviluppatori di Umbraco hello è un modo per gli ambienti di tooprovision clienti UaaS tooprovide rapidamente e senza limiti di capacità. Ma fornisce che un servizio ospitato dedicato in Data Center Umbraco avrebbe richiesto un numero elevato di capacità in eccesso toohandle aumenta in elaborazione. Ciò avrebbe comportato l'aggiunta di una notevole infrastruttura di calcolo che sarebbe stata frequentemente sottoutilizzata.

Inoltre, i team di sviluppo Umbraco hello desiderato una soluzione che consentirebbe tooreuse quanto più possibile il loro codice esistente. Gli sviluppatori di Umbraco Mikkel Madsen gli stati "Siamo lieti con strumenti di sviluppo Microsoft hello che è stato già familiarità, ad esempio Microsoft SQL Server, Database SQL di Microsoft Azure, ASP.net e Internet Information Services (IIS). Prima di investire in una IaaS o un PaaS cloud soluzione, Desideravamo toomake assicurarsi che verrebbe supporta il nostro gli strumenti di Microsoft e piattaforme, in modo non sarebbe abbiamo toomake considerevoli modifiche tooour codebase. "

toomeet tutti i relativi criteri Umbraco cercata un partner di cloud con hello qualificazioni seguenti:

* Affidabilità e capacità adeguata
* Supporto per strumenti di sviluppo di Microsoft, in modo che Umbraco tecnici non sarebbe forzato toocompletely reinventare proprio ambiente di sviluppo
* Presenza in tutti i mercati hello in cui UaaS in competizione (aziende necessità tooensure che possono accedere rapidamente ai dati e che sono archiviati i dati in una posizione che soddisfi i requisiti normativi internazionali)

## <a name="why-umbraco-chose-azure-for-uaas"></a>Perché Umbraco ha scelto Azure per UaaS
In base tooMorten Christensen "tenendo conto di tutte le opzioni, è selezionato Azure perché soddisfatto tutti i criteri, gestibilità e scalabilità toofamiliarity e la convenienza economica. Impostiamo ambienti hello in macchine virtuali di Azure e ogni ambiente dispone della propria istanza di Database SQL di Azure, con tutte le istanze di hello nei pool elastico. Separando i database tra ambienti di sviluppo, gestione temporanea e in tempo reale, possiamo offrire ai clienti ottime prestazioni isolamento corrispondente tooscale, ovvero una notevole vittoria. "

Morten continuerà, "prima, abbiamo tooprovision server per i database web manualmente. A questo punto, non abbiamo toothink su di esso. Tutto ciò che è automatizzato, dal provisioning toocleanup. "

Morten è inoltre buona hello scalabilità funzionalità fornite da Azure. "I pool elastici sono perfetti per l'offerta SaaS perché consentono di aumentare o ridurre la capacità in base alle esigenze. Il provisioning è semplice e grazie alla configurazione è possibile ottimizzare il livello di utilizzo". Stati morten, "semplicità hello del pool elastico, insieme a garanzia hello di Dtu in base a livelli di servizio, offre hello power tooprovision nuovo pool di risorse su richiesta. Di recente, uno dei nostri clienti più grande picco Dtu too100 nel proprio ambiente in tempo reale. Uso di Azure, i pool elastici fornito i database del cliente hello con risorse hello necessarie in tempo reale senza requisiti DTU toopredict. In altre parole, i clienti ottenere hello tempo che si aspettano e poter soddisfare i contratti di servizio delle prestazioni".

Mikkel Madsen sommi: "è stato adottato hello potente Azure algoritmo che si connette a un modello comune di SaaS scenario (caricamento nuovi clienti in tempo reale su larga scala) tooour applicazione (pre-provisioning del database, sia lo sviluppo e in tempo reale) nella parte superiore di hello tecnologia sottostante (tramite le code del Bus di servizio di Azure in combinazione con il Database di SQL Azure)."

## <a name="with-azure-uaas-is-exceeding-customer-expectations"></a>Con Azure il servizio UaaS supera le aspettative dei clienti
Dopo la scelta di Azure come partner di cloud, Umbraco è stato in grado di tooprovide UaaS clienti con prestazioni ottimizzate di gestione del contenuto, senza investimenti di hello risorse IT necessari da una soluzione indipendente. Come Morten è indicato "noi piace praticità developer hello e la scalabilità che offre Azure e i clienti sono ora con l'affidabilità e le funzionalità di hello. Il successo è stato grande da ogni punto di vista".

## <a name="more-information"></a>Altre informazioni
* toolearn ulteriori informazioni sui pool elastici Azure, vedere [pool elastici](sql-database-elastic-pool.md).
* toolearn ulteriori informazioni su Azure Service Bus, vedere [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).
* toolearn ulteriori informazioni sui ruoli Web e ruoli di lavoro, vedere [i ruoli di lavoro](../fundamentals-introduction-to-azure.md#compute).    
* toolearn informazioni sulle reti virtuali, vedere [la rete virtuale](https://azure.microsoft.com/documentation/services/virtual-network/).    
* toolearn ulteriori informazioni su backup e ripristino, vedere [la continuità aziendale](sql-database-business-continuity.md).    
* vedere toolearn ulteriori informazioni su Monitoraggio ppols, [monitoraggio pool](sql-database-elastic-pool-manage-portal.md).    
* toolearn ulteriori informazioni su Umbraco come servizio, vedere [Umbraco](https://umbraco.com/cloud).

