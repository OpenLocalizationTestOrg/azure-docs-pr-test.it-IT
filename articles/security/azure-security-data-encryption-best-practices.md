---
title: aaaData sicurezza e le procedure consigliate di crittografia | Documenti Microsoft
description: "Questo articolo presenta una serie di procedure consigliate per la sicurezza dei dati e la crittografia usando le funzionalità integrate di Azure."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 17ba67ad-e5cd-4a8f-b435-5218df753ca4
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: yurid
ms.openlocfilehash: 5057c85ed3107921462a40045e716675ea41e4bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-security-and-encryption-best-practices"></a>Procedure consigliate per la sicurezza dei dati e la crittografia in Azure
Uno dei hello chiavi toodata di protezione nel cloud hello è tenendo conto dei possibili stati di hello in cui i dati possono verificarsi e i controlli sono disponibili per tale stato. A scopo di hello di dati di Azure sicurezza crittografia le procedure consigliate e indicazioni di hello saranno intorno hello seguenti stati di dati:

* Inattivi: sono inclusi tutti gli oggetti, i contenitori e i tipi di archiviazione di informazioni esistenti in forma statica nei supporti fisici, siano essi dischi magnetici o dischi ottici.
* In transito: Quando vengono trasferiti dati tra i componenti, posizioni o i programmi, ad esempio tramite rete hello, su un bus di servizio (da on-premise toocloud e viceversa, incluse le connessioni ibride, ad esempio ExpressRoute) o durante un input/output processo, viene considerata come in movimento.

In questo articolo verrà illustrato un insieme di procedure consigliate per la crittografia e la sicurezza dei dati di Azure, Crittografia e hello esperienze di clienti come se stessi e queste procedure consigliate derivano dall'esperienza acquisita con la protezione dei dati di Azure.

Per ogni procedura consigliata verrà illustrato:

* Quali consigliabile hello
* Motivo per cui si desidera tooenable consigliata
* Se non è consigliata di hello tooenable, quale potrebbe essere il risultato di hello
* Procedura consigliata toohello alternative possibili
* Informazioni come procedura consigliata hello tooenable

Questo articolo di protezione dei dati di Azure e le procedure consigliate di crittografia si basa su un parere di consenso e funzionalità della piattaforma Azure e set di funzionalità, in cui si trovano in fase di hello in questo articolo è stato scritto. Opinioni e le tecnologie cambiano nel tempo e questo articolo verrà aggiornato in un tooreflect regolarmente le modifiche.

Le procedure consigliate per la sicurezza dei dati e la crittografia in Azure illustrate in questo articolo includono:

* Applicare l'autenticazione a più fattori
* Usare il controllo degli accessi in base al ruolo
* Crittografare le macchine virtuali di Azure
* Usare i moduli di protezione hardware
* Gestire con workstation sicure
* Abilitare la crittografia dei dati SQL
* Proteggere i dati in transito
* Applicare la crittografia dei dati a livello di file

## <a name="enforce-multi-factor-authentication"></a>Applicare l'autenticazione a più fattori
Hello innanzitutto l'accesso ai dati e il controllo in Microsoft Azure è utente di hello tooauthenticate. [Azure Multi-Factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md) è un metodo per verificare l'identità dell'utente in modo diverso rispetto alla semplice combinazione di nome utente e password. Questo metodo di autenticazione consente di salvaguardare accesso toodata e applicazioni rispettando richiesta dell'utente per un semplice processo.

Abilitando l'autenticazione a più fattori di Azure per gli utenti, si aggiunge un secondo livello di sicurezza toouser accessi e le transazioni. In questo caso, una transazione potrebbe accedere a un documento che si trova in un file server o in SharePoint Online. Azure MFA consente inoltre di probabilità di hello tooreduce IT che una credenziale compromessa avranno i dati del tooorganization di accesso.

