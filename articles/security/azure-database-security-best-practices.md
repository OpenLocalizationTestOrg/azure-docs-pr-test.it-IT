---
title: procedure ottimali di protezione database aaaAzure | Documenti Microsoft
description: Questo articolo fornisce un set di procedure consigliate per la sicurezza del database di Azure.
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
ms.date: 07/21/2017
ms.author: tomsh
ms.openlocfilehash: 78984291e8f74879c7f738e2ce3176c4be18d154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-best-practices"></a>Procedure consigliate per la sicurezza del database di Azure

La sicurezza è un tema della massima importanza per la gestione dei database ed è sempre stata una priorità per il database SQL di Azure. I database possono essere molto protetto toohelp soddisfare più normativi o i requisiti di sicurezza, inclusi HIPAA e ISO 27001/27002 PCI DSS livello 1, tra gli altri. Un elenco corrente di certificazioni di conformità di sicurezza è disponibile all'indirizzo hello [sito Microsoft Trust Center](http://azure.microsoft.com/support/trust-center/services/). È anche possibile scegliere tooplace i database nel Data Center di Azure specifico in base ai requisiti normativi.

In questo articolo verrà illustrato un insieme di procedure consigliate per la sicurezza del database di Azure, Queste procedure consigliate derivano dall'esperienza acquisita con la protezione del database di Azure e l'esperienza dei clienti hello come manualmente.

Per ogni procedura consigliata verrà illustrato:

-   Quali consigliabile hello
-   Motivo per cui si desidera tooenable consigliata
-   Se non è consigliata di hello tooenable, quale potrebbe essere il risultato di hello
-   Informazioni come procedura consigliata hello tooenable

Questo articolo di procedure ottimali di protezione del Database Azure si basa su un parere di consenso e funzionalità della piattaforma Azure e set di funzionalità in cui si trovano in fase di hello in questo articolo è stato scritto. Opinioni e le tecnologie cambiano nel tempo e questo articolo verrà aggiornato in un tooreflect regolarmente le modifiche.

Le procedure consigliate per la sicurezza del database di Azure discusse in questo articolo includono:

-   Usare l'accesso al database toorestrict regole firewall
-   Abilitare l'autenticazione del database
-   Proteggere i dati con la crittografia
-   Proteggere i dati in transito
-   Abilitare il controllo del database
-   Abilitare il rilevamento delle minacce per il database


## <a name="use-firewall-rules-toorestrict-database-access"></a>Usare l'accesso al database toorestrict regole firewall

Il database SQL di Microsoft Azure fornisce un servizio di database relazionale per Azure e altre applicazioni basate su Internet. sicurezza dall'accesso di tooprovide, Database SQL controlla l'accesso con le regole firewall limitando la connettività utilizzando un indirizzo IP, i meccanismi di autenticazione che richiede agli utenti tooprove loro identità e meccanismi di autorizzazione, limitando gli utenti toospecific azioni e i dati. I firewall impediscono tutti i server di database di access tooyour finché non si specifica quali computer dispongono di autorizzazioni. firewall Hello concede accesso toodatabases in base a hello provenienti dall'indirizzo IP di ogni richiesta.

![Regole del firewall](./media/azure-database-security-best-practices/azure-database-security-best-practices-Fig1.png)

Hello servizio Database SQL di Azure è disponibile solo tramite la porta TCP 1433. tooaccess un Database SQL da questo computer, verificare che il firewall del computer client consenta la comunicazione TCP in uscita sulla porta TCP 1433. Se non sono necessarie per altre applicazioni, bloccare le connessioni in ingresso sulla porta TCP 1433 usando le regole del firewall.

Come parte del processo di connessione hello, le connessioni da macchine virtuali di Azure vengono reindirizzate tooa diverso indirizzo IP e la porta, univoca per ogni ruolo di lavoro. numero di porta Hello è compreso nell'intervallo di hello da too11999 11000. Per altre informazioni sulle porte TCP, vedere [Porte superiori a 1433 per ADO.NET 4.5 e il database SQL](https://docs.microsoft.com/azure/sql-database/sql-database-develop-direct-route-ports-adonet-v12).

> [!Note]
> Per informazioni generali sulle regole del firewall, vedere l'articolo relativo alle [regole del firewall per il database SQL](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

## <a name="enable-database-authentication"></a>Abilitare l'autenticazione del database
Il database SQL supporta due tipi di autenticazione: l'autenticazione SQL e l'autenticazione di Azure Active Directory (Azure AD).

L'**autenticazione SQL** è consigliata nei casi seguenti:

