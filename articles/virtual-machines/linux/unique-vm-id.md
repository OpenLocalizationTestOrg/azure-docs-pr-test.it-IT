---
title: Ottenere un ID di macchina virtuale Linux di Azure | Documentazione Microsoft
description: Illustra come ottenere e usare un ID univoco di macchina virtuale Linux di Azure.
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
ms.openlocfilehash: 258ce425d5692730011cf2f4468dc0ba77f4cb79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a><span data-ttu-id="50881-103">Accesso e uso dell'ID univoco di una VM di Azure</span><span class="sxs-lookup"><span data-stu-id="50881-103">Accessing and Using Azure VM Unique ID</span></span>
<span data-ttu-id="50881-104">L'ID univoco di una VM di Azure è un identificatore a 128 bit codificato e archiviato nel sistema SMBIOS di tutte le VM IaaS di Azure e attualmente può essere letto usando i comandi BIOS della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="50881-104">Azure VM unique ID is a 128bits identifier encoded and stored in all Azure IaaS VM’s SMBIOS and can currently be read using platform BIOS commands.</span></span>

<span data-ttu-id="50881-105">L'ID univoco di una VM di Azure è una proprietà di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="50881-105">Azure VM unique ID is a Read-only property.</span></span> <span data-ttu-id="50881-106">L'ID univoco di una VM di Azure non verrà modificato in caso di riavvio, arresto (pianificato o non pianificato), avvio/arresto della deallocazione, riparazione di servizi o ripristino sul posto.</span><span class="sxs-lookup"><span data-stu-id="50881-106">Azure Unique VM ID won’t change upon reboot shutdown (either planned for unplanned), Start/Stop de-allocate, service healing or restore in place.</span></span> <span data-ttu-id="50881-107">Se, tuttavia, la VM è uno snapshot e viene copiata per creare una nuova istanza, viene configurato l'ID univoco della VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="50881-107">However, if the VM is a snapshot and copied to create a new instance, new Azure VM ID is configured.</span></span>

> [!NOTE]
> <span data-ttu-id="50881-108">Se in precedenza sono state create VM in esecuzione da quando questa nuova funzionalità è stata implementata (18 settembre 2014), riavviare ogni VM per ottenere automaticamente un ID univoco di Azure.</span><span class="sxs-lookup"><span data-stu-id="50881-108">If you have older VMs created and running since this new feature got rolled out (September 18, 2014), please restart your VM to automatically get an Azure unique ID.</span></span>
> 
> 

<span data-ttu-id="50881-109">Per accedere all'ID univoco di una VM di Azure dalla VM:</span><span class="sxs-lookup"><span data-stu-id="50881-109">To access Azure Unique VM ID from within the VM:</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="50881-110">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="50881-110">Create a VM</span></span>
<span data-ttu-id="50881-111">Per altre informazioni, vedere [Creare una macchina virtuale](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="50881-111">For more information, see [Create a Virtual Machine](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="connect-to-the-vm"></a><span data-ttu-id="50881-112">Connettersi alla VM</span><span class="sxs-lookup"><span data-stu-id="50881-112">Connect to the VM</span></span>
<span data-ttu-id="50881-113">Per altre informazioni, vedere [SSH da Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="50881-113">For more information, see [SSH from Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="query-vm-unique-id"></a><span data-ttu-id="50881-114">Effettuare una query dell'ID univoco di una VM</span><span class="sxs-lookup"><span data-stu-id="50881-114">Query VM Unique ID</span></span>
<span data-ttu-id="50881-115">Comando (l'esempio usa **Ubuntu**):</span><span class="sxs-lookup"><span data-stu-id="50881-115">Command (example uses **Ubuntu**):</span></span>

```bash
sudo dmidecode | grep UUID
```

<span data-ttu-id="50881-116">Risultati previsti per l'esempio:</span><span class="sxs-lookup"><span data-stu-id="50881-116">Example Expected Results:</span></span>

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

<span data-ttu-id="50881-117">A causa dell'ordinamento dei bit big endian, l'ID univoco effettivo della VM in questo caso sarà:</span><span class="sxs-lookup"><span data-stu-id="50881-117">Due to Big Endian bit ordering, the actual Unique VM ID in this case will be:</span></span>

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

<span data-ttu-id="50881-118">L'ID univoco di una VM di Azure può essere usato in scenari diversi indipendentemente dal fatto che la VM sia in esecuzione in Azure o in locale e consente di soddisfare eventuali requisiti relativi a licenze, creazione di report o verifica generale nelle distribuzioni IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="50881-118">Azure VM unique ID can be used in different scenarios whether the VM is running on Azure or on-premises and can help your licensing, reporting or general tracking requirements you may have on your Azure IaaS deployments.</span></span> <span data-ttu-id="50881-119">Diversi fornitori di software indipendenti che compilano applicazioni e le certificano in Azure potrebbero richiedere di identificare una VM di Azure durante il suo ciclo di vita e di indicare se la VM è in esecuzione in Azure, in locale o in altri provider di servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="50881-119">Many independent software vendors building applications and certifying them on Azure may require to identify an Azure VM throughout its lifecycle and to tell if the VM is running on Azure, on-Premises or on other cloud providers.</span></span> <span data-ttu-id="50881-120">Questo identificatore di piattaforma consente, ad esempio, di rilevare se la licenza del software è corretta o di correlare i dati di una VM all'origine, ad esempio per fornire assistenza nell'impostazione della metrica appropriata a seconda della piattaforma e per tenere traccia di questa metrica e correlarla tra gli altri utenti.</span><span class="sxs-lookup"><span data-stu-id="50881-120">This platform identifier can for example help detect if the software is properly licensed or help to correlate any VM data to its source such as to assist on setting the right metrics for the right platform and to track and correlate these metrics amongst other uses.</span></span>

