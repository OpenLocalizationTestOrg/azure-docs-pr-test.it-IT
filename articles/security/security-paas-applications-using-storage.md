---
title: le applicazioni PaaS aaaSecuring utilizzando l'archiviazione di Azure | Documenti Microsoft
description: " Informazioni sulle procedure consigliate di sicurezza in Archiviazione di Azure per proteggere le applicazioni PaaS Web e per dispositivi mobili. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: TomShinder
ms.openlocfilehash: 3fed75cb121e7f32eb8b948ee12ca35fb25eca7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-web-and-mobile-applications-using-azure-storage"></a>Protezione delle applicazioni PaaS Web e per dispositivi mobili usando Archiviazione di Azure
Questo articolo illustra un insieme di procedure consigliate di sicurezza in Archiviazione di Azure per la protezione delle applicazioni PaaS Web e per dispositivi mobili. Queste procedure consigliate derivano dall'esperienza acquisita con Azure e l'esperienza dei clienti hello come manualmente.

Hello [Guida alla protezione di archiviazione di Azure](../storage/common/storage-security-guide.md) è un'ottima fonte per informazioni dettagliate sulla sicurezza e di archiviazione di Azure.  Questo articolo illustra a un livello elevato alcuni dei concetti di hello trovati nella Guida alla protezione di hello e Guida alla protezione toohello di collegamenti, nonché altre origini, per ulteriori informazioni.

## <a name="azure-storage"></a>Archiviazione di Azure
Azure rende possibili toodeploy e utilizzare l'archiviazione in modi non facilmente ottenibili in locale. Con archiviazione di Azure è possibile raggiungere livelli elevati di scalabilità e disponibilità con un lavoro richiesto minimo. Non solo è foundation hello di archiviazione di Azure per Windows e Linux macchine virtuali di Azure, può inoltre supportare applicazioni distribuite di grandi dimensioni.

Archiviazione di Azure fornisce i seguenti quattro servizi hello: Blob di archiviazione, archiviazione tabelle, l'archiviazione delle code e archiviazione di File. vedere, più toolearn [tooMicrosoft introduzione di archiviazione di Azure](../storage/storage-introduction.md).

## <a name="best-practices"></a>Procedure consigliate
Questo articolo illustra hello procedure consigliate seguenti:

- Protezione dell'accesso:
   - Firme di accesso condiviso
   - Disco gestito
   - Controllo degli accessi in base al ruolo

- Crittografia di archiviazione:
   - Crittografia lato client per i dati di valore elevato
   - Crittografia dischi di Azure per le macchine virtuali (VM)
   - Crittografia del servizio di archiviazione

## <a name="access-protection"></a>Protezione dell'accesso
### <a name="use-shared-access-signature-instead-of-a-storage-account-key"></a>Usare la firma di accesso condiviso anziché una chiave dell'account di archiviazione

