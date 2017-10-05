---
title: Aggiornare l'agente Linux di Azure da Github | Microsoft Docs
description: Informazioni su come aggiornare all'ultima versione l'agente Linux di Azure per macchine virtuali Linux in Azure da GitHub
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: f1f19300-987d-4f29-9393-9aba866f049c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: mingzhan
ms.openlocfilehash: c79e37976a58ae5384b5856e0f7f258a773ef0fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-update-the-azure-linux-agent-on-a-vm"></a><span data-ttu-id="82259-103">Come aggiornare l'agente Linux di Azure in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="82259-103">How to update the Azure Linux Agent on a VM</span></span>

<span data-ttu-id="82259-104">Per aggiornare l' [agente Linux di Azure](https://github.com/Azure/WALinuxAgent) , su una VM Linux in Azure è necessario avere già:</span><span class="sxs-lookup"><span data-stu-id="82259-104">To update your [Azure Linux Agent](https://github.com/Azure/WALinuxAgent) on a Linux VM in Azure, you must already have:</span></span>

- <span data-ttu-id="82259-105">Una VM Linux in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="82259-105">A running Linux VM in Azure.</span></span>
- <span data-ttu-id="82259-106">Una connessione a tale VM Linux mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="82259-106">A connection to that Linux VM using SSH.</span></span>

<span data-ttu-id="82259-107">È sempre consigliabile cercare prima un pacchetto nel repository di distribuzione di Linux.</span><span class="sxs-lookup"><span data-stu-id="82259-107">You should always check for a package in the Linux distro repository first.</span></span> <span data-ttu-id="82259-108">È possibile che il pacchetto disponibile non sia la versione più recente; abilitando la funzione di aggiornamento automatico, si avrà la certezza di ottenere sempre la versione più recente dell'agente Linux.</span><span class="sxs-lookup"><span data-stu-id="82259-108">It is possible the package available may not be the latest version, however, enabling autoupdate will ensure the Linux Agent will always get the latest update.</span></span> <span data-ttu-id="82259-109">In caso di problemi durante l'installazione da Gestione pacchetti, è consigliabile rivolgersi al servizio di supporto del fornitore della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="82259-109">Should you have issues installing from the package managers, you should seek support from the distro vendor.</span></span>

## <a name="updating-the-azure-linux-agent"></a><span data-ttu-id="82259-110">Aggiornamento dell'agente Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="82259-110">Updating the Azure Linux Agent</span></span>

## <a name="ubuntu"></a><span data-ttu-id="82259-111">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="82259-111">Ubuntu</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="82259-112">Verificare la versione corrente del pacchetto</span><span class="sxs-lookup"><span data-stu-id="82259-112">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="82259-113">Aggiornare la cache del pacchetto</span><span class="sxs-lookup"><span data-stu-id="82259-113">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="82259-114">Installare la versione più recente del pacchetto</span><span class="sxs-lookup"><span data-stu-id="82259-114">Install the latest package version</span></span>

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="82259-115">Verificare che la funzione di aggiornamento automatico sia abilitata</span><span class="sxs-lookup"><span data-stu-id="82259-115">Ensure auto update is enabled</span></span>

<span data-ttu-id="82259-116">Per sapere se la funzione è abilitata:</span><span class="sxs-lookup"><span data-stu-id="82259-116">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="82259-117">Trovare "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="82259-117">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="82259-118">Se viene visualizzato questo output, la funzione è abilitata:</span><span class="sxs-lookup"><span data-stu-id="82259-118">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="82259-119">Per abilitarla, eseguire:</span><span class="sxs-lookup"><span data-stu-id="82259-119">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="82259-120">Riavviare il servizio waagent</span><span class="sxs-lookup"><span data-stu-id="82259-120">Restart the waagent service</span></span>

#### <a name="restart-agent-for-1404"></a><span data-ttu-id="82259-121">Riavviare l'agente per 14.04</span><span class="sxs-lookup"><span data-stu-id="82259-121">Restart agent for 14.04</span></span>

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a><span data-ttu-id="82259-122">Riavviare l'agente per 16.04 / 17.04</span><span class="sxs-lookup"><span data-stu-id="82259-122">Restart agent for 16.04 / 17.04</span></span>

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a><span data-ttu-id="82259-123">Debian</span><span class="sxs-lookup"><span data-stu-id="82259-123">Debian</span></span>

