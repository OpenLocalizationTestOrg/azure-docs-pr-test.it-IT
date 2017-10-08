---
title: aaaAccess e la sicurezza in modelli di Azure per le macchine virtuali di Windows | Documenti Microsoft
description: Macchine virtuali di Azure - Esercitazione DotNet Core
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: e671fc45-5e4d-40fd-aac5-290892713cc0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4b8227ae745b3b0a22d136e98d18479f8b1504c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a>Accesso e sicurezza nei modelli di Azure Resource Manager per macchine virtuali Windows

Applicazioni ospitate in Azure è probabilmente necessario toobe accesso su hello internet o una VPN o connessione Express Route con Azure. Hello negozio applicazione di esempio viene reso disponibile nel sito web hello hello internet con un indirizzo IP pubblico. Con l'accesso è stata stabilita, devono essere protette connessioni toohello accesso alle applicazioni e toohello risorse della macchina virtuale se stessi. La sicurezza dell'accesso è garantita da un gruppo di sicurezza di rete. 

Questo documento illustra in dettaglio come hello applicazione negozio viene protetto nel modello di gestione risorse di Azure di esempio hello. Tutte le dipendenze e le configurazioni univoche sono evidenziate. Per un'esperienza ottimale hello, pre-distribuire un'istanza di hello soluzione tooyour sottoscrizione di Azure e di lavoro nel modello di gestione risorse di Azure hello. è disponibili qui: modello completa Hello [musica archivio distribuzione in Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="public-ip-address"></a>Indirizzo IP pubblico
tooprovide accesso pubblico tooan risorse di Azure, una risorsa di indirizzo IP pubblica può essere utilizzato. L'indirizzo IP pubblico può essere configurato con un indirizzo IP statico o dinamico. Se viene utilizzato un indirizzo dinamico e macchina virtuale hello viene arrestata e deallocata, gli indirizzi di hello viene rimosso. Quando viene riavviato macchina hello, può essere assegnato un indirizzo IP pubblico diverso. modifica degli indirizzi tooprevent un IP, un indirizzo IP riservato può essere utilizzato. 

Un indirizzo IP pubblico possono essere aggiunti a un modello di Azure Resource Manager tooan utilizzando Visual Studio aggiungere Creazione guidata nuova risorsa, hello o mediante l'inserimento di un oggetto JSON valido in un modello. 

Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [indirizzo IP pubblico](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicIpAddressName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "public-ip"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

Un indirizzo IP pubblico può essere associato a una scheda di rete virtuale o a un servizio di bilanciamento del carico. In questo esempio, poiché hello sito Web di negozio viene bilanciato tra più macchine virtuali, hello indirizzo IP pubblico è collegato toohello bilanciamento del carico.

Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [associazione indirizzo IP pubblico con bilanciamento del carico](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

Hello indirizzo IP pubblico come rilevato da hello portale di Azure. Si noti che l'indirizzo IP pubblico hello è servizio di bilanciamento del carico tooa associati e non una macchina virtuale. Bilanciamento del carico di rete descritti nel documento successivo di hello di questa serie.

![Indirizzo IP pubblico](./media/dotnet-core-3-access-security/pubip-win.png)

Per altre informazioni sugli indirizzi IP pubblici di Azure, vedere [Indirizzi IP in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).

## <a name="network-security-group"></a>Gruppo di sicurezza di rete
Dopo l'accesso è stato stabilito tooAzure risorse, l'accesso deve essere limitato. Per le macchine virtuali di Azure, la sicurezza dell'accesso è garantita da un gruppo di sicurezza di rete. Hello negozio applicazione di esempio tutte le macchine virtuali toohello di accesso è limitato, ad eccezione di sulla porta 80 per l'accesso http e la porta 3389 per l'accesso RDP. Un gruppo di sicurezza di rete può essere aggiunto il modello di Azure Resource Manager tooan utilizzando Visual Studio aggiungere Creazione guidata nuova risorsa, hello o mediante l'inserimento di un oggetto JSON valido in un modello.

Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [Network Security Group](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('networkSecurityGroup')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-security-group"
  },
  "properties": {
    "securityRules": [
      {
        "name": "http",
        "properties": {
          "description": "http endpoint",
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80",
          "sourceAddressPrefix": "*",
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
      ........<truncated> 
    ]
  }
},
```

In questo esempio, gruppo di sicurezza di rete hello è associato l'oggetto di subnet hello dichiarato nella risorsa di rete virtuale hello. 

Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [associazione gruppo di sicurezza di rete con rete virtuale](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).

```json
"subnets": [
  {
    "name": "[variables('subnetName')]",
    "properties": {
      "addressPrefix": "10.0.0.0/24",
      "networkSecurityGroup": {
        "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
      }
    }
  }
]
```

Ecco il gruppo di sicurezza di rete hello simile da hello portale di Azure. Si noti che un gruppo di sicurezza di rete può essere associato a una subnet e/o a un'interfaccia di rete. In questo caso, hello NSG è subnet tooa associato. In questa configurazione, hello in ingresso regole si applica tooall macchine virtuali connesse toohello subnet.

![Gruppo di sicurezza di rete](./media/dotnet-core-3-access-security/nsg-win.png)

Per informazioni approfondite sui gruppi di sicurezza di rete, vedere [Che cos'è un gruppo di sicurezza di rete](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).

## <a name="next-step"></a>Passaggio successivo
<hr>

[Passaggio 3: Disponibilità e scalabilità nei modelli di Azure Resource Manager](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

