---
title: errori di artefatto aaaDiagnose nella macchina virtuale di Azure DevTest Labs | Documenti Microsoft
description: Informazioni su come gli errori di artefatto tootroubleshoot DevTest Labs
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
ms.openlocfilehash: 40b3cea72cf071cc5d9a6d002d309d923c3d3084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-artifact-failures-in-hello-lab"></a><span data-ttu-id="465b4-103">Diagnosticare gli errori di artefatto in lab hello</span><span class="sxs-lookup"><span data-stu-id="465b4-103">Diagnose artifact failures in hello lab</span></span> 
<span data-ttu-id="465b4-104">Dopo aver creato un elemento, è possibile controllare toosee se ha avuto esito positivo o non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="465b4-104">After you have created an artifact, you can check toosee if it succeeded or failed.</span></span> <span data-ttu-id="465b4-105">Registri di artefatto in DevTest Labs forniscono informazioni che è possibile utilizzare toodiagnose un errore di elemento.</span><span class="sxs-lookup"><span data-stu-id="465b4-105">Artifact logs in DevTest Labs provide information you can use toodiagnose an artifact failure.</span></span> <span data-ttu-id="465b4-106">Esistono due modi diversi, è possibile visualizzare le informazioni sul log per una macchina virtuale Windows hello artefatto.</span><span class="sxs-lookup"><span data-stu-id="465b4-106">There are a couple different ways you can view hello artifact log information for a Windows VM.</span></span>

> [!NOTE]
> <span data-ttu-id="465b4-107">tooensure che gli errori correttamente vengono identificati e descritto, è importante elemento hello è strutturato in modo corretto.</span><span class="sxs-lookup"><span data-stu-id="465b4-107">tooensure that failures are correctly identified and explained, it is important that hello artifact is properly structured.</span></span> <span data-ttu-id="465b4-108">Per informazioni su come toocorrectly costruire un elemento, vedere [creare gli elementi personalizzati](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="465b4-108">For information about how toocorrectly construct an artifact, see [Create custom artifacts](devtest-lab-artifact-author.md).</span></span> <span data-ttu-id="465b4-109">E toosee un esempio di un elemento strutturato correttamente, consultare questa [tipi di parametri di Test](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artefatto.</span><span class="sxs-lookup"><span data-stu-id="465b4-109">And toosee an example of a properly structured artifact, check out this [Test Parameter Types](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artifact.</span></span>

## <a name="troubleshoot-artifact-failures-using-hello-azure-portal"></a><span data-ttu-id="465b4-110">Risoluzione dei problemi di elemento utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="465b4-110">Troubleshoot artifact failures using hello Azure portal</span></span>
<span data-ttu-id="465b4-111">errori di toodiagnose portale Azure hello toouse durante la creazione dell'elemento, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="465b4-111">toouse hello Azure portal toodiagnose failures during artifact creation, follow these steps:</span></span>

1. <span data-ttu-id="465b4-112">Dall'elenco di hello delle risorse, selezionare l'ambiente lab.</span><span class="sxs-lookup"><span data-stu-id="465b4-112">From hello list of resources, select your lab.</span></span>

2. <span data-ttu-id="465b4-113">Scegliere una macchina virtuale di Windows che include l'elemento hello desiderato tooinvestigate hello.</span><span class="sxs-lookup"><span data-stu-id="465b4-113">Choose hello Windows VM that includes hello artifact you want tooinvestigate.</span></span>

3. <span data-ttu-id="465b4-114">Nel riquadro sinistro di hello in **generale**, scegliere **elementi**.</span><span class="sxs-lookup"><span data-stu-id="465b4-114">In hello left panel under **GENERAL**, choose **Artifacts**.</span></span> <span data-ttu-id="465b4-115">Viene visualizzato un elenco di elementi associati a tale macchina virtuale, che indicano il nome di hello dell'artefatto hello e il relativo stato.</span><span class="sxs-lookup"><span data-stu-id="465b4-115">A list of artifacts associated with that VM appears, indicating hello name of hello artifact and its status.</span></span>

   ![Esempio di archivio git dell’elemento](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. <span data-ttu-id="465b4-117">Scegliere un elemento che mostra lo stato **Failed**.</span><span class="sxs-lookup"><span data-stu-id="465b4-117">Choose an artifact that shows a status of **Failed**.</span></span> <span data-ttu-id="465b4-118">elemento Hello viene aperto e verrà visualizzato un messaggio di estensione che include i dettagli sull'errore hello dell'artefatto hello.</span><span class="sxs-lookup"><span data-stu-id="465b4-118">hello artifact opens and shows an extension message that includes details about hello failure of hello artifact.</span></span>

   ![Esempio di archivio git dell’elemento](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-hello-vm"></a><span data-ttu-id="465b4-120">Risolvere gli errori di artefatto di hello VM</span><span class="sxs-lookup"><span data-stu-id="465b4-120">Troubleshoot artifact failures from within hello VM</span></span>
<span data-ttu-id="465b4-121">i registri di artefatto hello tooview dalla macchina virtuale hello, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="465b4-121">tooview hello artifact logs from within hello virtual machine, follow these steps:</span></span>

1. <span data-ttu-id="465b4-122">Accedi toohello macchina virtuale che contiene l'elemento hello desiderato toodiagnose.</span><span class="sxs-lookup"><span data-stu-id="465b4-122">Log in toohello VM that contains hello artifact you want toodiagnose.</span></span>

2. <span data-ttu-id="465b4-123">Passare tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status dove "1.9 è numero di versione di hello estensione lato client.</span><span class="sxs-lookup"><span data-stu-id="465b4-123">Navigate tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status where "1.9 is hello CSE version number.</span></span>

   ![Esempio di archivio git dell’elemento](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. <span data-ttu-id="465b4-125">Aprire hello **stato** file tooview le informazioni che consente di diagnosticare gli errori di elemento per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="465b4-125">Open hello **status** file tooview information that helps diagnose artifact failures for that VM.</span></span>




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="465b4-126">Post di blog correlati</span><span class="sxs-lookup"><span data-stu-id="465b4-126">Related blog posts</span></span>
* [<span data-ttu-id="465b4-127">Aggiungere un dominio di Active Directory utilizzando un modello di gestione delle risorse in Azure DevTest Labs di tooexisting VM</span><span class="sxs-lookup"><span data-stu-id="465b4-127">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="465b4-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="465b4-128">Next steps</span></span>
* <span data-ttu-id="465b4-129">Informazioni su come troppo[aggiungere un ambiente lab tooa di repository Git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="465b4-129">Learn how too[add a Git repository tooa lab](devtest-lab-add-artifact-repo.md).</span></span>