### <a name="debian-7-wheezy"></a><span data-ttu-id="82259-124">Debian 7 "Wheezy"</span><span class="sxs-lookup"><span data-stu-id="82259-124">Debian 7 “Wheezy”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="82259-125">Verificare la versione corrente del pacchetto</span><span class="sxs-lookup"><span data-stu-id="82259-125">Check your current package version</span></span>

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="82259-126">Aggiornare la cache del pacchetto</span><span class="sxs-lookup"><span data-stu-id="82259-126">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="82259-127">Installare la versione più recente del pacchetto</span><span class="sxs-lookup"><span data-stu-id="82259-127">Install the latest package version</span></span>

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a><span data-ttu-id="82259-128">Abilitare l'aggiornamento automatico dell'agente</span><span class="sxs-lookup"><span data-stu-id="82259-128">Enable agent auto update</span></span>
<span data-ttu-id="82259-129">Per questa versione di Debian, che non ha una versione > = 2.0.16, la funzione di aggiornamento automatico non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="82259-129">This version of Debian does not have a version >= 2.0.16, therefore AutoUpdate is not available for it.</span></span> <span data-ttu-id="82259-130">L'output del comando precedente consente di determinare se il pacchetto è aggiornato.</span><span class="sxs-lookup"><span data-stu-id="82259-130">The output from the above command will show you if the package is up-to-date.</span></span>

### <a name="debian-8-jessie--debian-9-stretch"></a><span data-ttu-id="82259-131">Debian 8 "Jessie" / Debian 9 "Stretch"</span><span class="sxs-lookup"><span data-stu-id="82259-131">Debian 8 “Jessie” / Debian 9 “Stretch”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="82259-132">Verificare la versione corrente del pacchetto</span><span class="sxs-lookup"><span data-stu-id="82259-132">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="82259-133">Aggiornare la cache del pacchetto</span><span class="sxs-lookup"><span data-stu-id="82259-133">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="82259-134">Installare la versione più recente del pacchetto</span><span class="sxs-lookup"><span data-stu-id="82259-134">Install the latest package version</span></span>

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="82259-135">Verificare che la funzione di aggiornamento automatico sia abilitata</span><span class="sxs-lookup"><span data-stu-id="82259-135">Ensure auto update is enabled</span></span> 

<span data-ttu-id="82259-136">Per sapere se la funzione è abilitata:</span><span class="sxs-lookup"><span data-stu-id="82259-136">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="82259-137">Trovare "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="82259-137">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="82259-138">Se viene visualizzato questo output, la funzione è abilitata:</span><span class="sxs-lookup"><span data-stu-id="82259-138">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="82259-139">Per abilitarla, eseguire:</span><span class="sxs-lookup"><span data-stu-id="82259-139">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="82259-140">Riavviare il servizio waagent</span><span class="sxs-lookup"><span data-stu-id="82259-140">Restart the waagent service</span></span>

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a><span data-ttu-id="82259-141">Redhat / CentOS</span><span class="sxs-lookup"><span data-stu-id="82259-141">Redhat / CentOS</span></span>

### <a name="rhelcentos-6"></a><span data-ttu-id="82259-142">RHEL/CentOS 6</span><span class="sxs-lookup"><span data-stu-id="82259-142">RHEL/CentOS 6</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="82259-143">Verificare la versione corrente del pacchetto</span><span class="sxs-lookup"><span data-stu-id="82259-143">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="82259-144">Verificare gli aggiornamenti disponibili</span><span class="sxs-lookup"><span data-stu-id="82259-144">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="82259-145">Installare la versione più recente del pacchetto</span><span class="sxs-lookup"><span data-stu-id="82259-145">Install the latest package version</span></span>

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="82259-146">Verificare che la funzione di aggiornamento automatico sia abilitata</span><span class="sxs-lookup"><span data-stu-id="82259-146">Ensure auto update is enabled</span></span> 