-   Consente gli ambienti toosupport SQL Azure con sistemi operativi misti, in cui tutti gli utenti non sono autenticati da un dominio Windows.
-   Consente di toosupport applicazioni precedenti a SQL Azure e alle applicazioni di terze parti che richiedono l'autenticazione di SQL Server.
-   Consente agli utenti tooconnect da domini sconosciuti o non attendibili. Ad esempio, un'applicazione in cui clienti specifici si connettono con assegnati gli account di accesso di SQL Server stato hello tooreceive dei loro ordini.
-   Consente a SQL Azure toosupport applicazioni basate sul Web in cui gli utenti creano le proprie identità.
-   Software consente agli sviluppatori toodistribute in base alle applicazioni tramite una gerarchia di autorizzazioni complessa noto, predefinito degli account di accesso di SQL Server.

> [!Note]
> Tuttavia, l'autenticazione di SQL Server non può usare il protocollo di sicurezza Kerberos.

Se si usa l'**autenticazione di SQL** è necessario:

-   Gestire le credenziali sicuro hello.
-   Proteggere le credenziali di hello nella stringa di connessione hello.
-   (Potenzialmente) proteggere le credenziali di hello trasmesse in rete hello dal hello Web toohello database del server. Per ulteriori informazioni vedere [procedura: connettersi tooSQL Server utilizzando l'autenticazione di SQL in ASP.NET 2.0](https://msdn.microsoft.com/library/ms998300.aspx).

**L'autenticazione di Azure Active Directory** è un meccanismo di connessione di Database SQL di Azure tooMicrosoft e [SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is) usando le identità in Azure Active Directory (Azure AD). Con l'autenticazione di Azure AD, è possibile gestire centralmente le identità hello di utenti del database e altri servizi Microsoft in un'unica posizione centrale. Gestione centrale di ID fornisce un'unica posizione toomanage gli utenti del database e semplifica la gestione delle autorizzazioni. Esempio hello vantaggi:

-   Fornisce l'autenticazione Server tooSQL alternativo.
-   Consente di arrestare la proliferazione di hello delle identità tra server di database.
-   Consente la rotazione delle password in un'unica posizione.
-   I clienti possono gestire le autorizzazioni del database tramite gruppi (AAD) esterni.
-   Può eliminare l'archiviazione delle password abilitando l'autenticazione integrata di Windows e altre forme di autenticazione supportate da Azure Active Directory.
-   Autenticazione di Azure AD Usa identità tooauthenticate utenti di database indipendente a livello di database hello.
-   Azure AD supporta l'autenticazione basata su token per applicazioni che si connettono tooSQL Database.
-   L'autenticazione di Azure AD supporta la federazione dei domini di AD FS o l'autenticazione utente/password nativa per un'istanza locale di Azure Active Directory senza la sincronizzazione del dominio.
-   Azure AD supporta le connessioni da SQL Server Management Studio che utilizzano l'autenticazione universale di Active Directory, che include l'MFA (Multi-Factor Authentication). L'MFA include funzionalità avanzate di autenticazione con una serie di semplici opzioni di verifica, tra cui: chiamata telefonica, SMS, smart card con pin o notifica tramite app per dispositivi mobili. Per altre informazioni [Supporto di SQL Server Management Studio (SSMS) per l'autenticazione MFA di Azure AD con il database SQL e SQL Data Warehouse](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).

passaggi di configurazione Hello includono hello seguendo procedure tooconfigure e utilizzano l'autenticazione di Azure Active Directory.

-   Creare e popolare un'istanza di Azure AD.
-   Facoltativo: Associare o modificare hello active directory a cui è attualmente associato alla sottoscrizione di Azure.
-   Creare un amministratore di Azure Active Directory per il server di Azure SQL o per [Azure SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/).
- Configurare i computer client.
-   Creare utenti del database indipendente in tooAzure del database eseguito il mapping delle identità di Active Directory.
-   Connessione database tooyour usando le identità di Azure AD.

Informazioni dettagliate sono disponibili [qui](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).

## <a name="protect-your-data-using-encryption"></a>Proteggere i dati con la crittografia

