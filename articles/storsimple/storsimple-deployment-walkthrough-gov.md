---
title: dispositivo StorSimple aaaDeploy nel portale amministrativo | Documenti Microsoft
description: Descrive i passaggi di hello e procedure consigliate per la distribuzione dispositivo hello StorSimple Update 1 e il servizio nel portale di Azure per enti pubblici hello.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 3fe3648d-e0b6-4928-a2cb-8d3ccc50d62a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/17/2016
ms.author: v-sharos
ms.openlocfilehash: 045c838a28efc92d0f67ae3bab2a7393d1badc12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-in-hello-government-portal"></a>Distribuire il dispositivo StorSimple locale nel portale amministrativo hello
[!INCLUDE [storsimple-version-selector-deploy-gov](../../includes/storsimple-version-selector-deploy-gov.md)]

## <a name="overview"></a>Panoramica
Benvenuto nella distribuzione del dispositivo Azure StorSimple tooMicrosoft. Queste esercitazioni per la distribuzione applica toohello StorSimple 8000 Series in esecuzione 1 aggiornamento software nel portale di Azure per enti pubblici hello. Questa serie di esercitazioni viene descritto come tooconfigure dispositivo StorSimple e include un elenco di controllo di configurazione, i prerequisiti di configurazione e i dettagli della configurazione passaggi.

informazioni Hello in queste esercitazioni si presuppongono che si hanno esaminato precauzioni di sicurezza hello e decompressi, centralizzato in remoto e cablato dispositivo StorSimple. Se è ancora necessario tooperform quelle attività, iniziare con revisione hello [precauzioni di sicurezza](storsimple-safety.md). A seconda del modello di dispositivo, quindi è possibile decomprimere, montaggio in rack e cavo seguendo le istruzioni di hello in:

* [Decomprimere, montare su rack e cablare il dispositivo 8100](storsimple-8100-hardware-installation.md)
* [Decomprimere, montare su rack e cablare il dispositivo 8600](storsimple-8600-hardware-installation.md)

Sarà necessario amministratore privilegi toocomplete hello il programma di installazione e configurazione processo. È consigliabile rivedere l'elenco di controllo configurazione hello prima di iniziare. processo di distribuzione e la configurazione di Hello può richiedere alcuni toocomplete ora.