<span data-ttu-id="82259-147">Per sapere se la funzione è abilitata:</span><span class="sxs-lookup"><span data-stu-id="82259-147">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="82259-148">Trovare "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="82259-148">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="82259-149">Se viene visualizzato questo output, la funzione è abilitata:</span><span class="sxs-lookup"><span data-stu-id="82259-149">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="82259-150">Per abilitarla, eseguire:</span><span class="sxs-lookup"><span data-stu-id="82259-150">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="82259-151">Riavviare il servizio waagent</span><span class="sxs-lookup"><span data-stu-id="82259-151">Restart the waagent service</span></span>

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a><span data-ttu-id="82259-152">RHEL/CentOS 7</span><span class="sxs-lookup"><span data-stu-id="82259-152">RHEL/CentOS 7</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="82259-153">Verificare la versione corrente del pacchetto</span><span class="sxs-lookup"><span data-stu-id="82259-153">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="82259-154">Verificare gli aggiornamenti disponibili</span><span class="sxs-lookup"><span data-stu-id="82259-154">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="82259-155">Installare la versione più recente del pacchetto</span><span class="sxs-lookup"><span data-stu-id="82259-155">Install the latest package version</span></span>

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="82259-156">Verificare che la funzione di aggiornamento automatico sia abilitata</span><span class="sxs-lookup"><span data-stu-id="82259-156">Ensure auto update is enabled</span></span> 

<span data-ttu-id="82259-157">Per sapere se la funzione è abilitata:</span><span class="sxs-lookup"><span data-stu-id="82259-157">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="82259-158">Trovare "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="82259-158">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="82259-159">Se viene visualizzato questo output, la funzione è abilitata:</span><span class="sxs-lookup"><span data-stu-id="82259-159">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="82259-160">Per abilitarla, eseguire:</span><span class="sxs-lookup"><span data-stu-id="82259-160">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="82259-161">Riavviare il servizio waagent</span><span class="sxs-lookup"><span data-stu-id="82259-161">Restart the waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a><span data-ttu-id="82259-162">SUSE SLES</span><span class="sxs-lookup"><span data-stu-id="82259-162">SUSE SLES</span></span>

### <a name="suse-sles-11-sp4"></a><span data-ttu-id="82259-163">SUSE SLES 11 SP4</span><span class="sxs-lookup"><span data-stu-id="82259-163">SUSE SLES 11 SP4</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="82259-164">Verificare la versione corrente del pacchetto</span><span class="sxs-lookup"><span data-stu-id="82259-164">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="82259-165">Verificare gli aggiornamenti disponibili</span><span class="sxs-lookup"><span data-stu-id="82259-165">Check available updates</span></span>

<span data-ttu-id="82259-166">L'output sopra riportato consente di determinare se il pacchetto è aggiornato.</span><span class="sxs-lookup"><span data-stu-id="82259-166">The above output will show you if the package is up to date.</span></span>

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="82259-167">Installare la versione più recente del pacchetto</span><span class="sxs-lookup"><span data-stu-id="82259-167">Install the latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="82259-168">Verificare che la funzione di aggiornamento automatico sia abilitata</span><span class="sxs-lookup"><span data-stu-id="82259-168">Ensure auto update is enabled</span></span> 

<span data-ttu-id="82259-169">Per sapere se la funzione è abilitata:</span><span class="sxs-lookup"><span data-stu-id="82259-169">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="82259-170">Trovare "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="82259-170">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="82259-171">Se viene visualizzato questo output, la funzione è abilitata:</span><span class="sxs-lookup"><span data-stu-id="82259-171">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="82259-172">Per abilitarla, eseguire:</span><span class="sxs-lookup"><span data-stu-id="82259-172">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="82259-173">Riavviare il servizio waagent</span><span class="sxs-lookup"><span data-stu-id="82259-173">Restart the waagent service</span></span>

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a><span data-ttu-id="82259-174">SUSE SLES 12 SP2</span><span class="sxs-lookup"><span data-stu-id="82259-174">SUSE SLES 12 SP2</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="82259-175">Verificare la versione corrente del pacchetto</span><span class="sxs-lookup"><span data-stu-id="82259-175">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="82259-176">Verificare gli aggiornamenti disponibili</span><span class="sxs-lookup"><span data-stu-id="82259-176">Check available updates</span></span>

<span data-ttu-id="82259-177">L'output sopra riportato consente di determinare se il pacchetto è aggiornato.</span><span class="sxs-lookup"><span data-stu-id="82259-177">In the output from the above, this will show you if the package is upto date.</span></span>

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="82259-178">Installare la versione più recente del pacchetto</span><span class="sxs-lookup"><span data-stu-id="82259-178">Install the latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="82259-179">Verificare che la funzione di aggiornamento automatico sia abilitata</span><span class="sxs-lookup"><span data-stu-id="82259-179">Ensure auto update is enabled</span></span> 

