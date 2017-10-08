---
title: dispositivo virtuale aaaStorSimple Update 2 | Documenti Microsoft
description: Informazioni su come toocreate, distribuire e gestire un dispositivo virtuale StorSimple in una rete virtuale di Microsoft Azure. (Si applica tooStorSimple Update 2).
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: f37752a5-cd0c-479b-bef2-ac2c724bcc37
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.openlocfilehash: 8d2a0520f1ed30ebec929c2bdabb4838691b8ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-a-storsimple-virtual-device-in-azure"></a>Distribuire e gestire un dispositivo virtuale StorSimple in Azure
## <a name="overview"></a>Panoramica
Hello dispositivo StorSimple serie 8000 virtuale è una funzionalità aggiuntiva fornita con la soluzione di Microsoft Azure StorSimple. dispositivo virtuale StorSimple Hello viene eseguito in una macchina virtuale in una rete virtuale di Microsoft Azure e utilizzarlo tooback backup e clone dati dagli host. Questa esercitazione viene descritto come toodeploy e gestire un dispositivo virtuale in Azure ed è tooall applicabile per i dispositivi virtuali hello esegue la versione software Update 2 e inferiore.

#### <a name="virtual-device-model-comparison"></a>Confronto tra modelli di dispositivi virtuali
Hello StorSimple dispositivo virtuale è disponibile in due modelli, un standard 8010: spazio (precedentemente noto come hello 1100) e un premium 8020 (introdotta in Update 2). Un confronto tra due modelli di hello è inserito sotto.

