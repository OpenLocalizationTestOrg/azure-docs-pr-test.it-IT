---
title: aaaReset una password locale di Windows senza agente di Azure | Documenti Microsoft
description: "Come tooreset hello password dell'account utente locale di Windows quando l'agente guest Azure hello non è installato o funzionante in una macchina virtuale"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf353dd3-89c9-47f6-a449-f874f0957013
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/07/2017
ms.author: iainfou
ms.openlocfilehash: c559c31ea142f9cf50d2c5b6182c5355fec9bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a>Come tooreset password di Windows locale per la macchina virtuale di Azure
È possibile reimpostare la password di Windows locale di hello di una macchina virtuale in Azure utilizzando hello [portale di Azure o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) fornito è installato l'agente guest Azure hello. Questo metodo è hello tooreset di mezzo principale con una password per una macchina virtuale di Azure. Se si verificano problemi con l'agente guest Azure hello non risponde o non superati tooinstall dopo il caricamento di un'immagine personalizzata, è possibile reimpostare manualmente una password di Windows. In questo articolo illustra in dettaglio come tooreset una password di account locale mediante l'aggiunta di hello tooanother disco virtuale di origine del sistema operativo VM. 

> [!WARNING]
> Questo processo viene usato solo come ultima risorsa. Provare sempre una password utilizzando hello tooreset [portale di Azure o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) prima.
> 
> 

## <a name="overview-of-hello-process"></a>Panoramica del processo di hello
passaggi di base Hello per l'esecuzione di una password locale reimpostata per una macchina virtuale Windows in Azure quando nessun agente guest Azure toohello di accesso è il seguente:

* Eliminare una macchina virtuale di origine hello. i dischi virtuali Hello vengono mantenuti.
* Collegare tooanother disco della macchina virtuale di hello origine del sistema operativo VM su hello stessa posizione all'interno di sottoscrizione di Azure. Questa macchina virtuale è hello di cui viene fatto riferimento tooas risoluzione dei problemi di macchina virtuale.
* Utilizzando hello risoluzione dei problemi di macchina virtuale, creare i file di configurazione dal disco del sistema operativo della macchina virtuale di hello origine.
* Scollegare il disco del sistema operativo della macchina virtuale di hello da hello risoluzione dei problemi di macchina virtuale.
* Utilizzare un toocreate di gestione risorse modello una macchina virtuale con disco virtuale originale hello.
* Quando viene avviato a nuova macchina virtuale, hello hello i file di configurazione è creare hello aggiornamento della password dell'utente hello necessario.

## <a name="detailed-steps"></a>Procedura dettagliata
Provare sempre una password utilizzando hello tooreset [portale di Azure o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) prima di tentare di hello alla procedura seguente. Assicurarsi di disporre di un backup della VM prima di iniziare. 

1. Eliminare hello interessate VM nel portale di Azure. L'eliminazione hello VM Elimina solo i metadati hello, riferimento hello di hello VM in Azure. i dischi virtuali Hello vengono mantenuti quando viene eliminato hello VM:
   
   * Fare clic su hello seleziona macchina virtuale nel portale di Azure hello *eliminare*:
     
     ![Eliminare la VM esistente](./media/reset-local-password-without-agent/delete_vm.png)
