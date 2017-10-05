---
title: "Ottimizzare la velocità effettiva di rete della macchina virtuale | Documentazione Microsoft"
description: "Informazioni su come ottimizzare la velocità effettiva di rete della macchina virtuale di Azure."
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
ms.openlocfilehash: 914747983d4d974810836be66d6c6af343f58b60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a><span data-ttu-id="2bfab-103">Ottimizzare la velocità effettiva di rete per le macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="2bfab-103">Optimize network throughput for Azure virtual machines</span></span>

<span data-ttu-id="2bfab-104">Le macchine virtuali di Azure hanno impostazioni di rete predefinite che possono essere ottimizzate ulteriormente per una migliore velocità effettiva di rete.</span><span class="sxs-lookup"><span data-stu-id="2bfab-104">Azure virtual machines (VM) have default network settings that can be further optimized for network throughput.</span></span> <span data-ttu-id="2bfab-105">Questo articolo illustra come ottimizzare la velocità effettiva di rete per macchine virtuali Windows e Linux di Microsoft Azure, incluse le distribuzioni principali, ad esempio Ubuntu, CentOS e Red Hat.</span><span class="sxs-lookup"><span data-stu-id="2bfab-105">This article describes how to optimize network throughput for Microsoft Azure Windows and Linux VMs, including major distributions such as Ubuntu, CentOS and Red Hat.</span></span>

## <a name="windows-vm"></a><span data-ttu-id="2bfab-106">Macchina virtuale Windows</span><span class="sxs-lookup"><span data-stu-id="2bfab-106">Windows VM</span></span>

<span data-ttu-id="2bfab-107">Se la macchina virtuale di Windows è supportata da una [Rete accelerata](virtual-network-create-vm-accelerated-networking.md), abilitare tale funzionalità costituisce la configurazione ottimale per la velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="2bfab-107">If your Windows VM is supported with [Accelerated Networking](virtual-network-create-vm-accelerated-networking.md), enabling that feature would be the optimal configuration for throughput.</span></span> <span data-ttu-id="2bfab-108">Per tutte le altre macchine virtuali di Windows, tramite Receive-Side Scaling (RSS) esse possono raggiungere una velocità effettiva massima superiore rispetto a una VM senza RSS.</span><span class="sxs-lookup"><span data-stu-id="2bfab-108">For all other Windows VMs, using Receive Side Scaling (RSS) can reach higher maximal throughput than a VM without RSS.</span></span> <span data-ttu-id="2bfab-109">È possibile disabilitare RSS per impostazione predefinita in una macchina virtuale Windows.</span><span class="sxs-lookup"><span data-stu-id="2bfab-109">RSS may be disabled by default in a Windows VM.</span></span> <span data-ttu-id="2bfab-110">Completare la procedura seguente per determinare se RSS è abilitato e abilitarlo se è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="2bfab-110">Complete the following steps to determine whether RSS is enabled and to enable it if it's disabled.</span></span>

1. <span data-ttu-id="2bfab-111">Immettere il comando `Get-NetAdapterRss` di PowerShell per verificare se RSS è abilitato per una scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="2bfab-111">Enter the `Get-NetAdapterRss` PowerShell command to see if RSS is enabled for a network adapter.</span></span> <span data-ttu-id="2bfab-112">Nell'output di esempio seguente restituito da `Get-NetAdapterRss` RSS non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="2bfab-112">In the following example output returned from the `Get-NetAdapterRss`, RSS is not enabled.</span></span>

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. <span data-ttu-id="2bfab-113">Immettere il comando seguente per abilitare RSS:</span><span class="sxs-lookup"><span data-stu-id="2bfab-113">Enter the following command to enable RSS:</span></span>

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    <span data-ttu-id="2bfab-114">Il comando precedente non restituisce alcun output.</span><span class="sxs-lookup"><span data-stu-id="2bfab-114">The previous command does not have an output.</span></span> <span data-ttu-id="2bfab-115">Il comando ha modificato le impostazioni della scheda di interfaccia di rete, provocando la perdita di connettività temporanea per circa un minuto.</span><span class="sxs-lookup"><span data-stu-id="2bfab-115">The command changed NIC settings, causing temporary connectivity loss for about one minute.</span></span> <span data-ttu-id="2bfab-116">Durante la perdita di connettività viene visualizzata una finestra di dialogo di riconnessione.</span><span class="sxs-lookup"><span data-stu-id="2bfab-116">A Reconnecting dialog box appears during the connectivity loss.</span></span> <span data-ttu-id="2bfab-117">La connettività viene in genere ripristinata dopo il terzo tentativo.</span><span class="sxs-lookup"><span data-stu-id="2bfab-117">Connectivity is typically restored after the third attempt.</span></span>
3. <span data-ttu-id="2bfab-118">Verificare che RSS sia abilitato nella macchina virtuale immettendo di nuovo il comando `Get-NetAdapterRss`.</span><span class="sxs-lookup"><span data-stu-id="2bfab-118">Confirm that RSS is enabled in the VM by entering the `Get-NetAdapterRss` command again.</span></span> <span data-ttu-id="2bfab-119">Se l'esito è positivo, viene restituito l'output di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="2bfab-119">If successful, the following example output is returned:</span></span>

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a><span data-ttu-id="2bfab-120">VM Linux</span><span class="sxs-lookup"><span data-stu-id="2bfab-120">Linux VM</span></span>

