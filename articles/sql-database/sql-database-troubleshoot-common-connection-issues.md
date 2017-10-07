---
title: problemi di connessione comuni aaaTroubleshoot tooAzure Database SQL
description: Passaggi tooidentify e risolvere comuni errori di connessione per il Database SQL di Azure.
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: ac463d1c-aec8-443d-b66e-fa5eadcccfa8
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: eb5f2d7b123a76942c7e4a84a7f475344fbcb144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connection-issues-tooazure-sql-database"></a>Risolvere i problemi di connessione tooAzure Database SQL
Quando hello connessione tooAzure Database SQL non riesce, viene visualizzato [messaggi di errore](sql-database-develop-error-messages.md). Questo articolo tratta un argomento centrale che aiuta l'utente a risolvere i problemi di connettività del database SQL di Azure. Introduce [hello le cause più comuni](#cause) dei problemi di connessione, si consiglia [uno strumento di risoluzione dei problemi](#try-the-troubleshooter-for-azure-sql-database-connectivity-issues) che consente di problema hello identità e fornisce la risoluzione dei problemi toosolve passaggi [ gli errori temporanei](#troubleshoot-transient-errors) e [errori persistenti o non temporaneo](#troubleshoot-persistent-errors). 

Se si verificano problemi di connessione hello, hello provare a risolvere i problemi relativi alla procedura descritta in questo articolo.
[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="cause"></a>Causa
Problemi di connessione possono essere causati da uno qualsiasi dei seguenti hello:

* Errore tooapply procedure consigliate e linee guida di progettazione durante il processo di progettazione dell'applicazione hello.  Vedere [Cenni preliminari sullo sviluppo di Database SQL](sql-database-develop-overview.md) tooget avviato.
* Riconfigurazione del database SQL di Azure
* Impostazioni del firewall
* Timeout della connessione
* Informazioni di accesso non corrette
* Raggiungimento del limite massimo su alcune risorse del database SQL di Azure

In genere, è possibile classificare tooAzure problemi di connessione del Database SQL come indicato di seguito:

* [Errori temporanei (di breve durata o intermittenti)](#troubleshoot-transient-errors)
* [Errori non temporanei o permanenti (gli errori che si ripetono regolarmente)](#troubleshoot-persistent-errors)

## <a name="try-hello-troubleshooter-for-azure-sql-database-connectivity-issues"></a>La risoluzione dei problemi di hello per problemi di connettività di Database SQL di Azure
Se si verifica un errore di connessione specifico, provare [questo strumento](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database)che consente di identificare rapidamente e risolvere il problema.

## <a name="troubleshoot-transient-errors"></a>Risolvere i problemi causati da errori temporanei

Quando un'applicazione si connette a database SQL di Azure tooan, viene visualizzato hello seguente messaggio di errore:

```
Error code 40613: "Database <x> on server <y> is not currently available. Please retry hello connection later. If hello problem persists, contact customer support, and provide them hello session tracing ID of <z>"
```

> [!NOTE]
> Questo messaggio di errore è in genere temporaneo.
> 
> 

Questo errore si verifica quando hello Azure database viene spostato (o riconfigurato) e l'applicazione perde il proprio database SQL toohello di connessione. La riconfigurazione del database SQL avviene in seguito a eventi pianificati, ad esempio nel caso degli aggiornamenti software, o non pianificati, ad esempio per l'arresto anomalo di un processo o il bilanciamento del carico. La maggior parte degli eventi di riconfigurazione è di breve durata e deve essere completata in meno di 60 secondi al massimo. Tuttavia, questi eventi possono talvolta richiedere toofinish più lungo, ad esempio quando una transazione di grandi dimensioni provoca un ripristino con esecuzione prolungata.

### <a name="steps-tooresolve-transient-connectivity-issues"></a>Problemi di connettività temporanei tooresolve di passaggi

1. Controllare hello [Dashboard del servizio di Microsoft Azure](https://azure.microsoft.com/status) per eventuali interruzioni del servizio noti che si è verificato durante la fase di hello durante cui hello sono stati segnalati errori da un'applicazione hello.
2. Applicazioni che si connettono servizio cloud tooa, ad esempio Database SQL di Azure deve prevedere gli eventi di riconfigurazione periodica e implementare ripetere logica toohandle questi errori anziché superfici queste informazioni come toousers errori dell'applicazione. Hello revisione [errori temporanei](sql-database-connectivity-issues.md) sezione hello procedure consigliate e linee guida alla progettazione [Cenni preliminari sullo sviluppo di Database SQL](sql-database-develop-overview.md) per ulteriori informazioni e generale ripetere strategie. Per informazioni dettagliate, vedere gli esempi di codice in: [Raccolte di connessioni per database SQL e Server SQL](sql-database-libraries.md) .
3. Quando un database si avvicina i limiti di risorse, può apparire toobe un problema di connettività temporaneo. Vedere la pagina relativa alla [risoluzione dei problemi di prestazioni](sql-database-troubleshoot-performance.md).
4. Se i problemi di connettività di continuare o se hello durata per cui l'applicazione rileva l'errore hello maggiore di 60 secondi o se vengono riscontrate più occorrenze dell'errore hello in un determinato giorno, file di una richiesta di supporto tecnico di Azure selezionando **ottenere supporto** su hello [supporto Azure](https://azure.microsoft.com/support/options) sito.

## <a name="troubleshoot-persistent-errors"></a>Risolvere gli errori persistenti
Se un'applicazione hello non riesce in modo permanente tooconnect tooAzure Database SQL, in genere indica un problema con uno dei seguenti hello:

* Configurazione del firewall. Hello Azure SQL database o sul lato client il firewall blocchi tooAzure connessioni Database SQL.
* Rete di riconfigurazione sul lato client hello: ad esempio, un nuovo indirizzo IP o un server proxy.
* Errore dell'utente: ad esempio, stato digitato correttamente i parametri di connessione, ad esempio nome del server nella stringa di connessione hello hello.

### <a name="steps-tooresolve-persistent-connectivity-issues"></a>Problemi di connettività permanente tooresolve di passaggi
1. Impostare [regole del firewall](sql-database-configure-firewall-settings.md) tooallow indirizzo IP del client hello. Per temporaneo a scopo di test, impostare una regola del firewall utilizzando 0.0.0.0 come hello inizio intervallo di indirizzi IP e l'utilizzo di 255.255.255.255 come hello fine intervallo di indirizzi IP. Verrà aperta hello tooall gli indirizzi IP. Se questo risolve il problema di connettività, rimuovere la regola e creare una regola del firewall per un indirizzo o un intervallo di indirizzi IP adeguatamente limitato. 
2. In tutti i firewall tra il client di hello e hello Internet, assicurarsi che la porta 1433 è aperta per le connessioni in uscita. Revisione [configurare Windows Firewall di hello tooAllow accesso a SQL Server](https://msdn.microsoft.com/library/cc646023.aspx) e [protocolli e le porte richieste identità ibrida](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports) per puntatori aggiuntivi correlati tooadditional porte che è necessario tooopen per Autenticazione di Azure Active Directory.
3. Verificare la stringa di connessione e le altre impostazioni di connessione. Vedere la sezione stringa di connessione in hello hello [argomento problemi di connettività](sql-database-connectivity-issues.md#connections-to-azure-sql-database).
4. Controllare l'integrità del servizio nel dashboard di hello. Se si ritiene che si verifica un'interruzione internazionale, vedere [recuperare da un'interruzione](sql-database-disaster-recovery.md) per una nuova area tooa toorecover passaggi.

## <a name="next-steps"></a>Passaggi successivi
* [Risoluzione dei problemi di prestazioni del database SQL di Azure](sql-database-troubleshoot-performance.md)
* [Ricerca di documentazione hello in Microsoft Azure](http://azure.microsoft.com/search/documentation/)
* [Hello vista ultimi aggiornamenti del servizio di Database SQL di Azure toohello](http://azure.microsoft.com/updates/?service=sql-database)

## <a name="additional-resources"></a>Risorse aggiuntive
* [Panoramica dello sviluppo di database SQL](sql-database-develop-overview.md)
* [Linee guida generali per la gestione degli errori temporanei](../best-practices-retry-general.md)
* [Raccolte di connessioni per database SQL e Server SQL](sql-database-libraries.md)

