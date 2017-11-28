---
title: aaaGet un ID di macchina virtuale Linux di Azure | Documenti Microsoft
description: Viene descritto come tooget e utilizzare un Azure Linux VM ID univoco.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 136c5d28-ff6b-4466-b27f-7a29785b5d27
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 01/23/2017
ms.author: kmouss
ms.openlocfilehash: 4c8ddfc2e892824581e77649285ee8adbccd5def
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a><span data-ttu-id="c2220-103">Accesso e uso dell'ID univoco di una VM di Azure</span><span class="sxs-lookup"><span data-stu-id="c2220-103">Accessing and Using Azure VM Unique ID</span></span>
<span data-ttu-id="c2220-104">L'ID univoco di una VM di Azure è un identificatore a 128 bit codificato e archiviato nel sistema SMBIOS di tutte le VM IaaS di Azure e attualmente può essere letto usando i comandi BIOS della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="c2220-104">Azure VM unique ID is a 128bits identifier encoded and stored in all Azure IaaS VM’s SMBIOS and can currently be read using platform BIOS commands.</span></span>

<span data-ttu-id="c2220-105">L'ID univoco di una VM di Azure è una proprietà di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="c2220-105">Azure VM unique ID is a Read-only property.</span></span> <span data-ttu-id="c2220-106">L'ID univoco di una VM di Azure non verrà modificato in caso di riavvio, arresto (pianificato o non pianificato), avvio/arresto della deallocazione, riparazione di servizi o ripristino sul posto.</span><span class="sxs-lookup"><span data-stu-id="c2220-106">Azure Unique VM ID won’t change upon reboot shutdown (either planned for unplanned), Start/Stop de-allocate, service healing or restore in place.</span></span> <span data-ttu-id="c2220-107">Tuttavia, se hello VM è un toocreate snapshot e copia di una nuova istanza, nuovo ID di macchina virtuale di Azure è configurato.</span><span class="sxs-lookup"><span data-stu-id="c2220-107">However, if hello VM is a snapshot and copied toocreate a new instance, new Azure VM ID is configured.</span></span>

> [!NOTE]
> <span data-ttu-id="c2220-108">Se si dispone di macchine virtuali meno recenti create e in esecuzione poiché questa nuova funzionalità ottenuto implementata (18 settembre 2014), riavviare la macchina virtuale tooautomatically ottenere un ID univoco Azure.</span><span class="sxs-lookup"><span data-stu-id="c2220-108">If you have older VMs created and running since this new feature got rolled out (September 18, 2014), please restart your VM tooautomatically get an Azure unique ID.</span></span>
> 
> 

<span data-ttu-id="c2220-109">tooaccess univoco ID macchina virtuale Azure all'interno di hello VM:</span><span class="sxs-lookup"><span data-stu-id="c2220-109">tooaccess Azure Unique VM ID from within hello VM:</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="c2220-110">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c2220-110">Create a VM</span></span>
<span data-ttu-id="c2220-111">Per altre informazioni, vedere [Creare una macchina virtuale](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="c2220-111">For more information, see [Create a Virtual Machine](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="connect-toohello-vm"></a><span data-ttu-id="c2220-112">Connettersi toohello VM</span><span class="sxs-lookup"><span data-stu-id="c2220-112">Connect toohello VM</span></span>
<span data-ttu-id="c2220-113">Per altre informazioni, vedere [SSH da Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="c2220-113">For more information, see [SSH from Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="query-vm-unique-id"></a><span data-ttu-id="c2220-114">Effettuare una query dell'ID univoco di una VM</span><span class="sxs-lookup"><span data-stu-id="c2220-114">Query VM Unique ID</span></span>
<span data-ttu-id="c2220-115">Comando (l'esempio usa **Ubuntu**):</span><span class="sxs-lookup"><span data-stu-id="c2220-115">Command (example uses **Ubuntu**):</span></span>

```bash
sudo dmidecode | grep UUID
```

<span data-ttu-id="c2220-116">Risultati previsti per l'esempio:</span><span class="sxs-lookup"><span data-stu-id="c2220-116">Example Expected Results:</span></span>

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

<span data-ttu-id="c2220-117">A causa di tooBig bit ordine Little-Endian, hello effettivo ID univoco di VM in questo caso sarà:</span><span class="sxs-lookup"><span data-stu-id="c2220-117">Due tooBig Endian bit ordering, hello actual Unique VM ID in this case will be:</span></span>

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

<span data-ttu-id="c2220-118">ID univoco di VM Azure può essere usata in diversi scenari se hello macchina virtuale è in esecuzione in Azure o in locale e può aiutare i requisiti di gestione licenze, report o generale che è possibile in distribuzioni IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2220-118">Azure VM unique ID can be used in different scenarios whether hello VM is running on Azure or on-premises and can help your licensing, reporting or general tracking requirements you may have on your Azure IaaS deployments.</span></span> <span data-ttu-id="c2220-119">Molti fornitori di software indipendenti, applicazioni e la certificazione li in Azure possono richiedere una macchina virtuale di Azure in tutto il ciclo di vita e tootell tooidentify se hello macchina virtuale è in esecuzione in Azure, locale o in altri provider di cloud.</span><span class="sxs-lookup"><span data-stu-id="c2220-119">Many independent software vendors building applications and certifying them on Azure may require tooidentify an Azure VM throughout its lifecycle and tootell if hello VM is running on Azure, on-Premises or on other cloud providers.</span></span> <span data-ttu-id="c2220-120">Questo identificatore di piattaforma, ad esempio consente di rilevare se il software di hello correttamente è concesso in licenza o della Guida di qualsiasi origine tooits dati di macchina virtuale, ad esempio tooassist sull'impostazione hello destra la metrica per piattaforma destra hello e tootrack toocorrelate e correlare queste metriche, tra cui altri utilizzi.</span><span class="sxs-lookup"><span data-stu-id="c2220-120">This platform identifier can for example help detect if hello software is properly licensed or help toocorrelate any VM data tooits source such as tooassist on setting hello right metrics for hello right platform and tootrack and correlate these metrics amongst other uses.</span></span>