| Modello del dispositivo | 8010<sup>1</sup> | 8020 |
| --- | --- | --- |
| **Capacità massima** |30 TB |64 TB |
| **Macchina virtuale di Azure** |Standard_A3 (4 core, 7 GB di memoria) |Standard_DS3 (4 core, 14 GB di memoria) |
| **Compatibilità tra le versioni** |Versioni con aggiornamenti precedenti a Update 2 o successivi |Versioni con aggiornamenti Update 2 o successivi |
| **Aree di disponibilità** |Tutte le aree di Azure |Tutte le aree di Azure che supportano Archiviazione Premium e VM DS3 di Azure<br></br> Utilizzare [questo elenco](https://azure.microsoft.com/en-us/regions/services) toosee se entrambi *macchine virtuali > serie DS* e *archiviazione > lo spazio su disco* sono disponibili nel proprio paese. |
| **Tipo di archiviazione** |Usa l'Archiviazione Standard di Azure<br></br> Informazioni su come troppo[creare un account di archiviazione Standard](../storage/common/storage-create-storage-account.md) |Usa l'Archiviazione Standard di Azure<sup>2</sup> <br></br>Informazioni su come troppo[creare un account di archiviazione Premium](../storage/common/storage-premium-storage.md) |
| **Indicazioni relative al carico di lavoro** |Recupero a livello di elemento per i file dai backup |Scenari di sviluppo e test cloud, bassa latenza, carichi di lavoro a prestazioni superiori  <br></br>Dispositivo secondario per il ripristino di emergenza |

<sup>1</sup> *precedentemente noto come hello 1100*.

<sup>2</sup> *entrambi hello 8010: spazio e 8020 utilizzare l'archiviazione di Azure Standard per hello cloud livello hello differenza esiste solo nel livello di locale hello all'interno di dispositivo hello*.

Questo articolo descrive hello passaggi della procedura guidata di distribuzione di un dispositivo virtuale StorSimple in Azure. Dopo avere letto l'articolo, si sarà in grado di:

* Comprendere le differenze tra la periferica virtuale hello dal dispositivo fisico hello.
* Essere in grado di toocreate e configurare la periferica virtuale hello.
* Connettere la periferica virtuale toohello.
* Informazioni su come toowork con dispositivo virtuale hello.

Questa esercitazione si applica tooall hello dispositivi virtuali StorSimple esecuzione Update 2 e versioni successive.

## <a name="how-hello-virtual-device-differs-from-hello-physical-device"></a>Differenze di dispositivo virtuale hello dal dispositivo fisico hello
dispositivo virtuale StorSimple Hello è una versione solo software di StorSimple, eseguita in un singolo nodo in una macchina virtuale di Microsoft Azure. Hello dispositivo virtuale supporta ripristino di emergenza in cui non è disponibile, il dispositivo fisico ed è appropriato per l'utilizzo in un recupero a livello di elemento dal backup, ripristino di emergenza, locale e cloud di sviluppo e scenari di test.

#### <a name="differences-from-hello-physical-device"></a>Differenze rispetto a dispositivo fisico hello
Hello nella tabella seguente mostra alcune differenze fondamentali tra dispositivo virtuale StorSimple hello e dispositivo fisico StorSimple hello.

|  | Dispositivo fisico | Dispositivo virtuale |
| --- | --- | --- |
| **Posizione** |Si trova nel Data Center hello. |Viene eseguito in Azure. |
| **Interfacce di rete** |Ha sei interfacce di rete: da DATA 0 a DATA 5. |Ha una sola interfaccia di rete: DATA 0. |
| **Registrazione** |Registrato durante il passaggio di configurazione di hello. |La registrazione è un'attività separata. |
| **Chiave DEK del servizio** |Rigenerare sul dispositivo fisico hello e quindi aggiornare la periferica virtuale hello con chiave nuova hello. |Impossibile rigenerare dal dispositivo virtuale hello. |

## <a name="prerequisites-for-hello-virtual-device"></a>Prerequisiti per il dispositivo virtuale hello
Hello nelle sezioni seguenti illustrano i prerequisiti di configurazione hello per il dispositivo virtuale StorSimple. Toodeploying precedente un dispositivo virtuale, esaminare hello [considerazioni sulla sicurezza per l'utilizzo di un dispositivo virtuale](storsimple-security.md#storsimple-virtual-device-security).

#### <a name="azure-requirements"></a>Requisiti di Azure
Prima eseguire il provisioning di dispositivo virtuale hello, è necessario hello toomake seguente preparati nell'ambiente Azure:

* Per il dispositivo virtuale hello, [configurare una rete virtuale in Azure](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Se si usa l'archiviazione Premium, sarà necessario creare una rete virtuale in un'area di Azure che supporta l'archiviazione Premium. aree di archiviazione Premium Hello sono aree corrispondenti riga toohello per *lo spazio su disco* nell'elenco di hello di [servizi di Azure dall'area](https://azure.microsoft.com/en-us/regions/services).
* È un server DNS predefinito hello toouse consigliabile fornita da Azure anziché specificare nome del server DNS. Se il nome del server DNS non è valido o se hello server DNS non è in grado di tooresolve indirizzi correttamente, la creazione di hello del dispositivo virtuale hello avrà esito negativo.
* Le opzioni point-to-site e da sito a sito non sono obbligatorie, ma facoltative. Se si desidera, è possibile configurarle per scenari più avanzati.
* È possibile creare [macchine virtuali di Azure](../virtual-machines/virtual-machines-linux-about.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (server host) nella rete virtuale hello che puoi usare volumi hello esposti dal dispositivo virtuale hello. Questi server devono soddisfare i seguenti requisiti hello:                             

  * Svolgere il ruolo di macchine virtuali Windows o Linux nelle quali è installato il software iSCSI Initiator
  * Essere in esecuzione in hello stessa rete virtuale dispositivo virtuale hello.
  * Essere in grado di tooconnect toohello della destinazione iSCSI del dispositivo virtuale hello tramite indirizzo IP interno hello del dispositivo virtuale hello.
* Assicurarsi di aver configurato il supporto per iSCSI e cloud di traffico su hello stessa rete virtuale.

#### <a name="storsimple-requirements"></a>Requisiti di StorSimple
Apportare hello seguente servizio di Azure StorSimple tooyour aggiornamenti prima di creare un dispositivo virtuale:

* Aggiungere [record di controllo di accesso](storsimple-manage-acrs.md) per hello macchine virtuali che verranno toobe i server host per il dispositivo virtuale.
* Utilizzare un [account di archiviazione](storsimple-manage-storage-accounts.md#add-a-storage-account) in hello dispositivo virtuale hello stessa area. Gli account di archiviazione posti in aree diverse possono causare una riduzione delle prestazioni. È possibile utilizzare un account Standard o di archiviazione Premium con dispositivo virtuale hello. Ulteriori informazioni su come toocreate un [account di archiviazione Standard](../storage/common/storage-create-storage-account.md) o [account di archiviazione Premium](../storage/common/storage-premium-storage.md)
* Utilizzare un account di archiviazione diversi per la creazione di un dispositivo virtuale dalla hello quello utilizzato per i dati. Utilizzo di hello stesso account di archiviazione può comportare una riduzione delle prestazioni.

Assicurarsi di aver hello le seguenti informazioni prima di iniziare:

* L'account del portale di Azure classico con le credenziali di accesso.
* Una copia di hello chiave DEK del servizio dal dispositivo fisico.

## <a name="create-and-configure-hello-virtual-device"></a>Creare e configurare la periferica virtuale hello
Prima di eseguire queste procedure, assicurarsi di aver soddisfatto hello [prerequisiti per il dispositivo virtuale hello](#prerequisites-for-the-virtual-device).

Dopo aver creato una rete virtuale, configurato un servizio StorSimple Manager e registrato il dispositivo StorSimple fisico con il servizio di hello, è possibile utilizzare i seguenti passaggi toocreate hello e configurare un dispositivo virtuale StorSimple.

### <a name="step-1-create-a-virtual-device"></a>Passaggio 1: Creare un dispositivo virtuale
Eseguire hello dispositivo virtuale StorSimple hello toocreate i passaggi seguenti.

[!INCLUDE [Create a virtual device](../../includes/storsimple-create-virtual-device-u2.md)]

Se la creazione di hello del dispositivo virtuale hello non riesce in questo passaggio, non è possibile toohello connettività Internet. Per ulteriori informazioni, visitare troppo[risoluzione dei problemi di connettività Internet](#troubleshoot-internet-connectivity-errors) durante la creazione di un dispositivo virtuale.

### <a name="step-2-configure-and-register-hello-virtual-device"></a>Passaggio 2: Configurare e registrare il dispositivo virtuale hello
Prima di iniziare questa procedura, assicurarsi di disporre di una copia della chiave DEK del servizio hello. Hello chiave DEK del servizio è stata creata quando è stato configurato il primo dispositivo StorSimple e fosse toosave istruzioni riportate in una posizione sicura. Se non si dispone di una copia della chiave DEK del servizio hello, è necessario contattare il supporto Microsoft per assistenza.

Eseguire i seguenti passaggi tooconfigure hello e registrare il dispositivo virtuale StorSimple.

[!INCLUDE [Configure and register a virtual device](../../includes/storsimple-configure-register-virtual-device.md)]

### <a name="step-3-optional-modify-hello-device-configuration-settings"></a>Passaggio 3: Impostazioni di configurazione dispositivo hello modifica (facoltativo)
Hello nella sezione seguente descrive le impostazioni di configurazione dispositivo hello necessarie per il dispositivo virtuale StorSimple di hello se si desidera toouse CHAP, gestione Snapshot StorSimple o modificare la password di amministratore del dispositivo hello.

#### <a name="configure-hello-chap-initiator"></a>Configurare l'iniziatore CHAP hello
Questo parametro contiene le credenziali di hello previste per il dispositivo virtuale (destinazione) da iniziatori hello (server) che siano tentando di volumi hello tooaccess. Hello iniziatori forniranno un nome utente e una tooidentify password CHAP stessi tooyour dispositivo durante il processo di autenticazione. Per informazioni dettagliate, visitare troppo[configurare CHAP per il dispositivo](storsimple-configure-chap.md#unidirectional-or-one-way-authentication).

#### <a name="configure-hello-chap-target"></a>Configurare la destinazione CHAP hello
Questo parametro contiene le credenziali di hello che il dispositivo virtuale utilizza quando un iniziatore abilitata l'autenticazione CHAP richiede l'autenticazione reciproca o bidirezionale. Dispositivo virtuale verrà utilizzato un nome utente e dell'autenticazione CHAP inversa password tooidentify toohello iniziatore durante il processo di autenticazione. Tenere presente che le impostazioni di destinazione CHAP sono di tipo globale. Quando queste sono applicate, tutti hello volumi connessi toohello virtuale dispositivo di archiviazione utilizza l'autenticazione CHAP. Per informazioni dettagliate, visitare troppo[configurare CHAP per il dispositivo](storsimple-configure-chap.md#bidirectional-or-mutual-authentication).

#### <a name="configure-hello-storsimple-snapshot-manager-password"></a>Configurare password gestione Snapshot StorSimple hello
Software di gestione Snapshot StorSimple risiede nell'host di Windows e consente agli amministratori di backup toomanage del dispositivo StorSimple in forma di hello di locale e gli snapshot cloud.

> [!NOTE]
> Per il dispositivo virtuale hello, l'host di Windows è una macchina virtuale di Azure.
>
>

Quando si configura un dispositivo in Gestione Snapshot StorSimple hello, verrà richiesto tooprovide hello StorSimple dispositivo IP indirizzo e la password tooauthenticate il dispositivo di archiviazione. Per informazioni dettagliate, visitare troppo[password configurare Gestione Snapshot StorSimple](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password).

#### <a name="change-hello-device-administrator-password"></a>Password amministratore del dispositivo hello modifica
Quando si utilizza tooaccess di interfaccia di Windows PowerShell hello hello dispositivo virtuale, sarà necessario tooenter una password amministratore del dispositivo. Per sicurezza hello dei dati, si è obbligatorio toochange la password prima periferica virtuale hello può essere utilizzato. Per informazioni dettagliate, visitare troppo[password amministratore del dispositivo configura](storsimple-change-passwords.md#change-the-device-administrator-password).

## <a name="connect-remotely-toohello-virtual-device"></a>Connettersi in modalità remota la periferica virtuale toohello
Dispositivo virtuale tooyour di accesso remoto tramite l'interfaccia di Windows PowerShell hello non è abilitato per impostazione predefinita. È necessario innanzitutto tooenable gestione remota nel dispositivo virtuale hello e abilitarlo nel client hello che verrà utilizzato tooaccess dispositivo virtuale.

Hello in due passaggi processo tooconnect in modalità remota è illustrata di seguito.

### <a name="step-1-configure-remote-management"></a>Passaggio 1: Configurare la gestione remota
Eseguire hello seguendo i passaggi tooconfigure la gestione remota del dispositivo virtuale StorSimple.

[!INCLUDE [Configure remote management via HTTP for virtual device](../../includes/storsimple-configure-remote-management-http-device.md)]

### <a name="step-2-remotely-access-hello-virtual-device"></a>Passaggio 2: Accedere in modalità remota la periferica virtuale hello
Dopo avere abilitato la gestione remota nella pagina Configurazione del dispositivo StorSimple hello, è possibile utilizzare Windows PowerShell remoting tooconnect toohello dispositivo virtuale da un'altra macchina virtuale all'interno di hello stessa rete virtuale. ad esempio, è possibile connettersi dalla macchina virtuale che è configurato e utilizzato tooconnect iSCSI dell'host hello. Nella maggior parte delle distribuzioni, si risulterà già aperto un endpoint pubblico di tooaccess l'host macchina virtuale che è possibile utilizzare per l'accesso a dispositivo virtuale hello.

> [!WARNING]
> **Per una sicurezza ottimale, è consigliabile utilizzare HTTPS durante la connessione toohello endpoint e quindi eliminare gli endpoint di hello dopo aver completato la sessione remota di PowerShell.**
>
>

È necessario seguire procedure hello in [connette in remoto il dispositivo di StorSimple tooyour](storsimple-remote-connect.md) tooset di comunicazione remota per il dispositivo virtuale.

## <a name="connect-directly-toohello-virtual-device"></a>Connettersi direttamente la periferica virtuale toohello
È possibile anche connettersi direttamente toohello di dispositivo virtuale. Se si desidera tooconnect direttamente toohello dispositivo virtuale da un altro computer all'esterno di rete virtuale hello o ambiente di Microsoft Azure hello esterno, è necessario toocreate altri endpoint come descritto nella seguente procedura hello.

Eseguire i seguenti passaggi toocreate un endpoint pubblico nel dispositivo virtuale hello hello.

[!INCLUDE [Create public endpoints on a virtual device](../../includes/storsimple-create-public-endpoints-virtual-device.md)]

È consigliabile connettersi da un'altra macchina virtuale all'interno di hello stesso virtuale perché questa pratica riduce il numero di hello di endpoint pubblici nella rete virtuale di rete. Quando si utilizza questo metodo, è sufficiente connettersi toohello virtual machine tramite una sessione Desktop remoto e configurare tale macchina virtuale da usare come si farebbe con qualsiasi altro client di Windows in una rete locale. Numero di porta pubblica hello tooappend non è necessario perché la porta hello risulterà già nota.

## <a name="work-with-hello-storsimple-virtual-device"></a>Lavorare con dispositivo virtuale StorSimple hello
Dopo aver creato e configurato dispositivo virtuale StorSimple hello, si è pronto toostart utilizzo. È possibile utilizzare con i contenitori di volumi, volumi e criteri di backup su un dispositivo virtuale esattamente come si farebbe per un dispositivo StorSimple fisico. Hello unica differenza è che è necessario verificare di aver selezionato la periferica virtuale hello dall'elenco dei dispositivi toomake. Fare riferimento troppo[utilizzare toomanage di servizio StorSimple Manager hello un dispositivo virtuale](storsimple-manager-service-administration.md) per le procedure dettagliate di gestione diverse attività necessarie per la periferica virtuale hello hello.

Hello nelle sezioni seguenti vengono illustrano alcune delle differenze di hello che si verifica quando si lavora con dispositivo virtuale hello.

### <a name="maintain-a-storsimple-virtual-device"></a>Gestire un dispositivo virtuale StorSimple
Poiché si tratta di un dispositivo basato solo su software, manutenzione per il dispositivo virtuale hello è minimo quando confrontati toomaintenance per dispositivo fisico hello. È necessario hello le opzioni seguenti:

* **Gli aggiornamenti software** – è possibile visualizzare hello Data ultimo aggiornamento del software di hello, insieme a eventuali messaggi di stato di aggiornamento. È possibile utilizzare hello **scansione degli aggiornamenti** pulsante nella parte inferiore di hello di hello pagina tooperform un'analisi manuale, se si desidera toocheck di nuovi aggiornamenti. Se sono disponibili aggiornamenti, fare clic su **Installa aggiornamenti** tooinstall. Poiché è presente una sola interfaccia nel dispositivo virtuale hello, ciò significa che non vi saranno una lieve interruzione del servizio quando vengono applicati gli aggiornamenti. dispositivo virtuale Hello verrà arrestato e riavviato (se necessario) tooapply tutti gli aggiornamenti che sono stati rilasciati. Per una procedura dettagliata, vedere troppo[aggiornare il dispositivo](storsimple-update-device.md#install-regular-updates-via-the-azure-classic-portal).
* **Pacchetto di supporto** : È possibile creare e caricare un toohelp pacchetto di supporto Microsoft supporto risolvere i problemi con il dispositivo virtuale. Per una procedura dettagliata, vedere troppo[creare e gestire un pacchetto di supporto](storsimple-create-manage-support-package.md).

### <a name="storage-accounts-for-a-virtual-device"></a>Account di archiviazione di un dispositivo virtuale
Gli account di archiviazione vengono creati per l'utilizzo dal servizio StorSimple Manager hello, dal dispositivo virtuale hello e dal dispositivo fisico hello. Quando si creano gli account di archiviazione, è consigliabile utilizzare un'area identificatore hello nome descrittivo toohelp verificare tale area hello sia coerente in tutti i componenti di sistema hello. Per un dispositivo virtuale, è importante che tutti essere componenti hello hello agli stessi problemi di prestazioni tooprevent area.

Per una procedura dettagliata, vedere troppo[aggiungere un account di archiviazione](storsimple-manage-storage-accounts.md#add-a-storage-account).

### <a name="deactivate-a-storsimple-virtual-device"></a>Disattivare un dispositivo virtuale StorSimple
Disattivazione di un dispositivo virtuale elimina hello macchina virtuale e le risorse di hello create quando è stato eseguito il provisioning. Dispositivo virtuale hello è disattivata, non può essere ripristinato lo stato precedente tooits. Prima di disattivare la periferica virtuale hello, assicurarsi che toostop o eliminare i client e gli host che dipendono da esso.

Disattivazione di un dispositivo virtuale comporta hello seguenti azioni:

* dispositivo virtuale Hello viene rimosso.
* disco Hello del sistema operativo e i dischi dati creati per il dispositivo virtuale hello vengono rimossi.
* il servizio ospitato Hello e rete virtuale creati durante il provisioning vengono mantenuti. Se non si utilizzano, è necessario eliminarli manualmente.
* Gli snapshot cloud creati per il dispositivo virtuale hello vengono mantenuti.

Per una procedura dettagliata, vedere troppo[disattivare ed eliminare il dispositivo StorSimple](storsimple-deactivate-and-delete-device.md).

Non appena la periferica virtuale hello risulta disattivato nella pagina del servizio StorSimple Manager hello, è possibile eliminare la periferica virtuale hello dall'elenco di dispositivi in hello **dispositivi** pagina.

### <a name="start-stop-and-restart-a-virtual-device"></a>Avviare, arrestare e riavviare un dispositivo virtuale
A differenza di dispositivo fisico StorSimple hello, non vi è alcun risparmio energia o spegnimento toopush pulsante in un dispositivo virtuale StorSimple. Tuttavia, potrebbe essere casi in cui è necessario toostop e riavviare la periferica virtuale hello. Ad esempio, alcuni aggiornamenti potrebbero richiedere che hello che macchina virtuale di essere riavviato il processo di aggiornamento del toofinish hello. Hello il modo più semplice per è toostart, arrestare e riavviare un dispositivo virtuale è hello toouse Console di gestione di macchine virtuali.

Quando si esamina hello Console di gestione, lo stato del dispositivo virtuale hello è **esecuzione** perché viene avviato per impostazione predefinita dopo averlo creato. È possibile avviare, arrestare e riavviare una macchina virtuale in qualsiasi momento.

[!INCLUDE [Stop and restart virtual device](../../includes/storsimple-stop-restart-virtual-device.md)]

### <a name="reset-toofactory-defaults"></a>Reimposta valori predefiniti toofactory
Se si decide che si desidera toostart su con il dispositivo virtuale, è sufficiente disattivare eliminarlo e quindi crearne uno nuovo. Analogo a quando il dispositivo fisico viene reimpostato, il nuovo dispositivo virtuale non avrà aggiornamenti installati; Pertanto, assicurarsi che toocheck per gli aggiornamenti prima di utilizzarlo.

## <a name="fail-over-toohello-virtual-device"></a>Dispositivo virtuale toohello il failover
Ripristino di emergenza (ripristino di emergenza) è uno degli scenari chiave hello che hello dispositivo virtuale è stato progettato per StorSimple. In questo scenario, il dispositivo StorSimple fisico hello o intero Data Center potrebbero non essere disponibili. Fortunatamente, è possibile utilizzare le operazioni di toorestore dispositivo virtuale in un percorso alternativo. Durante il ripristino di emergenza, i contenitori di volumi di hello hello dispositivo di origine modificare la proprietà e vengono trasferiti toohello dispositivo virtuale. Hello prerequisiti per il ripristino di emergenza sono che la periferica virtuale hello è stata creata e configurata, sono stati portati offline tutti i volumi nel contenitore di volumi hello hello e hello contenitore di volumi sia associato uno snapshot nel cloud.

> [!NOTE]
> * Quando si utilizza un dispositivo virtuale come dispositivo secondario hello per ripristino di emergenza, tenere presente che hello 8010: spazio di archiviazione Standard di 30 TB, che 8020 ha 64 TB di spazio di archiviazione Premium. Hello maggiore capacità 8020 virtuale dispositivo potrebbe non essere più adatti per uno scenario di ripristino di emergenza.
> * Impossibile eseguire il failover o clonazione da un dispositivo che esegue Update 2 tooa dispositivo che esegue pre-aggiornamento 1. È tuttavia possibile eseguire il failover un dispositivo che esegue Update 2 tooa dispositivo che esegue Update 1 (1.1 o 1.2)
>
>

Per una procedura dettagliata, vedere troppo[dispositivo virtuale di failover tooa](storsimple-device-failover-disaster-recovery.md#fail-over-to-a-storsimple-virtual-device).

## <a name="shut-down-or-delete-hello-virtual-device"></a>Arrestare o eliminare dispositivo virtuale hello
Se già configurato e usato un virtuale StorSimple dispositivo ma ora toostop essere addebitati costi di calcolo per l'uso, è possibile arrestare la periferica virtuale hello. Arresto dispositivo virtuale hello non elimina il sistema operativo o dischi dati nell'archiviazione. Ma interrompe addebiti essere addebitati la sottoscrizione, ma i costi di archiviazione per hello del sistema operativo e i dischi dati continuerà.

Se si elimina o arrestare la periferica virtuale hello, verrà visualizzato come **Offline** pagina dispositivi hello di hello servizio StorSimple Manager. È possibile scegliere toodeactivate o eliminare il dispositivo di hello desiderato anche toodelete backup hello creati dal dispositivo virtuale hello. Per altre informazioni, vedere [Disattivare ed eliminare un dispositivo StorSimple](storsimple-deactivate-and-delete-device.md).

[!INCLUDE [Shut down a virtual device](../../includes/storsimple-shutdown-virtual-device.md)]

[!INCLUDE [Delete a virtual device](../../includes/storsimple-delete-virtual-device.md)]

## <a name="troubleshoot-internet-connectivity-errors"></a>Risolvere gli errori di connettività Internet
Durante la creazione di un dispositivo virtuale hello se è presente alcun toohello connettività Internet, il passaggio di creazione hello avrà esito negativo. tootroubleshoot se hello errore è dovuto alla connettività Internet eseguire hello nel portale di Azure classico hello come segue:

1. Creare una macchina virtuale Windows Server 2012 in Azure. Questa macchina virtuale deve utilizzare hello stesso account di archiviazione, rete virtuale e subnet dal dispositivo virtuale. Se si dispone già di un host Windows Server in Azure tramite hello stesso account di archiviazione, rete virtuale e subnet, si consente inoltre la connettività Internet hello tootroubleshoot.
2. Registro remoto nella macchina virtuale hello creato nel passaggio precedente hello.
3. Aprire una finestra di comando macchina virtuale hello (Win + R, quindi digitare `cmd`).
4. Eseguire hello seguente cmd al prompt dei comandi hello.

    `nslookup windows.net`
5. Se `nslookup` ha esito negativo, quindi l'errore di connettività Internet impedisce di registrazione del servizio StorSimple Manager toohello dispositivo virtuale hello.
6. Apportare modifiche di hello necessario tooyour tooensure di rete virtuale che hello dispositivo virtuale è in grado di tooaccess siti di Microsoft Azure, ad esempio "windows.net".

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[utilizzare toomanage di servizio StorSimple Manager hello un dispositivo virtuale](storsimple-manager-service-administration.md).
* Comprendere come troppo[ripristinare un volume StorSimple da un set di backup](storsimple-restore-from-backup-set.md).