Ad esempio: se si attiva Azure MFA per gli utenti e configurarlo toouse una telefonata o un SMS come verifica, se credenziali dell'utente hello sono compromesso, l'autore dell'attacco hello non essere in grado di tooaccess qualsiasi risorsa poiché non sarà possibile phone dell'accesso toouser. Le organizzazioni che non si aggiungono questo livello aggiuntivo di protezione dell'identità sono più vulnerabile agli attacchi di furto delle credenziali, con conseguente rischio di compromissione toodata.

Un'alternativa per le organizzazioni che vogliono controllo di autenticazione hello tookeep locale non è toouse [Server Azure multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-server.md), detta anche autenticazione a più fattori locale. Tramite questo metodo sarà comunque in grado di tooenforce autenticazione a più fattori, mantenendo hello MFA server locale.

Per ulteriori informazioni sull'autenticazione a più fattori di Azure, leggere l'articolo hello [Introduzione ad Azure multi-Factor Authentication nel cloud hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

## <a name="use-role-based-access-control-rbac"></a>Usare il controllo degli accessi in base al ruolo
Limitare l'accesso in base a hello [necessario tooknow](https://en.wikipedia.org/wiki/Need_to_know) e [privilegio](https://en.wikipedia.org/wiki/Principle_of_least_privilege) principi di sicurezza. Ciò è fondamentale per le organizzazioni che vogliono tooenforce criteri di sicurezza per l'accesso ai dati. Azure Role-Based Access controllo (RBAC) può essere utilizzato tooassign autorizzazioni toousers, gruppi e applicazioni in un determinato ambito. ambito Hello un'assegnazione di ruolo può essere una sottoscrizione, un gruppo di risorse o una singola risorsa.

È possibile sfruttare [ruoli RBAC incorporati](../active-directory/role-based-access-built-in-roles.md) in Azure tooassign privilegi toousers. È consigliabile utilizzare *collaboratore di Account di archiviazione* per gli operatori di cloud che necessitano di account di archiviazione toomanage e *collaboratore di Account di archiviazione classico* gli account di archiviazione classico toomanage di ruolo. Per gli operatori di cloud che necessita di macchine virtuali toomanage e account di archiviazione, è consigliabile aggiungerli troppo*collaboratore alla macchina virtuale* ruolo.

Le organizzazioni che non applicano il controllo di accesso ai dati con funzionalità come Controllo degli accessi in base al ruolo potrebbero concedere più privilegi del necessario ai propri utenti. Questo può causare la compromissione toodata con alcuni utenti con accesso toodata che sono non deve in primo luogo hello.

Maggiori informazioni su Azure RBAC leggendo l'articolo hello [gestire il controllo di accesso](../active-directory/role-based-access-control-configure.md).

## <a name="encrypt-azure-virtual-machines"></a>Crittografare le macchine virtuali di Azure
Per molte organizzazioni, la [crittografia dei dati inattivi](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) è un passaggio obbligatorio per assicurare la privacy, la conformità e la sovranità dei dati. Crittografia disco Azure consente tooencrypt gli amministratori IT Windows e i dischi di macchina virtuale IaaS Linux (VM). Crittografia disco Azure sfrutta hello settore caratteristica standard di BitLocker di Windows e funzionalità di data mining Crypt hello Linux tooprovide della crittografia del volume per hello del sistema operativo e i dischi dati hello.

È possibile sfruttare la crittografia del disco di Azure toohelp proteggere e salvaguardare toomeet i dati ai requisiti di sicurezza e conformità organizzativi. Le organizzazioni dovrebbero usare anche la crittografia toohelp attenuare i rischi correlati toounauthorized l'accesso ai dati. È inoltre consigliabile crittografare unità toowriting precedenti dati sensibili toothem.

Apportare tooencrypt che i volumi di dati della macchina virtuale e il volume di avvio ordine tooprotect dati inattivi nell'account di archiviazione di Azure. Proteggere i segreti e tutte le chiavi di crittografia hello sfruttando [insieme credenziali chiavi Azure](../key-vault/key-vault-whatis.md).

Per i server di Windows locale, prendere in considerazione hello crittografia procedure consigliate seguenti:

* Usare [BitLocker](https://technet.microsoft.com/library/dn306081.aspx) per la crittografia dei dati
* Archiviare le informazioni di ripristino in Servizi di dominio Active Directory.
* Se è presente qualsiasi problema che le chiavi BitLocker sono stati compromessi, è consigliabile che è formattare hello unità tooremove tutte le istanze di metadati di BitLocker hello unità hello o decrittografare e crittografare nuovamente l'intera unità hello.

Le organizzazioni che non impongono la crittografia dei dati sono probabilmente toodata toobe esposti i problemi di integrità, ad esempio gli utenti non autorizzati o malintenzionati rubare i dati e compromesso account ottenga l'accesso non autorizzato toodata in formato non crittografato. Oltre a tali rischi, aziende che dispongono di toocomply con dei regolamenti del settore, devono dimostrare che sono accurati e utilizza la sicurezza dei dati tooenhance controlli sicurezza corrette hello.

Sono disponibili ulteriori informazioni sulla crittografia del disco di Azure leggendo l'articolo hello [Azure crittografia disco per Windows e le macchine virtuali IaaS Linux](azure-security-disk-encryption.md).

## <a name="use-hardware-security-modules"></a>Usare i moduli di protezione hardware
Soluzioni di crittografia utilizzano dati tooencrypt chiavi private. È quindi fondamentale che queste chiavi vengano archiviate in modo sicuro. Gestione delle chiavi diventa parte integrante di protezione dei dati, dal momento che verrà toostore sfruttate le chiavi segrete che vengono utilizzati tooencrypt dati.

La crittografia del disco di Azure Usa [insieme credenziali chiavi Azure](https://azure.microsoft.com/services/key-vault/) toohelp controllare e gestire chiavi di crittografia del disco e i segreti nella sottoscrizione di insieme di credenziali delle chiavi, assicurando che tutti i dati nei dischi di macchina virtuale hello vengono crittografati a riposo in di Azure spazio di archiviazione. È consigliabile utilizzare chiavi tooaudit insieme credenziali chiavi Azure e utilizzo dei criteri.

Esistono molti toonot correlati di rischi intrinseci che i controlli di sicurezza appropriato in luogo tooprotect hello le chiavi segrete che sono stati utilizzati tooencrypt i dati. Se gli utenti malintenzionati hanno accesso le chiavi segrete toohello, verranno toodecrypt in grado di hello dati e avere accesso tooconfidential informazioni.

Maggiori informazioni su indicazioni generali per la gestione dei certificati in Azure, leggere l'articolo hello [gestione dei certificati in Azure: operazioni consigliate e sconsigliate](https://blogs.msdn.microsoft.com/azuresecurity/2015/07/13/certificate-management-in-azure-dos-and-donts/).

Per altre informazioni su Insieme di credenziali delle chiavi di Azure, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure](../key-vault/key-vault-get-started.md).

## <a name="manage-with-secure-workstations"></a>Gestire con workstation sicure
Poiché hello maggior parte dell'utente finale di hello attacchi destinazione hello, hello diventa uno dei punti di primario hello di attacco. Se un utente malintenzionato compromette endpoint hello, egli può sfruttare i dati del tooorganization di hello utente credenziali toogain accesso. La maggior parte degli attacchi di endpoint sono tootake in grado di sfruttare il fatto di hello che gli utenti finali sono gli amministratori di workstation locale.

È possibile ridurre questi rischi usando una workstation di gestione sicura. È consigliabile utilizzare un [workstation di accesso con privilegi (PAW)](https://technet.microsoft.com/library/mt634654.aspx) tooreduce superficie di attacco hello nella workstation. Queste workstation di gestione sicure consentono di limitare alcuni di questi attacchi e contribuiscono a proteggere i dati. Verificare che toouse PAW tooharden e blocco verso il basso la workstation. Si tratta di garanzie di sicurezza elevata tooprovide un passaggio importante per gli account sensibili, attività e la protezione dei dati.

Mancanza di endpoint protection potrebbe mettere a rischio i dati, assicurarsi che tooenforce criteri di sicurezza in tutti i dispositivi che vengono utilizzati tooconsume dati, indipendentemente dalla posizione di dati hello (cloud o locale).

È possibile ottenere informazioni workstation altri sui privilegi di accesso, leggere l'articolo hello [Securing Privileged Access](https://technet.microsoft.com/library/mt631194.aspx).

## <a name="enable-sql-data-encryption"></a>Abilitare la crittografia dei dati SQL
[Crittografia trasparente dei dati di Database SQL Azure](https://msdn.microsoft.com/library/dn948096.aspx) (TDE) contribuisce alla protezione dalle minacce di hello di attività dannose eseguendo la crittografia in tempo reale e la decrittografia di hello database, i backup associati, e i file di log delle transazioni a riposo senza richiesta di modifiche toohello applicazione.  Transparent Data Encryption crittografa l'archivio di hello di un intero database utilizzando una chiave di crittografia simmetrica hello chiamata chiave database.

Anche se archiviazione intera hello è crittografato, è molto importante tooalso crittografare il database stesso. Questa è un'implementazione di difesa hello approccio per la protezione dati. Se si utilizza [Database SQL di Azure](https://msdn.microsoft.com/library/0bf7e8ff-1416-4923-9c4c-49341e208c62.aspx) e tooprotect i dati sensibili, ad esempio carta di credito o numeri di previdenza sociale, è possibile crittografare i database con FIPS 140-2 convalidato a 256 bit della crittografia AES che soddisfi i requisiti di hello di molte standard del settore (ad esempio HIPAA, PCI).

È importante toounderstand che i file correlati troppo[estensione del pool di buffer](https://msdn.microsoft.com/library/dn133176.aspx) (BPE) non vengono crittografati quando un database viene crittografato con TDE. È necessario utilizzare strumenti di crittografia a livello di file system come BitLocker o hello [Encrypting File System](https://technet.microsoft.com/library/cc700811.aspx) (EFS) per tali file correlati.

Poiché un utente autorizzato, ad esempio un amministratore della sicurezza o un amministratore del database può accedere ai dati hello anche se il database di hello è crittografato con TDE, è necessario seguire anche indicazioni hello riportate di seguito:

* Autenticazione di SQL a livello di database hello
* Autenticazione di Azure AD con i ruoli di Controllo degli accessi in base al ruolo
* Gli utenti e applicazioni devono usare tooauthenticate account distinti. In questo modo è possibile limitare le autorizzazioni di hello concesso toousers e le applicazioni e ridurre i rischi di hello di attività dannose
* Sicurezza a livello di database implementano tramite i ruoli predefiniti del database (ad esempio db_datareader o db_datawriter) oppure è possibile creare ruoli personalizzati per l'applicazione di toogrant gli oggetti di database di autorizzazioni esplicite tooselected

Le organizzazioni che non usano la crittografia a livello di database potrebbero essere più esposte ad attacchi che potrebbero compromettere i dati presenti nel database SQL.

Sono disponibili ulteriori informazioni sulla crittografia TDE SQL leggendo l'articolo hello [Transparent Data Encryption con il Database di SQL Azure](https://msdn.microsoft.com/library/0bf7e8ff-1416-4923-9c4c-49341e208c62.aspx).

## <a name="protect-data-in-transit"></a>Proteggere i dati in transito
La protezione dei dati in transito deve essere una parte essenziale della strategia di protezione dati. Poiché i dati verranno spostate avanti e indietro da molte posizioni, hello generale si consiglia di utilizzare sempre dati tooexchange di protocolli SSL/TLS in posizioni diverse. In alcuni casi, è opportuno canale di comunicazione intera hello tooisolate tra le sedi locali e cloud dell'infrastruttura tramite una rete privata virtuale (VPN).

Per lo spostamento dei dati tra l'infrastruttura locale e Azure, è opportuno considerare le misure di protezione appropriate, ad esempio HTTPS o VPN.

Per le organizzazioni che richiedono l'accesso toosecure da più workstation in locale tooAzure, [Azure VPN site-to-site](../vpn-gateway/vpn-gateway-site-to-site-create.md).

Per le organizzazioni che richiedono l'accesso toosecure da una workstation trova tooAzure locale, utilizzare [Point-to-Site VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md).

Set di dati più grandi possono essere spostati su un collegamento WAN ad alta velocità dedicato, ad esempio [ExpressRoute](https://azure.microsoft.com/services/expressroute/). Se si sceglie toouse ExpressRoute, è anche possibile crittografare i dati hello hello a livello di applicazione utilizzando [SSL/TLS](https://support.microsoft.com/kb/257591) o altri protocolli per una maggiore protezione.

Se si interagisce con l'archiviazione di Azure tramite il portale di Azure hello, tutte le transazioni si verificano tramite HTTPS. [API REST di archiviazione](https://msdn.microsoft.com/library/azure/dd179355.aspx) tramite HTTPS può anche essere utilizzati toointeract con [di archiviazione di Azure](https://azure.microsoft.com/services/storage/) e [Database SQL di Azure](https://azure.microsoft.com/services/sql-database/).

Le organizzazioni che non soddisfano tooprotect dati in transito sono più sensibili per [attacchi man-in-the-middle](https://technet.microsoft.com/library/gg195821.aspx), [intercettazione](https://technet.microsoft.com/library/gg195641.aspx) e Hijack della sessione. Questi attacchi possono essere hello innanzitutto ottenere l'accesso ai dati tooconfidential.

Maggiori informazioni sull'opzione VPN di Azure leggendo l'articolo hello [pianificazione e progettazione per il Gateway VPN](../vpn-gateway/vpn-gateway-plan-design.md).

## <a name="enforce-file-level-data-encryption"></a>Applicare la crittografia dei dati a livello di file
Un altro livello di protezione che consente di aumentare il livello di hello di sicurezza per i dati che sta crittografando file hello stesso, indipendentemente dal percorso del file hello.

[Azure RMS](https://technet.microsoft.com/library/jj585026.aspx) toohelp di criteri di crittografia, identità e autorizzazione utilizza proteggere file e posta elettronica. Azure RMS opera su più dispositivi, tra cui telefoni, tablet e PC, applicando una protezione all'interno e all'esterno dell'organizzazione. Questa funzionalità è possibile poiché Azure RMS aggiunge un livello di protezione che rimane con dati hello, anche quando fuoriescono dai confini fisici dell'organizzazione.

Quando si usano Azure RMS tooprotect i file, si utilizza la crittografia standard del settore con il supporto completo di [FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/standards.html). Quando si utilizzano Azure RMS per la protezione dati, occorre garanzia hello che hello rimane associata file hello, anche se è copiato toostorage che non è incluso nel controllo hello del reparto IT, ad esempio un servizio di archiviazione cloud. Hello stesso comportamento si verifica per i file condivisi tramite posta elettronica, file hello viene protetto come un messaggio di posta elettronica tooan allegato, con istruzioni come tooopen hello protetto allegato.

Durante la pianificazione per l'adozione di Azure RMS è consigliabile hello segue:

* Installare hello [app RMS sharing](https://technet.microsoft.com/library/dn339006.aspx). Questa app si integra con le applicazioni Office installando un componente aggiuntivo di Office che offre agli utenti un modo semplice per proteggere direttamente i file.
* Configurare le applicazioni e servizi toosupport Azure RMS
* Creare [modelli personalizzati](https://technet.microsoft.com/library/dn642472.aspx) che rispecchiano i requisiti aziendali, ad esempio un modello per i dati riservati da applicare in tutti i messaggi di posta elettronica correlati a informazioni riservate.

Le organizzazioni che sono vulnerabili in [classificazione dei dati](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) e la protezione dei file potrebbe essere più vulnerabile toodata perdita. Senza protezione file appropriate, le organizzazioni non tooobtain in grado di ottenere informazioni aziendali accurate, monitoraggio per evitare eventuali abusi e impedire accessi non autorizzati toofiles.

Maggiori informazioni su Azure RMS, leggere l'articolo hello [Introduzione a Azure Rights Management](https://technet.microsoft.com/library/jj585016.aspx).
