---
title: Diagnosticare gli errori di elemento in una VM di Azure DevTest Labs | Microsoft Docs
description: Informazioni su come risolvere i problemi relativi a errori degli elementi in DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 115e0086-3293-4adf-8738-9f639f31f918
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: tarcher
ms.openlocfilehash: e4f2946d0ba0756f36622aded0e8594acabb9527
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="diagnose-artifact-failures-in-the-lab"></a><span data-ttu-id="d2761-103">Diagnosticare errori di elementi nel lab</span><span class="sxs-lookup"><span data-stu-id="d2761-103">Diagnose artifact failures in the lab</span></span> 
<span data-ttu-id="d2761-104">Dopo aver creato un elemento, è possibile verificare se l'esito è positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="d2761-104">After you have created an artifact, you can check to see if it succeeded or failed.</span></span> <span data-ttu-id="d2761-105">I log degli elementi in DevTest Labs forniscono informazioni che è possibile usare per diagnosticare un errore di elemento.</span><span class="sxs-lookup"><span data-stu-id="d2761-105">Artifact logs in DevTest Labs provide information you can use to diagnose an artifact failure.</span></span> <span data-ttu-id="d2761-106">Esistono due modi diversi per visualizzare le informazioni sul log degli elementi per una VM Windows.</span><span class="sxs-lookup"><span data-stu-id="d2761-106">There are a couple different ways you can view the artifact log information for a Windows VM.</span></span>

> [!NOTE]
> <span data-ttu-id="d2761-107">Per garantire che gli errori vengano identificati e descritti correttamente, è importante che l'elemento sia strutturato in modo corretto.</span><span class="sxs-lookup"><span data-stu-id="d2761-107">To ensure that failures are correctly identified and explained, it is important that the artifact is properly structured.</span></span> <span data-ttu-id="d2761-108">Per informazioni su come costruire correttamente un elemento, vedere [Creare elementi personalizzati](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="d2761-108">For information about how to correctly construct an artifact, see [Create custom artifacts](devtest-lab-artifact-author.md).</span></span> <span data-ttu-id="d2761-109">Per vedere un esempio di elemento strutturato correttamente, consultare questo elemento [Testare i tipi di parametri](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes).</span><span class="sxs-lookup"><span data-stu-id="d2761-109">And to see an example of a properly structured artifact, check out this [Test Parameter Types](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artifact.</span></span>

## <a name="troubleshoot-artifact-failures-using-the-azure-portal"></a><span data-ttu-id="d2761-110">Risolvere i problemi relativi agli errori di elemento mediante il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d2761-110">Troubleshoot artifact failures using the Azure portal</span></span>
<span data-ttu-id="d2761-111">Per usare il portale di Azure al fine di diagnosticare gli errori durante la creazione dell'elemento, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="d2761-111">To use the Azure portal to diagnose failures during artifact creation, follow these steps:</span></span>

1. <span data-ttu-id="d2761-112">Nell'elenco delle risorse selezionare il proprio lab.</span><span class="sxs-lookup"><span data-stu-id="d2761-112">From the list of resources, select your lab.</span></span>

2. <span data-ttu-id="d2761-113">Scegliere la VM Windows che include l'elemento da analizzare.</span><span class="sxs-lookup"><span data-stu-id="d2761-113">Choose the Windows VM that includes the artifact you want to investigate.</span></span>

3. <span data-ttu-id="d2761-114">Nel riquadro sinistro sotto **GENERALE** scegliere **Elementi**.</span><span class="sxs-lookup"><span data-stu-id="d2761-114">In the left panel under **GENERAL**, choose **Artifacts**.</span></span> <span data-ttu-id="d2761-115">Viene visualizzato un elenco di elementi associati a tale VM che indica il nome dell'elemento e il suo stato.</span><span class="sxs-lookup"><span data-stu-id="d2761-115">A list of artifacts associated with that VM appears, indicating the name of the artifact and its status.</span></span>

   ![Esempio di archivio git dell’elemento](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. <span data-ttu-id="d2761-117">Scegliere un elemento che mostra lo stato **Failed**.</span><span class="sxs-lookup"><span data-stu-id="d2761-117">Choose an artifact that shows a status of **Failed**.</span></span> <span data-ttu-id="d2761-118">L'elemento viene aperto e viene visualizzato un messaggio di estensione che include i dettagli sull'errore dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="d2761-118">The artifact opens and shows an extension message that includes details about the failure of the artifact.</span></span>

   ![Esempio di archivio git dell’elemento](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-the-vm"></a><span data-ttu-id="d2761-120">Risoluzione dei problemi di elemento dall'interno della VM</span><span class="sxs-lookup"><span data-stu-id="d2761-120">Troubleshoot artifact failures from within the VM</span></span>
<span data-ttu-id="d2761-121">Per visualizzare i log degli elementi all'interno della macchina virtuale, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="d2761-121">To view the artifact logs from within the virtual machine, follow these steps:</span></span>

1. <span data-ttu-id="d2761-122">Accedere alla VM che contiene l'elemento da analizzare.</span><span class="sxs-lookup"><span data-stu-id="d2761-122">Log in to the VM that contains the artifact you want to diagnose.</span></span>

2. <span data-ttu-id="d2761-123">Passare a C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status dove "1.9" è il numero di versione CSE.</span><span class="sxs-lookup"><span data-stu-id="d2761-123">Navigate to C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status where "1.9 is the CSE version number.</span></span>

   ![Esempio di archivio git dell’elemento](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. <span data-ttu-id="d2761-125">Aprire il file **status** per visualizzare le informazioni che consentono di diagnosticare gli errori di elemento per la VM.</span><span class="sxs-lookup"><span data-stu-id="d2761-125">Open the **status** file to view information that helps diagnose artifact failures for that VM.</span></span>




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="d2761-126">Post di blog correlati</span><span class="sxs-lookup"><span data-stu-id="d2761-126">Related blog posts</span></span>
* [<span data-ttu-id="d2761-127">Aggiungere una VM a un dominio di AD esistente usando un modello di Resource Manager in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="d2761-127">Join a VM to existing AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="d2761-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d2761-128">Next steps</span></span>
* <span data-ttu-id="d2761-129">Informazioni su come [Aggiungere un archivio Git a un lab](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="d2761-129">Learn how to [add a Git repository to a lab](devtest-lab-add-artifact-repo.md).</span></span>

