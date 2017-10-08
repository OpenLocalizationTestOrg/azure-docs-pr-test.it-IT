---
title: hello aaaUpdate agente Linux di Azure da GitHub | Documenti Microsoft
description: "Informazioni su come tooupdate agente Linux di Azure per le VM Linux nella versione più recente di Azure toohello da GitHub"
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
ms.openlocfilehash: 4ce7c56efc1e6563e6415f7687573f9fb9e7b4c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-hello-azure-linux-agent-on-a-vm"></a><span data-ttu-id="35046-103">Come tooupdate hello agente Linux di Azure in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="35046-103">How tooupdate hello Azure Linux Agent on a VM</span></span>

<span data-ttu-id="35046-104">tooupdate il [agente Linux di Azure](https://github.com/Azure/WALinuxAgent) in una VM Linux in Azure, è necessario disporre di:</span><span class="sxs-lookup"><span data-stu-id="35046-104">tooupdate your [Azure Linux Agent](https://github.com/Azure/WALinuxAgent) on a Linux VM in Azure, you must already have:</span></span>

- <span data-ttu-id="35046-105">Una VM Linux in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="35046-105">A running Linux VM in Azure.</span></span>
- <span data-ttu-id="35046-106">Una VM Linux di toothat connessione con SSH.</span><span class="sxs-lookup"><span data-stu-id="35046-106">A connection toothat Linux VM using SSH.</span></span>

<span data-ttu-id="35046-107">È sempre consigliabile ricercare innanzitutto un pacchetto nel repository di distribuzione di Linux hello.</span><span class="sxs-lookup"><span data-stu-id="35046-107">You should always check for a package in hello Linux distro repository first.</span></span> <span data-ttu-id="35046-108">È possibile pacchetto hello disponibile potrebbero non essere la versione più recente di hello, tuttavia, l'abilitazione degli aggiornamenti automatici garantisce hello agente Linux otterranno sempre l'aggiornamento più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="35046-108">It is possible hello package available may not be hello latest version, however, enabling autoupdate will ensure hello Linux Agent will always get hello latest update.</span></span> <span data-ttu-id="35046-109">Si devono avere problemi di installazione da gestori di pacchetti hello, è consigliabile rivolgersi supporto dal fornitore distro hello.</span><span class="sxs-lookup"><span data-stu-id="35046-109">Should you have issues installing from hello package managers, you should seek support from hello distro vendor.</span></span>

## <a name="updating-hello-azure-linux-agent"></a><span data-ttu-id="35046-110">Aggiornamento hello agente Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="35046-110">Updating hello Azure Linux Agent</span></span>

## <a name="ubuntu"></a><span data-ttu-id="35046-111">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="35046-111">Ubuntu</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="35046-112">Verificare la versione corrente del pacchetto</span><span class="sxs-lookup"><span data-stu-id="35046-112">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="35046-113">Aggiornare la cache del pacchetto</span><span class="sxs-lookup"><span data-stu-id="35046-113">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="35046-114">Installare una versione più recente del pacchetto hello</span><span class="sxs-lookup"><span data-stu-id="35046-114">Install hello latest package version</span></span>

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="35046-115">Verificare che la funzione di aggiornamento automatico sia abilitata</span><span class="sxs-lookup"><span data-stu-id="35046-115">Ensure auto update is enabled</span></span>

<span data-ttu-id="35046-116">Se è abilitato, verificare innanzitutto toosee:</span><span class="sxs-lookup"><span data-stu-id="35046-116">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="35046-117">Trovare "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="35046-117">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="35046-118">Se viene visualizzato questo output, la funzione è abilitata:</span><span class="sxs-lookup"><span data-stu-id="35046-118">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="35046-119">tooenable eseguire:</span><span class="sxs-lookup"><span data-stu-id="35046-119">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="35046-120">Riavviare il servizio di waagent hello</span><span class="sxs-lookup"><span data-stu-id="35046-120">Restart hello waagent service</span></span>

#### <a name="restart-agent-for-1404"></a><span data-ttu-id="35046-121">Riavviare l'agente per 14.04</span><span class="sxs-lookup"><span data-stu-id="35046-121">Restart agent for 14.04</span></span>

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a><span data-ttu-id="35046-122">Riavviare l'agente per 16.04 / 17.04</span><span class="sxs-lookup"><span data-stu-id="35046-122">Restart agent for 16.04 / 17.04</span></span>

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a><span data-ttu-id="35046-123">Debian</span><span class="sxs-lookup"><span data-stu-id="35046-123">Debian</span></span>

### <a name="debian-7-wheezy"></a><span data-ttu-id="35046-124">Debian 7 "Wheezy"</span><span class="sxs-lookup"><span data-stu-id="35046-124">Debian 7 “Wheezy”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="35046-125">Verificare la versione corrente del pacchetto</span><span class="sxs-lookup"><span data-stu-id="35046-125">Check your current package version</span></span>

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="35046-126">Aggiornare la cache del pacchetto</span><span class="sxs-lookup"><span data-stu-id="35046-126">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="35046-127">Installare una versione più recente del pacchetto hello</span><span class="sxs-lookup"><span data-stu-id="35046-127">Install hello latest package version</span></span>

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a><span data-ttu-id="35046-128">Abilitare l'aggiornamento automatico dell'agente</span><span class="sxs-lookup"><span data-stu-id="35046-128">Enable agent auto update</span></span>
<span data-ttu-id="35046-129">Per questa versione di Debian, che non ha una versione > = 2.0.16, la funzione di aggiornamento automatico non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="35046-129">This version of Debian does not have a version >= 2.0.16, therefore AutoUpdate is not available for it.</span></span> <span data-ttu-id="35046-130">output di Hello dalla hello sopra comando illustra se il pacchetto di hello è aggiornato.</span><span class="sxs-lookup"><span data-stu-id="35046-130">hello output from hello above command will show you if hello package is up-to-date.</span></span>

### <a name="debian-8-jessie--debian-9-stretch"></a><span data-ttu-id="35046-131">Debian 8 "Jessie" / Debian 9 "Stretch"</span><span class="sxs-lookup"><span data-stu-id="35046-131">Debian 8 “Jessie” / Debian 9 “Stretch”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="35046-132">Verificare la versione corrente del pacchetto</span><span class="sxs-lookup"><span data-stu-id="35046-132">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="35046-133">Aggiornare la cache del pacchetto</span><span class="sxs-lookup"><span data-stu-id="35046-133">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="35046-134">Installare una versione più recente del pacchetto hello</span><span class="sxs-lookup"><span data-stu-id="35046-134">Install hello latest package version</span></span>

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="35046-135">Verificare che la funzione di aggiornamento automatico sia abilitata</span><span class="sxs-lookup"><span data-stu-id="35046-135">Ensure auto update is enabled</span></span> 

<span data-ttu-id="35046-136">Se è abilitato, verificare innanzitutto toosee:</span><span class="sxs-lookup"><span data-stu-id="35046-136">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="35046-137">Trovare "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="35046-137">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="35046-138">Se viene visualizzato questo output, la funzione è abilitata:</span><span class="sxs-lookup"><span data-stu-id="35046-138">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="35046-139">tooenable eseguire:</span><span class="sxs-lookup"><span data-stu-id="35046-139">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="35046-140">Riavviare il servizio di waagent hello</span><span class="sxs-lookup"><span data-stu-id="35046-140">Restart hello waagent service</span></span>

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a><span data-ttu-id="35046-141">Redhat / CentOS</span><span class="sxs-lookup"><span data-stu-id="35046-141">Redhat / CentOS</span></span>

### <a name="rhelcentos-6"></a><span data-ttu-id="35046-142">RHEL/CentOS 6</span><span class="sxs-lookup"><span data-stu-id="35046-142">RHEL/CentOS 6</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="35046-143">Verificare la versione corrente del pacchetto</span><span class="sxs-lookup"><span data-stu-id="35046-143">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="35046-144">Verificare gli aggiornamenti disponibili</span><span class="sxs-lookup"><span data-stu-id="35046-144">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="35046-145">Installare una versione più recente del pacchetto hello</span><span class="sxs-lookup"><span data-stu-id="35046-145">Install hello latest package version</span></span>

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="35046-146">Verificare che la funzione di aggiornamento automatico sia abilitata</span><span class="sxs-lookup"><span data-stu-id="35046-146">Ensure auto update is enabled</span></span> 

<span data-ttu-id="35046-147">Se è abilitato, verificare innanzitutto toosee:</span><span class="sxs-lookup"><span data-stu-id="35046-147">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="35046-148">Trovare "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="35046-148">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="35046-149">Se viene visualizzato questo output, la funzione è abilitata:</span><span class="sxs-lookup"><span data-stu-id="35046-149">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="35046-150">tooenable eseguire:</span><span class="sxs-lookup"><span data-stu-id="35046-150">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="35046-151">Riavviare il servizio di waagent hello</span><span class="sxs-lookup"><span data-stu-id="35046-151">Restart hello waagent service</span></span>

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a><span data-ttu-id="35046-152">RHEL/CentOS 7</span><span class="sxs-lookup"><span data-stu-id="35046-152">RHEL/CentOS 7</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="35046-153">Verificare la versione corrente del pacchetto</span><span class="sxs-lookup"><span data-stu-id="35046-153">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="35046-154">Verificare gli aggiornamenti disponibili</span><span class="sxs-lookup"><span data-stu-id="35046-154">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="35046-155">Installare una versione più recente del pacchetto hello</span><span class="sxs-lookup"><span data-stu-id="35046-155">Install hello latest package version</span></span>

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="35046-156">Verificare che la funzione di aggiornamento automatico sia abilitata</span><span class="sxs-lookup"><span data-stu-id="35046-156">Ensure auto update is enabled</span></span> 

<span data-ttu-id="35046-157">Se è abilitato, verificare innanzitutto toosee:</span><span class="sxs-lookup"><span data-stu-id="35046-157">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="35046-158">Trovare "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="35046-158">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="35046-159">Se viene visualizzato questo output, la funzione è abilitata:</span><span class="sxs-lookup"><span data-stu-id="35046-159">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="35046-160">tooenable eseguire:</span><span class="sxs-lookup"><span data-stu-id="35046-160">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="35046-161">Riavviare il servizio di waagent hello</span><span class="sxs-lookup"><span data-stu-id="35046-161">Restart hello waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a><span data-ttu-id="35046-162">SUSE SLES</span><span class="sxs-lookup"><span data-stu-id="35046-162">SUSE SLES</span></span>

### <a name="suse-sles-11-sp4"></a><span data-ttu-id="35046-163">SUSE SLES 11 SP4</span><span class="sxs-lookup"><span data-stu-id="35046-163">SUSE SLES 11 SP4</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="35046-164">Verificare la versione corrente del pacchetto</span><span class="sxs-lookup"><span data-stu-id="35046-164">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="35046-165">Verificare gli aggiornamenti disponibili</span><span class="sxs-lookup"><span data-stu-id="35046-165">Check available updates</span></span>

<span data-ttu-id="35046-166">Hello sopra l'output viene visualizzato è se il pacchetto di hello backup toodate.</span><span class="sxs-lookup"><span data-stu-id="35046-166">hello above output will show you if hello package is up toodate.</span></span>

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="35046-167">Installare una versione più recente del pacchetto hello</span><span class="sxs-lookup"><span data-stu-id="35046-167">Install hello latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="35046-168">Verificare che la funzione di aggiornamento automatico sia abilitata</span><span class="sxs-lookup"><span data-stu-id="35046-168">Ensure auto update is enabled</span></span> 

<span data-ttu-id="35046-169">Se è abilitato, verificare innanzitutto toosee:</span><span class="sxs-lookup"><span data-stu-id="35046-169">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="35046-170">Trovare "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="35046-170">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="35046-171">Se viene visualizzato questo output, la funzione è abilitata:</span><span class="sxs-lookup"><span data-stu-id="35046-171">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="35046-172">tooenable eseguire:</span><span class="sxs-lookup"><span data-stu-id="35046-172">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="35046-173">Riavviare il servizio di waagent hello</span><span class="sxs-lookup"><span data-stu-id="35046-173">Restart hello waagent service</span></span>

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a><span data-ttu-id="35046-174">SUSE SLES 12 SP2</span><span class="sxs-lookup"><span data-stu-id="35046-174">SUSE SLES 12 SP2</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="35046-175">Verificare la versione corrente del pacchetto</span><span class="sxs-lookup"><span data-stu-id="35046-175">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="35046-176">Verificare gli aggiornamenti disponibili</span><span class="sxs-lookup"><span data-stu-id="35046-176">Check available updates</span></span>

<span data-ttu-id="35046-177">Nell'output di hello da hello precedente, verranno visualizzati è se il pacchetto di hello è aggiornata.</span><span class="sxs-lookup"><span data-stu-id="35046-177">In hello output from hello above, this will show you if hello package is upto date.</span></span>

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="35046-178">Installare una versione più recente del pacchetto hello</span><span class="sxs-lookup"><span data-stu-id="35046-178">Install hello latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="35046-179">Verificare che la funzione di aggiornamento automatico sia abilitata</span><span class="sxs-lookup"><span data-stu-id="35046-179">Ensure auto update is enabled</span></span> 

<span data-ttu-id="35046-180">Se è abilitato, verificare innanzitutto toosee:</span><span class="sxs-lookup"><span data-stu-id="35046-180">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="35046-181">Trovare "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="35046-181">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="35046-182">Se viene visualizzato questo output, la funzione è abilitata:</span><span class="sxs-lookup"><span data-stu-id="35046-182">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="35046-183">tooenable eseguire:</span><span class="sxs-lookup"><span data-stu-id="35046-183">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="35046-184">Riavviare il servizio di waagent hello</span><span class="sxs-lookup"><span data-stu-id="35046-184">Restart hello waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a><span data-ttu-id="35046-185">Oracle 6 e 7</span><span class="sxs-lookup"><span data-stu-id="35046-185">Oracle 6 and 7</span></span>

<span data-ttu-id="35046-186">Per Oracle Linux, assicurarsi che tale hello `Addons` repository è abilitato.</span><span class="sxs-lookup"><span data-stu-id="35046-186">For Oracle Linux, make sure that hello `Addons` repository is enabled.</span></span> <span data-ttu-id="35046-187">Scegliere file hello tooedit `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) o `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux) e modificare la riga hello `enabled=0` troppo`enabled=1` in **[ol6_addons]** o **[ol7_addons]** In questo file.</span><span class="sxs-lookup"><span data-stu-id="35046-187">Choose tooedit hello file `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), and change hello line `enabled=0` too`enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

