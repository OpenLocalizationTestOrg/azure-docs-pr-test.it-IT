---
title: 'Crittografia di database inattivi: Azure Cosmos DB | Microsoft Docs'
description: Informazioni sulla crittografia predefinita per tutti i dati offerta da Azure Cosmos DB.
services: cosmos-db
author: voellm
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 99725c52-d7ca-4bfa-888b-19b1569754d3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: voellm
ms.openlocfilehash: d52d55fe45fdd18394166ec7ccd6e46e8f8f434b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-database-encryption-at-rest"></a>Crittografia di dati inattivi del database in Azure Cosmos DB

Crittografia è una frase che in genere fa riferimento toohello crittografia dei dati sui dispositivi di archiviazione non volatili, ad esempio unità (SSD Solid) a stato solido e unità disco rigido (HDD). Cosmos DB archivia i propri database primari su SSD. Gli allegati multimediali e i backup vengono memorizzati nell'archiviazione BLOB di Azure, di cui in genere si esegue il backup su HDD. Con versione di hello di crittografia per Cosmos DB, vengono crittografati tutti i database, gli allegati di supporti e i backup. I dati ora vengono crittografati in transito (sulla rete hello) e a inattivi (volatile), fornire la crittografia end-to-end.

Come un servizio PaaS, Cosmos DB è toouse molto semplice. Poiché tutti i dati utente archiviati nel database Cosmos vengono crittografati a riposo e nel trasporto, non è tootake alcuna azione. Un altro modo tooput ciò è che la crittografia a rest è "on" per impostazione predefinita. Non esistono alcun tooturn controlli, o disattivare. È fornire questa funzionalità, continuando invece toomeet nostri [i contratti di servizio a disponibilità e prestazioni](https://azure.microsoft.com/support/legal/sla/cosmos-db).

## <a name="implement-encryption-at-rest"></a>Implementare la crittografia di dati inattivi

La crittografia dei dati inattivi viene implementata attraverso una serie di tecnologie di protezione, inclusi i sistemi di archiviazione protetta delle chiavi, le reti crittografate e le API di crittografia. I sistemi che decrittografano ed elaborano i dati includono toocommunicate i sistemi di gestione delle chiavi. Hello è illustrata la modalità di separazione di archiviazione di gestione di dati e hello crittografata delle chiavi. 

![Diagramma di progettazione](./media/database-encryption-at-rest/design-diagram.png)

flusso di base di una richiesta utente Hello è come segue:
- account del database utente Hello è ora pronta e chiavi di archiviazione vengono recuperate tramite un Provider di risorse del servizio di gestione di toohello richiesta.
- Un utente crea una connessione tooCosmos DB, tramite il trasporto HTTPS/protetto. (dettagli di hello astratta SDK hello).
- utente Hello invia un toobe documento JSON archiviati su hello connessione sicura creata in precedenza.
- documento JSON Hello è indicizzata, a meno che l'utente hello ha disattivato l'indicizzazione.
- Hello documento JSON sia i dati dell'indice vengono scritti toosecure archiviazione.
- Periodicamente, i dati vengono lettura dall'archiviazione sicura hello e backup toohello archivio Blob di Azure crittografato.

## <a name="frequently-asked-questions"></a>Domande frequenti

### <a name="q-how-much-more-does-azure-storage-cost-if-storage-service-encryption-is-enabled"></a>D: A quanto ammonta il costo aggiuntivo dell'Archiviazione di Azure se si abilita la crittografia del servizio di archiviazione?
R: Non sono previsti costi aggiuntivi.

### <a name="q-who-manages-hello-encryption-keys"></a>D: chi gestisce le chiavi di crittografia hello?
R: le chiavi di hello vengono gestite da Microsoft.

### <a name="q-how-often-are-encryption-keys-rotated"></a>D: Con quale frequenza vengono ruotate le chiavi di crittografia?
R: Microsoft ha un set di linee guida interne per la rotazione della chiave di crittografia che segue Cosmos DB. linee guida specifiche Hello non vengono pubblicate. Microsoft pubblica hello [Security Development Lifecycle (SDL)](https://www.microsoft.com/sdl/default.aspx), che viene considerata come un subset di indicazioni interno e dispone di procedure consigliate utili per gli sviluppatori.

### <a name="q-can-i-use-my-own-encryption-keys"></a>D: È possibile usare le proprie chiavi di crittografia?
R: cosmos DB è un servizio PaaS e abbiamo lavorato tookeep rigido hello servizio facile toouse. Spesso questa domanda viene usata come domanda di proxy per soddisfare un requisito conformità come PCI-DSS. Come parte della creazione di questa funzionalità, abbiamo collaborato con tooensure i revisori di conformità che i clienti che utilizzano DB Cosmos soddisfano i requisiti senza hello necessità toomanage stesse chiavi.
Di conseguenza, è attualmente non sono disponibili agli utenti hello opzione tooburden autonomamente con la gestione delle chiavi.

### <a name="q-what-regions-have-encryption-turned-on"></a>D: In quali aree è attiva la crittografia?
R: La crittografia è attiva in tutte le aree di Azure Cosmos DB per tutti i dati utente.

### <a name="q-does-encryption-affect-hello-performance-latency-and-throughput-slas"></a>D: crittografia influiscono sulla latenza di prestazioni hello e velocità effettiva i contratti di servizio?
R: non è Nessun impatto o modifiche toohello delle prestazioni i contratti di servizio dopo che la crittografia inattivi è abilitata per tutti gli account nuovi ed esistenti. Altre informazioni su hello [contratto di servizio per Cosmos DB](https://azure.microsoft.com/support/legal/sla/cosmos-db) pagina garanzie di toosee hello più recente.

### <a name="q-does-hello-local-emulator-support-encryption-at-rest"></a>D: emulatore locale hello supporta crittografia?
R: emulatore di hello è uno strumento di sviluppo/test autonomo e non utilizza i servizi di gestione delle chiavi hello che hello usato dal servizio Cosmos DB gestito. Il Consiglio è tooenable BitLocker sulle unità in cui si archiviano dati di test sensibili emulatore. Hello [emulatore supporta la modifica delle directory dati predefinita di hello](local-emulator.md) oppure utilizzare un percorso noto.

## <a name="next-steps"></a>Passaggi successivi

Per una panoramica della sicurezza Cosmos DB e i miglioramenti più recenti di hello, vedere [la protezione del database di Azure Cosmos DB](database-security.md).
Per ulteriori informazioni su certificazioni Microsoft, vedere hello [Azure Trust Center](https://azure.microsoft.com/en-us/support/trust-center/).