[Crittografia trasparente dei dati del Database di SQL Azure (TDE)](https://msdn.microsoft.com/library/dn948096.aspx) consente la protezione da minacce hello di attività dannose eseguendo la crittografia in tempo reale e la decrittografia di hello database, i backup associati, e i file di log delle transazioni a riposo senza richiesta di modifiche toohello applicazione. Transparent Data Encryption crittografa l'archivio di hello di un intero database utilizzando una chiave di crittografia simmetrica hello chiamata chiave database.

Anche se archiviazione intera hello è crittografato, è molto importante tooalso crittografare il database stesso. Questa è un'implementazione di difesa hello approccio per la protezione dati. Se si utilizza Database SQL di Azure e si desiderano tooprotect dati sensibili, ad esempio carta di credito o numeri di previdenza sociale, è possibile crittografare un database con la crittografia AES a 256 bit di 140-2 convalidato FIPS che soddisfi i requisiti di hello molti standard di settore (ad esempio HIPAA, PCI).

È importante toounderstand che i file correlati troppo[buffer pool estensione](https://docs.microsoft.com/sql/database-engine/configure-windows/buffer-pool-extension) non vengono crittografati quando un database viene crittografato con TDE. È necessario utilizzare strumenti di crittografia a livello di file system come [BitLocker](https://technet.microsoft.com/library/cc732774) o hello [Encrypting File System (EFS)](https://technet.microsoft.com/library/cc700811.aspx) per tali file correlati.

Poiché un utente autorizzato, ad esempio un amministratore della sicurezza o un amministratore del database può accedere ai dati hello anche se il database di hello è crittografato con TDE, è necessario seguire anche indicazioni hello riportate di seguito:

-   Abilitare l'autenticazione di SQL a livello di database hello.
-   Usare l'autenticazione di Azure AD con i ruoli di [Controllo degli accessi in base al ruolo](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is).
-   Gli utenti e applicazioni devono usare tooauthenticate account distinti. In questo modo è possibile limitare le autorizzazioni di hello concesso toousers e le applicazioni e ridurre i rischi di hello di attività dannose.
-   Implementare di sicurezza a livello di database tramite i ruoli predefiniti del database (ad esempio db_datareader o db_datawriter) oppure è possibile creare ruoli personalizzati per l'applicazione di toogrant gli oggetti di database tooselected autorizzazioni esplicite.

Per altri modi tooencrypt dei dati, prendere in considerazione:

-   [Crittografia a livello di cella](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt colonne specifiche o anche le celle di dati con le chiavi di crittografia diversi.
-   La crittografia in uso con Always Encrypted: [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx) consente ai client tooencrypt i dati sensibili all'interno delle applicazioni client e non rivelano toohello le chiavi di crittografia hello motore di Database (Database SQL o SQL Server). Di conseguenza, crittografia sempre attiva crea una separazione tra chi possiede i dati di hello (e può visualizzarli) e chi gestisce i dati hello (ma non può accedervi).
-   Utilizzo della sicurezza a livello di riga: sicurezza a livello di riga consente ai clienti toocontrol accesso toorows in una tabella di database in base alle caratteristiche di hello dell'utente hello esegue una query (ad esempio, gruppo appartenenza o l'esecuzione del contesto). Per altre informazioni, vedere [Sicurezza a livello di riga](https://msdn.microsoft.com/library/dn765131).

## <a name="protect-data-in-transit"></a>Proteggere i dati in transito
La protezione dei dati in transito deve essere una parte essenziale della strategia di protezione dati. Poiché i dati verranno spostate avanti e indietro da molte posizioni, hello generale si consiglia di utilizzare sempre dati tooexchange di protocolli SSL/TLS in posizioni diverse. In alcuni casi, è opportuno canale di comunicazione intera hello tooisolate tra le sedi locali e cloud dell'infrastruttura tramite una rete privata virtuale (VPN).

Per lo spostamento dei dati tra l'infrastruttura locale e Azure, è opportuno considerare le misure di protezione appropriate, ad esempio HTTPS o VPN.

Per le organizzazioni che richiedono l'accesso toosecure da più workstation in locale tooAzure, [Azure VPN site-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-site-to-site-create).

Per le organizzazioni che devono toosecure accesso dalle singole workstation si trova in locale o tooAzure fuori sede, è consigliabile usare [Point-to-Site VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-point-to-site-create).

Set di dati più grandi possono essere spostati su un collegamento WAN ad alta velocità dedicato, ad esempio [ExpressRoute](https://azure.microsoft.com/services/expressroute/). Se si sceglie toouse ExpressRoute, è anche possibile crittografare i dati hello hello a livello di applicazione utilizzando [SSL/TLS](https://support.microsoft.com/kb/257591) o altri protocolli per una maggiore protezione.

Se si interagisce con l'archiviazione di Azure tramite il portale di Azure hello, tutte le transazioni si verificano tramite HTTPS. [API REST di archiviazione](https://msdn.microsoft.com/library/azure/dd179355.aspx) tramite HTTPS può anche essere utilizzati toointeract con [di archiviazione di Azure](https://azure.microsoft.com/services/storage/) e [Database SQL di Azure](https://azure.microsoft.com/services/sql-database/).

Le organizzazioni che non soddisfano tooprotect dati in transito sono più sensibili per [attacchi man-in-the-middle](https://technet.microsoft.com/library/gg195821.aspx), [intercettazione](https://technet.microsoft.com/library/gg195641.aspx) e Hijack della sessione. Questi attacchi possono essere hello innanzitutto ottenere l'accesso ai dati tooconfidential.

altre informazioni sull'opzione VPN di Azure leggendo l'articolo hello toolearn [pianificazione e progettazione per il Gateway VPN](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-plan-design).

## <a name="enable-database-auditing"></a>Abilitare il controllo del database
Il controllo di un'istanza del motore di Database di SQL Server hello o un singolo database comporta il rilevamento e registrazione di eventi che si verificano nel motore di Database hello. SQL Server Audit consente di creare controlli del server che possono contenere specifiche di controllo del server per gli eventi a livello di server e specifiche di controllo del database per gli eventi a livello di database. Gli eventi controllati possono essere scritti i registri eventi toohello o tooaudit file.

Esistono numerosi livelli di controllo per SQL Server, in base ai requisiti legislativi o standard per l'installazione. SQL Server Audit fornisce strumenti hello e i processi necessari tooenable, archiviazione e visualizzazione controlli in vari oggetti server e database.

[Controllo del Database SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-auditing) tiene traccia degli eventi di database e li scrive i log di controllo tooan nell'account di archiviazione di Azure.

Il controllo consente di agevolare la conformità alle normative, comprendere le attività del database e ottenere informazioni su eventuali discrepanze e anomalie che potrebbero indicare problemi aziendali o sospette violazioni della sicurezza.

Il controllo Abilita e facilita norme toocompliance la conformità ma non garantisce la conformità.

toolearn informazioni sul controllo del database e come tooenable, leggere hello articolo [attivare il rilevamento di minaccia e di controllo nei computer SQL Server nel Centro protezione Azure](https://docs.microsoft.com/azure/security-center/security-center-enable-auditing-on-sql-servers).

## <a name="enable-database-threat-detection"></a>Abilitare il rilevamento delle minacce per il database
Rilevamento minacce SQL permette toodetect e rispondere toopotential minacce che si verificano fornendo gli avvisi di sicurezza sull'attività anomale. È possibile ricevere un avviso in caso di attività di database sospetta, potenziali vulnerabilità e attacchi SQL injection, nonché in caso di modelli di accesso ai database anomali. Avvisi di rilevamento minacce SQL forniscono i dettagli dell'attività sospette e consigliabile azione sulla tooinvestigate e ridurre il rischio di hello.

Ad esempio attacchi SQL injection è uno dei hello Web sicurezza problemi delle applicazioni su Internet, le applicazioni utilizzate tooattack basati sui dati hello. Gli utenti malintenzionati sfruttano applicazione vulnerabilità tooinject dannoso istruzioni SQL in campi di ingresso dell'applicazione, sono state violate oppure la modifica dei dati nel database di hello.

toolearn sulla tooset di rilevamento minacce del database in Azure, vedere portale hello [rilevamento minacce del Database SQL](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).

Gli avvisi per il rilevamento delle minacce di SQL sono integrati con il [Centro sicurezza di Azure](https://azure.microsoft.com/services/security-center/). Invitare tootry impostarlo per 60 giorni per liberare.

toolearn informazioni sul rilevamento minacce del Database e come tooenable, leggere hello articolo [attivare il rilevamento di minaccia e di controllo nei computer SQL Server nel Centro protezione Azure](https://docs.microsoft.com/azure/security-center/security-center-enable-auditing-on-sql-servers).

## <a name="conclusion"></a>Conclusioni
Il database di Azure è una piattaforma di database affidabile, con una gamma completa di funzionalità di sicurezza che soddisfano molti requisiti normativi e aziendali. È possibile proteggere dati, in quanto il controllo hello accesso fisico tooyour dati utilizzando un'ampia gamma di opzioni per la protezione dei dati in file hello-, colonna o a livello di riga con Transparent Data Encryption, la crittografia a livello di cella o sicurezza a livello di riga. Always Encrypted consente inoltre operazioni sui dati crittografati, semplificando il processo di hello di aggiornamenti dell'applicazione. A sua volta, i registri di accesso tooauditing dell'attività del Database SQL vengono fornite informazioni hello necessarie, consentendo tooknow come e quando si accede ai dati.

## <a name="next-steps"></a>Passaggi successivi
- toolearn più sulle regole del firewall, vedere [regole del Firewall](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).
- toolearn sugli utenti e account di accesso, vedere [gestire gli account di accesso](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins).
- Per un'esercitazione, vedere [Proteggere il database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial).
