---
title: Creare o modificare automaticamente i lab usando i modelli di Azure Resource Manager con PowerShell | Microsoft Docs
description: Informazioni su come usare i modelli di Azure Resource Manager con PowerShell per creare o modificare automaticamente i lab in un'istanza di DevTest Labs
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: dad9944c-0b20-48be-ba80-8f4aa0950903
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: cea4531175df2cc39790497dc049d27e23ffa0c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-or-modify-labs-automatically-using-azure-resource-manager-templates-and-powershell"></a><span data-ttu-id="5da07-103">Creare o modificare automaticamente i lab usando i modelli di Azure Resource Manager con PowerShell</span><span class="sxs-lookup"><span data-stu-id="5da07-103">Create or modify labs automatically using Azure Resource Manager templates and PowerShell</span></span>

<span data-ttu-id="5da07-104">DevTest Labs offre molti modelli di Azure Resource Manager e script di PowerShell utili per creare rapidamente e automaticamente nuovi lab o modificare quelli esistenti e quindi distribuire tali risorse.</span><span class="sxs-lookup"><span data-stu-id="5da07-104">DevTest Labs provides many Azure Resource Manager templates and PowerShell scripts that can help you quickly and automatically create new labs or modify existing labs and then deploy these resources.</span></span>

<span data-ttu-id="5da07-105">In questo articolo viene descritto il processo di utilizzo di questi modelli e script per automatizzare la creazione, modifica e distribuzione dei propri lab.</span><span class="sxs-lookup"><span data-stu-id="5da07-105">This article helps guide you through the process of using these templates and scripts to automate the creation, modification, and deployment of your labs.</span></span> <span data-ttu-id="5da07-106">In questo articolo viene anche indicato dove è possibile trovare altre informazioni su come usare PowerShell per eseguire alcune attività comuni in DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="5da07-106">This article also shows you where you can find more information about how to use PowerShell to perform some common tasks in DevTest Labs.</span></span>

## <a name="step-1-gather-your-templates-and-scripts"></a><span data-ttu-id="5da07-107">Passaggio 1: raccogliere modelli e script</span><span class="sxs-lookup"><span data-stu-id="5da07-107">Step 1: Gather your templates and scripts</span></span>
<span data-ttu-id="5da07-108">È possibile trovare [modelli di Azure Resource Manager](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) e [script di PowerShell](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) preconfigurati nel nostro [repository Github](https://github.com/Azure/azure-devtestlab) pubblico.</span><span class="sxs-lookup"><span data-stu-id="5da07-108">You can find pre-made [Azure Resource Manager templates](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) and [PowerShell scripts](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) at our public [Github repository](https://github.com/Azure/azure-devtestlab).</span></span> <span data-ttu-id="5da07-109">Usarli così come sono o personalizzarli in base alle proprie esigenze e archiviarli nel proprio [repository Git privato](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="5da07-109">Use them as-is, or customize them for your needs and store them in your own [private Git repo](devtest-lab-add-artifact-repo.md).</span></span> 

## <a name="step-2-modify-your-azure-resource-manager-template"></a><span data-ttu-id="5da07-110">Passaggio 2: modificare il modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5da07-110">Step 2: Modify your Azure Resource Manager template</span></span>
<span data-ttu-id="5da07-111">Se non è mai stato creato un modello, è possibile seguire i passaggi forniti in [Creare il primo modello di Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template).</span><span class="sxs-lookup"><span data-stu-id="5da07-111">You can follow the steps at [Create your first Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template) if you have never created a template before.</span></span>

<span data-ttu-id="5da07-112">Inoltre, l'articolo [Procedure consigliate per la creazione di modelli di Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) offre molti suggerimenti e linee guida per creare modelli di Azure Resource Manager affidabili e semplici da usare.</span><span class="sxs-lookup"><span data-stu-id="5da07-112">In addition, [Best practices for creating Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) offers many guidelines and suggestions to help you create Azure Resource Manager templates that are reliable and easy to use.</span></span> <span data-ttu-id="5da07-113">In genere, si userà una variazione di uno degli approcci o esempi forniti, modificando il modello in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="5da07-113">Typically, you will use a variation of one of the approaches or examples provided and modify your template for your needs.</span></span>

## <a name="step-3-deploy-resources-with-powershell"></a><span data-ttu-id="5da07-114">Passaggio 3: distribuire le risorse con PowerShell</span><span class="sxs-lookup"><span data-stu-id="5da07-114">Step 3: Deploy resources with PowerShell</span></span>
<span data-ttu-id="5da07-115">Dopo aver personalizzato i modelli e gli script, seguire i passaggi necessari per [distribuire le risorse con i modelli di Azure Resource Manager e Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="5da07-115">After you have customized your templates and scripts, follow the steps necessary to [deploy resources with Resource Manager templates and Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span> <span data-ttu-id="5da07-116">L'articolo contiene informazioni generali sull'uso di Azure PowerShell con i modelli di Azure Resource Manager per distribuire le risorse in Azure.</span><span class="sxs-lookup"><span data-stu-id="5da07-116">The article provides general information about using Azure PowerShell with Azure Resource Manager templates to deploy your resources to Azure.</span></span>


## <a name="common-tasks-you-can-perform-in-devtest-labs-using-powershell"></a><span data-ttu-id="5da07-117">Attività comuni che è possibile eseguire nei lab di DevTest Labs tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="5da07-117">Common tasks you can perform in DevTest labs using PowerShell</span></span>
<span data-ttu-id="5da07-118">Esistono molte altre attività comuni che è possibile automatizzare con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5da07-118">There are many other common tasks that you can automate by using PowerShell.</span></span> <span data-ttu-id="5da07-119">Nelle sezioni seguenti della documentazione vengono descritti i passaggi necessari per eseguire queste attività.</span><span class="sxs-lookup"><span data-stu-id="5da07-119">The following sections of the documentation outline the steps required to perform these tasks.</span></span>

* [<span data-ttu-id="5da07-120">Creare un'immagine personalizzata da un file VHD usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="5da07-120">Create a custom image from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
* [<span data-ttu-id="5da07-121">Caricare un file VHD nell'account di archiviazione del lab usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="5da07-121">Upload VHD file to lab's storage account using PowerShell</span></span>](devtest-lab-upload-vhd-using-powershell.md)
* [<span data-ttu-id="5da07-122">Aggiungere un utente esterno a un lab usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="5da07-122">Add an external user to a lab using PowerShell</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell)
* [<span data-ttu-id="5da07-123">Creare un ruolo personalizzato lab tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="5da07-123">Create a lab custom role using PowerShell</span></span>](devtest-lab-grant-user-permissions-to-specific-lab-policies.md#creating-a-lab-custom-role-using-powershell)

### <a name="next-steps"></a><span data-ttu-id="5da07-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5da07-124">Next steps</span></span>
* <span data-ttu-id="5da07-125">Informazioni su come creare un [repository Git privato](devtest-lab-add-artifact-repo.md) in cui verranno archiviati i modelli o script personalizzati.</span><span class="sxs-lookup"><span data-stu-id="5da07-125">Learn how to create a [private Git repository](devtest-lab-add-artifact-repo.md) where you will store your customized templates or scripts.</span></span>
* <span data-ttu-id="5da07-126">Esplorare i [modelli di Azure Resource Manager dalla raccolta di modelli di avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="5da07-126">Explore the [Azure Resource Manager templates from Azure Quickstart template gallery](https://github.com/Azure/azure-quickstart-templates).</span></span>
