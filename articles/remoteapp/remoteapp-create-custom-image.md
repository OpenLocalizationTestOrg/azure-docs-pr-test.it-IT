---
title: aaaHow toocreate un'immagine modello personalizzato per Azure RemoteApp | Documenti Microsoft
description: "Informazioni su come l'immagine toocreate un modello personalizzato per Azure RemoteApp. È possibile usare questo modello con una raccolta ibrida o cloud."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: b9ec5b51-f7cd-470b-8545-d0fd714c5982
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9e3a0b2d3cc56177ea51406e6cecfe19ff235340
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-custom-template-image-for-azure-remoteapp"></a>Come l'immagine toocreate un modello personalizzato per Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Azure RemoteApp utilizza un toohost immagine modello di Windows Server 2012 R2 tutti i programmi di hello che si desidera tooshare con gli utenti. toocreate un'immagine modello RemoteApp personalizzata, è possibile iniziare con un'immagine esistente o crearne uno nuovo. 

> [!TIP]
> E’ possibile creare un'immagine da una macchina virtuale di Azure. Storia true e consente di durata massima di hello e accetta tooimport hello immagine. Controllare i passaggi di hello [qui](remoteapp-image-on-azurevm.md).
> 
> 

i requisiti per l'immagine di hello che può essere caricato per l'utilizzo con Azure RemoteApp Hello sono:

* dimensioni dell'immagine Hello devono essere un multiplo del numero di MB. Se si tenta di tooupload un'immagine che non è un multiplo esatto, caricamento hello avrà esito negativo.
* dimensioni dell'immagine Hello devono essere 127 GB o più piccoli.
* Deve essere inclusa in un file VHD (i file VHDX [dischi rigidi virtuali Hyper-V] non sono attualmente supportati).
* Hello disco rigido virtuale non deve essere una macchina virtuale di generazione 2.
* è possibile Hello disco rigido virtuale a dimensione fissa o ad espansione dinamica. Un disco rigido virtuale ad espansione dinamica è consigliato perché richiede meno tooAzure tooupload tempo rispetto a un file di disco rigido virtuale a dimensione fissa.
* Hello disco deve essere inizializzato con stile di partizionamento hello il record di avvio principale (MBR, Master Boot Record). Hello stile di partizione GUID partizione GPT (tabella) non è supportata.
* Hello VHD deve contenere una singola installazione di Windows Server 2012 R2. Può contenere più volumi, ma solo uno che contiene un'installazione di Windows.
* ruolo di Hello sessione Desktop remoto Host () e funzionalità esperienza Desktop hello devono essere installati.
* ruolo Gestore connessione Desktop remoto Hello deve *non* installato.
* Hello Encrypting File System (EFS) deve essere disabilitato.
* Hello immagine deve essere preparata con Sysprep utilizzando parametri hello **/oobe /generalize /shutdown** (non utilizzare hello **/mode: VM** parametro).
* Il caricamento del disco VHD da una catena di snapshot non è supportato.

**Prima di iniziare**

È necessario seguente hello toodo prima di creare il servizio hello:

