---
title: aaaStorSimple Cloud Appliance Update 3 | Documenti Microsoft
description: Informazioni su come toocreate, distribuire e gestire un'applicazione Cloud StorSimple in una rete virtuale di Microsoft Azure. (Si applica tooStorSimple Update 3 e versioni successive).
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/10/2017
ms.author: alkohli
ms.openlocfilehash: ba60a629f1f4b8f0d4566eeb45bae8696f50d0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-a-storsimple-cloud-appliance-in-azure-update-3-and-later"></a>Distribuire e gestire un'appliance cloud StorSimple in Azure (aggiornamento 3 e versioni successive)

## <a name="overview"></a>Panoramica

Dispositivo di StorSimple 8000 Series Cloud Hello è una funzionalità aggiuntiva fornita con la soluzione di Microsoft Azure StorSimple. Hello StorSimple Appliance di Cloud viene eseguito in una macchina virtuale in una rete virtuale di Microsoft Azure e utilizzarlo tooback backup e clone dati dagli host.

In questo articolo descrive toodeploy processo dettagliato di hello e gestire un dispositivo StorSimple per Cloud in Azure. Dopo avere letto l'articolo, si sarà in grado di:

* Comprendere in che modo appliance di cloud hello differisce dal dispositivo fisico hello.
* Essere in grado di toocreate e configurare l'accessorio cloud hello.
* Connettere il dispositivo di cloud toohello.
* Informazioni su come toowork con hello cloud a dispositivo.

Questa esercitazione si applica hello tooall StorSimple Appliance di Cloud esegue l'aggiornamento 3 e versioni successive.

#### <a name="cloud-appliance-model-comparison"></a>Confronto tra i modelli dell'appliance cloud

Hello StorSimple Appliance di Cloud è disponibile in due modelli, un standard 8010: spazio (precedentemente noto come hello 1100) e un premium 8020 (introdotta in Update 2). Hello nella tabella seguente viene presentato un confronto tra due modelli di hello.

