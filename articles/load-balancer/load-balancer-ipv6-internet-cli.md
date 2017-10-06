---
title: bilanciamento del carico aaaCreate con una connessione Internet con IPv6 - CLI di Azure | Documenti Microsoft
description: Informazioni su come toocreate un Internet rivolto al bilanciamento del carico con IPv6 in Gestione risorse di Azure utilizzando hello CLI di Azure
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: ipv6, azure load balancer, dual stack, ip pubblico, ipv6 nativo, mobili, iot
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7ff75ac90d74a74e3d0c27672b36fbd955a086a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-hello-azure-cli"></a>Creare un servizio di bilanciamento del carico con IPv6 in Gestione di risorse di Azure mediante Azure CLI hello per Internet

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [Interfaccia della riga di comando di Azure](load-balancer-ipv6-internet-cli.md)
> * [Modello](load-balancer-ipv6-internet-template.md)

Azure Load Balancer è un servizio di bilanciamento del carico di livello 4 (TCP, UDP). servizio di bilanciamento del carico Hello garantisce disponibilità elevata mediante la distribuzione del traffico in entrata tra le istanze del servizio di integrità in servizi cloud o macchine virtuali in un set di bilanciamento del carico. Azure Load Balancer può anche presentare tali servizi su più porte, più indirizzi IP o entrambi.

## <a name="example-deployment-scenario"></a>Scenario di distribuzione di esempio

Hello diagramma seguente vengono illustrate soluzioni di bilanciamento del carico di hello distribuito utilizzando il modello di esempio hello descritto in questo articolo.

