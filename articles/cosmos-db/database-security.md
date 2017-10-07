---
title: sicurezza aaaDatabase - DB Cosmos Azure | Documenti Microsoft
description: Informazioni su come Azure Cosmos DB garantisca la protezione del database e la sicurezza dei dati.
keywords: sicurezza del database NoSQL, sicurezza delle informazioni, sicurezza dei dati, crittografia del database, protezione del database, criteri di sicurezza, test di sicurezza
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: a02a6a82-3baf-405c-9355-7a00aaa1a816
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: mimig
ms.openlocfilehash: 85ffa62f611bfad00bf3fc5dbe536f91f97f1113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-database-security"></a>Sicurezza database di Azure Cosmos DB

In questo articolo vengono illustrate procedure ottimali di protezione del database e le funzionalità principali offerte da Azure Cosmos DB toohelp impedire, rilevare e rispondere toodatabase violazioni.
 
## <a name="whats-new-in-azure-cosmos-db-security"></a>Novità della sicurezza di Azure Cosmos DB

La crittografia dei dati inattivi è ora disponibile per i documenti e i backup archiviati nel database Azure Cosmos in tutte le aree di Azure. La crittografia di dati inattivi viene applicata automaticamente sai per i clienti nuovi che per quelli esistenti in queste aree. Non tooconfigure necessario non è un valore specifico. e ottenere hello latenza grande stesso, velocità effettiva, disponibilità e funzionalità, come prima con il vantaggio di hello di conoscere i dati sono sicuro e protetto con crittografia inattivi.

## <a name="how-do-i-secure-my-database"></a>Come proteggere il database 

Protezione dei dati è una responsabilità condivisa tra, cliente hello e il provider di database. Provider di database hello che prescelto, a seconda della quantità di hello di responsabilità di eseguire può variare. Se si sceglie una soluzione locale, è necessario tooprovide tutti i dati da endpoint protection toophysical sicurezza hardware - Nessuna attività semplice. Se si sceglie un provider di database cloud PaaS, ad esempio Azure Cosmos DB, l'ambito di interesse si riduce considerevolmente. Hello seguente immagine, presa in prestito da Microsoft [responsabilità condivisa per il Cloud Computing](https://aka.ms/sharedresponsibility) white paper viene illustrato come le responsabilità del programmatore diminuisce con un provider di PaaS come Azure Cosmos DB.

![Responsabilità del provider di database e del cliente](./media/database-security/nosql-database-security-responsibilities.png)

Hello precedente diagramma Mostra componenti di protezione cloud di alto livello, ma gli elementi è necessario tooworry su in modo specifico per la soluzione di database? E come è possibile confrontare le soluzioni tooeach altri? 

È consigliabile seguire l'elenco di controllo dei requisiti di quali sistemi di database toocompare hello:

- Sicurezza di rete e impostazioni del firewall
- Autenticazione utente e controlli utente con granularità fine
- Dati tooreplicate possibilità a livello globale per gli errori locali
- Capacità tooperform failover da un data center tooanother
- Replica di dati locali all'interno di un data center
- Backup automatici dei dati
- Ripristino dei dati eliminati dai backup
- Proteggere e isolare i dati sensibili
- Monitoraggio per identificare gli attacchi
- Risponde tooattacks
- Capacità toogeo limite tooadhere toodata governance le restrizioni sui dati
- Protezione fisica dei server in data center protetti

