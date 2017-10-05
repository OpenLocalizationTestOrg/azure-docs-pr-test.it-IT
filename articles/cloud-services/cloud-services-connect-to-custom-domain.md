---
title: Connettere un servizio cloud a un controller di dominio personalizzato | Documentazione Microsoft
description: Informazioni su come connettere i ruoli Web/di lavoro a un dominio personalizzato di AD usando PowerShell e l'estensione di dominio di AD
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
ms.openlocfilehash: 17f6918371678ac849198bff4e3b3eea8678c660
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="connecting-azure-cloud-services-roles-to-a-custom-ad-domain-controller-hosted-in-azure"></a><span data-ttu-id="050b3-103">Connessione dei ruoli dei Servizi cloud di Azure a un controller di dominio personalizzato di AD ospitato in Azure</span><span class="sxs-lookup"><span data-stu-id="050b3-103">Connecting Azure Cloud Services Roles to a custom AD Domain Controller hosted in Azure</span></span>
<span data-ttu-id="050b3-104">È prima di tutto necessario configurare una rete virtuale (VNet) in Azure</span><span class="sxs-lookup"><span data-stu-id="050b3-104">We will first set up a Virtual Network (VNet) in Azure.</span></span> <span data-ttu-id="050b3-105">e quindi aggiungere a tale VNet un controller di dominio di Active Directory ospitato in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="050b3-105">We will then add an Active Directory Domain Controller (hosted on an Azure Virtual Machine) to the VNet.</span></span> <span data-ttu-id="050b3-106">I ruoli del servizio cloud esistente verranno quindi aggiunti alla rete virtuale creata in precedenza e connessi al controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="050b3-106">Next, we will add existing cloud service roles to the pre-created VNet, then connect them to the Domain Controller.</span></span>

<span data-ttu-id="050b3-107">Prima di iniziare è necessario notare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="050b3-107">Before we get started, couple of things to keep in mind:</span></span>

1. <span data-ttu-id="050b3-108">Questa esercitazione usa PowerShell ed è quindi necessario assicurarsi che Azure PowerShell sia installato e pronto per l'uso.</span><span class="sxs-lookup"><span data-stu-id="050b3-108">This tutorial uses PowerShell, so make sure you have Azure PowerShell installed and ready to go.</span></span> <span data-ttu-id="050b3-109">Per ottenere informazioni sulla configurazione di Azure PowerShell, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="050b3-109">To get help with setting up Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="050b3-110">Il controller di dominio di AD e le istanze dei ruoli Web/di lavoro devono essere presenti nella VNet.</span><span class="sxs-lookup"><span data-stu-id="050b3-110">Your AD Domain Controller and Web/Worker Role instances need to be in the VNet.</span></span>

<span data-ttu-id="050b3-111">Seguire questa guida dettagliata e in caso di problemi inserire commenti alla fine dell'articolo.</span><span class="sxs-lookup"><span data-stu-id="050b3-111">Follow this step-by-step guide and if you run into any issues, leave us a comment at the end of the article.</span></span> <span data-ttu-id="050b3-112">I commenti verranno letti e verrà fornita assistenza.</span><span class="sxs-lookup"><span data-stu-id="050b3-112">Someone will get back to you (yes, we do read comments).</span></span>

