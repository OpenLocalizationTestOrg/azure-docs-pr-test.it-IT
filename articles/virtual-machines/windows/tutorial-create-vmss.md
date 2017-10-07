---
title: una macchina virtuale scala set per Windows in Azure aaaCreate | Documenti Microsoft
description: "Creare e distribuire un'applicazione a disponibilità elevata in VM Windows usando un set di scalabilità di macchine virtuali"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: 
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: a3914571005c28a492c069d880992630851afae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a>Creare un set di scalabilità di macchine virtuali e distribuire un'app a disponibilità elevata in Windows
Un set di scalabilità della macchina virtuale consente toodeploy e gestire un set di macchine virtuali identiche e la scalabilità automatica. È possibile ridimensionare manualmente numero hello di macchine virtuali nel set di scalabilità hello o definire tooautoscale regole in base all'utilizzo della CPU, la richiesta di memoria o il traffico di rete. In questa esercitazione viene distribuito un set di scalabilità di macchine virtuali in Azure. Si apprenderà come:

> [!div class="checklist"]
> * Utilizzare toodefine estensione Script personalizzata hello un tooscale del sito IIS
> * Creare un bilanciamento del carico per il set di scalabilità
> * Creare un set di scalabilità di macchine virtuali
> * Aumentare o diminuire il numero di hello di istanze in un set di scalabilità
> * Creare regole di scalabilità automatica

Questa esercitazione richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo. Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind. Se è necessario tooupgrade, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).


## <a name="scale-set-overview"></a>Informazioni generali sui set di scalabilità
Set di scalabilità di utilizzare concetti simili come sono state descritte nell'esercitazione precedente hello troppo[creare macchine virtuali a disponibilità elevata](tutorial-availability-sets.md). Le VM di un set di scalabilità sono distribuite in domini di errore e di aggiornamento esattamente come le VM di un set di disponibilità.

Le macchine virtuali vengono create in base alle esigenze in un set di scalabilità. Definire toocontrol le regole di scalabilità automatica come e quando le macchine virtuali vengono aggiunti o rimossi dal set di scalabilità hello. Queste regole possono essere attivate in base a determinate metriche, ad esempio il carico della CPU, l'utilizzo della memoria o il traffico di rete.

Scala imposta supporto backup too1, 000 macchine virtuali quando si utilizza un'immagine della piattaforma Azure. Per i carichi di lavoro con installazione significativo o i requisiti di personalizzazione di macchina virtuale, è preferibile troppo[creare un'immagine di macchina virtuale personalizzata](tutorial-custom-images.md). È possibile creare le macchine virtuali too100 in una scala impostata quando si utilizza un'immagine personalizzata.


## <a name="create-an-app-tooscale"></a>Creare un'app tooscale
Per poter creare un set di scalabilità è prima necessario creare un gruppo di risorse con il comando [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). esempio Hello crea un gruppo di risorse denominato *myResourceGroupAutomate* in hello *EastUS* percorso:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

In un'esercitazione precedente, si è appreso come troppo[configurazione della macchina virtuale automatizzare](tutorial-automate-vm-deployment.md) utilizzando hello estensione Script personalizzata. Creare la configurazione di un set di scalabilità, quindi applicare un tooinstall estensione Script personalizzata e configurare IIS:

```powershell
# Create a config object
$vmssConfig = New-AzureRmVmssConfig `
    -Location EastUS `
    -SkuCapacity 2 `
    -SkuName Standard_DS2 `
    -UpgradePolicyMode Automatic

# Define hello script for your Custom Script Extension toorun
$publicSettings = @{
    "fileUris" = (,"https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1");
    "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1"
}

# Use Custom Script Extension tooinstall IIS and configure basic website
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings
```

## <a name="create-scale-load-balancer"></a>Creare un bilanciamento del carico di scalabilità
Azure Load Balancer è un bilanciamento del carico di livello 4 (TCP, UDP) che offre disponibilità elevata mediante la distribuzione del traffico in ingresso nelle macchine virtuali integre. Un probe di integrità di bilanciamento del carico consente di monitorare una determinata porta in ogni macchina virtuale e vengono distribuiti solo il traffico tooan operativo VM. Per ulteriori informazioni, vedere l'esercitazione successiva hello in [come tooload bilanciare le macchine virtuali Windows](tutorial-load-balancer.md).

Creare un bilanciamento del carico con un indirizzo IP pubblico che distribuisce il traffico Web sulla porta 80:

```powershell
# Create a public IP address
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupScaleSet `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP

# Create a frontend and backend IP pool
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool

# Create hello load balancer
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool

# Create a load balancer health probe on port 80
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2

# Create a load balancer rule toodistribute traffic on port 80
Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80

# Update hello load balancer configuration
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="create-a-scale-set"></a>Creare un set di scalabilità
Ora si può creare un set di scalabilità di macchine virtuali con [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm). esempio Hello crea un set denominato di scalabilità *myScaleSet*:

```powershell
# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig `
  -ImageReferencePublisher MicrosoftWindowsServer `
  -ImageReferenceOffer WindowsServer `
  -ImageReferenceSku 2016-Datacenter `
  -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig `
  -AdminUsername azureuser `
  -AdminPassword P@ssword! `
  -ComputerNamePrefix myVM

# Create hello virtual network resources
$subnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name "mySubnet" `
  -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName "myResourceGroupScaleSet" `
  -Name "myVnet" `
  -Location "EastUS" `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $subnet
