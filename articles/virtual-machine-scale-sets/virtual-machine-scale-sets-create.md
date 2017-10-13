---
title: "Creare un set di scalabilità di macchine virtuali di Azure | Microsoft Docs"
description: "Creare e distribuire un set di scalabilità di macchine virtuali Linux o Windows Azure con l'interfaccia della riga di comando di Azure, PowerShell, un modello o Visual Studio."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 07/21/2017
ms.author: adegeo
ms.openlocfilehash: 32af01aa545c541688128a7ae6bbb82a0e046f2d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a>Creare e distribuire un set di scalabilità di macchine virtuali
I set di scalabilità di macchine virtuali semplificano la distribuzione e la gestione di macchine virtuali identiche come un set. I set di scalabilità offrono un livello di calcolo scalabile e personalizzabile per applicazioni con iperscalabilità e supportano le immagini della piattaforma Windows, le immagini della piattaforma Linux, le immagini personalizzate e le estensioni. Per altre informazioni sui set di scalabilità, vedere [Set di scalabilità di macchine virtuali](virtual-machine-scale-sets-overview.md).

Questa esercitazione mostra come creare un set di scalabilità di macchine virtuali **senza** usare il portale di Azure. Per informazioni su come usare il portale di Azure, vedere [Come creare un set di scalabilità di macchine virtuali tramite il portale di Azure](virtual-machine-scale-sets-portal-create.md).

>[!NOTE]
>Per altre informazioni sulle risorse di Azure Resource Manager, vedere [Confronto tra distribuzione di Azure Resource Manager e classica](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="sign-in-to-azure"></a>Accedere ad Azure

Se si usa l'interfaccia della riga di comando di Azure 2.0 o Azure PowerShell per creare un set di scalabilità, per prima cosa è necessario accedere alla propria sottoscrizione.

Per altre informazioni su come installare, configurare e accedere ad Azure con l'interfaccia della riga di comando di Azure o con PowerShell, vedere [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) (Introduzione all'interfaccia della riga di comando di Azure 2.0) o [Get started with Azure PowerShell cmdlets](/powershell/azure/overview) (Introduzione ai cmdlet di Azure PowerShell).

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Per prima cosa è necessario creare un gruppo di risorse a cui sia associato il set di scalabilità di macchine virtuali.

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a>Creare un set di scalabilità dall'interfaccia della riga di comando di Azure

Con l'interfaccia della riga di comando di Azure, è possibile creare facilmente un set di scalabilità di macchine virtuali. Se omessi, i valori predefiniti vengono forniti automaticamente. Ad esempio, se non si specificano le informazioni relative alla rete virtuale, ne verrà creata una automaticamente. Se si omettono le parti seguenti, queste verranno create: 
- Un bilanciamento del carico
- Una rete virtuale
- Un indirizzo IP pubblico

Quando si sceglie l'immagine della macchina virtuale da usare nel set di scalabilità di macchine virtuali, sono disponibili alcune opzioni:

- URN  
L'identificatore di una risorsa:  
**Win2012R2Datacenter**

- Alias URN  
Il nome descrittivo di un URN:  
**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**

- ID risorsa personalizzata  
Il percorso di una risorsa di Azure:  
**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**

- Risorsa Web  
Il percorso di un URI HTTP:  
**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**

>[!TIP]
>È possibile ottenere un elenco di immagini disponibili con `az vm image list`.

Per creare un set di scalabilità di macchine virtuali, è necessario specificare quanto segue:

- Resource group 
- Nome
- Immagine del sistema operativo
- Informazioni di autenticazione 
 
L'esempio seguente crea un set di scalabilità di macchine virtuali di base (questo passaggio può richiedere alcuni minuti).

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

Dopo il completamento del comando il set di scalabilità di macchine virtuali è stato creato. Potrebbe essere necessario ottenere l'indirizzo IP della macchina virtuale per stabilire la connessione. È possibile ottenere varie informazioni relative alla macchina virtuale (incluso l'indirizzo IP) con il comando seguente. 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a>Creare un set di scalabilità da PowerShell

PowerShell è più complicato da usare rispetto all'interfaccia della riga di comando di Azure. Mentre l'interfaccia della riga di comando di Azure fornisce automaticamente le opzioni predefinite per le risorse di rete (bilanciamenti del carico, indirizzi IP, reti virtuali), questo non avviene in PowerShell. Anche fare riferimento a un'immagine con PowerShell è leggermente più complicato. È possibile ottenere immagini con i cmdlet seguenti:

1. Get-AzureRMVMImagePublisher
2. Get-AzureRMVMImageOffer
3. Get-AzureRmVMImageSku

Il lavoro dei cmdlet può essere reindirizzato in sequenza. Di seguito è riportato un esempio di come ottenere tutte le immagini per l'area **West US 2** (Stati Uniti occidentali 2) il cui nome dell'editore contiene **microsoft**.

```powershell
Get-AzureRMVMImagePublisher -Location WestUS2 | Where-Object PublisherName -Like *microsoft* | Get-AzureRMVMImageOffer | Get-AzureRmVMImageSku | Select-Object PublisherName, Offer, Skus
```

