---
title: aaaComparing immagini personalizzate e le formule di DevTest Labs | Documenti Microsoft
description: "Informazioni sulle differenze hello immagini personalizzate e le formule come macchina virtuale si basa in modo è possibile scegliere quella più appropriata per l'ambiente."
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
ms.openlocfilehash: 3c1d88dfe0ff94b8e825bb7a0b4aca3341c9330d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a><span data-ttu-id="583e9-103">Confronto tra immagini personalizzate e formule nei lab di sviluppo/test</span><span class="sxs-lookup"><span data-stu-id="583e9-103">Comparing custom images and formulas in DevTest Labs</span></span>
<span data-ttu-id="583e9-104">Sia le [immagini personalizzate](devtest-lab-create-template.md) che le [formule](devtest-lab-manage-formulas.md) possono essere usate come basi per [creare nuove macchine virtuali](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="583e9-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm-with-artifacts.md).</span></span> <span data-ttu-id="583e9-105">Tuttavia, hello chiave per distinguere le immagini personalizzate e le formule è che un'immagine personalizzata è semplicemente un'immagine basata su un disco rigido virtuale, mentre una formula è un'immagine basata su un disco rigido virtuale *oltre a* preconfigurato impostazioni - ad esempio dimensioni delle macchine Virtuali, rete virtuale, subnet e gli elementi.</span><span class="sxs-lookup"><span data-stu-id="583e9-105">However, hello key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span></span> <span data-ttu-id="583e9-106">Queste impostazioni preconfigurate vengono configurate con i valori predefiniti che possono essere sostituiti in fase di hello di creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="583e9-106">These preconfigured settings are set up with default values that can be overridden at hello time of VM creation.</span></span> <span data-ttu-id="583e9-107">In questo articolo illustra alcuni dei vantaggi di hello (Pro) e immagini personalizzate di toousing (cons) piuttosto che utilizzare formule svantaggi.</span><span class="sxs-lookup"><span data-stu-id="583e9-107">This article explains some of hello advantages (pros) and disadvantages (cons) toousing custom images versus using formulas.</span></span>

## <a name="custom-image-pros-and-cons"></a><span data-ttu-id="583e9-108">Vantaggi e svantaggi delle immagini personalizzate</span><span class="sxs-lookup"><span data-stu-id="583e9-108">Custom image pros and cons</span></span>
<span data-ttu-id="583e9-109">Immagini personalizzate forniscono un metodo statico e non modificabile di toocreate macchine virtuali da un ambiente desiderato.</span><span class="sxs-lookup"><span data-stu-id="583e9-109">Custom images provide a static, immutable way toocreate VMs from a desired environment.</span></span> 

<span data-ttu-id="583e9-110">**Vantaggi**</span><span class="sxs-lookup"><span data-stu-id="583e9-110">**Pros**</span></span>

* <span data-ttu-id="583e9-111">VM provisioning da un'immagine personalizzata è veloce, non vengono apportate modifiche dopo la macchina virtuale viene riattivata hello dall'immagine hello.</span><span class="sxs-lookup"><span data-stu-id="583e9-111">VM provisioning from a custom image is fast as nothing changes after hello VM is spun up from hello image.</span></span> <span data-ttu-id="583e9-112">Sono non disponibili in altre parole, tooapply impostazioni come immagine personalizzata hello è solo un'immagine senza le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="583e9-112">In other words, there are no settings tooapply as hello custom image is just an image without settings.</span></span> 
* <span data-ttu-id="583e9-113">Le macchine virtuali create da un'unica immagine personalizzata sono identiche.</span><span class="sxs-lookup"><span data-stu-id="583e9-113">VMs created from a single custom image are identical.</span></span>

<span data-ttu-id="583e9-114">**Svantaggi**</span><span class="sxs-lookup"><span data-stu-id="583e9-114">**Cons**</span></span>

* <span data-ttu-id="583e9-115">Se è necessario tooupdate alcuni aspetti dell'immagine personalizzata hello, è necessario ricreare l'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="583e9-115">If you need tooupdate some aspect of hello custom image, hello image must be recreated.</span></span>  

## <a name="formula-pros-and-cons"></a><span data-ttu-id="583e9-116">Vantaggi e svantaggi delle formule</span><span class="sxs-lookup"><span data-stu-id="583e9-116">Formula pros and cons</span></span>
<span data-ttu-id="583e9-117">Le formule forniscono un toocreate dinamico modo macchine virtuali dalle impostazioni di configurazione/hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="583e9-117">Formulas provide a dynamic way toocreate VMs from hello desired configuration/settings.</span></span>

<span data-ttu-id="583e9-118">**Vantaggi**</span><span class="sxs-lookup"><span data-stu-id="583e9-118">**Pros**</span></span>

* <span data-ttu-id="583e9-119">È possibile acquisire le modifiche nell'ambiente di hello hello volo tramite gli elementi.</span><span class="sxs-lookup"><span data-stu-id="583e9-119">Changes in hello environment can be captured on hello fly via artifacts.</span></span> <span data-ttu-id="583e9-120">Ad esempio, se si desidera che una macchina virtuale installata con i bit più recenti di hello dalla pipeline di rilascio o integra codice più recente di hello dal repository, è possibile specificare semplicemente un elemento che distribuisce i bit più recenti hello o inserisce il codice più recente di hello nella formula hello insieme a un immagine di base di destinazione.</span><span class="sxs-lookup"><span data-stu-id="583e9-120">For example, if you want a VM installed with hello latest bits from your release pipeline or enlist hello latest code from your repository, you can simply specify an artifact that deploys hello latest bits or enlists hello latest code in hello formula together with a target base image.</span></span> <span data-ttu-id="583e9-121">Ogni volta che questa formula macchine virtuali utilizzate toocreate, codice o i bit più recente hello sono distribuiti integrata toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="583e9-121">Whenever this formula is used toocreate VMs, hello latest bits/code are deployed/enlisted toohello VM.</span></span> 
* <span data-ttu-id="583e9-122">A differenza delle immagini personalizzate, le formule possono definire impostazioni predefinite come le dimensioni delle macchine virtuali e le impostazioni della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="583e9-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span></span> 
* <span data-ttu-id="583e9-123">le impostazioni di Hello salvate in una formula vengono visualizzate come valori predefiniti, ma possono essere modificate quando viene creato hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="583e9-123">hello settings saved in a formula are shown as default values, but can be modified when hello VM is created.</span></span> 

<span data-ttu-id="583e9-124">**Svantaggi**</span><span class="sxs-lookup"><span data-stu-id="583e9-124">**Cons**</span></span>

* <span data-ttu-id="583e9-125">La creazione di una macchina virtuale da una formula può richiedere più tempo rispetto alla creazione da un'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="583e9-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="583e9-126">Post di blog correlati</span><span class="sxs-lookup"><span data-stu-id="583e9-126">Related blog posts</span></span>
* [<span data-ttu-id="583e9-127">Custom images or formulas? (Immagini personalizzate o formule?)</span><span class="sxs-lookup"><span data-stu-id="583e9-127">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="583e9-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="583e9-128">Next steps</span></span>
- [<span data-ttu-id="583e9-129">Domande frequenti su DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="583e9-129">DevTest Labs FAQ</span></span>](devtest-lab-faq.md)