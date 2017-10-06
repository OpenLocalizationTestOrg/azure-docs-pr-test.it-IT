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
# <a name="how-toouse-boot-diagnostics-tootroubleshoot-linux-virtual-machines-in-azure"></a><span data-ttu-id="fb2ac-103">Come toouse Avvio diagnostica tootroubleshoot le macchine virtuali Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="fb2ac-103">How toouse boot diagnostics tootroubleshoot Linux virtual machines in Azure</span></span>

<span data-ttu-id="fb2ac-104">In Azure ora è disponibile il supporto per due funzionalità di debug: il supporto per l'output della console e per gli screenshot per il modello di distribuzione Resource Manager di Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="fb2ac-104">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="fb2ac-105">Quando si attiva la propria immagine tooAzure o anche l'avvio delle immagini della piattaforma hello, possono esistere molti motivi per cui una macchina virtuale ottiene in uno stato non avviabile.</span><span class="sxs-lookup"><span data-stu-id="fb2ac-105">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="fb2ac-106">Questi consentono di funzionalità si tooeasily diagnosticare e ripristinare le macchine virtuali da errori di avvio.</span><span class="sxs-lookup"><span data-stu-id="fb2ac-106">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="fb2ac-107">Per macchine virtuali Linux, è possibile visualizzare facilmente output di hello del log dal portale hello console:</span><span class="sxs-lookup"><span data-stu-id="fb2ac-107">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Portale di Azure](./media/boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="fb2ac-109">Tuttavia, per Windows e macchine virtuali Linux, Azure consente inoltre di toosee una schermata di hello VM dall'hypervisor hello:</span><span class="sxs-lookup"><span data-stu-id="fb2ac-109">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![Errore](./media/boot-diagnostics/screenshot2.png)

<span data-ttu-id="fb2ac-111">Entrambe le funzionalità sono supportate per Macchine virtuali di Azure in tutte le aree.</span><span class="sxs-lookup"><span data-stu-id="fb2ac-111">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="fb2ac-112">Si noti, schermate e l'output può richiedere fino a too10 minuti tooappear nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="fb2ac-112">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="fb2ac-113">Errori di avvio comuni</span><span class="sxs-lookup"><span data-stu-id="fb2ac-113">Common boot errors</span></span>

- [<span data-ttu-id="fb2ac-114">Problemi del file system</span><span class="sxs-lookup"><span data-stu-id="fb2ac-114">File system issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [<span data-ttu-id="fb2ac-115">Problemi del kernel</span><span class="sxs-lookup"><span data-stu-id="fb2ac-115">Kernel Issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [<span data-ttu-id="fb2ac-116">Errori relativi alla tabella del file system</span><span class="sxs-lookup"><span data-stu-id="fb2ac-116">FSTAB errors</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="fb2ac-117">Abilitare la diagnostica in una nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="fb2ac-117">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="fb2ac-118">Quando si crea una nuova macchina virtuale dal portale di anteprima di hello, selezionare hello **Azure Resource Manager** dall'elenco a discesa modello di distribuzione hello:</span><span class="sxs-lookup"><span data-stu-id="fb2ac-118">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![Gestione risorse](./media/boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="fb2ac-120">Configurare monitoraggio opzione tooselect hello account di archiviazione in cui si desidera tooplace hello questi file di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="fb2ac-120">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![Creare una macchina virtuale](./media/boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="fb2ac-122">Se si distribuisce un modello di gestione risorse di Azure, passare la risorsa di macchina virtuale tooyour e aggiungere una sezione del profilo di diagnostica hello.</span><span class="sxs-lookup"><span data-stu-id="fb2ac-122">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="fb2ac-123">Ricordare di intestazione della versione API toouse hello "2015-06-15".</span><span class="sxs-lookup"><span data-stu-id="fb2ac-123">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="fb2ac-124">profilo di diagnostica Hello consente tooselect hello account di archiviazione in cui tooput questi registri.</span><span class="sxs-lookup"><span data-stu-id="fb2ac-124">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

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

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="fb2ac-125">Aggiornare una macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="fb2ac-125">Update an existing virtual machine</span></span>

<span data-ttu-id="fb2ac-126">diagnostica di avvio tooenable tramite il portale di hello, è possibile aggiornare una macchina virtuale esistente tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="fb2ac-126">tooenable boot diagnostics through hello portal, you can also update an existing virtual machine through hello portal.</span></span> <span data-ttu-id="fb2ac-127">La diagnostica di avvio hello seleziona l'opzione e salvare.</span><span class="sxs-lookup"><span data-stu-id="fb2ac-127">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="fb2ac-128">Riavviare l'effetto di tootake hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fb2ac-128">Restart hello VM tootake effect.</span></span>

![Aggiornare una VM esistente](./media/boot-diagnostics/screenshot5.png)