```
PublisherName              Offer                    Skus
-------------              -----                    ----
microsoft-ads              linux-data-science-vm    linuxdsvm
microsoft-ads              standard-data-science-vm standard-data-science-vm
MicrosoftAzureSiteRecovery Process-Server           Windows-2012-R2-Datacenter
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Enterprise
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Standard
MicrosoftBizTalkServer     BizTalk-Server           2016-Developer
MicrosoftBizTalkServer     BizTalk-Server           2016-Enterprise
...
```

Il flusso di lavoro per la creazione di un set di scalabilità di macchine virtuali è il seguente:

1. Creare un oggetto di configurazione contenente informazioni sul set di scalabilità.
2. Fare riferimento all'immagine del sistema operativo di base.
3. Configurare le impostazioni del sistema operativo: autenticazione, prefisso del nome della VM e utente/password.
4. Configurare le impostazioni di rete.
5. Creare il set di scalabilità.

Questo esempio consente di creare un set di scalabilità di base a due istanze per un computer con installato Windows Server 2016.

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from the gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with the virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create the virtual network resources

## Basics
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name "my-subnet" -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name "my-network" -ResourceGroupName $rg -Location $location -AddressPrefix 10.0.0.0/16 -Subnet $subnet

## Load balancer
$publicIP = New-AzureRmPublicIpAddress -Name "PublicIP" -ResourceGroupName $rg -Location $location -AllocationMethod Static -DomainNameLabel "myuniquedomain"
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontend" -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
$probe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
$inboundNATRule1= New-AzureRmLoadBalancerRuleConfig -Name "webserver" -FrontendIpConfiguration $frontendIP -Protocol Tcp -FrontendPort 80 -BackendPort 80 -IdleTimeoutInMinutes 15 -Probe $probe -BackendAddressPool $backendPool
$inboundNATPool1 = New-AzureRmLoadBalancerInboundNatPoolConfig -Name "RDP" -FrontendIpConfigurationId $frontendIP.Id -Protocol TCP -FrontendPortRangeStart 53380 -FrontendPortRangeEnd 53390 -BackendPort 3389

New-AzureRmLoadBalancer -ResourceGroupName $rg -Name "LB1" -Location $location -FrontendIpConfiguration $frontendIP -LoadBalancingRule $inboundNATRule1 -InboundNatPool $inboundNATPool1 -BackendAddressPool $backendPool -Probe $probe

## IP address config
$ipConfig = New-AzureRmVmssIpConfig -Name "my-ipaddress" -LoadBalancerBackendAddressPoolsId $backendPool.Id -SubnetId $vnet.Subnets[0].Id -LoadBalancerInboundNatPoolsId $inboundNATPool1.Id

# Attach the virtual network to the IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create the scale set with the config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a>Usare un'immagine di macchina virtuale personalizzata
Se si sta creando un set di scalabilità da un'immagine personalizzata anziché fare riferimento a un'immagine di macchina virtuale dalla raccolta, il comando _Set AzureRmVmssStorageProfile_ avrà l'aspetto seguente:
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a>Creare un set di scalabilità da un modello

È possibile distribuire un set di scalabilità di macchine virtuali usando un modello di Azure Resource Manager. È possibile creare un modello personalizzato o usarne uno del [repository di modelli](https://azure.microsoft.com/resources/templates/?term=vmss). Questi modelli possono essere distribuiti direttamente alla sottoscrizione di Azure.

>[!NOTE]
>Per creare un modello personalizzato, si crea un file di testo JSON. Per informazioni generali su come creare e personalizzare un modello, vedere [Modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Un modello di esempio è disponibile [in GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set). Per altre informazioni su come creare e usare tale esempio, vedere [Un set di scalabilità a validità minima](.\virtual-machine-scale-sets-mvss-start.md).

## <a name="create-from-visual-studio"></a>Creare un set di scalabilità da Visual Studio

Con Visual Studio, è possibile creare un progetto del gruppo di risorse di Azure e aggiungervi un modello di set di scalabilità di macchine virtuali. È possibile scegliere se si desidera eseguire l'importazione da GitHub o dalla raccolta di applicazioni Web di Azure. Viene inoltre generato automaticamente uno script di PowerShell per la distribuzione. Per altre informazioni, vedere [Come creare un set di scalabilità di macchine virtuali con Visual Studio](virtual-machine-scale-sets-vs-create.md).

## <a name="create-from-the-azure-portal"></a>Creare un set di scalabilità dal portale di Azure

Il portale di Azure costituisce un modo semplice per creare rapidamente un set di scalabilità. Per altre informazioni, vedere [Come creare un set di scalabilità di macchine virtuali tramite il portale di Azure](virtual-machine-scale-sets-portal-create.md).

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni su [dischi dati](virtual-machine-scale-sets-attached-disks.md).

Informazioni su come [gestire le app](virtual-machine-scale-sets-deploy-app.md).
