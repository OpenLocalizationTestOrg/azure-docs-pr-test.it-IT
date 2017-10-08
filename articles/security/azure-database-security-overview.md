---
title: Panoramica della sicurezza database aaaAzure | Documenti Microsoft
description: "In questo articolo viene fornita una panoramica delle funzionalità di sicurezza di Azure database hello."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: TomSh
ms.openlocfilehash: 13f14b99d15800e85e9906a9d167eb0adf2135de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-overview"></a>Panoramica della sicurezza del database di Azure

La sicurezza è un tema della massima importanza per la gestione dei database ed è sempre stata una priorità per il database SQL di Azure. Il database SQL di Azure supporta la sicurezza della connessione con regole del firewall e crittografia delle connessioni. Supporta anche l'autenticazione con nome utente e password e l'autenticazione di Azure Active Directory, che usa identità gestite da Azure Active Directory. Per l'autorizzazione viene usato il controllo degli accessi in base al ruolo.

Database SQL di Azure supporta la crittografia eseguendo la crittografia in tempo reale e la decrittografia del database, i backup associati e i file di log delle transazioni a riposo senza richiedere modifiche toohello applicazione.

Microsoft offre ulteriori metodi tooencrypt i dati aziendali:

-   A livello di cella colonne specifiche di crittografia tooencrypt o anche le celle di dati con le chiavi di crittografia diversi.
-   Se è necessario un modulo di sicurezza hardware o la gestione centralizzata della gerarchia di chiavi di crittografia, prendere in considerazione l'uso di Azure Key Vault con SQL Server in una macchina virtuale di Azure.
-   Sempre crittografato (attualmente in anteprima) consente la crittografia trasparente tooapplications e consente ai client tooencrypt dati sensibili all'interno delle applicazioni client senza condividere le chiavi di crittografia hello con il Database SQL.

Controllo del Database SQL Azure consente alle aziende toorecord eventi tooan controllo accesso di archiviazione di Azure. Controllo del Database SQL si integra inoltre con analisi e report drill-down toofacilitate di Microsoft Power BI.

 Database di SQL Azure possono essere molto protetto toosatisfy più normativi o i requisiti di sicurezza, inclusi HIPAA e ISO 27001/27002 PCI DSS livello 1, tra gli altri. Un elenco corrente di certificazioni di conformità di sicurezza è disponibile all'indirizzo hello [sito Microsoft Azure Trust Center](http://azure.microsoft.com/support/trust-center/services/).

In questo articolo vengono illustrati concetti di base di hello di protezione del database SQL di Microsoft Azure strutturata, tabulare e dati relazionali. In particolare, questo articolo consente di iniziare a usare le risorse per la protezione dei dati, il controllo dell'accesso e il monitoraggio proattivo.

Cenni preliminari sulla sicurezza Database di Azure viene descritta la hello seguenti aree:

-   Proteggere i dati
-   Controllo di accesso
-   Monitoraggio proattivo
-   Gestione centralizzata della sicurezza
-   Azure Marketplace

## <a name="protect-data"></a>Proteggere i dati

