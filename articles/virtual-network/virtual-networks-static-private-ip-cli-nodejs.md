---
title: indirizzi IP privati aaaConfigure per le macchine virtuali - CLI di Azure 1.0 | Documenti Microsoft
description: Informazioni su come indirizzi IP privati tooconfigure per macchine virtuali tramite hello Azure interfaccia della riga di comando (CLI) 1.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6caae79c98c7bc5f246b7bb3bb8bd8f032eb2d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-10"></a>Configurare gli indirizzi IP privati per una macchina virtuale utilizzando hello Azure CLI 1.0


## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI 

È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello: 

- [Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) -CLI la prossima generazione per modello di distribuzione di gestione risorse hello 

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Questo articolo descrive il modello di distribuzione di gestione risorse di hello. È anche possibile [gestire l'indirizzo IP privato statico in modello di distribuzione classica hello](virtual-networks-static-private-ip-classic-cli.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

Hello esempio CLI di Azure comandi riportati di seguito prevedono un ambiente semplice già creato. Se si desidera comandi hello toorun così come sono visualizzati in questo documento, innanzitutto compilare descritto nell'ambiente di test di hello [creare una rete virtuale](virtual-networks-create-vnet-arm-cli.md).

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>Come toospecify un indirizzo IP privato statico di indirizzi durante la creazione di una macchina virtuale
una macchina virtuale denominata toocreate *DNS01* in hello *front-end* subnet di una rete virtuale denominata *TestVNet* con un indirizzo IP privato statico di *192.168.1.101*, attenersi alla procedura hello riportata di seguito:

1. Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.
2. Eseguire hello **modalità di configurazione azure** tooswitch tooResource Manager modalità comando, come illustrato di seguito.
   
        azure config mode arm
   
    Output previsto:
   
        info:    New mode is arm
3. Eseguire hello **public-ip di rete di azure creare** toocreate un indirizzo IP pubblico per hello macchina virtuale. elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.
   
        azure network public-ip create -g TestRG -n TestPIP -l centralus
   
    Output previsto:
   
        info:    Executing command network public-ip create
        + Looking up hello public ip "TestPIP"
        + Creating public ip address "TestPIP"
        + Looking up hello public ip "TestPIP"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP
        data:    Name                            : TestPIP
        data:    Type                            : Microsoft.Network/publicIPAddresses
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Allocation method               : Dynamic
        data:    Idle timeout                    : 4
        info:    network public-ip create command OK
   
   * **-g (o --resource-group)**. Nome dell'IP pubblico hello hello risorsa gruppo verrà creato.
   * **-n (o --nome)**. Nome dell'indirizzo IP pubblico hello.
   * **-l (o --location)**. Area di Azure in cui verrà creato l'indirizzo IP pubblico hello. Per questo scenario, *centralus*.
4. Eseguire hello **nic di rete di azure creare** toocreate comando una scheda di rete con un indirizzo IP privato statico. elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.
   
        azure network nic create -g TestRG -n TestNIC -l centralus -a 192.168.1.101 -m TestVNet -k FrontEnd
   
    Output previsto:
   
        + Looking up hello network interface "TestNIC"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC"
        + Looking up hello network interface "TestNIC"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
        data:    Name                            : TestNIC
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.101
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
   
   * **-a (o --private-ip-address)**. Indirizzo IP privato statico per hello scheda di rete.
   * **-m (o --subnet-vnet-name)**. Nome della rete virtuale in cui verrà creato hello NIC hello.
   * **-k (o --subnet-name)**. Nome della subnet hello in cui verrà creato hello NIC.
5. Eseguire hello **macchina virtuale di azure creare** comando toocreate hello macchina virtuale con indirizzo IP pubblico hello e scheda di rete creato in precedenza. elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.
   
        azure vm create -g TestRG -n DNS01 -l centralus -y Windows -f TestNIC -i TestPIP -F TestVNet -j FrontEnd -o vnetstorage -q bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 -u adminuser -p AdminP@ssw0rd
   
    Output previsto:
   
        info:    Executing command vm create
        + Looking up hello VM "DNS01"
        info:    Using hello VM Size "Standard_A1"
        warn:    hello image "bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2" will be used for VM
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account vnetstorage
        + Looking up hello NIC "TestNIC"
        info:    Found an existing NIC "TestNIC"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd" in hello NIC "TestNIC"
        info:    Found public ip parameters, trying toosetup PublicIP profile
        + Looking up hello public ip "TestPIP"
        info:    Found an existing PublicIP "TestPIP"
        info:    Configuring identified NIC IP configuration with PublicIP "TestPIP"
        + Updating NIC "TestNIC"
        + Looking up hello NIC "TestNIC"
        + Creating VM "DNS01"
        info:    vm create command OK
   
   * **-y (o --os-type)**. Tipo di sistema sia per la macchina virtuale, hello *Windows* o *Linux*.
   * **-f (o --nic-name)**. Nome di hello NIC hello VM utilizzerà.
   * **-i (o --public-ip-name)**. Nome di hello IP pubblico hello VM utilizzerà.
   * **-F (o --vnet-name)**. Nome della rete virtuale in cui verrà creato hello VM hello.
   * **-j (o --vnet-subnet-name)**. Nome della subnet hello in cui verrà creato hello macchina virtuale.

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Come indirizzo IP privato statico tooretrieve informazioni sull'indirizzo di una macchina virtuale
IP privato statico di tooview hello informazioni sull'indirizzo di hello macchina virtuale creata con lo script hello precedente, eseguire il comando CLI di Azure seguente hello e osservare i valori hello per *IP privato alloc (metodo)* e *indirizzo IP privato*:

    azure vm show -g TestRG -n DNS01

Output previsto:

    info:    Executing command vm show
    + Looking up hello VM "DNS01"
    + Looking up hello NIC "TestNIC"
    + Looking up hello public ip "TestPIP
    data:    Id                              :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    ProvisioningState               :Succeeded
    data:    Name                            :DNS01
    data:    Location                        :centralus
    data:    Type                            :Microsoft.Compute/virtualMachines
    data:
    data:    Hardware Profile:
    data:      Size                          :Standard_A1
    data:
    data:    Storage Profile:
    data:      Source image:
    data:        Id                          :/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/services/images/bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
    data:
    data:      OS Disk:
    data:        OSType                      :Windows
    data:        Name                        :cli08d7bd987a0112a8-os-1441774961355
    data:        Caching                     :ReadWrite
    data:        CreateOption                :FromImage
    data:        Vhd:
    data:          Uri                       :https://vnetstorage2.blob.core.windows.net/vhds/cli08d7bd987a0112a8-os-1441774961355vhd
    data:
    data:    OS Profile:
    data:      Computer Name                 :DNS01
    data:      User Name                     :adminuser
    data:      Windows Configuration:
    data:        Provision VM Agent          :true
    data:        Enable automatic updates    :true
    data:
    data:    Network Profile:
    data:      Network Interfaces:
    data:        Network Interface #1:
    data:          Id                        :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    data:          Primary                   :true
    data:          MAC Address               :00-0D-3A-90-1A-A8
    data:          Provisioning State        :Succeeded
    data:          Name                      :TestNIC
    data:          Location                  :centralus
    data:            Private IP alloc-method :Static
    data:            Private IP address      :192.168.1.101
    data:            Public IP address       :40.122.213.159
    info:    vm show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Come tooremove un indirizzo IP privato statico di indirizzi da una macchina virtuale
Non è possibile rimuovere un indirizzo IP privato statico da un gruppo NIC nell'infrastruttura CLI di Azure per Gestione risorse. È necessario creare una nuova scheda di rete che utilizza un indirizzo IP dinamico, rimuovere hello NIC precedente da hello macchina virtuale e quindi aggiungere hello toohello NIC nuova macchina virtuale. toochange hello NIC per hello VM usata int eh comandi precedenti, attenersi alla procedura hello riportata di seguito.

1. Eseguire hello **nic di rete di azure creare** comando toocreate una scheda di rete di nuovo utilizzando l'allocazione dell'IP dinamico. Si noti come non è necessario l'indirizzo IP hello toospecify questo momento.
   
        azure network nic create -g TestRG -n TestNIC2 -l centralus -m TestVNet -k FrontEnd
   
    Output previsto:
   
        info:    Executing command network nic create
        + Looking up hello network interface "TestNIC2"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC2"
        + Looking up hello network interface "TestNIC2"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
        data:    Name                            : TestNIC2
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.6
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
2. Eseguire hello **set di macchine virtuali di azure** comando toochange hello scheda di rete utilizzata dalla macchina virtuale hello.
   
        azure vm set -g TestRG -n DNS01 -N TestNIC2
   
    Output previsto:
   
        info:    Executing command vm set
        + Looking up hello VM "DNS01"
        + Looking up hello NIC "TestNIC2"
        + Updating VM "DNS01"
        info:    vm set command OK
3. Se si desidera, eseguire hello **nic di rete di azure Elimina** comando toodelete hello vecchia interfaccia di rete.
   
        azure network nic delete -g TestRG -n TestNIC --quiet
   
    Output previsto:
   
        info:    Executing command network nic delete
        + Looking up hello network interface "TestNIC"
        + Deleting network interface "TestNIC"
        info:    network nic delete command OK

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Come un indirizzo IP privato statico tooadd indirizzo tooan macchina virtuale esistente
tooadd un statico privato IP indirizzo toohello scheda di rete utilizzata dalla macchina virtuale creata utilizzando lo script hello precedente, eseguire hello comando seguente:

    azure network nic set -g TestRG -n TestNIC2 -a 192.168.1.101

Output previsto:

    info:    Executing command network nic set
    + Looking up hello network interface "TestNIC2"
    + Updating network interface "TestNIC2"
    + Looking up hello network interface "TestNIC2"
    data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
    data:    Name                            : TestNIC2
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : centralus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-90-29-25
    data:    Enable IP forwarding            : false
    data:    Virtual machine                 : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    IP configurations:
    data:      Name                          : NIC-config
    data:      Provisioning state            : Succeeded
    data:      Private IP address            : 192.168.1.101
    data:      Private IP Allocation Method  : Static
    data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su [indirizzi IP pubblici riservati](virtual-networks-reserved-public-ip.md) .
* Informazioni su [indirizzi IP pubblici a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md) .
* Consultare hello [API REST per IP riservato](https://msdn.microsoft.com/library/azure/dn722420.aspx).

