---
title: aaaCreate un'immagine di Azure RemoteApp basata su una macchina virtuale di Azure | Documenti Microsoft
description: Informazioni su come toocreate un'immagine di Azure RemoteApp a partire da una macchina virtuale di Azure.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d41583ef-6cd8-4115-8dcb-b2cd5b3d301a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 2d432bcb15be68a2946d91b5f36f41d980726338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a>Creare un'immagine di Azure RemoteApp basata su una macchina virtuale di Azure
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

È possibile creare immagini di Azure RemoteApp (che contengono hello App che condivise nella raccolta) da una macchina virtuale di Azure. È anche possibile scegliere toouse un'immagine di macchina virtuale è stata aggiunta una raccolta di immagini di macchina virtuale di Azure toohello che soddisfi tutti i requisiti di immagine hello Azure RemoteApp, è possibile utilizzare l'immagine di macchina virtuale come punto di partenza per la propria macchina virtuale, se si desidera. Cercare solo l'immagine di "Windows Server Host sessione Desktop remoto" hello nella libreria hello.

Sono disponibili due passaggi toocreate, la propria immagine basata su una macchina virtuale di Azure: creare l'immagine di hello e quindi caricare il file da tooAzure libreria di hello macchina virtuale di Azure RemoteApp.

## <a name="create-a-custom-image-based-on-an-azure-vm"></a>Creare un'immagine personalizzata basata su una macchina virtuale di Azure
Utilizzare queste toocreate passaggi un'immagine basata su una macchina virtuale di Azure.

1. Creare una macchina virtuale di Azure. È possibile utilizzare hello "Windows Server Host sessione Desktop remoto" o "Windows Server Remote Desktop sessione Host con Microsoft Office 365 ProPlus" immagine di hello dalla raccolta di immagini di macchina virtuale di Azure hello. Questa immagine soddisfi tutti i requisiti di immagine hello Azure RemoteApp modello.
   
    Per i dettagli, vedere [Creare una macchina virtuale che esegue Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
2. Connettersi toohello macchina virtuale, installare e configurare App hello che si desidera tooshare tramite RemoteApp. Verificare che tooperform eventuali configurazioni aggiuntive di Windows necessari per le app.
   
    Per informazioni dettagliate, vedere [come tooLog nella macchina virtuale che esegue Windows Server tooa](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Se si utilizza una delle immagini di Windows Server Host sessione Desktop remoto hello, vi è uno script di convalida inclusi che garantirà che la macchina virtuale soddisfa hello RemoteApp pre-reqs. toorun script, fare doppio clic su **ValidateRemoteAppImage** sul desktop hello. Verificare che tutti gli errori segnalati dallo script hello risolti prima del passaggio successivo toohello di procedere.
4. SYSPREP generalizzare e acquisire l'immagine di hello. Vedere [come tooCapture tooUse una macchina virtuale di Windows come modello](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) per le istruzioni.

## <a name="import-hello-image-into-hello-azure-remoteapp-image-library"></a>Importare l'immagine hello in libreria di immagini di hello Azure RemoteApp
Utilizzare queste nuova immagine hello tooimport passaggi in Azure RemoteApp:

1. In hello **immagini modello** scheda:
   
   * Se non sono disponibili immagini, fare clic su **Caricare o importare un'immagine modello**.
   * Se si dispone già almeno un'immagine, fare clic su  **+**  tooadd una nuova immagine.
2. Selezionare **Importare un'immagine dalla raccolta di macchine virtuali** e fare clic su **Avanti**.
3. Nella pagina successiva di hello, selezionare l'immagine personalizzata hello elenco e verificare che siano seguite illustrate hello al momento della creazione dell'immagine. Fare clic su **Avanti**.
4. Immettere un nome per la nuova immagine di RemoteApp hello e scegliere il percorso di hello, quindi fare clic su processo di importazione hello toostart hello segno di spunta.

> [!NOTE]
> È possibile importare immagini da qualsiasi posizione di Azure supportati da macchine virtuali di Azure tooany località di Azure supportati da Azure RemoteApp. A seconda delle posizioni hello importazione hello può richiedere too25 minuti.
> 
> 

È ora pronto toocreate la nuova raccolta, ovvero un [cloud](remoteapp-create-cloud-deployment.md) insieme o [ibrida](remoteapp-create-hybrid-deployment.md), in base alle proprie esigenze.

