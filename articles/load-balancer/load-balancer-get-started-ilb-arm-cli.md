---
title: un uso interno aaaCreate bilanciamento del carico - CLI di Azure | Documenti Microsoft
description: Informazioni su come un servizio di bilanciamento del carico interno utilizzando toocreate hello CLI di Azure in Gestione risorse
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c7a24e92-b4da-43c0-90f2-841c1b7ce489
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3aea6fdb07600f0d661ec6b8ffc784b03380a127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-by-using-hello-azure-cli"></a>Creare un servizio di bilanciamento del carico interno utilizzando hello CLI di Azure

> [!div class="op_single_selector"]
> * [Portale di Azure](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Interfaccia della riga di comando di Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Modello](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).  In questo articolo viene illustrato l'utilizzo modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché hello [modello di distribuzione classica](load-balancer-get-started-ilb-classic-cli.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-solution-by-using-hello-azure-cli"></a>Distribuire la soluzione hello utilizzando hello CLI di Azure

Hello alla procedura seguente viene illustrato come toocreate con una connessione Internet il bilanciamento del carico con Gestione risorse di Azure CLI. Con Gestione risorse di Azure, ogni risorsa viene creata e configurata individualmente e riunire toocreate una risorsa.

È necessario toocreate e configurare hello oggetti toodeploy un bilanciamento del carico seguenti:

* **Configurazione di IP front-end**: contiene gli indirizzi IP pubblici per il traffico di rete in ingresso
* **Pool di indirizzi back-end**: contiene le interfacce di rete (NIC) che consentono di tooreceive il traffico di rete dal servizio di bilanciamento del carico hello hello macchine virtuali
* **Regole di bilanciamento del carico**: contiene le regole che eseguono il mapping di una porta pubblica su tooport del servizio di bilanciamento carico di hello nel pool di indirizzi back-end di hello
* **Regole NAT in ingresso**: contiene le regole che eseguono il mapping di una porta pubblica nella porta di tooa del bilanciamento del carico hello per una macchina virtuale specifica nel pool di indirizzi back-end di hello
* **Probe**: contiene i probe di integrità che vengono utilizzati toocheck hello disponibilità delle istanze di macchine virtuali nel pool di indirizzi back-end di hello

Per altre informazioni, vedere [Supporto di Azure Resource Manager per Load Balancer](load-balancer-arm.md).

## <a name="set-up-cli-toouse-resource-manager"></a>Impostare CLI toouse Gestione risorse

1. Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md). Seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.
2. Eseguire hello **modalità di configurazione azure** comando tooswitch tooResource Manager modalità, come indicato di seguito:

    ```azurecli
    azure config mode arm
    ```

    Output previsto:

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a>Per creare un servizio di bilanciamento del carico interno, attenersi alla procedura dettagliata descritta di seguito

1. Accedi tooAzure.

    ```azurecli
    azure login
    ```

    Quando richiesto, immettere le credenziali di Azure.

2. Modificare la modalità di gestione delle risorse hello comando strumenti tooAzure.

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Tutte le risorse in Azure Resource Manager vengono associate a un gruppo di risorse. Se non è ancora stato fatto, creare un gruppo di risorse.

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a>Creare un set di bilanciamento del carico interno

1. Creare un bilanciamento del carico interno

    In hello seguente scenario, viene creato un gruppo di risorse denominato nrprg nell'area Stati Uniti orientali.

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > Tutte le risorse per un bilanciamento del carico interno, ad esempio le reti virtuali e subnet della rete virtuale, è necessario hello stesso gruppo di risorse e in hello stessa area.

2. Creare un indirizzo IP front-end di bilanciamento del carico interno hello.

    indirizzo IP Hello in uso deve essere entro l'intervallo di hello subnet della rete virtuale.

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. Creare il pool di indirizzi back-end di hello.

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    Dopo aver definito un indirizzo IP front-end e un pool di indirizzi back-end, è possibile creare regole del servizio di bilanciamento del carico, regole NAT in ingresso e probe di integrità personalizzati.

4. Creare una regola di bilanciamento del carico di bilanciamento del carico interno hello.

    Quando si seguono i passaggi precedenti hello, hello comando crea una regola di bilanciamento del carico per l'ascolto tooport 1433 nel pool di server front-end hello e pool di indirizzi back-end toohello di traffico di invio con bilanciamento del carico di rete, anche tramite la porta 1433.

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. Creare regole NAT in ingresso.

    Le regole NAT in ingresso sono endpoint toocreate utilizzati in un bilanciamento del carico che vanno tooa macchina virtuale specifica istanza. passaggi precedenti Hello create due regole NAT per il desktop remoto.

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. Creare il probe di integrità servizio di bilanciamento del carico hello.

    Un probe di integrità controlla tutti toomake istanze macchina virtuale che possono inviare il traffico di rete. istanza di macchina virtuale Hello con i controlli di probe non viene rimosso dal servizio di bilanciamento del carico hello fino a quando non diventa nuovamente online e un controllo di probe determina che è integro.

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > piattaforma Microsoft Azure Hello utilizza un indirizzo IPv4 statico, instradabile pubblicamente per un'ampia gamma di scenari di amministrazione. indirizzo IP Hello è 168.63.129.16. Questo indirizzo IP non deve essere bloccato da alcun firewall, perché potrebbe causare un comportamento imprevisto.
    > Con riguardo tooAzure interno il bilanciamento del carico, viene utilizzato questo indirizzo IP dal monitoraggio probe di stato di integrità hello toodetermine bilanciamento del carico hello per le macchine virtuali in un set con carico bilanciato. Se un gruppo di sicurezza di rete è utilizzata toorestrict traffico tooAzure le macchine virtuali in un set di internamente con bilanciamento del carico o applicato tooa subnet della rete virtuale, assicurarsi che una regola di sicurezza di rete viene aggiunto il traffico tooallow 168.63.129.16.

## <a name="create-nics"></a>Creare NIC

È necessario toocreate NIC (o modificare quelli esistenti) e associarli tooNAT regole, regole di bilanciamento del carico e probe.

1. Creare una scheda di rete denominata *lb-nic1 essere*e quindi associarlo hello *rdp1* NAT regola e hello *beilb* pool di indirizzi back-end.

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
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

2. Creare una scheda di rete denominata *lb-nic2 essere*e quindi associarlo hello *rdp2* NAT regola e hello *beilb* pool di indirizzi back-end.

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. Creare una macchina virtuale denominata *DB1*e quindi associarlo hello NIC denominato *lb-nic1 essere*. Un account di archiviazione denominato *web1nrp* sia stato creato prima hello eseguito il comando seguente:

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > Macchine virtuali in un toobe necessità bilanciamento di carico in hello stesso set di disponibilità. Utilizzare `azure availset create` toocreate un gruppo di disponibilità.

4. Creare una macchina virtuale (VM) denominata *DB2*e quindi associarlo hello NIC denominato *lb-nic2 essere*. Un account di archiviazione denominato *web1nrp* è stato creato prima di eseguire hello comando seguente.

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a>Eliminare un servizio di bilanciamento del carico

tooremove un bilanciamento del carico, utilizzare hello comando seguente:

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a>Passaggi successivi

[Configurare una modalità di distribuzione del servizio di bilanciamento del carico usando l'affinità dell'IP di origine](load-balancer-distribution-mode.md)

[Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico](load-balancer-tcp-idle-timeout.md)