<span data-ttu-id="35046-188">Quindi, tooinstall hello versione più recente di hello agente Linux di Azure, tipo:</span><span class="sxs-lookup"><span data-stu-id="35046-188">Then, tooinstall hello latest version of hello Azure Linux Agent, type:</span></span>

```bash
sudo yum install WALinuxAgent
```

<span data-ttu-id="35046-189">Se non si trova il repository di componente aggiuntivo hello è semplicemente possibile aggiungere queste righe alla fine del file .repo in base a versione Oracle Linux tooyour hello:</span><span class="sxs-lookup"><span data-stu-id="35046-189">If you don't find hello add-on repository you can simply add these lines at hello end of your .repo file according tooyour Oracle Linux release:</span></span>

<span data-ttu-id="35046-190">Per macchine virtuali Oracle Linux 6:</span><span class="sxs-lookup"><span data-stu-id="35046-190">For Oracle Linux 6 virtual machines:</span></span>

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

<span data-ttu-id="35046-191">Per macchine virtuali Oracle Linux 7:</span><span class="sxs-lookup"><span data-stu-id="35046-191">For Oracle Linux 7 virtual machines:</span></span>

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

<span data-ttu-id="35046-192">Quindi digitare:</span><span class="sxs-lookup"><span data-stu-id="35046-192">Then type:</span></span>

