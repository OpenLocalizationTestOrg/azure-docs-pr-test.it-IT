---
title: Confronto tra immagini personalizzate e formule nei lab di sviluppo/test | Documentazione Microsoft
description: "Conoscere le differenze tra le immagini personalizzate e le formule come basi per le macchine virtuali consente di decidere quale soluzione è più adatta per il proprio ambiente."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a3cb259a-7d80-40ec-8ee8-45105704d589
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tarcher
ms.openlocfilehash: ff771abc26c08f0adb977c29739d2f5c91924b21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a><span data-ttu-id="4da0e-103">Confronto tra immagini personalizzate e formule nei lab di sviluppo/test</span><span class="sxs-lookup"><span data-stu-id="4da0e-103">Comparing custom images and formulas in DevTest Labs</span></span>
<span data-ttu-id="4da0e-104">Sia le [immagini personalizzate](devtest-lab-create-template.md) che le [formule](devtest-lab-manage-formulas.md) possono essere usate come basi per [creare nuove macchine virtuali](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="4da0e-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm-with-artifacts.md).</span></span> <span data-ttu-id="4da0e-105">La differenza principale tra le immagini personalizzate e le formule è che un'immagine personalizzata è semplicemente un'immagine basata su un disco rigido virtuale, mentre una formula è un'immagine basata su un disco rigido virtuale *con in più* impostazioni preconfigurate, ad esempio dimensioni della macchina virtuale, rete virtuale e subnet, ed elementi.</span><span class="sxs-lookup"><span data-stu-id="4da0e-105">However, the key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span></span> <span data-ttu-id="4da0e-106">Le impostazioni preconfigurate vengono specificate con valori predefiniti che possono essere sostituiti al momento della creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4da0e-106">These preconfigured settings are set up with default values that can be overridden at the time of VM creation.</span></span> <span data-ttu-id="4da0e-107">Questo articolo illustra alcuni dei vantaggi e degli svantaggi relativi all'uso delle immagini personalizzate e delle formule.</span><span class="sxs-lookup"><span data-stu-id="4da0e-107">This article explains some of the advantages (pros) and disadvantages (cons) to using custom images versus using formulas.</span></span>

## <a name="custom-image-pros-and-cons"></a><span data-ttu-id="4da0e-108">Vantaggi e svantaggi delle immagini personalizzate</span><span class="sxs-lookup"><span data-stu-id="4da0e-108">Custom image pros and cons</span></span>
<span data-ttu-id="4da0e-109">Le immagini personalizzate offrono un modo statico e non modificabile per creare macchine virtuali da un ambiente di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="4da0e-109">Custom images provide a static, immutable way to create VMs from a desired environment.</span></span> 

<span data-ttu-id="4da0e-110">**Vantaggi**</span><span class="sxs-lookup"><span data-stu-id="4da0e-110">**Pros**</span></span>

* <span data-ttu-id="4da0e-111">Il provisioning della macchina virtuale da un'immagine personalizzata è veloce poiché non vengono apportate modifiche dopo che la macchina virtuale viene attivata dall'immagine.</span><span class="sxs-lookup"><span data-stu-id="4da0e-111">VM provisioning from a custom image is fast as nothing changes after the VM is spun up from the image.</span></span> <span data-ttu-id="4da0e-112">In altre parole, non vi sono impostazioni da applicare poiché l'immagine personalizzata è semplicemente un'immagine senza impostazioni.</span><span class="sxs-lookup"><span data-stu-id="4da0e-112">In other words, there are no settings to apply as the custom image is just an image without settings.</span></span> 
* <span data-ttu-id="4da0e-113">Le macchine virtuali create da un'unica immagine personalizzata sono identiche.</span><span class="sxs-lookup"><span data-stu-id="4da0e-113">VMs created from a single custom image are identical.</span></span>

<span data-ttu-id="4da0e-114">**Svantaggi**</span><span class="sxs-lookup"><span data-stu-id="4da0e-114">**Cons**</span></span>

* <span data-ttu-id="4da0e-115">Se è necessario aggiornare alcuni aspetti dell'immagine personalizzata, si dovrà ricreare l'immagine.</span><span class="sxs-lookup"><span data-stu-id="4da0e-115">If you need to update some aspect of the custom image, the image must be recreated.</span></span>  

## <a name="formula-pros-and-cons"></a><span data-ttu-id="4da0e-116">Vantaggi e svantaggi delle formule</span><span class="sxs-lookup"><span data-stu-id="4da0e-116">Formula pros and cons</span></span>
<span data-ttu-id="4da0e-117">Le formule offrono un modo dinamico per creare macchine virtuali in base a una configurazione o alle impostazioni desiderate.</span><span class="sxs-lookup"><span data-stu-id="4da0e-117">Formulas provide a dynamic way to create VMs from the desired configuration/settings.</span></span>

<span data-ttu-id="4da0e-118">**Vantaggi**</span><span class="sxs-lookup"><span data-stu-id="4da0e-118">**Pros**</span></span>

* <span data-ttu-id="4da0e-119">È possibile acquisire in tempo reale le modifiche apportate nell'ambiente in tempo reale usando gli elementi.</span><span class="sxs-lookup"><span data-stu-id="4da0e-119">Changes in the environment can be captured on the fly via artifacts.</span></span> <span data-ttu-id="4da0e-120">Ad esempio, per installare una macchina virtuale con i bit più recenti della pipeline di rilascio o integrare il codice più recente dal repository, è possibile specificare semplicemente un elemento che consenta di distribuire i bit più recenti o integri il codice più recente nella formula insieme a un'immagine di base di destinazione.</span><span class="sxs-lookup"><span data-stu-id="4da0e-120">For example, if you want a VM installed with the latest bits from your release pipeline or enlist the latest code from your repository, you can simply specify an artifact that deploys the latest bits or enlists the latest code in the formula together with a target base image.</span></span> <span data-ttu-id="4da0e-121">Ogni volta che la formula viene usata per creare macchine virtuali, il codice o i bit più recenti vengono integrati o distribuiti alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4da0e-121">Whenever this formula is used to create VMs, the latest bits/code are deployed/enlisted to the VM.</span></span> 
* <span data-ttu-id="4da0e-122">A differenza delle immagini personalizzate, le formule possono definire impostazioni predefinite come le dimensioni delle macchine virtuali e le impostazioni della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4da0e-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span></span> 
* <span data-ttu-id="4da0e-123">Le impostazioni salvate in una formula vengono visualizzate come valori predefiniti, ma possono essere modificate quando viene creata la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4da0e-123">The settings saved in a formula are shown as default values, but can be modified when the VM is created.</span></span> 

<span data-ttu-id="4da0e-124">**Svantaggi**</span><span class="sxs-lookup"><span data-stu-id="4da0e-124">**Cons**</span></span>

* <span data-ttu-id="4da0e-125">La creazione di una macchina virtuale da una formula può richiedere più tempo rispetto alla creazione da un'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="4da0e-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="4da0e-126">Post di blog correlati</span><span class="sxs-lookup"><span data-stu-id="4da0e-126">Related blog posts</span></span>
* [<span data-ttu-id="4da0e-127">Custom images or formulas? (Immagini personalizzate o formule?)</span><span class="sxs-lookup"><span data-stu-id="4da0e-127">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="4da0e-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4da0e-128">Next steps</span></span>
- [<span data-ttu-id="4da0e-129">Domande frequenti su DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4da0e-129">DevTest Labs FAQ</span></span>](devtest-lab-faq.md)