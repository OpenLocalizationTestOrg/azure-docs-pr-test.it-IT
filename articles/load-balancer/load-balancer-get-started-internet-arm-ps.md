---
title: una connessione Internet Azure aaaCreate bilanciamento del carico - PowerShell | Documenti Microsoft
description: Informazioni su come toocreate con una connessione Internet il bilanciamento del carico di gestione risorse tramite PowerShell
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 8257f548-7019-417f-b15f-d004a1eec826
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e4e0e5271bc83c23fc62c0910e784c57d2b30065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started"></a>Creazione di un servizio di bilanciamento del carico per Internet in Resource Manager con PowerShell

> [!div class="op_single_selector"]
> * [Portale](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Interfaccia della riga di comando di Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Modello](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Questo articolo descrive il modello di distribuzione di gestione risorse di hello. È anche possibile [informazioni su come toocreate con una connessione Internet il bilanciamento del carico utilizzando il modello di distribuzione classica hello](load-balancer-get-started-internet-classic-cli.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-by-using-azure-powershell"></a>Distribuzione di soluzioni hello tramite Azure PowerShell

Hello, seguire le procedure seguenti spiegano come toocreate con una connessione Internet il bilanciamento del carico con Gestione risorse di Azure PowerShell. Con Gestione risorse di Azure, ogni risorsa viene creata e configurata individualmente e riunire toocreate un bilanciamento del carico.

È necessario creare e configurare hello oggetti toodeploy un bilanciamento del carico seguenti:

* Configurazione IP front-end: contiene gli indirizzi IP pubblici (PIP) per il traffico di rete in ingresso.
* Pool di indirizzi back-end: contiene le interfacce di rete (NIC) per tooreceive il traffico di rete dal servizio di bilanciamento del carico hello hello macchine virtuali.
* Regole di bilanciamento del carico: contiene le regole che eseguono il mapping di una porta pubblica nella porta di tooa del bilanciamento del carico hello nel pool di indirizzi back-end di hello.
* Regole NAT in ingresso: contiene le regole che eseguono il mapping di una porta pubblica nella porta di tooa del bilanciamento del carico hello per una macchina virtuale specifica nel pool di indirizzi back-end di hello.
* Probe: contiene disponibilità toocheck utilizzati probe di integrità delle istanze di macchine virtuali nel pool di indirizzi back-end di hello.

Per altre informazioni, vedere [Supporto di Azure Resource Manager per Load Balancer](load-balancer-arm.md).

## <a name="set-up-powershell-toouse-resource-manager"></a>Configurare PowerShell toouse Gestione risorse

Assicurarsi di disporre di hello ultima versione di produzione del modulo di gestione risorse di Azure hello per PowerShell:

1. Accedi tooAzure.

    ```powershell
    Login-AzureRmAccount
    ```

    Immettere le credenziali quando richiesto.

2. Controllare le sottoscrizioni di hello per account hello.

    ```powershell
    Get-AzureRmSubscription
    ```

3. Scegliere quali di toouse le sottoscrizioni di Azure.

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. Creare un gruppo di risorse. Se si usa un gruppo di risorse esistente, ignorare questo passaggio.

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>Creare una rete virtuale e un indirizzo IP pubblico per il pool IP front-end di hello

1. Creare una subnet e una rete virtuale

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. Creare una Azure pubblica risorsa indirizzo IP, denominata **PublicIP**, utilizzato da un pool IP front-end con nome DNS hello toobe **loadbalancernrp.westus.cloudapp.azure.com**. hello comando seguente usa hello tipo di allocazione statica.

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > bilanciamento del carico di Hello Usa etichetta hello del dominio dell'indirizzo IP pubblico hello come prefisso per il nome di dominio completo. Ciò è diverso dal modello di distribuzione classica hello, che utilizza il servizio di cloud hello come hello bilanciamento del carico FQDN.
   > In questo esempio, hello FQDN è **loadbalancernrp.westus.cloudapp.azure.com**.

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a>Creazione di un pool di indirizzi IP front-end e un pool di indirizzi back-end

1. Creare un pool IP front-end denominato **LB-Frontend** che utilizza hello **PublicIp** risorse.

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. Creare un pool di indirizzi back-end denominato **LB-backend**.

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a>Creazione di regole NAT, una regola di bilanciamento del carico, un probe e un servizio di bilanciamento del carico

In questo esempio crea hello seguenti elementi:

* Un tootranslate regola NAT in ingresso tutti il traffico su porta 3441 tooport 3389
* Un tootranslate regola NAT in ingresso tutti il traffico su porta 3442 tooport 3389
* Probe regola toocheck hello lo stato di integrità in una pagina denominata **HealthProbe.aspx**
* Un toobalance regola di bilanciamento carico di tutto il traffico in ingresso sulla porta 80 tooport 80 su hello indirizzi nel pool back-end hello
* Un servizio di bilanciamento del carico che usa tutti questi oggetti

Usare i passaggi seguenti:

1. Creare le regole NAT di hello.

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. Creare un probe di integrità. Esistono due modi tooconfigure un probe:

    Probe HTTP

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    Probe TCP

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. Creare una regola del servizio di bilanciamento del carico.

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. Creare servizio di bilanciamento del carico hello tramite gli oggetti hello creato in precedenza.

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a>Creare NIC

Creare interfacce di rete (o modificare quelli esistenti) e quindi associarle tooNAT regole, regole di bilanciamento del carico e probe:

1. Ottenere la rete virtuale hello e una subnet della rete virtuale, in cui le schede NIC hello necessario toobe creato.

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. Creare una scheda di rete denominata **lb-nic1 essere**e associarlo a una regola NAT prima hello e pool di indirizzi back-end primo (e unico) hello.

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. Creare una scheda di rete denominata **lb-nic2 essere**e associarlo a una regola NAT secondo hello e pool di indirizzi back-end primo (e unico) hello.

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. Controllare le schede NIC hello.

        $backendnic1

    Output previsto:

        Name                 : lb-nic1-be
        ResourceGroupName    : NRP-RG
        Location             : westus
        Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
        ResourceGuid         : 896cac4f-152a-40b9-b079-3e2201a5906e
        ProvisioningState    : Succeeded
        Tags                 :
        VirtualMachine       : null
        IpConfigurations     : [
                            {
                            "Name": "ipconfig1",
                            "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                            "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1",
                            "PrivateIpAddress": "10.0.2.6",
                            "PrivateIpAllocationMethod": "Static",
                            "Subnet": {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                            },
                            "ProvisioningState": "Succeeded",
                            "PrivateIpAddressVersion": "IPv4",
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
                            "Primary": true,
                            "ApplicationGatewayBackendAddressPools": []
                            }
                        ]
        DnsSettings          : {
                            "DnsServers": [],
                            "AppliedDnsServers": [],
                            "InternalDomainNameSuffix": "prcwibzcuvie5hnxav0yjks2cd.dx.internal.cloudapp.net"
                        }
        EnableIPForwarding   : False
        NetworkSecurityGroup : null
        Primary              :

5. Hello utilizzare `Add-AzureRmVMNetworkInterface` cmdlet tooassign hello NIC toodifferent macchine virtuali.

## <a name="create-a-virtual-machine"></a>Creare una macchina virtuale

Per indicazioni sulla creazione di una macchina virtuale e sull'assegnazione di una scheda di interfaccia di rete, vedere [Creare una VM di Azure con PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

## <a name="add-hello-network-interface-toohello-load-balancer"></a>Aggiungere toohello hello rete interfaccia il bilanciamento del carico

1. Recuperare bilanciamento del carico hello da Azure.

    Caricare la risorsa di servizio di bilanciamento carico hello in una variabile (se non è stato fatto che ancora). viene chiamato variabile Hello **$lb**. Utilizzare hello nomi identici dalla risorsa di bilanciamento del carico hello creato in precedenza.

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. Carica la variabile di tooa hello configurazione back-end.

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. Caricare l'interfaccia di rete hello già creato in una variabile. nome della variabile Hello è **$nic**. Hello nome di interfaccia di rete è hello stesso da hello l'esempio precedente.

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. Modificare la configurazione back-end di hello nell'interfaccia di rete hello.

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. Salvare un oggetto di interfaccia di rete hello.

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    Dopo l'aggiunta di un'interfaccia di rete pool back-end di bilanciamento del carico toohello, avvia la ricezione di traffico di rete in base alle regole di bilanciamento del carico hello per tale risorsa di bilanciamento del carico.

## <a name="update-an-existing-load-balancer"></a>Aggiornare un bilanciamento del carico esistente

1. Hello con bilanciamento del carico da hello l'esempio precedente, assegnare una variabile di toohello oggetto servizio di bilanciamento carico **$slb** utilizzando `Get-AzureLoadBalancer`.

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. Nel seguente esempio di hello, aggiungere una regola NAT in ingresso - tramite la porta 81 nel pool di server front-end hello e 8181 per pool back-end hello - tooan del bilanciamento del carico esistente.

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. Salvare una nuova configurazione hello utilizzando `Set-AzureLoadBalancer`.

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a>Rimuovere un bilanciamento del carico

Utilizzare il comando hello `Remove-AzureLoadBalancer` toodelete un bilanciamento del carico creato in precedenza denominato **NRP LB** in un gruppo di risorse denominato **NRP RG**.

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> È possibile utilizzare l'opzione facoltativa hello **-Force** prompt hello tooavoid per l'eliminazione.

## <a name="next-steps"></a>Passaggi successivi

[Introduzione alla configurazione del bilanciamento del carico interno](load-balancer-get-started-ilb-arm-ps.md)

[Configurare una modalità di distribuzione del servizio di bilanciamento del carico](load-balancer-distribution-mode.md)

[Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico](load-balancer-tcp-idle-timeout.md)
