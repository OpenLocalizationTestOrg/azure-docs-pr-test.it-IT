---
title: un uso interno aaaCreate bilanciamento del carico - CLI di Azure classico | Documenti Microsoft
description: Informazioni su come un servizio di bilanciamento carico interno utilizzando toocreate hello CLI di Azure nel modello di distribuzione classica hello
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: becbbbde-a118-4269-9444-d3153f00bf34
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: ef29dfda5f7a75a411bbabe8b688a31c6bf81113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-hello-azure-cli"></a>Introduzione alla creazione di un bilanciamento del carico interno (classico) utilizzando hello CLI di Azure

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Interfaccia della riga di comando di Azure](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Servizi cloud](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).  In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Informazioni su come troppo[eseguire questi passaggi tramite il modello di gestione risorse di hello](load-balancer-get-started-ilb-arm-cli.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="toocreate-an-internal-load-balancer-set-for-virtual-machines"></a>toocreate un bilanciamento del carico interno è impostato per le macchine virtuali

toocreate un bilanciamento del carico interno impostato e hello server che invierà i tooit di traffico, è necessario eseguire il seguente hello:

1. Creare un'istanza interna il bilanciamento del carico che fungerà da endpoint hello in arrivo traffico toobe con bilanciato del carico tra i server hello di un set con carico bilanciato.
2. Aggiungere gli endpoint corrispondenti toohello le macchine virtuali che riceveranno il traffico in ingresso hello.
3. Configurare i server hello che invieranno hello traffico toobe con bilanciamento del carico toosend loro traffico toohello indirizzo IP virtuale (VIP) dell'istanza di hello interno il bilanciamento del carico.

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a>Procedura dettagliata sulla creazione di un servizio di bilanciamento del carico interno tramite CLI

Questa guida viene spiegato come toocreate un bilanciamento del carico interno in base a hello scenario precedente.

1. Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.
2. Eseguire hello **modalità di configurazione azure** comando tooswitch tooclassic modalità come illustrato di seguito.

    ```azurecli
    azure config mode asm
    ```

    Output previsto:

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a>Creazione dell’endpoint e del set del servizio di bilanciamento del carico

scenario di Hello presuppone hello macchine "DB1" e "DB2" in un servizio cloud denominato "mytestcloud". Entrambe le macchine virtuali utilizzano una rete virtuale denominata "my testvnet" con subnet "subnet-1".

In questa guida verrà creato un set del servizio di bilanciamento del carico interno utilizzando la porta 1433 come porta privata e la porta 1433 come porta locale.

Si tratta di uno scenario comune in cui si dispone di macchine virtuali SQL hello back-end utilizzando che un server di database hello tooguarantee bilanciamento di carico interno non verrà esposto direttamente tramite un indirizzo IP pubblico.

### <a name="step-1"></a>Passaggio 1

Creare un set di bilanciamento del carico interno utilizzando `azure network service internal-load-balancer add`.

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

Per ulteriori informazioni, vedere `azure service internal-load-balancer --help` .

È possibile controllare le proprietà del servizio di bilanciamento di carico interno hello comando hello `azure service internal-load-balancer list` *nome del servizio cloud*.

Di seguito segue un esempio di output di hello:

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a>Passaggio 2

Configurare un bilanciamento del carico interno hello impostata quando si aggiungono endpoint prima di hello. Associare hello endpoint, macchina virtuale e un probe porta toohello bilanciamento del carico interno impostato in questo passaggio.

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a>Passaggio 3

Verificare tramite configurazione del servizio di bilanciamento carico di hello `azure vm show` *nome della macchina virtuale*

```azurecli
azure vm show DB1
```

output di Hello sarà:

    azure vm show DB1
    info:    Executing command vm show
    + Getting virtual machines
    data:    DNSName "mytestcloud.cloudapp.net"
    data:    Location "East US 2"
    data:    VMName "DB1"
    data:    IPAddress "192.168.2.4"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "db1-DB1-0-201511120457370846"
    data:    OSDisk mediaLink "https://XXXX.blob.core.windows.net/vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "137.116.64.107"
    data:    VirtualIPAddresses 0 name "db1ContractContract"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    VirtualIPAddresses 1 address "192.168.2.7"
    data:    VirtualIPAddresses 1 name "ilbset"
    data:    Network Endpoints 0 localPort 5986
    data:    Network Endpoints 0 name "PowerShell"
    data:    Network Endpoints 0 port 5986
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 3389
    data:    Network Endpoints 1 name "Remote Desktop"
    data:    Network Endpoints 1 port 60173
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 1433
    data:    Network Endpoints 2 name "tcp-1433-1433"
    data:    Network Endpoints 2 port 1433
    data:    Network Endpoints 2 loadBalancerProbe port 1433
    data:    Network Endpoints 2 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 2 loadBalancerProbe intervalInSeconds 300
    data:    Network Endpoints 2 loadBalancerProbe timeoutInSeconds 600
    data:    Network Endpoints 2 protocol "tcp"
    data:    Network Endpoints 2 virtualIPAddress "192.168.2.7"
    data:    Network Endpoints 2 enableDirectServerReturn false
    data:    Network Endpoints 2 loadBalancerName "ilbset"
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a>Creare un endpoint di desktop remoto per una macchina virtuale

È possibile creare un traffico di rete tooforward endpoint desktop remoto da una porta locale tooa di porta pubblica per l'utilizzo di una macchina virtuale specifica `azure vm endpoint create`.

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a>Rimuovere la macchina virtuale dal servizio di bilanciamento del carico

È possibile rimuovere una macchina virtuale da un bilanciamento del carico interno impostato tramite l'eliminazione di endpoint hello associata. Dopo la rimozione di endpoint hello, macchina virtuale hello non appartengono a bilanciamento del carico toohello imposta più.

Utilizzando l'esempio hello precedente, è possibile rimuovere endpoint hello creato per la macchina virtuale "DB1" dal servizio di bilanciamento del carico interno "ilbset" utilizzando il comando hello `azure vm endpoint delete`.

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

Per ulteriori informazioni, vedere `azure vm endpoint --help` .

## <a name="next-steps"></a>Passaggi successivi

[Configurare una modalità di distribuzione del servizio di bilanciamento del carico utilizzando l’affinità dell’IP di origine](load-balancer-distribution-mode.md)

[Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico](load-balancer-tcp-idle-timeout.md)