Il database SQL protegge i dati in movimento con [Transport Layer Security](https://support.microsoft.com/kb/3135244) (TLS), i dati inattivi con [Transparent Data Encryption](http://go.microsoft.com/fwlink/?LinkId=526242) (TDE) e i dati in uso con [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx).

Argomenti trattati in questa sezione:

-   Crittografia di dati in movimento
-   Crittografia di dati inattivi
-   Crittografia di dati in uso (client)

Per altri modi tooencrypt dei dati, prendere in considerazione:

-   [Crittografia a livello di cella](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt colonne specifiche o anche le celle di dati con le chiavi di crittografia diversi.
-   Se è necessario un modulo di sicurezza Hardware o la gestione centralizzata della gerarchia di chiavi di crittografia, è consigliabile utilizzare l' [insieme di credenziali chiave di Azure con SQL Server in una relativa macchina virtuale](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx).

### <a name="encryption-in-motion"></a>Crittografia di dati in movimento

Un problema comune per tutte le applicazioni client/server è necessario hello privacy durante lo spostamento dei dati su reti pubbliche e private. Se i dati trasferiti in rete non è crittografati, è hello ritenere che possono essere acquisito e furto da parte di utenti non autorizzati. Quando si gestiscono i servizi di database, è necessario assicurarsi che i dati vengono crittografati tra hello database client e server, nonché tra server di database che comunicano tra loro e con applicazioni di livello intermedio toomake.

Un problema quando si amministra una rete riguarda la protezione dei dati inviati tra le applicazioni in una rete non attendibile. È possibile utilizzare [TLS/SSL](https://docs.microsoft.com/windows-server/security/tls/transport-layer-security-protocol) tooauthenticate server e client e usare quindi i messaggi di tooencrypt tra entità hello autenticato.

Nel processo di autenticazione hello, un client TLS/SSL invia un server TLS/SSL tooa e hello server risponde con le informazioni di hello tooauthenticate stesso è necessario che tale server hello. Server e client hello eseguire un ulteriore scambio di chiavi di sessione e hello termina di finestra di dialogo di autenticazione. Al termine dell'autenticazione, può iniziare la comunicazione protetta con SSL tra hello server e client di hello con chiavi di crittografia simmetrica hello stabilite durante il processo di autenticazione hello.

Tutte le connessioni tooAzure Database di SQL richiedono una crittografia SSL/TLS () tutti gli orari mentre i dati sono "in transito" tooand dal database hello. SQL Azure Usa i client e server tooauthenticate TLS/SSL e usare quindi i messaggi di tooencrypt tra entità hello autenticato. Nella stringa di connessione dell'applicazione, è necessario specificare una connessione hello tooencrypt di parametri e non tootrust hello certificato del server (eseguita automaticamente se si copia la stringa di connessione hello portale classico di Azure), in caso contrario hello connessione verrà Verifica identità hello del server hello e saranno soggetti attacchi troppo "man-in-the-middle". Per hello driver ADO.NET, ad esempio, questi parametri di stringa di connessione Encrypt = True e TrustServerCertificate = False.

### <a name="encryption-at-rest"></a>Crittografia di dati inattivi
È possibile adottare diversi database di precauzioni toohelp hello protetto, ad esempio la progettazione di un sistema sicuro, la crittografia dei dati riservati e la creazione di un firewall attorno hello database server. Tuttavia, in uno scenario in cui vengono rubati supporti fisici di hello (ad esempio unità o nastri di backup), un malintenzionato possibile solo ripristinare o collegare database hello ed esplorare i dati di hello.

Una soluzione tooencrypt hello contiene dati sensibili nel database di hello e protegge le chiavi di hello che vengono utilizzati tooencrypt hello dati con un certificato. Ciò impedisce chi è sprovvisto delle chiavi di hello utilizzando i dati di hello, ma questo tipo di protezione deve essere pianificato.

Questo problema, SQL Server e SQL Azure supporta toosolve [Transparent Data Encryption (TDE)](https://docs.microsoft.com/sql/relational-databases/securityrecryption/transparent-data-encryption-tde). TDE crittografa i file di dati di SQL Server e del database SQL di Azure, noti come dati di crittografia inattivi.

Crittografia trasparente dei dati di Database SQL Azure contribuisce alla protezione dalle minacce di hello di attività dannose eseguendo la crittografia in tempo reale e la decrittografia del database hello, i backup associati e i file di log delle transazioni a riposo senza richiedere modifiche applicazione toohello.  

Transparent Data Encryption crittografa l'archivio di hello di un intero database utilizzando una chiave di crittografia simmetrica hello chiamata chiave database. Nel Database SQL, chiave di crittografia del database hello è protetto da un certificato server predefinito. certificato server predefinito Hello è univoco per ogni server di Database SQL.

Se un database partecipa a una relazione GeoDR, è protetto da una chiave diversa in ogni server. Se due database sono connesso toohello nello stesso server, condividono hello stesso certificato predefinito. Microsoft ruota automaticamente questi certificati almeno ogni 90 giorni. Per una descrizione generale della funzionalità TDE, vedere [Transparent Data Encryption (TDE)](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde).

### <a name="encryption-in-use-client"></a>Crittografia di dati in uso (client)

La maggior parte delle violazioni di dati comportano il furto di hello di dati critici, ad esempio numeri di carta di credito o informazioni personali. I database possono essere veri e propri forzieri di informazioni sensibili e contenere dati personali dei clienti, informazioni riservate sulla concorrenza e dati di proprietà intellettuale. I dati persi o rubati, in particolare i dati dei clienti, possono causare danni di immagine, svantaggi competitivi, sanzioni e persino problemi legali.

![Always Encrypted](./media/azure-databse-security-overview/azure-database-fig1.png)

[Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx) è un funzionalità progettata tooprotect dati sensibili, ad esempio numeri di carta di credito o numeri di identificazione nazionali (ad esempio, Usa numeri di previdenza sociale), archiviati in Database SQL di Azure o SQL Server database. Always Encrypted consente ai client tooencrypt dati sensibili all'interno delle applicazioni client senza mai rivelare toohello le chiavi di crittografia hello motore di Database (Database SQL o SQL Server).

Always Encrypted fornisce una separazione tra chi possiede i dati di hello (e può visualizzarli) e chi gestisce i dati hello (ma non può accedervi). Per garantire agli amministratori di database locali, operatori di database cloud o altri con privilegi elevati, ma gli utenti non autorizzati, non è possibile accedere ai dati crittografato hello,

Inoltre, crittografia sempre attiva rende tooapplications trasparente la crittografia. Un driver abilitato Always Encrypted installato nel computer client hello in modo che è possibile crittografare e decrittografare dati sensibili nell'applicazione client hello automaticamente. driver Hello crittografa i dati di hello in colonne sensibili prima di passare i dati di hello toohello motore di Database e riscrive automaticamente le query in modo che un'applicazione hello semantica toohello vengono mantenute. Analogamente, driver hello decrittografa in modo trasparente i dati, archiviati in colonne di database crittografato, contenuti nei risultati della query.

## <a name="access-control"></a>Controllo di accesso
sicurezza tooprovide, Database SQL controlla l'accesso con la limitazione di connettività utilizzando un indirizzo IP, i meccanismi di autenticazione che richiede agli utenti tooprove regole del firewall, identità e meccanismi di autorizzazione, limitando gli utenti toospecific azioni e i dati.

### <a name="database-access"></a>Accesso al database

Protezione dei dati inizia con il controllo di accesso ai dati tooyour. Data Center Hello che ospita i dati gestisce l'accesso fisico, sebbene sia possibile configurare una firewall toomanage protezione a livello di rete hello. È anche possibile controllare l'accesso configurando gli account di accesso per l'autenticazione e definendo le autorizzazioni per i ruoli del server e del database.

Argomenti trattati in questa sezione:

-   Firewall e regole del firewall
-   Autenticazione
-   Authorization

#### <a name="firewall-and-firewall-rules"></a>Firewall e regole del firewall

Il database SQL di Microsoft Azure fornisce un servizio di database relazionale per Azure e altre applicazioni basate su Internet. toohelp proteggere i dati, i firewall impediscono tutti i server di database di access tooyour finché non si specifica quali computer dispongono di autorizzazioni. firewall Hello concede accesso toodatabases in base a hello provenienti dall'indirizzo IP di ogni richiesta. Per altre informazioni, vedere [Panoramica sulle regole del firewall per il database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

Hello [Database SQL di Azure](https://azure.microsoft.com/services/sql-database/) servizio è disponibile solo tramite la porta TCP 1433. tooaccess un Database SQL da questo computer, verificare che il firewall del computer client consenta la comunicazione TCP in uscita sulla porta TCP 1433. Se non sono necessarie per altre applicazioni, bloccare le connessioni in ingresso sulla porta TCP 1433.

#### <a name="authentication"></a>Autenticazione

L'autenticazione del database SQL si riferisce toohow dimostrare la propria identità durante la connessione di database toohello. Il database SQL supporta due tipi di autenticazione:

-   **L'autenticazione di SQL:** viene creato un account di accesso singolo quando viene creata un'istanza SQL logica, chiamato hello Account sottoscrittore del Database SQL. Tale account, che effettua la connessione con l'[autenticazione di SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview) (nome utente e password), Questo account è che un amministratore nell'istanza di server logico hello e in tutti i database utente collegato toothat istanza. le autorizzazioni di Hello di hello Account sottoscrittore non possono essere limitate. Può esistere un solo account di questo tipo.
-   **Azure Active Directory Authentication:** [l'autenticazione di Azure Active Directory](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication) è un meccanismo di connessione tooMicrosoft Database SQL di Azure e SQL Data Warehouse usando le identità in Azure Active Directory ( Azure AD). In questo modo si toocentrally gestire le identità di utenti del database.

![Autenticazione](./media/azure-databse-security-overview/azure-database-fig2.png)

 I vantaggi dell'autenticazione di Azure Active Directory includono:
  - Fornisce l'autenticazione Server tooSQL alternativo.
  - Consente di arrestare la proliferazione di hello delle identità tra server di database e consente la rotazione di password in un'unica posizione.
  - È possibile gestire le autorizzazioni del database tramite gruppi (Azure Active Directory) esterni.
  - Può eliminare l'archiviazione delle password abilitando l'autenticazione integrata di Windows e altre forme di autenticazione supportate da Azure Active Directory.

#### <a name="authorization"></a>Authorization
[Autorizzazione](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins) fa riferimento toowhat un utente può eseguire all'interno di un Database SQL di Azure e questa funzionalità è controllata dal database dell'account utente [le appartenenze ai ruoli](https://msdn.microsoft.com/library/ms189121) e [autorizzazioni a livello di oggetto](https://msdn.microsoft.com/library/ms191291.aspx). L'autorizzazione è il processo di hello per determinare le risorse di entità a protezione diretta di un'entità può accedere e quali operazioni sono consentite per le risorse.

### <a name="application-access"></a>Accesso all'applicazione

Argomenti trattati in questa sezione:

-   Maschera dati dinamica
-   Sicurezza a livello di riga

#### <a name="dynamic-data-masking"></a>Maschera dati dinamica
Un addetto al servizio a un call center può identificare i chiamanti da diverse cifre del numero di previdenza sociale o dal numero della carta di credito, ma tali dati, gli elementi non devono essere completamente visibili toohello rappresentante del servizio.

Può definire una regola di maschera che tutte le maschere ma hello ultime quattro cifre di qualsiasi numero di previdenza sociale o un numero di carta di credito nel set di risultati hello delle query.

![Maschera dati dinamica](./media/azure-databse-security-overview/azure-database-fig3.png)

Ad esempio, una maschera dati appropriata può essere definito tooprotect informazioni identificabili personalmente (PII) dati, uno sviluppatore può eseguire query su ambienti di produzione per la risoluzione dei problemi senza violare la regolamentazione di conformità.

[SQL Database maschera dati dinamica](https://docs.microsoft.com/azure/sql-database/sql-database-dynamic-data-masking-get-started) limita l'esposizione dei dati sensibili nascondendoli agli utenti con privilegi toonon. La maschera dati dinamica è supportata per la versione di hello V12 del Database SQL di Azure.

[La maschera dati dinamica](https://docs.microsoft.com/sql/relational-databases/security/dynamic-data-masking) impedisce che i dati di accesso non autorizzato toosensitive abilitando toodesignate la quantità di hello dati sensibili tooreveal con un impatto minimo sul livello di applicazione hello. È una funzionalità basata su criteri di sicurezza che consente di nascondere i dati sensibili hello nel set di risultati hello di una query su campi di database designati, senza dati hello hello database non viene modificati.


> [!Note]
> La maschera dati dinamica può essere configurata Database Azure salve, amministratore del server o ruoli di sicurezza responsabile della.

#### <a name="row-level-security"></a>Sicurezza a livello di riga
Un altro requisito di sicurezza comune per i database multi-tenant è la [sicurezza a livello di riga](https://msdn.microsoft.com/library/dn765131.aspx). Questa funzionalità consente di toocontrol accesso toorows in una tabella di database in base alle caratteristiche di hello dell'utente hello esegue una query (ad esempio, gruppo appartenenza o l'esecuzione del contesto).

![Sicurezza a livello di riga](./media/azure-databse-security-overview/azure-database-fig4.png)

logica di restrizione di accesso Hello si trova sul livello di database hello piuttosto che distante dai dati hello in un altro livello applicazione. sistema di database Hello applica restrizioni di accesso di hello ogni volta che viene eseguito un tentativo di accesso ai dati da qualsiasi livello. In questo modo il sistema di sicurezza più affidabile e solido grazie alla riduzione della superficie di attacco di hello del sistema di sicurezza.

La sicurezza a livello di riga introduce il controllo di accesso basato su predicato. Questa funzione offre una valutazione flessibile e centralizzata basata su predicato che può prendere in considerazione i metadati o altri criteri hello amministratore determina come appropriata. predicato Hello viene utilizzato come un criterio toodetermine hello utente dispone di dati di hello toohello accesso appropriato in base agli attributi utente o meno. Il controllo di accesso basato su etichetta può essere implementato usando il controllo di accesso basato su predicato.

## <a name="proactive-monitoring"></a>Monitoraggio proattivo
Il database SQL protegge i dati fornendo funzionalità di **controllo** e di **rilevamento delle minacce**.

### <a name="auditing"></a>Controllo
Controllo del Database SQL aumenta il possibilità toogain approfondite eventi e le modifiche che si verificano all'interno del database hello, inclusi gli aggiornamenti e le query sui dati hello.

[Controllo del Database SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-auditing-get-started) tiene traccia degli eventi di database e li scrive i log di controllo tooan nell'account di archiviazione di Azure. Il controllo consente di agevolare la conformità alle normative, comprendere le attività del database e ottenere informazioni su eventuali discrepanze e anomalie che potrebbero indicare problemi aziendali o sospette violazioni della sicurezza. Il controllo Abilita e facilita norme toocompliance la conformità ma non garantisce la conformità.

Il controllo del database SQL consente di:

-   **Conservare** un audit trail di eventi selezionati. È possibile definire le categorie di database azioni toobe controllato.
-   **Creare report** sulle attività del database. È possibile utilizzare i report preconfigurati e tooget un dashboard iniziare rapidamente con attività e la notifica degli eventi.
-   **Analizzare** i report. È possibile individuare eventi sospetti, attività insolite e tendenze.

Esistono due metodi di controllo:

-   **Il servizio controllo BLOB** -registri tooAzure nell'archiviazione Blob. Questo è un metodo di controllo più recente che fornisce prestazioni più elevate, supporta una maggiore granularità del controllo a livello di oggetto ed è più conveniente.
-   **Il controllo tabella** -registri tooAzure archiviazione tabella.

### <a name="threat-detection"></a>Introduzione al rilevamento delle minacce
La funzionalità di [rilevamento delle minacce del database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection) rileva attività sospette che indicano potenziali minacce alla sicurezza. Rilevamento minacce consente toorespond toosuspicious eventi nel database di hello, ad esempio attacchi injection SQL, che si verificano. Fornisce avvisi e consente l'utilizzo di hello di controllo del Database SQL Azure tooexplore eventi sospetti hello.

![Rilevamento delle minacce](./media/azure-databse-security-overview/azure-database-fig5.jpg)

Ad esempio attacchi SQL injection è uno dei hello Web sicurezza problemi delle applicazioni su Internet, le applicazioni utilizzate tooattack basati sui dati hello. Gli utenti malintenzionati sfruttano applicazione vulnerabilità tooinject dannoso istruzioni SQL in campi di ingresso dell'applicazione, sono state violate oppure la modifica dei dati nel database di hello.

I responsabili della sicurezza o altri amministratori designati possono ricevere una notifica immediata sulle attività di database sospette non appena si verificano. Ogni notifica fornisce i dettagli dell'attività sospette hello e suggerisce come toofurther analizzare e ridurre il rischio di hello.        

## <a name="centralized-security-management"></a>Gestione centralizzata della sicurezza

[Centro sicurezza di Azure](https://azure.microsoft.com/documentation/services/security-center/) consente di impedire, rilevare e rispondere toothreats. Offre funzionalità integrate di monitoraggio della sicurezza e gestione dei criteri tra le sottoscrizioni di Azure, facilita il rilevamento delle minacce che altrimenti passerebbero inosservate e funziona con un ampio ecosistema di soluzioni di sicurezza.

[Centro sicurezza PC](https://docs.microsoft.com/azure/security-center/security-center-sql-database) consente di conservare i dati nel Database SQL fornendo visibilità sicurezza hello del server e database. Con il Centro sicurezza è possibile:

-   Definire i criteri per la crittografia e il controllo del database SQL.
-   Monitoraggio della sicurezza hello di risorse del Database SQL per tutte le sottoscrizioni.
-   Identificare e correggere rapidamente i problemi di sicurezza.
-   Integrare gli avvisi generati dal [rilevamento delle minacce del database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).
-   Il Centro sicurezza supporta l'accesso in base al ruolo.

## <a name="azure-marketplace"></a>Azure Marketplace

Hello Azure Marketplace è un marketplace di applicazioni e servizi online che consente di Start-up e software indipendenti (ISV) di fornitori toooffer clientela soluzioni tooAzure tutto il mondo hello.
Hello Azure Marketplace combina ecosistemi di partner di Microsoft Azure in un'unica piattaforma di toobetter serve i clienti e partner. Fare clic su [qui](https://azuremarketplace.microsoft.com/marketplace/apps?search=Database%20Security&page=1) tooglance prodotti sicurezza del database disponibili sul mercato Azure.

## <a name="next-steps"></a>Passaggi successivi

- Altre informazioni sulla [protezione del database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial).
- Altre informazioni sul [Centro sicurezza di Azure e il servizio database SQL di Azure](https://docs.microsoft.com/azure/security-center/security-center-sql-database).
- toolearn ulteriori informazioni su funzionalità di rilevamento minacce, vedere [rilevamento minacce del Database SQL](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).
- vedere, più toolearn [prestazioni del database SQL migliorare](https://docs.microsoft.com/azure/sql-database/sql-database-performance-tutorial). 
