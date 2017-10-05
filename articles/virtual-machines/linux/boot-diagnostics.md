---
title: Diagnostica di avvio per le macchine virtuali Linux in Azure | Microsoft Docs
description: "Panoramica delle due funzionalità di debug per le macchine virtuali Linux in Azure"
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
ms.openlocfilehash: 70254d39b5c6326166f7e29fdfc99533835502f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-boot-diagnostics-to-troubleshoot-linux-virtual-machines-in-azure"></a><span data-ttu-id="6089a-103">Come usare la diagnostica di avvio per risolvere i problemi relativi alle macchine virtuali Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="6089a-103">How to use boot diagnostics to troubleshoot Linux virtual machines in Azure</span></span>

<span data-ttu-id="6089a-104">In Azure ora è disponibile il supporto per due funzionalità di debug: il supporto per l'output della console e per gli screenshot per il modello di distribuzione Resource Manager di Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="6089a-104">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="6089a-105">Quando si usa l'immagine personale in Azure o anche quando si avvia una delle immagini della piattaforma, una macchina virtuale può passare a uno stato non avviabile per diversi motivi.</span><span class="sxs-lookup"><span data-stu-id="6089a-105">When bringing your own image to Azure or even booting one of the platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="6089a-106">Queste funzionalità consentono di diagnosticare facilmente gli errori di avvio e di ripristinare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="6089a-106">These features enable you to easily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="6089a-107">Per le macchine virtuali Linux, è possibile visualizzare facilmente l'output del log della console dal portale:</span><span class="sxs-lookup"><span data-stu-id="6089a-107">For Linux Virtual Machines, you can easily view the output of your console log from the Portal:</span></span>

![Portale di Azure](./media/boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="6089a-109">Per le macchine virtuali sia Windows che Linux, Azure consente anche di visualizzare uno screenshot della VM dall'hypervisor:</span><span class="sxs-lookup"><span data-stu-id="6089a-109">However, for both Windows and Linux Virtual Machines, Azure also enables you to see a screenshot of the VM from the hypervisor:</span></span>

![Errore](./media/boot-diagnostics/screenshot2.png)

<span data-ttu-id="6089a-111">Entrambe le funzionalità sono supportate per Macchine virtuali di Azure in tutte le aree.</span><span class="sxs-lookup"><span data-stu-id="6089a-111">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="6089a-112">Si noti che la visualizzazione degli screenshot e dell'output nell'account di archiviazione può richiedere fino a 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="6089a-112">Note, screenshots, and output can take up to 10 minutes to appear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="6089a-113">Errori di avvio comuni</span><span class="sxs-lookup"><span data-stu-id="6089a-113">Common boot errors</span></span>

- [<span data-ttu-id="6089a-114">Problemi del file system</span><span class="sxs-lookup"><span data-stu-id="6089a-114">File system issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [<span data-ttu-id="6089a-115">Problemi del kernel</span><span class="sxs-lookup"><span data-stu-id="6089a-115">Kernel Issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [<span data-ttu-id="6089a-116">Errori relativi alla tabella del file system</span><span class="sxs-lookup"><span data-stu-id="6089a-116">FSTAB errors</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="6089a-117">Abilitare la diagnostica in una nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="6089a-117">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="6089a-118">Quando si crea una nuova macchina virtuale dal portale di anteprima, selezionare **Azure Resource Manager** dall'elenco a discesa del modello di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="6089a-118">When creating a new Virtual Machine from the Preview Portal, select the **Azure Resource Manager** from the deployment model dropdown:</span></span>
 
    ![Gestione risorse](./media/boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="6089a-120">Configurare l'opzione Monitoraggio per selezionare l'account di archiviazione in cui si vogliono inserire questi file di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="6089a-120">Configure the Monitoring option to select the storage account where you would like to place these diagnostic files.</span></span>
 
    ![Creare una macchina virtuale](./media/boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="6089a-122">Se si esegue la distribuzione da un modello di Azure Resource Manager, passare alla risorsa macchina virtuale e aggiungere la sezione del profilo di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="6089a-122">If you are deploying from an Azure Resource Manager template, navigate to your Virtual Machine resource and append the diagnostics profile section.</span></span> <span data-ttu-id="6089a-123">Si ricordi di usare l'intestazione di versione API "2015-06-15".</span><span class="sxs-lookup"><span data-stu-id="6089a-123">Remember to use the “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="6089a-124">Il profilo di diagnostica consente di selezionare l'account di archiviazione in cui si vogliono inserire questi log.</span><span class="sxs-lookup"><span data-stu-id="6089a-124">The diagnostics profile enables you to select the storage account where you want to put these logs.</span></span>

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

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="6089a-125">Aggiornare una macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="6089a-125">Update an existing virtual machine</span></span>

<span data-ttu-id="6089a-126">Per abilitare la diagnostica dal portale, è anche possibile aggiornare una macchina virtuale esistente dal portale.</span><span class="sxs-lookup"><span data-stu-id="6089a-126">To enable boot diagnostics through the portal, you can also update an existing virtual machine through the portal.</span></span> <span data-ttu-id="6089a-127">Selezionare l'opzione Diagnostica di avvio e fare clic su Salva.</span><span class="sxs-lookup"><span data-stu-id="6089a-127">Select the Boot Diagnostics option and Save.</span></span> <span data-ttu-id="6089a-128">Riavviare la VM per rendere effettivo l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="6089a-128">Restart the VM to take effect.</span></span>

![Aggiornare una VM esistente](./media/boot-diagnostics/screenshot5.png)