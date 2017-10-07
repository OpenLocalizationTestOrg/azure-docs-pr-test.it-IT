---
title: Azure interna aaaCreate bilanciamento del carico - PowerShell | Documenti Microsoft
description: Informazioni su come toocreate un interno bilanciamento del carico con PowerShell in Gestione risorse
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 4b9657c77aa32a142de49ff7871ed6a396b22223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a>Creare un servizio di bilanciamento del carico interno con PowerShell

> [!div class="op_single_selector"]
> * [Portale di Azure](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Interfaccia della riga di comando di Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Modello](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).  In questo articolo viene illustrato l'utilizzo modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché hello [modello di distribuzione classica](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

Hello alla procedura seguente viene illustrato come toocreate un interno bilanciamento del carico con Gestione risorse di Azure PowerShell. Con Gestione risorse di Azure, hello elementi toocreate un bilanciamento del carico interno vengono configurate singolarmente e quindi combinati toocreate un bilanciamento del carico.

È necessario toocreate e configurare hello oggetti toodeploy un bilanciamento del carico seguenti:

* Configurazione IP end front - configurerà l'indirizzo IP privato hello in arrivo il traffico di rete
* Pool di indirizzi back-end - configurerà le interfacce di rete hello che riceveranno il traffico con carico bilanciato hello in arrivo dal pool IP front-end
* Regole di bilanciamento del carico - di origine e configurazione della porta locale per hello bilanciamento del carico.
* Probe - configura i probe di stato di integrità hello per le istanze di macchina virtuale hello.
* Regole NAT in ingresso - configurare l'accesso alla toodirectly regole di porta hello una delle istanze di macchine virtuali hello.

È possibile ottenere altre informazioni sui componenti del servizio di bilanciamento del carico con Gestione risorse di Azure in [Supporto di Gestione risorse di Azure per il bilanciamento del carico](load-balancer-arm.md).

Hello passaggi seguenti illustrano come tooconfigure un bilanciamento del carico tra due macchine virtuali.

## <a name="setup-powershell-toouse-resource-manager"></a>Il programma di installazione PowerShell toouse Gestione risorse

Assicurarsi di disporre hello ultima versione di produzione di hello modulo Azure per PowerShell e PowerShell è installato installazione tooaccess correttamente la sottoscrizione di Azure.

### <a name="step-1"></a>Passaggio 1

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Passaggio 2

Controllare le sottoscrizioni di hello per account hello

```powershell
Get-AzureRmSubscription
```

Sarà richiesto tooAuthenticate con le credenziali.

### <a name="step-3"></a>Passaggio 3

Scegliere quali di toouse le sottoscrizioni di Azure.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a>Creare un gruppo di risorse per il servizio di bilanciamento del carico

Creare un nuovo gruppo di risorse (ignorare questo passaggio se si usa un gruppo di risorse esistente)

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso Viene utilizzato come percorso predefinito di hello per le risorse in tale gruppo di risorse. Assicurarsi che tutti i comandi toocreate utilizzerà un bilanciamento del carico hello stesso gruppo di risorse.

In hello esempio precedente viene creato un gruppo di risorse denominato "NRP-RG" e il percorso "Stati Uniti occidentali".

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a>Creare la rete virtuale e un indirizzo IP privato per il pool di indirizzi IP front-end

Crea una subnet per la rete virtuale hello e assegna toovariable $backendSubnet

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

Creare una rete virtuale:

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

Crea rete virtuale hello e aggiunge una rete virtuale di essere lb-subnet toohello subnet hello NRPVNet e assegna toovariable $vnet

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a>Creare il pool di indirizzi IP front-end e il pool di indirizzi back-end

Impostazione di un pool IP front-end per hello in arrivo carico del traffico di rete del servizio di bilanciamento e traffico con carico bilanciato di back-end indirizzi pool tooreceive hello.

### <a name="step-1"></a>Passaggio 1

Creare un pool IP di front-end utilizzando l'indirizzo IP privato hello 10.0.2.5 per hello subnet 10.0.2.0/24 che sarà l'endpoint del traffico di rete in ingresso hello.

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a>Passaggio 2

Configurare un pool di indirizzi back-end utilizzato traffico in ingresso tooreceive dal pool IP front-end:

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a>Creare regole di bilanciamento del carico, regole NAT, probe e il servizio di bilanciamento del carico

Dopo la creazione di pool IP front-end di hello e pool di indirizzi back-end di hello, è necessario utilizzare le regole di hello toocreate apparterranno toohello risorsa di bilanciamento del carico:

### <a name="step-1"></a>Passaggio 1

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

esempio Hello precedente crea hello seguenti elementi:

* La regola NAT tutti in ingresso che il traffico tooport 3441 entra tooport 3389.
* una seconda regola NAT tutti in ingresso che il traffico tooport 3442 entra tooport 3389.
* una regola di bilanciamento del carico che caricherà bilanciare tutto il traffico in ingresso sulla porta di porta pubblica 80 toolocal 80 nel pool di indirizzi back-end hello.
* una regola di probe che controlla lo stato di integrità hello per il percorso "HealthProbe.aspx"

### <a name="step-2"></a>Passaggio 2

