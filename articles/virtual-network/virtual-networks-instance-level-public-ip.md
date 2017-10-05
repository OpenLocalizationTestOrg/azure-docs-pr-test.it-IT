---
title: Indirizzi IP pubblici a livello di istanza di Azure (classico) | Microsoft Docs
description: Informazioni sugli IP pubblici a livello di istanza (ILPIP) e su come gestirli tramite PowerShell.
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
ms.openlocfilehash: 773043f2841ec7539b0d49357dec6bcb9f4f78a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="instance-level-public-ip-classic-overview"></a><span data-ttu-id="95806-103">Panoramica sugli indirizzi IP pubblici (classici) a livello di istanza</span><span class="sxs-lookup"><span data-stu-id="95806-103">Instance level public IP (Classic) overview</span></span>
<span data-ttu-id="95806-104">Un indirizzo IP pubblico a livello di istanza (ILPIP) è un indirizzo IP pubblico che è possibile assegnare direttamente all'istanza del ruolo della macchina virtuale o dei servizi cloud in cui risiede l'istanza del ruolo o la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="95806-104">An instance level public IP (ILPIP) is a public IP address that you can assign directly to a VM or Cloud Services role instance, rather than to the cloud service that your VM or role instance reside in.</span></span> <span data-ttu-id="95806-105">Un ILPIP non sostituisce l'indirizzo IP virtuale (VIP) assegnato al servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="95806-105">An ILPIP doesn’t take the place of the virtual IP (VIP) that is assigned to your cloud service.</span></span> <span data-ttu-id="95806-106">Piuttosto, si tratta di un indirizzo IP aggiuntivo che è possibile usare per connettersi direttamente all'istanza della macchina virtuale o del ruolo.</span><span class="sxs-lookup"><span data-stu-id="95806-106">Rather, it’s an additional IP address that you can use to connect directly to your VM or role instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="95806-107">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="95806-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="95806-108">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="95806-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="95806-109">Si consiglia di creare macchine virtuali tramite Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="95806-109">Microsoft recommends creating VMs through Resource Manager.</span></span> <span data-ttu-id="95806-110">Verificare di conoscere il funzionamento degli [indirizzi IP](virtual-network-ip-addresses-overview-classic.md) in Azure.</span><span class="sxs-lookup"><span data-stu-id="95806-110">Make sure you understand how [IP addresses](virtual-network-ip-addresses-overview-classic.md) work in Azure.</span></span>

![Differenza tra ILPIP e VIP](./media/virtual-networks-instance-level-public-ip/Figure1.png)

<span data-ttu-id="95806-112">Come illustrato nella figura 1, al servizio cloud si accede tramite un indirizzo VIP, mentre alle singole macchine virtuali si accede in genere tramite VIP:&lt;numero di porta&gt;.</span><span class="sxs-lookup"><span data-stu-id="95806-112">As shown in Figure 1, the cloud service is accessed using a VIP, while the individual VMs are normally accessed using VIP:&lt;port number&gt;.</span></span> <span data-ttu-id="95806-113">Assegnando un ILPIP a una macchina virtuale specifica, è possibile accedere a questa macchina virtuale direttamente tramite l’indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="95806-113">By assigning an ILPIP to a specific VM, that VM can be accessed directly using that IP address.</span></span>

<span data-ttu-id="95806-114">Quando si crea un servizio cloud in Azure, i record A DNS corrispondenti vengono creati automaticamente per consentire l'accesso al servizio tramite un nome di dominio completo (FQDN) anziché tramite l'indirizzo VIP effettivo.</span><span class="sxs-lookup"><span data-stu-id="95806-114">When you create a cloud service in Azure, corresponding DNS A records are created automatically to allow access to the service through a fully qualified domain name (FQDN), instead of using the actual VIP.</span></span> <span data-ttu-id="95806-115">Lo stesso processo si verifica per un ILPIP, che consente l'accesso all'istanza della macchina virtuale o del ruolo mediante FQDN anziché ILPIP.</span><span class="sxs-lookup"><span data-stu-id="95806-115">The same process happens for an ILPIP, allowing access to the VM or role instance by FQDN instead of the ILPIP.</span></span> <span data-ttu-id="95806-116">Se ad esempio si crea un servizio cloud denominato *contosoadservice* e si configura un ruolo Web denominato *contosoweb* con due istanze, Azure registra per le istanze i record A seguenti:</span><span class="sxs-lookup"><span data-stu-id="95806-116">For instance, if you create a cloud service named *contosoadservice*, and you configure a web role named *contosoweb* with two instances, Azure registers the following A records for the instances:</span></span>

