---
title: una macchina virtuale di Windows nel modello di distribuzione classica hello - Azure aaaResize | Documenti Microsoft
description: Ridimensionare una macchina virtuale di Windows creata nel modello di distribuzione classica hello, tramite Azure Powershell.
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e3038215-001c-406e-904d-e0f4e326a4c7
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 39fab14431e2351c9515b0611e850eccfec7a798
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm-created-in-hello-classic-deployment-model"></a>Ridimensiona una macchina virtuale Windows creata nel modello di distribuzione classica hello
Questo articolo illustra come tooresize macchine Virtuali di Windows creati nel modello di distribuzione classica hello con Azure Powershell.

Quando si considerano hello possibilità tooresize una macchina virtuale, esistono due concetti che controllano l'intervallo di hello della macchina virtuale di dimensioni disponibili tooresize hello. primo concetto Hello è area hello in cui è distribuita la macchina virtuale. elenco di Hello di dimensioni disponibili nell'area è nella scheda Servizi hello della pagina web di hello aree di Azure. concetto secondo Hello è hello all'hardware fisico che ospita la macchina virtuale. Hello fisici che ospitano macchine virtuali viene raggruppati in cluster di hardware fisico comuni. metodo Hello della modifica di una dimensione di macchina virtuale è diverso a seconda se hello desiderato nuova dimensione di macchina virtuale è supportato dal cluster hardware hello attualmente ospitando hello macchina virtuale.

> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. È anche possibile [ridimensiona una macchina virtuale creata nel modello di distribuzione di gestione risorse di hello](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="add-your-account"></a>Aggiungere il proprio account
È necessario configurare Azure PowerShell toowork con risorse di Azure classiche. Seguire i passaggi di hello sotto le risorse classiche tooconfigure Azure PowerShell toomanage.

1. Al prompt di PowerShell hello digitare `Add-AzureAccount` e fare clic su **invio**. 
2. Digitare l'indirizzo di posta elettronica hello associati alla sottoscrizione Azure e fare clic su **continua**. 
3. Digitare la password dell'account hello. 
4. Fare clic su **Accedi**. 

## <a name="resize-in-hello-same-hardware-cluster"></a>Ridimensionare in hello stesso cluster hardware
tooresize dimensione tooa macchina virtuale disponibile in cluster hardware hello hosting hello macchina virtuale, eseguire hello alla procedura seguente.

1. Eseguire il comando PowerShell toolist hello dimensioni delle macchine Virtuali disponibili in hello hardware cluster ospita hello cloud servizio che contiene hello VM seguente hello.
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. Eseguire hello seguenti comandi tooresize hello macchina virtuale.
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a>Ridimensionare in un nuovo cluster hardware
dimensione tooa macchina virtuale non è disponibile in hello hardware cluster ospita tooresize hello VM, hello servizio cloud e tutte le macchine virtuali nel servizio cloud hello devono essere ricreate. Ogni servizio cloud è ospitato in un cluster singolo hardware pertanto tutte le macchine virtuali nel servizio cloud hello devono essere una dimensione è supportata in un cluster hardware. Hello seguente verrà descritta la modalità tooresize una macchina virtuale eliminando e ricreando quindi hello cloud service.

1. Eseguire hello seguente PowerShell comando toolist hello dimensioni delle macchine Virtuali disponibili nell'area di hello. 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. Prendere nota di tutte le impostazioni di configurazione per ogni macchina virtuale nel servizio cloud hello contenente hello VM toobe ridimensionato. 
3. Eliminare tutte le macchine virtuali nel servizio cloud hello selezionando i dischi di hello hello opzione tooretain per ogni macchina virtuale.
4. Ricreare hello VM toobe ridimensionato con dimensioni VM hello desiderato.
5. Ricreare tutte le altre macchine virtuali che erano presenti nel servizio cloud hello utilizzando una dimensione di macchina virtuale disponibile in cluster hardware hello ora ospita il servizio di cloud hello.

Uno script di esempio per l'eliminazione e la nuova creazione di un servizio cloud mediante una nuova dimensione di VM è disponibile [qui](https://github.com/Azure/azure-vm-scripts). 

## <a name="next-steps"></a>Passaggi successivi
* [Ridimensiona una macchina virtuale creata nel modello di distribuzione di gestione risorse di hello](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

