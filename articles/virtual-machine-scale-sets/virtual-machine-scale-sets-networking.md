---
title: "aaaNetworking per il set di scalabilità di macchine virtuali di Azure | Documenti Microsoft"
description: "Configurazione delle proprietà della rete per i set di scalabilità di macchine virtuali di Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: guybo
ms.openlocfilehash: ef3f0cfe648d2195c051a73987e654f0e15d13bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a>Rete per i set di scalabilità di macchine virtuali di Azure

Quando si distribuisce una macchina virtuale di Azure di scala impostato tramite il portale di hello, alcune proprietà di rete vengono impostate come predefinite, ad esempio un servizio di bilanciamento del carico di Azure con connessioni in entrata regole NAT. In questo articolo viene descritto come toouse alcune hello più avanzate funzionalità di rete che è possibile configurare con scala imposta.

È possibile configurare le funzionalità hello trattate in questo articolo, utilizzando i modelli di gestione risorse di Azure. Sono inclusi anche esempi dell'interfaccia della riga di comando di Azure e di PowerShell per le funzionalità selezionate. Usare l'interfaccia della riga di comando 2.10 e PowerShell 4.2.0 o versione successiva.

## <a name="accelerated-networking"></a>Rete accelerata
Azure [Accelerated rete](../virtual-network/virtual-network-create-vm-accelerated-networking.md) migliora le prestazioni di rete abilitando la macchina virtuale tooa di single root i/o virtualization (SR-IOV). toouse accelerated con set di scalabilità di rete, impostare enableAcceleratedNetworking troppo**true** nelle impostazioni di configurazioni del set di scalabilità. ad esempio:
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
      "name": "niconfig1",
      "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
          ...
        ]
      }
    }
   ]
}
```

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a>Creare un set di scalabilità che faccia riferimento a un'istanza di Azure Load Balancer esistente
Quando viene creato un set di scalabilità mediante hello portale di Azure, viene creato un nuovo bilanciamento del carico per la maggior parte delle opzioni di configurazione. Se si crea un set di scalabilità, che deve tooreference un bilanciamento del carico esistente, è possibile farlo tramite CLI. Hello lo script di esempio seguente crea un bilanciamento del carico e quindi crea un set di scalabilità, che fa riferimento a essa:
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a>Impostazioni DNS configurabili
Per impostazione predefinita, set di scalabilità di intraprendere hello le impostazioni DNS specifiche di hello tra reti VIRTUALI e subnet che in cui sono stati creati. È tuttavia possibile configurare le impostazioni DNS hello per una scala impostata direttamente.
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a>Creazione di un set di scalabilità con server DNS configurabili
toocreate una scala impostata con una configurazione DNS personalizzata utilizzando 2.0 CLI, aggiungere hello **-server - dns** argomento toohello **vmss creare** separati di comando, seguito da uno spazio indirizzi ip del server. ad esempio:
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
server DNS personalizzati tooconfigure in un modello di Azure, aggiungere configurazioni sezione del set di una scala di toohello proprietà dnsSettings. ad esempio:
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a>Creazione di un set di scalabilità con nomi di dominio di macchine virtuali configurabili
toocreate una scala impostata con un nome DNS personalizzato per le macchine virtuali utilizzando 2.0 CLI, aggiungere hello **nome di dominio - vm** argomento toohello **vmss creare** comando, seguito da una stringa che rappresenta il nome di dominio di hello.

nome di dominio tooset hello in un modello di Azure, aggiungere un **dnsSettings** proprietà set di scalabilità toohello **configurazioni** sezione. ad esempio:

```json
"networkProfile": {
  "networkInterfaceConfigurations": [
    {
    "name": "nic1",
    "properties": {
      "primary": "true",
      "ipConfigurations": [
      {
        "name": "ip1",
        "properties": {
          "subnet": {
            "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
          },
          "publicIPAddressconfiguration": {
            "name": "publicip",
            "properties": {
            "idleTimeoutInMinutes": 10,
              "dnsSettings": {
                "domainNameLabel": "[parameters('vmssDnsName')]"
              }
            }
          }
        }
      }
    ]
    }
}
```

output di Hello, per il nome dns di ogni macchina virtuale sarà in hello seguente formato: 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a>IPv4 pubblico per macchina virtuale
Per le macchine virtuali di un set di scalabilità di Azure in genere non sono necessari indirizzi IP pubblici specifici. Per la maggior parte degli scenari, è più economico e sicuro tooassociate un pubblica IP indirizzo tooa carico bilanciamento o tooan singola macchina virtuale (noto anche come jumpbox), che instrada le macchine virtuali set tooscale le connessioni in ingresso in base alle esigenze (ad esempio, tramite regole NAT in ingresso).

Tuttavia, alcuni scenari richiedono set di scalabilità di macchine virtuali toohave proprio indirizzo IP pubblico indirizzi. Il gioco è riportato un esempio, in cui una console deve toomake una connessione diretta tooa cloud macchina virtuale, che esegue l'elaborazione di gioco fisica. Un altro esempio è toomake connessioni esterne tooone necessario le macchine virtuali in un altro in aree geografiche in un database distribuito.

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a>Creazione di un set di scalabilità con un IP pubblico per ogni macchina virtuale
toocreate un set di scalabilità che assegna una pubblica macchina virtuale tooeach di indirizzi IP con 2.0 CLI, aggiungere hello **-public-ip per ogni vm** parametro toohello **vmss creare** comando. 

toocreate una scala impostata utilizzando un modello di Azure, assicurarsi hello API versione di hello risorsa Microsoft.Compute/virtualMachineScaleSets almeno **2017-03-30**e aggiungere un **publicIpAddressConfiguration**Set di scalabilità di toohello proprietà JSON della sezione di configurazione IP. ad esempio:

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
Modello di esempio: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)

### <a name="querying-hello-public-ip-addresses-of-hello-virtual-machines-in-a-scale-set"></a>Esecuzione di query hello indirizzo IP pubblico del set di indirizzi di hello le macchine virtuali in una scala
gli indirizzi IP pubblici di toolist hello assegnato tooscale set le macchine virtuali utilizzando 2.0 CLI, utilizzare hello **az vmss elenco-istanza-public-IP** comando.

scala toolist imposta gli indirizzi IP pubblici tramite PowerShell, utilizzare hello _Get AzureRmPublicIpAddress_ comando. ad esempio:
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

È inoltre possibile gli indirizzi IP pubblici di query hello facendo riferimento direttamente all'id della configurazione degli indirizzi IP pubblica hello risorsa hello. ad esempio:
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

gli indirizzi IP pubblici di tooquery hello assegnato tooscale set le macchine virtuali utilizzando hello [Esplora inventario risorse di Azure](https://resources.azure.com), o hello API REST di Azure con la versione **2017-03-30** o versione successiva.

indirizzi IP pubblici tooview per una scala impostata utilizzando hello Esplora inventario risorse, esaminare hello **publicipaddresses** sezione del set di scalabilità. Ad esempio: https://resources.azure.com/subscriptions/_ID_sottoscrizione_/resourceGroups/_gruppo_di_risorse_/providers/Microsoft.Compute/virtualMachineScaleSets/_set_di_scalabilità_di_macchine_virtuali_/publicipaddresses

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

Output di esempio:
```json
{
  "value": [
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/pipvmss/virtualMachines/0/networkInterfaces/pipvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"a64060d5-4dea-4379-a11d-b23cd49a3c8d\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "ee8cb20f-af8e-4cd6-892f-441ae2bf701f",
        "ipAddress": "13.84.190.11",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/0/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    },
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"5f6ff30c-a24c-4818-883c-61ebd5f9eee8\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "036ce266-403f-41bd-8578-d446d7397c2f",
        "ipAddress": "13.84.159.176",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    }
```

## <a name="multiple-ip-addresses-per-nic"></a>Più indirizzi IP per ogni scheda di interfaccia di rete
Tutte le schede NIC associata tooa che macchina virtuale in un set di scalabilità può avere uno o più configurazioni IP associate. A ogni configurazione viene assegnato un indirizzo IP privato. Ogni configurazione può anche avere una risorsa di indirizzo IP pubblico associata. toounderstand quanti indirizzi IP possono essere assegnato tooa NIC, e quanti indirizzi IP pubblici, è possibile utilizzare in una sottoscrizione di Azure, fare riferimento troppo[i limiti di Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).

## <a name="multiple-nics-per-virtual-machine"></a>Più schede di interfaccia di rete per ogni macchina virtuale
È possibile disporre di schede NIC too8 per ogni macchina virtuale, a seconda delle dimensioni della macchina. numero massimo di schede NIC Hello per ogni computer è disponibile in hello [articolo dimensioni VM](../virtual-machines/windows/sizes.md). Hello riportato di seguito è che una scala di imposta il profilo di rete con più voci di interfaccia di rete e più indirizzi IP pubblici per ogni macchina virtuale:
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
        "name": "nic1",
        "properties": {
            "primary": "true",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        },
        {
        "name": "nic2",
        "properties": {
            "primary": "false",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        }
    ]
}
```

## <a name="nsg-per-scale-set"></a>Gruppi di sicurezza di rete per ogni set di scalabilità
Gruppi di sicurezza di rete possono essere applicati direttamente il set di scalabilità tooa, aggiungendo una sezione di configurazione riferimento toohello rete interfaccia della scala hello imposta proprietà della macchina virtuale.

ad esempio: 
```
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sulle reti virtuali di Azure, vedere troppo[questa documentazione](../virtual-network/virtual-networks-overview.md).
