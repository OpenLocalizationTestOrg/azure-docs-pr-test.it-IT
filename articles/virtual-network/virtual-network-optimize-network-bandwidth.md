---
title: "velocità effettiva della rete VM aaaOptimize | Documenti Microsoft"
description: "Informazioni su come macchina virtuale di Azure toooptimize rete velocità effettiva."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: steveesp
ms.openlocfilehash: a5cff2d0ab6e3553c3f90d99629521a431477de0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a><span data-ttu-id="3f873-103">Ottimizzare la velocità effettiva di rete per le macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="3f873-103">Optimize network throughput for Azure virtual machines</span></span>

<span data-ttu-id="3f873-104">Le macchine virtuali di Azure hanno impostazioni di rete predefinite che possono essere ottimizzate ulteriormente per una migliore velocità effettiva di rete.</span><span class="sxs-lookup"><span data-stu-id="3f873-104">Azure virtual machines (VM) have default network settings that can be further optimized for network throughput.</span></span> <span data-ttu-id="3f873-105">In questo articolo viene descritto come toooptimize velocità effettiva di rete per Microsoft Windows Azure e le macchine virtuali Linux, incluse le distribuzioni principali quali Ubuntu, CentOS e Red Hat.</span><span class="sxs-lookup"><span data-stu-id="3f873-105">This article describes how toooptimize network throughput for Microsoft Azure Windows and Linux VMs, including major distributions such as Ubuntu, CentOS and Red Hat.</span></span>

## <a name="windows-vm"></a><span data-ttu-id="3f873-106">Macchina virtuale Windows</span><span class="sxs-lookup"><span data-stu-id="3f873-106">Windows VM</span></span>

<span data-ttu-id="3f873-107">Se la macchina virtuale di Windows è supportata con [Accelerated rete](virtual-network-create-vm-accelerated-networking.md), abilitare tale funzionalità sarebbe una configurazione ottimale di hello per la velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="3f873-107">If your Windows VM is supported with [Accelerated Networking](virtual-network-create-vm-accelerated-networking.md), enabling that feature would be hello optimal configuration for throughput.</span></span> <span data-ttu-id="3f873-108">Per tutte le altre macchine virtuali di Windows, tramite Receive-Side Scaling (RSS) esse possono raggiungere una velocità effettiva massima superiore rispetto a una VM senza RSS.</span><span class="sxs-lookup"><span data-stu-id="3f873-108">For all other Windows VMs, using Receive Side Scaling (RSS) can reach higher maximal throughput than a VM without RSS.</span></span> <span data-ttu-id="3f873-109">È possibile disabilitare RSS per impostazione predefinita in una macchina virtuale Windows.</span><span class="sxs-lookup"><span data-stu-id="3f873-109">RSS may be disabled by default in a Windows VM.</span></span> <span data-ttu-id="3f873-110">Completare i seguenti passaggi toodetermine se è abilitato RSS hello e tooenable se è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="3f873-110">Complete hello following steps toodetermine whether RSS is enabled and tooenable it if it's disabled.</span></span>

