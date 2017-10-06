---
title: elenco di controllo sicurezza database aaaAzure | Documenti Microsoft
description: Questo articolo fornisce un set di elenco di controllo per la sicurezza del database di Azure.
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: 5e3a69591df3c8508a8707a2d47068342863ce93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-checklist"></a>Elenco di controllo per la sicurezza del database di Azure

toohelp migliorare la sicurezza, Database Azure include una serie di controlli di sicurezza predefinite che è possibile utilizzare toolimit e controllare l'accesso.

incluse le seguenti:

-   Un firewall che consente di toocreate [regole del firewall](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-firewall-configure) limitando la connettività utilizzando un indirizzo IP,
-   Firewall di livello server accessibili da hello portale di Azure
-   Regole del firewall a livello di database accessibili da SSMS
-   Database tooyour connettività sicura tramite stringhe di connessione protetta
-   Usare la gestione degli accessi
-   Crittografia dei dati
-   Controllo del database SQL
-   Rilevamento delle minacce nel database SQL

## <a name="introduction"></a>Introduzione
Il cloud computing richiede nuovi paradigmi di sicurezza che sono utenti applicazioni toomany familiarità, gli amministratori di database e i programmatori. Di conseguenza, alcune organizzazioni sono tooimplement propense un'infrastruttura cloud per la gestione di data di scadenza tooperceived rischi di sicurezza. Tuttavia, la maggior parte di questo problema può essere mitigata tramite una migliore comprensione della funzionalità di sicurezza hello incorporate in Microsoft Azure e Database SQL di Microsoft Azure.

## <a name="checklist"></a>Elenco di controllo
È consigliabile leggere hello [Azure Database Security Best Practices](https://docs.microsoft.com/en-us/azure/security/azure-database-security-best-practices) articolo precedente tooreviewing questo elenco di controllo. Dopo aver compreso le procedure consigliate di hello sarà in grado di tooget hello meglio questo elenco di controllo. È quindi possibile utilizzare toomake questo elenco di controllo per assicurarsi che si sono stati risolti i problemi importanti di hello nella sicurezza del database di Azure.


|Categoria dell'elenco di controllo| Descrizione|
| ------------ | -------- |
|**Proteggere i dati**||
| <br> Crittografia in movimento/transito| <ul><li>[Livello di sicurezza del trasporto](https://docs.microsoft.com/en-us/windows-server/security/tls/transport-layer-security-protocol), per la crittografia dei dati quando i dati si spostano toohello reti.</li><li>Database richiede una connessione sicura da client basati su hello [TDS (flusso di dati tabulare)](https://msdn.microsoft.com/en-in/library/dd357628.aspx) protocollo TLS (Transport Layer Security).</li></ul> |
|<br>Crittografia di dati inattivi| <ul><li>[Transparent Data Encryption](http://go.microsoft.com/fwlink/?LinkId=526242), quando i dati inattivi vengono archiviati fisicamente in qualsiasi forma digitale.</li></ul>|
|**Controllare l'accesso**||  
|<br> Accesso al database | <ul><li>[Autenticazione](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access) l'autenticazione AD (Autenticazione di Azure Active Directory) usa identità gestite da Azure Active Directory.</li><li>[Autorizzazione](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access) concedere agli utenti hello privilegi minimi necessari.</li></ul> |
|<br>Accesso all'applicazione| <ul><li>[Sicurezza di livello di riga](https://msdn.microsoft.com/library/dn765131) (utilizzando criteri di sicurezza, a hello stesso tempo, limitare l'accesso a livello di riga in base al contesto di identità, ruolo o l'esecuzione di un utente).</li><li>[La maschera dati dinamica](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-dynamic-data-masking-get-started) (con autorizzazione & criteri, limita l'esposizione dei dati sensibili nascondendoli agli utenti con privilegi toonon)</li></ul>|
|**Monitoraggio proattivo**||  
| <br>Monitoraggio e rilevamento| <ul><li>[Il controllo](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing) tiene traccia degli eventi di database e li scrive i log di controllo tooan / attività Accedi il [account di archiviazione Azure](https://docs.microsoft.com/en-us/azure/storage/storage-create-storage-account).</li><li>Tenere traccia dell'integrità del database di Azure tramite i [log attività di Monitoraggio di Azure](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs).</li><li>[Rilevamento delle minacce](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-threat-detection) rileva attività database anomale che possono indicare potenziali database toohello rischi di sicurezza. </li></ul> |
|<br>Centro sicurezza di Azure| <ul><li>Il [Monitoraggio dati](https://docs.microsoft.com/en-us/azure/security-center/security-center-enable-auditing-on-sql-databases) usa il centro sicurezza di Azure come soluzione di monitoraggio di sicurezza centralizzato per SQL e altri servizi di Azure.</li></ul>|     

## <a name="conclusion"></a>Conclusione
Il database di Azure è una piattaforma di database affidabile, con una gamma completa di funzionalità di sicurezza che soddisfano molti requisiti normativi e aziendali. È possibile proteggere i dati facilmente il controllo hello accesso fisico tooyour dati e tramite un'ampia gamma di opzioni per la protezione dei dati in file hello-, colonna o a livello di riga con Transparent Data Encryption, la crittografia a livello di cella o sicurezza a livello di riga. Always Encrypted consente inoltre operazioni sui dati crittografati, semplificando il processo di hello di aggiornamenti dell'applicazione. A sua volta, i registri di accesso tooauditing dell'attività del Database SQL vengono fornite informazioni hello necessarie, consentendo tooknow come e quando si accede ai dati.

## <a name="next-steps"></a>Passaggi successivi
È possibile migliorare la protezione hello del database rispetto a utenti malintenzionati o di accesso non autorizzato con pochi semplici passaggi. In questa esercitazione si apprenderà come:

- Configurare le [regole del firewall](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-firewall-configure) per il server e/o il database.
- Proteggere i dati con la [crittografia](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/sql-server-encryption).
- Abilitare il [controllo del database SQL](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing).

