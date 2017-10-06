---
title: diagnostica aaaBoot per le macchine virtuali Linux in Azure | Documento di Microsoft
description: "Panoramica delle funzionalità di debug due hello per le macchine virtuali Linux in Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: Deland-Han
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: delhan
ms.openlocfilehash: d355d512de09d2f1d7a2718e3db3fb99c9dd9e24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-boot-diagnostics-tootroubleshoot-linux-virtual-machines-in-azure"></a>Come toouse Avvio diagnostica tootroubleshoot le macchine virtuali Linux in Azure

In Azure ora è disponibile il supporto per due funzionalità di debug: il supporto per l'output della console e per gli screenshot per il modello di distribuzione Resource Manager di Macchine virtuali di Azure. 

Quando si attiva la propria immagine tooAzure o anche l'avvio delle immagini della piattaforma hello, possono esistere molti motivi per cui una macchina virtuale ottiene in uno stato non avviabile. Questi consentono di funzionalità si tooeasily diagnosticare e ripristinare le macchine virtuali da errori di avvio.

Per macchine virtuali Linux, è possibile visualizzare facilmente output di hello del log dal portale hello console:

![Portale di Azure](./media/boot-diagnostics/screenshot1.png)
 
Tuttavia, per Windows e macchine virtuali Linux, Azure consente inoltre di toosee una schermata di hello VM dall'hypervisor hello:

![Errore](./media/boot-diagnostics/screenshot2.png)

Entrambe le funzionalità sono supportate per Macchine virtuali di Azure in tutte le aree. Si noti, schermate e l'output può richiedere fino a too10 minuti tooappear nell'account di archiviazione.

## <a name="common-boot-errors"></a>Errori di avvio comuni

- [Problemi del file system](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [Problemi del kernel](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [Errori relativi alla tabella del file system](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a>Abilitare la diagnostica in una nuova macchina virtuale
1. Quando si crea una nuova macchina virtuale dal portale di anteprima di hello, selezionare hello **Azure Resource Manager** dall'elenco a discesa modello di distribuzione hello:
 
    ![Gestione risorse](./media/boot-diagnostics/screenshot3.jpg)

2. Configurare monitoraggio opzione tooselect hello account di archiviazione in cui si desidera tooplace hello questi file di diagnostica.
 
    ![Creare una macchina virtuale](./media/boot-diagnostics/screenshot4.jpg)

3. Se si distribuisce un modello di gestione risorse di Azure, passare la risorsa di macchina virtuale tooyour e aggiungere una sezione del profilo di diagnostica hello. Ricordare di intestazione della versione API toouse hello "2015-06-15".

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. profilo di diagnostica Hello consente tooselect hello account di archiviazione in cui tooput questi registri.

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

## <a name="update-an-existing-virtual-machine"></a>Aggiornare una macchina virtuale esistente

diagnostica di avvio tooenable tramite il portale di hello, è possibile aggiornare una macchina virtuale esistente tramite il portale di hello. La diagnostica di avvio hello seleziona l'opzione e salvare. Riavviare l'effetto di tootake hello macchina virtuale.

![Aggiornare una VM esistente](./media/boot-diagnostics/screenshot5.png)