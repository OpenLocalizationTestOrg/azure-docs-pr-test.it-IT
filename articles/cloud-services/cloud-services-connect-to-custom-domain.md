---
title: aaaConnect tooa un servizio Cloud del Controller di dominio personalizzato | Documenti Microsoft
description: Informazioni su come tooconnect personalizzato tooa ruoli web/di lavoro dominio di Active Directory tramite PowerShell e l'estensione di dominio Active Directory
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1e2d7c87-d254-4e7a-a832-67f84411ec95
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 9540190ccf17c03e55159c6c68429eee29e0a558
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-cloud-services-roles-tooa-custom-ad-domain-controller-hosted-in-azure"></a><span data-ttu-id="2714f-103">Connessione personalizzata tooa i ruoli di servizi Cloud di Azure il Controller di dominio Active Directory ospitato in Azure</span><span class="sxs-lookup"><span data-stu-id="2714f-103">Connecting Azure Cloud Services Roles tooa custom AD Domain Controller hosted in Azure</span></span>
<span data-ttu-id="2714f-104">È prima di tutto necessario configurare una rete virtuale (VNet) in Azure</span><span class="sxs-lookup"><span data-stu-id="2714f-104">We will first set up a Virtual Network (VNet) in Azure.</span></span> <span data-ttu-id="2714f-105">Sarà quindi necessario aggiungere una rete virtuale di toohello Controller dominio Active Directory (ospitato in una macchina virtuale di Azure).</span><span class="sxs-lookup"><span data-stu-id="2714f-105">We will then add an Active Directory Domain Controller (hosted on an Azure Virtual Machine) toohello VNet.</span></span> <span data-ttu-id="2714f-106">Successivamente, si verrà aggiungere esistente toohello di ruoli del servizio cloud creato in precedenza rete virtuale, quindi connetterle toohello Controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="2714f-106">Next, we will add existing cloud service roles toohello pre-created VNet, then connect them toohello Domain Controller.</span></span>

<span data-ttu-id="2714f-107">Prima di iniziare, paio di aspetti tookeep presente:</span><span class="sxs-lookup"><span data-stu-id="2714f-107">Before we get started, couple of things tookeep in mind:</span></span>

1. <span data-ttu-id="2714f-108">In questa esercitazione Usa PowerShell, pertanto assicurarsi di avere installato Azure PowerShell e pronto toogo.</span><span class="sxs-lookup"><span data-stu-id="2714f-108">This tutorial uses PowerShell, so make sure you have Azure PowerShell installed and ready toogo.</span></span> <span data-ttu-id="2714f-109">Guida di tooget all'impostazione di Azure PowerShell, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2714f-109">tooget help with setting up Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="2714f-110">Le istanze del Controller di dominio Active Directory e ruolo Web/di lavoro necessario toobe in hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="2714f-110">Your AD Domain Controller and Web/Worker Role instances need toobe in hello VNet.</span></span>

<span data-ttu-id="2714f-111">Seguire questa procedura dettagliata e se si verificano problemi, lascia un commento alla fine di hello dell'articolo hello.</span><span class="sxs-lookup"><span data-stu-id="2714f-111">Follow this step-by-step guide and if you run into any issues, leave us a comment at hello end of hello article.</span></span> <span data-ttu-id="2714f-112">Un utente verrà inviata tooyou (Sì, abbiamo leggere commenti).</span><span class="sxs-lookup"><span data-stu-id="2714f-112">Someone will get back tooyou (yes, we do read comments).</span></span>