Creazione di bilanciamento del carico hello sommando tutti gli oggetti (le regole NAT, regole di bilanciamento del carico, le configurazioni di probe):

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a>Creare interfacce di rete

Dopo la creazione di bilanciamento del carico interno hello, è necessario definire le interfacce di rete verranno ricevuto hello in arrivo con carico bilanciato il traffico di rete, le regole NAT e probe. in questo caso, l'interfaccia di rete Hello viene configurata singolarmente e può essere assegnato macchina virtuale tooa in un secondo momento.

### <a name="step-1"></a>Passaggio 1

Ottenere risorse hello virtuale rete e subnet toocreate interfacce di rete:

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

Questo passaggio viene creata un'interfaccia di rete che appartengono a pool back-end di bilanciamento del carico toohello e associare la regola NAT prima hello per RDP per questa interfaccia di rete:

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a>Passaggio 2

Creare una seconda interfaccia di rete denominata LB-Nic2-BE:

Questo passaggio viene creata una seconda interfaccia di rete, assegnazione toohello il bilanciamento del carico stesso terminare pool e associare la regola NAT secondo hello creato per RDP:

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

risultato finale Hello mostrerà seguente hello:

    $backendnic1

Output previsto:

    Name                 : lb-nic1-be
    ResourceGroupName    : NRP-RG
    Location             : westus
    Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
    Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
    ProvisioningState    : Succeeded
    Tags                 :
    VirtualMachine       : null
    IpConfigurations     : [
                         {
                           "PrivateIpAddress": "10.0.2.6",
                           "PrivateIpAllocationMethod": "Static",
                           "Subnet": {
                             "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                           },
                           "PublicIpAddress": {
                             "Id": null
                           },
                           "LoadBalancerBackendAddressPools": [
                             {
                               "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                             }
                           ],
                           "LoadBalancerInboundNatRules": [
                             {
                               "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                             }
                           ],
                           "ProvisioningState": "Succeeded",
                           "Name": "ipconfig1",
                           "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                           "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1"
                         }
                       ]
    DnsSettings          : {
                         "DnsServers": [],
                         "AppliedDnsServers": []
                       }
    AppliedDnsSettings   :
    NetworkSecurityGroup : null
    Primary              : False



### <a name="step-3"></a>Passaggio 3

Utilizzare hello comando Add-AzureRmVMNetworkInterface tooassign hello NIC tooa macchina virtuale.

È possibile trovare istruzioni dettagliate toocreate una macchina virtuale hello e assegnare tooa NIC seguente documentazione hello: [creare una macchina virtuale di Azure con PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

## <a name="add-hello-network-interface"></a>Aggiungere l'interfaccia di rete hello

Se si dispone già di una macchina virtuale creata, è possibile aggiungere l'interfaccia di rete hello con hello alla procedura seguente:

### <a name="step-1"></a>Passaggio 1

Caricare la risorsa di servizio di bilanciamento carico hello in una variabile (se non è stato fatto che ancora). variabile di Hello utilizzato è denominato $lb e utilizzare hello stessi nomi di risorsa di bilanciamento del carico hello creati in precedenza.

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a>Passaggio 2

Carica la variabile tooa di configurazione back-end di hello.

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a>Passaggio 3

Caricare l'interfaccia di rete hello già creato in una variabile. nome della variabile Hello utilizzato è $ scheda di rete. nome di interfaccia di rete Hello utilizzato è hello stesso esempio hello precedente.

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a>Passaggio 4

Modificare la configurazione back-end di hello nell'interfaccia di rete hello.

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a>Passaggio 5

Salvare un oggetto di interfaccia di rete hello.

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

Dopo l'aggiunta di un'interfaccia di rete pool back-end di bilanciamento del carico toohello, avvia la ricezione di traffico di rete in base alle regole per la risorsa del servizio di bilanciamento carico di bilanciamento del carico di hello.

## <a name="update-an-existing-load-balancer"></a>Aggiornare un bilanciamento del carico esistente

### <a name="step-1"></a>Passaggio 1
Usa bilanciamento del carico hello dall'esempio hello precedente, assegnare $slb utilizzando Get-AzureRmLoadBalancer toovariable di oggetto servizio di bilanciamento carico

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a>Passaggio 2

Nell'esempio seguente di hello, si aggiungerà una nuova regola NAT in ingresso utilizzando la porta 81 nel front-end hello e porta 8181 per il backup di hello end di bilanciamento del carico di pool tooan esistente

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a>Passaggio 3

Salvare hello nuova configurazione utilizzando Set-AzureLoadBalancer

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a>Rimuovere un bilanciamento del carico

Utilizzare hello comando Remove-AzureRmLoadBalancer toodelete un bilanciamento del carico creato in precedenza denominata "NRP-LB" in un gruppo di risorse denominato "NRP-RG"

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> È possibile utilizzare hello facoltativo switch - Force tooavoid hello Richiedi l'eliminazione.

## <a name="next-steps"></a>Passaggi successivi

[Configurare una modalità di distribuzione del bilanciamento del carico](load-balancer-distribution-mode.md)

[Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico](load-balancer-tcp-idle-timeout.md)