* [Iscriversi](https://azure.microsoft.com/services/remoteapp/) a RemoteApp.
* Creare un account utente in Active Directory toouse come account del servizio RemoteApp hello. Limitare le autorizzazioni di hello per questo account in modo che questo può associarsi solo dominio toohello macchine. Per altre informazioni, vedere [Configurare Azure Active Directory per RemoteApp](remoteapp-ad.md) .
* Raccogliere informazioni sulla rete locale: informazioni sull'indirizzo IP e dettagli sul dispositivo VPN.
* Installare hello [Azure PowerShell](/powershell/azure/overview) modulo.
* Raccogliere informazioni sugli utenti hello che si desidera accedere toogrant a. Le informazioni possono essere relative all'account Microsoft o all'account di lavoro Active Directory per gli utenti.

## <a name="create-a-template-image"></a>Creazione di un'immagine modello
Di seguito vengono hello passaggi di alto livello toocreate una nuova immagine modello da zero.

1. Procurarsi un DVD o un'immagine ISO di Windows Server 2012 R2 Update.
2. Creare un file VHD.
3. Installare Windows Server 2012 R2.
4. Installare il ruolo di sessione Desktop remoto Host () hello e la funzionalità esperienza Desktop hello.
5. Installare funzionalità aggiuntive richieste dalle applicazioni.
6. Installare e configurare le applicazioni. app di condivisione toomake più semplice, aggiungere le app o i programmi che si desidera tooshare toohello **avviare** menu dell'immagine di hello, in particolare in **%systemdrive%\ProgramData\Microsoft\Windows\Start Avvio\Programmi.
7. Eseguire eventuali configurazioni aggiuntive di Windows richieste dalle applicazioni.
8. Disabilitare hello Encrypting File System (EFS).
9. **REQUIRED:** andare tooWindows Update e installare tutti gli aggiornamenti importanti.
10. Immagine SYSPREP hello.

Hello sono procedure dettagliate per la creazione di una nuova immagine:

1. Procurarsi un DVD o un'immagine ISO di Windows Server 2012 R2 Update.
2. Creare un disco VHD usando Gestione disco.
   
   1. Avviare Gestione disco (diskmgmt.msc).
   2. Creare un file VHD a espansione dinamica di dimensioni non inferiori a 40 GB. (Stimare hello di spazio necessaria per Windows, le applicazioni e le personalizzazioni. Windows Server con il ruolo di host sessione Desktop remoto hello e installata la funzionalità esperienza Desktop richiederà circa 10 GB di spazio).
      
      1. Fare clic su **Azione > Crea file VHD**.
      2. Specificare il percorso di hello, dimensioni e il formato di disco rigido virtuale. Selezionare **A espansione dinamica**, quindi fare clic su **OK**.
      
      L'operazione dura alcuni secondi. Una volta completato hello creazione del disco rigido virtuale, verrà visualizzato un nuovo disco senza qualsiasi lettera di unità e nello stato "Non inizializzato" nella console Gestione disco hello.
      
      * Fare doppio clic su disco hello (non lo spazio non allocato hello) e quindi fare clic su **Inizializza disco**. Selezionare **MBR** (Master Boot Record) come stile di partizione hello e quindi fare clic su **OK**.
      * Creare un nuovo volume: destro hello spazio non allocato e quindi fare clic su **nuovo Volume semplice**. È possibile accettare le impostazioni predefinite nella procedura guidata hello hello, ma assicurarsi di assegnare un potenziali problemi tooavoid lettera unità quando si carica l'immagine modello hello.
      * Fare doppio clic su disco hello e quindi fare clic su **Scollega file VHD**.
3. Installare Windows Server 2012 R2:
   
   1. Creare una nuova macchina virtuale. Utilizzare Creazione guidata macchina virtuale in Hyper-V Manager o Client Hyper-V hello.
      1. Nella pagina Impostazione generazione hello scegliere **generazione 1**.
      2. Nella pagina Connessione disco rigido virtuale hello selezionare **utilizzare un disco rigido virtuale esistente**e passare toohello disco rigido virtuale creato nel passaggio precedente hello.
      3. Nella pagina Opzioni di installazione hello selezionare **installa un sistema operativo da un CD/DVD_ROM**, quindi selezionare il percorso di hello del supporto di installazione di Windows Server 2012 R2.
      4. Scegliere altre opzioni di hello guidata necessarie tooinstall Windows e le applicazioni. Completare la procedura guidata hello.
   2. Al termine della procedura guidata hello, modificare le impostazioni di hello della macchina virtuale hello e apportare altre modifiche necessarie tooinstall Windows e i programmi, ad esempio il numero di hello di processori virtuali e quindi fare clic su **OK**.
   3. Connettere la macchina virtuale di toohello e installare Windows Server 2012 R2.
4. Installare il ruolo di sessione Desktop remoto Host () hello e funzionalità esperienza Desktop hello:
   1. Avviare Server Manager.
   2. Fare clic su **Aggiungi ruoli e funzionalità** nella schermata iniziale di hello o da hello **Gestisci** menu.
   3. Fare clic su **Avanti** nella pagina prima di iniziare hello.
   4. Selezionare **Installazione basata su ruoli o basata su funzionalità**, quindi fare clic su **Avanti**.
   5. Selezionare macchina locale hello hello elenco e quindi fare clic su **Avanti**.
   6. Selezionare **Servizi Desktop remoto** e fare clic su **Avanti**.
   7. Espandere **Interfacce utente e infrastruttura** e selezionare **Esperienza desktop**.
   8. Fare clic su **Aggiungi funzionalità** e quindi su **Avanti**.
   9. Nella pagina di hello Servizi Desktop remoto, fare clic su **Avanti**.
   10. Fare clic su **Host sessione Desktop remoto**.
   11. Fare clic su **Aggiungi funzionalità** e quindi su **Avanti**.
   12. Nella pagina hello Conferma selezioni per l'installazione, selezionare **riavvio del server di destinazione hello automaticamente se necessario**, quindi fare clic su **Sì** hello riavvio avviso.
   13. Fare clic su **Installa**. Hello computer verrà riavviato.
5. Installare funzionalità aggiuntive richieste dalle applicazioni, ad esempio hello .NET Framework 3.5. funzionalità di hello tooinstall, eseguire hello Aggiunta guidata ruoli e funzionalità.
6. Installare e configurare i programmi hello e applicazioni da toopublish tramite RemoteApp.

> [!IMPORTANT]
> Installare il ruolo di host sessione Desktop remoto hello prima di installare applicazioni tooensure che vengano rilevati problemi relativi alla compatibilità delle applicazioni prima immagine hello è caricato tooRemoteApp.
> 
> Verificare che un'applicazione tooyour di scelta rapida (**lnk** file) viene visualizzata in hello **avviare** menu per tutti gli utenti (%systemdrive%\ProgramData\Microsoft\Windows\Start Avvio\Programmi). Verificare inoltre che icona hello viene visualizzato in hello **avviare** menu sia quella desiderata toosee gli utenti. In caso contrario, modificarla (Non *hanno* menu Start di tooadd hello applicazione toohello, ma rende di molto più semplice applicazione hello toopublish in RemoteApp. In caso contrario, è tooprovide hello percorso di installazione hello applicazione quando si pubblica l'applicazione hello.)
> 
> 