<span data-ttu-id="82259-180">Per sapere se la funzione è abilitata:</span><span class="sxs-lookup"><span data-stu-id="82259-180">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="82259-181">Trovare "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="82259-181">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="82259-182">Se viene visualizzato questo output, la funzione è abilitata:</span><span class="sxs-lookup"><span data-stu-id="82259-182">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="82259-183">Per abilitarla, eseguire:</span><span class="sxs-lookup"><span data-stu-id="82259-183">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="82259-184">Riavviare il servizio waagent</span><span class="sxs-lookup"><span data-stu-id="82259-184">Restart the waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a><span data-ttu-id="82259-185">Oracle 6 e 7</span><span class="sxs-lookup"><span data-stu-id="82259-185">Oracle 6 and 7</span></span>

<span data-ttu-id="82259-186">Per Oracle Linux, verificare che il repository `Addons` sia abilitato.</span><span class="sxs-lookup"><span data-stu-id="82259-186">For Oracle Linux, make sure that the `Addons` repository is enabled.</span></span> <span data-ttu-id="82259-187">Scegliere di modificare il file `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) o `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux ) e la riga `enabled=0` in `enabled=1` sotto **[ol6_addons]** o **[ol7_addons]** in questo file.</span><span class="sxs-lookup"><span data-stu-id="82259-187">Choose to edit the file `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), and change the line `enabled=0` to `enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

<span data-ttu-id="82259-188">Installare quindi la versione più recente dell'agente Linux di Azure e digitare:</span><span class="sxs-lookup"><span data-stu-id="82259-188">Then, to install the latest version of the Azure Linux Agent, type:</span></span>

```bash
sudo yum install WALinuxAgent
```

<span data-ttu-id="82259-189">Se non si trova il repository del componente aggiuntivo, è possibile aggiungere le righe seguenti alla fine del file con estensione repo in base alla versione di Oracle Linux:</span><span class="sxs-lookup"><span data-stu-id="82259-189">If you don't find the add-on repository you can simply add these lines at the end of your .repo file according to your Oracle Linux release:</span></span>

<span data-ttu-id="82259-190">Per macchine virtuali Oracle Linux 6:</span><span class="sxs-lookup"><span data-stu-id="82259-190">For Oracle Linux 6 virtual machines:</span></span>

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

<span data-ttu-id="82259-191">Per macchine virtuali Oracle Linux 7:</span><span class="sxs-lookup"><span data-stu-id="82259-191">For Oracle Linux 7 virtual machines:</span></span>

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

<span data-ttu-id="82259-192">Quindi digitare:</span><span class="sxs-lookup"><span data-stu-id="82259-192">Then type:</span></span>

```bash
sudo yum update WALinuxAgent
```

<span data-ttu-id="82259-193">In genere è sufficiente, ma se per qualche motivo è necessario installarla da https://github.com direttamente, attenersi alla seguente procedura.</span><span class="sxs-lookup"><span data-stu-id="82259-193">Typically this is all you need, but if for some reason you need to install it from https://github.com directly, use the following steps.</span></span>


## <a name="update-the-linux-agent-when-no-agent-package-exists-for-distribution"></a><span data-ttu-id="82259-194">Aggiornare l'agente Linux se per la distribuzione non è presente alcun pacchetto agente</span><span class="sxs-lookup"><span data-stu-id="82259-194">Update the Linux Agent when no agent package exists for distribution</span></span>

