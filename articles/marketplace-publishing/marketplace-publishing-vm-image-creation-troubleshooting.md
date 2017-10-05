---
title: Come risolvere problemi comuni durante la creazione del disco rigido virtuale | Documentazione Microsoft
description: Risposte alle domande frequenti sulla risoluzione dei problemi durante la creazione del disco rigido virtuale.
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: 
editor: 
ms.assetid: e39563d8-8646-4cb7-b078-8b10ac35b494
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 09/26/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c4e88a9fbb15dd90d619b159ae1065dfacc1907f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-troubleshoot-common-issues-encountered-during-vhd-creation"></a><span data-ttu-id="e067f-103">Come risolvere problemi comuni incontrati durante la creazione del disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="e067f-103">How to troubleshoot common issues encountered during VHD creation</span></span>
<span data-ttu-id="e067f-104">Questo articolo viene fornito per aiutare gli sviluppatori e/o i co-amministratori di Azure Marketplace nel caso in cui registrino un problema o abbiano domande generiche nel momento in cui pubblicano o gestiscono la propria soluzione basata su macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e067f-104">This article is provided to help an Azure Marketplace publisher and/or co-administrator that may experience an issue or have common questions while publishing or managing their virtual machine solution(s).</span></span>

1. <span data-ttu-id="e067f-105">Come è possibile modificare il nome dell'host?</span><span class="sxs-lookup"><span data-stu-id="e067f-105">How do I change the name of the host?</span></span>
   
    <span data-ttu-id="e067f-106">Non è possibile aggiornare il nome dell'host dopo aver creato la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e067f-106">Once VM is created, users can’t update the name of the host.</span></span>
2. <span data-ttu-id="e067f-107">Come reimpostare il servizio Desktop remoto o la relativa password di accesso?</span><span class="sxs-lookup"><span data-stu-id="e067f-107">How to reset the Remote Desktop service or its login password?</span></span>
   
   * [<span data-ttu-id="e067f-108">Riferimento per macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="e067f-108">Reference for Windows VM</span></span>](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-reset-rdp/)
   * [<span data-ttu-id="e067f-109">Riferimento per macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="e067f-109">Reference for Linux VM</span></span>](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
3. <span data-ttu-id="e067f-110">Come generare nuovi certificati SSH?</span><span class="sxs-lookup"><span data-stu-id="e067f-110">How to generate new ssh certificates?</span></span>
   
   <span data-ttu-id="e067f-111">Vedere il collegamento: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)</span><span class="sxs-lookup"><span data-stu-id="e067f-111">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)</span></span>
4. <span data-ttu-id="e067f-112">Come configurare un certificato VPN aperto?</span><span class="sxs-lookup"><span data-stu-id="e067f-112">How to configure an open VPN certificate?</span></span>
   
   <span data-ttu-id="e067f-113">Vedere il collegamento: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)</span><span class="sxs-lookup"><span data-stu-id="e067f-113">Please refer to the link: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)</span></span>
5. <span data-ttu-id="e067f-114">Quali sono i criteri di supporto per l'esecuzione di software server Microsoft nell'ambiente di macchina virtuale di Microsoft Azure (Infrastructure-as-a-Service) ?</span><span class="sxs-lookup"><span data-stu-id="e067f-114">What is the support policy for running Microsoft server software in the Microsoft Azure virtual machine environment (infrastructure-as-a-service)?</span></span>
   
   <span data-ttu-id="e067f-115">Vedere il collegamento: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span><span class="sxs-lookup"><span data-stu-id="e067f-115">Please refer to the link: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span></span>
6. <span data-ttu-id="e067f-116">Le macchine virtuali hanno un identificatore univoco?</span><span class="sxs-lookup"><span data-stu-id="e067f-116">Do Virtual Machines have any unique identifier?</span></span>
   
   <span data-ttu-id="e067f-117">Azure codifica un ID univoco in ogni macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e067f-117">Azure encodes Azure VM Unique ID in every VM.</span></span> <span data-ttu-id="e067f-118">Per maggiori informazioni, visitare il blog e la documentazione appropriati.</span><span class="sxs-lookup"><span data-stu-id="e067f-118">See details in this blog and documentation.</span></span>
7. <span data-ttu-id="e067f-119">In una macchina virtuale, com'è possibile gestire l'estensione di script personalizzati nell'attività di avvio?</span><span class="sxs-lookup"><span data-stu-id="e067f-119">In a VM how can I manage the custom script extension in the startup task?</span></span>
   
   <span data-ttu-id="e067f-120">Vedere il collegamento: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)</span><span class="sxs-lookup"><span data-stu-id="e067f-120">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)</span></span>
8. <span data-ttu-id="e067f-121">Come creare una macchina virtuale dal portale di Azure usando il disco rigido virtuale caricato in archiviazione Premium?</span><span class="sxs-lookup"><span data-stu-id="e067f-121">How to create a VM from the Azure portal using the VHD that is uploaded to premium storage?</span></span>
   
   <span data-ttu-id="e067f-122">Questa funzionalità non è ancora supportata.</span><span class="sxs-lookup"><span data-stu-id="e067f-122">We do not support this feature yet.</span></span>
9. <span data-ttu-id="e067f-123">In Azure Marketplace sono supportate applicazioni a 32 bit?</span><span class="sxs-lookup"><span data-stu-id="e067f-123">Is a 32-bit app supported in the Azure Marketplace?</span></span>
   
   <span data-ttu-id="e067f-124">Per informazioni sui criteri di supporto, vedere il collegamento: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span><span class="sxs-lookup"><span data-stu-id="e067f-124">Please refer to the link for details on the support policy: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span></span>
10. <span data-ttu-id="e067f-125">Ogni volta che si tenta di creare un'immagine dai dischi rigidi virtuali, in PowerShell viene visualizzato un errore che indica che il disco rigido virtuale è già registrato con l'archivio immagini come risorsa.</span><span class="sxs-lookup"><span data-stu-id="e067f-125">Every time I am trying to create an image from my VHDs, I get the error “.VHD is already registered with image repository as the resource” in PowerShell.</span></span> <span data-ttu-id="e067f-126">Ma non ho creato alcun tipo di risorsa in precedenza, né ho trovato un'immagine con questo nome in Azure.</span><span class="sxs-lookup"><span data-stu-id="e067f-126">I did not create any image before nor did I find any image with this name in Azure.</span></span> <span data-ttu-id="e067f-127">Come posso risolvere il problema?</span><span class="sxs-lookup"><span data-stu-id="e067f-127">How do I resolve this?</span></span>
    
    <span data-ttu-id="e067f-128">Questo problema si verifica in genere se l'utente ha eseguito il provisioning di una macchina virtuale da questo disco rigido virtuale, creando un blocco sul disco virtuale.</span><span class="sxs-lookup"><span data-stu-id="e067f-128">This usually happen if the user provisioned a VM from this VHD and there is a lock on that VHD.</span></span> <span data-ttu-id="e067f-129">Verificare che non sia stata allocata nessuna macchina virtuale da questo disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="e067f-129">Please check that there is no VM allocated from this VHD.</span></span> <span data-ttu-id="e067f-130">Se il problema persiste, generare un ticket di supporto usando questo collegamento o dal portale di pubblicazione (maggiori dettagli sono disponibili nella risposta alla domanda 11).</span><span class="sxs-lookup"><span data-stu-id="e067f-130">If the error still persist , then please raise a support ticket using this link or from the Publishing portal regarding this (details are given in the answer of question 11).</span></span>