$ipConfig = New-AzureRmVmssIpConfig `
  -Name "myIPConfig" `
  -LoadBalancerBackendAddressPoolsId $lb.BackendAddressPools[0].Id `
  -SubnetId $vnet.Subnets[0].Id

# Attach hello virtual network toohello config object
Add-AzureRmVmssNetworkInterfaceConfiguration `
  -VirtualMachineScaleSet $vmssConfig `
  -Name "network-config" `
  -Primary $true `
  -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myScaleSet `
  -VirtualMachineScaleSet $vmssConfig
```

Accetta toocreate di pochi minuti e configurare tutti i set di hello scalabilità delle risorse e le macchine virtuali.


## <a name="test-your-app"></a>Test dell'app
toosee il sito Web IIS in azione, ottenere indirizzo IP pubblico di hello del servizio di bilanciamento del carico con [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). esempio Hello Ottiene hello di indirizzo IP per *myPublicIP* creati come parte del set di scalabilità hello:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

Immettere l'indirizzo IP pubblico hello nel browser web tooa. viene visualizzata, Hello app, inclusi hostname hello di hello VM che hello il carico del traffico di bilanciamento del carico distribuito per:

![Esecuzione del sito IIS](./media/tutorial-create-vmss/running-iis-site.png)

toosee set nell'azione di scalabilità hello, è possibile forza l'aggiornamento del carico di web browser toosee hello distribuire il servizio di bilanciamento del traffico tra tutte le macchine virtuali hello esegue l'app.


## <a name="management-tasks"></a>Attività di gestione
Nel ciclo di vita hello del set di scalabilità di hello, potrebbe essere necessario toorun uno o più attività di gestione. Inoltre, è consigliabile toocreate script che automatizzano le varie attività di ciclo di vita. Azure PowerShell fornisce un toodo rapidamente le attività. Di seguito vengono illustrate alcune attività comuni.

### <a name="view-vms-in-a-scale-set"></a>Visualizzare le macchine virtuali in un set di scalabilità
imposta un elenco di macchine virtuali in esecuzione nella scala tooview, utilizzare [Get AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) come indicato di seguito:

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Loop through hello instanaces in your scale set
for ($i=1; $i -le ($scaleset.Sku.Capacity - 1); $i++) {
    Get-AzureRmVmssVM -ResourceGroupName myResourceGroupScaleSet `
      -VMScaleSetName myScaleSet `
      -InstanceId $i
}
```


### <a name="increase-or-decrease-vm-instances"></a>Aumentare o diminuire le istanze delle macchine virtuali
numero di hello toosee di istanze attualmente in una scala impostate, utilizzare [Get AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) ed eseguire query su *sku.capacity*:

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

È possibile quindi manualmente aumentare o diminuire il numero di hello di macchine virtuali in hello set di scalabilità con [aggiornamento AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss). Hello che segue viene impostato il numero di hello di macchine virtuali la scala impostata troppo*5*:

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Set and update hello capacity of your scale set
$scaleset.sku.capacity = 5
Update-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -Name myScaleSet `
    -VirtualMachineScaleSet $scaleset
```

Se accetta alcuni hello tooupdate di minuti specificato numero di istanze in set di scalabilità.


### <a name="configure-autoscale-rules"></a>Configurare le regole di scalabilità automatica
Anziché imposta manualmente il numero di hello di istanze di ridimensionamento la scala, definire le regole di scalabilità automatica. Queste regole consentono il monitoraggio hello istanze la scala è impostata e rispondono di conseguenza, in base alle metriche e alle soglie definite. Hello di esempio seguente consente una scalabilità orizzontale numero hello di istanze di uno quando carico hello medio della CPU è maggiore di 60% in un periodo di 5 minuti. Se il carico della CPU Media hello quindi scende sotto il 30% in un periodo di 5 minuti, le istanze di hello vengono ridimensionate da un'istanza:

```powershell
# Define your scale set information
$mySubscriptionId = (Get-AzureRmSubscription).Id
$myResourceGroup = "myResourceGroupScaleSet"
$myScaleSet = "myScaleSet"
$myLocation = "East US"

# Create a scale up rule tooincrease hello number instances after 60% average CPU usage exceeded for a 5 minute period
$myRuleScaleUp = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator GreaterThan `
  -MetricStatistic Average `
  -Threshold 60 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Increase `
  -ScaleActionValue 1

# Create a scale down rule toodecrease hello number of instances after 30% average CPU usage over a 5 minute period
$myRuleScaleDown = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator LessThan `
  -MetricStatistic Average `
  -Threshold 30 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Decrease `
  -ScaleActionValue 1

# Create a scale profile with your scale up and scale down rules
$myScaleProfile = New-AzureRmAutoscaleProfile `
  -DefaultCapacity 2  `
  -MaximumCapacity 10 `
  -MinimumCapacity 2 `
  -Rules $myRuleScaleUp,$myRuleScaleDown `
  -Name "autoprofile"

# Apply hello autoscale rules
Add-AzureRmAutoscaleSetting `
  -Location $myLocation `
  -Name "autosetting" `
  -ResourceGroup $myResourceGroup `
  -TargetResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -AutoscaleProfiles $myScaleProfile
```


## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione è stato creato un set di scalabilità di macchine virtuali. Si è appreso come:

> [!div class="checklist"]
> * Utilizzare toodefine estensione Script personalizzata hello un tooscale del sito IIS
> * Creare un bilanciamento del carico per il set di scalabilità
> * Creare un set di scalabilità di macchine virtuali
> * Aumentare o diminuire il numero di hello di istanze in un set di scalabilità
> * Creare regole di scalabilità automatica

Spostare toolearn esercitazione successiva toohello ulteriori informazioni su concetti per le macchine virtuali di bilanciamento del carico.

> [!div class="nextstepaction"]
> [Bilanciare il carico di macchine virtuali](tutorial-load-balancer.md)
