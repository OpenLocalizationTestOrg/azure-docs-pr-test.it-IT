---
title: aaaOverview di sicurezza in archivio Data Lake | Documenti Microsoft
description: "Comprendere il motivo per cui Azure Data Lake Store è un archivio Big Data più sicuro"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ebd5b2ac-c5cc-46d4-9cfd-1a1ee70024c2
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 69e20bd046a9427202074baf59bff13f5b6a83ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="security-in-azure-data-lake-store"></a>Sicurezza in Archivio Azure Data Lake
Molte aziende sfruttano analitica dei dati di grandi dimensioni per business insights toohelp che li rendere smart decisioni. Un'organizzazione potrebbe presentare un ambiente complesso e regolamentato, con un numero crescente di utenti diversi. È essenziale per un toomake enterprise assicurarsi che i dati aziendali critici viene archiviati in modo più sicuro, con livello di accesso consentito agli utenti di tooindividual corretto hello. Archivio Azure Data Lake è progettato toohelp soddisfare questi requisiti di sicurezza. In questo articolo, informazioni sulle funzionalità di sicurezza di hello di archivio Data Lake, tra cui:

* Autenticazione
* Authorization
* Isolamento rete
* Protezione dati
* Controllo

## <a name="authentication-and-identity-management"></a>Autenticazione e gestione delle identità
L'autenticazione è il processo di hello mediante il quale viene verificata l'identità dell'utente quando l'utente di hello interagisce con l'archivio Data Lake o con qualsiasi servizio che si connette tooData Lake archivio. Per la gestione delle identità e autenticazione, viene utilizzato l'archivio Data Lake [Azure Active Directory](../active-directory/active-directory-whatis.md), un'identità e accessi gestione soluzione cloud che semplifica la gestione di utenti e gruppi hello.

Ogni sottoscrizione Azure può essere associata a un'istanza di Azure Active Directory. Solo gli utenti e le identità del servizio che sono definite nel servizio Azure Active Directory possono accedere all'account archivio Data Lake, tramite hello portale di Azure, gli strumenti da riga di comando, o le applicazioni client, che l'organizzazione delle compilazioni tramite hello Azure Data Archivio Lake SDK. I vantaggi principali dell'uso di Azure Active Directory come meccanismo di controllo di accesso centralizzato sono:

* Gestione semplificata del ciclo di vita dell'identità. identità Hello di un utente o un servizio (un'identità dell'entità servizio) può essere rapidamente creato e revocare rapidamente semplicemente eliminando o la disattivazione di hello account nella directory hello.
* Autenticazione a più fattori [Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) offre un livello di sicurezza aggiuntivo per l'accesso degli utenti e le transazioni.
* Autenticazione da qualsiasi client usando un protocollo aperto standard, ad esempio OAuth oppure OpenID.
* Federazione con provider di identità cloud e servizi di directory dell'organizzazione.

## <a name="authorization-and-access-control"></a>Autorizzazione e controllo di accesso
Dopo che un utente viene autenticato da Azure Active Directory in modo che hello utente possa accedere archivio Azure Data Lake, controlli di autorizzazione di accesso le autorizzazioni per archivio Data Lake. Archivio Data Lake separa l'autorizzazione per le attività relative all'account e dati correlati nell'hello seguente modo:

* [Controllo degli accessi in base al ruolo](../active-directory/role-based-access-control-what-is.md) (RBAC) fornito da Azure per la gestione degli account.
* POSIX ACL per l'accesso ai dati nell'archivio di hello

### <a name="rbac-for-account-management"></a>Controllo degli accessi in base al ruolo per la gestione degli account
Quattro ruoli di base vengono definiti per Data Lake Store per impostazione predefinita. i ruoli di Hello consentono diverse operazioni su un account archivio Data Lake tramite hello portale di Azure, i cmdlet di PowerShell e API REST. Hello proprietario e i ruoli per i collaboratori possono eseguire un'ampia gamma di funzioni di amministrazione account hello. È possibile assegnare hello lettore ruolo toousers che devono solo interagire con i dati.

![Ruoli Controllo degli accessi in base al ruolo](./media/data-lake-store-security-overview/rbac-roles.png "Ruoli Controllo degli accessi in base al ruolo")

