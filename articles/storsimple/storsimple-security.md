---
title: sicurezza di serie 8000 aaaStorSimple | Documenti Microsoft
description: "Viene descritto hello funzionalità di sicurezza e privacy per proteggere il servizio StorSimple, dispositivi e dati in locale e nel cloud hello."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: a21d19c6-83b4-418c-9380-323bb9f76612
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/03/2016
ms.author: v-sharos
ms.openlocfilehash: b9e6c8b3371b4039549972cf507052312ed7cdaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-security-and-data-protection"></a>Sicurezza e protezione dei dati di StorSimple
## <a name="overview"></a>Panoramica
La sicurezza è delle principali preoccupazioni per chi sta adottando una nuova tecnologia, soprattutto quando hello tecnologia viene utilizzata con dati riservati o proprietari. Quando si valutano tecnologie diverse, è necessario tenere in considerazione l'aumento dei rischi e dei costi per la protezione dei dati. Microsoft Azure StorSimple offre sia una soluzione di privacy e sicurezza per la protezione dati, tooensure di supporto: 

* **Riservatezza** – Solo le entità autorizzate possono visualizzare i dati. 
* **Integrità** – Solo le entità autorizzate possono modificare o eliminare i dati.

Hello soluzioni di Microsoft Azure StorSimple è costituito da quattro componenti principali che interagiscono tra loro:

* **Il servizio StorSimple Manager ospitato in Microsoft Azure** : servizio di gestione di hello utilizzare tooconfigure ed eseguire il provisioning hello dispositivo StorSimple.
* **Dispositivo StorSimple** – Dispositivo fisico installato nel data center. Tutti gli host e i client che generano dati di connettono il dispositivo StorSimple toohello e dispositivo hello gestisce dati hello e spostarlo toohello cloud di Azure a seconda dei casi.
* **I client/host connessi dispositivo toohello** : hello client dell'infrastruttura che si connettono dispositivo StorSimple toohello e generare dati che devono essere toobe protetto.
* **Archiviazione cloud** : hello posizione nel cloud di Azure dove vengono archiviati dati hello.

Hello sezioni seguenti descrivono le funzionalità di sicurezza StorSimple hello che consentono di proteggere ciascuno di questi componenti e i dati di hello archiviati su di essi. Include inoltre un elenco di domande che potrebbero avere sulla protezione di Microsoft Azure StorSimple e relative risposte hello.

## <a name="storsimple-manager-service-protection"></a>Protezione del servizio StorSimple Manager
Hello servizio StorSimple Manager è un servizio di gestione ospitato in Microsoft Azure e utilizzato toomanage tutti i dispositivi StorSimple che l'organizzazione ha acquistato. Hello servizio StorSimple Manager è possibile accedere utilizzando le credenziali aziendali di toolog sulla toohello portale di Azure classico tramite un web browser. 

Accesso toohello servizio StorSimple Manager richiede che l'organizzazione dispone di una sottoscrizione di Azure a cui sia incluso StorSimple. La sottoscrizione determina le funzionalità di hello che è possibile accedere in hello portale di Azure classico. Se l'organizzazione non dispone di una sottoscrizione di Azure e si desidera toolearn ulteriori informazioni, vedere [iscriversi a Azure come organizzazione](../active-directory/sign-up-organization.md). 

Poiché hello servizio StorSimple Manager è ospitato in Azure, è protetto dalle funzionalità di sicurezza di Azure hello. Per ulteriori informazioni sulle funzionalità di sicurezza hello fornita da Microsoft Azure, visitare toohello [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/security/).

## <a name="storsimple-device-protection"></a>Protezione del dispositivo StorSimple
dispositivo StorSimple Hello è un dispositivo di archiviazione ibrido locale contenente unità (SSD Solid) e le unità disco rigido (HDD), oltre a controller ridondanti e funzionalità di failover automatico. controller Hello gestire l'archiviazione a più livelli, il posizionamento attualmente usati (o hot) dati nell'archiviazione locale (nel dispositivo StorSimple hello o server locali), durante lo spostamento di dati utilizzati meno frequentemente toohello nel cloud.

Autorizzato solo i dispositivi possono toojoin hello servizio StorSimple Manager creato nella sottoscrizione di Azure StorSimple. tooauthorize un dispositivo, è necessario registrarlo con il servizio StorSimple Manager hello fornendo la chiave di registrazione del servizio hello. chiave di registrazione del servizio Hello è una chiave casuale a 128 bit generata nel portale di Azure classico hello. 

