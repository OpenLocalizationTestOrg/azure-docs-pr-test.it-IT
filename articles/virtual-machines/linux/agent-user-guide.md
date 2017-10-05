---
title: Panoramica dell'agente di VM Linux di Azure | Documentazione Microsoft
description: Informazioni su come installare e configurare l'agente Linux (waagent) per gestire l'interazione della macchina virtuale con il controller di infrastruttura di Azure.
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
ms.openlocfilehash: 486ad6bb148583a957fb82b7954ff94f853b12cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="understanding-and-using-the-azure-linux-agent"></a><span data-ttu-id="9b8f3-103">Informazioni e uso dell'agente Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="9b8f3-103">Understanding and using the Azure Linux Agent</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a><span data-ttu-id="9b8f3-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="9b8f3-104">Introduction</span></span>
<span data-ttu-id="9b8f3-105">L'agente Linux di Microsoft Azure (waagent) gestisce il provisioning di Linux e FreeBSD e l'interazione della macchina virtuale con il controller di infrastruttura di Azure.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-105">The Microsoft Azure Linux Agent (waagent) manages Linux & FreeBSD provisioning, and VM interaction with the Azure Fabric Controller.</span></span> <span data-ttu-id="9b8f3-106">Per le distribuzioni IaaS di Linux e FreeBSD, sono disponibili le funzionalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="9b8f3-106">It provides the following functionality for Linux and FreeBSD IaaS deployments:</span></span>

