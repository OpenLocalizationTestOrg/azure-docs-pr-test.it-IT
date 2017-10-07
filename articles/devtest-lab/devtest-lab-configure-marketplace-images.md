---
title: impostazioni delle immagini aaaConfigure Azure Marketplace in Azure DevTest Labs | Documenti Microsoft
description: Specificare le immagini di Azure Marketplace che possono essere usate per la creazione di una VM in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: bb4b7f1c0cbe967bee724f7ee20f64f8c4ea58ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a><span data-ttu-id="11a19-103">Configurare le impostazioni dell'immagine di Azure Marketplace in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="11a19-103">Configure Azure Marketplace image settings in Azure DevTest Labs</span></span>
<span data-ttu-id="11a19-104">DevTest Labs supporta la creazione macchine virtuali basate su immagini di Azure Marketplace a seconda della modalità di configurazione di Azure Marketplace toobe di immagini usato nell'ambiente lab.</span><span class="sxs-lookup"><span data-stu-id="11a19-104">DevTest Labs supports creating VMs based on Azure Marketplace images depending on how you have configured Azure Marketplace images toobe used in your lab.</span></span> <span data-ttu-id="11a19-105">In questo articolo illustra come toospecify che, se presente, le immagini di Azure Marketplace possono essere utilizzati durante la creazione di macchine virtuali in un ambiente lab.</span><span class="sxs-lookup"><span data-stu-id="11a19-105">This article shows you how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span> <span data-ttu-id="11a19-106">In questo modo si garantisce che il team dispone solo di immagini di Marketplace toohello di accesso che necessarie.</span><span class="sxs-lookup"><span data-stu-id="11a19-106">This ensures that your team only has access toohello Marketplace images they need.</span></span> 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a><span data-ttu-id="11a19-107">Selezionare le immagini di Azure Marketplace consentite per la creazione di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="11a19-107">Select which Azure Marketplace images are allowed when creating a VM</span></span>
1. <span data-ttu-id="11a19-108">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="11a19-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="11a19-109">Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="11a19-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="11a19-110">Elenco dei laboratori hello selezionare lab desiderato hello.</span><span class="sxs-lookup"><span data-stu-id="11a19-110">From hello list of labs, select hello desired lab.</span></span> 
4. <span data-ttu-id="11a19-111">Nel pannello del lab hello, selezionare **criteri di configurazione e**.</span><span class="sxs-lookup"><span data-stu-id="11a19-111">On hello lab's blade, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="11a19-112">Nel pannello **Configuration and policies** (Configurazione e criteri) di lab in **Virtual Machine Bases** (Basi della macchina virtuale) selezionare **Marketplace images** (Immagini Marketplace).</span><span class="sxs-lookup"><span data-stu-id="11a19-112">On lab's **Configuration and policies** blade under **Virtual Machine Bases**, select **Marketplace images**.</span></span>
6. <span data-ttu-id="11a19-113">Specificare se si desidera che tutti hello Azure Marketplace completo immagini toobe disponibili per l'utilizzo come base di una nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="11a19-113">Specify whether you want all hello qualified Azure Marketplace images toobe available for use as a base of a new VM.</span></span> <span data-ttu-id="11a19-114">Se si seleziona **Sì**, quindi tutte le immagini di Azure Marketplace hello che soddisfano tutte hello seguenti criteri sono consentite in hello lab:</span><span class="sxs-lookup"><span data-stu-id="11a19-114">If you select **Yes**, then all hello Azure Marketplace images that meet all hello following criteria are allowed in hello lab:</span></span>
   
   * <span data-ttu-id="11a19-115">immagine di Hello crea una singola macchina virtuale, **e**</span><span class="sxs-lookup"><span data-stu-id="11a19-115">hello image creates a single VM, **and**</span></span>
   * <span data-ttu-id="11a19-116">immagine di Hello Usa le macchine virtuali di Azure Resource Manager tooprovision, **e**</span><span class="sxs-lookup"><span data-stu-id="11a19-116">hello image uses Azure Resource Manager tooprovision VMs, **and**</span></span>
   * <span data-ttu-id="11a19-117">immagine di Hello non richiede l'acquisto di un piano di licenze aggiuntive</span><span class="sxs-lookup"><span data-stu-id="11a19-117">hello image doesn't require purchasing an extra licensing plan</span></span>
     
    <span data-ttu-id="11a19-118">Se non si desidera alcun toobe immagini consentito, o si desidera toospecify le immagini possono essere utilizzati, selezionare **n**.</span><span class="sxs-lookup"><span data-stu-id="11a19-118">If you want no images toobe allowed, or you want toospecify which images can be used, select **No**.</span></span>
     
     ![Opzione tooallow tutti Marketplace immagini toobe utilizzati come immagini di base per le macchine virtuali](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. <span data-ttu-id="11a19-120">Se si seleziona **n** toohello precedente passaggio hello **immagini consentiti/Seleziona tutti** casella di controllo è abilitato.</span><span class="sxs-lookup"><span data-stu-id="11a19-120">If you select **No** toohello previous step, hello **Allowed images/Select all** checkbox is enabled.</span></span> 
   <span data-ttu-id="11a19-121">È possibile utilizzare questa opzione insieme hello ricerca tooquickly selezionare o deselezionare tutti gli elementi di hello visualizzati nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="11a19-121">You can use this option together with hello search box tooquickly select or deselect all hello items displayed in hello list.</span></span>
   * <span data-ttu-id="11a19-122">Selezionare le immagini di Azure Marketplace hello desiderate tooallow per la creazione di VM singolarmente selezionando la casella di controllo corrispondente per l'immagine.</span><span class="sxs-lookup"><span data-stu-id="11a19-122">Select hello Azure Marketplace images you want tooallow for VM creation individually by checking each image's corresponding checkbox.</span></span>
   * <span data-ttu-id="11a19-123">Senza selezionare alcun elemento dall'elenco hello se non vuoi tooallow qualsiasi toobe immagini di Azure Marketplace usati nel lab hello.</span><span class="sxs-lookup"><span data-stu-id="11a19-123">Select nothing from hello list if you don't want tooallow any Azure Marketplace images toobe used in hello lab.</span></span>
   
    ![È possibile specificare quali immagini di Azure Marketplace possono essere usate come immagini di base per le macchine virtuali](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="11a19-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="11a19-125">Next steps</span></span>
<span data-ttu-id="11a19-126">Dopo aver configurato come immagini di Azure Marketplace sono consentite durante la creazione di una macchina virtuale, hello è troppo[aggiungere un ambiente lab tooyour VM](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="11a19-126">Once you have configured how Azure Marketplace images are allowed when creating a VM, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