![Chiave di registrazione del servizio](./media/storsimple-security/ServiceRegistrationKey.png)

toolearn come ottenere un go chiave, la registrazione di servizio troppo[passaggio 2: chiave di registrazione del servizio Get hello](storsimple-deployment-walkthrough.md#step-2-get-the-service-registration-key).

chiave di registrazione del servizio Hello è una chiave lunga che contiene i 100 caratteri. È possibile copiare la chiave hello e salvarlo in un file di testo in un luogo sicuro in modo che sia possibile usarlo tooauthorize altri dispositivi in base alle esigenze. Se dopo aver registrato il primo dispositivo, chiave di registrazione del servizio hello viene perso, è possibile generare una nuova chiave dal servizio StorSimple Manager hello. Ciò non influirà sull'operazione di hello dei dispositivi esistenti. 

Dopo aver registrato un dispositivo, utilizza i token toocommunicate con Microsoft Azure. chiave di registrazione del servizio Hello non viene utilizzato dopo la registrazione del dispositivo.

> [!NOTE]
> È consigliabile che si rigenera chiave di registrazione del servizio hello dopo ogni uso.
> 
> 

## <a name="protect-your-storsimple-solution-via-passwords"></a>Proteggere la soluzione StorSimple con le password
Le password sono un aspetto importante della sicurezza dei computer e vengono spesso utilizzate nella soluzione StorSimple hello toohelp assicurarsi che i dati siano tooauthorized accessibili solo dagli utenti. StorSimple consente hello tooconfigure seguenti password:

* Password amministratore del dispositivo StorSimple
* Password di destinazione e iniziatore CHAP (Challenge Handshake Authentication Protocol)
* Password di Gestione snapshot StorSimple

### <a name="windows-powershell-for-storsimple-and-hello-storsimple-device-administrator-password"></a>Windows PowerShell per StorSimple e hello password amministratore del dispositivo StorSimple
Windows PowerShell per StorSimple è un'interfaccia della riga di comando che è possibile utilizzare un dispositivo di StorSimple toomanage hello. Windows PowerShell per StorSimple include funzionalità che consentono di tooregister il dispositivo, configurare l'interfaccia di rete hello sul dispositivo, installare alcuni tipi di aggiornamento, risolvere i problemi del dispositivo per l'accesso alla sessione di supporto hello e modificare lo stato del dispositivo hello . Connessione toohello la console seriale sul dispositivo hello o usando la comunicazione remota di Windows PowerShell, è possibile accedere Windows PowerShell per StorSimple.

La comunicazione remota di PowerShell può essere stabilita su HTTPS o HTTP. Se è abilitata la gestione remota su HTTPS, è necessario gestione remota di hello toodownload dal dispositivo hello del certificato e installarlo sul client remoto hello. Per ulteriori informazioni sulla comunicazione remota di PowerShell, vedere troppo[connettersi in remoto il dispositivo di StorSimple tooyour](storsimple-remote-connect.md).

Dopo aver utilizzato Windows PowerShell per StorSimple tooconnect toohello dispositivo, sarà necessario toolog tooprovide hello dispositivo amministratore password nel dispositivo toohello.

![Password amministratore del dispositivo](./media/storsimple-security/DeviceAdminPW.png)

Mantenere hello presenti procedure consigliate seguenti:

* La gestione remota è disattivata per impostazione predefinita. È possibile utilizzare tooenable servizio StorSimple Manager di hello è. Per una protezione ottimale, accesso remoto deve essere abilitato solo durante il periodo di tempo che è effettivamente necessario hello.
* Se si modifica la password di hello, essere toonotify che tutti gli utenti di accesso remoto in modo che non si verifica una perdita di connettività imprevisti.
* Hello servizio StorSimple Manager non è possibile recuperare le password esistenti: solo reimpostarle. È consigliabile archiviare tutte le password in un luogo sicuro in modo che non si dispone tooreset una password se si dimentichi. Se è necessario tooreset una password, essere toonotify che tutti gli utenti prima di reimpostarla. 

Interfaccia di Windows PowerShell hello è possibile accedere tramite un dispositivo toohello connessione seriale. È anche possibile accedervi in modalità remota usando HTTP o HTTPS, che offrono una maggiore sicurezza. HTTPS offre un livello più elevato di sicurezza rispetto a una connessione seriale o HTTP. Tuttavia, toouse HTTPS, è innanzitutto necessario installare un certificato nel computer client hello che avrà accesso dispositivo hello. È possibile scaricare il certificato di accesso remoto hello dalla pagina di configurazione dispositivo hello in hello servizio StorSimple Manager. Se il certificato di hello per l'accesso remoto viene perso, è necessario scaricare un nuovo certificato e propagarlo tooall client gestione remota toouse autorizzati.

### <a name="challenge-handshake-authentication-protocol-chap-initiator-and-target-passwords"></a>Password di destinazione e iniziatore CHAP (Challenge Handshake Authentication Protocol)
CHAP è uno schema di autenticazione utilizzato da hello identità hello toovalidate del dispositivo StorSimple di client remoti. verifica di Hello si basa su una password condivisa. CHAP può essere unidirezionale o bidirezionale (reciproco). Con CHAP unidirezionale, destinazione hello (dispositivo StorSimple hello) autentica un iniziatore (host). CHAP reciproco o inverso richiede che la destinazione hello autentica l'iniziatore di hello e successivamente hello iniziatore autentica destinazione di hello. StorSimple può essere dei metodi toouse configurato.

Tenere hello segue quando si configura il protocollo CHAP:

* nome utente Hello deve contenere meno di 233 caratteri.
* password CHAP Hello deve essere compreso tra 12 e 16 caratteri. Il tentativo di toouse un nome utente o una password più lungo comporterà un errore di autenticazione sull'host di Windows hello.
* Non è possibile utilizzare hello stessa password per l'iniziatore CHAP hello sia destinazione CHAP hello.
* Dopo aver impostato la password di hello, può essere modificata, ma non può essere recuperata. Se viene modificata la password di hello, essere toonotify che tutti gli utenti di accesso remoto in modo che possano connettersi correttamente il dispositivo di StorSimple toohello.

Per ulteriori informazioni sull'autenticazione CHAP e come tooconfigure per la soluzione StorSimple, andare troppo[configurare CHAP per il dispositivo StorSimple](storsimple-configure-chap.md).

### <a name="storsimple-snapshot-manager-password"></a>Password di Gestione snapshot StorSimple
Gestione Snapshot StorSimple è uno snap-in Microsoft Management Console (MMC) che utilizza gruppi di volumi e backup coerenti con l'applicazione toogenerate del servizio Copia Shadow del Volume di Windows hello. Inoltre, è possibile usare clone e gestione Snapshot StorSimple toocreate pianificazioni di backup o ripristinare volumi.

Quando si configura un toouse dispositivo StorSimple Snapshot Manager, sarà la password di StorSimple Snapshot Manager hello tooprovide obbligatorio. Questa password viene impostata in Windows PowerShell per StorSimple durante la registrazione. password Hello può anche essere impostata e modificata da hello servizio StorSimple Manager. Questa password autentica il dispositivo di hello StorSimple Snapshot Manager.

![Password di Gestione snapshot StorSimple](./media/storsimple-security/SnapshotMgrPassword.png)

password gestione Snapshot StorSimple Hello deve essere di 14 caratteri too15 e deve contenere 3 o più di una combinazione di caratteri maiuscoli, minuscoli, numerici e speciali. Dopo aver impostato la password di StorSimple Snapshot Manager hello, può essere modificata, ma non può essere recuperata. Se si modifica la password di hello, essere toonotify che tutti gli utenti remoti.

Per ulteriori informazioni su StorSimple Snapshot Manager, andare troppo[che cos'è StorSimple Snapshot Manager?](storsimple-what-is-snapshot-manager.md)

### <a name="password-best-practices"></a>Procedure consigliate per le password
È consigliabile utilizzare la seguente hello toohelp linee guida per assicurarsi che le password di StorSimple sono complesse e protette:

* Cambiare le password ogni tre mesi. Modifica delle password hello viene applicata all'anno.
* Usare password complesse. Per ulteriori informazioni, visitare troppo[creare password più complesse e proteggerli](http://blogs.microsoft.com/cybertrust/2014/08/25/create-stronger-passwords-and-protect-them/).
* Utilizzare sempre password diverse per i meccanismi di accesso diverso; ogni password hello specificata deve essere univoca.
* Non condividere le password con tutti gli utenti che non è un dispositivo StorSimple autorizzato tooaccess hello.
* Non parlare di una password davanti ad altri o Accennare al formato hello di una password.
* Se si ritiene che sia stato compromesso un account o password, report reparto di sicurezza delle informazioni di hello tooyour degli eventi imprevisti.
* Considerare tutte le password come informazioni sensibili e riservate. 

## <a name="storsimple-data-protection"></a>Protezione dei dati di StorSimple
Questa sezione vengono descritte le funzionalità di sicurezza StorSimple hello che proteggono i dati in transito e i dati archiviati.

Come descritto in altre sezioni, le password sono utilizzati tooauthorize e autenticare gli utenti prima di poter ottenere soluzione StorSimple tooyour di accesso. Un'altra considerazione sulla sicurezza riguarda la protezione dei dati dagli utenti non autorizzati durante il trasferimento da un sistema di archiviazione a un altro e durante l'archiviazione. Hello nelle sezioni seguenti vengono descritti le funzionalità di protezione dati hello fornite con StorSimple.

> [!NOTE]
> La deduplicazione offre una protezione aggiuntiva per i dati archiviati nel dispositivo StorSimple hello e nel servizio di archiviazione Microsoft Azure. Quando i dati sono deduplicati, oggetti dati hello archiviati separatamente dal toomap metadati utilizzati hello e accedervi: nessun dato di hello tooreconstruct contesto a livello di archiviazione disponibili in base volumi, file system o il nome di file.
> 
> 

## <a name="protect-data-flowing-through-hello-service"></a>Proteggere i dati che passano attraverso il servizio hello
scopo principale di Hello di hello servizio StorSimple Manager è toomanage e configurare il dispositivo di StorSimple hello. Hello servizio StorSimple Manager in esecuzione in Microsoft Azure. Si utilizza hello Azure tooenter portale classico dei dati di configurazione e quindi di utilizza hello StorSimple Manager toosend hello dati toohello dispositivo del servizio di Microsoft Azure. StorSimple utilizza un sistema di coppie di chiavi asimmetriche toohelp assicurarsi che una compromissione di hello servizio di Azure avrà come risultato non in grado di compromettere le informazioni memorizzate. 

![Crittografia dei dati in esecuzione](./media/storsimple-security/DataEncryption.png)

sistema della chiave asimmetrica Hello consente di proteggere i dati di hello che passa attraverso il servizio hello come indicato di seguito:

1. Un certificato di crittografia di dati che utilizza una coppia di chiavi pubblica e privata asimmetrica viene generato sul dispositivo hello e tooprotect utilizzati hello dati. Hello chiavi vengono generate quando hello primo dispositivo è registrato. 
2. Hello certificato le chiavi DEK vengono esportate in un file di scambio di informazioni personali (PFX) che è protetto da hello chiave DEK del servizio, che è una chiave a 128 bit complessa generata in modo casuale dal primo dispositivo hello durante la registrazione.
3. chiave pubblica di Hello del certificato di hello viene resa in modo sicuro disponibile toohello servizio StorSimple Manager e la chiave privata di hello rimane con il dispositivo hello.
4. Data immissione servizio hello viene crittografato con chiave pubblica di hello e decrittografati tramite la chiave privata hello archiviata sul dispositivo hello, assicurando che il servizio di Azure hello non può decrittografare dati hello propagazione toohello dispositivo.

Chiave DEK Hello viene generato solo hello primo dispositivo registrato con il servizio di hello. Tutti i dispositivi successivi che sono registrati con il servizio hello devono usare hello stessa chiave DEK del servizio. 

> [!IMPORTANT]
> È molto importante toomake una copia della chiave DEK del servizio hello e salvarlo in un luogo sicuro. Una copia della chiave DEK del servizio hello deve essere archiviata in modo che è possibile accedere a una persona autorizzata e può essere facilmente comunicata toohello amministratore del dispositivo.
> 
> Se chiave DEK hello viene perso, un addetto del supporto tecnico Microsoft consentono tooretrieve offriva di disporre di almeno un dispositivo in uno stato online. Si consiglia di modificare chiave DEK hello dopo averli recuperati. Per istruzioni, vedere troppo[chiave DEK del servizio modifica hello](storsimple-service-dashboard.md#change-the-service-data-encryption-key).
> 
> 

È possibile modificare chiave DEK hello e il corrispondente certificato di crittografia dei dati di hello selezionando hello **Modifica chiave DEK del servizio** opzione nel dashboard del servizio hello. tooensure che la protezione dei dati non è compromessa, è necessario utilizzare una fisico StorSimple dispositivo toochange hello chiave DEK del servizio. Modifica delle chiavi di crittografia hello, è necessario che tutti i dispositivi vengano aggiornati con chiave nuova hello. Pertanto, è consigliabile modificare la chiave hello quando tutti i dispositivi sono online. Se i dispositivi sono offline, le rispettive chiavi possono essere modificate in un altro momento. i dispositivi di Hello con la chiave scaduta saranno ancora in grado di toorun backup, ma non saranno in grado di toorestore dati finché non viene aggiornato chiave hello. Per ulteriori informazioni, visitare troppo[dashboard del servizio StorSimple Manager di utilizzare hello](storsimple-service-dashboard.md).

Chiave DEK Hello e certificato di crittografia dati hello non scadono. Tuttavia, si consiglia di modificare la crittografia dei dati di servizio hello chiave annualmente toohelp impedire compromissione della chiave.

## <a name="protect-data-at-rest"></a>Proteggere i dati inattivi
dispositivo StorSimple Hello gestisce i dati archiviandoli in più livelli localmente e nel cloud hello, a seconda della frequenza di utilizzo. Tutti i computer sono connessi toohello dispositivo invia dati toohello dispositivo, che quindi sposta dati toohello nel cloud, come appropriato host. Dati viene trasferiti dal cloud di toohello dispositivo hello in modo sicuro tramite Internet hello. Ogni dispositivo ha una destinazione iSCSI che copre tutti i volumi condivisi del dispositivo. Tutti i dati vengono crittografati prima che venga inviato toocloud archiviazione. 

![Chiave di crittografia di archiviazione cloud](./media/storsimple-security/CloudStorageEncryption.png)

toohelp garantire la sicurezza di hello e integrità dei dati spostati cloud toohello, StorSimple consente chiavi di crittografia archiviazione cloud toodefine come indicato di seguito:

* Chiave di crittografia archiviazione cloud hello è specificare quando si crea un contenitore del volume. chiave di Hello non può essere modificata o aggiunta in un secondo momento. 
* Tutti i volumi in una condivisione di contenitore di volume hello stessa chiave di crittografia. Se si desidera una forma diversa della crittografia per un volume specifico, è consigliabile creare un nuovo toohost contenitore volume tale volume.
* Quando si immette una chiave di crittografia archiviazione cloud hello in hello servizio StorSimple Manager, chiave di hello viene crittografata utilizzando hello parte pubblica della chiave DEK del servizio hello e quindi inviati toohello dispositivo.
* chiave di crittografia archiviazione cloud Hello non viene archiviata nel servizio hello ed è noto solo toohello dispositivo.
* Specificare una chiave di crittografia per l'archiviazione cloud è facoltativo. È possibile inviare i dati crittografati nel dispositivo di toohello hello host.

### <a name="additional-security-best-practices"></a>Procedure di sicurezza aggiuntive
* Suddividere il traffico: isolare la rete SAN iSCSI dal traffico utente in una LAN aziendale distribuendo una rete completamente separata e utilizzando le VLAN dove l’isolamento fisico non è un'opzione. Una rete dedicata per l'archiviazione iSCSI garantisce sicurezza hello e prestazioni dei dati aziendali critici. Combinare il traffico di archiviazione e il traffico utente su una rete LAN aziendale non è consigliato e può aumentare la latenza e causare errori di rete.
* Per la sicurezza di rete sul lato host, utilizzare le interfacce di rete che supportano il protocollo TCP/IP Offload Engine (TOE). TOE riduce il carico della CPU elaborando TCP nella scheda di rete hello.

## <a name="protect-data-via-storage-accounts"></a>Proteggere i dati mediante gli account di archiviazione
Ogni sottoscrizione di Microsoft Azure può creare uno o più account di archiviazione. (Un account di archiviazione fornisce uno spazio dei nomi univoco per l'utilizzo di dati archiviati nel cloud di Azure hello). Account di archiviazione tooa di accesso è controllato dalle chiavi di accesso e di sottoscrizione di hello associate a tale account di archiviazione. 

Quando si crea un account di archiviazione, Microsoft Azure genera due chiavi di accesso di archiviazione a 512 bit, uno dei quali viene utilizzato per l'autenticazione del dispositivo StorSimple hello accede account di archiviazione hello. Una sola di queste chiavi è in uso. altra chiave Hello è tenuta di riserva è toorotate hello chiavi periodicamente. chiavi toorotate, rendere chiave secondaria hello active e chiave primaria hello di eliminazione. È quindi possibile creare una nuova chiave per l'utilizzo durante la rotazione successiva hello. Per motivi di sicurezza, molti data center richiedono la rotazione delle chiavi. 

Per la rotazione delle chiavi, è opportuno seguire queste procedure consigliate:

* È consigliabile ruotare chiavi account di archiviazione regolarmente toohelp assicurarsi che l'account di archiviazione non è accessibile da utenti non autorizzati.
* Periodicamente, l'amministratore di Azure deve modificare o rigenerare la chiave primaria o secondaria hello hello nella sezione archiviazione di account di archiviazione di Azure toodirectly portale classico accesso hello hello.

## <a name="protect-data-via-encryption"></a>Proteggere i dati mediante la crittografia
StorSimple Usa hello seguono gli algoritmi di crittografia tooprotect dati archiviati in o in viaggio tra i componenti di hello della soluzione StorSimple.

| Algoritmo | Lunghezza chiave | Protocolli/applicazioni/commenti |
| --- | --- | --- |
| RSA |2048 |RSA PKCS 1 v 1.5 viene usato da Azure tooencrypt portale classico i dati di configurazione che viene inviati toohello dispositivo hello: ad esempio, l'archiviazione delle credenziali, configurazione del dispositivo StorSimple, degli account e le chiavi di crittografia archiviazione cloud. |
| AES |256 |AES con CBC è parte pubblica di hello tooencrypt utilizzato della chiave DEK del servizio hello prima di essere inviato dal dispositivo StorSimple hello toohello portale di Azure classico. Anche usato dai hello StorSimple dispositivo tooencrypt dati prima dell'invio dei dati hello toohello account di archiviazione cloud. |

## <a name="storsimple-virtual-device-security"></a>Sicurezza del dispositivo virtuale StorSimple
[!INCLUDE [storsimple virtual device security](../../includes/storsimple-virtual-device-security.md)]

## <a name="frequently-asked-questions-faq"></a>Domande frequenti
Hello di seguito è riportate alcune domande e risposte relative alla sicurezza e di Microsoft Azure StorSimple.

**D:** Il servizio è compromesso. Quali sono i passaggi successivi da eseguire?

**R:** è necessario modificare hello chiave DEK del servizio e chiavi di account di archiviazione hello hello account di archiviazione viene usato per suddividere in livelli i dati. Per istruzioni, vedere: 

* [Modifica chiave DEK del servizio hello](storsimple-service-dashboard.md#change-the-service-data-encryption-key)
* [Rotazione delle chiavi degli account di archiviazione](storsimple-manage-storage-accounts.md#key-rotation-of-storage-accounts)

**Q:** ho un nuovo dispositivo StorSimple che richiede un tipo di chiave di registrazione del servizio hello. Come posso ottenerla?

**R:** questa chiave è stata creata al momento della creazione del servizio StorSimple Manager hello. Quando si utilizza dispositivo toohello tooconnect del servizio StorSimple Manager di hello, è possibile utilizzare tooview pagina avvio rapido del servizio di hello o chiave di registrazione del servizio hello rigenerare. Generare una nuova chiave di registrazione del servizio, i dispositivi registrati esistenti hello non verranno applicate. Per istruzioni, vedere:

* [Consente di visualizzare o rigenerare la chiave di registrazione del servizio hello](storsimple-service-dashboard.md#view-or-regenerate-the-service-registration-key)

**D:** Ho perso la chiave DEK del servizio. Cosa devo fare?

**R:** Contattare il supporto Microsoft. Per poter accedere tooa sessione di supporto nel dispositivo e aiutare a recuperare la chiave hello (purché almeno un dispositivo sia in linea). Immediatamente dopo aver ottenuto una chiave di crittografia di hello servizio dati, è consigliabile modificarlo tooensure tale nuova chiave hello è noto solo tooyou. Per istruzioni, vedere:

* [Modifica chiave DEK del servizio hello](storsimple-service-dashboard.md#change-the-service-data-encryption-key)

**Q:** autorizzato un dispositivo per una modifica della chiave DEK del servizio, ma non è stato avviato il processo di modifica hello. Cosa devo fare?

**R:** se hello periodo di timeout è scaduto, sarà anche necessario dispositivo hello tooreauthorize per hello servizio modifica della chiave DEK e avviare di nuovo il processo di hello.

**Q:** in seguito alla modifica chiave DEK hello, ma non ho potuto tooupdate hello altri dispositivi entro le 4 ore. È necessario toostart nuovamente?

**R:** hello periodo di 4 ore è solo per l'avvio del processo hello modifica. Dopo avere avviato il processo di aggiornamento hello in hello autorizzato dispositivo StorSimple, autorizzazione hello è valido fino a quando non vengono aggiornati tutti i dispositivi.

**Q:** l'amministratore di StorSimple ha lasciato l'azienda di hello. Cosa devo fare?

**R:** modificare e reimpostare le password che consentono di dispositivo StorSimple toohello di accesso e modificare hello servizio dati crittografia chiave tooensure che le nuove informazioni hello non sono noto toounauthorized personale di hello. Per istruzioni, vedere:

* [Utilizzare toochange servizio StorSimple Manager di hello le password di storsimple](storsimple-change-passwords.md)
* [Modifica chiave DEK del servizio hello](storsimple-service-dashboard.md#change-the-service-data-encryption-key)
* [Configurare CHAP per il dispositivo StorSimple](storsimple-configure-chap.md)

**Q:** voglio tooprovide hello gestione Snapshot StorSimple password tooa host che si connette il dispositivo di StorSimple toohello ma hello password non è disponibile. In che modo è possibile risolvere questo problema?

**R:** se hai dimenticato la password di hello, è necessario crearne uno nuovo. Quindi, assicurarsi che tooinform tutti gli utenti esistenti che hello password è stata modificata e che devono aggiornare i relativi toouse client hello nuova password. Per istruzioni, vedere:

* [Modificare la password di StorSimple Snapshot Manager hello](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password)
* [Autenticazione di un dispositivo](storsimple-snapshot-manager-manage-devices.md#authenticate-a-device)

**Q:** certificato hello per toohello di accesso remoto di Windows PowerShell per StorSimple è stato modificato sul dispositivo hello. Come posso aggiornare i client di accesso remoto?

**R:** è possibile scaricare il nuovo certificato di hello dal servizio StorSimple Manager hello e quindi inviarlo toobe installato nell'archivio di certificati hello del client di accesso remoto. Per istruzioni, vedere:

* [Cmdlet Import-Certificate](https://technet.microsoft.com/library/hh848630.aspx)

**Q:** miei dati sono protetti se viene compromesso hello servizio StorSimple Manager?

**R:** I dati di configurazione del servizio sono sempre crittografati con la chiave pubblica quando vengono visualizzati in un Web browser. Perché servizio hello non ha una chiave privata toohello di accesso, il servizio di hello non essere in grado di toosee tutti i dati. Se il servizio StorSimple Manager hello è compromesso, non l'impatto è perché non sono presenti chiavi archiviate in hello servizio StorSimple Manager.

**Q:** se un utente ottiene il certificato di crittografia dati toohello di accesso, verranno miei dati verranno compromessi?

**R:** Microsoft Azure Archivia chiave DEK del cliente hello (file con estensione pfx) in un formato crittografato. Poiché verrà crittografati i file con estensione pfx hello e hello servizio StorSimple non dispone di file con estensione pfx hello servizio dati crittografia chiave toodecrypt hello, semplicemente file con estensione pfx toohello di accesso non espone alcun dato segreto.

**D:** Cosa accade se un ente pubblico chiede i miei dati a Microsoft?

**R:** perché tutti i dati di hello vengono crittografati nel servizio hello e hello chiave privata viene mantenuta con dispositivo hello, hello governativa entità deve richiedere hello cliente dati hello. 

## <a name="next-steps"></a>Passaggi successivi
[Distribuire il dispositivo StorSimple](storsimple-deployment-walkthrough.md).

