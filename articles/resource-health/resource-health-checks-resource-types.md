---
title: "aaaSupported tipi di risorse tramite integrità delle risorse di Azure | Documenti Microsoft"
description: "Tipi di risorse supportati tramite Integrità risorse di Azure"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 03/19/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: a37d5c33f6ef6fdfbce0daf392bc7fa57853c7d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resource-types-and-health-checks-in-azure-resource-health"></a>Tipi di risorse e controlli di integrità in Integrità risorse di Azure
Di seguito è riportato un elenco completo di tutti i controlli di hello eseguito tramite l'integrità delle risorse da tipi di risorse.

## <a name="microsoftcacheredisredis"></a>Microsoft.CacheRedis/Redis
|Controlli eseguiti|
|---|
|<ul><li>Backup di tutti i nodi della Cache di hello e in esecuzione?</li><li>Cache di hello raggiungibili dai Data Center hello?</li><li>Ha raggiunto il numero massimo di hello di connessioni della Cache di hello?</li><li> Cache di hello esaurito la memoria disponibile? </li><li>Cache di hello presenta un numero elevato di errori di pagina?</li><li>È hello Cache sovraccarico?</li></ul>|

## <a name="microsoftcdnprofile"></a>Microsoft.CDN/profile
|Controlli eseguiti|
|---|
|<ul> <li>Qualsiasi endpoint hello viene arrestato, rimosso o non configurati correttamente?</li><li>È accessibile per operazioni di configurazione della rete CDN portale supplementare hello?</li><li>Sono presenti problemi di recapito continuo con hello endpoint rete CDN?</li><li>Gli utenti modificabili configurazione hello delle risorse della rete CDN?</li><li>Le modifiche alla configurazione propagazione velocità hello previsto?</li><li>Possano utenti gestire la configurazione di rete CDN hello utilizzando hello portale di Azure, PowerShell o API hello?</li> </ul>|

## <a name="microsoftclassiccomputevirtualmachines"></a>Microsoft.classiccompute/virtualmachines
|Controlli eseguiti|
|---|
|<ul><li>Sia i server host hello attivo e in esecuzione?</li><li>L'avvio del sistema operativo host di hello completata?</li><li>Contenitore della macchina virtuale hello è eseguito il provisioning e acceso?</li><li>C'è connettività di rete tra host hello e account di archiviazione hello?</li><li>Hello l'avvio del sistema operativo guest hello completata?</li><li>È in corso la manutenzione pianificata?</li></ul>|

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.cognitiveservices/accounts
|Controlli eseguiti|
|---|
|<ul><li>Account hello raggiungibili dai Data Center hello?</li><li>È hello cognitivi Provider di risorse servizi disponibili?</li><li>È hello cognitivi servizio disponibile nell'area appropriata hello?</li><li>Leggere può eseguire operazioni su account di archiviazione hello dei metadati di risorsa hello?</li><li>È stata raggiunta la quota di chiamata API hello?</li><li>È stato raggiunto limite-lettura delle chiamate API hello?</li></ul>|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.compute/virtualmachines
|Controlli eseguiti|
|---|
|<ul><li>Server hello che ospita la macchina virtuale di e in esecuzione?</li><li>L'avvio del sistema operativo host di hello completata?</li><li>Contenitore della macchina virtuale hello è eseguito il provisioning e acceso?</li><li>C'è connettività di rete tra host hello e account di archiviazione hello?</li><li>Hello l'avvio del sistema operativo guest hello completata?</li><li>È in corso la manutenzione pianificata?</li></ul>|

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.datalakeanalytics/accounts
|Controlli eseguiti|
|---|
|<ul><li>Possano agli utenti di inviare processi tooData Lake Analitica in hello area?</li><li>Tale area hello eseguito e completato correttamente in processi di base?</li><li>Gli utenti elencare gli elementi del catalogo nella regione hello?</li>|


## <a name="microsoftdatalakestoreaccounts"></a>Microsoft.datalakestore/accounts
|Controlli eseguiti|
|---|
|<ul><li>Gli utenti possono caricare l'archivio data Lake di tooData nell'area di hello?</li><li>Gli utenti scaricare dati dall'archivio Data Lake nella regione hello?</li></ul>|

