---
title: indirizzi IP privati aaaConfigure per le macchine virtuali - CLI di Azure 2.0 | Documenti Microsoft
description: Informazioni su come indirizzi IP privati tooconfigure per macchine virtuali tramite hello Azure interfaccia della riga di comando (CLI) 2.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0e278e6ac63c0cda061cf70ab0edfaff5491c03b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-20"></a>Configurare gli indirizzi IP privati per una macchina virtuale utilizzando hello Azure CLI 2.0

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI 

È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello: 

- [Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – la CLI per hello classic e risorse Gestione modelli di distribuzione 
- [Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) -la prossima generazione CLI per modello di distribuzione Gestione risorse hello (in questo articolo)

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Questo articolo descrive il modello di distribuzione di gestione risorse di hello. È anche possibile [gestire l'indirizzo IP privato statico in modello di distribuzione classica hello](virtual-networks-static-private-ip-classic-cli.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> Hello esempio CLI di Azure 2.0 comandi riportati di seguito prevedono un ambiente semplice già creato. Se si desidera comandi hello toorun così come sono visualizzati in questo documento, innanzitutto compilare descritto nell'ambiente di test di hello [creare una rete virtuale](virtual-networks-create-vnet-arm-cli.md).

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a>Specificare un indirizzo IP statico privato durante la creazione di una macchina virtuale

una macchina virtuale denominata toocreate *DNS01* in hello *front-end* subnet di una rete virtuale denominata *TestVNet* con un indirizzo IP privato statico di *192.168.1.101*, attenersi alla procedura hello riportata di seguito:

1. Se non hai ancora, installare e configurare più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) e accedere con un account Azure tooan [accesso az](/cli/azure/#login). 

2. Creare un indirizzo IP pubblico per hello VM con hello [az rete public-ip creare](/cli/azure/network/public-ip#create) comando. elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.

    > [!NOTE]
    > È possibile preferibile o necessario toouse valori diversi per gli argomenti in questa e passaggi successivi, a seconda dell'ambiente.
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    Output previsto:
   
   ```json
   {
        "publicIp": {
            "idleTimeoutInMinutes": 4,
            "ipAddress": "52.176.43.167",
            "provisioningState": "Succeeded",
            "publicIPAllocationMethod": "Static",
            "resourceGuid": "79e8baa3-33ce-466a-846c-37af3c721ce1"
        }
    }
    ```

   * `--resource-group`: Nome del gruppo di risorse hello toocreate hello IP pubblico.
   * `--name`: Nome dell'indirizzo IP pubblico hello.
   * `--location`: Azure area nella quale hello toocreate indirizzo IP pubblico.

3. Eseguire hello [az rete nic creare](/cli/azure/network/nic#create) toocreate comando una scheda di rete con un indirizzo IP privato statico. elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati. 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    Output previsto:
   
    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.101",
                "privateIPAllocationMethod": "Static",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>"
        }
    }
    ```
    
    Parametri

    * `--private-ip-address`: Indirizzo IP privato statico per hello scheda di rete.
    * `--vnet-name`: Nome di rete virtuale hello in cui toocreate hello scheda di rete.
    * `--subnet`: Nome della subnet di hello in cui hello toocreate scheda di rete.

4. Eseguire hello [macchina virtuale di azure creare](/cli/azure/vm/nic#create) comando toocreate hello macchina virtuale con indirizzo IP pubblico hello e scheda di rete creato in precedenza. elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.
   
    ```azurecli
    az vm create \
    --resource-group TestRG \
    --name DNS01 \
    --location centralus \
    --image Debian \
    --admin-username adminuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics TestNIC
    ```

    Output previsto:
   
    ```json
    {
        "fqdns": "",
        "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01",
        "location": "centralus",
        "macAddress": "00-0D-3A-92-C1-66",
        "powerState": "VM running",
        "privateIpAddress": "192.168.1.101",
        "publicIpAddress": "",
        "resourceGroup": "TestRG"
    }
    ```
   
   I parametri diversi da hello base [creare vm az](/cli/azure/vm#create) parametri.

   * `--nics`: Nome di hello toowhich di hello NIC VM è collegato.
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a>Recuperare le informazioni relative all'indirizzo IP privato statico per una macchina virtuale

tooview hello indirizzo IP privato statico che è stato creato, eseguire il comando CLI di Azure seguente hello e osservare i valori hello per *IP privato alloc (metodo)* e *indirizzo IP privato*:

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

Output previsto:

```json
"192.168.1.101"
```

toodisplay hello informazioni IP specifiche di hello NIC per la macchina virtuale, hello query NIC in particolare:

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

output di Hello è simile al seguente:

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a>Rimuovere un indirizzo IP statico privato da una macchina virtuale

Non è possibile rimuovere un indirizzo IP privato statico da una scheda di interfaccia di rete nell'interfaccia della riga di comando per le distribuzioni di Resource Manager. È necessario:
- Creare una nuova scheda di interfaccia di rete che usa un indirizzo IP dinamico
- Impostare hello NIC in VM hello hello appena creati scheda di rete. 

toochange hello NIC per la macchina virtuale utilizzata in comandi hello precedenti, hello procedura hello riportata di seguito.

1. Eseguire hello **nic di rete di azure creare** comando toocreate una scheda di rete di nuovo con un nuovo indirizzo IP di allocazione dell'IP dinamico. Si noti che poiché non è specificato alcun indirizzo IP, il metodo di allocazione hello è **dinamica**.

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    Output previsto:

    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.4",
                "privateIPAllocationMethod": "Dynamic",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "0808a61c-476f-4d08-98ee-0fa83671b010"
        }
    }
    ```

2. Eseguire hello **set di macchine virtuali di azure** comando toochange hello scheda di rete utilizzata dalla macchina virtuale hello.
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    Output previsto:
   
    ```json
    [
        {
            "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC3",
            "primary": true,
            "resourceGroup": "TestRG"
        }
    ]
    ```

    > [!NOTE]
    > Se hello VM è sufficientemente grande toohave più di una scheda di rete, eseguire hello **nic di rete di azure Elimina** comando toodelete hello vecchia interfaccia di rete.
   
## <a name="next-steps"></a>Passaggi successivi
* Informazioni su [indirizzi IP pubblici riservati](virtual-networks-reserved-public-ip.md) .
* Informazioni su [indirizzi IP pubblici a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md) .
* Consultare hello [API REST per IP riservato](https://msdn.microsoft.com/library/azure/dn722420.aspx).