> [!NOTE]
> <span data-ttu-id="9b8f3-107">Vedere il file [LEGGIMI](https://github.com/Azure/WALinuxAgent/blob/master/README.md) dell'agente Linux di Azure per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-107">See the Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) for additional details.</span></span>
> 
> 

* <span data-ttu-id="9b8f3-108">**Provisioning dell'immagine**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-108">**Image Provisioning**</span></span>
  
  * <span data-ttu-id="9b8f3-109">Creazione di un account utente</span><span class="sxs-lookup"><span data-stu-id="9b8f3-109">Creation of a user account</span></span>
  * <span data-ttu-id="9b8f3-110">Configurazione dei tipi di autenticazione SSH</span><span class="sxs-lookup"><span data-stu-id="9b8f3-110">Configuring SSH authentication types</span></span>
  * <span data-ttu-id="9b8f3-111">Distribuzione di coppie di chiavi e chiavi pubbliche SSH</span><span class="sxs-lookup"><span data-stu-id="9b8f3-111">Deployment of SSH public keys and key pairs</span></span>
  * <span data-ttu-id="9b8f3-112">Impostazione del nome host</span><span class="sxs-lookup"><span data-stu-id="9b8f3-112">Setting the host name</span></span>
  * <span data-ttu-id="9b8f3-113">Pubblicazione del nome host nel DNS della piattaforma</span><span class="sxs-lookup"><span data-stu-id="9b8f3-113">Publishing the host name to the platform DNS</span></span>
  * <span data-ttu-id="9b8f3-114">Segnalazione dell'ID digitale della chiave dell'host SSH alla piattaforma</span><span class="sxs-lookup"><span data-stu-id="9b8f3-114">Reporting SSH host key fingerprint to the platform</span></span>
  * <span data-ttu-id="9b8f3-115">Gestione del disco risorse</span><span class="sxs-lookup"><span data-stu-id="9b8f3-115">Resource Disk Management</span></span>
  * <span data-ttu-id="9b8f3-116">Formattazione e montaggio del disco risorse</span><span class="sxs-lookup"><span data-stu-id="9b8f3-116">Formatting and mounting the resource disk</span></span>
  * <span data-ttu-id="9b8f3-117">Configurazione dell'area di swap</span><span class="sxs-lookup"><span data-stu-id="9b8f3-117">Configuring swap space</span></span>
* <span data-ttu-id="9b8f3-118">**Rete**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-118">**Networking**</span></span>
  
  * <span data-ttu-id="9b8f3-119">Gestisce i percorsi per migliorare la compatibilità con i server DHCP della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-119">Manages routes to improve compatibility with platform DHCP servers</span></span>
  * <span data-ttu-id="9b8f3-120">Garantisce la stabilità del nome dell'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="9b8f3-120">Ensures the stability of the network interface name</span></span>
* <span data-ttu-id="9b8f3-121">**Kernel**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-121">**Kernel**</span></span>
  
  * <span data-ttu-id="9b8f3-122">Configura un NUMA virtuale (disabilitare per kernel <2.6.37)</span><span class="sxs-lookup"><span data-stu-id="9b8f3-122">Configures virtual NUMA (disable for kernel <2.6.37)</span></span>
  * <span data-ttu-id="9b8f3-123">Usa l'entropia Hyper-V per /dev/random</span><span class="sxs-lookup"><span data-stu-id="9b8f3-123">Consumes Hyper-V entropy for /dev/random</span></span>
  * <span data-ttu-id="9b8f3-124">Configura i timeout SCSI per il dispositivo radice (che può essere remoto)</span><span class="sxs-lookup"><span data-stu-id="9b8f3-124">Configures SCSI timeouts for the root device (which could be remote)</span></span>
* <span data-ttu-id="9b8f3-125">**Diagnostica**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-125">**Diagnostics**</span></span>
  
  * <span data-ttu-id="9b8f3-126">Reindirizzamento della console alla porta seriale</span><span class="sxs-lookup"><span data-stu-id="9b8f3-126">Console redirection to the serial port</span></span>
* <span data-ttu-id="9b8f3-127">**Distribuzioni SCVMM**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-127">**SCVMM Deployments**</span></span>
  
  * <span data-ttu-id="9b8f3-128">Rileva e avvia l'agente VMM per Linux durante l'esecuzione in un ambiente System Center Virtual Machine Manager 2012 R2</span><span class="sxs-lookup"><span data-stu-id="9b8f3-128">Detects and bootstraps the VMM agent for Linux when running in a System Center Virtual Machine Manager 2012 R2 environment</span></span>
* <span data-ttu-id="9b8f3-129">**Estensione VM**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-129">**VM Extension**</span></span>
  
  * <span data-ttu-id="9b8f3-130">Inserire il componente creato da Microsoft e partner in VM Linux (IaaS) per attivare il software e l'automazione di configurazione</span><span class="sxs-lookup"><span data-stu-id="9b8f3-130">Inject component authored by Microsoft and Partners into Linux VM (IaaS) to enable software and configuration automation</span></span>
  * <span data-ttu-id="9b8f3-131">Implementazione di riferimento di estensione VM in [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span><span class="sxs-lookup"><span data-stu-id="9b8f3-131">VM Extension reference implementation on [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span></span>

## <a name="communication"></a><span data-ttu-id="9b8f3-132">Comunicazione</span><span class="sxs-lookup"><span data-stu-id="9b8f3-132">Communication</span></span>
<span data-ttu-id="9b8f3-133">Il flusso di informazioni dalla piattaforma all'agente avviene tramite due canali:</span><span class="sxs-lookup"><span data-stu-id="9b8f3-133">The information flow from the platform to the agent occurs via two channels:</span></span>

* <span data-ttu-id="9b8f3-134">Un DVD collegato in fase di avvio per le distribuzioni IaaS.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-134">A boot-time attached DVD for IaaS deployments.</span></span> <span data-ttu-id="9b8f3-135">Nel DVD è incluso un file di configurazione conforme a OVF che include tutte le informazioni di provisioning diverse dalle coppie di chiavi SSH effettive.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-135">This DVD includes an OVF-compliant configuration file that includes all provisioning information other than the actual SSH keypairs.</span></span>
* <span data-ttu-id="9b8f3-136">Un endpoint TCP che espone un'API REST usata per ottenere la configurazione della distribuzione e della topologia.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-136">A TCP endpoint exposing a REST API used to obtain deployment and topology configuration.</span></span>

## <a name="requirements"></a><span data-ttu-id="9b8f3-137">Requisiti</span><span class="sxs-lookup"><span data-stu-id="9b8f3-137">Requirements</span></span>
<span data-ttu-id="9b8f3-138">I sistemi seguenti sono stati testati e funzionano con l'agente Linux di Azure:</span><span class="sxs-lookup"><span data-stu-id="9b8f3-138">The following systems have been tested and are known to work with the Azure Linux Agent:</span></span>

> [!NOTE]
> <span data-ttu-id="9b8f3-139">È possibile che questo elenco sia diverso da quello ufficiale dei sistemi supportati sulla piattaforma Microsoft Azure, come descritto di seguito: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span><span class="sxs-lookup"><span data-stu-id="9b8f3-139">This list may differ from the official list of supported systems on the Microsoft Azure Platform, as described here: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span></span>
> 
> 

* <span data-ttu-id="9b8f3-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="9b8f3-140">CoreOS</span></span>
* <span data-ttu-id="9b8f3-141">CentOS 6.3+</span><span class="sxs-lookup"><span data-stu-id="9b8f3-141">CentOS 6.3+</span></span>
* <span data-ttu-id="9b8f3-142">Red Hat Enterprise Linux 6.7+</span><span class="sxs-lookup"><span data-stu-id="9b8f3-142">Red Hat Enterprise Linux 6.7+</span></span>
* <span data-ttu-id="9b8f3-143">Debian 7.0+</span><span class="sxs-lookup"><span data-stu-id="9b8f3-143">Debian 7.0+</span></span>
* <span data-ttu-id="9b8f3-144">Ubuntu 12.04+</span><span class="sxs-lookup"><span data-stu-id="9b8f3-144">Ubuntu 12.04+</span></span>
* <span data-ttu-id="9b8f3-145">openSUSE 12.3+</span><span class="sxs-lookup"><span data-stu-id="9b8f3-145">openSUSE 12.3+</span></span>
* <span data-ttu-id="9b8f3-146">SLES 11 SP3+</span><span class="sxs-lookup"><span data-stu-id="9b8f3-146">SLES 11 SP3+</span></span>
* <span data-ttu-id="9b8f3-147">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="9b8f3-147">Oracle Linux 6.4+</span></span>

<span data-ttu-id="9b8f3-148">Altri sistemi supportati:</span><span class="sxs-lookup"><span data-stu-id="9b8f3-148">Other Supported Systems:</span></span>

* <span data-ttu-id="9b8f3-149">FreeBSD 10+ (agente Linux di Azure v2.0.10+)</span><span class="sxs-lookup"><span data-stu-id="9b8f3-149">FreeBSD 10+ (Azure Linux Agent v2.0.10+)</span></span>

<span data-ttu-id="9b8f3-150">Per il corretto funzionamento dell'agente Linux sono necessari alcuni package di sistema:</span><span class="sxs-lookup"><span data-stu-id="9b8f3-150">The Linux agent depends on some system packages in order to function properly:</span></span>

* <span data-ttu-id="9b8f3-151">Python 2.6+</span><span class="sxs-lookup"><span data-stu-id="9b8f3-151">Python 2.6+</span></span>
* <span data-ttu-id="9b8f3-152">OpenSSL 1.0+</span><span class="sxs-lookup"><span data-stu-id="9b8f3-152">OpenSSL 1.0+</span></span>
* <span data-ttu-id="9b8f3-153">OpenSSH 5.3+</span><span class="sxs-lookup"><span data-stu-id="9b8f3-153">OpenSSH 5.3+</span></span>
* <span data-ttu-id="9b8f3-154">Utilità file system: sfdisk, fdisk, mkfs, separate</span><span class="sxs-lookup"><span data-stu-id="9b8f3-154">Filesystem utilities: sfdisk, fdisk, mkfs, parted</span></span>
* <span data-ttu-id="9b8f3-155">Strumenti password: chpasswd, sudo</span><span class="sxs-lookup"><span data-stu-id="9b8f3-155">Password tools: chpasswd, sudo</span></span>
* <span data-ttu-id="9b8f3-156">Strumenti di elaborazione testo: sed, grep</span><span class="sxs-lookup"><span data-stu-id="9b8f3-156">Text processing tools: sed, grep</span></span>
* <span data-ttu-id="9b8f3-157">Strumenti di rete: ip-route</span><span class="sxs-lookup"><span data-stu-id="9b8f3-157">Network tools: ip-route</span></span>
* <span data-ttu-id="9b8f3-158">Supporto di kernel per l'installazione di file system UDF.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-158">Kernel support for mounting UDF filesystems.</span></span>

## <a name="installation"></a><span data-ttu-id="9b8f3-159">Installazione</span><span class="sxs-lookup"><span data-stu-id="9b8f3-159">Installation</span></span>
<span data-ttu-id="9b8f3-160">Il metodo preferito per l'installazione e l'aggiornamento dell'agente Linux di Azure prevede l'installazione tramite un pacchetto RPM o DEB dal repository di pacchetti della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-160">Installation using an RPM or a DEB package from your distribution's package repository is the preferred method of installing and upgrading the Azure Linux Agent.</span></span> <span data-ttu-id="9b8f3-161">Tutti i [provider di distribuzione supportati](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrano il pacchetto agente Linux di Azure nelle immagini e nei repository.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-161">All the [endorsed distribution providers](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrate the Azure Linux agent package into their images and repositories.</span></span>

<span data-ttu-id="9b8f3-162">Leggere la documentazione nel [repository dell'agente Linux di Azure su GitHub](https://github.com/Azure/WALinuxAgent) per conoscere le opzioni di installazione avanzate, ad esempio l'installazione da origine o da percorsi personalizzati o prefissi.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-162">Refer to the documentation in the [Azure Linux Agent repo on GitHub](https://github.com/Azure/WALinuxAgent) for advanced installation options, such as installing from source or to custom locations or prefixes.</span></span>

## <a name="command-line-options"></a><span data-ttu-id="9b8f3-163">Opzioni da riga di comando</span><span class="sxs-lookup"><span data-stu-id="9b8f3-163">Command Line Options</span></span>
### <a name="flags"></a><span data-ttu-id="9b8f3-164">Flag</span><span class="sxs-lookup"><span data-stu-id="9b8f3-164">Flags</span></span>
* <span data-ttu-id="9b8f3-165">verbose: aumenta il livello di dettaglio del comando specificato</span><span class="sxs-lookup"><span data-stu-id="9b8f3-165">verbose: Increase verbosity of specified command</span></span>
* <span data-ttu-id="9b8f3-166">force: ignora la conferma interattiva per determinati comandi</span><span class="sxs-lookup"><span data-stu-id="9b8f3-166">force: Skip interactive confirmation for some commands</span></span>

### <a name="commands"></a><span data-ttu-id="9b8f3-167">Comandi:</span><span class="sxs-lookup"><span data-stu-id="9b8f3-167">Commands</span></span>
* <span data-ttu-id="9b8f3-168">help: elenca i flag e i comandi supportati.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-168">help: Lists the supported commands and flags.</span></span>
* <span data-ttu-id="9b8f3-169">deprovision: tenta di pulire il sistema per renderlo idoneo per un nuovo provisioning.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-169">deprovision: Attempt to clean the system and make it suitable for re-provisioning.</span></span> <span data-ttu-id="9b8f3-170">Questa operazione comporta l'eliminazione di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="9b8f3-170">This operation deleted the following:</span></span>
  
  * <span data-ttu-id="9b8f3-171">Tutte le chiavi host (se Provisioning.RegenerateSshHostKeyPair è 'y' nel file di configurazione)</span><span class="sxs-lookup"><span data-stu-id="9b8f3-171">All SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in the configuration file)</span></span>
  * <span data-ttu-id="9b8f3-172">Configurazione NameServer in /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="9b8f3-172">Nameserver configuration in /etc/resolv.conf</span></span>
  * <span data-ttu-id="9b8f3-173">Password radice da /etc/shadow (se Provisioning.DeleteRootPassword è 'y' nel file di configurazione)</span><span class="sxs-lookup"><span data-stu-id="9b8f3-173">Root password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in the configuration file)</span></span>
  * <span data-ttu-id="9b8f3-174">Lease client DHCP memorizzati nella cache</span><span class="sxs-lookup"><span data-stu-id="9b8f3-174">Cached DHCP client leases</span></span>
  * <span data-ttu-id="9b8f3-175">Ripristina il nome host su localhost.localdomain</span><span class="sxs-lookup"><span data-stu-id="9b8f3-175">Resets host name to localhost.localdomain</span></span>

> [!WARNING]
> <span data-ttu-id="9b8f3-176">Il deprovisioning non garantisce che dall'immagine vengano cancellate tutte le informazioni sensibili e che l'immagine sia adatta per la ridistribuzione.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-176">Deprovisioning does not guarantee that the image is cleared of all sensitive information and suitable for redistribution.</span></span>
> 
> 

* <span data-ttu-id="9b8f3-177">deprovision+user: esegue tutte le operazioni in -deprovision (sopra) ed elimina l'ultimo account utente sottoposto a provisioning (ottenuto da /var/lib/waagent) e i dati associati.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-177">deprovision+user: Performs everything under -deprovision (above) and also deletes the last provisioned user account (obtained from /var/lib/waagent) and associated data.</span></span> <span data-ttu-id="9b8f3-178">Questo parametro viene usato per il deprovisioning di un'immagine precedentemente sottoposta a provisioning in Azure in modo che possa essere acquisita e riutilizzata.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-178">This parameter is when de-provisioning an image that was previously provisioning on Azure so it may be captured and re-used.</span></span>
* <span data-ttu-id="9b8f3-179">version: visualizza la versione di waagent</span><span class="sxs-lookup"><span data-stu-id="9b8f3-179">version: Displays the version of waagent</span></span>
* <span data-ttu-id="9b8f3-180">serialconsole: configura GRUB affinché contrassegni ttyS0 (la prima porta seriale) come console di avvio.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-180">serialconsole: Configures GRUB to mark ttyS0 (the first serial port) as the boot console.</span></span> <span data-ttu-id="9b8f3-181">Questo garantisce che i log di avvio del kernel vengano inviati alla porta seriale e resi disponibili per il debug.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-181">This ensures that kernel bootup logs are sent to the serial port and made available for debugging.</span></span>
* <span data-ttu-id="9b8f3-182">daemon: esegue waagent come daemon per gestire l'interazione con la piattaforma.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-182">daemon: Run waagent as a daemon to manage interaction with the platform.</span></span> <span data-ttu-id="9b8f3-183">Questo argomento è specificato per waagent nello script di inizializzazione di waagent.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-183">This argument is specified to waagent in the waagent init script.</span></span>
* <span data-ttu-id="9b8f3-184">start: esegue waagent come processo in background</span><span class="sxs-lookup"><span data-stu-id="9b8f3-184">start: Run waagent as a background process</span></span>

## <a name="configuration"></a><span data-ttu-id="9b8f3-185">Configurazione</span><span class="sxs-lookup"><span data-stu-id="9b8f3-185">Configuration</span></span>
<span data-ttu-id="9b8f3-186">Un file di configurazione (/etc/waagent.conf) controlla le azioni dell'agente waagent.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-186">A configuration file (/etc/waagent.conf) controls the actions of waagent.</span></span> <span data-ttu-id="9b8f3-187">Di seguito è riportato un file di configurazione di esempio:</span><span class="sxs-lookup"><span data-stu-id="9b8f3-187">A sample configuration file is shown below:</span></span>

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

<span data-ttu-id="9b8f3-188">Di seguito sono descritte le opzioni di configurazione disponibili in modo dettagliato.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-188">The various configuration options are described in detail below.</span></span> <span data-ttu-id="9b8f3-189">Le opzioni di configurazione sono di tre tipi: Boolean, String o Integer.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-189">Configuration options are of three types; Boolean, String or Integer.</span></span> <span data-ttu-id="9b8f3-190">Le opzioni di configurazione booleane possono essere specificate come "y" o "n".</span><span class="sxs-lookup"><span data-stu-id="9b8f3-190">The Boolean configuration options can be specified as "y" or "n".</span></span> <span data-ttu-id="9b8f3-191">È possibile usare la parola chiave speciale "None" per alcune voci di configurazione di tipo stringa, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-191">The special keyword "None" may be used for some string type configuration entries as detailed below.</span></span>

<span data-ttu-id="9b8f3-192">**Provisioning.Enabled:**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-192">**Provisioning.Enabled:**</span></span>  
<span data-ttu-id="9b8f3-193">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="9b8f3-193">Type: Boolean</span></span>  
<span data-ttu-id="9b8f3-194">Predefinito: y</span><span class="sxs-lookup"><span data-stu-id="9b8f3-194">Default: y</span></span>

<span data-ttu-id="9b8f3-195">Consente all'utente di attivare o disattivare la funzionalità di provisioning nell'agente.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-195">This allows the user to enable or disable the provisioning functionality in the agent.</span></span> <span data-ttu-id="9b8f3-196">I valori validi sono "y" o "n".</span><span class="sxs-lookup"><span data-stu-id="9b8f3-196">Valid values are "y" or "n".</span></span> <span data-ttu-id="9b8f3-197">Se il provisioning è disabilitato, le chiavi utente e host SSH nell'immagine vengono mantenute e qualsiasi configurazione specificata nell'API di provisioning di Azure viene ignorata.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-197">If provisioning is disabled, SSH host and user keys in the image are preserved and any configuration specified in the Azure provisioning API is ignored.</span></span>

> [!NOTE]
> <span data-ttu-id="9b8f3-198">Per impostazione predefinita il parametro `Provisioning.Enabled` è impostato su "n" nelle immagini Ubuntu Cloud che usano cloud-init per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-198">The `Provisioning.Enabled` parameter defaults to "n" on Ubuntu Cloud Images that use cloud-init for provisioning.</span></span>
> 
> 

<span data-ttu-id="9b8f3-199">**Provisioning.DeleteRootPassword:**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-199">**Provisioning.DeleteRootPassword:**</span></span>  
<span data-ttu-id="9b8f3-200">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="9b8f3-200">Type: Boolean</span></span>  
<span data-ttu-id="9b8f3-201">Predefinito: n</span><span class="sxs-lookup"><span data-stu-id="9b8f3-201">Default: n</span></span>

<span data-ttu-id="9b8f3-202">Se questa voce è impostata, la password radice nel file /etc/shadow viene cancellata durante il processo di provisioning.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-202">If set, the root password in the /etc/shadow file is erased during the provisioning process.</span></span>

<span data-ttu-id="9b8f3-203">**Provisioning.RegenerateSshHostKeyPair:**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-203">**Provisioning.RegenerateSshHostKeyPair:**</span></span>  
<span data-ttu-id="9b8f3-204">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="9b8f3-204">Type: Boolean</span></span>  
<span data-ttu-id="9b8f3-205">Predefinito: y</span><span class="sxs-lookup"><span data-stu-id="9b8f3-205">Default: y</span></span>

<span data-ttu-id="9b8f3-206">Se questa voce è impostata, tutte le coppie di chiavi host SSH (ecdsa, dsa e rsa) vengono eliminate da /etc/ssh/ durante il processo di provisioning</span><span class="sxs-lookup"><span data-stu-id="9b8f3-206">If set, all SSH host key pairs (ecdsa, dsa and rsa) are deleted during the provisioning process from /etc/ssh/.</span></span> <span data-ttu-id="9b8f3-207">e viene generata un'unica coppia di chiavi aggiornata.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-207">And a single fresh key pair is generated.</span></span>

<span data-ttu-id="9b8f3-208">Il tipo di crittografia per la coppia di chiavi aggiornata è configurabile dalla voce Provisioning.SshHostKeyPairType.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-208">The encryption type for the fresh key pair is configurable by the Provisioning.SshHostKeyPairType entry.</span></span> <span data-ttu-id="9b8f3-209">Si noti che alcune distribuzioni ricreeranno le coppie di chiavi SSH per qualsiasi tipo di crittografia mancante al riavvio del daemon SSH, ad esempio in caso di riavvio.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-209">Please note that some distributions will re-create SSH key pairs for any missing encryption types when the SSH daemon is restarted (for example, upon a reboot).</span></span>

<span data-ttu-id="9b8f3-210">**Provisioning.SshHostKeyPairType:**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-210">**Provisioning.SshHostKeyPairType:**</span></span>  
<span data-ttu-id="9b8f3-211">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="9b8f3-211">Type: String</span></span>  
<span data-ttu-id="9b8f3-212">Predefinito: rsa</span><span class="sxs-lookup"><span data-stu-id="9b8f3-212">Default: rsa</span></span>

<span data-ttu-id="9b8f3-213">È possibile impostare questa voce su un tipo di algoritmo di crittografia supportato dal daemon SSH nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-213">This can be set to an encryption algorithm type that is supported by the SSH daemon on the virtual machine.</span></span> <span data-ttu-id="9b8f3-214">I valori supportati sono in genere "rsa", "dsa" e "ecdsa".</span><span class="sxs-lookup"><span data-stu-id="9b8f3-214">The typically supported values are "rsa", "dsa" and "ecdsa".</span></span> <span data-ttu-id="9b8f3-215">Si noti che "putty.exe" in Windows non supporta il tipo "ecdsa".</span><span class="sxs-lookup"><span data-stu-id="9b8f3-215">Note that "putty.exe" on Windows does not support "ecdsa".</span></span> <span data-ttu-id="9b8f3-216">Se pertanto si intende usare putty.exe in Windows per connettersi a una distribuzione Linux, usare "rsa" o "dsa".</span><span class="sxs-lookup"><span data-stu-id="9b8f3-216">So, if you intend to use putty.exe on Windows to connect to a Linux deployment, please use "rsa" or "dsa".</span></span>

<span data-ttu-id="9b8f3-217">**Provisioning.MonitorHostName:**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-217">**Provisioning.MonitorHostName:**</span></span>  
<span data-ttu-id="9b8f3-218">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="9b8f3-218">Type: Boolean</span></span>  
<span data-ttu-id="9b8f3-219">Predefinito: y</span><span class="sxs-lookup"><span data-stu-id="9b8f3-219">Default: y</span></span>

<span data-ttu-id="9b8f3-220">Se questa voce è impostata, waagent monitorerà la macchina virtuale Linux per rilevare modifiche del nome host (come restituite dal comando "hostname") e aggiornerà automaticamente la configurazione di rete nell'immagine per riflettere la modifica.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-220">If set, waagent will monitor the Linux virtual machine for hostname changes (as returned by the "hostname" command) and automatically update the networking configuration in the image to reflect the change.</span></span> <span data-ttu-id="9b8f3-221">Per effettuare il push della modifica del nome ai server DNS, la funzionalità di rete nella macchina virtuale verrà riavviata,</span><span class="sxs-lookup"><span data-stu-id="9b8f3-221">In order to push the name change to the DNS servers, networking will be restarted in the virtual machine.</span></span> <span data-ttu-id="9b8f3-222">causando una breve interruzione nella connettività Internet.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-222">This will result in brief loss of Internet connectivity.</span></span>

<span data-ttu-id="9b8f3-223">**Provisioning.DecodeCustomData**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-223">**Provisioning.DecodeCustomData**</span></span>  
<span data-ttu-id="9b8f3-224">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="9b8f3-224">Type: Boolean</span></span>  
<span data-ttu-id="9b8f3-225">Predefinito: n</span><span class="sxs-lookup"><span data-stu-id="9b8f3-225">Default: n</span></span>

<span data-ttu-id="9b8f3-226">Se impostato, waagent decodificherà CustomData da Base64.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-226">If set, waagent will decode CustomData from Base64.</span></span>

<span data-ttu-id="9b8f3-227">**Provisioning.ExecuteCustomData**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-227">**Provisioning.ExecuteCustomData**</span></span>  
<span data-ttu-id="9b8f3-228">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="9b8f3-228">Type: Boolean</span></span>  
<span data-ttu-id="9b8f3-229">Predefinito: n</span><span class="sxs-lookup"><span data-stu-id="9b8f3-229">Default: n</span></span>

<span data-ttu-id="9b8f3-230">Se impostato, waagent eseguirà CustomData dopo il provisioning.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-230">If set, waagent will execute CustomData after provisioning.</span></span>

<span data-ttu-id="9b8f3-231">**Provisioning.PasswordCryptId**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-231">**Provisioning.PasswordCryptId**</span></span>  
<span data-ttu-id="9b8f3-232">Tipo: stringa</span><span class="sxs-lookup"><span data-stu-id="9b8f3-232">Type:String</span></span>  
<span data-ttu-id="9b8f3-233">Predefinito: 6</span><span class="sxs-lookup"><span data-stu-id="9b8f3-233">Default:6</span></span>

<span data-ttu-id="9b8f3-234">Algoritmo usato dalla crittografia durante la generazione di hash della password.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-234">Algorithm used by crypt when generating password hash.</span></span>  
 <span data-ttu-id="9b8f3-235">1 - MD5</span><span class="sxs-lookup"><span data-stu-id="9b8f3-235">1 - MD5</span></span>  
 <span data-ttu-id="9b8f3-236">2a - Blowfish</span><span class="sxs-lookup"><span data-stu-id="9b8f3-236">2a - Blowfish</span></span>  
 <span data-ttu-id="9b8f3-237">5 - SHA-256</span><span class="sxs-lookup"><span data-stu-id="9b8f3-237">5 - SHA-256</span></span>  
 <span data-ttu-id="9b8f3-238">6 - SHA-512</span><span class="sxs-lookup"><span data-stu-id="9b8f3-238">6 - SHA-512</span></span>  

<span data-ttu-id="9b8f3-239">**Provisioning.PasswordCryptSaltLength**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-239">**Provisioning.PasswordCryptSaltLength**</span></span>  
<span data-ttu-id="9b8f3-240">Tipo: stringa</span><span class="sxs-lookup"><span data-stu-id="9b8f3-240">Type:String</span></span>  
<span data-ttu-id="9b8f3-241">Predefinito: 10</span><span class="sxs-lookup"><span data-stu-id="9b8f3-241">Default:10</span></span>

<span data-ttu-id="9b8f3-242">Lunghezza di salt casuale usata durante la generazione di hash della password.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-242">Length of random salt used when generating password hash.</span></span>

<span data-ttu-id="9b8f3-243">**ResourceDisk.Format:**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-243">**ResourceDisk.Format:**</span></span>  
<span data-ttu-id="9b8f3-244">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="9b8f3-244">Type: Boolean</span></span>  
<span data-ttu-id="9b8f3-245">Predefinito: y</span><span class="sxs-lookup"><span data-stu-id="9b8f3-245">Default: y</span></span>

<span data-ttu-id="9b8f3-246">Se questa voce è impostata, il disco risorse fornito dalla piattaforma verrà formattato e montato da waagent se il tipo di file system richiesto dall'utente in "ResourceDisk.Filesystem" è diverso da "ntfs".</span><span class="sxs-lookup"><span data-stu-id="9b8f3-246">If set, the resource disk provided by the platform will be formatted and mounted by waagent if the filesystem type requested by the user in "ResourceDisk.Filesystem" is anything other than "ntfs".</span></span> <span data-ttu-id="9b8f3-247">Una singola partizione di tipo Linux (83) verrà resa disponibile nel disco.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-247">A single partition of type Linux (83) will be made available on the disk.</span></span> <span data-ttu-id="9b8f3-248">Si noti che la partizione non verrà formattata se è possibile montarla correttamente.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-248">Note that this partition will not be formatted if it can be successfully mounted.</span></span>

<span data-ttu-id="9b8f3-249">**ResourceDisk.Filesystem:**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-249">**ResourceDisk.Filesystem:**</span></span>  
<span data-ttu-id="9b8f3-250">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="9b8f3-250">Type: String</span></span>  
<span data-ttu-id="9b8f3-251">Predefinito: ext4</span><span class="sxs-lookup"><span data-stu-id="9b8f3-251">Default: ext4</span></span>

<span data-ttu-id="9b8f3-252">Specifica il tipo di file system per il disco risorse.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-252">This specifies the filesystem type for the resource disk.</span></span> <span data-ttu-id="9b8f3-253">I valori supportati variano in base alla distribuzione Linux.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-253">Supported values vary by Linux distribution.</span></span> <span data-ttu-id="9b8f3-254">Se la stringa è X, è necessario che mkfs.X sia presente nell'immagine Linux.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-254">If the string is X, then mkfs.X should be present on the Linux image.</span></span> <span data-ttu-id="9b8f3-255">Le immagini SLES 11 in genere utilizzano il valore 'ext3'.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-255">SLES 11 images should typically use 'ext3'.</span></span> <span data-ttu-id="9b8f3-256">Le immagini FreeBSD in questo caso devono usare il valore 'ufs2'.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-256">FreeBSD images should use 'ufs2' here.</span></span>

<span data-ttu-id="9b8f3-257">**ResourceDisk.MountPoint:**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-257">**ResourceDisk.MountPoint:**</span></span>  
<span data-ttu-id="9b8f3-258">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="9b8f3-258">Type: String</span></span>  
<span data-ttu-id="9b8f3-259">Predefinito: /mnt/resource</span><span class="sxs-lookup"><span data-stu-id="9b8f3-259">Default: /mnt/resource</span></span> 

<span data-ttu-id="9b8f3-260">Specifica il percorso in cui è montato il disco risorse.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-260">This specifies the path at which the resource disk is mounted.</span></span> <span data-ttu-id="9b8f3-261">Si noti che il disco risorse è un disco *temporaneo* e potrebbe essere svuotato in seguito al deprovisioning della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-261">Note that the resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span>

<span data-ttu-id="9b8f3-262">**ResourceDisk.MountOptions**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-262">**ResourceDisk.MountOptions**</span></span>  
<span data-ttu-id="9b8f3-263">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="9b8f3-263">Type: String</span></span>  
<span data-ttu-id="9b8f3-264">Predefinito: nessuno</span><span class="sxs-lookup"><span data-stu-id="9b8f3-264">Default: None</span></span>

<span data-ttu-id="9b8f3-265">Specifica le opzioni di montaggio del disco da passare al comando.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-265">Specifies disk mount options to be passed to the mount -o command.</span></span> <span data-ttu-id="9b8f3-266">È un elenco di valori delimitato da virgole, ad esempio</span><span class="sxs-lookup"><span data-stu-id="9b8f3-266">This is a comma separated list of values, ex.</span></span> <span data-ttu-id="9b8f3-267">nodev,nosuid.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-267">'nodev,nosuid'.</span></span> <span data-ttu-id="9b8f3-268">Vedere montaggio(8) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-268">See mount(8) for details.</span></span>

<span data-ttu-id="9b8f3-269">**ResourceDisk.EnableSwap:**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-269">**ResourceDisk.EnableSwap:**</span></span>  
<span data-ttu-id="9b8f3-270">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="9b8f3-270">Type: Boolean</span></span>  
<span data-ttu-id="9b8f3-271">Predefinito: n</span><span class="sxs-lookup"><span data-stu-id="9b8f3-271">Default: n</span></span>

<span data-ttu-id="9b8f3-272">Se questa voce è impostata, viene creato un file di scambio (/swapfile) nel disco risorse e aggiunto all'area di swap del sistema.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-272">If set, a swap file (/swapfile) is created on the resource disk and added to the system swap space.</span></span>

<span data-ttu-id="9b8f3-273">**ResourceDisk.SwapSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-273">**ResourceDisk.SwapSizeMB:**</span></span>  
<span data-ttu-id="9b8f3-274">Tipo: numero intero</span><span class="sxs-lookup"><span data-stu-id="9b8f3-274">Type: Integer</span></span>  
<span data-ttu-id="9b8f3-275">Predefinito: 0</span><span class="sxs-lookup"><span data-stu-id="9b8f3-275">Default: 0</span></span>

<span data-ttu-id="9b8f3-276">Dimensione del file di scambio in megabyte.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-276">The size of the swap file in megabytes.</span></span>

<span data-ttu-id="9b8f3-277">**Logs.Verbose:**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-277">**Logs.Verbose:**</span></span>  
<span data-ttu-id="9b8f3-278">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="9b8f3-278">Type: Boolean</span></span>  
<span data-ttu-id="9b8f3-279">Predefinito: n</span><span class="sxs-lookup"><span data-stu-id="9b8f3-279">Default: n</span></span>

<span data-ttu-id="9b8f3-280">Se questa voce è impostata, viene incrementato il livello di dettaglio del log.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-280">If set, log verbosity is boosted.</span></span> <span data-ttu-id="9b8f3-281">Waagent registra in /var/log/waagent.log e usufruisce della funzionalità logrotate del sistema per la rotazione dei log.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-281">Waagent logs to /var/log/waagent.log and leverages the system logrotate functionality to rotate logs.</span></span>

<span data-ttu-id="9b8f3-282">**OS.EnableRDMA**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-282">**OS.EnableRDMA**</span></span>  
<span data-ttu-id="9b8f3-283">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="9b8f3-283">Type: Boolean</span></span>  
<span data-ttu-id="9b8f3-284">Predefinito: n</span><span class="sxs-lookup"><span data-stu-id="9b8f3-284">Default: n</span></span>

<span data-ttu-id="9b8f3-285">Se impostato, l'agente tenterà di installare e caricare un driver del kernel RDMA adatto alla versione del firmware nell'hardware sottostante.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-285">If set, the agent will attempt to install and then load an RDMA kernel driver that matches the version of the firmware on the underlying hardware.</span></span>

<span data-ttu-id="9b8f3-286">**OS.RootDeviceScsiTimeout:**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-286">**OS.RootDeviceScsiTimeout:**</span></span>  
<span data-ttu-id="9b8f3-287">Tipo: numero intero</span><span class="sxs-lookup"><span data-stu-id="9b8f3-287">Type: Integer</span></span>  
<span data-ttu-id="9b8f3-288">Predefinito: 300</span><span class="sxs-lookup"><span data-stu-id="9b8f3-288">Default: 300</span></span>

<span data-ttu-id="9b8f3-289">Consente di configurare il timeout SCSI in secondi nel disco del sistema operativo e nelle unità dati.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-289">This configures the SCSI timeout in seconds on the OS disk and data drives.</span></span> <span data-ttu-id="9b8f3-290">Se questa voce non è impostata, vengono usate le impostazioni predefinite del sistema.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-290">If not set, the system defaults are used.</span></span>

<span data-ttu-id="9b8f3-291">**OS.OpensslPath:**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-291">**OS.OpensslPath:**</span></span>  
<span data-ttu-id="9b8f3-292">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="9b8f3-292">Type: String</span></span>  
<span data-ttu-id="9b8f3-293">Predefinito: nessuno</span><span class="sxs-lookup"><span data-stu-id="9b8f3-293">Default: None</span></span>

<span data-ttu-id="9b8f3-294">È possibile aggiungere questa voce per specificare un percorso alternativo per il file binario openssl da usare per le operazioni di crittografia.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-294">This can be used to specify an alternate path for the openssl binary to use for cryptographic operations.</span></span>

<span data-ttu-id="9b8f3-295">**HttpProxy.Host, HttpProxy.Port**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-295">**HttpProxy.Host, HttpProxy.Port**</span></span>  
<span data-ttu-id="9b8f3-296">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="9b8f3-296">Type: String</span></span>  
<span data-ttu-id="9b8f3-297">Predefinito: nessuno</span><span class="sxs-lookup"><span data-stu-id="9b8f3-297">Default: None</span></span>

<span data-ttu-id="9b8f3-298">Se impostato, l'agente userà il server proxy per accedere a Internet.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-298">If set, the agent will use this proxy server to access the internet.</span></span> 

## <a name="ubuntu-cloud-images"></a><span data-ttu-id="9b8f3-299">Immagini di Ubuntu Cloud</span><span class="sxs-lookup"><span data-stu-id="9b8f3-299">Ubuntu Cloud Images</span></span>
<span data-ttu-id="9b8f3-300">Si noti che le immagini di Ubuntu Cloud utilizzano [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) per eseguire molte attività di configurazione che verrebbero altrimenti gestite dall’agente Linux di Azure.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-300">Note that Ubuntu Cloud Images utilize [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) to perform many configuration tasks that would otherwise be managed by the Azure Linux Agent.</span></span>  <span data-ttu-id="9b8f3-301">Tenere presenti le differenze seguenti:</span><span class="sxs-lookup"><span data-stu-id="9b8f3-301">Please note the following differences:</span></span>

* <span data-ttu-id="9b8f3-302">**Provisioning.Enabled** è "n" nelle immagini di Ubuntu Cloud che utilizzano cloud-init per eseguire attività di provisioning.</span><span class="sxs-lookup"><span data-stu-id="9b8f3-302">**Provisioning.Enabled** defaults to "n" on Ubuntu Cloud Images that use cloud-init to perform provisioning tasks.</span></span>
* <span data-ttu-id="9b8f3-303">I seguenti parametri di configurazione non hanno alcun effetto sulle immagini di Ubuntu Cloud che utilizzano cloud-init per gestire disco risorse e spazio di scambio:</span><span class="sxs-lookup"><span data-stu-id="9b8f3-303">The following configuration parameters have no effect on Ubuntu Cloud Images that use cloud-init to manage the resource disk and swap space:</span></span>
  
  * <span data-ttu-id="9b8f3-304">**ResourceDisk.Format**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-304">**ResourceDisk.Format**</span></span>
  * <span data-ttu-id="9b8f3-305">**ResourceDisk.Filesystem**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-305">**ResourceDisk.Filesystem**</span></span>
  * <span data-ttu-id="9b8f3-306">**ResourceDisk.MountPoint**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-306">**ResourceDisk.MountPoint**</span></span>
  * <span data-ttu-id="9b8f3-307">**ResourceDisk.EnableSwap**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-307">**ResourceDisk.EnableSwap**</span></span>
  * <span data-ttu-id="9b8f3-308">**ResourceDisk.SwapSizeMB**</span><span class="sxs-lookup"><span data-stu-id="9b8f3-308">**ResourceDisk.SwapSizeMB**</span></span>
* <span data-ttu-id="9b8f3-309">Vedere le risorse seguenti per configurare il punto di montaggio del disco di risorsa e scambiare spazio nelle immagini di Ubuntu Cloud durante il provisioning:</span><span class="sxs-lookup"><span data-stu-id="9b8f3-309">Please see the following resources to configure the resource disk mount point and swap space on Ubuntu Cloud Images during provisioning:</span></span>
  
  * [<span data-ttu-id="9b8f3-310">Ubuntu Wiki: Configurare partizioni di scambio</span><span class="sxs-lookup"><span data-stu-id="9b8f3-310">Ubuntu Wiki: Configure Swap Partitions</span></span>](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [<span data-ttu-id="9b8f3-311">Inserimento di dati personalizzati in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="9b8f3-311">Injecting Custom Data into an Azure Virtual Machine</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

