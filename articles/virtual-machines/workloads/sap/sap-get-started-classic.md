---
title: Uso di SAP sulle macchine virtuali Linux | Microsoft Docs
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
ms.openlocfilehash: 66eb53f99ce4b30ec283243deb3649c9ca897a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-sap-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="d0b97-103">Uso di SAP su macchine virtuali Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="d0b97-103">Using SAP on Linux virtual machines in Azure</span></span>
<span data-ttu-id="d0b97-104">Cloud computing è un termine ampiamente diffuso che sta assumendo un'importanza sempre più rilevante nel settore IT, dalle piccole imprese fino alle grandi aziende e alle multinazionali.</span><span class="sxs-lookup"><span data-stu-id="d0b97-104">Cloud Computing is a widely used term which is gaining more and more importance within the IT industry, from small companies up to large and multinational corporations.</span></span> <span data-ttu-id="d0b97-105">Microsoft Azure è la piattaforma di servizi cloud di Microsoft che offre un'ampia gamma di nuove possibilità.</span><span class="sxs-lookup"><span data-stu-id="d0b97-105">Microsoft Azure is the Cloud Services Platform from Microsoft which offers a wide spectrum of new possibilities.</span></span> <span data-ttu-id="d0b97-106">I clienti possono infatti effettuare rapidamente il provisioning e il deprovisioning di applicazioni come servizi cloud, senza essere soggetti a eventuali limiti tecnici o di budget.</span><span class="sxs-lookup"><span data-stu-id="d0b97-106">Now customers are able to rapidly provision and de-provision applications as Cloud-Services, so they are not limited to technical or budgeting restrictions.</span></span> <span data-ttu-id="d0b97-107">Anziché investire tempo e denaro nell'infrastruttura hardware, le aziende possono concentrarsi sull'applicazione, sui processi aziendali e sui vantaggi per clienti e utenti.</span><span class="sxs-lookup"><span data-stu-id="d0b97-107">Instead of investing time and budget into hardware infrastructure, companies can focus on the application, business processes and its benefits for customers and users.</span></span>

<span data-ttu-id="d0b97-108">Grazie alle macchine virtuali Microsoft Azure, Microsoft offre una piattaforma IaaS (Infrastructure as a Service, infrastruttura distribuita come servizio) completa.</span><span class="sxs-lookup"><span data-stu-id="d0b97-108">With Microsoft Azure virtual machines, Microsoft offers a comprehensive Infrastructure as a Service (IaaS) platform.</span></span> <span data-ttu-id="d0b97-109">Le applicazioni basate su SAP NetWeaver sono supportate in Macchine virtuali di Azure (IaaS).</span><span class="sxs-lookup"><span data-stu-id="d0b97-109">SAP NetWeaver based applications are supported on Azure Virtual Machines (IaaS).</span></span> <span data-ttu-id="d0b97-110">I white paper seguenti descrivono come pianificare e implementare applicazioni basate su SAP NetWeaver su macchine virtuali Windows in Azure.</span><span class="sxs-lookup"><span data-stu-id="d0b97-110">The whitepapers below describe how to plan and implement SAP NetWeaver based applications on Windows virtual machines in Azure.</span></span> <span data-ttu-id="d0b97-111">È anche possibile implementare applicazioni basate su SAP NetWeaver su [macchine virtuali Windows](../../virtual-machines-windows-classic-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d0b97-111">You can also implement SAP NetWeaver based applications on [Windows virtual machines](../../virtual-machines-windows-classic-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure-suse-linux-virtual-machines"></a><span data-ttu-id="d0b97-112">SAP NetWeaver nelle macchine virtuali SUSE Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="d0b97-112">SAP NetWeaver on Azure SUSE Linux Virtual Machines</span></span>
<span data-ttu-id="d0b97-113">Titolo: Test di SAP NetWeaver nelle macchine virtuali SUSE Linux di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d0b97-113">Title: Testing SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span>

<span data-ttu-id="d0b97-114">Riepilogo: attualmente, non è previsto alcun supporto ufficiale di SAP per l'esecuzione di SAP NetWeaver nelle macchine virtuali Linux di Azure.</span><span class="sxs-lookup"><span data-stu-id="d0b97-114">Summary: There is no official SAP support for running SAP NetWeaver on Azure Linux VMs at this point in time.</span></span> <span data-ttu-id="d0b97-115">Tuttavia, i clienti potrebbero richiedere di eseguire alcuni test o considerare di eseguire SAP dimostrativi o sistemi di formazione in macchine virtuali Linux di Azure fino a quando non è necessario contattare il supporto SAP.</span><span class="sxs-lookup"><span data-stu-id="d0b97-115">Nevertheless customers might want to do some testing or might consider to run SAP demo or training systems on Azure Linux VMs as long as there is no need for contacting SAP support.</span></span> <span data-ttu-id="d0b97-116">In questo articolo viene descritto come configurare le macchine virtuali SUSE Linux di Azure per l'esecuzione di SAP; inoltre, vengono forniti alcuni suggerimenti di base per evitare errori potenziali comuni.</span><span class="sxs-lookup"><span data-stu-id="d0b97-116">This article should help setting up Azure SUSE Linux VMs for running SAP and gives some basic hints in order to avoid common potential pitfalls.</span></span>

<span data-ttu-id="d0b97-117">Ultimo aggiornamento: dicembre 2015</span><span class="sxs-lookup"><span data-stu-id="d0b97-117">Updated: December 2015</span></span>

[<span data-ttu-id="d0b97-118">Questo articolo è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="d0b97-118">This article can be found here</span></span>](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

