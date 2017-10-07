---
title: un'immagine di una macchina virtuale Windows Azure aaaCapture | Documenti Microsoft
description: Acquisire un'immagine di una macchina virtuale Windows Azure creata con il modello di distribuzione classica hello.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: a5986eac-4cf3-40bd-9b79-7c811806b880
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: b9bbc437012aa44295f90941c9d72e39509df28f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-hello-classic-deployment-model"></a>Acquisire un'immagine di una macchina virtuale Windows Azure creata con il modello di distribuzione classica hello.
> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Per informazioni sul modello di Gestione risorse, vedere [Acquisire un'immagine gestita di una macchina virtuale generalizzata in Azure](../capture-image-resource.md).

In questo articolo illustra come toocapture macchina virtuale di Azure che esegue Windows in modo da utilizzare come un'immagine toocreate altre macchine virtuali. Questa immagine include disco del sistema operativo hello e i dischi dati sono collegati macchina virtuale toohello. Non include le configurazioni di rete, pertanto sarà necessario tooset le configurazioni di rete quando si crea hello altre macchine virtuali che utilizzano l'immagine di hello.

Archivi Azure hello immagine in **immagini di macchina virtuale (classico)**, **calcolo** hello di servizio elencato quando si visualizza tutti i servizi di Azure. Si tratta di hello stessa posizione in cui sono archiviate tutte le immagini caricate dall'utente. Per altre informazioni sulle immagini, vedere [Informazioni sulle immagini per le macchine virtuali Linux](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).

## <a name="before-you-begin"></a>Prima di iniziare
Questa procedura si presuppone di aver già creato una macchina virtuale di Azure e configurato hello di sistema, incluso il collegamento a eventuali dischi dati. Se non è stata eseguita questa operazione, vedere i seguenti articoli per informazioni sulla creazione e la preparazione della macchina virtuale hello hello:

* [Creare una macchina virtuale da un'immagine](createportal.md)
* [Come tooattach dati su disco di macchina virtuale tooa](attach-disk.md)
* Assicurarsi che i ruoli del server hello sono supportati con Sysprep. Per ulteriori informazioni, vedere [Supporto Sysprep per i ruoli server](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).

> [!WARNING]
> Questo processo Elimina macchina virtuale originale hello dopo l'acquisizione.
>
>

Precedente toocapturing un'immagine di macchina virtuale di Azure, è consigliabile eseguire il backup hello macchina virtuale di destinazione. È possibile eseguire il backup delle macchine virtuali di Azure con Backup di Azure. Per informazioni dettagliate, vedere [Backup delle macchine virtuali di Azure](../../../backup/backup-azure-vms.md). Altre soluzioni sono disponibili da partner certificati. toofind sulle risorse attualmente disponibili, eseguire la ricerca hello Azure Marketplace.

## <a name="capture-hello-virtual-machine"></a>Acquisire una macchina virtuale hello
1. In hello [portale di Azure](http://portal.azure.com), **Connetti** macchina virtuale toohello. Per istruzioni, vedere [come toosign nella macchina virtuale tooa che esegue Windows Server][How toosign in tooa virtual machine running Windows Server].
2. Aprire una finestra del Prompt dei comandi come amministratore.
3. Modificare anche le directory hello`%windir%\system32\sysprep`, quindi eseguire sysprep.exe.
4. Hello **System Preparation Tool** viene visualizzata la finestra di dialogo. Hello seguenti:

   * In **Azione pulizia sistema** selezionare **Passare alla Configurazione guidata** e verificare che l'opzione **Generalizza** sia selezionata. Per ulteriori informazioni sull'utilizzo di Sysprep, vedere [come tooUse Sysprep: An Introduction][How tooUse Sysprep: An Introduction].
   * In **Opzioni di arresto del sistema** selezionare **Arresta il sistema**.
   * Fare clic su **OK**.

   ![Eseguire Sysprep.](./media/capture-image/SysprepGeneral.png)
5. Sysprep arresta la macchina virtuale di hello, che modifica lo stato di hello della macchina virtuale hello nel portale di Azure hello troppo**arrestato**.
6. Nel portale di Azure hello, fare clic su **macchine virtuali (classico)** e selezionare hello macchina virtuale da toocapture. Hello **immagini di macchina virtuale (classico)** gruppo è elencato in **calcolo** quando si visualizza **più servizi**.

7. Nella barra dei comandi di hello, fare clic su **acquisire**.

   ![Acquisire la macchina virtuale](./media/capture-image/CaptureVM.png)

   Hello **hello acquisizione macchina virtuale** viene visualizzata la finestra di dialogo.

8. In **nome immagine**, digitare un nome per la nuova immagine hello. In **etichetta immagine**, digitare un'etichetta per la nuova immagine hello.

9. Fare clic su **Sysprep è stato eseguito sulla macchina virtuale hello**. Questa casella di controllo si riferisce toohello azioni con Sysprep nei passaggi 3-5. Un'immagine _deve_ generalizzati eseguendo Sysprep prima di aggiungere un Server Windows set tooyour immagine di immagini personalizzate.

10. Al termine dell'acquisizione hello, nuova immagine hello viene reso disponibile in hello **Marketplace**, in hello **calcolo**, **immagini di macchina virtuale (classico)** contenitore.

    ![Acquisizione dell'immagine eseguita correttamente](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a>Passaggi successivi
immagine di Hello è pronto toobe utilizzato toocreate le macchine virtuali. toodo, si creerà una macchina virtuale selezionando hello **più servizi** voce di menu nella parte inferiore di hello di hello dal menu servizi, quindi **immagini di macchina virtuale (classico)** in hello **calcolo**gruppo. Per istruzioni, vedere [Creare una macchina virtuale da un'immagine](createportal.md).

[How toosign in tooa virtual machine running Windows Server]:connect-logon.md
[How tooUse Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[hello virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of hello virtual machine]: ./media/capture-image/CaptureVM.png
[Enter hello image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use hello captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