Si noti che, sebbene per la gestione degli account vengono assegnati i ruoli, alcuni ruoli sulle toodata di accesso. È necessario toouse ACL toocontrol accesso toooperations che un utente può eseguire nel sistema di file hello. Hello nella tabella seguente mostra un riepilogo di rights management e diritti di accesso ai dati per hello ruoli predefiniti.

| Ruoli | Diritti di gestione | Diritti di accesso ai dati | Spiegazione |
| --- | --- | --- | --- |
| Nessun ruolo assegnato |None |Regolato da ACL |utente di Hello non può utilizzare hello Azure portal o Azure PowerShell cmdlet toobrowse archivio Data Lake. utente di Hello può utilizzare solo gli strumenti da riga di comando. |
| Proprietario |Tutti |Tutti |ruolo di proprietario Hello è un utente avanzato. Questo ruolo può gestire tutto e ha accesso completo toodata. |
| Reader |Sola lettura |Regolato da ACL |ruolo di lettore Hello possibile visualizzare tutti gli elementi relativi alla gestione di account, ad esempio quale utente è assegnato il ruolo di toowhich. ruolo di lettore Hello non è possibile apportare le modifiche. |
| Collaboratore |Tutti tranne quelli di aggiunta e rimozione dei ruoli |Regolato da ACL |ruolo di collaboratore Hello è possibile gestire alcuni aspetti di un account, ad esempio le distribuzioni e la creazione e la gestione degli avvisi. ruolo di collaboratore Hello non è possibile aggiungere o rimuovere i ruoli. |
| Amministratore accessi utente |Aggiunta e rimozione dei ruoli |Regolato da ACL |ruolo di amministratore di accesso utente Hello può gestire tooaccounts di accesso utente. |

