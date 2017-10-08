---
title: Panoramica di agente VM Linux aaaAzure | Documenti Microsoft
description: Informazioni su come tooinstall e configurare l'agente Linux (waagent) toomanage l'interazione della macchina virtuale con il Controller di infrastruttura di Azure.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: e41de979-6d56-40b0-8916-895bf215ded6
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: szark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4e08c84d9205f4db7aae6fd1568ec1f15fba395c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-and-using-hello-azure-linux-agent"></a><span data-ttu-id="b1111-103">Comprensione e l'utilizzo di hello agente Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="b1111-103">Understanding and using hello Azure Linux Agent</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a><span data-ttu-id="b1111-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="b1111-104">Introduction</span></span>
<span data-ttu-id="b1111-105">Hello Microsoft agente Linux di Azure (waagent) gestisce Linux e FreeBSD provisioning e interazione di VM con hello Controller di infrastruttura di Azure.</span><span class="sxs-lookup"><span data-stu-id="b1111-105">hello Microsoft Azure Linux Agent (waagent) manages Linux & FreeBSD provisioning, and VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="b1111-106">Fornisce hello seguenti funzionalità per le distribuzioni di Linux e FreeBSD IaaS:</span><span class="sxs-lookup"><span data-stu-id="b1111-106">It provides hello following functionality for Linux and FreeBSD IaaS deployments:</span></span>