## <a name="microsoftdocumentdbdatabaseaccounts"></a>Microsoft.documentdb/databaseAccounts
|Controlli eseguiti|
|---|
|<ul><li>Sono state richieste database o una raccolta non servite a causa di indisponibilità del servizio DocumentDB tooa?</li><li>Sono state tutte le richieste di documenti non servite a causa di indisponibilità del servizio DocumentDB tooa?</li></ul>|

## <a name="microsoftnetworkconnections"></a>Microsoft.network/connections
|Controlli eseguiti|
|---|
|<ul><li>È stato connesso tunnel VPN hello?</li><li>Sono presenti conflitti di configurazione in connessione hello?</li><li>Chiavi già condivise hello siano configurate correttamente?</li><li>È raggiungibile dispositivo locale di hello VPN?</li><li>Sono presenti le mancate corrispondenze in Criteri di sicurezza IPSec/IKE hello?</li><li>È di connessione VPN S2S hello correttamente provisioning o in uno stato di errore?</li><li>È la connessione di rete virtuale a hello correttamente provisioning o in uno stato di errore?</li></ul>|

## <a name="microsoftnetworkvirtualnetworkgateways"></a>Microsoft.network/virtualNetworkGateways
|Controlli eseguiti|
|---|
|<ul><li>È possibile raggiungerlo dal gateway VPN hello hello internet?</li><li>È hello Gateway VPN in modalità standby?</li><li>È in esecuzione hello servizio VPN gateway hello?</li></ul>|

## <a name="microsoftnotificationhubsnamespace"></a>Microsoft.NotificationHubs/namespace
|Controlli eseguiti|
|---|
|<ul><li> Le operazioni di runtime come la registrazione, l'installazione o trasmissione possono essere eseguite nello spazio dei nomi hello?</li></ul>|

## <a name="microsoftpowerbiworkspacecollections"></a>Microsoft.PowerBI/workspaceCollections
|Controlli eseguiti|
|---|
|<ul><li>Sistema operativo host hello sia attivo in esecuzione?</li><li>Sia raggiungibile da all'esterno di datacenter hello workspaceCollection hello?</li><li>È hello Provider di risorse di Power BI disponibili?</li><li>È hello PowerBI Service disponibile nell'area appropriata hello?</li></ul>|

## <a name="microsoftsearchsearchservices"></a>Microsoft.search/searchServices
|Controlli eseguiti|
|---|
|<ul><li>Eseguire le operazioni di diagnostica del cluster hello?</li></ul>|

## <a name="microsoftsqlserverdatabase"></a>Microsoft.SQL/Server/database
|Controlli eseguiti|
|---|
|<ul><li> Sono state database toohello gli account di accesso?</li></ul>|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs
|Controlli eseguiti|
|---|
|<ul><li>Sono tutti gli host hello in cui il processo di hello è l'esecuzione di backup e in esecuzione?</li><li>È stato Impossibile toostart di hello processo?</li><li>Sono in corso aggiornamenti di runtime?</li><li>È il processo di hello in uno stato previsto (ad esempio in esecuzione o arrestato dal cliente)?</li><li>Hello processo durante le eccezioni di memoria insufficiente?</li><li>Sono in corso aggiornamenti di calcolo pianificati?</li><li>È hello Gestione esecuzioni (piano di controllo) disponibili?</li></ul>|

## <a name="microsoftwebserverfarms"></a>Microsoft.web/serverFarms
|Controlli eseguiti|
|---|
|<ul><li>Sia i server host hello attivo e in esecuzione?</li><li>Internet Information Services è in esecuzione?</li><li>Servizio di bilanciamento del carico hello è in esecuzione?</li><li>Hello il piano di servizio Web sia raggiungibile dal Data Center hello?</li><li>È disponibile hello storage account hosting hello contenuto dei siti per la server farm hello??</li></ul>|

## <a name="microsoftwebsites"></a>Microsoft.web/sites
|Controlli eseguiti|
|---|
|<ul><li>Sia i server host hello attivo e in esecuzione?</li><li>Internet Information Server è in esecuzione?</li><li>Servizio di bilanciamento del carico hello è in esecuzione?</li><li>Hello App Web sia raggiungibile dal Data Center hello?</li><li>Account di archiviazione hello ospita il contenuto del sito hello disponibile?</li></ul>|

Vedere toolearn queste risorse ulteriori informazioni sull'integrità delle risorse:
-  [Integrità delle risorse tooAzure introduzione](Resource-health-overview.md)
-  [Domande frequenti su Integrità risorse di Azure](Resource-health-faq.md)