<span data-ttu-id="2714f-113">rete Hello che fa riferimento al servizio cloud hello deve essere un **rete virtuale classica**.</span><span class="sxs-lookup"><span data-stu-id="2714f-113">hello network that is referenced by hello cloud service must be a **classic virtual network**.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="2714f-114">Creare una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="2714f-114">Create a Virtual Network</span></span>
<span data-ttu-id="2714f-115">È possibile creare una rete virtuale in Azure utilizzando hello portale di Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2714f-115">You can create a Virtual Network in Azure using hello Azure portal or PowerShell.</span></span> <span data-ttu-id="2714f-116">Per questa esercitazione verrà usato PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2714f-116">For this tutorial, we will use PowerShell.</span></span> <span data-ttu-id="2714f-117">una rete virtuale utilizzando toocreate hello Azure portale, vedere [crea rete virtuale](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="2714f-117">toocreate a Virtual Network using hello Azure portal, see [Create Virtual Network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

```powershell
#Create Virtual Network

$vnetStr =
@"<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
    <VirtualNetworkConfiguration>
    <VirtualNetworkSites>
        <VirtualNetworkSite name="[your-vnet-name]" Location="West US">
        <AddressSpace>
            <AddressPrefix>[your-address-prefix]</AddressPrefix>
        </AddressSpace>
        <Subnets>
            <Subnet name="[your-subnet-name]">
            <AddressPrefix>[your-subnet-range]</AddressPrefix>
            </Subnet>
        </Subnets>
        </VirtualNetworkSite>
    </VirtualNetworkSites>
    </VirtualNetworkConfiguration>
</NetworkConfiguration>
"@;

$vnetConfigPath = "<path-to-vnet-config>"
Set-AzureVNetConfig -ConfigurationPath $vnetConfigPath
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="2714f-118">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="2714f-118">Create a Virtual Machine</span></span>
<span data-ttu-id="2714f-119">Dopo aver completato l'impostazione di hello rete virtuale, sarà necessario toocreate un Controller di dominio Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2714f-119">Once you have completed setting up hello Virtual Network, you will need toocreate an AD Domain Controller.</span></span> <span data-ttu-id="2714f-120">Per questa esercitazione verrà configurato un controller di dominio di AD in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2714f-120">For this tutorial, we will be setting up an AD Domain Controller on an Azure Virtual Machine.</span></span>

<span data-ttu-id="2714f-121">toodo, creare una macchina virtuale mediante PowerShell usando hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="2714f-121">toodo this, create a virtual machine through PowerShell using hello following commands:</span></span>

```powershell
# Initialize variables
# VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.

$vnetname = '<your-vnet-name>'
$subnetname = '<your-subnet-name>'
$vmsvc1 = '<your-hosted-service>'
$vm1 = '<your-vm-name>'
$username = '<your-username>'
$password = '<your-password>'
$affgrp = '<your- affgrp>'

# Create a VM and add it toohello Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-tooa-domain-controller"></a><span data-ttu-id="2714f-122">Alzare di livello il Controller di dominio di tooa macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="2714f-122">Promote your Virtual Machine tooa Domain Controller</span></span>
<span data-ttu-id="2714f-123">hello tooconfigure macchina virtuale come Controller di dominio Active Directory, sarà anche necessario toolog in toohello macchina virtuale e configurarlo.</span><span class="sxs-lookup"><span data-stu-id="2714f-123">tooconfigure hello Virtual Machine as an AD Domain Controller, you will need toolog in toohello VM and configure it.</span></span>

<span data-ttu-id="2714f-124">toolog in toohello VM, è possibile ottenere il file RDP hello tramite PowerShell, hello di utilizzare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2714f-124">toolog in toohello VM, you can get hello RDP file through PowerShell, use hello following commands:</span></span>

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

<span data-ttu-id="2714f-125">Dopo sei toohello VM, impostare la macchina virtuale come Controller di dominio Active Directory dal seguente Guida dettagliata di hello [come tooset il Controller di dominio Active Directory del cliente](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="2714f-125">Once you are signed in toohello VM, set up your Virtual Machine as an AD Domain Controller by following hello step-by-step guide on [How tooset up your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span></span>

## <a name="add-your-cloud-service-toohello-virtual-network"></a><span data-ttu-id="2714f-126">Aggiungere la rete virtuale di toohello servizio Cloud</span><span class="sxs-lookup"><span data-stu-id="2714f-126">Add your Cloud Service toohello Virtual Network</span></span>
<span data-ttu-id="2714f-127">Successivamente, è necessario tooadd il toohello di distribuzione del servizio cloud nuova rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="2714f-127">Next, you need tooadd your cloud service deployment toohello new VNet.</span></span> <span data-ttu-id="2714f-128">toodo, modificare il file cscfg del servizio cloud aggiungendo hello sezioni pertinenti tooyour cscfg utilizzando Visual Studio o hello editor di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="2714f-128">toodo this, modify your cloud service cscfg by adding hello relevant sections tooyour cscfg using Visual Studio or hello editor of your choice.</span></span>

```xml
<ServiceConfiguration serviceName="[hosted-service-name]" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="[os-family]" osVersion="*">
    <Role name="[role-name]">
    <Instances count="[number-of-instances]" />
    </Role>
    <NetworkConfiguration>

    <!--optional-->
    <Dns>
        <DnsServers><DnsServer name="[dns-server-name]" IPAddress="[ip-address]" /></DnsServers>
    </Dns>
    <!--optional-->

    <!--VNet settings
        VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.-->
    <VirtualNetworkSite name="[virtual-network-name]" />
    <AddressAssignments>
        <InstanceAddress roleName="[role-name]">
        <Subnets>
            <Subnet name="[subnet-name]" />
        </Subnets>
        </InstanceAddress>
    </AddressAssignments>
    <!--VNet settings-->

    </NetworkConfiguration>
</ServiceConfiguration>
```

<span data-ttu-id="2714f-129">Successivamente, compilare il progetto di servizi cloud e distribuirlo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2714f-129">Next build your cloud services project and deploy it tooAzure.</span></span> <span data-ttu-id="2714f-130">tooget Guida alla distribuzione tooAzure di pacchetto i servizi cloud, vedere [come tooCreate e distribuire un servizio Cloud](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span><span class="sxs-lookup"><span data-stu-id="2714f-130">tooget help with deploying your cloud services package tooAzure, see [How tooCreate and Deploy a Cloud Service](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span></span>

## <a name="connect-your-webworker-roles-toohello-domain"></a><span data-ttu-id="2714f-131">Connettersi al dominio toohello di ruoli web/di lavoro</span><span class="sxs-lookup"><span data-stu-id="2714f-131">Connect your web/worker roles toohello domain</span></span>
<span data-ttu-id="2714f-132">Dopo aver distribuito il progetto servizio cloud in Azure, collegare il dominio toohello personalizzato AD istanze di ruolo utilizzando hello estensione di dominio Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2714f-132">Once your cloud service project is deployed on Azure, connect your role instances toohello custom AD domain using hello AD Domain Extension.</span></span> <span data-ttu-id="2714f-133">hello tooadd distribuzione di servizi di dominio Active Directory estensione tooyour esistente cloud e il dominio personalizzato hello join, eseguire hello comandi di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="2714f-133">tooadd hello AD Domain Extension tooyour existing cloud services deployment and join hello custom domain, execute hello following commands in PowerShell:</span></span>

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension toohello cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

<span data-ttu-id="2714f-134">L'operazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="2714f-134">And that's it.</span></span>

<span data-ttu-id="2714f-135">I servizi cloud devono essere tooyour aggiunti a un controller di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="2714f-135">Your cloud services should be joined tooyour custom domain controller.</span></span> <span data-ttu-id="2714f-136">Se si desidera approfondire hello diverse opzioni disponibili per toolearn come estensione di dominio Active Directory, utilizzare hello PowerShell tooconfigure la Guida.</span><span class="sxs-lookup"><span data-stu-id="2714f-136">If you would like toolearn more about hello different options available for how tooconfigure AD Domain Extension, use hello PowerShell help.</span></span> <span data-ttu-id="2714f-137">Di seguito sono riportati alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="2714f-137">A couple of examples follow:</span></span>

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