E anche se potrebbe sembrare ovvio, recenti [violazioni di database su larga scala](http://thehackernews.com/2017/01/mongodb-database-security.html) ci ricordare di importanza di semplice ma critici hello di hello seguenti requisiti:
- Server con patch che vengono mantenuti i toodate
- Crittografia SSL/HTTPS predefinita
- Account amministrativi con password complesse

## <a name="how-does-azure-cosmos-db-secure-my-database"></a>Protezione del database con Azure Cosmos DB

Diamo un'occhiata nuovamente hello elenco precedente, il numero di tali requisiti di sicurezza DB Cosmos Azure fornisce? ogni singolo requisito di sicurezza.

La tabella seguente li illustra in dettaglio.

|Requisito di sicurezza|Approccio alla sicurezza di Azure Cosmos DB|
|---|---|---|
|Sicurezza di rete|Utilizzo di un firewall IP è hello primo livello di protezione toosecure del database. Azure Cosmos DB supporta ora controlli di accesso IP basati su criteri per il supporto del firewall in ingresso. controlli di accesso basato su IP Hello sono simili regole del firewall toohello utilizzate dai sistemi di database tradizionale, ma sono espansi in modo che un account di database DB Cosmos Azure è accessibile solo da un set di computer o i servizi cloud approvato. <br><br>Azure DB Cosmos consente tooenable è un indirizzo IP specifico (168.61.48.0), un intervallo IP (168.61.48.0/8) e combinazione di indirizzi IP e gli intervalli. <br><br>Tutte le richieste che hanno origine da computer non compresi in questo elenco di elementi consentiti vengono bloccate da Azure Cosmos DB. Le richieste di approvazione macchine e servizi cloud devono completare quindi hello toobe di processo di autenticazione specificato toohello controllo di accesso alle risorse.<br><br>Per altre informazioni, vedere [Azure Cosmos DB firewall support](firewall-support.md) (Supporto del firewall di Azure Cosmos DB).|
|Authorization|Azure Cosmos DB usa HMAC (Hash Message Authentication Code) per l'autorizzazione. <br><br>Ogni richiesta viene generato un hash con chiave segreta account hello e hash con codifica base 64 successivo hello viene inviato con ogni tooAzure chiamata DB Cosmos. richiesta toovalidate hello, usato dal servizio Azure Cosmos DB hello hello chiave privata corretta e proprietà toogenerate un hash, quindi confronta il valore di hello con hello richiesta hello. Se due valori hello corrispondono, operazione hello è autorizzato correttamente e hello richiesta viene elaborata, in caso contrario si verifica un errore di autorizzazione e hello richiesta viene rifiutata.<br><br>È possibile utilizzare un [chiave master](secure-access-to-data.md#master-keys), o un [token della risorsa](secure-access-to-data.md#resource-tokens) consentendo risorsa tooa accesso granulare, ad esempio un documento.<br><br>Altre informazioni, vedere [protezione dell'accesso alle risorse Cosmos DB tooAzure](secure-access-to-data.md).|
|Utenti e autorizzazioni|Utilizzo di hello [chiave master](#master-key) per conto di hello, è possibile creare risorse utenti e risorse di autorizzazione per ogni database. Oggetto [token della risorsa](#resource-token) è associata a un'autorizzazione in un database e determina se l'utente hello ha accesso (lettura / scrittura, sola lettura, o nessun accesso) tooan di risorsa dell'applicazione nel database di hello. Le risorse dell'applicazione includono raccolte, documenti, allegati, stored procedure, trigger e funzioni definite dall'utente. token della risorsa Hello viene quindi utilizzata durante l'autenticazione tooprovide o negare l'accesso toohello risorse.<br><br>Altre informazioni, vedere [protezione dell'accesso alle risorse Cosmos DB tooAzure](secure-access-to-data.md).|
|Integrazione di Active Directory (controllo degli accessi in base al ruolo)| È anche possibile fornire accesso toohello account del database utilizzando il controllo di accesso (IAM) nel portale di Azure hello, come illustrato nella schermata di hello che segue questa tabella. IAM fornisce il controllo degli accessi in base al ruolo e si integra con Active Directory. È possibile utilizzare i ruoli predefiniti o personalizzati per utenti singoli e gruppi, come illustrato nella seguente immagine hello.|
|Replica globale|DB Cosmos Azure offre turnkey distribuzione globale, che consentono di tooreplicate tooany i dati tra Data Center di tutto il mondo di Azure con hello fare clic su di un pulsante. Replica globale consente di offrire una scalabilità globale e fornire l'accesso a bassa latenza tooyour dati tutto il mondo hello.<br><br>Nel contesto di sicurezza hello globale replica assicura la protezione dei dati da errori locali.<br><br>Per altre informazioni, vedere [Distribuire i dati a livello globale](distribute-data-globally.md).|
|Failover a livello di area|Se i dati sono stati replicati in più di un data center, Azure Cosmos DB esegue il rollover automatico delle operazioni, nel caso in cui un data center di un'area specifica passi alla modalità offline. È possibile creare un elenco di aree di failover utilizzando le aree di hello in cui i dati vengono replicati con priorità. <br><br>Per altre informazioni, vedere [Failover a livello di area in Azure Cosmos DB](regional-failover.md).|
|Replica locale|Anche all'interno di un singolo data center, Azure Cosmos DB replica automaticamente i dati per la disponibilità elevata che si hello scelta di [livelli di coerenza](consistency-levels.md). A differenza di tutti gli altri servizi di database, assicura un  [contratto di servizio con una disponibilità del tempo di attività pari al 99,99%](https://azure.microsoft.com/support/legal/sla/cosmos-db) e offre una garanzia dal punto di vista finanziario.|
|Backup online automatizzati|I backup dei database Azure Cosmos DB vengono eseguiti periodicamente e salvati in un archivio con ridondanza geografica. <br><br>Per altre informazioni, vedere [Backup online automatico e ripristino con Azure Cosmos DB](online-backup-and-restore.md).|
|Ripristinare i data eliminati|Hello backup automatizzati possono essere utilizzati toorecover dati può essere eliminato backup troppo ~ 30 giorni dopo l'evento hello. <br><br>Per altre informazioni, vedere [Backup online automatico e ripristino con Azure Cosmos DB](online-backup-and-restore.md)|
|Proteggere e isolare i dati sensibili|Tutti i dati in aree hello elencati in [Novità?](#whats-new) ora vengono crittografati a riposo.<br><br>Informazioni personali e altri dati riservati possono essere isolato toospecific raccolte di lettura e scrittura o accesso in sola lettura può essere limitato toospecific utenti.|
|Monitorare gli attacchi|Usando la registrazione di controllo e i log attività, è possibile monitorare l'account per identificare attività normali e anomale. È possibile visualizzare le operazioni eseguite su risorse, che ha avviato l'operazione di hello, quando si è verificato il funzionamento di hello, stato hello dell'operazione hello e molto più come illustrato nella schermata di hello segue questa tabella.|
|Rispondere tooattacks|Una volta che si hanno contattato il supporto di Azure tooreport un potenziale attacco, viene avviato un processo di risposta agli eventi imprevisti-passaggio 5. obiettivo di Hello del processo di hello-passaggio 5 è più rapidamente possibile toorestore normale servizio sicurezza e le operazioni dopo che viene rilevato un problema e viene avviata un'analisi più approfondita.<br><br>Altre informazioni, vedere [risposta di sicurezza di Microsoft Azure nel Cloud hello](https://aka.ms/securityresponsepaper).|
|Definizione del geo-fencing|Azure Cosmos DB assicura la conformità e la governance dei dati per le aree sovrane, ad esempio Germania, Cina, US Gov.|
|Strutture protette|I dati in Azure Cosmos DB vengono archiviati in unità SSD nei data center protetti di Azure.<br><br>Per altre informazioni, vedere [Data center globali Microsoft](https://www.microsoft.com/en-us/cloud-platform/global-datacenters)|
|Crittografia HTTPS/SSL/TLS|A tutte le interazioni Azure Cosmos DB da client a servizio viene applicato SSL/TLS 1.2. Anche a tutte le repliche all'interno di data center e tra data center viene applicato SSL/TLS 1.2.|
|Crittografia di dati inattivi|Tutti i dati archiviati in Azure Cosmos DB vengono crittografati quando sono inattivi. Per altre informazioni, vedere [Crittografia dei dati inattivi in Azure Cosmos DB](.\database-encryption-at-rest.md)|
|Server con patch|Come un database gestito, Azure Cosmos DB Elimina hello necessità toomanage e patch server, che viene eseguita automaticamente.|
|Account amministrativi con password complesse|Il disco rigido toobelieve è anche necessario toomention questo requisito, ma a differenza degli altri concorrenti, è Impossibile toohave un account amministrativo senza password nel database di Azure Cosmos.<br><br> La sicurezza usa SSL e l'autenticazione basata su segreti HMAC è supportata per impostazione predefinita.|
|Certificazioni di sicurezza e protezione dei dati|Azure Cosmos DB ha le certificazioni [ISO 27001](https://www.microsoft.com/en-us/TrustCenter/Compliance/ISO-IEC-27001), [clausole del modello dell'Unione Europea](https://www.microsoft.com/en-us/TrustCenter/Compliance/EU-Model-Clauses) e [HIPAA](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA). Altre certificazioni saranno presto disponibili.|

Hello seguente schermata mostra integrazione di Active directory (RBAC) tramite il controllo di accesso (IAM) nel portale di Azure hello: ![(IAM) di controllo di accesso nel portale di Azure - che illustra la protezione del database hello](./media/database-security/nosql-database-security-identity-access-management-iam-rbac.png)

Hello schermata riportata di seguito viene illustrato come utilizzare la registrazione di controllo e l'attività registra toomonitor account: ![log attività per Azure Cosmos DB](./media/database-security/nosql-database-security-application-logging.png)

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sulle chiavi master e i token di risorsa, vedere [tooAzure di accesso di protezione dei dati Cosmos DB](secure-access-to-data.md).

Per altre informazioni sulle certificazioni Microsoft, vedere il [Centro protezione di Azure](https://azure.microsoft.com/support/trust-center/).
