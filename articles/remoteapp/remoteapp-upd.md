---
title: salvare le impostazioni e dati utente, aaaHow non Azure RemoteApp? | Microsoft Docs
description: Informazioni su come vengono salvati i dati utente tramite disco hello Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: e125af62-5c1a-4186-a238-52f537f7bb34
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: dccebc7861e8a0d87cb3ee174f399a2df7fe023c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-remoteapp-save-user-data-and-settings"></a>Azure RemoteApp come salva dati e impostazioni?
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Azure RemoteApp salva identità utente e personalizzazioni nei dispositivi e nelle sessioni. Tali dati utente vengono archiviati in un disco per ogni raccolta per utente, noto come disco del profilo utente (UPD). disco Hello segue utente hello e assicura hello utente dispone di un'esperienza coerente, indipendentemente dal fatto in cui accedono.

I dischi dei profili utente sono completamente trasparenti toohello utente, gli utenti di salvare una cartella documenti tootheir di documenti (su quanto visualizzato toobe un'unità locale) e modificare le impostazioni di app come al solito. AT hello stesso vengono mantenute le impostazioni di tempo, tutti personali quando ci si connette tooAzure RemoteApp da qualsiasi dispositivo. Tutti gli utenti di hello vede i relativi dati in hello stessa posizione.

Ogni UPD dispone di 50GB di archiviazione permanente e contiene entrambe le impostazioni applicazione e dati utente. 

Leggere le informazioni specifiche sui dati del profilo utente.

> [!NOTE]
> È necessario toodisable hello UPD? È ora possibile eseguire questa operazione: per informazioni dettagliate, consultare il post di blog di Pavithra relativo alla [disabilitazione dei dischi dei profili utente in Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/).
> 
> 

## <a name="how-can-an-admin-get-toohello-data"></a>Come un amministratore può ottenere i dati toohello?
Se sono necessari dati hello tooaccess per uno degli utenti (per il ripristino di emergenza o se utente hello lascia la società hello), contattare il supporto tecnico di Azure e fornire informazioni sulla sottoscrizione hello per la raccolta di hello e identità utente hello. il team di Azure RemoteApp Hello fornirà un toohello URL VHD. Scaricare il disco rigido virtuale e recuperare i documenti o i file necessari. Si noti che hello disco rigido virtuale è 50GB, in modo richiederà toodownload un bit è.

## <a name="is-hello-data-backed-up"></a>Dati hello viene eseguito il backup?
Sì, si salva una copia di backup dei dati utente hello per ogni area geografica. Hello dati è di sola lettura ed è possibile accedere in hello stesso modo come dati normali hello sarebbe (contattare tooget Azure RemoteApp è), se hello data center primario è inattivo. dati Hello sono percorso di backup copiati toohello in tempo reale e abbiamo non dispongono di copie di versioni diverse. In tal caso, il danneggiamento dei dati, nel è non saranno in grado di toorestore è noto in precedenza versione funzionante, ma se hello data center primario è inattivo, si sarà in grado di tooget dati definite dall'utente tooa hello altra posizione.

## <a name="how-do-users-see-hello-upd-on-hello-server-side"></a>Come gli utenti visualizzano hello UPD sul lato server hello?
Ciascun utente avrà le proprie directory server che esegue il mapping tootheir UPD hello: c:\Users\username.

## <a name="whats-hello-best-way-toouse-outlook-and-upd"></a>Che cos'è hello migliore modo toouse Outlook e UPD?
Azure RemoteApp Salva lo stato di Outlook di hello (cassette postali, pst) tra le sessioni. tooenable, abbiamo base hello toobe PST archiviati nei dati di profilo utente hello (c:\users\<nomeutente >). Questo è il percorso predefinito hello per i dati di hello, pertanto, a condizione che non si modifica il percorso di hello, dati hello verranno mantenute tra le sessioni.

È inoltre consigliabile utilizzare la modalità "cache" in Outlook e utilizzare la modalità "server/online" per la ricerca.

Per altre informazioni sull'uso di Outlook e Azure RemoteApp, consultare [questo articolo](remoteapp-outlook.md) .

## <a name="what-about-redirection"></a>Come funziona il reindirizzamento?
È possibile configurare utenti toolet accedere ai dispositivi locali mediante la configurazione di Azure RemoteApp [reindirizzamento](remoteapp-redirection.md). Dispositivi locali potranno quindi essere in grado di tooaccess dati hello hello UPD.

## <a name="can-i-use-my-upd-as-a-network-share"></a>È possibile utilizzare l’UPD come condivisione di rete?
No. UPDs non può essere utilizzato come una condivisione di rete. Un UPD è utente toohello disponibile solo quando l'utente di hello è attivamente connesso tooAzure RemoteApp.

## <a name="if-i-delete-a-user-from-a-collection-is-their-upd-deleted"></a>Se si elimina un utente da una raccolta, viene eliminato anche il suo UPD?
No, quando si elimina un utente, è non eliminare automaticamente hello UPD - invece è archiviare dati hello fino a quando non si elimina raccolta hello. 90 giorni dopo l'eliminazione di una raccolta di hello, vengono eliminati tutti che. 

Se è necessario toodelete un UPD da una raccolta, contattare Azure RemoteApp, è possibile eliminare UPD dal nostro lato.

## <a name="can-i-access-my-users-upds-either-current-or-deleted-users"></a>È possibile accedere agli UPD dei propri utenti (utenti correnti o eliminati)?
Sì, se si contatta il [Azure RemoteApp](mailto:remoteappforum@microsoft.com), è possibile impostare è con un tooaccess URL dati hello. È necessario sul toodownload 10 ore i dati o file da hello UPD prima della scadenza accesso hello.

## <a name="are-upds-available-offline"></a>Gli UPD sono disponibili offline?
In questo momento non si forniscono tooUPDs accesso offline, oltre a finestra di accesso di 10 ore hello descritto in precedenza. Ciò significa che si dispone attualmente di un modo tooprovide all'accesso per attività abbastanza a lungo toocomplete più complessa, come in esecuzione un software antivirus in hello che o l'accesso ai dati per un controllo.

## <a name="do-registry-key-settings-persist"></a>Vengono mantenute le impostazioni della chiave del Registro di sistema?
Sì, scrittura tooHKEY_Current_User fa parte di hello UPD.

## <a name="can-i-disable-upds-for-a-collection"></a>È possibile disattivare gli UPD per una raccolta?
Sì, è possibile chiedere toodisable Azure RemoteApp che per una sottoscrizione, ma non è possibile eseguire manualmente. Ciò significa che che verranno disabilitati per tutte le raccolte nella sottoscrizione hello.

È possibile che toodisable delle hello seguenti situazioni: 

* È necessario disporre di accesso e controllo completi dei dati utente (a scopo di controllo e verifica, ad esempio negli istituti finanziari).
* Si dispone di parti 3rd utente profilo di gestione soluzioni in locale e si desidera utilizzarli nella distribuzione di Azure RemoteApp dominio toocontinue. Ciò richiede hello profilo agente toobe caricati immagine gold hello. 
* Non è necessario spazio di archiviazione di dati locale o si dispongono di tutti i dati nel hello cloud o la condivisione file e si desidera toocontrol salvataggio di dati localmente utilizzando Azure RemoteApp.

Per altre informazioni, vedere il post di blog relativo alla [disabilitazione dei dischi dei profili utente in Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/).

## <a name="can-i-restrict-users-from-saving-data-toohello-system-drive"></a>È possibile limitare gli utenti dal salvataggio di unità di sistema toohello dati?
Sì, ma è necessario tooset che backup nel modello hello immagine prima di creare una raccolta di hello. Utilizzare hello unità di sistema toohello accesso tooblock i passaggi seguenti:

1. Eseguire **gpedit. msc** nell'immagine modello hello.
2. Passare troppo**configurazione utente > modelli amministrativi > componenti di Windows > Esplora**.
3. Hello seleziona le opzioni seguenti:
   * **Nascondi le unità specificate in risorse del Computer**
   * **Impedire l'accesso toodrives dal computer locale**

## <a name="can-i-seed-upds-i-want-tooput-some-data-in-hello-upd-thats-available-hello-first-time-hello-user-signs-in"></a>È possibile inizializzare gli UPD? Si desidera tooput alcuni dati hello UPD che è disponibile hello hello utente effettua l'accesso.
Sì, quando si crea l'immagine modello hello, è possibile aggiungere profilo predefinito toohello di informazioni. Questa informazione verrà quindi aggiunta toohello UPD.

## <a name="can-i-change-hello-size-of-hello-upd-depending-on-how-much-data-i-want-toostore"></a>È possibile modificare le dimensioni di hello di hello UPD a seconda della quantità di dati desiderato toostore?
No, tutti gli UPD hanno 50 GB di spazio di archiviazione. Se si desidera toostore quantità diverse di dati, provare l'esempio hello:

1. Disabilitare che per la raccolta di hello.
2. Configurare una condivisione file per gli utenti tooaccess.
3. Condivisione di file hello carico usando uno script di avvio. Per ulteriori informazioni sugli script di avvio in Azure RemoteApp, vedere di seguito.
4. Indirizzare gli utenti toosave condivisione file di tutti i dati toohello.

## <a name="how-do-i-run-a-startup-script-in-azure-remoteapp"></a>Come eseguire uno script di avvio in Azure RemoteApp
Se si desidera toorun uno script di avvio, iniziare creando un'attività pianificata nell'immagine modello hello verrà toouse per la raccolta di hello. (Eseguire tale operazione *prima* di eseguire sysprep.) 

![Creare un'attività di sistema](./media/remoteapp-upd/upd1.png)

![Creare un'attività di sistema che viene eseguita quando un utente accede](./media/remoteapp-upd/upd2.png)

In hello **generale** scheda, hello toochange assicurarsi di essere **Account utente** in sicurezza troppo "BUILTIN\Users".

![Modificare il gruppo tooa account utente di hello](./media/remoteapp-upd/upd4.png)

attività pianificata Hello verrà avviato lo script di avvio, utilizzando le credenziali dell'utente hello. Pianificare hello attività toorun ogni volta un utente accede.

![Imposta il trigger hello per le attività di hello come "All'accesso"](./media/remoteapp-upd/upd3.png)

È inoltre possibile usare [gli script di avvio basati su criteri di gruppo](https://technet.microsoft.com/library/cc779329%28v=ws.10%29.aspx). 

## <a name="what-about-placing-a-startup-script-in-hello-start-menu-would-that-work"></a>Menu di avvio per quanto riguarda l'inserimento di uno script di avvio in hello? Funziona?
In altre parole, è possibile creare un file con estensione bat che esegue uno script di finestra di configurazione e salvarlo toohello c:\ProgramData\Microsoft\Windows\Start di Avvio\Programmi\Esecuzione e hanno quindi lo script eseguito ogni volta che un utente avvia una sessione di RemoteApp?

No, che non è supportata con Azure RemoteApp, che utilizza host sessione Desktop remoto, che non supporta inoltre gli script di avvio nel menu Start hello.

## <a name="can-i-use-mstscexe-hello-remote-desktop-program-tooconfigure-logon-scripts"></a>È possibile utilizzare gli script di accesso tooconfigure mstsc.exe (programma di Desktop remoto hello)?
No, tale opzione non è supportata da Azure RemoteApp.

## <a name="can-i-store-data-on-hello-vm-locally"></a>È possibile archiviare dati nel hello macchina virtuale in locale?
NO, dati archiviati in un punto qualsiasi in hello VM diverso in hello UPD andranno persi. È un utente di hello elevata probabilità non sarà possibile ricevere hello hello VM stesso successivo che eseguono l'accesso in Azure RemoteApp. Persistenza utente-VM, non è mantenuto in modo utente hello non accederanno a hello stessa macchina virtuale e hello dati andranno perduti. Inoltre, quando si aggiorna la raccolta hello, le macchine virtuali esistenti vengono sostituite con un nuovo set di macchine virtuali, che significa che i dati archiviati in una macchina virtuale stessa hello hello viene perso. si consiglia Hello di dati toostore hello UPD, archiviazione condivisa come file di Azure, un file server all'interno di una rete virtuale o nel cloud hello usando un sistema di archiviazione cloud come DropBox.

## <a name="how-do-i-mount-an-azure-file-share-on-a-vm-using-powershell"></a>Come montare una condivisione di File di Azure in una VM, tramite PowerShell
È possibile utilizzare hello unità hello toomount di Net-PSDrive cmdlet, come indicato di seguito:

    New-PSDrive -Name <drive-name> -PSProvider FileSystem -Root \\<storage-account-name>.file.core.windows.net\<share-name> -Credential :<storage-account-name>


È inoltre possibile salvare le credenziali eseguendo hello:

    cmdkey /add:<storage-account-name>.file.core.windows.net /user:<storage-account-name> /pass:<storage-account-key>


Che consente di ignorare hello - parametro delle credenziali nel cmdlet New-PSDrive hello.

