---
title: aaaStatic interno classica - VM di Azure - IP privato
description: Informazioni IP interno statico (DIP) e in che modo toomanage li
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 93444c6f-af1b-41f8-a035-77f5c0302bf0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.openlocfilehash: 5abe1c59f2f3ed19bcf56c269dfe57ac32d4f601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a>Come un indirizzo IP privato interno statico tooset indirizzo tramite PowerShell (versione classica)
Nella maggior parte dei casi, non è necessario toospecify un indirizzo IP interno statico per la macchina virtuale. Le macchine virtuali in una rete virtuale infatti ricevono automaticamente un indirizzo IP interno da un intervallo specificato. In alcuni casi è tuttavia opportuno specificare un indirizzo IP statico per una determinata macchina virtuale, Ad esempio, se la macchina virtuale è corso toorun DNS o sarà un controller di dominio. Un indirizzo IP interno statico rimane associato hello VM anche attraverso un arresto o deprovisioning. 

> [!IMPORTANT]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Microsoft consiglia di utilizzano hello più nuove distribuzioni [il modello di distribuzione di gestione risorse](virtual-networks-static-private-ip-arm-ps.md).
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a>Come tooverify se è disponibile un indirizzo IP specifico
tooverify se hello indirizzo IP *10.0.0.7* è disponibile in una rete virtuale denominata *TestVnet*, eseguire il comando PowerShell seguente hello e verificare il valore di hello per *IsAvailable*:

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> Se si desidera tootest un comando di hello in precedenza in un ambiente sicuro, seguire le linee guida hello in [creare una rete virtuale (classico)](virtual-networks-create-vnet-classic-pportal.md) toocreate una rete virtuale denominata *TestVnet* e verificare che venga utilizzato hello  *10.0.0.0/8* lo spazio degli indirizzi.
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a>Come toospecify un indirizzo IP interno statico durante la creazione di una macchina virtuale
Hello script di PowerShell riportato di seguito crea un nuovo servizio cloud denominato *TestService*, quindi recupera un'immagine da Azure, quindi crea una macchina virtuale denominata *TestVM* in hello nuovo servizio cloud usando hello recuperato immagine, set di hello toobe macchina virtuale in una subnet denominata *Subnet-1*e imposta *10.0.0.7* come un indirizzo IP interno statico per hello VM:

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a>Come tooretrieve interne informazioni IP statici per una macchina virtuale
tooview hello interne informazioni IP statici per hello macchina virtuale creata con lo script hello precedente, eseguire il comando PowerShell seguente hello e osservare i valori hello per *IpAddress*:

    Get-AzureVM -Name TestVM -ServiceName TestService

    DeploymentName              : TestService
    Name                        : TestVM
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 10.0.0.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : TestVM
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : rsR2-797
    AvailabilitySetName         : 
    DNSName                     : http://testservice000.cloudapp.net/
    Status                      : Provisioning
    GuestAgentStatus            : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 
    PublicIPName                : 
    NetworkInterfaces           : {}
    ServiceName                 : TestService
    OperationDescription        : Get-AzureVM
    OperationId                 : 34c1560a62f0901ab75cde4fed8e8bd1
    OperationStatus             : OK

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a>Come tooremove un indirizzo IP interno statico da una macchina virtuale
tooremove hello indirizzo IP interno statico aggiunta toohello VM hello allo script precedente, eseguire il comando PowerShell seguente hello:

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a>Come tooadd un tooan IP interno statico macchina virtuale esistente
tooadd un toohello IP interno statico macchina virtuale creata utilizzando lo script hello sopra, Run il seguente comando:

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a>Passaggi successivi
[IP riservato](virtual-networks-reserved-public-ip.md)

[IP pubblico a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md)

[API REST di IP riservati](https://msdn.microsoft.com/library/azure/dn722420.aspx)

