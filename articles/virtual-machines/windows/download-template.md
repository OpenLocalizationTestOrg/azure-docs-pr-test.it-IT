---
title: Scaricare il modello per una macchina virtuale di Azure | Microsoft Docs
description: Scaricare il modello per una macchina virtuale per facilitare l'automazione delle distribuzioni nel modello di distribuzione di Resource Manager
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 51ef4f51-0942-4249-afea-4a3f87ce1ff8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 9e4c0c3cf0e233447369a24b1d5fe27495abd1cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="download-the-template-for-a-vm"></a><span data-ttu-id="bb621-103">Scaricare il modello per una VM</span><span class="sxs-lookup"><span data-stu-id="bb621-103">Download the template for a VM</span></span>
<span data-ttu-id="bb621-104">Quando si crea una macchina virtuale in Azure con il portale o con PowerShell, viene creato automaticamente un modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bb621-104">When you create a VM in Azure using the portal or PowerShell, a Resource Manager template is automatically created for you.</span></span> <span data-ttu-id="bb621-105">È possibile usare questo modello per duplicare rapidamente una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="bb621-105">You can use this template to quickly duplicate a deployment.</span></span> <span data-ttu-id="bb621-106">Il modello contiene informazioni su tutte le risorse in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="bb621-106">The template contains information about all of the resources in a resource group.</span></span> <span data-ttu-id="bb621-107">Per una macchina virtuale, questo significa che il modello contiene tutto ciò che viene creato in supporto della macchina virtuale all'interno del gruppo di risorse, comprese le risorse di rete.</span><span class="sxs-lookup"><span data-stu-id="bb621-107">For a virtual machine, this means the template contains everything that is created in support of the VM in that resource group, including the networking resources.</span></span>

## <a name="download-the-template-using-the-portal"></a><span data-ttu-id="bb621-108">Scaricare il modello usando il portale</span><span class="sxs-lookup"><span data-stu-id="bb621-108">Download the template using the portal</span></span>
1. <span data-ttu-id="bb621-109">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bb621-109">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="bb621-110">Selezionare **Macchine virtuali** nel menu dell'hub.</span><span class="sxs-lookup"><span data-stu-id="bb621-110">One the hub menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="bb621-111">Selezionare la macchina virtuale dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="bb621-111">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="bb621-112">Selezionare **Script di automazione**.</span><span class="sxs-lookup"><span data-stu-id="bb621-112">Select **Automation script**.</span></span>
5. <span data-ttu-id="bb621-113">Selezionare **Scarica** e salvare il file .zip nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="bb621-113">Select **Download** and save the .zip file to your local computer.</span></span>
6. <span data-ttu-id="bb621-114">Aprire il file .zip ed estrarne i file in una cartella.</span><span class="sxs-lookup"><span data-stu-id="bb621-114">Open the .zip file and extract the files to a folder.</span></span> <span data-ttu-id="bb621-115">Il file .zip contiene:</span><span class="sxs-lookup"><span data-stu-id="bb621-115">The .zip file will contain:</span></span>
   
   * <span data-ttu-id="bb621-116">deploy.ps1</span><span class="sxs-lookup"><span data-stu-id="bb621-116">deploy.ps1</span></span>
   * <span data-ttu-id="bb621-117">deploy.sh</span><span class="sxs-lookup"><span data-stu-id="bb621-117">deploy.sh</span></span> 
   * <span data-ttu-id="bb621-118">deployer.rb</span><span class="sxs-lookup"><span data-stu-id="bb621-118">deployer.rb</span></span>
   * <span data-ttu-id="bb621-119">DeploymentHelper.cs</span><span class="sxs-lookup"><span data-stu-id="bb621-119">DeploymentHelper.cs</span></span>
   * <span data-ttu-id="bb621-120">parameters.json</span><span class="sxs-lookup"><span data-stu-id="bb621-120">parameters.json</span></span>
   * <span data-ttu-id="bb621-121">template.json</span><span class="sxs-lookup"><span data-stu-id="bb621-121">template.json</span></span>

<span data-ttu-id="bb621-122">Il file template.json è il modello.</span><span class="sxs-lookup"><span data-stu-id="bb621-122">The template.json file is the template.</span></span>

## <a name="download-the-template-using-powershell"></a><span data-ttu-id="bb621-123">Scaricare il modello con PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb621-123">Download the template using PowerShell</span></span>
<span data-ttu-id="bb621-124">È anche possibile scaricare il file di modello .json usando il cmdlet [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx).</span><span class="sxs-lookup"><span data-stu-id="bb621-124">You can also download the .json template file using the [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span></span> <span data-ttu-id="bb621-125">È possibile usare il parametro `-path` per fornire il nome file e il percorso per il file .json.</span><span class="sxs-lookup"><span data-stu-id="bb621-125">You can use the `-path` parameter to provide the filename and path for the .json file.</span></span> <span data-ttu-id="bb621-126">In questo esempio viene illustrato come scaricare il modello per il gruppo di risorse denominato **myResourceGroup** nella cartella **C:\users\public\downloads** del computer locale.</span><span class="sxs-lookup"><span data-stu-id="bb621-126">This example shows how to download the template for the resource group named **myResourceGroup** to the **C:\users\public\downloads** folder on your local computer.</span></span>

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a><span data-ttu-id="bb621-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bb621-127">Next steps</span></span>
<span data-ttu-id="bb621-128">Per altre informazioni sulla distribuzione di risorse usando i modelli, vedere [Procedura dettagliata del modello di Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="bb621-128">To learn more about deploying resources using templates, see [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