| Modello del dispositivo | 8010<sup>1</sup> | 8020 |
| --- | --- | --- |
| **Capacità massima** |30 TB |64 TB |
| **Macchina virtuale di Azure** |Standard_A3 (4 core, 7 GB di memoria)| Standard_DS3 (4 core, 14 GB di memoria)|
| **Aree di disponibilità** |Tutte le aree di Azure |Le aree di Azure che supportano Archiviazione Premium e VM DS3 di Azure<br></br>Utilizzare [questo elenco](https://azure.microsoft.com/regions/services/) toosee se entrambi **macchine virtuali > serie DS** e **archiviazione > lo spazio su disco** sono disponibili nel proprio paese. |
| **Tipo di archiviazione** |Usa l'Archiviazione Standard di Azure<br></br> Informazioni su come troppo[creare un account di archiviazione Standard](../storage/common/storage-create-storage-account.md) |Usa l'Archiviazione Standard di Azure<sup>2</sup> <br></br>Informazioni su come troppo[creare un account di archiviazione Premium](../storage/common/storage-premium-storage.md) |
| **Indicazioni relative al carico di lavoro** |Recupero a livello di elemento per i file dai backup |Scenari di sviluppo e test basati su cloud <br></br>Bassa latenza e carichi di lavoro a prestazioni superiori<br></br>Dispositivo secondario per il ripristino di emergenza |

<sup>1</sup> *precedentemente noto come hello 1100*.

<sup>2</sup> *entrambi hello 8010: spazio e 8020 utilizzare l'archiviazione di Azure Standard per hello cloud livello hello differenza esiste solo nel livello di locale hello all'interno di dispositivo hello*.

## <a name="how-hello-cloud-appliance-differs-from-hello-physical-device"></a>Differenze di appliance di cloud hello dal dispositivo fisico hello

Hello StorSimple Appliance di Cloud è una versione solo software di StorSimple, eseguita in un singolo nodo in una macchina virtuale di Microsoft Azure. dispositivo cloud Hello supporta scenari di ripristino di emergenza in cui il dispositivo fisico non è disponibile. dispositivo cloud Hello è appropriato per l'utilizzo in un recupero a livello di elemento dal backup, ripristino di emergenza locale e scenari di sviluppo e test basati su cloud.

#### <a name="differences-from-hello-physical-device"></a>Differenze rispetto a dispositivo fisico hello

Hello nella tabella seguente mostra alcune differenze fondamentali tra hello StorSimple Appliance di Cloud e il dispositivo fisico StorSimple hello.

|  | Dispositivo fisico | Appliance cloud |
| --- | --- | --- |
| **Posizione** |Si trova nel Data Center hello. |Viene eseguito in Azure. |
| **Interfacce di rete** |Ha sei interfacce di rete: da DATA 0 a DATA 5. |Ha una sola interfaccia di rete: DATA 0. |
| **Registrazione** |Registrato durante il passaggio di configurazione iniziale di hello. |La registrazione è un'attività separata. |
| **Chiave DEK del servizio** |Rigenerare sul dispositivo fisico hello e quindi aggiornare il dispositivo di cloud hello con chiave nuova hello. |Impossibile rigenerare dal dispositivo cloud hello. |
| **Tipi di volume supportati** |Supporta volumi sia aggiunti in locale che a livelli. |Supporta solo volumi a livelli. |

## <a name="prerequisites-for-hello-cloud-appliance"></a>Prerequisiti per il dispositivo di cloud hello

Hello le sezioni seguenti vengono illustrati i prerequisiti di configurazione hello per il dispositivo StorSimple per Cloud. Prima di distribuire un'applicazione cloud, esaminare le considerazioni sulla sicurezza hello per l'utilizzo di un'applicazione cloud.

[!INCLUDE [StorSimple Cloud Appliance security](../../includes/storsimple-8000-cloud-appliance-security.md)]

#### <a name="azure-requirements"></a>Requisiti di Azure

Prima eseguire il provisioning di appliance di cloud hello, è necessario hello toomake seguente preparati nell'ambiente Azure:

* Assicurarsi che un dispositivo fisico StorSimple serie 8000 (modello 8100 o 8600) sia stato distribuito e sia in esecuzione nel data center. Registrare il dispositivo con hello stesso servizio di gestione di dispositivi StorSimple che intendi toocreate a StorSimple Appliance di Cloud per.
* Per il dispositivo di cloud hello, [configurare una rete virtuale in Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). Se si usa l'archiviazione Premium, sarà necessario creare una rete virtuale in un'area di Azure che supporta l'archiviazione Premium. aree di archiviazione Premium Hello sono aree corrispondenti toohello riga per l'archiviazione su disco in hello [elenco di servizi di Azure dall'area](https://azure.microsoft.com/regions/services/).
* È consigliabile usare server DNS predefinito di hello fornita da Azure anziché specificare nome del server DNS. Se il nome del server DNS non è valido o se hello server DNS non è in grado di tooresolve indirizzi correttamente, la creazione di hello del dispositivo cloud hello non riesce.
* Le opzioni point-to-site e da sito a sito non sono obbligatorie, ma facoltative. Se si desidera, è possibile configurarle per scenari più avanzati.
* È possibile creare [macchine virtuali di Azure](../virtual-machines/virtual-machines-windows-quick-create-portal.md) (server host) nella rete virtuale hello che puoi usare volumi hello esposti dal dispositivo cloud hello. Questi server devono soddisfare i seguenti requisiti hello:

  * Svolgere il ruolo di macchine virtuali Windows o Linux nelle quali è installato il software iSCSI Initiator
  * Essere in esecuzione in hello stessa rete virtuale appliance di cloud hello.
  * Essere in grado di tooconnect toohello della destinazione iSCSI del dispositivo cloud hello tramite indirizzo IP interno hello del dispositivo cloud hello.
  * Assicurarsi di aver configurato il supporto per iSCSI e cloud di traffico su hello stessa rete virtuale.

#### <a name="storsimple-requirements"></a>Requisiti di StorSimple

Apportare hello seguente servizio di gestione di dispositivi StorSimple tooyour aggiornamenti prima di creare un'applicazione cloud:

* Aggiungere [record di controllo di accesso](storsimple-8000-manage-acrs.md) per le macchine virtuali hello che sono server del corso toobe hello host per l'applicazione cloud.
* Utilizzare un [account di archiviazione](storsimple-8000-manage-storage-accounts.md#add-a-storage-account) in hello appliance di cloud hello stessa area. Gli account di archiviazione posti in aree diverse possono causare una riduzione delle prestazioni. È possibile utilizzare un account Standard o di archiviazione Premium con dispositivo cloud hello. Ulteriori informazioni su come toocreate un [account di archiviazione Standard](../storage/common/storage-create-storage-account.md) o [account di archiviazione Premium](../storage/common/storage-premium-storage.md)
* Utilizzare un account di archiviazione diversi per la creazione di cloud accessorio da hello quello utilizzato per i dati. Utilizzo di hello stesso account di archiviazione può comportare una riduzione delle prestazioni.

Assicurarsi di aver hello le seguenti informazioni prima di iniziare:

* Account del portale di Azure con credenziali di accesso.
* Una copia di hello chiave DEK del servizio dal dispositivo fisico registrazione del servizio di gestione di dispositivi StorSimple toohello.

## <a name="create-and-configure-hello-cloud-appliance"></a>Creare e configurare il dispositivo di cloud hello

Prima di eseguire queste procedure, assicurarsi di aver soddisfatto hello [prerequisiti per il dispositivo di cloud hello](#prerequisites-for-the-cloud-appliance).

Eseguire hello seguendo i passaggi toocreate un'applicazione Cloud StorSimple.

### <a name="step-1-create-a-cloud-appliance"></a>Passaggio 1: Creare un'appliance cloud

Eseguire hello seguendo i passaggi toocreate hello StorSimple Appliance di Cloud.

[!INCLUDE [Create a cloud appliance](../../includes/storsimple-8000-create-cloud-appliance-u2.md)]

Se la creazione di hello del dispositivo cloud hello non riesce in questo passaggio, non è possibile toohello connettività Internet. Per ulteriori informazioni, visitare troppo[risoluzione dei problemi di connettività Internet](#troubleshoot-internet-connectivity-errors) durante la creazione di un'applicazione cloud.

### <a name="step-2-configure-and-register-hello-cloud-appliance"></a>Passaggio 2: Configurare e registrare il dispositivo di cloud hello

Prima di iniziare questa procedura, assicurarsi di disporre di una copia della chiave DEK del servizio hello. chiave di crittografia di Hello servizio dati viene creato quando il primo dispositivo fisico StorSimple è stato registrato con il servizio di gestione di dispositivi StorSimple hello. È stato toosave istruzioni riportate in una posizione sicura. Se non si dispone di una copia della chiave DEK del servizio hello, è necessario contattare il supporto Microsoft per assistenza.

Eseguire i seguenti passaggi tooconfigure hello e registrare il dispositivo StorSimple per Cloud.

[!INCLUDE [Configure and register a cloud appliance](../../includes/storsimple-8000-configure-register-cloud-appliance.md)]

### <a name="step-3-optional-modify-hello-device-configuration-settings"></a>Passaggio 3: Impostazioni di configurazione dispositivo hello modifica (facoltativo)

Hello nella sezione seguente vengono descritte le impostazioni di configurazione dispositivo hello necessari per hello StorSimple Appliance di Cloud, se si desidera toouse CHAP, gestione Snapshot StorSimple o modificare una password amministratore del dispositivo hello.

#### <a name="configure-hello-chap-initiator"></a>Configurare l'iniziatore CHAP hello

Questo parametro contiene le credenziali di hello previste per il dispositivo a cloud (destinazione) da iniziatori hello (server) che siano tentando di volumi hello tooaccess. iniziatori Hello forniscono un nome utente e una tooidentify password CHAP stessi tooyour dispositivo durante il processo di autenticazione. Per informazioni dettagliate, visitare troppo[configurare CHAP per il dispositivo](storsimple-8000-configure-chap.md#unidirectional-or-one-way-authentication).

#### <a name="configure-hello-chap-target"></a>Configurare la destinazione CHAP hello

Questo parametro contiene le credenziali di hello che il cloud utilizzato quando un iniziatore abilitata l'autenticazione CHAP richiede l'autenticazione reciproca o bidirezionale. Il dispositivo di cloud utilizza un nome utente e dell'autenticazione CHAP inversa password tooidentify toohello iniziatore durante il processo di autenticazione.

> [!NOTE]
> Le impostazioni della destinazione CHAP sono impostazioni globali. Quando queste impostazioni vengono applicate, tutti i volumi di hello connessa l'autenticazione CHAP toohello cloud accessorio utilizzare.

Per informazioni dettagliate, visitare troppo[configurare CHAP per il dispositivo](storsimple-8000-configure-chap.md#bidirectional-or-mutual-authentication).

#### <a name="configure-hello-storsimple-snapshot-manager-password"></a>Configurare password gestione Snapshot StorSimple hello

Software di gestione Snapshot StorSimple risiede nell'host di Windows e consente agli amministratori di backup toomanage del dispositivo StorSimple in forma di hello di locale e gli snapshot cloud.

> [!NOTE]
> Per il dispositivo di cloud hello, l'host di Windows è una macchina virtuale di Azure.

Quando si configura un dispositivo in Gestione Snapshot StorSimple hello, viene chiesto tooprovide hello StorSimple dispositivo IP indirizzo e la password tooauthenticate il dispositivo di archiviazione. Per informazioni dettagliate, visitare troppo[password configurare Gestione Snapshot StorSimple](storsimple-8000-change-passwords.md#set-the-storsimple-snapshot-manager-password).

#### <a name="change-hello-device-administrator-password"></a>Password amministratore del dispositivo hello modifica

Quando si utilizza tooaccess di interfaccia di Windows PowerShell hello hello appliance di cloud, è necessario tooenter una password amministratore del dispositivo. Per sicurezza hello dei dati, è necessario modificare la password prima di poter utilizzare il dispositivo di cloud hello. Per informazioni dettagliate, visitare troppo[password amministratore del dispositivo configura](../storsimple/storsimple-8000-change-passwords.md#change-the-device-administrator-password).

## <a name="connect-remotely-toohello-cloud-appliance"></a>Connettersi in remoto il dispositivo di cloud toohello

Dispositivo cloud tooyour di accesso remoto tramite l'interfaccia di Windows PowerShell hello non è abilitato per impostazione predefinita. È necessario abilitare gestione remota nel dispositivo cloud hello prima e quindi su hello client utilizzato appliance di cloud tooaccess hello.

Hello seguendo la procedura in due passaggi viene descritto come tooconnect in modalità remota tooyour cloud dello strumento.

### <a name="step-1-configure-remote-management"></a>Passaggio 1: Configurare la gestione remota

Eseguire hello seguendo i passaggi tooconfigure la gestione remota del dispositivo StorSimple per Cloud.

[!INCLUDE [Configure remote management via HTTP for cloud appliance](../../includes/storsimple-8000-configure-remote-management-http-device.md)]

### <a name="step-2-remotely-access-hello-cloud-appliance"></a>Passaggio 2: Accedere in remoto il dispositivo di cloud hello

Dopo aver abilitato la gestione remota nel dispositivo cloud hello, utilizzare strumento di Windows PowerShell remoting tooconnect toohello da un'altra macchina virtuale all'interno di hello stessa rete virtuale. Ad esempio, è possibile connettersi dalla macchina virtuale che è configurato e utilizzato tooconnect iSCSI dell'host hello. Nella maggior parte delle distribuzioni, tooaccess un endpoint pubblico verrà aperto l'host macchina virtuale che è possibile utilizzare per l'accesso a dispositivo cloud hello.

> [!WARNING]
> **Per una sicurezza ottimale, è consigliabile utilizzare HTTPS durante la connessione toohello endpoint e quindi eliminare gli endpoint di hello dopo aver completato la sessione remota di PowerShell.**

È necessario seguire procedure hello in [connette in remoto il dispositivo di StorSimple tooyour](storsimple-8000-remote-connect.md) tooset di gestione remota per il dispositivo a cloud.

## <a name="connect-directly-toohello-cloud-appliance"></a>Connettersi direttamente toohello appliance di cloud

È inoltre possibile connettere direttamente toohello appliance di cloud. tooconnect direttamente dispositivo da un altro computer all'esterno del cloud toohello hello ambiente di Microsoft Azure hello esterno o di rete virtuale, è necessario creare endpoint aggiuntivi.

Eseguire i seguenti passaggi toocreate un endpoint pubblico sul dispositivo per cloud hello hello.

[!INCLUDE [Create public endpoints on a cloud appliance](../../includes/storsimple-8000-create-public-endpoints-cloud-appliance.md)]

È consigliabile connettersi da un'altra macchina virtuale all'interno di hello stesso virtuale perché questa pratica riduce il numero di hello di endpoint pubblici nella rete virtuale di rete. In questo caso, la connessione macchina virtuale toohello tramite una sessione Desktop remoto e quindi configurare tale macchina virtuale da usare come si farebbe con qualsiasi altro client di Windows in una rete locale. Numero di porta pubblica hello tooappend non è necessario perché la porta hello è già nota.

## <a name="work-with-hello-storsimple-cloud-appliance"></a>Lavorare con hello StorSimple Appliance di Cloud

Dopo aver creato e configurato hello StorSimple Appliance di Cloud, si è toostart pronto utilizzo. In un'appliance cloud è possibile usare contenitori di volumi, volumi e criteri di backup così come in un dispositivo fisico StorSimple. Hello unica differenza è che è necessario verificare di aver selezionato il dispositivo di cloud hello dall'elenco dei dispositivi toomake. Fare riferimento troppo[utilizzare toomanage servizio di gestione di dispositivi StorSimple hello un'applicazione cloud](storsimple-8000-manager-service-administration.md) per le procedure dettagliate di gestione diverse attività per dispositivo cloud hello hello.

Hello nelle sezioni seguenti vengono illustrano alcune delle differenze di hello che si verifica quando si lavora con dispositivo cloud hello.

### <a name="maintain-a-storsimple-cloud-appliance"></a>Gestire un'appliance cloud StorSimple

Poiché si tratta di un dispositivo basato solo su software, manutenzione per il dispositivo cloud hello è minimo quando confrontati toomaintenance per dispositivo fisico hello.

Non è possibile aggiornare un'appliance cloud. Usare hello l'ultima versione del software toocreate nuovi accessori di cloud.


### <a name="storage-accounts-for-a-cloud-appliance"></a>Account di archiviazione per un'appliance cloud

Gli account di archiviazione vengono creati per l'utilizzo tramite il servizio di gestione di dispositivi StorSimple hello, appliance di cloud hello e dispositivo fisico hello. Quando si creano gli account di archiviazione, è consigliabile utilizzare un identificatore di area nel nome descrittivo hello. In questo modo otterrai che tale area hello sia coerente in tutti i componenti di sistema hello. Per un'applicazione cloud, è importante che tutti i componenti di hello presenti hello agli stessi problemi di prestazioni tooprevent area.

Per una procedura dettagliata, vedere troppo[aggiungere un account di archiviazione](storsimple-8000-manage-storage-accounts.md#add-a-storage-account).

### <a name="deactivate-a-storsimple-cloud-appliance"></a>Disattivare un'appliance cloud StorSimple

Quando si disattiva un'applicazione cloud, l'azione di hello Elimina hello macchina virtuale e le risorse di hello create quando è stato eseguito il provisioning. Dopo la disattivazione di appliance di cloud hello, non può essere ripristinato lo stato precedente tooits. Prima di disattivare il dispositivo di cloud hello, assicurarsi che toostop o eliminare i client e gli host che dipendono da esso.

Disattivazione di un'applicazione cloud produce hello seguenti azioni:

* dispositivo cloud Hello è stato rimosso.
* disco Hello del sistema operativo e i dischi dati creati per il dispositivo di hello cloud vengono rimossi.
* il servizio ospitato Hello e rete virtuale creati durante il provisioning vengono mantenuti. Se non si utilizzano, è necessario eliminarli manualmente.
* Gli snapshot cloud creati per il dispositivo di hello cloud vengono mantenuti.

Per una procedura dettagliata, vedere troppo[disattivare ed eliminare il dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).

Non appena il dispositivo di cloud hello risulta disattivato nel Pannello di servizio di gestione di dispositivi StorSimple hello, è possibile eliminare dispositivo cloud hello dall'elenco di dispositivi in hello **dispositivi** blade.

### <a name="start-stop-and-restart-a-cloud-appliance"></a>Avviare, arrestare e riavviare un'appliance cloud
A differenza di dispositivo fisico StorSimple hello, non vi è alcun risparmio energia o spegnimento toopush pulsante in un dispositivo di StorSimple Cloud. Tuttavia, potrebbe essere casi in cui è necessario toostop e riavviare appliance di cloud hello.

Hello il modo più semplice per è toostart, arrestare e riavviare un'applicazione cloud è tramite hello pannello servizio macchine virtuali. Passare il servizio di Virtual machine hello. Hello l'elenco di macchine virtuali, identificare dispositivo hello VM corrispondente tooyour cloud (nome) e fare clic sul nome di macchina virtuale hello. Quando si esamina il pannello delle macchine virtuali, è stato appliance di cloud hello **esecuzione** perché viene avviato per impostazione predefinita dopo averlo creato. È possibile avviare, arrestare e riavviare una macchina virtuale in qualsiasi momento.

[!INCLUDE [Stop and restart cloud appliance](../../includes/storsimple-8000-stop-restart-cloud-appliance.md)]

### <a name="reset-toofactory-defaults"></a>Reimposta valori predefiniti toofactory
Se si decide che si desidera toostart su con il dispositivo di cloud, disattivare ed eliminarla e quindi crearne uno nuovo.

## <a name="fail-over-toohello-cloud-appliance"></a>Eseguire il failover toohello appliance di cloud
Ripristino di emergenza (ripristino di emergenza) è uno di hello gli scenari principali che hello StorSimple Appliance di Cloud è stato progettato per. In questo scenario, il dispositivo StorSimple fisico hello o intero Data Center potrebbe non essere disponibile. Fortunatamente, è possibile utilizzare le operazioni toorestore appliance di cloud in un percorso alternativo. Durante il ripristino di emergenza, i contenitori di volumi hello hello dispositivo di origine modificare la proprietà e sono trasferiti toohello appliance di cloud.

prerequisiti di Hello per ripristino di emergenza sono:

* dispositivo di Hello cloud viene creato e configurato.
* Tutti i volumi nel contenitore di volumi hello hello sono offline.
* contenitore di volumi Hello che si esegue il failover, è associato uno snapshot nel cloud.

> [!NOTE]
> * Quando si utilizza un'applicazione cloud come dispositivo secondario hello per ripristino di emergenza, tenere presente che hello 8010: spazio di archiviazione Standard di 30 TB, che 8020 ha 64 TB di spazio di archiviazione Premium. dispositivo di Hello maggiore capacità 8020 cloud potrebbe essere più adatto per uno scenario di ripristino di emergenza.

Per una procedura dettagliata, vedere troppo[failover appliance di cloud tooa](storsimple-8000-device-failover-cloud-appliance.md).

## <a name="delete-hello-cloud-appliance"></a>Eliminare il dispositivo di cloud hello
Se già configurato e usato un dispositivo di StorSimple Cloud ma decide toostop essere addebitati costi di calcolo per l'uso, è necessario interrompere appliance di cloud hello. Arresto appliance di cloud hello dealloca hello macchina virtuale. Questa azione interromperà l'addebito di costi nella sottoscrizione. costi di archiviazione Hello per hello del sistema operativo e i dischi dati tuttavia continuerà.

gli addebiti toostop tutti hello, è necessario eliminare il dispositivo di cloud hello. backup di hello toodelete creati dal dispositivo di hello cloud, è possibile disattivare o eliminare il dispositivo hello. Per altre informazioni, vedere [Disattivare ed eliminare un dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).

[!INCLUDE [Delete a cloud appliance](../../includes/storsimple-8000-delete-cloud-appliance.md)]

## <a name="troubleshoot-internet-connectivity-errors"></a>Risolvere gli errori di connettività Internet
Durante la creazione di un'applicazione cloud hello se è presente alcun toohello connettività Internet, il passaggio di creazione di hello ha esito negativo. tootroubleshoot gli errori di connettività Internet, eseguire hello in hello portale di Azure come segue:

1. [Creare una macchina virtuale Windows Server 2012 in Azure](/articles/virtual-machines/windows/quick-create-portal.md). Questa macchina virtuale deve utilizzare hello stesso account di archiviazione, rete virtuale e subnet dal dispositivo per il cloud. Se è presente un host Windows Server in Azure tramite hello stesso account di archiviazione, rete virtuale e subnet, si consente inoltre la connettività Internet hello tootroubleshoot.
2. Registro remoto nella macchina virtuale hello creato nel passaggio precedente hello.
3. Aprire una finestra di comando macchina virtuale hello (Win + R, quindi digitare `cmd`).
4. Eseguire hello seguente cmd al prompt dei comandi hello.

    `nslookup windows.net`
5. Se `nslookup` ha esito negativo, quindi impedisce appliance di cloud hello tramite la registrazione del servizio di gestione di dispositivi StorSimple toohello errore di connettività Internet.
6. Apportare modifiche di hello necessario tooyour tooensure di rete virtuale che hello appliance di cloud è in grado di tooaccess siti di Microsoft Azure, ad esempio _windows.net_.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[utilizzare toomanage servizio di gestione di dispositivi StorSimple hello un'applicazione cloud](storsimple-8000-manager-service-administration.md).
* Comprendere come troppo[ripristinare un volume StorSimple da un set di backup](storsimple-8000-restore-from-backup-set-u2.md).