> [!NOTE]
> <span data-ttu-id="b1111-107">Vedere agente Linux di Azure hello [Leggimi](https://github.com/Azure/WALinuxAgent/blob/master/README.md) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="b1111-107">See hello Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) for additional details.</span></span>
> 
> 

* <span data-ttu-id="b1111-108">**Provisioning dell'immagine**</span><span class="sxs-lookup"><span data-stu-id="b1111-108">**Image Provisioning**</span></span>
  
  * <span data-ttu-id="b1111-109">Creazione di un account utente</span><span class="sxs-lookup"><span data-stu-id="b1111-109">Creation of a user account</span></span>
  * <span data-ttu-id="b1111-110">Configurazione dei tipi di autenticazione SSH</span><span class="sxs-lookup"><span data-stu-id="b1111-110">Configuring SSH authentication types</span></span>
  * <span data-ttu-id="b1111-111">Distribuzione di coppie di chiavi e chiavi pubbliche SSH</span><span class="sxs-lookup"><span data-stu-id="b1111-111">Deployment of SSH public keys and key pairs</span></span>
  * <span data-ttu-id="b1111-112">Nome dell'impostazione hello host</span><span class="sxs-lookup"><span data-stu-id="b1111-112">Setting hello host name</span></span>
  * <span data-ttu-id="b1111-113">Pubblicazione hello Nome toohello piattaforma host DNS</span><span class="sxs-lookup"><span data-stu-id="b1111-113">Publishing hello host name toohello platform DNS</span></span>
  * <span data-ttu-id="b1111-114">Piattaforma di toohello impronta digitale della chiave SSH host Reporting</span><span class="sxs-lookup"><span data-stu-id="b1111-114">Reporting SSH host key fingerprint toohello platform</span></span>
  * <span data-ttu-id="b1111-115">Gestione del disco risorse</span><span class="sxs-lookup"><span data-stu-id="b1111-115">Resource Disk Management</span></span>
  * <span data-ttu-id="b1111-116">Formattazione e quindi montare il disco di risorsa hello</span><span class="sxs-lookup"><span data-stu-id="b1111-116">Formatting and mounting hello resource disk</span></span>
  * <span data-ttu-id="b1111-117">Configurazione dell'area di swap</span><span class="sxs-lookup"><span data-stu-id="b1111-117">Configuring swap space</span></span>
* <span data-ttu-id="b1111-118">**Rete**</span><span class="sxs-lookup"><span data-stu-id="b1111-118">**Networking**</span></span>
  
  * <span data-ttu-id="b1111-119">Gestisce le route tooimprove compatibilità con i server DHCP di piattaforma</span><span class="sxs-lookup"><span data-stu-id="b1111-119">Manages routes tooimprove compatibility with platform DHCP servers</span></span>
  * <span data-ttu-id="b1111-120">Assicura la stabilità di hello del nome di interfaccia di rete hello</span><span class="sxs-lookup"><span data-stu-id="b1111-120">Ensures hello stability of hello network interface name</span></span>
* <span data-ttu-id="b1111-121">**Kernel**</span><span class="sxs-lookup"><span data-stu-id="b1111-121">**Kernel**</span></span>
  
  * <span data-ttu-id="b1111-122">Configura un NUMA virtuale (disabilitare per kernel <2.6.37)</span><span class="sxs-lookup"><span data-stu-id="b1111-122">Configures virtual NUMA (disable for kernel <2.6.37)</span></span>
  * <span data-ttu-id="b1111-123">Usa l'entropia Hyper-V per /dev/random</span><span class="sxs-lookup"><span data-stu-id="b1111-123">Consumes Hyper-V entropy for /dev/random</span></span>
  * <span data-ttu-id="b1111-124">Consente di configurare i timeout di SCSI per il dispositivo di primo livello hello (che può essere remoto)</span><span class="sxs-lookup"><span data-stu-id="b1111-124">Configures SCSI timeouts for hello root device (which could be remote)</span></span>
* <span data-ttu-id="b1111-125">**Diagnostica**</span><span class="sxs-lookup"><span data-stu-id="b1111-125">**Diagnostics**</span></span>
  
  * <span data-ttu-id="b1111-126">Porta seriale toohello il reindirizzamento della console</span><span class="sxs-lookup"><span data-stu-id="b1111-126">Console redirection toohello serial port</span></span>
* <span data-ttu-id="b1111-127">**Distribuzioni SCVMM**</span><span class="sxs-lookup"><span data-stu-id="b1111-127">**SCVMM Deployments**</span></span>
  
  * <span data-ttu-id="b1111-128">Rileva e avvia l'agente VMM hello per Linux durante l'esecuzione in un ambiente System Center Virtual Machine Manager 2012 R2</span><span class="sxs-lookup"><span data-stu-id="b1111-128">Detects and bootstraps hello VMM agent for Linux when running in a System Center Virtual Machine Manager 2012 R2 environment</span></span>
* <span data-ttu-id="b1111-129">**Estensione VM**</span><span class="sxs-lookup"><span data-stu-id="b1111-129">**VM Extension**</span></span>
  
  * <span data-ttu-id="b1111-130">Inserire i componenti creati da Microsoft e dai partner in automazione di software e la configurazione di tooenable VM Linux (IaaS)</span><span class="sxs-lookup"><span data-stu-id="b1111-130">Inject component authored by Microsoft and Partners into Linux VM (IaaS) tooenable software and configuration automation</span></span>
  * <span data-ttu-id="b1111-131">Implementazione di riferimento di estensione VM in [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span><span class="sxs-lookup"><span data-stu-id="b1111-131">VM Extension reference implementation on [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span></span>

## <a name="communication"></a><span data-ttu-id="b1111-132">Comunicazione</span><span class="sxs-lookup"><span data-stu-id="b1111-132">Communication</span></span>
<span data-ttu-id="b1111-133">flusso di informazioni Hello dall'agente di hello piattaforma toohello avviene tramite due canali:</span><span class="sxs-lookup"><span data-stu-id="b1111-133">hello information flow from hello platform toohello agent occurs via two channels:</span></span>

* <span data-ttu-id="b1111-134">Un DVD collegato in fase di avvio per le distribuzioni IaaS.</span><span class="sxs-lookup"><span data-stu-id="b1111-134">A boot-time attached DVD for IaaS deployments.</span></span> <span data-ttu-id="b1111-135">Il DVD include un file di configurazione conformi OVF che include tutte le informazioni di provisioning diverso da coppie di chiavi SSH effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="b1111-135">This DVD includes an OVF-compliant configuration file that includes all provisioning information other than hello actual SSH keypairs.</span></span>
* <span data-ttu-id="b1111-136">Un endpoint TCP espone un'API REST utilizzato tooobtain distribuzione e configurazione della topologia.</span><span class="sxs-lookup"><span data-stu-id="b1111-136">A TCP endpoint exposing a REST API used tooobtain deployment and topology configuration.</span></span>

## <a name="requirements"></a><span data-ttu-id="b1111-137">Requisiti</span><span class="sxs-lookup"><span data-stu-id="b1111-137">Requirements</span></span>
<span data-ttu-id="b1111-138">Hello sistemi seguenti sono stati testati e sono note toowork con hello agente Linux di Azure:</span><span class="sxs-lookup"><span data-stu-id="b1111-138">hello following systems have been tested and are known toowork with hello Azure Linux Agent:</span></span>

> [!NOTE]
> <span data-ttu-id="b1111-139">Questo elenco può differire dall'elenco ufficiale di hello dei sistemi supportati nella piattaforma Microsoft Azure, hello, come descritto qui: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span><span class="sxs-lookup"><span data-stu-id="b1111-139">This list may differ from hello official list of supported systems on hello Microsoft Azure Platform, as described here: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span></span>
> 
> 

* <span data-ttu-id="b1111-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b1111-140">CoreOS</span></span>
* <span data-ttu-id="b1111-141">CentOS 6.3+</span><span class="sxs-lookup"><span data-stu-id="b1111-141">CentOS 6.3+</span></span>
* <span data-ttu-id="b1111-142">Red Hat Enterprise Linux 6.7+</span><span class="sxs-lookup"><span data-stu-id="b1111-142">Red Hat Enterprise Linux 6.7+</span></span>
* <span data-ttu-id="b1111-143">Debian 7.0+</span><span class="sxs-lookup"><span data-stu-id="b1111-143">Debian 7.0+</span></span>
* <span data-ttu-id="b1111-144">Ubuntu 12.04+</span><span class="sxs-lookup"><span data-stu-id="b1111-144">Ubuntu 12.04+</span></span>
* <span data-ttu-id="b1111-145">openSUSE 12.3+</span><span class="sxs-lookup"><span data-stu-id="b1111-145">openSUSE 12.3+</span></span>
* <span data-ttu-id="b1111-146">SLES 11 SP3+</span><span class="sxs-lookup"><span data-stu-id="b1111-146">SLES 11 SP3+</span></span>
* <span data-ttu-id="b1111-147">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="b1111-147">Oracle Linux 6.4+</span></span>

<span data-ttu-id="b1111-148">Altri sistemi supportati:</span><span class="sxs-lookup"><span data-stu-id="b1111-148">Other Supported Systems:</span></span>

* <span data-ttu-id="b1111-149">FreeBSD 10+ (agente Linux di Azure v2.0.10+)</span><span class="sxs-lookup"><span data-stu-id="b1111-149">FreeBSD 10+ (Azure Linux Agent v2.0.10+)</span></span>

<span data-ttu-id="b1111-150">agente Linux di Hello dipende da alcuni pacchetti di sistema in ordine toofunction correttamente:</span><span class="sxs-lookup"><span data-stu-id="b1111-150">hello Linux agent depends on some system packages in order toofunction properly:</span></span>

* <span data-ttu-id="b1111-151">Python 2.6+</span><span class="sxs-lookup"><span data-stu-id="b1111-151">Python 2.6+</span></span>
* <span data-ttu-id="b1111-152">OpenSSL 1.0+</span><span class="sxs-lookup"><span data-stu-id="b1111-152">OpenSSL 1.0+</span></span>
* <span data-ttu-id="b1111-153">OpenSSH 5.3+</span><span class="sxs-lookup"><span data-stu-id="b1111-153">OpenSSH 5.3+</span></span>
* <span data-ttu-id="b1111-154">Utilità file system: sfdisk, fdisk, mkfs, separate</span><span class="sxs-lookup"><span data-stu-id="b1111-154">Filesystem utilities: sfdisk, fdisk, mkfs, parted</span></span>
* <span data-ttu-id="b1111-155">Strumenti password: chpasswd, sudo</span><span class="sxs-lookup"><span data-stu-id="b1111-155">Password tools: chpasswd, sudo</span></span>
* <span data-ttu-id="b1111-156">Strumenti di elaborazione testo: sed, grep</span><span class="sxs-lookup"><span data-stu-id="b1111-156">Text processing tools: sed, grep</span></span>
* <span data-ttu-id="b1111-157">Strumenti di rete: ip-route</span><span class="sxs-lookup"><span data-stu-id="b1111-157">Network tools: ip-route</span></span>
* <span data-ttu-id="b1111-158">Supporto di kernel per l'installazione di file system UDF.</span><span class="sxs-lookup"><span data-stu-id="b1111-158">Kernel support for mounting UDF filesystems.</span></span>

## <a name="installation"></a><span data-ttu-id="b1111-159">Installazione</span><span class="sxs-lookup"><span data-stu-id="b1111-159">Installation</span></span>
<span data-ttu-id="b1111-160">Installazione utilizzando un RPM o un pacchetto DEB dal repository di pacchetti di distribuzione è il metodo di hello preferito di installazione e aggiornamento hello agente Linux di Azure.</span><span class="sxs-lookup"><span data-stu-id="b1111-160">Installation using an RPM or a DEB package from your distribution's package repository is hello preferred method of installing and upgrading hello Azure Linux Agent.</span></span> <span data-ttu-id="b1111-161">Hello tutti [approvate per i provider di distribuzione](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrare pacchetto dell'agente Linux di Azure hello in un repository e le immagini.</span><span class="sxs-lookup"><span data-stu-id="b1111-161">All hello [endorsed distribution providers](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrate hello Azure Linux agent package into their images and repositories.</span></span>

<span data-ttu-id="b1111-162">Consultare la documentazione di toohello in hello [repository agente Linux di Azure su GitHub](https://github.com/Azure/WALinuxAgent) per le opzioni di installazione avanzata, ad esempio l'installazione da posizioni di origine o toocustom o prefissi.</span><span class="sxs-lookup"><span data-stu-id="b1111-162">Refer toohello documentation in hello [Azure Linux Agent repo on GitHub](https://github.com/Azure/WALinuxAgent) for advanced installation options, such as installing from source or toocustom locations or prefixes.</span></span>

## <a name="command-line-options"></a><span data-ttu-id="b1111-163">Opzioni da riga di comando</span><span class="sxs-lookup"><span data-stu-id="b1111-163">Command Line Options</span></span>
### <a name="flags"></a><span data-ttu-id="b1111-164">Flag</span><span class="sxs-lookup"><span data-stu-id="b1111-164">Flags</span></span>
* <span data-ttu-id="b1111-165">verbose: aumenta il livello di dettaglio del comando specificato</span><span class="sxs-lookup"><span data-stu-id="b1111-165">verbose: Increase verbosity of specified command</span></span>
* <span data-ttu-id="b1111-166">force: ignora la conferma interattiva per determinati comandi</span><span class="sxs-lookup"><span data-stu-id="b1111-166">force: Skip interactive confirmation for some commands</span></span>

### <a name="commands"></a><span data-ttu-id="b1111-167">Comandi:</span><span class="sxs-lookup"><span data-stu-id="b1111-167">Commands</span></span>
* <span data-ttu-id="b1111-168">Guida in linea: Elenca i flag e i comandi di hello è supportato.</span><span class="sxs-lookup"><span data-stu-id="b1111-168">help: Lists hello supported commands and flags.</span></span>
* <span data-ttu-id="b1111-169">deprovisioning: tentativo sistema hello tooclean e renderlo idoneo per il nuovo provisioning.</span><span class="sxs-lookup"><span data-stu-id="b1111-169">deprovision: Attempt tooclean hello system and make it suitable for re-provisioning.</span></span> <span data-ttu-id="b1111-170">Questa operazione eliminati seguente hello:</span><span class="sxs-lookup"><span data-stu-id="b1111-170">This operation deleted hello following:</span></span>
  
  * <span data-ttu-id="b1111-171">Tutte le chiavi host SSH (se Provisioning.RegenerateSshHostKeyPair 'y' nel file di configurazione hello)</span><span class="sxs-lookup"><span data-stu-id="b1111-171">All SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="b1111-172">Configurazione NameServer in /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="b1111-172">Nameserver configuration in /etc/resolv.conf</span></span>
  * <span data-ttu-id="b1111-173">Password radice da /etc/shadow. (se Provisioning.DeleteRootPassword 'y' nel file di configurazione hello)</span><span class="sxs-lookup"><span data-stu-id="b1111-173">Root password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="b1111-174">Lease client DHCP memorizzati nella cache</span><span class="sxs-lookup"><span data-stu-id="b1111-174">Cached DHCP client leases</span></span>
  * <span data-ttu-id="b1111-175">Reimposta host toolocalhost.localdomain nome</span><span class="sxs-lookup"><span data-stu-id="b1111-175">Resets host name toolocalhost.localdomain</span></span>

> [!WARNING]
> <span data-ttu-id="b1111-176">Deprovisioning non garantisce che l'immagine hello è deselezionata di tutte le informazioni riservate e adatto per la ridistribuzione.</span><span class="sxs-lookup"><span data-stu-id="b1111-176">Deprovisioning does not guarantee that hello image is cleared of all sensitive information and suitable for redistribution.</span></span>
> 
> 

* <span data-ttu-id="b1111-177">deprovisioning + utente: consente di eseguire tutto - deprovisioning (sopra) e anche Elimina account provisioning utente ultimo hello (ottenuto dal /var/lib/waagent) e i dati associati.</span><span class="sxs-lookup"><span data-stu-id="b1111-177">deprovision+user: Performs everything under -deprovision (above) and also deletes hello last provisioned user account (obtained from /var/lib/waagent) and associated data.</span></span> <span data-ttu-id="b1111-178">Questo parametro viene usato per il deprovisioning di un'immagine precedentemente sottoposta a provisioning in Azure in modo che possa essere acquisita e riutilizzata.</span><span class="sxs-lookup"><span data-stu-id="b1111-178">This parameter is when de-provisioning an image that was previously provisioning on Azure so it may be captured and re-used.</span></span>
* <span data-ttu-id="b1111-179">versione: Visualizza la versione di hello del comando waagent</span><span class="sxs-lookup"><span data-stu-id="b1111-179">version: Displays hello version of waagent</span></span>
* <span data-ttu-id="b1111-180">serialconsole: Configura GRUB toomark ttyS0 (hello prima porta seriale) come console di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="b1111-180">serialconsole: Configures GRUB toomark ttyS0 (hello first serial port) as hello boot console.</span></span> <span data-ttu-id="b1111-181">Ciò garantisce che i log di avvio del kernel siano inviati toothe della porta seriale e resi disponibili per il debug.</span><span class="sxs-lookup"><span data-stu-id="b1111-181">This ensures that kernel bootup logs are sent toothe serial port and made available for debugging.</span></span>
* <span data-ttu-id="b1111-182">daemon: runas waagent un'interazione toomanage daemon con piattaforma hello.</span><span class="sxs-lookup"><span data-stu-id="b1111-182">daemon: Run waagent as a daemon toomanage interaction with hello platform.</span></span> <span data-ttu-id="b1111-183">Questo argomento è toowaagent specificato nello script di inizializzazione waagent hello.</span><span class="sxs-lookup"><span data-stu-id="b1111-183">This argument is specified toowaagent in hello waagent init script.</span></span>
* <span data-ttu-id="b1111-184">start: esegue waagent come processo in background</span><span class="sxs-lookup"><span data-stu-id="b1111-184">start: Run waagent as a background process</span></span>

## <a name="configuration"></a><span data-ttu-id="b1111-185">Configurazione</span><span class="sxs-lookup"><span data-stu-id="b1111-185">Configuration</span></span>
<span data-ttu-id="b1111-186">Un file di configurazione (/ etc/waagent.conf) controlli hello azioni di comando waagent.</span><span class="sxs-lookup"><span data-stu-id="b1111-186">A configuration file (/etc/waagent.conf) controls hello actions of waagent.</span></span> <span data-ttu-id="b1111-187">Di seguito è riportato un file di configurazione di esempio:</span><span class="sxs-lookup"><span data-stu-id="b1111-187">A sample configuration file is shown below:</span></span>

    Provisioning.Enabled=y
    Provisioning.DeleteRootPassword=n
    Provisioning.RegenerateSshHostKeyPair=y
    Provisioning.SshHostKeyPairType=rsa
    Provisioning.MonitorHostName=y
    Provisioning.DecodeCustomData=n
    Provisioning.ExecuteCustomData=n
    Provisioning.PasswordCryptId=6
    Provisioning.PasswordCryptSaltLength=10
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.MountOptions=None
    ResourceDisk.EnableSwap=n
    ResourceDisk.SwapSizeMB=0
    LBProbeResponder=y
    Logs.Verbose=n
    OS.RootDeviceScsiTimeout=300
    OS.OpensslPath=None
    HttpProxy.Host=None
    HttpProxy.Port=None

<span data-ttu-id="b1111-188">Hello che varie opzioni di configurazione sono descritti in dettaglio di seguito.</span><span class="sxs-lookup"><span data-stu-id="b1111-188">hello various configuration options are described in detail below.</span></span> <span data-ttu-id="b1111-189">Le opzioni di configurazione sono di tre tipi: Boolean, String o Integer.</span><span class="sxs-lookup"><span data-stu-id="b1111-189">Configuration options are of three types; Boolean, String or Integer.</span></span> <span data-ttu-id="b1111-190">opzioni di configurazione booleano Hello possono essere specificate come "y" o "n".</span><span class="sxs-lookup"><span data-stu-id="b1111-190">hello Boolean configuration options can be specified as "y" or "n".</span></span> <span data-ttu-id="b1111-191">Hello parola chiave speciale "None" possono essere utilizzati per alcune stringa tipo voci di configurazione come descritto in dettaglio riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="b1111-191">hello special keyword "None" may be used for some string type configuration entries as detailed below.</span></span>

<span data-ttu-id="b1111-192">**Provisioning.Enabled:**</span><span class="sxs-lookup"><span data-stu-id="b1111-192">**Provisioning.Enabled:**</span></span>  
<span data-ttu-id="b1111-193">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="b1111-193">Type: Boolean</span></span>  
<span data-ttu-id="b1111-194">Predefinito: y</span><span class="sxs-lookup"><span data-stu-id="b1111-194">Default: y</span></span>

<span data-ttu-id="b1111-195">Questo consente hello utente tooenable o disabilitare il provisioning delle funzionalità nell'agente hello hello.</span><span class="sxs-lookup"><span data-stu-id="b1111-195">This allows hello user tooenable or disable hello provisioning functionality in hello agent.</span></span> <span data-ttu-id="b1111-196">I valori validi sono "y" o "n".</span><span class="sxs-lookup"><span data-stu-id="b1111-196">Valid values are "y" or "n".</span></span> <span data-ttu-id="b1111-197">Se il provisioning è disabilitato, le chiavi di host e dell'utente SSH nell'immagine hello vengono mantenute e viene ignorata qualsiasi configurazione specificata in hello Azure API di provisioning.</span><span class="sxs-lookup"><span data-stu-id="b1111-197">If provisioning is disabled, SSH host and user keys in hello image are preserved and any configuration specified in hello Azure provisioning API is ignored.</span></span>

> [!NOTE]
> <span data-ttu-id="b1111-198">Hello `Provisioning.Enabled` troppo "n" in Ubuntu Cloud immagini che utilizzano cloud-inizializzazione per il provisioning di valori predefiniti dei parametri.</span><span class="sxs-lookup"><span data-stu-id="b1111-198">hello `Provisioning.Enabled` parameter defaults too"n" on Ubuntu Cloud Images that use cloud-init for provisioning.</span></span>
> 
> 

<span data-ttu-id="b1111-199">**Provisioning.DeleteRootPassword:**</span><span class="sxs-lookup"><span data-stu-id="b1111-199">**Provisioning.DeleteRootPassword:**</span></span>  
<span data-ttu-id="b1111-200">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="b1111-200">Type: Boolean</span></span>  
<span data-ttu-id="b1111-201">Predefinito: n</span><span class="sxs-lookup"><span data-stu-id="b1111-201">Default: n</span></span>

<span data-ttu-id="b1111-202">Se set, la password radice hello nel file hello e così via/shadow vengono cancellati durante hello processo di provisioning.</span><span class="sxs-lookup"><span data-stu-id="b1111-202">If set, hello root password in hello /etc/shadow file is erased during hello provisioning process.</span></span>

<span data-ttu-id="b1111-203">**Provisioning.RegenerateSshHostKeyPair:**</span><span class="sxs-lookup"><span data-stu-id="b1111-203">**Provisioning.RegenerateSshHostKeyPair:**</span></span>  
<span data-ttu-id="b1111-204">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="b1111-204">Type: Boolean</span></span>  
<span data-ttu-id="b1111-205">Predefinito: y</span><span class="sxs-lookup"><span data-stu-id="b1111-205">Default: y</span></span>

<span data-ttu-id="b1111-206">Se impostato, tutti SSH host coppie di chiavi (ecdsa e dsa o rsa) viene eliminato durante hello da /etc/hosts ssh/processo di provisioning.</span><span class="sxs-lookup"><span data-stu-id="b1111-206">If set, all SSH host key pairs (ecdsa, dsa and rsa) are deleted during hello provisioning process from /etc/ssh/.</span></span> <span data-ttu-id="b1111-207">e viene generata un'unica coppia di chiavi aggiornata.</span><span class="sxs-lookup"><span data-stu-id="b1111-207">And a single fresh key pair is generated.</span></span>

<span data-ttu-id="b1111-208">tipo di crittografia Hello per hello nuova coppia di chiavi è configurabile hello Provisioning.SshHostKeyPairType voce.</span><span class="sxs-lookup"><span data-stu-id="b1111-208">hello encryption type for hello fresh key pair is configurable by hello Provisioning.SshHostKeyPairType entry.</span></span> <span data-ttu-id="b1111-209">Si noti che alcune distribuzioni creerà nuovamente le coppie di chiavi SSH per qualsiasi tipo di crittografia mancante quando si riavvia il daemon SSH hello (ad esempio, dopo un riavvio).</span><span class="sxs-lookup"><span data-stu-id="b1111-209">Please note that some distributions will re-create SSH key pairs for any missing encryption types when hello SSH daemon is restarted (for example, upon a reboot).</span></span>

<span data-ttu-id="b1111-210">**Provisioning.SshHostKeyPairType:**</span><span class="sxs-lookup"><span data-stu-id="b1111-210">**Provisioning.SshHostKeyPairType:**</span></span>  
<span data-ttu-id="b1111-211">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="b1111-211">Type: String</span></span>  
<span data-ttu-id="b1111-212">Predefinito: rsa</span><span class="sxs-lookup"><span data-stu-id="b1111-212">Default: rsa</span></span>

<span data-ttu-id="b1111-213">Tipo di algoritmo di crittografia tooan è supportato dal daemon SSH hello nella macchina virtuale hello può essere impostato.</span><span class="sxs-lookup"><span data-stu-id="b1111-213">This can be set tooan encryption algorithm type that is supported by hello SSH daemon on hello virtual machine.</span></span> <span data-ttu-id="b1111-214">i valori Hello in genere supportato sono "rsa", "dsa" e "ecdsa".</span><span class="sxs-lookup"><span data-stu-id="b1111-214">hello typically supported values are "rsa", "dsa" and "ecdsa".</span></span> <span data-ttu-id="b1111-215">Si noti che "putty.exe" in Windows non supporta il tipo "ecdsa".</span><span class="sxs-lookup"><span data-stu-id="b1111-215">Note that "putty.exe" on Windows does not support "ecdsa".</span></span> <span data-ttu-id="b1111-216">In tal caso, se si intende toouse putty.exe Windows tooconnect tooa distribuzione Linux, utilizzare "rsa" o "dsa".</span><span class="sxs-lookup"><span data-stu-id="b1111-216">So, if you intend toouse putty.exe on Windows tooconnect tooa Linux deployment, please use "rsa" or "dsa".</span></span>

<span data-ttu-id="b1111-217">**Provisioning.MonitorHostName:**</span><span class="sxs-lookup"><span data-stu-id="b1111-217">**Provisioning.MonitorHostName:**</span></span>  
<span data-ttu-id="b1111-218">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="b1111-218">Type: Boolean</span></span>  
<span data-ttu-id="b1111-219">Predefinito: y</span><span class="sxs-lookup"><span data-stu-id="b1111-219">Default: y</span></span>

<span data-ttu-id="b1111-220">Se impostato, waagent eseguito il monitoraggio macchina virtuale di Linux hello per le modifiche di nome host (come restituito dal comando "hostname" hello) e Aggiorna configurazione di rete hello nella modifica di hello immagine tooreflect hello.</span><span class="sxs-lookup"><span data-stu-id="b1111-220">If set, waagent will monitor hello Linux virtual machine for hostname changes (as returned by hello "hostname" command) and automatically update hello networking configuration in hello image tooreflect hello change.</span></span> <span data-ttu-id="b1111-221">In nome hello toopush modificare toohello i server DNS, rete verrà riavviata nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="b1111-221">In order toopush hello name change toohello DNS servers, networking will be restarted in hello virtual machine.</span></span> <span data-ttu-id="b1111-222">causando una breve interruzione nella connettività Internet.</span><span class="sxs-lookup"><span data-stu-id="b1111-222">This will result in brief loss of Internet connectivity.</span></span>

<span data-ttu-id="b1111-223">**Provisioning.DecodeCustomData**</span><span class="sxs-lookup"><span data-stu-id="b1111-223">**Provisioning.DecodeCustomData**</span></span>  
<span data-ttu-id="b1111-224">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="b1111-224">Type: Boolean</span></span>  
<span data-ttu-id="b1111-225">Predefinito: n</span><span class="sxs-lookup"><span data-stu-id="b1111-225">Default: n</span></span>

<span data-ttu-id="b1111-226">Se impostato, waagent decodificherà CustomData da Base64.</span><span class="sxs-lookup"><span data-stu-id="b1111-226">If set, waagent will decode CustomData from Base64.</span></span>

<span data-ttu-id="b1111-227">**Provisioning.ExecuteCustomData**</span><span class="sxs-lookup"><span data-stu-id="b1111-227">**Provisioning.ExecuteCustomData**</span></span>  
<span data-ttu-id="b1111-228">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="b1111-228">Type: Boolean</span></span>  
<span data-ttu-id="b1111-229">Predefinito: n</span><span class="sxs-lookup"><span data-stu-id="b1111-229">Default: n</span></span>

<span data-ttu-id="b1111-230">Se impostato, waagent eseguirà CustomData dopo il provisioning.</span><span class="sxs-lookup"><span data-stu-id="b1111-230">If set, waagent will execute CustomData after provisioning.</span></span>

<span data-ttu-id="b1111-231">**Provisioning.PasswordCryptId**</span><span class="sxs-lookup"><span data-stu-id="b1111-231">**Provisioning.PasswordCryptId**</span></span>  
<span data-ttu-id="b1111-232">Tipo: stringa</span><span class="sxs-lookup"><span data-stu-id="b1111-232">Type:String</span></span>  
<span data-ttu-id="b1111-233">Predefinito: 6</span><span class="sxs-lookup"><span data-stu-id="b1111-233">Default:6</span></span>

<span data-ttu-id="b1111-234">Algoritmo usato dalla crittografia durante la generazione di hash della password.</span><span class="sxs-lookup"><span data-stu-id="b1111-234">Algorithm used by crypt when generating password hash.</span></span>  
 <span data-ttu-id="b1111-235">1 - MD5</span><span class="sxs-lookup"><span data-stu-id="b1111-235">1 - MD5</span></span>  
 <span data-ttu-id="b1111-236">2a - Blowfish</span><span class="sxs-lookup"><span data-stu-id="b1111-236">2a - Blowfish</span></span>  
 <span data-ttu-id="b1111-237">5 - SHA-256</span><span class="sxs-lookup"><span data-stu-id="b1111-237">5 - SHA-256</span></span>  
 <span data-ttu-id="b1111-238">6 - SHA-512</span><span class="sxs-lookup"><span data-stu-id="b1111-238">6 - SHA-512</span></span>  

<span data-ttu-id="b1111-239">**Provisioning.PasswordCryptSaltLength**</span><span class="sxs-lookup"><span data-stu-id="b1111-239">**Provisioning.PasswordCryptSaltLength**</span></span>  
<span data-ttu-id="b1111-240">Tipo: stringa</span><span class="sxs-lookup"><span data-stu-id="b1111-240">Type:String</span></span>  
<span data-ttu-id="b1111-241">Predefinito: 10</span><span class="sxs-lookup"><span data-stu-id="b1111-241">Default:10</span></span>

<span data-ttu-id="b1111-242">Lunghezza di salt casuale usata durante la generazione di hash della password.</span><span class="sxs-lookup"><span data-stu-id="b1111-242">Length of random salt used when generating password hash.</span></span>

<span data-ttu-id="b1111-243">**ResourceDisk.Format:**</span><span class="sxs-lookup"><span data-stu-id="b1111-243">**ResourceDisk.Format:**</span></span>  
<span data-ttu-id="b1111-244">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="b1111-244">Type: Boolean</span></span>  
<span data-ttu-id="b1111-245">Predefinito: y</span><span class="sxs-lookup"><span data-stu-id="b1111-245">Default: y</span></span>

<span data-ttu-id="b1111-246">Se impostato, il disco di risorsa hello fornito dalla piattaforma hello verrà formattato e montato da waagent se il tipo di file System hello richiesto dall'utente hello in "ResourceDisk.Filesystem" è diverso da "ntfs".</span><span class="sxs-lookup"><span data-stu-id="b1111-246">If set, hello resource disk provided by hello platform will be formatted and mounted by waagent if hello filesystem type requested by hello user in "ResourceDisk.Filesystem" is anything other than "ntfs".</span></span> <span data-ttu-id="b1111-247">Una singola partizione di tipo Linux (83) verrà resa disponibile su disco hello.</span><span class="sxs-lookup"><span data-stu-id="b1111-247">A single partition of type Linux (83) will be made available on hello disk.</span></span> <span data-ttu-id="b1111-248">Si noti che la partizione non verrà formattata se è possibile montarla correttamente.</span><span class="sxs-lookup"><span data-stu-id="b1111-248">Note that this partition will not be formatted if it can be successfully mounted.</span></span>

<span data-ttu-id="b1111-249">**ResourceDisk.Filesystem:**</span><span class="sxs-lookup"><span data-stu-id="b1111-249">**ResourceDisk.Filesystem:**</span></span>  
<span data-ttu-id="b1111-250">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="b1111-250">Type: String</span></span>  
<span data-ttu-id="b1111-251">Predefinito: ext4</span><span class="sxs-lookup"><span data-stu-id="b1111-251">Default: ext4</span></span>

<span data-ttu-id="b1111-252">Specifica il tipo di file System hello per il disco di risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="b1111-252">This specifies hello filesystem type for hello resource disk.</span></span> <span data-ttu-id="b1111-253">I valori supportati variano in base alla distribuzione Linux.</span><span class="sxs-lookup"><span data-stu-id="b1111-253">Supported values vary by Linux distribution.</span></span> <span data-ttu-id="b1111-254">Se la stringa hello X, quindi mkfs. X devono essere presenti nell'immagine Linux hello.</span><span class="sxs-lookup"><span data-stu-id="b1111-254">If hello string is X, then mkfs.X should be present on hello Linux image.</span></span> <span data-ttu-id="b1111-255">Le immagini SLES 11 in genere utilizzano il valore 'ext3'.</span><span class="sxs-lookup"><span data-stu-id="b1111-255">SLES 11 images should typically use 'ext3'.</span></span> <span data-ttu-id="b1111-256">Le immagini FreeBSD in questo caso devono usare il valore 'ufs2'.</span><span class="sxs-lookup"><span data-stu-id="b1111-256">FreeBSD images should use 'ufs2' here.</span></span>

<span data-ttu-id="b1111-257">**ResourceDisk.MountPoint:**</span><span class="sxs-lookup"><span data-stu-id="b1111-257">**ResourceDisk.MountPoint:**</span></span>  
<span data-ttu-id="b1111-258">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="b1111-258">Type: String</span></span>  
<span data-ttu-id="b1111-259">Predefinito: /mnt/resource</span><span class="sxs-lookup"><span data-stu-id="b1111-259">Default: /mnt/resource</span></span> 

<span data-ttu-id="b1111-260">Specifica il percorso di hello in corrispondenza del quale è stato montato il disco di risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="b1111-260">This specifies hello path at which hello resource disk is mounted.</span></span> <span data-ttu-id="b1111-261">Si noti il disco di risorsa hello è un *temporaneo* del disco e può essere svuotata quando hello VM è deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="b1111-261">Note that hello resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span>

<span data-ttu-id="b1111-262">**ResourceDisk.MountOptions**</span><span class="sxs-lookup"><span data-stu-id="b1111-262">**ResourceDisk.MountOptions**</span></span>  
<span data-ttu-id="b1111-263">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="b1111-263">Type: String</span></span>  
<span data-ttu-id="b1111-264">Predefinito: nessuno</span><span class="sxs-lookup"><span data-stu-id="b1111-264">Default: None</span></span>

<span data-ttu-id="b1111-265">Specifica disco montaggio opzioni toobe passato toohello montaggio -o comando.</span><span class="sxs-lookup"><span data-stu-id="b1111-265">Specifies disk mount options toobe passed toohello mount -o command.</span></span> <span data-ttu-id="b1111-266">È un elenco di valori delimitato da virgole, ad esempio</span><span class="sxs-lookup"><span data-stu-id="b1111-266">This is a comma separated list of values, ex.</span></span> <span data-ttu-id="b1111-267">nodev,nosuid.</span><span class="sxs-lookup"><span data-stu-id="b1111-267">'nodev,nosuid'.</span></span> <span data-ttu-id="b1111-268">Vedere montaggio(8) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="b1111-268">See mount(8) for details.</span></span>

<span data-ttu-id="b1111-269">**ResourceDisk.EnableSwap:**</span><span class="sxs-lookup"><span data-stu-id="b1111-269">**ResourceDisk.EnableSwap:**</span></span>  
<span data-ttu-id="b1111-270">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="b1111-270">Type: Boolean</span></span>  
<span data-ttu-id="b1111-271">Predefinito: n</span><span class="sxs-lookup"><span data-stu-id="b1111-271">Default: n</span></span>

<span data-ttu-id="b1111-272">Se impostato, un file di swapping (o file di scambio) viene creato nel disco di risorsa hello e aggiungere spazio di swapping sistema toohello.</span><span class="sxs-lookup"><span data-stu-id="b1111-272">If set, a swap file (/swapfile) is created on hello resource disk and added toohello system swap space.</span></span>

<span data-ttu-id="b1111-273">**ResourceDisk.SwapSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="b1111-273">**ResourceDisk.SwapSizeMB:**</span></span>  
<span data-ttu-id="b1111-274">Tipo: numero intero</span><span class="sxs-lookup"><span data-stu-id="b1111-274">Type: Integer</span></span>  
<span data-ttu-id="b1111-275">Predefinito: 0</span><span class="sxs-lookup"><span data-stu-id="b1111-275">Default: 0</span></span>

<span data-ttu-id="b1111-276">dimensioni Hello del file di swapping hello in megabyte.</span><span class="sxs-lookup"><span data-stu-id="b1111-276">hello size of hello swap file in megabytes.</span></span>

<span data-ttu-id="b1111-277">**Logs.Verbose:**</span><span class="sxs-lookup"><span data-stu-id="b1111-277">**Logs.Verbose:**</span></span>  
<span data-ttu-id="b1111-278">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="b1111-278">Type: Boolean</span></span>  
<span data-ttu-id="b1111-279">Predefinito: n</span><span class="sxs-lookup"><span data-stu-id="b1111-279">Default: n</span></span>

<span data-ttu-id="b1111-280">Se questa voce è impostata, viene incrementato il livello di dettaglio del log.</span><span class="sxs-lookup"><span data-stu-id="b1111-280">If set, log verbosity is boosted.</span></span> <span data-ttu-id="b1111-281">Comando Waagent registra too/var/log/waagent.log e sfrutta hello sistema logrotate funzionalità toorotate log.</span><span class="sxs-lookup"><span data-stu-id="b1111-281">Waagent logs too/var/log/waagent.log and leverages hello system logrotate functionality toorotate logs.</span></span>

<span data-ttu-id="b1111-282">**OS.EnableRDMA**</span><span class="sxs-lookup"><span data-stu-id="b1111-282">**OS.EnableRDMA**</span></span>  
<span data-ttu-id="b1111-283">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="b1111-283">Type: Boolean</span></span>  
<span data-ttu-id="b1111-284">Predefinito: n</span><span class="sxs-lookup"><span data-stu-id="b1111-284">Default: n</span></span>

<span data-ttu-id="b1111-285">Se impostato, hello agente verrà tenta tooinstall e quindi caricare un driver del kernel RDMA corrispondente versione di hello del firmware hello in hello hardware sottostante.</span><span class="sxs-lookup"><span data-stu-id="b1111-285">If set, hello agent will attempt tooinstall and then load an RDMA kernel driver that matches hello version of hello firmware on hello underlying hardware.</span></span>

<span data-ttu-id="b1111-286">**OS.RootDeviceScsiTimeout:**</span><span class="sxs-lookup"><span data-stu-id="b1111-286">**OS.RootDeviceScsiTimeout:**</span></span>  
<span data-ttu-id="b1111-287">Tipo: numero intero</span><span class="sxs-lookup"><span data-stu-id="b1111-287">Type: Integer</span></span>  
<span data-ttu-id="b1111-288">Predefinito: 300</span><span class="sxs-lookup"><span data-stu-id="b1111-288">Default: 300</span></span>

<span data-ttu-id="b1111-289">Consente di configurare hello SCSI timeout in secondi in unità disco e i dati di hello del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="b1111-289">This configures hello SCSI timeout in seconds on hello OS disk and data drives.</span></span> <span data-ttu-id="b1111-290">Se non è impostato, il sistema hello vengono utilizzati valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="b1111-290">If not set, hello system defaults are used.</span></span>

<span data-ttu-id="b1111-291">**OS.OpensslPath:**</span><span class="sxs-lookup"><span data-stu-id="b1111-291">**OS.OpensslPath:**</span></span>  
<span data-ttu-id="b1111-292">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="b1111-292">Type: String</span></span>  
<span data-ttu-id="b1111-293">Predefinito: nessuno</span><span class="sxs-lookup"><span data-stu-id="b1111-293">Default: None</span></span>

<span data-ttu-id="b1111-294">Può essere utilizzato toospecify un percorso alternativo per toouse binario di openssl hello per le operazioni di crittografia.</span><span class="sxs-lookup"><span data-stu-id="b1111-294">This can be used toospecify an alternate path for hello openssl binary toouse for cryptographic operations.</span></span>

<span data-ttu-id="b1111-295">**HttpProxy.Host, HttpProxy.Port**</span><span class="sxs-lookup"><span data-stu-id="b1111-295">**HttpProxy.Host, HttpProxy.Port**</span></span>  
<span data-ttu-id="b1111-296">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="b1111-296">Type: String</span></span>  
<span data-ttu-id="b1111-297">Predefinito: nessuno</span><span class="sxs-lookup"><span data-stu-id="b1111-297">Default: None</span></span>

<span data-ttu-id="b1111-298">Se impostato, hello agente utilizzerà questo proxy server tooaccess hello internet.</span><span class="sxs-lookup"><span data-stu-id="b1111-298">If set, hello agent will use this proxy server tooaccess hello internet.</span></span> 

## <a name="ubuntu-cloud-images"></a><span data-ttu-id="b1111-299">Immagini di Ubuntu Cloud</span><span class="sxs-lookup"><span data-stu-id="b1111-299">Ubuntu Cloud Images</span></span>
<span data-ttu-id="b1111-300">Si noti che le immagini Cloud Ubuntu utilizzare [cloud init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform hello di molte attività di configurazione che, in caso contrario, viene gestita da agente Linux di Azure.</span><span class="sxs-lookup"><span data-stu-id="b1111-300">Note that Ubuntu Cloud Images utilize [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform many configuration tasks that would otherwise be managed by hello Azure Linux Agent.</span></span>  <span data-ttu-id="b1111-301">Si noti hello seguenti differenze:</span><span class="sxs-lookup"><span data-stu-id="b1111-301">Please note hello following differences:</span></span>

* <span data-ttu-id="b1111-302">**Provisioning.Enabled** troppo "n" in Ubuntu Cloud immagini che utilizzano cloud init tooperform provisioning attività predefinite.</span><span class="sxs-lookup"><span data-stu-id="b1111-302">**Provisioning.Enabled** defaults too"n" on Ubuntu Cloud Images that use cloud-init tooperform provisioning tasks.</span></span>
* <span data-ttu-id="b1111-303">Hello seguenti parametri di configurazione non hanno alcun effetto sulle immagini di Cloud Ubuntu che utilizzano cloud init toomanage hello risorsa spazio su disco e lo scambio:</span><span class="sxs-lookup"><span data-stu-id="b1111-303">hello following configuration parameters have no effect on Ubuntu Cloud Images that use cloud-init toomanage hello resource disk and swap space:</span></span>
  
  * <span data-ttu-id="b1111-304">**ResourceDisk.Format**</span><span class="sxs-lookup"><span data-stu-id="b1111-304">**ResourceDisk.Format**</span></span>
  * <span data-ttu-id="b1111-305">**ResourceDisk.Filesystem**</span><span class="sxs-lookup"><span data-stu-id="b1111-305">**ResourceDisk.Filesystem**</span></span>
  * <span data-ttu-id="b1111-306">**ResourceDisk.MountPoint**</span><span class="sxs-lookup"><span data-stu-id="b1111-306">**ResourceDisk.MountPoint**</span></span>
  * <span data-ttu-id="b1111-307">**ResourceDisk.EnableSwap**</span><span class="sxs-lookup"><span data-stu-id="b1111-307">**ResourceDisk.EnableSwap**</span></span>
  * <span data-ttu-id="b1111-308">**ResourceDisk.SwapSizeMB**</span><span class="sxs-lookup"><span data-stu-id="b1111-308">**ResourceDisk.SwapSizeMB**</span></span>
* <span data-ttu-id="b1111-309">Vedere hello dopo il punto di montaggio disco risorse tooconfigure hello risorse e scambiare spazio sulle immagini Cloud Ubuntu durante il provisioning:</span><span class="sxs-lookup"><span data-stu-id="b1111-309">Please see hello following resources tooconfigure hello resource disk mount point and swap space on Ubuntu Cloud Images during provisioning:</span></span>
  
  * [<span data-ttu-id="b1111-310">Ubuntu Wiki: Configurare partizioni di scambio</span><span class="sxs-lookup"><span data-stu-id="b1111-310">Ubuntu Wiki: Configure Swap Partitions</span></span>](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [<span data-ttu-id="b1111-311">Inserimento di dati personalizzati in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="b1111-311">Injecting Custom Data into an Azure Virtual Machine</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