In una soluzione IaaS, le macchine virtuali Windows Server o Linux vengono in genere protette dalle minacce di divulgazione e manomissione usando meccanismi di controllo di accesso. In Windows si userebbero gli [elenchi di controllo di accesso (ACL)](../virtual-network/virtual-networks-acl.md) e in Linux si userebbe probabilmente [chmod](https://en.wikipedia.org/wiki/Chmod). In pratica, ciò è esattamente ciò che si farebbe attualmente per proteggere i file in un server nel proprio data center.

La funzionalità PaaS è diversa. Uno dei hello file più comuni modi toostore in Microsoft Azure è toouse [archiviazione Blob di Azure](../storage/storage-dotnet-how-to-use-blobs.md). Una differenza tra l'archiviazione Blob e di archiviazione di file è dei / o file hello e i metodi di protezione hello forniti con i/o file.

Il controllo di accesso è fondamentale. toohelp è possibile controllare l'archiviazione tooAzure accesso, hello sistema genera due chiavi dell'account di archiviazione a 512 bit (SAKs) quando si [creare un account di archiviazione](../storage/common/storage-create-storage-account.md). livello di Hello di ridondanza chiave rende possibile si tooavoid servizio interrupt durante la rotazione della chiave di routine.

Chiavi di accesso di archiviazione sono i segreti ad alta priorità e devono essere accessibile toothose responsabile per il controllo di accesso di archiviazione. Se persone sbagliate hello ottenere l'accesso chiavi toothese, essi verranno dispone del controllo completo di spazio di archiviazione e potrebbe sostituire, eliminare o aggiungere toostorage file. Sono inclusi il malware e altri tipi di contenuto che potrebbero compromettere l'organizzazione o i clienti.

È comunque necessario un tooobjects di accesso tooprovide modo nell'archiviazione. tooprovide più granulari di accesso è possibile sfruttare [firma di accesso condiviso](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (SAS). Hello SAS rende possibile il tooshare oggetti specifici nel servizio di archiviazione per un intervallo di tempo predefinito e con autorizzazioni specifiche. Una firma di accesso condiviso consente toodefine:

- intervallo di Hello in cui hello è valido, inclusi l'ora di inizio hello e l'ora di scadenza hello SAS.
- autorizzazioni Hello concesse da hello SAS. Ad esempio, una firma di accesso condiviso in un blob potrebbe concedere a un utente di lettura e blob toothat le autorizzazioni di scrittura, ma non eliminare le autorizzazioni.
- Un indirizzo IP facoltativo o intervallo di indirizzi IP da cui accettare l'archiviazione di Azure hello SAS. Ad esempio, specificare un intervallo di indirizzi IP appartenenti tooyour organizzazione. Fornisce un'altra misura di sicurezza per la firma di accesso condiviso.
- protocollo Hello su cui l'archiviazione di Azure accetta hello SAS. È possibile utilizzare questo tooclients accesso toorestrict di parametro facoltativo tramite HTTPS.

Firma di accesso condiviso consente tooshare hello contenuto desiderato tooshare senza fornire le chiavi dell'Account di archiviazione. Utilizzando sempre SAS nell'applicazione è un tooshare in modo sicuro le risorse di archiviazione senza compromettere le chiavi di account di archiviazione.

vedere, più toolearn [tramite firme di accesso condiviso](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (SAS). altre informazioni sulle potenziali rischi e le indicazioni di toomitigate toolearn tali rischi, vedere [procedure consigliate quando si usa SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

### <a name="use-managed-disks-for-vms"></a>Usare dischi gestiti per le macchine virtuali

Quando si sceglie [dischi gestiti di Azure](../storage/storage-managed-disks-overview.md), Azure gestisce gli account di archiviazione hello utilizzati per i dischi di macchina virtuale. È sufficiente toodo scegliere il tipo di hello del disco (Standard o Premium) e dimensioni del disco hello; Archiviazione di Azure eseguirà hello rest. Non è necessario tooworry sui limiti di scalabilità che potrebbero disporre di richieste in caso contrario gli account di archiviazione toomultiple tooyou.

vedere, più toolearn [domande frequenti sui gestite e i dischi premium](../storage/storage-faq-for-disks.md).

### <a name="use-role-based-access-control"></a>Usare il controllo degli accessi in base al ruolo

Abbiamo parlato in precedenza utilizzando tooobjects di firma di accesso condiviso (SAS) toogrant limitato l'accesso dei client tooother account di archiviazione, senza esporre la chiave di account di archiviazione di account. Talvolta i rischi di hello associati a una specifica operazione su account di archiviazione hello superare vantaggi in termini di firma di accesso condiviso. A volte risulta più semplice accesso toomanage in altri modi.

Un altro modo toomanage l'accesso è toouse [gestire il controllo di accesso](../active-directory/role-based-access-control-what-is.md) (RBAC). Con RBAC, si è concentrati sulla disposizione dei dipendenti hello conoscere esattamente le autorizzazioni che necessarie, in base tooknow necessità hello e i principi di sicurezza con privilegi minimi. Numero eccessivo di autorizzazioni possono esporre un tooattackers account. Un numero di autorizzazioni insufficiente ostacola l'efficienza del lavoro dei dipendenti. Il controllo degli accessi in base al ruolo di Azure consente di risolvere questo problema offrendo una gestione granulare degli accessi per Azure. Ciò è fondamentale per le organizzazioni che vogliono tooenforce criteri di sicurezza per l'accesso ai dati.

È possibile utilizzare ruoli RBAC incorporati in Azure tooassign privilegi toousers. Considerare l'uso di collaboratori di Account di archiviazione per gli operatori di cloud che necessitano di account di archiviazione toomanage e gli account di archiviazione classico toomanage di ruolo di collaboratore di Account di archiviazione classico. Per gli operatori di cloud che devono essere toomanage macchine virtuali, ma non una rete virtuale hello o toowhich di account di archiviazione che sono connessi, è consigliabile aggiungerli toohello ruolo di collaboratore alla macchina virtuale.

Le organizzazioni che non applicano il controllo di accesso ai dati con funzionalità come Controllo degli accessi in base al ruolo potrebbero concedere più privilegi del necessario ai propri utenti. Ciò può comportare toodata compromissione consentendo alcuni toodata accesso gli utenti hanno non deve in primo luogo hello.

toolearn che su RBAC, vedere:

- [Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-control-configure.md)
- [Ruoli predefiniti per il controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-built-in-roles.md)
- [Guida alla protezione di archiviazione Azure](../storage/common/storage-security-guide.md) per informazioni su come toosecure account di archiviazione con RBAC

## <a name="storage-encryption"></a>Crittografia di archiviazione
### <a name="use-client-side-encryption-for-high-value-data"></a>Usare la crittografia lato client per i dati di valore elevato

Abilita crittografia lato client è tooprogrammatically crittografare i dati in transito prima di caricare tooAzure archiviazione e decrittografare i dati a livello di codice quando questi vengono recuperati dall'archivio.  Questo approccio consente la crittografia dei dati in transito, ma anche dei dati inattivi.  Crittografia client-side è metodo più sicuro hello la crittografia dei dati, ma occorre applicazione tooyour di toomake modifiche a livello di codice e implementare i processi di gestione delle chiavi.

Crittografia client-side consente inoltre il controllo esclusivo toohave sulle proprie chiavi di crittografia.  È possibile generare e gestire chiavi di crittografia personalizzate.  Crittografia lato client utilizza una tecnica di busta in cui hello libreria client di archiviazione di Azure genera una contenuto chiave di crittografia (CEK) che viene eseguito il wrapping (crittografata) con chiave di crittografia della chiave hello (CHIAVI). Hello KEK è identificato da un identificatore di chiave e può essere una coppia di chiavi asimmetriche o di una chiave simmetrica e possono essere gestiti in locale o memorizzati [insieme credenziali chiavi Azure](../key-vault/key-vault-whatis.md).

Crittografia client-side è incorporata in Java hello e le librerie client di archiviazione .NET hello.  Vedere [Crittografia lato client e Azure Key Vault per Archiviazione di Microsoft Azure](../storage/storage-client-side-encryption.md) per informazioni sulla crittografia dei dati all'interno di applicazioni client e la generazione e gestione di chiavi di crittografia personalizzate.

### <a name="azure-disk-encryption-for-vms"></a>Crittografia dischi di Azure per le VM
Crittografia dischi di Azure è una funzionalità che consente di crittografare i dischi delle macchine virtuali IaaS Windows e Linux. Crittografia disco Azure sfrutta hello settore caratteristica standard di BitLocker di Windows e funzionalità di data mining Crypt hello Linux tooprovide della crittografia del volume per hello del sistema operativo e i dischi dati hello. soluzione hello è integrato con insieme credenziali chiavi Azure toohelp è controllare e gestire i segreti e tutte le chiavi di crittografia del disco hello nella sottoscrizione dell'insieme di credenziali chiave. soluzione Hello assicura anche che tutti i dati nei dischi di macchina virtuale hello vengono crittografati a riposo nell'archiviazione Azure.

Vedere [Crittografia dischi di Azure per le macchine virtuali IaaS Windows e Linux](azure-security-disk-encryption.md).

### <a name="storage-service-encryption"></a>Crittografia del servizio di archiviazione
Quando [la crittografia del servizio di archiviazione](../storage/storage-service-encryption.md) per archiviazione di File è abilitata, i dati di hello vengono crittografati automaticamente utilizzando la crittografia AES-256. Microsoft gestisce tutti hello crittografia, decrittografia e la gestione delle chiavi. Questa funzionalità è disponibile per i tipi di ridondanza archiviazione con ridondanza locale e con ridondanza geografica.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo ha introdotto raccolta tooa di archiviazione di Azure le procedure consigliate per proteggere il PaaS web e applicazioni per dispositivi mobili. toolearn più sulla protezione di distribuzioni PaaS, vedere:

- [Protezione delle distribuzioni PaaS](security-paas-deployments.md)
- [Protezione delle applicazioni Web e per dispositivi mobili in PaaS mediante i Servizi app di Azure](security-paas-applications-using-app-services.md)
- [Protezione di database PaaS in Azure](security-paas-applications-using-sql.md)
