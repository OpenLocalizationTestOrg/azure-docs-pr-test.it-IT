---
title: aaaDeploying risorse di calcolo di Windows con modelli di gestione risorse di Azure | Documenti Microsoft
description: Macchine virtuali di Azure - Esercitazione DotNet Core
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b026fe81-1bc1-4899-ac32-886091671498
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dee228a492b08053713829e156e5b5ba304d7588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-windows-vms"></a>Architettura delle applicazioni con i modelli di Azure Resource Manager per macchine virtuali Windows

Quando si sviluppa una distribuzione di gestione risorse di Azure, i requisiti di calcolo necessario toobe mappato tooAzure risorse e servizi. Se un'applicazione è costituita da diversi endpoint http, un database e un servizio di memorizzazione di dati, hello risorse di Azure che ospitano ognuno di questi componenti deve toobe ragionato. Ad esempio, un'applicazione hello esempio negozio include un'applicazione web ospitata in una macchina virtuale e un database SQL, che è ospitato in database SQL di Azure. 

Questo documento vengono indicati come risorse di calcolo negozio hello configurate nel modello di gestione risorse di Azure di esempio hello. Tutte le dipendenze e le configurazioni univoche sono evidenziate. Per un'esperienza ottimale hello, pre-distribuire un'istanza di hello soluzione tooyour sottoscrizione di Azure e di lavoro nel modello di gestione risorse di Azure hello. è disponibili qui: modello completa Hello [musica archivio distribuzione in Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="virtual-machine"></a>Macchina virtuale
applicazione di archiviazione di file musicali Hello include un'applicazione web in cui i clienti possono esplorare e acquistare musica. Esistono vari servizi di Azure che possono ospitare applicazioni Web. In questo esempio viene usata una macchina virtuale. Utilizza modello negozio di esempio hello, viene distribuita una macchina virtuale, installare un server web e sito Web di archivio musica hello installato e configurato. Per i migliori risultati hello di questo articolo, distribuzione della macchina virtuale solo hello è descritta in dettaglio. configurazione di Hello del server web hello e dell'applicazione hello è descritta in dettaglio in un articolo più avanti.

Una macchina virtuale può essere aggiunti tooa modello utilizzando Visual Studio Aggiungi nuova risorsa o procedura guidata, inserendo JSON valido nel modello di distribuzione hello hello. Quando si distribuisce una macchina virtuale, sono necessarie anche alcune risorse correlate. Se usi Visual Studio toocreate hello modello, queste risorse vengono create automaticamente. Se si crea manualmente il modello di hello, queste risorse devono toobe inserito e configurato.

Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [JSON di macchina virtuale](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).

```json
{
  {
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "tags": {
    "displayName": "virtual-machine"
  },
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('vhdStorageName'))]",
    "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]",
    "nicLoop"
  ],
  "properties": {
    "availabilitySet": {
      "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
    },
  ........<truncated>  
}
```

Una volta distribuito, le proprietà della macchina virtuale hello possono essere visualizzate nel portale di Azure hello.

![Macchina virtuale](./media/dotnet-core-2-architecture/vm-win.png)

## <a name="storage-account"></a>Account di archiviazione
Gli account di archiviazione presentano molte funzionalità e opzioni di archiviazione. Per il contesto di hello delle macchine virtuali di Azure, un account di archiviazione contiene hello dischi rigidi virtuali della macchina virtuale hello e per eventuali dischi dati aggiuntivi. esempio di negozio Hello include uno storage account toohold hello unità disco rigido virtuale di ogni macchina virtuale nella distribuzione hello. 

Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [Account di archiviazione](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[variables('vhdStorageName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "storage-account"
  },
  "properties": {
    "accountType": "[variables('vhdStorageType')]"
  }
}
```

Un account di archiviazione è associato a una macchina virtuale all'interno della dichiarazione di modello di gestione risorse di hello della macchina virtuale hello. 

Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [macchina virtuale e Account di archiviazione associazione](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).

```json
"osDisk": {
  "name": "osdisk",
  "vhd": {
    "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/',variables('vhdStorageName')), '2015-06-15').primaryEndpoints.blob,'vhds/osdisk', copyindex(), '.vhd')]"
  },
  "caching": "ReadWrite",
  "createOption": "FromImage"
}
```

Dopo la distribuzione, l'account di archiviazione hello possono essere visualizzati nel portale di Azure hello.

![Account di archiviazione](./media/dotnet-core-2-architecture/storacct-win.png)

Facendo clic in un contenitore blob account di archiviazione hello, possono essere visualizzati i file di disco rigido virtuale hello per ogni macchina virtuale distribuita con il modello di hello.

![Unità disco rigido virtuali](./media/dotnet-core-2-architecture/vhd-win.png)

Per altre informazioni su Archiviazione di Azure, vedere [Documentazione su Archiviazione](https://azure.microsoft.com/documentation/services/storage/).

## <a name="virtual-network"></a>Rete virtuale
Se una macchina virtuale richiede una rete interna, ad esempio hello possibilità toocommunicate con altre macchine virtuali e le risorse di Azure, è necessario una rete virtuale di Azure.  Una rete virtuale non rendere hello macchina virtuale accessibili tramite internet hello. La connettività pubblica richiede un indirizzo IP pubblico, come descritto più avanti in questa serie.

Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [rete virtuale e le subnet](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/virtualNetworks",
  "name": "[variables('virtualNetworkName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Network/networkSecurityGroups/', variables('networkSecurityGroup'))]"
  ],
  "tags": {
    "displayName": "virtual-network"
  },
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/24"
      ]
    },
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
  }
}
```

Dal portale di Azure hello, rete virtuale hello è simile a hello seguente immagine. Si noti che tutte le macchine virtuali distribuite con il modello di hello toohello collegati di rete virtuale.

![Rete virtuale](./media/dotnet-core-2-architecture/vnet-win.png)

## <a name="network-interface"></a>Interfaccia di rete
 Un'interfaccia di rete si connette a una rete virtuale della macchina virtuale tooa, in particolare subnet tooa che è stata definita nella rete virtuale hello. 

 Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [interfaccia di rete](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceName'), copyindex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-interface"
  },
  "copy": {
    "name": "nicLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
    "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIpAddressName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'RDP-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "subnet": {
            "id": "[variables('subnetRef')]"
          },
          "loadBalancerBackendAddressPools": [
            {
              "id": "[variables('lbPoolID')]"
            }
          ],
          "loadBalancerInboundNatRules": [
            {
              "id": "[concat(variables('lbID'),'/inboundNatRules/RDP-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

Ogni risorsa di macchina virtuale include un profilo di rete, interfaccia di rete Hello è associata a una macchina virtuale hello in questo profilo.  

Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [il profilo di rete di macchina virtuale](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceName'), copyindex()))]"
    }
  ]
}
```

Dal portale di Azure hello, l'interfaccia di rete hello è simile a hello seguente immagine. indirizzo IP interno Hello e associazione di hello macchina virtuale possono essere visualizzati sulla risorsa di interfaccia di rete hello.

![Interfaccia di rete](./media/dotnet-core-2-architecture/nic-win.png)

Per altre informazioni sulle reti virtuali di Azure, vedere [Documentazione su Rete virtuale](https://azure.microsoft.com/documentation/services/virtual-network/).

## <a name="azure-sql-database"></a>Database SQL di Azure
Macchina virtuale tooa hosting del sito Web di hello Negozio, un Database di SQL Azure è inoltre database dell'archivio di musica hello toohost distribuito. Hello vantaggio offerto dall'utilizzo del Database SQL di Azure qui è un secondo set di macchine virtuali che non sia obbligatorio, scalabilità e disponibilità è incorporata nel servizio di hello.

È possibile aggiungere un database SQL di Azure utilizzando Visual Studio Aggiungi nuova risorsa o procedura guidata, inserendo un JSON valido in un modello di hello. Hello risorsa di SQL Server include un nome utente e una password che vengono concessi i diritti amministrativi sull'istanza di SQL Server hello. Viene inoltre aggiunta una risorsa di firewall SQL. Per impostazione predefinita, le applicazioni ospitate in Azure sono in grado di tooconnect con l'istanza SQL hello. applicazione esterna tooallow tali una SQL Server Management studio tooconnect toohello istanza SQL, firewall hello deve toobe configurato. Per i migliori risultati hello della demo negozio hello, la configurazione predefinita di hello è corretta. 

Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [database SQL di Azure](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicstoresqlName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('adminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicstoresqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

Visualizzazione di hello SQL server e database MusicStore come illustrato nel portale di Azure hello.

![SQL Server](./media/dotnet-core-2-architecture/sql-win.png)

Per altre informazioni sulla distribuzione del database SQL di Azure, vedere [Documentazione su Database SQL](https://azure.microsoft.com/documentation/services/sql-database/).

## <a name="next-step"></a>Passaggio successivo
<hr>

[Passaggio 2: Accesso e sicurezza nei modelli di Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