* <span data-ttu-id="95806-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="95806-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span></span>
* <span data-ttu-id="95806-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="95806-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span></span> 

> [!NOTE]
> <span data-ttu-id="95806-119">È possibile assegnare un solo ILPIP per ogni istanza di macchina virtuale o ruolo.</span><span class="sxs-lookup"><span data-stu-id="95806-119">You can assign only one ILPIP for each VM or role instance.</span></span> <span data-ttu-id="95806-120">È possibile usare fino a 5 ILPIP per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="95806-120">You can use up to 5 ILPIPs per subscription.</span></span> <span data-ttu-id="95806-121">Gli ILPIP non sono supportati per le macchine virtuali a più NIC.</span><span class="sxs-lookup"><span data-stu-id="95806-121">ILPIPs are not supported for multi-NIC VMs.</span></span>
> 
> 

## <a name="why-would-i-request-an-ilpip"></a><span data-ttu-id="95806-122">Perché è necessario richiedere un ILPIP?</span><span class="sxs-lookup"><span data-stu-id="95806-122">Why would I request an ILPIP?</span></span>
<span data-ttu-id="95806-123">Se si desidera connettersi all'istanza della VM o del ruolo tramite un indirizzo IP assegnato direttamente all'istanza, anziché usare il servizio cloud VIP:&lt;numero porta&gt;, richiedere un ILPIP per l'istanza della VM o del ruolo.</span><span class="sxs-lookup"><span data-stu-id="95806-123">If you want to be able to connect to your VM or role instance by an IP address assigned directly to it, rather than using the cloud service VIP:&lt;port number&gt;, request an ILPIP for your VM or your role instance.</span></span>

