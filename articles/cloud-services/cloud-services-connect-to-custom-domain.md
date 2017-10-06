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
# <a name="connecting-azure-cloud-services-roles-tooa-custom-ad-domain-controller-hosted-in-azure"></a>Connessione personalizzata tooa i ruoli di servizi Cloud di Azure il Controller di dominio Active Directory ospitato in Azure
È prima di tutto necessario configurare una rete virtuale (VNet) in Azure Sarà quindi necessario aggiungere una rete virtuale di toohello Controller dominio Active Directory (ospitato in una macchina virtuale di Azure). Successivamente, si verrà aggiungere esistente toohello di ruoli del servizio cloud creato in precedenza rete virtuale, quindi connetterle toohello Controller di dominio.

Prima di iniziare, paio di aspetti tookeep presente:

1. In questa esercitazione Usa PowerShell, pertanto assicurarsi di avere installato Azure PowerShell e pronto toogo. Guida di tooget all'impostazione di Azure PowerShell, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).
2. Le istanze del Controller di dominio Active Directory e ruolo Web/di lavoro necessario toobe in hello rete virtuale.

Seguire questa procedura dettagliata e se si verificano problemi, lascia un commento alla fine di hello dell'articolo hello. Un utente verrà inviata tooyou (Sì, abbiamo leggere commenti).

rete Hello che fa riferimento al servizio cloud hello deve essere un **rete virtuale classica**.

## <a name="create-a-virtual-network"></a>Creare una rete virtuale
È possibile creare una rete virtuale in Azure utilizzando hello portale di Azure o PowerShell. Per questa esercitazione verrà usato PowerShell. una rete virtuale utilizzando toocreate hello Azure portale, vedere [crea rete virtuale](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

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

## <a name="create-a-virtual-machine"></a>Creare una macchina virtuale
Dopo aver completato l'impostazione di hello rete virtuale, sarà necessario toocreate un Controller di dominio Active Directory. Per questa esercitazione verrà configurato un controller di dominio di AD in una macchina virtuale di Azure.

toodo, creare una macchina virtuale mediante PowerShell usando hello seguenti comandi:

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

## <a name="promote-your-virtual-machine-tooa-domain-controller"></a>Alzare di livello il Controller di dominio di tooa macchina virtuale
hello tooconfigure macchina virtuale come Controller di dominio Active Directory, sarà anche necessario toolog in toohello macchina virtuale e configurarlo.

toolog in toohello VM, è possibile ottenere il file RDP hello tramite PowerShell, hello di utilizzare i comandi seguenti:

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

Dopo sei toohello VM, impostare la macchina virtuale come Controller di dominio Active Directory dal seguente Guida dettagliata di hello [come tooset il Controller di dominio Active Directory del cliente](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).

## <a name="add-your-cloud-service-toohello-virtual-network"></a>Aggiungere la rete virtuale di toohello servizio Cloud
Successivamente, è necessario tooadd il toohello di distribuzione del servizio cloud nuova rete virtuale. toodo, modificare il file cscfg del servizio cloud aggiungendo hello sezioni pertinenti tooyour cscfg utilizzando Visual Studio o hello editor di propria scelta.

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

Successivamente, compilare il progetto di servizi cloud e distribuirlo tooAzure. tooget Guida alla distribuzione tooAzure di pacchetto i servizi cloud, vedere [come tooCreate e distribuire un servizio Cloud](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)

## <a name="connect-your-webworker-roles-toohello-domain"></a>Connettersi al dominio toohello di ruoli web/di lavoro
Dopo aver distribuito il progetto servizio cloud in Azure, collegare il dominio toohello personalizzato AD istanze di ruolo utilizzando hello estensione di dominio Active Directory. hello tooadd distribuzione di servizi di dominio Active Directory estensione tooyour esistente cloud e il dominio personalizzato hello join, eseguire hello comandi di PowerShell seguente:

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

L'operazione è terminata.

I servizi cloud devono essere tooyour aggiunti a un controller di dominio personalizzato. Se si desidera approfondire hello diverse opzioni disponibili per toolearn come estensione di dominio Active Directory, utilizzare hello PowerShell tooconfigure la Guida. Di seguito sono riportati alcuni esempi:

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