<span data-ttu-id="2bfab-121">RSS è sempre abilitato per impostazione predefinita nella macchina virtuale Linux di Azure.</span><span class="sxs-lookup"><span data-stu-id="2bfab-121">RSS is always enabled by default in an Azure Linux VM.</span></span> <span data-ttu-id="2bfab-122">I kernel Linux rilasciati a partire da gennaio 2017 includono opzioni di ottimizzazione di rete che consentono a una macchina virtuale Linux di ottenere una velocità effettiva di rete superiore.</span><span class="sxs-lookup"><span data-stu-id="2bfab-122">Linux kernels released since January, 2017 include new network optimization options that enable a Linux VM to achieve higher network throughput.</span></span>

### <a name="ubuntu"></a><span data-ttu-id="2bfab-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="2bfab-123">Ubuntu</span></span>

<span data-ttu-id="2bfab-124">Per ottenere l'ottimizzazione, aggiornare prima di tutto la versione supportata più recente, a partire da giugno 2017, ovvero:</span><span class="sxs-lookup"><span data-stu-id="2bfab-124">In order to get the optimization, first update to the latest supported version, as of June 2017, which is:</span></span>
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
<span data-ttu-id="2bfab-125">Al termine dell'aggiornamento, immettere i comandi seguenti per ottenere il kernel più recente:</span><span class="sxs-lookup"><span data-stu-id="2bfab-125">After the update is complete, enter the following commands to get the latest kernel:</span></span>

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

<span data-ttu-id="2bfab-126">Comando facoltativo:</span><span class="sxs-lookup"><span data-stu-id="2bfab-126">Optional command:</span></span>

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a><span data-ttu-id="2bfab-127">Kernel Ubuntu Azure (anteprima)</span><span class="sxs-lookup"><span data-stu-id="2bfab-127">Ubuntu Azure Preview kernel</span></span>
> [!WARNING]
> <span data-ttu-id="2bfab-128">È possibile che il kernel Azure Linux (anteprima) non abbia lo stesso livello di disponibilità e affidabilità delle immagini e dei kernel del Marketplace disponibili a livello generale.</span><span class="sxs-lookup"><span data-stu-id="2bfab-128">This Azure Linux Preview kernel may not have the same level of availability and reliability as Marketplace images and kernels that are in general availability release.</span></span> <span data-ttu-id="2bfab-129">La funzionalità non è supportata, potrebbe avere funzioni vincolate e potrebbe non essere affidabile come il kernel predefinito.</span><span class="sxs-lookup"><span data-stu-id="2bfab-129">The feature is not supported, may have constrained capabilities, and may not be as reliable as the default kernel.</span></span> <span data-ttu-id="2bfab-130">Non usare questo kernel per carichi di lavoro di produzione.</span><span class="sxs-lookup"><span data-stu-id="2bfab-130">Do not use this kernel for production workloads.</span></span>