1. <span data-ttu-id="3f873-111">Immettere hello `Get-NetAdapterRss` toosee comando di PowerShell se RSS è abilitato per una scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="3f873-111">Enter hello `Get-NetAdapterRss` PowerShell command toosee if RSS is enabled for a network adapter.</span></span> <span data-ttu-id="3f873-112">In hello seguente esempio di output restituito da hello `Get-NetAdapterRss`, non è abilitato RSS.</span><span class="sxs-lookup"><span data-stu-id="3f873-112">In hello following example output returned from hello `Get-NetAdapterRss`, RSS is not enabled.</span></span>

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. <span data-ttu-id="3f873-113">Immettere hello tooenable comando RSS seguente:</span><span class="sxs-lookup"><span data-stu-id="3f873-113">Enter hello following command tooenable RSS:</span></span>

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    <span data-ttu-id="3f873-114">comando precedente Hello non possiede un output.</span><span class="sxs-lookup"><span data-stu-id="3f873-114">hello previous command does not have an output.</span></span> <span data-ttu-id="3f873-115">comando Hello modificato le impostazioni di interfaccia di rete, causando la perdita di connettività temporaneo per circa un minuto.</span><span class="sxs-lookup"><span data-stu-id="3f873-115">hello command changed NIC settings, causing temporary connectivity loss for about one minute.</span></span> <span data-ttu-id="3f873-116">Durante la perdita di connettività hello viene visualizzata una finestra di dialogo riconnessione in corso.</span><span class="sxs-lookup"><span data-stu-id="3f873-116">A Reconnecting dialog box appears during hello connectivity loss.</span></span> <span data-ttu-id="3f873-117">Connettività in genere viene ripristinata dopo il tentativo di terzo hello.</span><span class="sxs-lookup"><span data-stu-id="3f873-117">Connectivity is typically restored after hello third attempt.</span></span>
3. <span data-ttu-id="3f873-118">Confermare che RSS è abilitato nella VM hello immettendo hello `Get-NetAdapterRss` nuovo il comando.</span><span class="sxs-lookup"><span data-stu-id="3f873-118">Confirm that RSS is enabled in hello VM by entering hello `Get-NetAdapterRss` command again.</span></span> <span data-ttu-id="3f873-119">Se ha esito positivo, viene restituito hello output di esempio riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3f873-119">If successful, hello following example output is returned:</span></span>

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a><span data-ttu-id="3f873-120">VM Linux</span><span class="sxs-lookup"><span data-stu-id="3f873-120">Linux VM</span></span>

<span data-ttu-id="3f873-121">RSS è sempre abilitato per impostazione predefinita nella macchina virtuale Linux di Azure.</span><span class="sxs-lookup"><span data-stu-id="3f873-121">RSS is always enabled by default in an Azure Linux VM.</span></span> <span data-ttu-id="3f873-122">Il kernel Linux rilasciato a partire da gennaio January 2017 include nuove opzioni di ottimizzazione di rete che consentono una VM Linux tooachieve maggiore velocità effettiva della rete.</span><span class="sxs-lookup"><span data-stu-id="3f873-122">Linux kernels released since January, 2017 include new network optimization options that enable a Linux VM tooachieve higher network throughput.</span></span>

### <a name="ubuntu"></a><span data-ttu-id="3f873-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="3f873-123">Ubuntu</span></span>

<span data-ttu-id="3f873-124">Ottimizzazione di hello tooget ordine, prima di aggiornare toohello supportata più recente versione, a partire da giugno 2017, ovvero:</span><span class="sxs-lookup"><span data-stu-id="3f873-124">In order tooget hello optimization, first update toohello latest supported version, as of June 2017, which is:</span></span>
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
<span data-ttu-id="3f873-125">Al termine dell'aggiornamento di hello, immettere hello kernel più recente di comandi tooget hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="3f873-125">After hello update is complete, enter hello following commands tooget hello latest kernel:</span></span>

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

<span data-ttu-id="3f873-126">Comando facoltativo:</span><span class="sxs-lookup"><span data-stu-id="3f873-126">Optional command:</span></span>

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a><span data-ttu-id="3f873-127">Kernel Ubuntu Azure (anteprima)</span><span class="sxs-lookup"><span data-stu-id="3f873-127">Ubuntu Azure Preview kernel</span></span>
> [!WARNING]
> <span data-ttu-id="3f873-128">Questa versione di anteprima Linux Azure potrebbe non disporre kernel hello dello stesso livello di disponibilità e affidabilità come immagini Marketplace e directcompute che sono in genere il rilascio di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="3f873-128">This Azure Linux Preview kernel may not have hello same level of availability and reliability as Marketplace images and kernels that are in general availability release.</span></span> <span data-ttu-id="3f873-129">funzionalità di Hello non è supportato, può avere vincolato funzionalità e potrebbe non essere affidabili kernel predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="3f873-129">hello feature is not supported, may have constrained capabilities, and may not be as reliable as hello default kernel.</span></span> <span data-ttu-id="3f873-130">Non usare questo kernel per carichi di lavoro di produzione.</span><span class="sxs-lookup"><span data-stu-id="3f873-130">Do not use this kernel for production workloads.</span></span>