<span data-ttu-id="050b3-113">La rete a cui viene fatto riferimento dal servizio cloud deve essere una **rete virtuale classica**.</span><span class="sxs-lookup"><span data-stu-id="050b3-113">The network that is referenced by the cloud service must be a **classic virtual network**.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="050b3-114">Creare una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="050b3-114">Create a Virtual Network</span></span>
<span data-ttu-id="050b3-115">È possibile creare una rete virtuale in Azure usando il portale di Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="050b3-115">You can create a Virtual Network in Azure using the Azure portal or PowerShell.</span></span> <span data-ttu-id="050b3-116">Per questa esercitazione verrà usato PowerShell.</span><span class="sxs-lookup"><span data-stu-id="050b3-116">For this tutorial, we will use PowerShell.</span></span> <span data-ttu-id="050b3-117">Per creare una rete virtuale usando il portale di Azure, vedere [Creare una rete virtuale](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="050b3-117">To create a Virtual Network using the Azure portal, see [Create Virtual Network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

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

## <a name="create-a-virtual-machine"></a><span data-ttu-id="050b3-118">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="050b3-118">Create a Virtual Machine</span></span>
<span data-ttu-id="050b3-119">Dopo il completamento della configurazione della rete virtuale, sarà necessario creare un controller di dominio di AD.</span><span class="sxs-lookup"><span data-stu-id="050b3-119">Once you have completed setting up the Virtual Network, you will need to create an AD Domain Controller.</span></span> <span data-ttu-id="050b3-120">Per questa esercitazione verrà configurato un controller di dominio di AD in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="050b3-120">For this tutorial, we will be setting up an AD Domain Controller on an Azure Virtual Machine.</span></span>

<span data-ttu-id="050b3-121">A questo scopo, creare una macchina virtuale tramite PowerShell usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="050b3-121">To do this, create a virtual machine through PowerShell using the following commands:</span></span>

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

# Create a VM and add it to the Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-to-a-domain-controller"></a><span data-ttu-id="050b3-122">Alzare la macchina virtuale al livello di controller di dominio</span><span class="sxs-lookup"><span data-stu-id="050b3-122">Promote your Virtual Machine to a Domain Controller</span></span>
<span data-ttu-id="050b3-123">Per configurare la macchina virtuale come controller di dominio di AD, sarà necessario accedere alla macchina virtuale e configurarla.</span><span class="sxs-lookup"><span data-stu-id="050b3-123">To configure the Virtual Machine as an AD Domain Controller, you will need to log in to the VM and configure it.</span></span>

<span data-ttu-id="050b3-124">Per accedere alla macchina virtuale, è possibile ottenere il file RDP tramite PowerShell e usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="050b3-124">To log in to the VM, you can get the RDP file through PowerShell, use the following commands:</span></span>

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

<span data-ttu-id="050b3-125">Dopo avere effettuato l'accesso alla macchina virtuale, configurarla come controller di dominio di AD seguendo la guida dettagliata che illustra [come configurare il controller di dominio personalizzato di AD](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="050b3-125">Once you are signed in to the VM, set up your Virtual Machine as an AD Domain Controller by following the step-by-step guide on [How to set up your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span></span>

## <a name="add-your-cloud-service-to-the-virtual-network"></a><span data-ttu-id="050b3-126">Aggiungere il servizio cloud alla rete virtuale</span><span class="sxs-lookup"><span data-stu-id="050b3-126">Add your Cloud Service to the Virtual Network</span></span>
<span data-ttu-id="050b3-127">Sarà quindi necessario aggiungere la distribuzione del servizio cloud alla nuova rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="050b3-127">Next, you need to add your cloud service deployment to the new VNet.</span></span> <span data-ttu-id="050b3-128">A questo scopo, modificare il file cscfg del servizio cloud aggiungendo le sezioni rilevanti mediante Visual Studio o l'editor preferito.</span><span class="sxs-lookup"><span data-stu-id="050b3-128">To do this, modify your cloud service cscfg by adding the relevant sections to your cscfg using Visual Studio or the editor of your choice.</span></span>

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

<span data-ttu-id="050b3-129">Compilare quindi il progetto dei servizi cloud e distribuirlo in Azure.</span><span class="sxs-lookup"><span data-stu-id="050b3-129">Next build your cloud services project and deploy it to Azure.</span></span> <span data-ttu-id="050b3-130">Per ottenere informazioni sulla distribuzione del pacchetto di servizi cloud in Azure, vedere [Come creare e distribuire un servizio cloud](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span><span class="sxs-lookup"><span data-stu-id="050b3-130">To get help with deploying your cloud services package to Azure, see [How to Create and Deploy a Cloud Service](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span></span>

## <a name="connect-your-webworker-roles-to-the-domain"></a><span data-ttu-id="050b3-131">Connettere i ruoli Web/di lavoro al dominio</span><span class="sxs-lookup"><span data-stu-id="050b3-131">Connect your web/worker roles to the domain</span></span>
<span data-ttu-id="050b3-132">Dopo la distribuzione del progetto di servizi cloud in Azure, connettere le istanze del ruolo al dominio personalizzato di AD usando l'estensione del dominio di AD.</span><span class="sxs-lookup"><span data-stu-id="050b3-132">Once your cloud service project is deployed on Azure, connect your role instances to the custom AD domain using the AD Domain Extension.</span></span> <span data-ttu-id="050b3-133">Per aggiungere l'estensione di dominio di AD alla distribuzione esistente dei servizi cloud e aggiungere il dominio personalizzato, eseguire i comandi seguenti in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="050b3-133">To add the AD Domain Extension to your existing cloud services deployment and join the custom domain, execute the following commands in PowerShell:</span></span>

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension to the cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

<span data-ttu-id="050b3-134">L'operazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="050b3-134">And that's it.</span></span>

<span data-ttu-id="050b3-135">I servizi cloud sono stati aggiunti al controller di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="050b3-135">Your cloud services should be joined to your custom domain controller.</span></span> <span data-ttu-id="050b3-136">Per altre informazioni sulle diverse opzioni disponibili per la configurazione dell'estensione di dominio di AD, usare la Guida di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="050b3-136">If you would like to learn more about the different options available for how to configure AD Domain Extension, use the PowerShell help.</span></span> <span data-ttu-id="050b3-137">Di seguito sono riportati alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="050b3-137">A couple of examples follow:</span></span>

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
