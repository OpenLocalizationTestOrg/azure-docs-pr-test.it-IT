---
title: gli indirizzi IP pubblico (versione classica) aaaAzure a livello di istanza | Documenti Microsoft
description: Informazioni istanza livello IP (ILPIP) gli indirizzi pubblici e come toomanage loro tramite PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 07eef6ec-7dfe-4c4d-a2c2-be0abfb48ec5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: 832143ee6fdd80b634e1cebfddc759a8cacda583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="instance-level-public-ip-classic-overview"></a>Panoramica sugli indirizzi IP pubblici (classici) a livello di istanza
Un'istanza livello IP pubblico (ILPIP) è un indirizzo IP pubblico che è possibile assegnare direttamente tooa istanza del ruolo VM o i servizi Cloud, anziché come servizio cloud toohello che l'istanza del ruolo o macchine Virtuali si trovano in. Un ILPIP non avranno luogo hello di hello indirizzo IP virtuale (VIP) del servizio cloud tooyour assegnato. Si tratta piuttosto di un indirizzo IP aggiuntivo che è possibile utilizzare tooconnect direttamente tooyour macchina virtuale o istanza di ruolo.

> [!IMPORTANT]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di creare macchine virtuali tramite Resource Manager. Verificare di conoscere il funzionamento degli [indirizzi IP](virtual-network-ip-addresses-overview-classic.md) in Azure.

![Differenza tra ILPIP e VIP](./media/virtual-networks-instance-level-public-ip/Figure1.png)

Come illustrato nella figura 1, si accede utilizzando un indirizzo VIP di servizio cloud hello, mentre hello singole macchine virtuali in genere è possibile accedere tramite VIP:&lt;il numero di porta&gt;. Assegnando un tooa ILPIP macchina virtuale specifica, che possono essere VM accessibili direttamente tramite l'indirizzo IP.

Quando si crea un servizio cloud in Azure, i record DNS A corrispondenti vengono creati automaticamente servizio di toohello tooallow accesso tramite un nome di dominio completo (FQDN), anziché hello effettivo VIP. Hello stesso processo si verifica per un ILPIP, consentendo l'accesso toohello macchina virtuale o istanza di ruolo di dominio completo anziché hello ILPIP. Ad esempio, se si crea un servizio cloud denominato *contosoadservice*, e si configura un ruolo web denominato *contosoweb* con due istanze, hello Azure registri dopo un record per le istanze di hello:

* contosoweb\_IN_0.contosoadservice.cloudapp.net
* contosoweb\_IN_1.contosoadservice.cloudapp.net 

> [!NOTE]
> È possibile assegnare un solo ILPIP per ogni istanza di macchina virtuale o ruolo. È possibile utilizzare backup ILPIPs too5 per ogni sottoscrizione. Gli ILPIP non sono supportati per le macchine virtuali a più NIC.
> 
> 

## <a name="why-would-i-request-an-ilpip"></a>Perché è necessario richiedere un ILPIP?
Se si desidera toobe tooconnect in grado di tooyour macchina virtuale o istanza del ruolo da un indirizzo IP assegnato direttamente tooit, anziché utilizzare cloud hello indirizzo VIP del servizio:&lt;il numero di porta&gt;, richiedere un ILPIP per la macchina virtuale o l'istanza del ruolo.

* **FTP Active** -assegnando un tooa ILPIP macchina virtuale, può ricevere traffico su qualsiasi porta. Endpoint non sono necessari per hello tooreceive traffico delle macchine Virtuali.  Per informazioni sul protocollo hello FTP, vedere [Panoramica del protocollo FTP] (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview).
* **IP in uscita** : il traffico in uscita proveniente da hello macchina virtuale è stato eseguito il mapping toohello ILPIP come origine di hello e hello ILPIP identifica in modo univoco le entità di tooexternal VM hello.

> [!NOTE]
> In hello precedente, un indirizzo ILPIP era tooas di cui si fa riferimento un indirizzo IP (PIP) pubblico.
> 

## <a name="manage-an-ilpip-for-a-vm"></a>Gestire un ILPIP per una macchina virtuale
Hello seguenti attività consentono di toocreate, assegnare e rimuovere ILPIPs da macchine virtuali:

### <a name="how-toorequest-an-ilpip-during-vm-creation-using-powershell"></a>Come toorequest un ILPIP durante la creazione della macchina virtuale con PowerShell
Hello lo script di PowerShell seguente crea un servizio cloud denominato *FTP*, recupera un'immagine da Azure, crea una macchina virtuale denominata *FTPInstance* immagine hello recuperato, imposta hello VM toouse un ILPIP, e aggiunge hello VM toohello nuovo servizio:

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-tooretrieve-ilpip-information-for-a-vm"></a>Modalità informazioni ILPIP tooretrieve per una macchina virtuale
hello tooview ILPIP informazioni hello creata con hello script precedente per la macchina virtuale eseguire il comando PowerShell seguente hello e osservare i valori hello per *PublicIPAddress* e *PublicIPName*:

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

Output previsto:
 
    DeploymentName              : FTPService
    Name                        : FTPInstance
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : ReadyRole
    IpAddress                   : 100.74.118.91
    InstanceStateDetails        : 
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : FTPInstance
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : FTPInstance
    AvailabilitySetName         : 
    DNSName                     : http://ftpservice888.cloudapp.net/
    Status                      : ReadyRole
    GuestAgentStatus            :   Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 104.43.142.188
    PublicIPName                : ftpip
    NetworkInterfaces           : {}
    ServiceName                 : FTPService
    OperationDescription        : Get-AzureVM
    OperationId                 : 568d88d2be7c98f4bbb875e4d823718e
    OperationStatus             : OK

### <a name="how-tooremove-an-ilpip-from-a-vm"></a>Come tooremove un ILPIP da una macchina virtuale
hello tooremove ILPIP aggiunto toohello VM hello script precedente per eseguire il comando PowerShell seguente hello:

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-tooadd-an-ilpip-tooan-existing-vm"></a>Come un tooan ILPIP tooadd macchina virtuale esistente
tooadd un toohello ILPIP macchina virtuale creata utilizzando lo script hello precedente, eseguire hello comando seguente:

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a>Gestire un ILPIP per un'istanza del ruolo del servizi cloud

tooadd un'istanza del ruolo ILPIP tooa servizi Cloud, hello completo alla procedura seguente:

1. Scaricare i file con estensione cscfg hello per i passaggi del servizio cloud hello completando hello in hello [come servizi Cloud tooConfigure](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) articolo.
2. File con estensione cscfg di hello aggiornamento aggiungendo hello `InstanceAddress` elemento. Hello seguente esempio viene aggiunto un ILPIP denominato *MyPublicIP* tooa istanza del ruolo denominato *WebRole1*: 

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ILPIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
          <ConfigurationSettings>
        <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
          </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <InstanceAddress roleName="WebRole1">
        <PublicIPs>
          <PublicIP name="MyPublicIP" domainNameLabel="MyPublicIP" />
            </PublicIPs>
          </InstanceAddress>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>
    ```
3. Caricare file con estensione cscfg hello per i passaggi del servizio cloud hello completando hello in hello [come servizi Cloud tooConfigure](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) articolo.

## <a name="next-steps"></a>Passaggi successivi
* Comprendere come [gli indirizzi IP](virtual-network-ip-addresses-overview-classic.md) funziona nel modello di distribuzione classica hello.
* Informazioni sugli [indirizzi IP riservati](virtual-networks-reserved-public-ip.md).