> [!NOTE]
> informazioni sulla distribuzione di StorSimple Hello pubblicate sul sito Web di Microsoft Azure hello applica tooStorSimple solo dispositivi della serie 8000. Per informazioni complete sui dispositivi serie 7000 hello, visitare: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com). Per informazioni sulla distribuzione di 7000 serie, vedere hello [StorSimple Guida introduttiva del sistema](http://onlinehelp.storsimple.com/111_Appliance/).
> 
> 

## <a name="deployment-steps"></a>Passaggi di distribuzione
Eseguire questi tooconfigure passaggi obbligatori del dispositivo StorSimple e connetterla servizio StorSimple Manager tooyour. Inoltre toohello necessari passaggi, vi sono passaggi facoltativi e le procedure che necessari durante la distribuzione di hello. istruzioni dettagliate di distribuzione Hello indicano quando è necessario eseguire ognuno di questi passaggi facoltativi.

| Passaggio | Descrizione |
| --- | --- |
| **PREREQUISITI** |Questi devono toobe completata in preparazione per la distribuzione di hello future. |
| Elenco di controllo configurazione della distribuzione. |Utilizzare questo elenco di controllo toogather e registra le informazioni precedenti tooand durante la distribuzione di hello. |
| Prerequisiti di distribuzione. |Questi convalidare hello ambiente è pronto per la distribuzione. |
|  | |
| **DISTRIBUZIONE PASSO PER PASSO** |Questi passaggi sono necessari toodeploy dispositivo StorSimple nell'ambiente di produzione. |
| Passaggio 1: Creare un nuovo servizio. |Configurare la gestione del cloud e l'archiviazione per il dispositivo StorSimple. Ignorare questo passaggio se si dispone di un servizio esistente per altri dispositivi StorSimple. |
| Passaggio 2: Ottenere una chiave di registrazione del servizio hello. |Utilizzare questa chiave tooregister & connettere il dispositivo StorSimple con il servizio di gestione di hello. |
| Passaggio 3: Configurare e registrare il dispositivo hello tramite Windows PowerShell per StorSimple. |Connessione di rete di tooyour hello dispositivo e registrarlo con il programma di installazione di Azure toocomplete hello mediante il servizio di gestione di hello. |
| Passaggio 4: Completare l'installazione minima del dispositivo</br>Facoltativo: aggiornare il dispositivo StorSimple. |Utilizzare l'installazione di dispositivi di hello Gestione servizio toocomplete hello e abilitarlo tooprovide archiviazione. |
| Passaggio 5: Creare un contenitore di volumi. |Creare un contenitore di volumi tooprovision. Un contenitore di volumi sono account di archiviazione, della larghezza di banda e le impostazioni di crittografia per tutti i volumi di hello in esso contenuti. |
| Passaggio 6: Creare un volume. |Eseguire il provisioning di volumi di archiviazione nel dispositivo StorSimple hello per i server. |
| Passaggio 7: Montare, inizializzare e formattare un volume.</br>Facoltativo: Configurare MPIO. |Connettere l'archiviazione iSCSI di toohello server fornito dal dispositivo hello. Se si desidera configurare MPIO tooensure che i server in grado di tollerare errori dell'interfaccia, rete e collegamento. |
| Passaggio 8: Eseguire un backup. |Impostare tooprotect il criterio di backup dei dati |
|  | |
| **ALTRE PROCEDURE** |Procedure toothese toorefer potrebbe essere necessario quando si distribuisce la soluzione. |
| Configurare un nuovo account di archiviazione per il servizio di hello. | |
| Usare PuTTY tooconnect toohello console seriale del dispositivo. | |
| Cercare e applicare gli aggiornamenti. | |
| Ottenere hello nome qualificato iSCSI di un host Windows Server. | |
| Creare un backup manuale. | |
| Configurare MPIO. | |

## <a name="deployment-configuration-checklist"></a>Elenco di controllo configurazione della distribuzione
Hello seguente elenco di controllo configurazione distribuzione descrive informazioni hello necessarie toocollect prima e durante la configurazione software hello nel dispositivo StorSimple. Alcune di queste informazioni anticipatamente preparazione consente di semplificare il processo di hello del dispositivo StorSimple hello nell'ambiente di distribuzione. Utilizzare questa nota tooalso elenco di controllo per le modalità di configurazione di hello quando si distribuisce il dispositivo.

| Fase | Parametro | Dettagli | Valori |
| --- | --- | --- | --- |
| **Cablare il dispositivo** |Accesso seriale |Configurazione iniziale del dispositivo |Sì/No |
|  | | | |
| **Configurare e registrare il dispositivo** |Impostazioni di rete Data 0 |Indirizzo IP Data 0:</br>Subnet mask:</br>Gateway:</br>Server DNS primario:</br>Server NTP primario:</br>IP/FQDN server proxy Web (facoltativo):</br>porta proxy Web: | |
| &nbsp; |Password amministratore del dispositivo |La password deve avere una lunghezza compresa tra gli 8 e i 15 caratteri e deve contenere minuscole, maiuscole, numeri e caratteri speciali. | |
| &nbsp; |Password di Gestione snapshot StorSimple |La password deve avere una lunghezza compresa tra i 14 e i 15 caratteri e deve contenere caratteri minuscoli, maiuscoli, numerici e speciali. | |
| &nbsp; |Chiave di registrazione del servizio |Questa chiave viene generata da hello portale di Azure. | |
| &nbsp; |Chiave DEK del servizio |Questa chiave viene creata quando il dispositivo di hello è registrato con il servizio di gestione di hello tramite hello Windows PowerShell per StorSimple. Copiare questo codice e salvarlo in un luogo sicuro. | |
|  | | | |
| **Completare la configurazione minima del dispositivo** |Nome descrittivo del dispositivo |Si tratta di un nome descrittivo per il dispositivo hello. | |
| &nbsp; |Fuso orario |Il dispositivo utilizzerà questo fuso orario per tutte le operazioni pianificate. | |
| &nbsp; |Server DNS secondario |Si tratta di una configurazione necessaria. | |
| &nbsp; |Interfaccia di rete: controller IP fissi del controller Data 0 |Questi indirizzi IP deve essere toohello instradabile su Internet.</br>Indirizzo IP fisso controller 0:</br>indirizzo IP fisso controller 1: | |
|  | | | |
| **Impostazioni interfaccia di rete aggiuntive** |Interfaccia di rete: Data 1</br>ISCSI è abilitato, non configurare hello Gateway. |Scopo: Cloud/ISCSI/non utilizzato</br>Indirizzo IP:</br>Subnet mask:</br>Gateway: | |
| &nbsp; |Interfaccia di rete: Data 2</br>ISCSI è abilitato, non configurare hello Gateway. |Scopo: Cloud/ISCSI/non utilizzato</br>Indirizzo IP:</br>Subnet mask:</br>Gateway: | |
| &nbsp; |Interfaccia di rete: Data 3</br>ISCSI è abilitato, non configurare hello Gateway. |Scopo: Cloud/ISCSI/non utilizzato</br>Indirizzo IP:</br>Subnet mask:</br>Gateway: | |
| &nbsp; |Interfaccia di rete: Data 4</br>ISCSI è abilitato, non configurare hello Gateway. |Scopo: Cloud/ISCSI/non utilizzato</br>Indirizzo IP:</br>Subnet mask:</br>Gateway: | |
| &nbsp; |Interfaccia di rete: Data 5</br>ISCSI è abilitato, non configurare hello Gateway. |Scopo: Cloud/ISCSI/non utilizzato</br>Indirizzo IP:</br>Subnet mask:</br>Gateway: | |
|  | | | |
| **Creare un contenitore di volumi** |Nome del contenitore di volume: |Nome contenitore hello | |
| &nbsp; |Account di archiviazione Azure: |Storage account access & nome chiave tooassociate con questo contenitore del volume | |
| &nbsp; |Chiave di crittografia di archiviazione cloud: |Chiave di crittografia per l'archiviazione in ogni contenitore | |
|  | | | |
| **Creare un volume** |Dettagli per ogni volume |Nome del volume: | |
| &nbsp; |&nbsp; |Dimensione: | |
| &nbsp; |&nbsp; |Tipo di utilizzo: | |
| &nbsp; |&nbsp; |Nome ACR: | |
| &nbsp; |&nbsp; |Criteri di backup predefinito: | |
|  | | | |
| **Montare, inizializzare e formattare un volume** |Dettagli per ogni server host connessione toohello archiviazione |Nome del Server di Windows: | |
| &nbsp; |&nbsp; |Windows Server nome qualificato iSCSI: | |
| &nbsp; |&nbsp; |Nome di volume di Windows Server: | |
| &nbsp; |&nbsp; |Lettera di unità o punti di montaggio NTFS: | |

## <a name="deployment-prerequisites"></a>Prerequisiti di distribuzione
Hello le sezioni seguenti vengono illustrati i prerequisiti di configurazione hello per il servizio StorSimple Manager e il dispositivo StorSimple.

### <a name="for-hello-storsimple-manager-service"></a>Per hello servizio StorSimple Manager
Prima di iniziare, verificare che:

* Si dispone dell'account Microsoft con credenziali di accesso.
* Si dispone dell'account di archiviazione di Microsoft Azure con credenziali di accesso.
* Sottoscrizione di Microsoft Azure è abilitata per hello servizio StorSimple Manager. La sottoscrizione deve essere acquistata tramite hello [contratto Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).
* Si dispone di accesso tooterminal emulazione software, ad esempio PuTTY.

### <a name="for-hello-device-in-hello-datacenter"></a>Per il dispositivo hello in Data Center hello
Prima di configurare il dispositivo di hello, verificare quanto segue:

* Il dispositivo è completamente disimballato, montato su un rack e cablato per l’alimentazione, la rete e l’accesso seriale come descritto in:
  
  * [Decomprimere, montare su rack e cablare il dispositivo 8100](storsimple-8100-hardware-installation.md)
  * [Decomprimere, montare su rack e cablare il dispositivo 8600](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a>Per la rete hello in Data Center hello
Prima di iniziare, verificare che:

* Hello porte nel firewall datacenter sono tooallow aperto per il traffico iSCSI e cloud come descritto in [requisiti di rete per il dispositivo StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).

## <a name="step-by-step-deployment"></a>DISTRIBUZIONE PASSO PER PASSO
Utilizzare hello seguendo le istruzioni dettagliate toodeploy dispositivo StorSimple in Data Center hello.

## <a name="step-1-create-a-new-service"></a>Passaggio 1: Creare un nuovo servizio
Un servizio StorSimple Manager può gestire più dispositivi StorSimple. Eseguire i seguenti passaggi toocreate una nuova istanza del servizio StorSimple Manager hello hello.

[!INCLUDE [storsimple-create-new-service-gov](../../includes/storsimple-create-new-service-gov.md)]

> [!IMPORTANT]
> Se non si abilita la creazione automatica di un account di archiviazione hello con il servizio, sarà necessario toocreate almeno un account di archiviazione, dopo avere creato un servizio. Tale account di archiviazione verrà utilizzato in fase di creazione di un contenitore di volumi.
> 
> * Se non è stato creato automaticamente un account di archiviazione, andare troppo[configurare un nuovo account di archiviazione per il servizio hello](#configure-a-new-storage-account-for-the-service) per istruzioni dettagliate.
> * Se è abilitata la creazione automatica di hello di un account di archiviazione, andare troppo[passaggio 2: chiave di registrazione del servizio Get hello](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>Passaggio 2: Ottenere una chiave di registrazione del servizio hello
Dopo aver hello servizio StorSimple Manager sia in esecuzione, sarà necessario chiave di registrazione del servizio tooget hello. Questa chiave è tooregister utilizzato e connettersi al servizio di toohello dispositivo StorSimple.

Eseguire i passaggi hello portale amministrativo hello.

[!INCLUDE [storsimple-get-service-registration-key-gov](../../includes/storsimple-get-service-registration-key-gov.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>Passaggio 3: Configurare e registrare il dispositivo hello tramite Windows PowerShell per StorSimple
Usare Windows PowerShell per StorSimple toocomplete hello la configurazione iniziale del dispositivo StorSimple, come illustrato nella seguente procedura hello. È necessario toocomplete software di emulazione di terminale toouse questo passaggio. Per ulteriori informazioni, vedere [console seriale del dispositivo usare PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console).

[!INCLUDE [storsimple-configure-and-register-device-gov](../../includes/storsimple-configure-and-register-device-gov.md)]

## <a name="step-4-complete-minimum-device-setup"></a>Passaggio 4: Completare l'installazione minima del dispositivo
Per la configurazione minima del dispositivo di hello del dispositivo StorSimple, verrà richiesto di:

* Impostare il server DNS secondario hello.
* Abilitare iSCSI in almeno un'interfaccia di rete.
* Assegnare indirizzi IP fisso controller hello tooboth.

Eseguire hello alla procedura seguente nel programma di installazione di hello portale amministrativo toocomplete hello minima del dispositivo.

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a>Passaggio 5: Creare un contenitore di volumi
Un contenitore di volumi sono account di archiviazione, della larghezza di banda e le impostazioni di crittografia per tutti i volumi di hello in esso contenuti. Sarà necessario toocreate un contenitore del volume prima di poter avviare il provisioning di volumi nel dispositivo StorSimple.

Eseguire i passaggi hello portale amministrativo toocreate un contenitore di volumi hello.

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>Passaggio 6: Creare un volume
Dopo aver creato un contenitore di volumi, è possibile eseguire il provisioning di un volume di archiviazione nel dispositivo StorSimple hello per i server. Eseguire i passaggi hello portale amministrativo toocreate un volume hello.

> [!IMPORTANT]
> StorSimple di Azure consente di creare solo volumi di thin provisioning.  Non è possibile creare volumi con provisioning completo o parziale in un sistema StorSimple di Azure.
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>Passaggio 7: Montare, inizializzare e formattare un volume
Eseguire questi passaggi nell'host di Windows Server.

> [!IMPORTANT]
> * Per la disponibilità elevata hello della soluzione StorSimple, è consigliabile configurare MPIO in iSCSI di tooconfiguring precedente server (facoltativo) l'host. Configurazione MPIO sui server host garantisce che i server hello in grado di tollerare un collegamento, rete o errori dell'interfaccia.
> * Per MPIO e iSCSI istruzioni installazione e configurazione in host Windows Server, visitare troppo[configurare MPIO per il dispositivo StorSimple](storsimple-configure-mpio-windows-server.md). Questi anche verrà includono hello passaggi toomount, inizializzare e formattare volumi StorSimple.
> * Per MPIO e iSCSI istruzioni installazione e configurazione in un host Linux, andare troppo[configurare MPIO per l'host StorSimple Linux](storsimple-configure-mpio-on-linux.md)
> 
> 

Se si decide di non tooconfigure MPIO, esegue hello seguendo i passaggi toomount, inizializzare e formattare i volumi StorSimple su un host Windows Server.

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>Passaggio 8: Eseguire un backup
I backup garantiscono la protezione temporizzata dei volumi e migliorano la recuperabilità riducendo al minimo i tempi di ripristino. È possibile eseguire due tipi di backup su un dispositivo StorSimple: snapshot locali e snapshot nel cloud. Ciascuno di questi tipi di backup può essere **pianificato** o **manuale**.

Eseguire i passaggi hello portale amministrativo toocreate un backup pianificato hello.

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

È possibile eseguire un backup manuale in qualsiasi momento. Per le procedure, andare troppo[creare un backup manuale](#create-a-manual-backup).

## <a name="configure-a-new-storage-account-for-hello-service"></a>Configurare un nuovo account di archiviazione per il servizio hello
Questo è un passaggio facoltativo che è necessario tooperform solo se non si abilita la creazione automatica di un account di archiviazione hello con il servizio. Un account di archiviazione di Microsoft Azure è un contenitore di volumi StorSimple di toocreate obbligatorio.

Se è necessario un account di archiviazione di Azure in un'area diversa toocreate, vedere [informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md) per istruzioni dettagliate.

Eseguire i passaggi hello portale amministrativo, in hello hello **servizio StorSimple Manager** pagina.

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>Utilizzare una console seriale del dispositivo toohello tooconnect PuTTY
tooconnect tooWindows PowerShell per StorSimple, è necessario software di emulazione di terminale toouse, ad esempio PuTTY. È possibile usare PuTTY quando si accede dispositivo hello direttamente tramite la console seriale hello o aprendo una sessione telnet da un computer remoto.

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>Cercare e applicare gli aggiornamenti
L’aggiornamento del dispositivo può richiedere diverse ore. Eseguire seguendo i passaggi tooscan per hello e applicare gli aggiornamenti nel dispositivo.

<!--If you have a gateway configured on a network interface other than Data 0, you will need toodisable Data 2 and Data 3 network interfaces before installing hello update. Go too**Devices > Configure** and disable Data 2 and Data 3 interfaces. You should re-enable these interfaces after hello device is updated.-->

#### <a name="tooupdate-your-device"></a>tooupdate del dispositivo
1. Nel dispositivo hello **avvio rapido** pagina, fare clic su **dispositivi**. Selezionare il dispositivo fisico di hello, fare clic su **manutenzione** e quindi fare clic su **analisi aggiornamenti**.  
2. Viene creato un processo tooscan per gli aggiornamenti disponibili. Se sono disponibili aggiornamenti, hello **analisi aggiornamenti** cambia troppo**Installa aggiornamenti**. Fare clic su **Installa aggiornamenti**.
3. Verrà creato un processo di aggiornamento. Monitorare l'aggiornamento di stato hello passando troppo**processi**.
   
   > [!NOTE]
   > Quando viene avviato il processo di aggiornamento di hello, visualizza immediatamente hello stato pari a 50. stato di Hello cambia percentuale too100 solo al termine del processo di aggiornamento hello. Non vi sono stati in tempo reale per il processo di aggiornamento hello.
   > 
   > 
4. Dopo aver completato l'aggiornamento dispositivo hello, abilitare le interfacce di rete Data 2 e Data 3 se questi sono stati disabilitati.

## <a name="get-hello-iqn-of-a-windows-server-host"></a>Ottenere hello nome qualificato iSCSI di un host Windows Server
Eseguire i seguenti passaggi tooget hello iSCSI hello nome qualificato di un host Windows che esegue Windows Server® 2012.

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>Creare un backup manuale
Eseguire i passaggi backup manuale hello portale amministrativo toocreate una richiesta per un singolo volume nel dispositivo StorSimple hello.

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup-gov.md)]

## <a name="configure-mpio"></a>Configurare MPIO
Multipath I/O (MPIO) è una funzionalità facoltativa e non è installata in Windows Server per impostazione predefinita. Deve essere installata come funzionalità tramite Server Manager. Per istruzioni sull'installazione di MPIO, andare troppo[configurare MPIO per il dispositivo StorSimple](storsimple-configure-mpio-windows-server.md).

Per istruzioni sull'installazione di MPIO per un dispositivo StorSimple tooa connesso host Linux andare troppo[configurare MPIO per l'host Linux](storsimple-configure-mpio-on-linux.md).

> [!NOTE]
> La funzionalità MPIO non è supportata in un dispositivo virtuale StorSimple.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* Configurare un [dispositivo virtuale](storsimple-virtual-device-u2.md).
* Hello utilizzare [servizio StorSimple Manager](https://msdn.microsoft.com/library/azure/dn772396.aspx) toomanage dispositivo StorSimple.