2. Collegare toohello di disco del sistema operativo della macchina virtuale di hello origine risoluzione dei problemi di macchina virtuale. Hello risoluzione dei problemi di macchina virtuale deve essere in hello stessa area come disco del sistema operativo della macchina virtuale di hello origine (ad esempio `West US`):
   
   * Selezionare la risoluzione dei problemi di macchina virtuale nel portale di Azure hello hello. Fare clic su *Dischi* | *Collega esistente*:
     
     ![Collegare un disco esistente](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     Selezionare *File VHD* e quindi selezionare l'account di archiviazione hello che contiene la macchina virtuale di origine:
     
     ![Selezionare l'account di archiviazione](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     Selezionare il contenitore di origine hello. contenitore di origine Hello è in genere *dischi rigidi virtuali*:
     
     ![Selezionare il contenitore di archiviazione](./media/reset-local-password-without-agent/disks_select_container.png)
     
     Selezionare hello tooattach di disco rigido virtuale del sistema operativo. Fare clic su *selezionare* processo hello toocomplete:
     
     ![Selezionare il disco virtuale di origine](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. Toohello macchina virtuale tramite Desktop remoto di risoluzione dei problemi di connessione e assicurarsi che è visibile disco del sistema operativo della macchina virtuale di hello origine:
   
   * Selezionare la risoluzione dei problemi di macchina virtuale nel portale di Azure hello hello e fare clic su *Connetti*.
   * Aprire il file RDP hello che scarica. Immettere nome utente di hello e la password di hello risoluzione dei problemi di macchina virtuale.
   * In Esplora File, cercare il disco di dati hello che è collegato. Se hello origine che disco rigido virtuale della macchina virtuale è hello toohello disco collegato dati solo la risoluzione dei problemi di macchina virtuale, questa deve essere unità f: hello:
     
     ![Visualizzare il disco dati collegato](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. Creare `gpt.ini` in `\Windows\System32\GroupPolicy` sul disco della macchina virtuale di hello origine (se esiste gpt.ini, rinominare toogpt.ini.bak):
   
   > [!WARNING]
   > Assicurarsi che non accidentalmente creare hello i seguenti file in C:\Windows, hello unità del sistema operativo per la risoluzione dei problemi di VM hello. Creare i seguenti file nell'unità di hello del sistema operativo per la macchina virtuale che viene collegato un disco dati di origine hello.
   > 
   > 
   
   * Aggiungere hello dopo le righe in hello `gpt.ini` file creato:
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![Creare gpt.ini](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. Creare `scripts.ini` in `\Windows\System32\GroupPolicy\Machine\Scripts`. Accertarsi che vengano visualizzate le cartelle nascoste. Se necessario, creare hello `Machine` o `Scripts` cartelle.
   
   * Aggiungere hello seguente hello righe `scripts.ini` file creato:
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![Creare scripts.ini](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. Creare `FixAzureVM.cmd` in `\Windows\System32` con hello contenuto seguente, sostituendo `<username>` e `<newpassword>` con valori personalizzati:
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![Creare FixAzureVM.cmd](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    Quando si definisce una nuova password hello, è necessario soddisfare i requisiti di complessità password hello configurato per la macchina virtuale.
7. Nel portale di Azure, scollegare il disco di hello dalla risoluzione dei problemi di VM hello:
   
   * Selezionare la risoluzione dei problemi di macchina virtuale nel portale di Azure hello hello, fare clic su *dischi*.
   * I dischi di dati selezionare hello collegati nel passaggio 2, fare clic su *scollegamento*:
     
     ![Scollegare il disco](./media/reset-local-password-without-agent/detach_disk.png)
8. Prima di creare una macchina virtuale, è possibile ottenere il disco del sistema operativo di hello URI tooyour origine:
   
   * Fare clic su account di archiviazione hello selezionare nel portale di Azure hello *BLOB*.
   * Selezionare il contenitore di hello. contenitore di origine Hello è in genere *dischi rigidi virtuali*:
     
     ![Selezionare il BLOB dell'account di archiviazione](./media/reset-local-password-without-agent/select_storage_details.png)
     
     Selezionare il disco rigido virtuale del sistema operativo VM di origine e fare clic su hello *copia* pulsante Avanti toohello *URL* nome:
     
     ![Copiare l'URI del disco](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. Creare una macchina virtuale dal disco del sistema operativo della macchina virtuale di hello origine:
   
   * Utilizzare [questo modello di gestione risorse di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate una macchina virtuale da un disco rigido virtuale specializzata. Fare clic su hello `Deploy tooAzure` hello tooopen pulsante portale di Azure con i dettagli di hello basati su modelli popolato automaticamente.
   * Se si desiderano tooretain tutte le impostazioni precedenti hello per hello macchina virtuale, selezionare *modifica modelli* tooprovide la rete virtuale esistente, subnet, scheda di rete o indirizzo IP pubblico.
   * In hello `OSDISKVHDURI` la casella di testo di parametro, hello Incolla ottenere l'URI dell'origine del disco rigido virtuale nel precedente passaggio hello:
     
     ![Creare una VM dal modello](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. Dopo aver hello nuova macchina virtuale è in esecuzione, connettersi toohello macchina virtuale tramite Desktop remoto con password hello specificata in hello `FixAzureVM.cmd` script.
11. Da toohello la sessione remota nuova macchina virtuale, rimuovere hello seguente file tooclean ambiente hello:
    
    * Da %windir%\System32
      * rimuovere FixAzureVM.cmd
    * Da %windir%\System32\GroupPolicy\Machine\
      * rimuovere scripts.ini
    * Da %windir%\System32\GroupPolicy
      * rimuovere gpt.ini (gpt.ini esistenti prima, se è stata rinominata toogpt.ini.bak, ridenominazione hello bak file indietro toogpt.ini)

## <a name="next-steps"></a>Passaggi successivi
Se non è possibile connettersi tramite Desktop remoto, vedere hello [Guida alla risoluzione dei problemi di RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Hello [RDP risoluzione dei problemi di Guida dettagliate](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) esamina la risoluzione dei problemi relativi a metodi anziché i passaggi specifici. È anche possibile [aprire una richiesta di supporto tecnico di Azure](https://azure.microsoft.com/support/options/) per ricevere un supporto pratico.