<span data-ttu-id="82259-195">Installare wget (in alcune distribuzioni non viene installato per impostazione predefinita, ad esempio in Redhat, CentOS e Oracle Linux versione 6.4 e 6.5) digitando `sudo yum install wget` nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="82259-195">Install wget (there are some distros that don't install it by default, such as Redhat, CentOS, and Oracle Linux versions 6.4 and 6.5) by typing `sudo yum install wget` on the command line.</span></span>

### <a name="1-download-the-latest-version"></a><span data-ttu-id="82259-196">1. Scaricare la versione più recente</span><span class="sxs-lookup"><span data-stu-id="82259-196">1. Download the latest version</span></span>
<span data-ttu-id="82259-197">Aprire [la versione dell’agente Linux di Azure in Github](https://github.com/Azure/WALinuxAgent/releases) in una pagina Web e trovare il numero di versione più recente.</span><span class="sxs-lookup"><span data-stu-id="82259-197">Open [the release of Azure Linux Agent in GitHub](https://github.com/Azure/WALinuxAgent/releases) in a web page, and find out the latest version number.</span></span> <span data-ttu-id="82259-198">(È possibile individuare la versione corrente digitando `waagent --version`.)</span><span class="sxs-lookup"><span data-stu-id="82259-198">(You can locate your current version by typing `waagent --version`.)</span></span>

#### <a name="for-version-22x-or-later-type"></a><span data-ttu-id="82259-199">Per la versione 2.2.x o successiva, digitare:</span><span class="sxs-lookup"><span data-stu-id="82259-199">For version 2.2.x or later, type:</span></span>
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

<span data-ttu-id="82259-200">La riga seguente usa la versione 2.2.0 come esempio:</span><span class="sxs-lookup"><span data-stu-id="82259-200">The following line uses version 2.2.0 as an example:</span></span>

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-the-azure-linux-agent"></a><span data-ttu-id="82259-201">2. Installare l'agente Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="82259-201">2. Install the Azure Linux Agent</span></span>

#### <a name="for-version-22x-use"></a><span data-ttu-id="82259-202">Per la versione 2.2.x, usare:</span><span class="sxs-lookup"><span data-stu-id="82259-202">For version 2.2.x, use:</span></span>
<span data-ttu-id="82259-203">Potrebbe essere necessario installare prima il pacchetto `setuptools`. Vedere [qui](https://pypi.python.org/pypi/setuptools).</span><span class="sxs-lookup"><span data-stu-id="82259-203">You may need to install the package `setuptools` first--see [here](https://pypi.python.org/pypi/setuptools).</span></span> <span data-ttu-id="82259-204">Quindi eseguire:</span><span class="sxs-lookup"><span data-stu-id="82259-204">Then run:</span></span>

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="82259-205">Verificare che la funzione di aggiornamento automatico sia abilitata</span><span class="sxs-lookup"><span data-stu-id="82259-205">Ensure auto update is enabled</span></span>

<span data-ttu-id="82259-206">Per sapere se la funzione è abilitata:</span><span class="sxs-lookup"><span data-stu-id="82259-206">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="82259-207">Trovare "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="82259-207">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="82259-208">Se viene visualizzato questo output, la funzione è abilitata:</span><span class="sxs-lookup"><span data-stu-id="82259-208">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="82259-209">Per abilitarla, eseguire:</span><span class="sxs-lookup"><span data-stu-id="82259-209">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-the-waagent-service"></a><span data-ttu-id="82259-210">3. Riavviare il servizio waagent</span><span class="sxs-lookup"><span data-stu-id="82259-210">3. Restart the waagent service</span></span>
<span data-ttu-id="82259-211">Per la maggior parte delle distribuzioni Linux:</span><span class="sxs-lookup"><span data-stu-id="82259-211">For most of Linux distros:</span></span>

```bash
sudo service waagent restart
```

<span data-ttu-id="82259-212">Per Ubuntu, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="82259-212">For Ubuntu, use:</span></span>

```bash
sudo service walinuxagent restart
```

<span data-ttu-id="82259-213">Per CoreOS, usare:</span><span class="sxs-lookup"><span data-stu-id="82259-213">For CoreOS, use:</span></span>

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-the-azure-linux-agent-version"></a><span data-ttu-id="82259-214">4. Verificare la versione dell'agente Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="82259-214">4. Confirm the Azure Linux Agent version</span></span>
    
```bash
waagent -version
```

<span data-ttu-id="82259-215">Per CoreOS, il comando sopra riportato potrebbe non funzionare.</span><span class="sxs-lookup"><span data-stu-id="82259-215">For CoreOS, the above command may not work.</span></span>

<span data-ttu-id="82259-216">Si noterà che l'agente Linux di Azure è stato aggiornato alla nuova versione.</span><span class="sxs-lookup"><span data-stu-id="82259-216">You will see that the Azure Linux Agent version has been updated to the new version.</span></span>

<span data-ttu-id="82259-217">Per altre informazioni relative all'agente Linux di Azure, vedere [Azure Linux Agent README](https://github.com/Azure/WALinuxAgent).</span><span class="sxs-lookup"><span data-stu-id="82259-217">For more information regarding the Azure Linux Agent, see [Azure Linux Agent README](https://github.com/Azure/WALinuxAgent).</span></span>