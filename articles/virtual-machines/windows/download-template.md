---
title: modello di hello aaaDownload per una macchina virtuale di Azure | Documenti Microsoft
description: Scaricare hello templatefor toohelp una macchina virtuale con l'automazione delle distribuzioni nel modello di distribuzione di gestione risorse di hello
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
ms.openlocfilehash: 86fd05f67409019b5e5c9023881745047860eee1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-template-for-a-vm"></a><span data-ttu-id="3df7a-103">Scaricare il modello di hello per una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="3df7a-103">Download hello template for a VM</span></span>
<span data-ttu-id="3df7a-104">Quando si crea una macchina virtuale in Azure mediante portale hello o PowerShell, gestione delle risorse di modello viene creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3df7a-104">When you create a VM in Azure using hello portal or PowerShell, a Resource Manager template is automatically created for you.</span></span> <span data-ttu-id="3df7a-105">È possibile utilizzare questo duplicato di tooquickly una distribuzione modello.</span><span class="sxs-lookup"><span data-stu-id="3df7a-105">You can use this template tooquickly duplicate a deployment.</span></span> <span data-ttu-id="3df7a-106">modello di Hello contiene informazioni su tutte le risorse di hello in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="3df7a-106">hello template contains information about all of hello resources in a resource group.</span></span> <span data-ttu-id="3df7a-107">Per una macchina virtuale, ciò significa modello hello contiene tutto ciò che viene creato per supportare hello macchina virtuale in tale gruppo di risorse, tra cui le risorse di rete hello.</span><span class="sxs-lookup"><span data-stu-id="3df7a-107">For a virtual machine, this means hello template contains everything that is created in support of hello VM in that resource group, including hello networking resources.</span></span>

## <a name="download-hello-template-using-hello-portal"></a><span data-ttu-id="3df7a-108">Scaricare il modello di hello tramite il portale di hello</span><span class="sxs-lookup"><span data-stu-id="3df7a-108">Download hello template using hello portal</span></span>
1. <span data-ttu-id="3df7a-109">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3df7a-109">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3df7a-110">Un hello hub dal menu **macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="3df7a-110">One hello hub menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="3df7a-111">Selezionare macchina virtuale hello hello elenco.</span><span class="sxs-lookup"><span data-stu-id="3df7a-111">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="3df7a-112">Selezionare **Script di automazione**.</span><span class="sxs-lookup"><span data-stu-id="3df7a-112">Select **Automation script**.</span></span>
5. <span data-ttu-id="3df7a-113">Selezionare **scaricare** e salvare computer tooyour di file con estensione zip hello locale.</span><span class="sxs-lookup"><span data-stu-id="3df7a-113">Select **Download** and save hello .zip file tooyour local computer.</span></span>
6. <span data-ttu-id="3df7a-114">Aprire il file con estensione zip hello ed estrarre cartella tooa hello.</span><span class="sxs-lookup"><span data-stu-id="3df7a-114">Open hello .zip file and extract hello files tooa folder.</span></span> <span data-ttu-id="3df7a-115">file con estensione zip Hello conterrà:</span><span class="sxs-lookup"><span data-stu-id="3df7a-115">hello .zip file will contain:</span></span>
   
   * <span data-ttu-id="3df7a-116">deploy.ps1</span><span class="sxs-lookup"><span data-stu-id="3df7a-116">deploy.ps1</span></span>
   * <span data-ttu-id="3df7a-117">deploy.sh</span><span class="sxs-lookup"><span data-stu-id="3df7a-117">deploy.sh</span></span> 
   * <span data-ttu-id="3df7a-118">deployer.rb</span><span class="sxs-lookup"><span data-stu-id="3df7a-118">deployer.rb</span></span>
   * <span data-ttu-id="3df7a-119">DeploymentHelper.cs</span><span class="sxs-lookup"><span data-stu-id="3df7a-119">DeploymentHelper.cs</span></span>
   * <span data-ttu-id="3df7a-120">parameters.json</span><span class="sxs-lookup"><span data-stu-id="3df7a-120">parameters.json</span></span>
   * <span data-ttu-id="3df7a-121">template.json</span><span class="sxs-lookup"><span data-stu-id="3df7a-121">template.json</span></span>

<span data-ttu-id="3df7a-122">file template.json Hello è il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="3df7a-122">hello template.json file is hello template.</span></span>

## <a name="download-hello-template-using-powershell"></a><span data-ttu-id="3df7a-123">Scaricare il modello di hello tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="3df7a-123">Download hello template using PowerShell</span></span>
<span data-ttu-id="3df7a-124">È inoltre possibile scaricare i file di modello con estensione JSON hello utilizzando hello [esportazione AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3df7a-124">You can also download hello .json template file using hello [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span></span> <span data-ttu-id="3df7a-125">È possibile utilizzare hello `-path` parametro tooprovide hello filename e il percorso di file con estensione JSON hello.</span><span class="sxs-lookup"><span data-stu-id="3df7a-125">You can use hello `-path` parameter tooprovide hello filename and path for hello .json file.</span></span> <span data-ttu-id="3df7a-126">Questo esempio viene illustrato come modello hello toodownload per il gruppo di risorse hello denominati **myResourceGroup** toohello **C:\users\public\downloads** cartella nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="3df7a-126">This example shows how toodownload hello template for hello resource group named **myResourceGroup** toohello **C:\users\public\downloads** folder on your local computer.</span></span>

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a><span data-ttu-id="3df7a-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3df7a-127">Next steps</span></span>
<span data-ttu-id="3df7a-128">toolearn più sulla distribuzione di risorse utilizzando i modelli, vedere [procedura dettagliata di modello di gestione risorse](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="3df7a-128">toolearn more about deploying resources using templates, see [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