```bash
sudo yum update WALinuxAgent
```

<span data-ttu-id="35046-193">In genere è sufficiente, ma se per qualche motivo, che è necessario tooinstall da https://github.com direttamente, utilizzare hello seguendo i passaggi.</span><span class="sxs-lookup"><span data-stu-id="35046-193">Typically this is all you need, but if for some reason you need tooinstall it from https://github.com directly, use hello following steps.</span></span>


## <a name="update-hello-linux-agent-when-no-agent-package-exists-for-distribution"></a><span data-ttu-id="35046-194">Aggiornare l'agente Linux di hello quando è presente alcun pacchetto dell'agente per la distribuzione</span><span class="sxs-lookup"><span data-stu-id="35046-194">Update hello Linux Agent when no agent package exists for distribution</span></span>

<span data-ttu-id="35046-195">Installare wget (sono disponibili alcune distribuzioni che non installano per impostazione predefinita, ad esempio Oracle Linux, in CentOS e Red Hat versioni 6.4 e 6.5) digitando `sudo yum install wget` nella riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="35046-195">Install wget (there are some distros that don't install it by default, such as Redhat, CentOS, and Oracle Linux versions 6.4 and 6.5) by typing `sudo yum install wget` on hello command line.</span></span>

### <a name="1-download-hello-latest-version"></a><span data-ttu-id="35046-196">1. Scaricare la versione più recente di hello</span><span class="sxs-lookup"><span data-stu-id="35046-196">1. Download hello latest version</span></span>
<span data-ttu-id="35046-197">Aprire [hello versione dell'agente Linux di Azure in GitHub](https://github.com/Azure/WALinuxAgent/releases) in una pagina web e individuare il numero di versione più recente hello.</span><span class="sxs-lookup"><span data-stu-id="35046-197">Open [hello release of Azure Linux Agent in GitHub](https://github.com/Azure/WALinuxAgent/releases) in a web page, and find out hello latest version number.</span></span> <span data-ttu-id="35046-198">(È possibile individuare la versione corrente digitando `waagent --version`.)</span><span class="sxs-lookup"><span data-stu-id="35046-198">(You can locate your current version by typing `waagent --version`.)</span></span>

#### <a name="for-version-22x-or-later-type"></a><span data-ttu-id="35046-199">Per la versione 2.2.x o successiva, digitare:</span><span class="sxs-lookup"><span data-stu-id="35046-199">For version 2.2.x or later, type:</span></span>
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

<span data-ttu-id="35046-200">Hello riga seguente usa versione 2.2.0 ad esempio:</span><span class="sxs-lookup"><span data-stu-id="35046-200">hello following line uses version 2.2.0 as an example:</span></span>

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-hello-azure-linux-agent"></a><span data-ttu-id="35046-201">2. Installare hello agente Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="35046-201">2. Install hello Azure Linux Agent</span></span>

#### <a name="for-version-22x-use"></a><span data-ttu-id="35046-202">Per la versione 2.2.x, usare:</span><span class="sxs-lookup"><span data-stu-id="35046-202">For version 2.2.x, use:</span></span>
<span data-ttu-id="35046-203">Potrebbe essere necessario pacchetto hello tooinstall `setuptools` prima - [qui](https://pypi.python.org/pypi/setuptools).</span><span class="sxs-lookup"><span data-stu-id="35046-203">You may need tooinstall hello package `setuptools` first--see [here](https://pypi.python.org/pypi/setuptools).</span></span> <span data-ttu-id="35046-204">Quindi eseguire:</span><span class="sxs-lookup"><span data-stu-id="35046-204">Then run:</span></span>

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="35046-205">Verificare che la funzione di aggiornamento automatico sia abilitata</span><span class="sxs-lookup"><span data-stu-id="35046-205">Ensure auto update is enabled</span></span>

<span data-ttu-id="35046-206">Se è abilitato, verificare innanzitutto toosee:</span><span class="sxs-lookup"><span data-stu-id="35046-206">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="35046-207">Trovare "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="35046-207">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="35046-208">Se viene visualizzato questo output, la funzione è abilitata:</span><span class="sxs-lookup"><span data-stu-id="35046-208">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="35046-209">tooenable eseguire:</span><span class="sxs-lookup"><span data-stu-id="35046-209">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-hello-waagent-service"></a><span data-ttu-id="35046-210">3. Riavviare il servizio di waagent hello</span><span class="sxs-lookup"><span data-stu-id="35046-210">3. Restart hello waagent service</span></span>
<span data-ttu-id="35046-211">Per la maggior parte delle distribuzioni Linux:</span><span class="sxs-lookup"><span data-stu-id="35046-211">For most of Linux distros:</span></span>

```bash
sudo service waagent restart
```

<span data-ttu-id="35046-212">Per Ubuntu, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="35046-212">For Ubuntu, use:</span></span>

```bash
sudo service walinuxagent restart
```

<span data-ttu-id="35046-213">Per CoreOS, usare:</span><span class="sxs-lookup"><span data-stu-id="35046-213">For CoreOS, use:</span></span>

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-hello-azure-linux-agent-version"></a><span data-ttu-id="35046-214">4. Verificare hello agente Linux di Azure versione</span><span class="sxs-lookup"><span data-stu-id="35046-214">4. Confirm hello Azure Linux Agent version</span></span>
    
```bash
waagent -version
```

<span data-ttu-id="35046-215">Per CoreOS, hello sopra comando potrebbe non funzionare.</span><span class="sxs-lookup"><span data-stu-id="35046-215">For CoreOS, hello above command may not work.</span></span>

<span data-ttu-id="35046-216">Si noterà che hello agente Linux di Azure versione è stata aggiornata toohello nuova versione.</span><span class="sxs-lookup"><span data-stu-id="35046-216">You will see that hello Azure Linux Agent version has been updated toohello new version.</span></span>

<span data-ttu-id="35046-217">Per ulteriori informazioni sulla hello agente Linux di Azure, vedere [Leggimi agente Linux di Azure](https://github.com/Azure/WALinuxAgent).</span><span class="sxs-lookup"><span data-stu-id="35046-217">For more information regarding hello Azure Linux Agent, see [Azure Linux Agent README](https://github.com/Azure/WALinuxAgent).</span></span>
