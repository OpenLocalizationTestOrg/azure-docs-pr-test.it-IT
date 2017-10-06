---
title: con una connessione Internet aaaCreate bilanciamento del carico - CLI di Azure | Documenti Microsoft
description: Informazioni su come toocreate un Internet rivolto al bilanciamento del carico con Gestione risorse hello CLI di Azure
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a8bcdd88-f94c-4537-8143-c710eaa86818
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: cadb5edb3b4a4e2f0813109d027eaafdc7ef7303
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-load-balancer-using-hello-azure-cli"></a>Creazione di un bilanciamento del carico internet utilizzando hello CLI di Azure

> [!div class="op_single_selector"]
> * [Portale](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Interfaccia della riga di comando di Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Modello](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Questo articolo descrive il modello di distribuzione di gestione risorse di hello. È anche possibile [informazioni su come toocreate una connessione Internet bilanciamento del carico utilizzando la distribuzione classica](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-using-hello-azure-cli"></a>La distribuzione di soluzioni hello utilizzando hello CLI di Azure

Hello alla procedura seguente viene illustrato come una connessione Internet toocreate bilanciamento del carico con Gestione risorse di Azure CLI. Con Gestione risorse di Azure creata e configurata singolarmente ogni risorsa, quindi riunire toocreate una risorsa.

È necessario creare e configurare hello oggetti toodeploy un bilanciamento del carico seguenti:

* Configurazione di IP front-end: contiene gli indirizzi IP pubblici per il traffico di rete in ingresso.
* Pool di indirizzi di back-end - contiene le interfacce di rete (NIC) per tooreceive il traffico di rete dal servizio di bilanciamento del carico hello hello macchine virtuali.
* Regole di bilanciamento del carico - contiene le regole di mapping di una porta pubblica su tooport del servizio di bilanciamento carico di hello nel pool di indirizzi back-end di hello.
* Regole NAT in ingresso - contiene le regole di mapping di una porta pubblica nella porta di tooa del bilanciamento del carico hello per una macchina virtuale specifica nel pool di indirizzi back-end di hello.
* Probe - contiene integrità probe usati toocheck disponibilità delle istanze di macchine virtuali nel pool di indirizzi back-end di hello.

Per altre informazioni, vedere [Supporto di Gestione risorse di Azure per il servizio di bilanciamento del carico](load-balancer-arm.md).

## <a name="set-up-cli-toouse-resource-manager"></a>Impostare CLI toouse Gestione risorse

1. Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.
2. Eseguire hello **modalità di configurazione azure** tooswitch tooResource Manager modalità comando, come illustrato di seguito.

    ```azurecli
        azure config mode arm
    ```

    Output previsto:

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>Creare una rete virtuale e un indirizzo IP pubblico per il pool IP front-end di hello

1. Creare una rete virtuale (VNet) denominata *NRPVnet* in Stati Uniti orientali hello utilizzando un gruppo di risorse denominato *NRPRG*.

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    Creare una subnet denominata *NRPVnetSubnet* con un blocco CIDR di 10.0.0.0/24 in *NRPVnet*.

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. Creare un indirizzo IP pubblico denominato *NRPPublicIP* toobe utilizzato da un pool IP front-end con nome DNS *loadbalancernrp.eastus.cloudapp.azure.com*. comando hello seguente utilizza il tipo di allocazione statica hello e timeout di inattività di 4 minuti.

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > bilanciamento del carico Hello utilizzerà l'etichetta del dominio dell'indirizzo IP pubblico hello hello come il nome di dominio completo. Questo una modifica dalla distribuzione classica, che utilizza il servizio di cloud hello come hello bilanciamento del carico completamente dominio nome completo (FQDN).
   > In questo esempio, hello FQDN è *loadbalancernrp.eastus.cloudapp.azure.com*.

## <a name="create-a-load-balancer"></a>Creare un servizio di bilanciamento del carico

il comando seguente Hello crea un bilanciamento del carico denominato *NRPlb* in hello *NRPRG* gruppo di risorse in hello *Stati Uniti orientali* località di Azure.

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a>Creare un pool di indirizzi IP front-end e un pool di indirizzi back-end
Questo esempio viene illustrato come toocreate hello front-end pool IP che riceve il traffico di rete in ingresso di hello in hello bilanciamento del carico e il pool IP back-end in cui pool front-end hello invia il traffico di rete con carico bilanciato hello hello.

1. Creare un pool IP front-end associazione hello creato nel passaggio precedente hello e bilanciamento del carico hello indirizzo IP pubblico.

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. Configurare un pool di indirizzi back-end utilizzato traffico in ingresso tooreceive dal pool IP front-end hello.

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a>Creare regole di bilanciamento del carico, regole NAT e probe

Questo esempio crea hello seguenti elementi.

* un dispositivo NAT regola tootranslate tutto il traffico in ingresso sulla porta 21 tooport 22<sup>1</sup>
* un dispositivo NAT tutto il traffico in ingresso sulla porta 23 tooport 22 tootranslate della regola
* un toobalance regola di bilanciamento carico di tutto il traffico in ingresso sulla porta 80 tooport 80 su hello indirizzi nel pool back-end hello.
* probe regola toocheck hello lo stato di integrità in una pagina denominata *HealthProbe.aspx*.

<sup>1</sup> le regole NAT sono associati tooa macchina virtuale specifica istanza bilanciamento del carico hello. il traffico di rete Hello in arrivo sulla porta 21 viene inviato a macchina virtuale specifica tooa sulla porta 22 associata a questa regola NAT. È necessario specificare un protocollo (UDP o TCP) per una regola NAT. Entrambi i protocolli non possono essere assegnato toohello stessa porta.

1. Creare le regole NAT di hello.

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. Creare una regola del servizio di bilanciamento del carico.

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. Creare un probe di integrità.

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. Verificare le impostazioni.

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    Output previsto:

        info:    Executing command network lb show
        + Looking up hello load balancer "nrplb"
        + Looking up hello public ip "NRPPublicIP"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb
        data:    Name                            : nrplb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : eastus
        data:    Provisioning State              : Succeeded
        data:    Frontend IP configurations:
        data:      Name                          : NRPfrontendpool
        data:      Provisioning state            : Succeeded
        data:      Public IP address id          : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/publicIPAddresses/NRPPublicIP
        data:      Public IP allocation method   : Static
        data:      Public IP address             : 40.114.13.145
        data:
        data:    Backend address pools:
        data:      Name                          : NRPbackendpool
        data:      Provisioning state            : Succeeded
        data:
        data:    Load balancing rules:
        data:      Name                          : HTTP
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 80
        data:      Backend port                  : 80
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:      Backend address pool          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:
        data:    Inbound NAT rules:
        data:      Name                          : ssh1
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 21
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:      Name                          : ssh2
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 23
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:    Probes:
        data:      Name                          : healthprobe
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Http
        data:      Port                          : 80
        data:      Interval in seconds           : 15
        data:      Number of probes              : 4
        data:
        info:    network lb show command OK

## <a name="create-nics"></a>Creare NIC

È necessario toocreate NIC (o modificare quelli esistenti) e associarli tooNAT regole, regole di bilanciamento del carico e probe.

1. Creare una scheda di rete denominata *lb-nic1 essere*e associarlo a hello *rdp1* NAT regola e hello *NRPbackendpool* pool di indirizzi back-end.

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    Output previsto:

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. Creare una scheda di rete denominata *lb-nic2 essere*e associarlo a hello *rdp2* NAT regola e hello *NRPbackendpool* pool di indirizzi back-end.

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. Creare una macchina virtuale (VM) denominata *web1*e associarlo a una scheda di rete denominata hello *lb-nic1 essere*. Un account di archiviazione denominato *web1nrp* è stato creato prima dell'esecuzione comando hello riportato di seguito.

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > Macchine virtuali in un toobe necessità bilanciamento di carico in hello stesso set di disponibilità. Utilizzare `azure availset create` toocreate un gruppo di disponibilità.

    output di Hello deve essere simile toohello seguenti:

        info:    Executing command vm create
        + Looking up hello VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using hello VM Size "Standard_A1"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account web1nrp
        + Looking up hello availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up hello NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in hello NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > messaggio informativo Hello **si tratta di una scheda di rete senza publicIP configurato** previsto poiché hello NIC creato per la connessione utilizzando l'indirizzo IP pubblico di hello carico bilanciamento tooInternet bilanciamento del carico di hello.

    Poiché hello *lb-nic1 essere* NIC è associata a hello *rdp1* regola NAT, è possibile connettersi troppo*web1* tramite RDP porta 3441 nel servizio di bilanciamento del carico hello.

4. Creare una macchina virtuale (VM) denominata *web2*e associarlo a una scheda di rete denominata hello *lb-nic2 essere*. Un account di archiviazione denominato *web1nrp* è stato creato prima dell'esecuzione comando hello riportato di seguito.

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a>Aggiornare un bilanciamento del carico esistente
È possibile aggiungere regole che fanno riferimento a un servizio di bilanciamento del carico esistente. Nell'esempio riportato di seguito hello, una nuova regola di bilanciamento del carico viene aggiunto a bilanciamento del carico esistente tooan **NRPlb**

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a>Eliminare un servizio di bilanciamento del carico
Utilizzare hello comando tooremove un bilanciamento del carico seguenti:

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a>Passaggi successivi
[Introduzione alla configurazione del bilanciamento del carico interno](load-balancer-get-started-ilb-arm-cli.md)

[Configurare una modalità di distribuzione del servizio di bilanciamento del carico](load-balancer-distribution-mode.md)

[Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico](load-balancer-tcp-idle-timeout.md)
