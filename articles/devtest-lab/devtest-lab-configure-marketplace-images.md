---
title: Configurare le impostazioni dell'immagine di Azure Marketplace in Azure DevTest Labs | Documentazione Microsoft
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
ms.openlocfilehash: 5f888c9d92a9164cc7d3d1aed66c29a724b365d7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a><span data-ttu-id="df4b3-103">Configurare le impostazioni dell'immagine di Azure Marketplace in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="df4b3-103">Configure Azure Marketplace image settings in Azure DevTest Labs</span></span>
<span data-ttu-id="df4b3-104">Lab di sviluppo/test supporta la creazione di VM basate su immagini di Azure Marketplace in base alla configurazione delle immagini di Azure Marketplace da usare nel lab.</span><span class="sxs-lookup"><span data-stu-id="df4b3-104">DevTest Labs supports creating VMs based on Azure Marketplace images depending on how you have configured Azure Marketplace images to be used in your lab.</span></span> <span data-ttu-id="df4b3-105">Questo articolo illustra come specificare eventuali immagini di Azure Marketplace da usare durante la creazione di VM in un lab.</span><span class="sxs-lookup"><span data-stu-id="df4b3-105">This article shows you how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span> <span data-ttu-id="df4b3-106">Ciò garantisce che il team abbia accesso solo alle immagini del Marketplace necessarie.</span><span class="sxs-lookup"><span data-stu-id="df4b3-106">This ensures that your team only has access to the Marketplace images they need.</span></span> 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a><span data-ttu-id="df4b3-107">Selezionare le immagini di Azure Marketplace consentite per la creazione di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="df4b3-107">Select which Azure Marketplace images are allowed when creating a VM</span></span>
1. <span data-ttu-id="df4b3-108">Accedere al [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="df4b3-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="df4b3-109">Selezionare **Altri servizi** e quindi **DevTest Labs** dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="df4b3-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="df4b3-110">Nell'elenco dei lab selezionare il lab desiderato.</span><span class="sxs-lookup"><span data-stu-id="df4b3-110">From the list of labs, select the desired lab.</span></span> 
4. <span data-ttu-id="df4b3-111">Nel pannello del lab selezionare **Configurazione e criteri**.</span><span class="sxs-lookup"><span data-stu-id="df4b3-111">On the lab's blade, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="df4b3-112">Nel pannello **Configuration and policies** (Configurazione e criteri) di lab in **Virtual Machine Bases** (Basi della macchina virtuale) selezionare **Marketplace images** (Immagini Marketplace).</span><span class="sxs-lookup"><span data-stu-id="df4b3-112">On lab's **Configuration and policies** blade under **Virtual Machine Bases**, select **Marketplace images**.</span></span>
6. <span data-ttu-id="df4b3-113">Specificare se si desidera che tutte le immagini di Azure Marketplace qualificate siano disponibili per essere usate come base di una nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="df4b3-113">Specify whether you want all the qualified Azure Marketplace images to be available for use as a base of a new VM.</span></span> <span data-ttu-id="df4b3-114">Se si seleziona **Sì**, tutte le immagini di Azure Marketplace che soddisfano tutti i criteri seguenti saranno disponibili nel lab:</span><span class="sxs-lookup"><span data-stu-id="df4b3-114">If you select **Yes**, then all the Azure Marketplace images that meet all the following criteria are allowed in the lab:</span></span>
   
   * <span data-ttu-id="df4b3-115">L'immagine crea una singola macchina virtuale **e**</span><span class="sxs-lookup"><span data-stu-id="df4b3-115">The image creates a single VM, **and**</span></span>
   * <span data-ttu-id="df4b3-116">L'immagine usa Azure Resource Manager per il provisioning delle macchine virtuali **e**</span><span class="sxs-lookup"><span data-stu-id="df4b3-116">The image uses Azure Resource Manager to provision VMs, **and**</span></span>
   * <span data-ttu-id="df4b3-117">L'immagine non richiede l'acquisto di un piano di licenze aggiuntivo</span><span class="sxs-lookup"><span data-stu-id="df4b3-117">The image doesn't require purchasing an extra licensing plan</span></span>
     
    <span data-ttu-id="df4b3-118">Se non si desidera autorizzare alcuna immagine o si desidera specificare le immagini che possono essere usate, selezionare **No**.</span><span class="sxs-lookup"><span data-stu-id="df4b3-118">If you want no images to be allowed, or you want to specify which images can be used, select **No**.</span></span>
     
     ![Opzione per consentire l'uso di tutte le immagini di Marketplace come immagini di base per le macchine virtuali](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. <span data-ttu-id="df4b3-120">Se si seleziona **No** nel passaggio precedente, la casella di controllo **Immagini consentite/Seleziona tutto** viene abilitata.</span><span class="sxs-lookup"><span data-stu-id="df4b3-120">If you select **No** to the previous step, the **Allowed images/Select all** checkbox is enabled.</span></span> 
   <span data-ttu-id="df4b3-121">È possibile usare questa opzione con la casella di ricerca per selezionare o deselezionare rapidamente tutti gli elementi visualizzati nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="df4b3-121">You can use this option together with the search box to quickly select or deselect all the items displayed in the list.</span></span>
   * <span data-ttu-id="df4b3-122">Selezionare le singole immagini di Azure Marketplace che si desidera rendere disponibili per la creazione di macchine virtuali selezionando la casella di controllo corrispondente all'immagine.</span><span class="sxs-lookup"><span data-stu-id="df4b3-122">Select the Azure Marketplace images you want to allow for VM creation individually by checking each image's corresponding checkbox.</span></span>
   * <span data-ttu-id="df4b3-123">Non selezionare alcuna voce nell'elenco se non si desidera rendere disponibile alcuna immagine di Azure Marketplace per l'uso nel lab.</span><span class="sxs-lookup"><span data-stu-id="df4b3-123">Select nothing from the list if you don't want to allow any Azure Marketplace images to be used in the lab.</span></span>
   
    ![È possibile specificare quali immagini di Azure Marketplace possono essere usate come immagini di base per le macchine virtuali](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="df4b3-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="df4b3-125">Next steps</span></span>
<span data-ttu-id="df4b3-126">Dopo avere configurato le immagini di Azure Marketplace consentite per la creazione di una macchina virtuale, il passaggio successivo consiste nell'[aggiungere una macchina virtuale nel lab](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="df4b3-126">Once you have configured how Azure Marketplace images are allowed when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