Per istruzioni, vedere [assegnare gli utenti o gruppi di protezione account archivio Lake tooData](data-lake-store-secure-data.md#assign-users-or-security-groups-to-azure-data-lake-store-accounts).

### <a name="using-acls-for-operations-on-file-systems"></a>Uso degli ACL per le operazioni sui file system
Data Lake Store è un file system gerarchico come HDFS (Hadoop Distributed File System) e supporta gli [elenchi di controllo di accesso POSIX](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists). Controlla (r) di lettura, scrittura (w) ed eseguire (tooresources le autorizzazioni per il ruolo di proprietario hello, per il gruppo proprietari hello e per altri utenti e gruppi x). In hello Data Lake archivio pubblico Preview (versione corrente di hello), gli ACL possono essere abilitati nella cartella radice hello, le sottocartelle e sui singoli file. Per altre informazioni sul funzionamento degli elenchi di controllo di accesso nel contesto di Data Lake Store, vedere [Controllo di accesso in Data Lake Store](data-lake-store-access-control.md).

È consigliabile definire gli elenchi di controllo di accesso per più utenti usando [gruppi di sicurezza](../active-directory/active-directory-accessmanagement-manage-groups.md). Aggiungere il gruppo di sicurezza tooa utenti e quindi assegnare gli elenchi ACL hello per un gruppo di sicurezza toothat file o cartella. Questo è utile quando si desidera tooprovide accesso personalizzato, perché si è limitati tooadding un massimo di 9 voci per l'accesso personalizzato. Per ulteriori informazioni su come toobetter proteggere i dati archiviati nell'archivio Data Lake tramite gruppi di sicurezza di Azure Active Directory, vedere [assegnare gli utenti o gruppo di sicurezza come toohello ACL di sistema di file di archivio Azure Data Lake](data-lake-store-secure-data.md#filepermissions).

![Elencare gli accessi standard e personalizzati](./media/data-lake-store-security-overview/adl.acl.2.png "Elencare gli accessi standard e personalizzati")

## <a name="network-isolation"></a>Isolamento rete
Archiviazione dei dati di tooyour di usare l'archivio Data Lake toohelp controllo accesso a livello di rete hello. È possibile stabilire firewall e definire un intervallo di indirizzi IP per i client attendibili. Con un intervallo di indirizzi IP, solo i client che hanno un indirizzo IP interno hello definito possono connettersi tooData Lake archivio.

![Impostazioni del firewall e accesso IP](./media/data-lake-store-security-overview/firewall-ip-access.png "Impostazioni del firewall e indirizzo IP")

## <a name="data-protection"></a>Protezione dati
Azure Data Lake Store protegge i dati durante tutto il loro ciclo di vita. Per i dati in transito, archivio Data Lake utilizza i dati di toosecure protocollo di hello standard del settore Transport Layer Security (TLS) su rete hello.

![Crittografia in Data Lake Store](./media/data-lake-store-security-overview/adls-encryption.png "Crittografia in Data Lake Store")

Archivio Data Lake offre anche la crittografia per i dati vengono archiviati in account hello. Puoi scegliere toohave i dati crittografati o optare per alcuna crittografia. Se il consenso esplicito per la crittografia dei dati archiviati nell'archivio Data Lake sono crittografato toostoring precedenti nel supporto permanente. In tal caso, archivio Data Lake automaticamente crittografa i dati precedenti toopersisting e decrittografa tooretrieval precedente dei dati, pertanto è completamente trasparente toohello client l'accesso ai dati hello. Non sussiste alcuna modifica di codice necessaria per hello client side tooencrypt/decrittografare i dati.

Gestione delle chiavi, archivio Data Lake fornisce due modalità per la gestione delle chiavi di crittografia master (MEKs), che sono necessari per decrittografare i dati archiviati in hello archivio Data Lake. È possibile consentire archivio Data Lake gestirà automaticamente MEKs hello oppure scegliere la proprietà tooretain di hello MEKs con l'account insieme credenziali chiavi Azure. Specificare la modalità di gestione delle chiavi hello durante la creazione di un account archivio Data Lake. Per ulteriori informazioni sulla configurazione relative a crittografia tooprovide, vedere [introduzione archivio Azure Data Lake tramite il portale di Azure hello](data-lake-store-get-started-portal.md).

## <a name="auditing-and-diagnostic-logs"></a>Log di controllo e diagnostica
È possibile usare i log di diagnostica o di controllo a seconda che si stiano cercando log relativi alle attività correlate alla gestione o alle attività correlate ai dati.

* Attività correlate alla gestione usare le API di gestione risorse di Azure e sono visibili nel portale di Azure hello tramite i log di controllo.
* Attività correlate ai dati utilizzare le API REST WebHDFS e resi visibili nel portale di Azure hello tramite i log di diagnostica.

### <a name="auditing-logs"></a>Log di controllo
toocomply alle normative, un'organizzazione potrebbe richiedere gli itinerari di controllo adeguate se è necessario toodig in specifici eventi imprevisti. Data Lake Store prevede monitoraggio e controllo integrati e registra tutte le attività di gestione dell'account.

Per gli audit trail gestione di account, visualizzare e scegliere le colonne di hello che si desidera toolog. È anche possibile esportare i registri di controllo tooAzure archiviazione.

![Log di controllo](./media/data-lake-store-security-overview/audit-logs.png "Log di controllo")

### <a name="diagnostic-logs"></a>Log di diagnostica
È possibile impostare gli itinerari di controllo di accesso ai dati nel portale di Azure (in impostazioni di diagnostica) hello e creare un account di archiviazione Blob di Azure in cui sono archiviati i log di hello.

![Log di diagnostica](./media/data-lake-store-security-overview/diagnostic-logs.png "Log di diagnostica")

Dopo aver configurato le impostazioni di diagnostica, è possibile visualizzare i registri di hello in hello **i log di diagnostica** scheda.

Per altre informazioni sull'uso dei log di diagnostica con Azure Data Lake Store, vedere [Accesso ai log di diagnostica per Azure Data Lake Store](data-lake-store-diagnostic-logs.md).

## <a name="summary"></a>Riepilogo
I clienti aziendali richiedono una piattaforma cloud analitica di dati che è toouse sicura e semplice. Archivio Azure Data Lake è progettato toohelp soddisfare questi requisiti tramite la gestione delle identità e l'autenticazione tramite l'integrazione di Azure Active Directory, basata sugli ACL di autorizzazione, l'isolamento rete, la crittografia dei dati in transito e inattivi (presto hello futuro) e il controllo.

Se si desidera toosee nuove funzionalità di archivio Data Lake, inviare commenti e suggerimenti in hello [UserVoice di archivio Data Lake forum](https://feedback.azure.com/forums/327234-data-lake).

## <a name="see-also"></a>Vedere anche
* [Panoramica di Archivio Data Lake di Azure](data-lake-store-overview.md)
* [Introduzione a Data Lake Store](data-lake-store-get-started-portal.md)
* [Proteggere i dati in Data Lake Store](data-lake-store-secure-data.md)