![Scenario del bilanciamento del carico](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

In questo scenario creerai hello seguendo le risorse di Azure:

* due macchine virtuali (VM)
* un'interfaccia di rete virtuale per ogni VM con l'assegnazione degli indirizzi IPv4 e IPv6
* un servizio di bilanciamento del carico con connessione Internet con un indirizzo IP pubblico IPv4 e IPv6
* un Set di disponibilità toothat contiene macchine virtuali hello due
* due bilanciamento regole toomap hello VIP toohello privato endpoint pubblici di carico

## <a name="deploying-hello-solution-using-hello-azure-cli"></a>La distribuzione di soluzioni hello utilizzando hello CLI di Azure

Hello alla procedura seguente viene illustrato come una connessione Internet toocreate bilanciamento del carico con Gestione risorse di Azure CLI. Con Gestione risorse di Azure, ogni risorsa viene creata e configurata individualmente e riunire toocreate una risorsa.

toodeploy un bilanciamento del carico, per creare e configurare hello seguenti oggetti:

* Configurazione di IP front-end: contiene gli indirizzi IP pubblici per il traffico di rete in ingresso.
* Pool di indirizzi di back-end - contiene le interfacce di rete (NIC) per tooreceive il traffico di rete dal servizio di bilanciamento del carico hello hello macchine virtuali.
* Regole di bilanciamento del carico - contiene le regole di mapping di una porta pubblica su tooport del servizio di bilanciamento carico di hello nel pool di indirizzi back-end di hello.
* Regole NAT in ingresso - contiene le regole di mapping di una porta pubblica nella porta di tooa del bilanciamento del carico hello per una macchina virtuale specifica nel pool di indirizzi back-end di hello.
* Probe - contiene integrità probe usati toocheck disponibilità delle istanze di macchine virtuali nel pool di indirizzi back-end di hello.

Per altre informazioni, vedere [Supporto di Azure Resource Manager per Load Balancer](load-balancer-arm.md).

## <a name="set-up-your-cli-environment-toouse-azure-resource-manager"></a>Impostare il toouse ambiente CLI Gestione risorse di Azure

Per questo esempio, gli strumenti CLI hello in esecuzione in una finestra di comando di PowerShell. Non si sono utilizzando i cmdlet di Azure PowerShell hello ma si utilizza la leggibilità tooimprove funzionalità script di PowerShell e il riutilizzo.

1. Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.
2. Eseguire hello **azure configurazione modalità** modalità Manager tooResource tooswitch di comando.

    ```azurecli
    azure config mode arm
    ```

    Output previsto:

        info:    New mode is arm

3. Accedi tooAzure e ottenere un elenco di sottoscrizioni.

    ```azurecli
    azure login
    ```

    Immettere le credenziali di Azure quando richiesto.

    ```azurecli
    azure account list
    ```

    Selezionare la sottoscrizione di hello da toouse. Prendere nota dell'Id sottoscrizione hello per successiva hello.

4. Impostare le variabili di PowerShell per l'utilizzo con i comandi CLI hello.

    ```powershell
    $subscriptionid = "########-####-####-####-############"  # enter subscription id
    $location = "southcentralus"
    $rgName = "pscontosorg1southctrlus09152016"
    $vnetName = "contosoIPv4Vnet"
    $vnetPrefix = "10.0.0.0/16"
    $subnet1Name = "clicontosoIPv4Subnet1"
    $subnet1Prefix = "10.0.0.0/24"
    $subnet2Name = "clicontosoIPv4Subnet2"
    $subnet2Prefix = "10.0.1.0/24"
    $dnsLabel = "contoso09152016"
    $lbName = "myIPv4IPv6Lb"
    ```

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a>Creare un gruppo di risorse, un servizio di bilanciamento del carico, una rete virtuale e subnet

1. Creare un gruppo di risorse

    ```azurecli
    azure group create $rgName $location
    ```

2. Creare un servizio di bilanciamento del carico

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. Creare una rete virtuale.

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    Creare due subnet nella rete virtuale.

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-hello-front-end-pool"></a>Creare gli indirizzi IP pubblici per il pool di server front-end hello

1. Impostare le variabili PowerShell hello

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. Creare un pubblico hello front-end IP pool di indirizzi IP.

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > bilanciamento del carico di Hello Usa etichetta hello del dominio dell'indirizzo IP pubblico hello come il nome di dominio completo. Questa distribuzione classica, che utilizza nome del servizio cloud hello come servizio di bilanciamento del carico FQDN hello una modifica.
    > In questo esempio, hello FQDN è *contoso09152016.southcentralus.cloudapp.azure.com*.

## <a name="create-front-end-and-back-end-pools"></a>Creare pool front-end e back-end

Questo esempio crea pool IP front-end hello che riceve il traffico di rete in ingresso di hello nel servizio di bilanciamento del carico hello e pool IP back-end di hello in pool front-end hello invia il traffico di rete con carico bilanciato hello.

1. Impostare le variabili PowerShell hello

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. Creare un pool IP front-end associazione hello creato nel passaggio precedente hello e bilanciamento del carico hello indirizzo IP pubblico.

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-hello-probe-nat-rules-and-lb-rules"></a>Creare regole LB probe hello e le regole NAT

In questo esempio crea hello seguenti elementi:

* un toocheck regola probe per la porta 80 tooTCP di connettività
* un dispositivo NAT regola tootranslate tutto il traffico in ingresso sulla porta 3389 tooport 3389 per RDP<sup>1</sup>
* un dispositivo NAT regola tootranslate tutto il traffico in ingresso sulla porta 3391 tooport 3389 per RDP<sup>1</sup>
* un toobalance regola di bilanciamento carico di tutto il traffico in ingresso sulla porta 80 tooport 80 su hello indirizzi nel pool back-end hello.

<sup>1</sup> le regole NAT sono associati tooa macchina virtuale specifica istanza bilanciamento del carico hello. macchina virtuale specifica toohello e la porta associata alla regola NAT hello, viene inviato il traffico di rete Hello in arrivo sulla porta 3389. È necessario specificare un protocollo (UDP o TCP) per una regola NAT. Entrambi i protocolli non possono essere assegnato toohello stessa porta.

1. Impostare le variabili PowerShell hello

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. Creare il probe hello

    Hello seguente viene creato un probe TCP verifica per la porta TCP tooback-end di connettività 80 ogni 15 secondi. Contrassegna risorsa back-end hello disponibile dopo due tentativi consecutivi non riusciti.

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. Creare le regole NAT in ingresso che consentono le connessioni RDP risorse back-end toohello

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. Creazione di regole che il traffico toodifferent back-end le porte di trasmissione a seconda di quale richiesta hello front-end ha ricevuto un bilanciamento del carico

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. Verificare le impostazioni

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    Output previsto:

        info:    Executing command network lb show
        info:    Looking up hello load balancer "myIPv4IPv6Lb"
        data:    Id                              : /subscriptions/########-####-####-####-############/resourceGroups/pscontosorg1southctrlus09152016/providers/Microsoft.Network/loadBalancers/myIPv4IPv6Lb
        data:    Name                            : myIPv4IPv6Lb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : southcentralus
        data:    Provisioning state              : Succeeded
        data:
        data:    Frontend IP configurations:
        data:    Name             Provisioning state  Private IP allocation  Private IP   Subnet  Public IP
        data:    ---------------  ------------------  ---------------------  -----------  ------  ---------
        data:    FrontendVipIPv4  Succeeded           Dynamic                                     myIPv4Vip
        data:    FrontendVipIPv6  Succeeded           Dynamic                                     myIPv6Vip
        data:
        data:    Probes:
        data:    Name                 Provisioning state  Protocol  Port  Path  Interval  Count
        data:    -------------------  ------------------  --------  ----  ----  --------  -----
        data:    ProbeForIPv4AndIPv6  Succeeded           Tcp       80          15        2
        data:
        data:    Backend Address Pools:
        data:    Name             Provisioning state
        data:    ---------------  ------------------
        data:    BackendPoolIPv4  Succeeded
        data:    BackendPoolIPv6  Succeeded
        data:
        data:    Load Balancing Rules:
        data:    Name                  Provisioning state  Load distribution  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    --------------------  ------------------  -----------------  --------  -------------  ------------  ------------------  -----------------------
        data:    LBRuleForIPv4-Port80  Succeeded           Default            Tcp       80             80            false               4
        data:    LBRuleForIPv6-Port80  Succeeded           Default            Tcp       80             8080          false               4
        data:
        data:    Inbound NAT Rules:
        data:    Name                 Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    -------------------  ------------------  --------  -------------  ------------  ------------------  -----------------------
        data:    NatRule-For-Rdp-VM1  Succeeded           Tcp       3389           3389          false               4
        data:    NatRule-For-Rdp-VM2  Succeeded           Tcp       3391           3389          false               4
        info:    network lb show

## <a name="create-nics"></a>Creare NIC

Creare schede di rete e associarli tooNAT regole, regole di bilanciamento del carico e probe.

1. Impostare le variabili PowerShell hello

    ```powershell
    $nic1Name = "myIPv4IPv6Nic1"
    $nic2Name = "myIPv4IPv6Nic2"
    $subnet1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet1Name"
    $subnet2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet2Name"
    $backendAddressPoolV4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV4Name"
    $backendAddressPoolV6Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV6Name"
    $natRule1V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule1V4Name"
    $natRule2V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule2V4Name"
    ```

2. Creare una scheda di interfaccia di rete per ogni back-end e aggiungere una configurazione di IPv6.

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-hello-back-end-vm-resources-and-attach-each-nic"></a>Creare risorse macchina virtuale back-end di hello e associare ogni scheda di rete

toocreate macchine virtuali, è necessario disporre di un account di archiviazione. Per il bilanciamento del carico, le macchine virtuali hello necessario toobe membri di un set di disponibilità. Per altre informazioni sulla creazione di VM, vedere [Creare una VM di Azure con PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)

1. Impostare le variabili PowerShell hello

    ```powershell
    $storageAccountName = "ps08092016v6sa0"
    $availabilitySetName = "myIPv4IPv6AvailabilitySet"
    $vm1Name = "myIPv4IPv6VM1"
    $vm2Name = "myIPv4IPv6VM2"
    $nic1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic1Name"
    $nic2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic2Name"
    $disk1Name = "WindowsVMosDisk1"
    $disk2Name = "WindowsVMosDisk2"
    $osDisk1Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk1Name.vhd"
    $osDisk2Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk2Name.vhd"
    $imageurn "MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest"
    $vmUserName = "vmUser"
    $mySecurePassword = "PlainTextPassword*1"
    ```

    > [!WARNING]
    > Questo esempio Usa hello username e password per le macchine virtuali hello in testo non crittografato. Appropriato prestare attenzione quando utilizzando le credenziali in hello deselezionare. Per un metodo più sicuro per la gestione delle credenziali in PowerShell, vedere hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.

2. Creare set di account e la disponibilità di archiviazione hello

    Quando si crea hello macchine virtuali, è possibile utilizzare un account di archiviazione esistente. Hello comando seguente crea un nuovo account di archiviazione.

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    Successivamente, creare set di disponibilità hello.

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. Creare macchine virtuali hello con schede di rete hello associata

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a>Passaggi successivi

[Introduzione alla configurazione del bilanciamento del carico interno](load-balancer-get-started-ilb-arm-cli.md)

[Configurare una modalità di distribuzione del servizio di bilanciamento del carico](load-balancer-distribution-mode.md)

[Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico](load-balancer-tcp-idle-timeout.md)
