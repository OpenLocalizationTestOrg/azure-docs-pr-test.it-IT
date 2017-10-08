---
title: indirizzi IP privati aaaConfigure per le macchine virtuali (classico) - Azure PowerShell | Documenti Microsoft
description: Informazioni su come di indirizzi IP privati tooconfigure per le macchine virtuali (classico) tramite PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 60c7b489-46ae-48af-a453-2b429a474afd
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 99546ee9c2c4eb9aa7b67f30721d37ef9b2944f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-powershell"></a>Configurare indirizzi IP privati per una macchina virtuale (classica) mediante PowerShell

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Questo articolo descrive il modello di distribuzione classica hello. È anche possibile [gestire un indirizzo IP privato statico nel modello di distribuzione di gestione risorse di hello](virtual-networks-static-private-ip-arm-ps.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

Hello comandi di esempio PowerShell riportato di seguito prevedono un ambiente semplice già creato. Se si desidera comandi hello toorun così come sono visualizzati in questo documento, innanzitutto compilare descritto nell'ambiente di test di hello [creare una rete virtuale](virtual-networks-create-vnet-classic-netcfg-ps.md).

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a>Come tooverify se è disponibile un indirizzo IP specifico
tooverify se hello indirizzo IP *192.168.1.101* è disponibile in una rete virtuale denominata *TestVNet*, eseguire il comando PowerShell seguente hello e verificare il valore di hello per *IsAvailable*:

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 192.168.1.101 

Output previsto:

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>Come toospecify un indirizzo IP privato statico di indirizzi durante la creazione di una macchina virtuale
Hello script di PowerShell riportato di seguito crea un nuovo servizio cloud denominato *TestService*, quindi recupera un'immagine da Azure, crea una macchina virtuale denominata *DNS01* in hello nuovo servizio cloud usando hello recuperato immagine, imposta Hello toobe macchina virtuale in una subnet denominata *front-end*e imposta *192.168.1.7* come un indirizzo IP privato statico per hello VM:

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage | where {$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name DNS01 -InstanceSize Small -ImageName $image.ImageName |
      Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! |
      Set-AzureSubnet –SubnetNames FrontEnd |
      Set-AzureStaticVNetIP -IPAddress 192.168.1.7 |
      New-AzureVM -ServiceName TestService –VNetName TestVNet

Output previsto:

    WARNING: No deployment found in service: 'TestService'.
    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    New-AzureService     fcf705f1-d902-011c-95c7-b690735e7412 Succeeded      
    New-AzureVM          3b99a86d-84f8-04e5-888e-b6fc3c73c4b9 Succeeded  

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Come indirizzo IP privato statico tooretrieve informazioni sull'indirizzo di una macchina virtuale
IP privato statico di tooview hello informazioni sull'indirizzo di hello macchina virtuale creata con lo script hello precedente, eseguire il comando PowerShell seguente hello e osservare i valori hello per *IpAddress*:

    Get-AzureVM -Name DNS01 -ServiceName TestService

Output previsto:

    DeploymentName              : TestService
    Name                        : DNS01
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 192.168.1.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : DNS01
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

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Come tooremove un indirizzo IP privato statico di indirizzi da una macchina virtuale
tooremove hello indirizzo IP privato statico aggiunta toohello VM hello allo script precedente, hello esecuzione comando PowerShell seguente:

    Get-AzureVM -ServiceName TestService -Name DNS01 |
      Remove-AzureStaticVNetIP |
      Update-AzureVM

Output previsto:

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Update-AzureVM       052fa6f6-1483-0ede-a7bf-14f91f805483 Succeeded

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Come un indirizzo IP privato statico tooadd indirizzo tooan macchina virtuale esistente
tooadd un statico privato IP indirizzo toohello macchina virtuale creata utilizzando lo script hello sopra, Run il seguente comando:

    Get-AzureVM -ServiceName TestService -Name DNS01 |
      Set-AzureStaticVNetIP -IPAddress 192.168.1.7 |
      Update-AzureVM

Output previsto:

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Update-AzureVM       77d8cae2-87e6-0ead-9738-7c7dae9810cb Succeeded 

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su [indirizzi IP pubblici riservati](virtual-networks-reserved-public-ip.md) .
* Informazioni su [indirizzi IP pubblici a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md) .
* Consultare hello [API REST per IP riservato](https://msdn.microsoft.com/library/azure/dn722420.aspx).