* <span data-ttu-id="95806-124">**FTP attivo**: assegnando un ILPIP a una macchina virtuale è possibile che questa riceva il traffico su qualsiasi porta.</span><span class="sxs-lookup"><span data-stu-id="95806-124">**Active FTP** - By assigning an ILPIP to a VM, it can receive traffic on any port.</span></span> <span data-ttu-id="95806-125">Gli endpoint non sono necessari per la macchina virtuale affinché questa riceva il traffico.</span><span class="sxs-lookup"><span data-stu-id="95806-125">Endpoints are not required for the VM to receive traffic.</span></span>  <span data-ttu-id="95806-126">Per informazioni dettagliate sul protocollo FTP, vedere la (https://it.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[panoramica del protocollo FTP].</span><span class="sxs-lookup"><span data-stu-id="95806-126">See (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[FTP Protocol Overview] for details on the FTP protocol.</span></span>
* <span data-ttu-id="95806-127">**IP in uscita**: viene eseguito il mapping del traffico in uscita proveniente dalla macchina virtuale all'ILPIP come origine e l'ILPIP identifica in modo univoco la macchina virtuale sulle entità esterne.</span><span class="sxs-lookup"><span data-stu-id="95806-127">**Outbound IP** - Outbound traffic originating from the VM is mapped to the ILPIP as the source and the ILPIP uniquely identifies the VM to external entities.</span></span>

> [!NOTE]
> <span data-ttu-id="95806-128">In passato, un indirizzo ILPIP veniva definito indirizzo IP pubblico (PIP).</span><span class="sxs-lookup"><span data-stu-id="95806-128">In the past, an ILPIP address was referred to as a public IP (PIP) address.</span></span>
> 

## <a name="manage-an-ilpip-for-a-vm"></a><span data-ttu-id="95806-129">Gestire un ILPIP per una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="95806-129">Manage an ILPIP for a VM</span></span>
<span data-ttu-id="95806-130">Le attività seguenti consentono di creare, assegnare e rimuovere gli ILPIP dalle macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="95806-130">The following tasks enable you to create, assign, and remove ILPIPs from VMs:</span></span>

### <a name="how-to-request-an-ilpip-during-vm-creation-using-powershell"></a><span data-ttu-id="95806-131">Come richiedere un ILPIP durante la creazione della macchina virtuale mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="95806-131">How to request an ILPIP during VM creation using PowerShell</span></span>
<span data-ttu-id="95806-132">Lo script di PowerShell riportato di seguito crea un nuovo servizio cloud denominato *FTPService*, recupera un'immagine da Azure, crea una macchina virtuale denominata *FTPInstance* usando l'immagine recuperata, imposta la macchina virtuale per usare un ILPIP e aggiunge la macchina virtuale al nuovo servizio:</span><span class="sxs-lookup"><span data-stu-id="95806-132">The following PowerShell script creates a cloud service named *FTPService*, retrieves an image from Azure, creates a VM named *FTPInstance* using the retrieved image, sets the VM to use an ILPIP, and adds the VM to the new service:</span></span>

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-to-retrieve-ilpip-information-for-a-vm"></a><span data-ttu-id="95806-133">Come recuperare informazioni su ILPIP per una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="95806-133">How to retrieve ILPIP information for a VM</span></span>
<span data-ttu-id="95806-134">Per visualizzare le informazioni su ILPIP per la macchina virtuale creata con lo script precedente, eseguire il comando di PowerShell seguente e osservare i valori per *PublicIPAddress* e *PublicIPName*:</span><span class="sxs-lookup"><span data-stu-id="95806-134">To view the ILPIP information for the VM created with the previous script, run the following PowerShell command and observe the values for *PublicIPAddress* and *PublicIPName*:</span></span>

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

<span data-ttu-id="95806-135">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="95806-135">Expected output:</span></span>
 
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

### <a name="how-to-remove-an-ilpip-from-a-vm"></a><span data-ttu-id="95806-136">Come rimuovere un ILPIP da una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="95806-136">How to remove an ILPIP from a VM</span></span>
<span data-ttu-id="95806-137">Per rimuovere un ILPIP aggiunto alla macchina virtuale nello script precedente, eseguire il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="95806-137">To remove the ILPIP added to the VM in the previous script, run the following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-to-add-an-ilpip-to-an-existing-vm"></a><span data-ttu-id="95806-138">Come aggiungere un ILPIP a una macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="95806-138">How to add an ILPIP to an existing VM</span></span>
<span data-ttu-id="95806-139">Per aggiungere un ILPIP alla macchina virtuale creata usando lo script precedente, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="95806-139">To add an ILPIP to the VM created using the script previous, run the following command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a><span data-ttu-id="95806-140">Gestire un ILPIP per un'istanza del ruolo del servizi cloud</span><span class="sxs-lookup"><span data-stu-id="95806-140">Manage an ILPIP for a Cloud Services role instance</span></span>

<span data-ttu-id="95806-141">Per aggiungere un ILPIP a un'istanza del ruolo dei servizi cloud, completare i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="95806-141">To add an ILPIP to a Cloud Services role instance, complete the following steps:</span></span>

1. <span data-ttu-id="95806-142">Scaricare il file con estensione CSCFG per il servizio cloud completando la procedura nell'articolo [Come configurare i servizi cloud](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg).</span><span class="sxs-lookup"><span data-stu-id="95806-142">Download the .cscfg file for the cloud service by completing the steps in the [How to Configure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>
2. <span data-ttu-id="95806-143">Aggiornare il file con estensione CSCFG aggiungendo l'elemento `InstanceAddress`.</span><span class="sxs-lookup"><span data-stu-id="95806-143">Update the .cscfg file by adding the `InstanceAddress` element.</span></span> <span data-ttu-id="95806-144">Nell'esempio seguente viene aggiunto un ILPIP denominato *MyPublicIP* a un'istanza di ruolo denominata *WebRole1*:</span><span class="sxs-lookup"><span data-stu-id="95806-144">The following sample adds an ILPIP named *MyPublicIP* to a role instance named *WebRole1*:</span></span> 

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
3. <span data-ttu-id="95806-145">Caricare il file con estensione CSCFG per il servizio cloud completando la procedura nell'articolo [Come configurare i servizi cloud](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg).</span><span class="sxs-lookup"><span data-stu-id="95806-145">Upload the .cscfg file for the cloud service by completing the steps in the [How to Configure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95806-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="95806-146">Next steps</span></span>
* <span data-ttu-id="95806-147">Informazioni sul funzionamento degli [indirizzi IP](virtual-network-ip-addresses-overview-classic.md) nel modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="95806-147">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in the classic deployment model.</span></span>
* <span data-ttu-id="95806-148">Informazioni sugli [indirizzi IP riservati](virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="95806-148">Learn about [Reserved IPs](virtual-networks-reserved-public-ip.md).</span></span>