<span data-ttu-id="3f873-131">Installando hello proposto kernel Linux di Azure, è possibile ottenere prestazioni di velocità effettiva significativo.</span><span class="sxs-lookup"><span data-stu-id="3f873-131">Significant throughput performance can be achieved by installing hello proposed Azure Linux kernel.</span></span> <span data-ttu-id="3f873-132">tootry questo kernel, aggiungere questo too/etc/apt/sources.list riga</span><span class="sxs-lookup"><span data-stu-id="3f873-132">tootry this kernel, add this line too/etc/apt/sources.list</span></span>

```bash
#add this toohello end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

<span data-ttu-id="3f873-133">Eseguire quindi questi comandi come radice.</span><span class="sxs-lookup"><span data-stu-id="3f873-133">Then run these commands as root.</span></span>
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a><span data-ttu-id="3f873-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="3f873-134">CentOS</span></span>

<span data-ttu-id="3f873-135">Ottimizzazione di hello tooget ordine, prima di aggiornare toohello supportata più recente versione, a partire da luglio 2017, ovvero:</span><span class="sxs-lookup"><span data-stu-id="3f873-135">In order tooget hello optimization, first update toohello latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
<span data-ttu-id="3f873-136">Al termine dell'aggiornamento di hello, installare hello più recente Linux Integration Services (LIS).</span><span class="sxs-lookup"><span data-stu-id="3f873-136">After hello update is complete, install hello latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="3f873-137">ottimizzazione della velocità effettiva di Hello è LIS, a partire da 4.2.2-2.</span><span class="sxs-lookup"><span data-stu-id="3f873-137">hello throughput optimization is in LIS, starting from 4.2.2-2.</span></span> <span data-ttu-id="3f873-138">Immettere i seguenti comandi tooinstall LIS hello:</span><span class="sxs-lookup"><span data-stu-id="3f873-138">Enter hello following commands tooinstall LIS:</span></span>

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a><span data-ttu-id="3f873-139">Red Hat</span><span class="sxs-lookup"><span data-stu-id="3f873-139">Red Hat</span></span>

<span data-ttu-id="3f873-140">Ottimizzazione di hello tooget ordine, prima di aggiornare toohello supportata più recente versione, a partire da luglio 2017, ovvero:</span><span class="sxs-lookup"><span data-stu-id="3f873-140">In order tooget hello optimization, first update toohello latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
<span data-ttu-id="3f873-141">Al termine dell'aggiornamento di hello, installare hello più recente Linux Integration Services (LIS).</span><span class="sxs-lookup"><span data-stu-id="3f873-141">After hello update is complete, install hello latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="3f873-142">ottimizzazione della velocità effettiva di Hello è LIS, a partire da 4.2.</span><span class="sxs-lookup"><span data-stu-id="3f873-142">hello throughput optimization is in LIS, starting from 4.2.</span></span> <span data-ttu-id="3f873-143">Immettere hello toodownload i comandi seguenti e installarli:</span><span class="sxs-lookup"><span data-stu-id="3f873-143">Enter hello following commands toodownload and install LIS:</span></span>

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

<span data-ttu-id="3f873-144">Altre informazioni su Linux Integration Services versione 4.2 per Hyper-V visualizzando hello [pagina di download](https://www.microsoft.com/download/details.aspx?id=55106).</span><span class="sxs-lookup"><span data-stu-id="3f873-144">Learn more about Linux Integration Services Version 4.2 for Hyper-V by viewing hello [download page](https://www.microsoft.com/download/details.aspx?id=55106).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f873-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3f873-145">Next steps</span></span>
* <span data-ttu-id="3f873-146">Ora che hello VM è ottimizzato, vedere il risultato di hello con [della larghezza di banda/test della velocità effettiva macchina virtuale di Azure](virtual-network-bandwidth-testing.md) per lo scenario.</span><span class="sxs-lookup"><span data-stu-id="3f873-146">Now that hello VM is optimized, see hello result with [Bandwidth/Throughput testing Azure VM](virtual-network-bandwidth-testing.md) for your scenario.</span></span>
* <span data-ttu-id="3f873-147">Altre informazioni sono disponibili nell'articolo [Domande frequenti sulla rete virtuale di Azure](virtual-networks-faq.md).</span><span class="sxs-lookup"><span data-stu-id="3f873-147">Learn more with [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
