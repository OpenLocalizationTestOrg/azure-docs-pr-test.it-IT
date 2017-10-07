---
title: aaaUsing SAP nelle macchine virtuali Linux | Documenti Microsoft
description: Informazioni sull'uso di SAP in macchine virtuali (VM) Linux in Microsoft Azure
services: virtual-machines-linux,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: f9cd93dc-71ad-48a4-8778-4e48aec484a6
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: a805cdecb515239057e185a92bf5c4d4e707f72f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="9cd43-103">Uso di SAP su macchine virtuali Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="9cd43-103">Using SAP on Linux virtual machines in Azure</span></span>
<span data-ttu-id="9cd43-104">Il cloud Computing è un termine ampiamente diffuso importanza sempre maggiore di hello settore IT, dalle piccole imprese di società toolarge e implementazione.</span><span class="sxs-lookup"><span data-stu-id="9cd43-104">Cloud Computing is a widely used term which is gaining more and more importance within hello IT industry, from small companies up toolarge and multinational corporations.</span></span> <span data-ttu-id="9cd43-105">Microsoft Azure è una piattaforma di servizi Cloud Microsoft che offre un'ampia gamma di nuove possibilità hello.</span><span class="sxs-lookup"><span data-stu-id="9cd43-105">Microsoft Azure is hello Cloud Services Platform from Microsoft which offers a wide spectrum of new possibilities.</span></span> <span data-ttu-id="9cd43-106">I clienti sono ora toorapidly in grado di effettuare il provisioning e la prestazione applicazioni come servizi Cloud, in modo che non siano tootechnical limitato o restrizioni budget.</span><span class="sxs-lookup"><span data-stu-id="9cd43-106">Now customers are able toorapidly provision and de-provision applications as Cloud-Services, so they are not limited tootechnical or budgeting restrictions.</span></span> <span data-ttu-id="9cd43-107">Invece di investire tempo e denaro nell'infrastruttura hardware, le organizzazioni possono dedicarsi applicazione hello, i processi di business e i vantaggi per clienti e utenti.</span><span class="sxs-lookup"><span data-stu-id="9cd43-107">Instead of investing time and budget into hardware infrastructure, companies can focus on hello application, business processes and its benefits for customers and users.</span></span>

<span data-ttu-id="9cd43-108">Grazie alle macchine virtuali Microsoft Azure, Microsoft offre una piattaforma IaaS (Infrastructure as a Service, infrastruttura distribuita come servizio) completa.</span><span class="sxs-lookup"><span data-stu-id="9cd43-108">With Microsoft Azure virtual machines, Microsoft offers a comprehensive Infrastructure as a Service (IaaS) platform.</span></span> <span data-ttu-id="9cd43-109">Le applicazioni basate su SAP NetWeaver sono supportate in Macchine virtuali di Azure (IaaS).</span><span class="sxs-lookup"><span data-stu-id="9cd43-109">SAP NetWeaver based applications are supported on Azure Virtual Machines (IaaS).</span></span> <span data-ttu-id="9cd43-110">white paper Hello riportato di seguito viene descritto come tooplan e implementare SAP NetWeaver su applicazioni basate su macchine virtuali Windows in Azure.</span><span class="sxs-lookup"><span data-stu-id="9cd43-110">hello whitepapers below describe how tooplan and implement SAP NetWeaver based applications on Windows virtual machines in Azure.</span></span> <span data-ttu-id="9cd43-111">È anche possibile implementare applicazioni basate su SAP NetWeaver su [macchine virtuali Windows](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9cd43-111">You can also implement SAP NetWeaver based applications on [Windows virtual machines](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure-suse-linux-virtual-machines"></a><span data-ttu-id="9cd43-112">SAP NetWeaver nelle macchine virtuali SUSE Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="9cd43-112">SAP NetWeaver on Azure SUSE Linux Virtual Machines</span></span>
<span data-ttu-id="9cd43-113">titolo: aaaTesting SAP NetWeaver in macchine virtuali di Microsoft Azure SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="9cd43-113">title: aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span>

<span data-ttu-id="9cd43-114">Riepilogo: attualmente, non è previsto alcun supporto ufficiale di SAP per l'esecuzione di SAP NetWeaver nelle macchine virtuali Linux di Azure.</span><span class="sxs-lookup"><span data-stu-id="9cd43-114">Summary: There is no official SAP support for running SAP NetWeaver on Azure Linux VMs at this point in time.</span></span> <span data-ttu-id="9cd43-115">Tuttavia i clienti possono toodo alcuni test o potrebbero considerare toorun sistemi demo o di formazione di SAP in macchine virtuali Linux di Azure fino a quando non è necessario per contattare il supporto SAP.</span><span class="sxs-lookup"><span data-stu-id="9cd43-115">Nevertheless customers might want toodo some testing or might consider toorun SAP demo or training systems on Azure Linux VMs as long as there is no need for contacting SAP support.</span></span> <span data-ttu-id="9cd43-116">In questo articolo per l'esecuzione di SAP deve permettere la configurazione di macchine virtuali di Azure SUSE Linux e fornisce alcuni suggerimenti di base nell'ordine tooavoid potenziali problemi comuni.</span><span class="sxs-lookup"><span data-stu-id="9cd43-116">This article should help setting up Azure SUSE Linux VMs for running SAP and gives some basic hints in order tooavoid common potential pitfalls.</span></span>

<span data-ttu-id="9cd43-117">Ultimo aggiornamento: dicembre 2015</span><span class="sxs-lookup"><span data-stu-id="9cd43-117">Updated: December 2015</span></span>

[<span data-ttu-id="9cd43-118">Questo articolo è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="9cd43-118">This article can be found here</span></span>](../../virtual-machines-linux-sap-on-suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