1. Eseguire eventuali configurazioni aggiuntive di Windows richieste dalle applicazioni.
2. Disabilitare hello Encrypting File System (EFS). Eseguire hello seguente comando in una finestra di comando con privilegi elevati:
   
     Fsutil behavior set disableencryption 1
   
   In alternativa, è possibile impostare o aggiungere hello il valore DWORD nel Registro di sistema hello seguente:
   
     HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableEncryption = 1
3. Se si compila l'immagine all'interno di una macchina virtuale di Azure, rinominare hello  **\%windir%\Panther\Unattend.xml** file script di caricamento hello utilizzato in un secondo momento da in corso verrà bloccata. Modificare il nome di hello del tooUnattend.old file in modo che il file hello sarà comunque necessario nel caso in cui è necessario toorevert la distribuzione.
4. Andare tooWindows Update e installare tutti gli aggiornamenti importanti. Potrebbe essere necessario toorun Windows Update più volte tooget tutti gli aggiornamenti. (a volte un aggiornamento installato richiede a sua volta un aggiornamento).
5. Immagine SYSPREP hello. Al prompt dei comandi con privilegi elevati eseguire hello comando seguente:
   
   **C:\Windows\System32\sysprep\sysprep.exe /generalize /oobe /shutdown**
   
   **Nota:** non utilizzano hello **/mode: VM** commutatore di hello SYSPREP comando anche se si tratta di una macchina virtuale.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato l'immagine modello personalizzato, è necessario tooupload che tooyour immagine raccolta RemoteApp. La raccolta di, utilizzare informazioni hello in hello toocreate gli articoli seguenti:

* [Come toocreate una raccolta ibrida di RemoteApp](remoteapp-create-hybrid-deployment.md)
* [Come toocreate una raccolta di cloud di RemoteApp](remoteapp-create-cloud-deployment.md)

