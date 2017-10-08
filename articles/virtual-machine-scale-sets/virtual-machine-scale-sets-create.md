---
title: imposta una scala di macchina virtuale di Azure aaaCreate | Documenti Microsoft
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
ms.openlocfilehash: 73de25c1dd2424e64655b3accfea848926e72f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a>Creare e distribuire un set di scalabilità di macchine virtuali
Set di scalabilità di macchine virtuali semplificano automaticamente toodeploy e gestire macchine virtuali identiche come un set. I set di scalabilità offrono un livello di calcolo scalabile e personalizzabile per applicazioni con iperscalabilità e supportano le immagini della piattaforma Windows, le immagini della piattaforma Linux, le immagini personalizzate e le estensioni. Per altre informazioni sui set di scalabilità, vedere [Set di scalabilità di macchine virtuali](virtual-machine-scale-sets-overview.md).

Questa esercitazione viene illustrato come toocreate un scalabilità della macchina virtuale impostare **senza** utilizzando hello portale di Azure. Per informazioni su come toouse hello portale di Azure, vedere [come toocreate impostato di scalabilità di macchine virtuali con hello Azure portal](virtual-machine-scale-sets-portal-create.md).

>[!NOTE]
>Per altre informazioni sulle risorse di Azure Resource Manager, vedere [Confronto tra distribuzione di Azure Resource Manager e classica](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="sign-in-tooazure"></a>Accedi tooAzure

Se si utilizza l'interfaccia CLI di Azure 2.0 o Azure PowerShell toocreate una scala impostata, è innanzitutto necessario toosign nella sottoscrizione tooyour.

Per ulteriori informazioni su come tooinstall, configurare e accesso tooAzure con CLI di Azure o PowerShell, vedere [Introduzione a Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) o [Introduzione ai cmdlet di Azure PowerShell](/powershell/azure/overview).

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

È necessario innanzitutto toocreate è associato un gruppo di risorse che il set di scalabilità della macchina virtuale hello.

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a>Creare un set di scalabilità dall'interfaccia della riga di comando di Azure

Con l'interfaccia della riga di comando di Azure, è possibile creare facilmente un set di scalabilità di macchine virtuali. Se omessi, i valori predefiniti vengono forniti automaticamente. Ad esempio, se non si specificano le informazioni relative alla rete virtuale, ne verrà creata una automaticamente. Se si omette le seguenti parti hello, essi vengono creati automaticamente: 
- Un bilanciamento del carico
- Una rete virtuale
- Un indirizzo IP pubblico

Quando scelta hello immagine di macchina virtuale che si desidera toouse nel set di scalabilità della macchina virtuale hello, sono disponibili alcune opzioni:

- URN  
Identificatore Hello di una risorsa:  
**Win2012R2Datacenter**

- Alias URN  
nome descrittivo di Hello di un URN:  
**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**

- ID risorsa personalizzata  
Hello percorso tooan risorse di Azure:  
**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**

- Risorsa Web  
Hello percorso tooan URI HTTP:  
**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**

>[!TIP]
>È possibile ottenere un elenco di immagini disponibili con `az vm image list`.

toocreate set di scalabilità di macchine virtuali, è necessario specificare i seguenti hello:

- Gruppo di risorse 
- Nome
- Immagine del sistema operativo
- Informazioni di autenticazione 
 
Hello di esempio seguente crea un set di scalabilità della macchina virtuale di base (questa operazione potrebbe richiedere alcuni minuti).

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

Una volta terminato il comando hello si avranno ora la scalabilità della macchina virtuale creato. Potrebbe essere necessario l'indirizzo IP di hello tooget della macchina virtuale hello in modo che sia possibile connettersi tooit. È possibile ottenere numerose informazioni sui diversi sulla macchina virtuale hello (incluso l'indirizzo IP hello) con hello comando seguente. 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a>Creare un set di scalabilità da PowerShell

PowerShell è più complicato toouse di CLI di Azure. Mentre l'interfaccia della riga di comando di Azure fornisce automaticamente le opzioni predefinite per le risorse di rete (bilanciamenti del carico, indirizzi IP, reti virtuali), questo non avviene in PowerShell. Anche fare riferimento a un'immagine con PowerShell è leggermente più complicato. È possibile ottenere le immagini con hello seguente cmdlet:

1. Get-AzureRMVMImagePublisher
2. Get-AzureRMVMImageOffer
3. Get-AzureRmVMImageSku

può essere inoltrato tramite pipe Hello cmdlet funzionano in sequenza. Di seguito è riportato un esempio di come tooget tutte le immagini per hello **Stati Uniti occidentali 2** area con un server di pubblicazione con nome hello **microsoft** in essa contenuti.

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

flusso di lavoro di Hello per la creazione di un set di scalabilità della macchina virtuale è indicato di seguito:

1. Creare un oggetto di configurazione che contiene informazioni sui set di scalabilità hello.
2. Riferimento hello del sistema operativo immagine di base.
3. Configurare le impostazioni del sistema operativo hello: autenticazione, il prefisso del nome di macchina virtuale e utente/passaggio.
4. Configurare le impostazioni di rete.
5. Creare set di scalabilità hello.

Questo esempio consente di creare un set di scalabilità di base a due istanze per un computer con installato Windows Server 2016.

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create hello virtual network resources

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

# Attach hello virtual network toohello IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a>Usare un'immagine di macchina virtuale personalizzata
Se si sta creando una scala impostato da un'immagine personalizzata, anziché fare riferimento a un'immagine di macchina virtuale da raccolta hello, hello _Set AzureRmVmssStorageProfile_ comando è analogo al seguente:
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a>Creare un set di scalabilità da un modello

È possibile distribuire un set di scalabilità di macchine virtuali usando un modello di Azure Resource Manager. È possibile creare un modello personalizzato o usarne uno dal hello [repository modello](https://azure.microsoft.com/resources/templates/?term=vmss). Questi modelli possono essere distribuiti direttamente tooyour sottoscrizione di Azure.

>[!NOTE]
>toocreate un modello personalizzato, si crea un file di testo JSON. Per informazioni generali su come toocreate e personalizzare un modello, vedere [modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Un modello di esempio è disponibile [in GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set). Per ulteriori informazioni su come toocreate e usare tale esempio, vedere [set vitali di scala minimo](.\virtual-machine-scale-sets-mvss-start.md).

## <a name="create-from-visual-studio"></a>Creare un set di scalabilità da Visual Studio

Con Visual Studio, è possibile creare un progetto di gruppo di risorse di Azure e aggiungere che un scalabilità della macchina virtuale impostata tooit modello. È possibile scegliere se si desidera tooimport da GitHub o hello raccolta applicazioni Web di Azure. Viene inoltre generato automaticamente uno script di PowerShell per la distribuzione. Per ulteriori informazioni, vedere [come toocreate set di scalabilità di macchine virtuali con Visual Studio](virtual-machine-scale-sets-vs-create.md).

## <a name="create-from-hello-azure-portal"></a>Il nome di hello portale di Azure

Hello portale di Azure fornisce un modo pratico tooquickly creare un set di scalabilità. Per ulteriori informazioni, vedere [come toocreate impostato di scalabilità di macchine virtuali con hello Azure portal](virtual-machine-scale-sets-portal-create.md).

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni su [dischi dati](virtual-machine-scale-sets-attached-disks.md).

Informazioni su come troppo[gestire le app](virtual-machine-scale-sets-deploy-app.md).
