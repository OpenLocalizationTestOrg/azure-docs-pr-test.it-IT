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
# <a name="resize-a-windows-vm-created-in-hello-classic-deployment-model"></a><span data-ttu-id="d21d0-103">Ridimensiona una macchina virtuale Windows creata nel modello di distribuzione classica hello</span><span class="sxs-lookup"><span data-stu-id="d21d0-103">Resize a Windows VM created in hello classic deployment model</span></span>
<span data-ttu-id="d21d0-104">Questo articolo illustra come tooresize macchine Virtuali di Windows creati nel modello di distribuzione classica hello con Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="d21d0-104">This article shows you how tooresize a Windows VM, created in hello classic deployment model using Azure Powershell.</span></span>

<span data-ttu-id="d21d0-105">Quando si considerano hello possibilità tooresize una macchina virtuale, esistono due concetti che controllano l'intervallo di hello della macchina virtuale di dimensioni disponibili tooresize hello.</span><span class="sxs-lookup"><span data-stu-id="d21d0-105">When considering hello ability tooresize a VM, there are two concepts which control hello range of sizes available tooresize hello virtual machine.</span></span> <span data-ttu-id="d21d0-106">primo concetto Hello è area hello in cui è distribuita la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d21d0-106">hello first concept is hello region in which your VM is deployed.</span></span> <span data-ttu-id="d21d0-107">elenco di Hello di dimensioni disponibili nell'area è nella scheda Servizi hello della pagina web di hello aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="d21d0-107">hello list of VM sizes available in region is under hello Services tab of hello Azure Regions web page.</span></span> <span data-ttu-id="d21d0-108">concetto secondo Hello è hello all'hardware fisico che ospita la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d21d0-108">hello second concept is hello physical hardware currently hosting your VM.</span></span> <span data-ttu-id="d21d0-109">Hello fisici che ospitano macchine virtuali viene raggruppati in cluster di hardware fisico comuni.</span><span class="sxs-lookup"><span data-stu-id="d21d0-109">hello physical servers hosting VMs are grouped together in clusters of common physical hardware.</span></span> <span data-ttu-id="d21d0-110">metodo Hello della modifica di una dimensione di macchina virtuale è diverso a seconda se hello desiderato nuova dimensione di macchina virtuale è supportato dal cluster hardware hello attualmente ospitando hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d21d0-110">hello method of changing a VM size differs depending on if hello desired new VM size is supported by hello hardware cluster currently hosting hello VM.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="d21d0-111">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d21d0-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d21d0-112">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="d21d0-112">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="d21d0-113">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="d21d0-113">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="d21d0-114">È anche possibile [ridimensiona una macchina virtuale creata nel modello di distribuzione di gestione risorse di hello](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d21d0-114">You can also [resize a VM created in hello Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="add-your-account"></a><span data-ttu-id="d21d0-115">Aggiungere il proprio account</span><span class="sxs-lookup"><span data-stu-id="d21d0-115">Add your account</span></span>
<span data-ttu-id="d21d0-116">È necessario configurare Azure PowerShell toowork con risorse di Azure classiche.</span><span class="sxs-lookup"><span data-stu-id="d21d0-116">You must configure Azure PowerShell toowork with classic Azure resources.</span></span> <span data-ttu-id="d21d0-117">Seguire i passaggi di hello sotto le risorse classiche tooconfigure Azure PowerShell toomanage.</span><span class="sxs-lookup"><span data-stu-id="d21d0-117">Follow hello steps below tooconfigure Azure PowerShell toomanage classic resources.</span></span>

1. <span data-ttu-id="d21d0-118">Al prompt di PowerShell hello digitare `Add-AzureAccount` e fare clic su **invio**.</span><span class="sxs-lookup"><span data-stu-id="d21d0-118">At hello PowerShell prompt, type `Add-AzureAccount` and click **Enter**.</span></span> 
2. <span data-ttu-id="d21d0-119">Digitare l'indirizzo di posta elettronica hello associati alla sottoscrizione Azure e fare clic su **continua**.</span><span class="sxs-lookup"><span data-stu-id="d21d0-119">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="d21d0-120">Digitare la password dell'account hello.</span><span class="sxs-lookup"><span data-stu-id="d21d0-120">Type in hello password for your account.</span></span> 
4. <span data-ttu-id="d21d0-121">Fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="d21d0-121">Click **Sign in**.</span></span> 

## <a name="resize-in-hello-same-hardware-cluster"></a><span data-ttu-id="d21d0-122">Ridimensionare in hello stesso cluster hardware</span><span class="sxs-lookup"><span data-stu-id="d21d0-122">Resize in hello same hardware cluster</span></span>
<span data-ttu-id="d21d0-123">tooresize dimensione tooa macchina virtuale disponibile in cluster hardware hello hosting hello macchina virtuale, eseguire hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="d21d0-123">tooresize a VM tooa size available in hello hardware cluster hosting hello VM, perform hello following steps.</span></span>

