---
title: una macchina virtuale nel portale di Azure hello aaaCreate | Documenti Microsoft
description: Creare una macchina virtuale Windows in hello portale di Azure.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 3848a3d06a7ce377633db78ea385826ed40f94fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-running-windows-in-hello-azure-portal"></a>Creare una macchina virtuale Windows in esecuzione in hello portale di Azure
> [!div class="op_single_selector"]
> * [Portale di Azure](tutorial.md)
> * [PowerShell: distribuzione classica](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Informazioni su come troppo[eseguire questi passaggi tramite il modello di distribuzione di gestione risorse di hello](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) utilizzando hello **portale di Azure**.

In questa esercitazione illustra come toocreate di Azure macchina virtuale (VM) in esecuzione Windows in hello portale di Azure. Si userà un'immagine di Windows Server, ad esempio, ma che è solo una di hello molte immagini offerte di Azure. Si noti che le opzioni dell’immagine dipendono dalla sottoscrizione. Ad esempio, le immagini del desktop di Windows potrebbero essere disponibile tooMSDN sottoscrittori.

In questa sezione illustra come hello toouse **Dashboard** in hello tooselect portale Azure e quindi creare macchine virtuali hello.

È inoltre possibile creare VM usando le [proprie immagini](createupload-vhd.md). toolearn su questo e altri metodi, vedere [toocreate modi diversi una macchina virtuale Windows](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

<!-- 02/27/2017 Video removed as it was based on hello classic portal. -->

## <a id="createvirtualmachine"></a>Crea macchina virtuale hello
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[creare una macchina virtuale con modello di distribuzione di gestione risorse di hello](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in hello portale di Azure.
* Accedere a macchina virtuale toohello. Per istruzioni, vedere [accedere alla macchina virtuale tooa che esegue Windows Server](connect-logon.md).
* Collegare un dati toostore su disco. È possibile collegare sia dischi vuoti sia dischi contenenti dati. Per istruzioni, vedere hello [collegare una macchina virtuale di Windows di dati su disco tooa creata con il modello di distribuzione classica hello](attach-disk.md).