<span data-ttu-id="2bfab-131">È possibile ottenere prestazioni significative per la velocità effettiva installando il kernel Azure Linux proposto.</span><span class="sxs-lookup"><span data-stu-id="2bfab-131">Significant throughput performance can be achieved by installing the proposed Azure Linux kernel.</span></span> <span data-ttu-id="2bfab-132">Per provare a usare il kernel, aggiungere questa riga a /etc/apt/sources.list</span><span class="sxs-lookup"><span data-stu-id="2bfab-132">To try this kernel, add this line to /etc/apt/sources.list</span></span>

```bash
#add this to the end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

<span data-ttu-id="2bfab-133">Eseguire quindi questi comandi come radice.</span><span class="sxs-lookup"><span data-stu-id="2bfab-133">Then run these commands as root.</span></span>
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a><span data-ttu-id="2bfab-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="2bfab-134">CentOS</span></span>

<span data-ttu-id="2bfab-135">Per ottenere l'ottimizzazione, eseguire prima di tutto l'aggiornamento alla versione supportata più recente, a partire da luglio 2017, ovvero:</span><span class="sxs-lookup"><span data-stu-id="2bfab-135">In order to get the optimization, first update to the latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
<span data-ttu-id="2bfab-136">Al termine dell'aggiornamento, installare la versione più recente di Linux Integration Services (LIS).</span><span class="sxs-lookup"><span data-stu-id="2bfab-136">After the update is complete, install the latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="2bfab-137">L'ottimizzazione della velocità effettiva è disponibile in LIS a partire dalla versione 4.2.2-2.</span><span class="sxs-lookup"><span data-stu-id="2bfab-137">The throughput optimization is in LIS, starting from 4.2.2-2.</span></span> <span data-ttu-id="2bfab-138">Immettere i comandi seguenti per installare LIS:</span><span class="sxs-lookup"><span data-stu-id="2bfab-138">Enter the following commands to install LIS:</span></span>

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a><span data-ttu-id="2bfab-139">Red Hat</span><span class="sxs-lookup"><span data-stu-id="2bfab-139">Red Hat</span></span>

<span data-ttu-id="2bfab-140">Per ottenere l'ottimizzazione, eseguire prima di tutto l'aggiornamento alla versione supportata più recente, a partire da luglio 2017, ovvero:</span><span class="sxs-lookup"><span data-stu-id="2bfab-140">In order to get the optimization, first update to the latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
<span data-ttu-id="2bfab-141">Al termine dell'aggiornamento, installare la versione più recente di Linux Integration Services (LIS).</span><span class="sxs-lookup"><span data-stu-id="2bfab-141">After the update is complete, install the latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="2bfab-142">L'ottimizzazione della velocità effettiva è disponibile in LIS a partire dalla versione 4.2.</span><span class="sxs-lookup"><span data-stu-id="2bfab-142">The throughput optimization is in LIS, starting from 4.2.</span></span> <span data-ttu-id="2bfab-143">Immettere i comandi seguenti per scaricare e installare LIS:</span><span class="sxs-lookup"><span data-stu-id="2bfab-143">Enter the following commands to download and install LIS:</span></span>

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

<span data-ttu-id="2bfab-144">Per altre informazioni su Linux Integration Services versione 4.2 per Hyper-V, vedere la [pagina di download](https://www.microsoft.com/download/details.aspx?id=55106).</span><span class="sxs-lookup"><span data-stu-id="2bfab-144">Learn more about Linux Integration Services Version 4.2 for Hyper-V by viewing the [download page](https://www.microsoft.com/download/details.aspx?id=55106).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bfab-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2bfab-145">Next steps</span></span>
* <span data-ttu-id="2bfab-146">Dopo avere ottimizzato la VM, verificare il risultato con [Test della larghezza di banda/velocità effettiva della VM di Azure](virtual-network-bandwidth-testing.md) per lo scenario.</span><span class="sxs-lookup"><span data-stu-id="2bfab-146">Now that the VM is optimized, see the result with [Bandwidth/Throughput testing Azure VM](virtual-network-bandwidth-testing.md) for your scenario.</span></span>
* <span data-ttu-id="2bfab-147">Altre informazioni sono disponibili nell'articolo [Domande frequenti sulla rete virtuale di Azure](virtual-networks-faq.md).</span><span class="sxs-lookup"><span data-stu-id="2bfab-147">Learn more with [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