1. <span data-ttu-id="d21d0-124">Eseguire il comando PowerShell toolist hello dimensioni delle macchine Virtuali disponibili in hello hardware cluster ospita hello cloud servizio che contiene hello VM seguente hello.</span><span class="sxs-lookup"><span data-stu-id="d21d0-124">Run hello following PowerShell command toolist hello VM sizes available in hello hardware cluster hosting hello cloud service which contains hello VM.</span></span>
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. <span data-ttu-id="d21d0-125">Eseguire hello seguenti comandi tooresize hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d21d0-125">Run hello following commands tooresize hello VM.</span></span>
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a><span data-ttu-id="d21d0-126">Ridimensionare in un nuovo cluster hardware</span><span class="sxs-lookup"><span data-stu-id="d21d0-126">Resize on a new hardware cluster</span></span>
<span data-ttu-id="d21d0-127">dimensione tooa macchina virtuale non è disponibile in hello hardware cluster ospita tooresize hello VM, hello servizio cloud e tutte le macchine virtuali nel servizio cloud hello devono essere ricreate.</span><span class="sxs-lookup"><span data-stu-id="d21d0-127">tooresize a VM tooa size not available in hello hardware cluster hosting hello VM, hello cloud service and all VMs in hello cloud service must be recreated.</span></span> <span data-ttu-id="d21d0-128">Ogni servizio cloud è ospitato in un cluster singolo hardware pertanto tutte le macchine virtuali nel servizio cloud hello devono essere una dimensione è supportata in un cluster hardware.</span><span class="sxs-lookup"><span data-stu-id="d21d0-128">Each cloud service is hosted on a single hardware cluster so all VMs in hello cloud service must be a size that is supported on a hardware cluster.</span></span> <span data-ttu-id="d21d0-129">Hello seguente verrà descritta la modalità tooresize una macchina virtuale eliminando e ricreando quindi hello cloud service.</span><span class="sxs-lookup"><span data-stu-id="d21d0-129">hello following steps will describe how tooresize a VM by deleting and then recreating hello cloud service.</span></span>

1. <span data-ttu-id="d21d0-130">Eseguire hello seguente PowerShell comando toolist hello dimensioni delle macchine Virtuali disponibili nell'area di hello.</span><span class="sxs-lookup"><span data-stu-id="d21d0-130">Run hello following PowerShell command toolist hello VM sizes available in hello region.</span></span> 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. <span data-ttu-id="d21d0-131">Prendere nota di tutte le impostazioni di configurazione per ogni macchina virtuale nel servizio cloud hello contenente hello VM toobe ridimensionato.</span><span class="sxs-lookup"><span data-stu-id="d21d0-131">Make note of all configuration settings for each VM in hello cloud service which contains hello VM toobe resized.</span></span> 
3. <span data-ttu-id="d21d0-132">Eliminare tutte le macchine virtuali nel servizio cloud hello selezionando i dischi di hello hello opzione tooretain per ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d21d0-132">Delete all VMs in hello cloud service selecting hello option tooretain hello disks for each VM.</span></span>
4. <span data-ttu-id="d21d0-133">Ricreare hello VM toobe ridimensionato con dimensioni VM hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="d21d0-133">Recreate hello VM toobe resized using hello desired VM size.</span></span>
5. <span data-ttu-id="d21d0-134">Ricreare tutte le altre macchine virtuali che erano presenti nel servizio cloud hello utilizzando una dimensione di macchina virtuale disponibile in cluster hardware hello ora ospita il servizio di cloud hello.</span><span class="sxs-lookup"><span data-stu-id="d21d0-134">Recreate all other VMs which were in hello cloud service using a VM size available in hello hardware cluster now hosting hello cloud service.</span></span>

<span data-ttu-id="d21d0-135">Uno script di esempio per l'eliminazione e la nuova creazione di un servizio cloud mediante una nuova dimensione di VM è disponibile [qui](https://github.com/Azure/azure-vm-scripts).</span><span class="sxs-lookup"><span data-stu-id="d21d0-135">A sample script for deleting and recreating a cloud service using a new VM size can be found [here](https://github.com/Azure/azure-vm-scripts).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d21d0-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d21d0-136">Next steps</span></span>
* <span data-ttu-id="d21d0-137">[Ridimensiona una macchina virtuale creata nel modello di distribuzione di gestione risorse di hello](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d21d0-137">[Resize a VM created in hello Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

