---
title: Azure con Azure RemoteApp aaaSQL | Documenti Microsoft
description: Informazioni su come toouse SQL Azure con Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
editor: 
ms.assetid: 35f81d75-bfd7-4980-807e-00339f2cb2a4
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: fec4cb1f1ab3cde03b6ff613650e01bae3552824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-azure-with-azure-remoteapp"></a>SQL Azure con Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Spesso quando i clienti scelgono toohost delle applicazioni Windows nel cloud hello con Azure RemoteApp desiderano anche toomigrate i propri dati, ad esempio SQL Server in hello cloud per la distribuzione di un intero cloud. Ciò consente di ospitare nel cloud l'intera soluzione che risulta accessibile ovunque in qualsiasi momento da qualsiasi dispositivo con Azure RemoteApp. Di seguito sono riportati collegamenti e i riferimenti insieme a indicazioni toohelp è con questo processo.  

## <a name="migrate-your-sql-data"></a>Eseguire la migrazione dei dati di SQL
Iniziare con [la migrazione di un tooAzure di database di SQL Server Database SQL](../sql-database/sql-database-cloud-migrate.md). 

## <a name="configure-azure-remoteapp"></a>Configurare Azure RemoteApp
Ospitare l'applicazione Windows in Azure RemoteApp. Di seguito sono elencati i passaggi generali:

1. Creare hello [modello VM di Azure RemoteApp](remoteapp-imageoptions.md). 
2. Installare un'applicazione hello necessarie in hello macchina virtuale.
3. Configurare un'applicazione hello in modo che si connette toohello database di SQL Server e verificare che il funzionamento.
4. Sysprep e arrestare hello macchina virtuale. Acquisirla come immagine da usare con Azure. **Nota:** è necessario che un'applicazione hello sia le informazioni sulla connettività tramite il processo di sysprep hello tooretain in grado di hello DB tooensure. Se un'applicazione hello è informazioni di connessione non è possibile tooretain hello DB, è possibile fornitore hello tooengage di toocheck applicazione hello modo è possibile specificare la stringa di connessione hello.
5. Importare l'immagine personalizzata hello alla libreria di Azure RemoteApp selezionando hello corretta posizione geografica che si trova la distribuzione di SQL Azure. 
6. Distribuire una raccolta RemoteApp in hello stessi dati come la distribuzione di SQL Azure utilizzando hello sopra modello al centro e pubblicano un'applicazione hello. Distribuzione di Azure RemoteApp in hello stesso data center, come la distribuzione di SQL Azure consente di garantire velocità di connessione più veloce hello e ridurre la latenza. 

## <a name="app-and-sql-configuration-considerations"></a>Considerazioni sulla configurazione dell'app e di SQL:
Esistono alcuni punti tooconsider quando si utilizza SQL Azure con RemoteApp:

Informazioni su [tooconfigure SQL Azure database firewall](../sql-database/sql-database-firewall-configure.md). Un estratto di codice degli stati di articolo hello, "inizialmente, tutti i server di Database SQL di Azure tooyour accesso è bloccato dal firewall hello. In ordine toobegin utilizzando il server di Database SQL di Azure, è necessario passare toohello portale classico e specificare una o più regole firewall di livello server che consentono di server di accesso tooyour Database SQL di Azure. Utilizzare toospecify regole firewall di hello quale indirizzo IP compreso tra hello Internet consentiti e o meno le applicazioni Azure possano tentare server di Database SQL di Azure tooyour tooconnect".

Inoltre, quando un computer tenta di server di database tooyour tooconnect da hello Internet, firewall hello controlla hello provenienti dall'indirizzo IP di una richiesta hello set completo di hello di livello server e (se richiesto) regole firewall a livello di database. "Se l'indirizzo IP hello della richiesta di hello è in uno degli intervalli di hello specificati nelle regole del firewall a livello di server hello, hello connessione viene concessa tooyour server di Database SQL di Azure." Quindi è possibile usare intervalli IP e non solo singoli indirizzi IP di origine.

Seguire le istruzioni dettagliate hello in [procedura: configurare le impostazioni del firewall nel Database SQL mediante il portale di Azure hello](../sql-database/sql-database-configure-firewall-settings.md) intervallo IP di toospecify hello. Quando si configurano le regole Firewall di SQL hello, specificare l'intervallo IP hello della subnet hello specificato per hello raccolta di Azure RemoteApp. Questo dovrebbe consentire tooconnect toohello DB di SQL Server ARA hello anche se verrà dinamicamente-assegnati gli indirizzi IP.

## <a name="troubleshooting"></a>Risoluzione dei problemi
Se verifica hello dell'utilizzo di un'applicazione client ospitata in Azure RemoteApp che si connette tooa SQL del database in cui è ospitato in Azure o locale è lento potrebbe esserci una serie di motivi perché.  

* Latenza di rete da tooAzure il dispositivo è elevata. Spostare toohello connessione di rete migliore e più rapido che è possibile per ottenere prestazioni ottimali. Utilizzare [azurespeed.com](http://azurespeed.com/) come un tootest strumento generico centro dati tooAzure latenza dispositivi.  
* L'app client ospitata in Azure RemoteApp è in condizione di stress. Selezionare un altro piano di fatturazione, ad esempio la fatturazione Premium, per migliorare le prestazioni. Un'altra soluzione consiste risorse hello toomonitor dell'applicazione: durante una sessione attiva, eseguire una sequenza di tasti ctrl-alt-end che avvierà hello SAS schermata, scegliere Gestione attività e osservare l'utilizzo delle risorse per l'app.
* SQL Server è in condizioni di stress o non è ottimizzato. Seguire le indicazioni relative a SQL per la risoluzione dei problemi. 

