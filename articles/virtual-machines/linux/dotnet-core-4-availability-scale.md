---
title: aaaAvailability e scala in modelli di gestione risorse di Azure | Documenti Microsoft
description: Macchine virtuali di Azure - Esercitazione DotNet Core
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8fcfea79-f017-4658-8c51-74242fcfb7f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6f830ca0a64e6b65859312bdf31dc0af59e2b978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-linux-vms"></a>Disponibilità e scalabilità nei modelli di Azure Resource Manager per macchine virtuali Linux

Disponibilità e scalabilità vedere toouptime e hello richiesta toomeet possibilità. Se un'applicazione deve essere del 99,9% di tempo hello, è necessario toohave un'architettura che consente di più risorse di calcolo simultanee. Ad esempio, invece di un singolo sito Web, una configurazione con un livello più elevato di disponibilità include più istanze dello stesso sito, con bilanciamento del carico tecnologia li hello. In questa configurazione, un'istanza di un'applicazione hello può essere disattivata per manutenzione, mentre hello rimanenti continua toofunction. Scala in hello invece fa riferimento la domanda di tooserve tooan applicazioni possibilità. Con un carico bilanciata applicazione, aggiungendo o rimuovendo istanze dal pool hello consente una richiesta di applicazione tooscale toomeet.

Questo documento illustra in dettaglio come distribuzione di esempio negozio hello è configurato per la disponibilità e scalabilità. Tutte le dipendenze e le configurazioni univoche sono evidenziate. Per un'esperienza ottimale hello, pre-distribuire un'istanza di hello soluzione tooyour sottoscrizione di Azure e di lavoro nel modello di gestione risorse di Azure hello. è disponibili qui: modello completa Hello [distribuzione archivio musica in Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

## <a name="availability-set"></a>Set di disponibilità
Un set di disponibilità si estende logicamente sulle macchine virtuali di Azure attraverso host fisici e altri componenti dell'infrastruttura, ad esempio alimentatori e hardware di rete fisica. I set di disponibilità assicurano che non tutte le macchine virtuali siano interessate da attività di manutenzione, errori dei dispositivi o altri tempi di inattività. Un Set di disponibilità può essere aggiunto tooan modello di gestione risorse di Azure utilizzando Visual Studio aggiungere Creazione guidata nuova risorsa hello o inserimento JSON valido in un modello.

Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [Set di disponibilità](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "avalibility-set"
  },
  "properties": {
    "platformUpdateDomainCount": 5,
    "platformFaultDomainCount": 3
  }
}
```

Un set di disponibilità viene dichiarato come proprietà di una risorsa di macchina virtuale. 

Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [Set di disponibilità di associazione con la macchina virtuale](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
disponibilità Hello impostata come illustrato da hello portale di Azure. Ogni macchina virtuale e informazioni dettagliate sulla configurazione di hello sono illustrate di seguito.

![Set di disponibilità](./media/dotnet-core-4-availability-scale/aset.png)

Per informazioni approfondite sui set di disponibilità, vedere [Gestione della disponibilità delle macchine virtuali](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

## <a name="network-load-balancer"></a>Servizio di bilanciamento del carico
Mentre un set di disponibilità garantisce tolleranza di errore di applicazione, un bilanciamento del carico rende disponibili molte istanze di un'applicazione hello in un unico indirizzo di rete. Più istanze di un'applicazione possono essere ospitate nel numero di macchine virtuali, ciascuno di essi connessa tooa servizio di bilanciamento del carico. Come si accede a un'applicazione hello, le route del servizio di bilanciamento carico di hello hello richiesta in ingresso tra i membri di hello associata. Un servizio di bilanciamento del carico possono essere aggiunti utilizzando Visual Studio aggiungere Creazione guidata nuova risorsa hello o inserendo correttamente formattato risorse JSON nel modello di gestione risorse di Azure hello.

Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [bilanciamento del carico di rete](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-front"
  },
  ........<truncated>
}
```

Poiché l'applicazione di esempio hello è esposto toohello internet con un indirizzo IP pubblico, questo indirizzo è associato con bilanciamento del carico hello. 

Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [associazione di bilanciamento del carico di rete con indirizzo IP pubblico](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicipaddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

Dal portale di Azure hello, hello Panoramica di bilanciamento carico di rete Mostra associazione hello con indirizzo IP pubblico hello.

![Servizio di bilanciamento del carico](./media/dotnet-core-4-availability-scale/nlb.png)

## <a name="load-balancer-rule"></a>Regola del servizio di bilanciamento del carico
Quando si utilizza un bilanciamento del carico, vengono configurate le regole che controllano come il traffico viene bilanciato tra le risorse di hello previsto. Con un'applicazione hello esempio Negozio, il traffico che arriva nella porta 80 dell'indirizzo IP pubblico hello e viene distribuito tra la porta 80 di tutte le macchine virtuali. 

Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [regola di bilanciamento del carico](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).

```json
"loadBalancingRules": [
  {
    "name": "[variables('loadBalencerRule')]",
    "properties": {
      "frontendIPConfiguration": {
        "id": "[concat(resourceId('Microsoft.Network/loadBalancers', variables('loadBalancerName')), '/frontendIPConfigurations/LoadBalancerFrontend')]"
      },
      "backendAddressPool": {
        "id": "[variables('lbPoolID')]"
      },
      "protocol": "Tcp",
      "frontendPort": 80,
      "backendPort": 80,
      "enableFloatingIP": false,
      "idleTimeoutInMinutes": 5,
      "probe": {
        "id": "[variables('lbProbeID')]"
      }
    }
  }
]
```

Una vista della rete hello caricare regola di bilanciamento del carico dal portale di hello.

![Regola del servizio di bilanciamento del carico di rete](./media/dotnet-core-4-availability-scale/lbrule.png)

## <a name="load-balancer-probe"></a>Probe del servizio di bilanciamento del carico
servizio di bilanciamento del carico Hello deve inoltre toomonitor ogni macchina virtuale in modo che le richieste vengono soddisfatte solo i sistemi toorunning. Questo monitoraggio avviene tramite l'esecuzione costante del probe su una porta predefinita. distribuzione di negozio Hello è tooprobe configurata la porta 80 in tutti inclusa le macchine virtuali. 

Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [Probe di bilanciamento del carico](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).

```json
"probes": [
  {
    "properties": {
      "protocol": "Tcp",
      "port": 80,
      "intervalInSeconds": 15,
      "numberOfProbes": 2
    },
    "name": "lbprobe"
  }
]
```

probe di bilanciamento del carico Hello rilevato da hello portale di Azure.

![Probe del servizio di bilanciamento del carico di rete](./media/dotnet-core-4-availability-scale/lbprobe.png)

## <a name="inbound-nat-rules"></a>Regole NAT in ingresso
Quando si utilizza un bilanciamento del carico, è necessario toobe regole allocate che forniscono l'accesso non carico bilanciato tooeach macchina virtuale. Ad esempio, quando si crea una connessione SSH con ogni macchina virtuale, il carico del traffico non deve essere bilanciato, ma è necessario che sia configurato un percorso predeterminato. I percorsi di questo tipo vengono configurati mediante una risorsa di regola NAT in ingresso. Utilizzare questa risorsa, comunicazioni in ingresso possono essere mappato tooindividual macchine virtuali. 

Con l'applicazione di archiviazione di file musicali hello, una porta a partire da 5000 è mappato tooport 22 in ogni macchina virtuale per l'accesso SSH. Hello `copyindex()` funzione è utilizzata tooincrement hello porta in ingresso, ad esempio che hello seconda macchina virtuale riceve una porta in ingresso di 5001, hello 5002 terzo e così via. 

Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [le regole NAT in ingresso](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270). 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'SSH-VM', copyIndex())]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "lbNatLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
  ],
  "properties": {
    "frontendIPConfiguration": {
      "id": "[variables('ipConfigID')]"
    },
    "protocol": "tcp",
    "frontendPort": "[copyIndex(5000)]",
    "backendPort": 22,
    "enableFloatingIP": false
  }
}
```

Esempio di una regola NAT in ingresso come hello visualizzato nel portale di Azure. Per ogni macchina virtuale nella distribuzione hello viene creata una regola di SSH NAT.

![Regola NAT in ingresso](./media/dotnet-core-4-availability-scale/natrule.png)

Per informazioni dettagliate su hello bilanciamento del carico di rete di Azure, vedere [bilanciamento del carico per servizi di infrastruttura di Azure](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="deploy-multiple-vms"></a>Distribuire più macchine virtuali
Infine, per una funzione di tooeffectively Set di disponibilità o bilanciamento del carico, sono necessari più macchine virtuali. Più macchine virtuali possono essere distribuite tramite funzione di copia modello hello Azure Resource Manager. Utilizza la funzione di copia hello, non è necessario toodefine un numero finito di macchine virtuali, invece questo valore può essere specificato in modo dinamico in fase di hello della distribuzione. funzione di copia Hello utilizza hello numerose istanze toocreated e gestisce la distribuzione di numero adeguato di hello di macchine virtuali e le risorse associate.

Nel modello di esempio di archivio musica hello è definito un parametro che accetta un numero di istanza. Questo numero viene utilizzato in tutto il modello di hello durante la creazione di macchine virtuali e le relative risorse.

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 1,
  "metadata": {
    "description": "Number of VM instances toobe created behind load balancer."
  }
}
```

In hello risorsa di macchina virtuale, il ciclo di copia hello viene assegnato un nome e numero hello del parametro di istanze usati toocontrol hello copie risultante.

Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [funzione di copia macchina virtuale](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300). 

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Compute/virtualMachines",
"name": "[concat(variables('vmName'),copyindex())]",
"location": "[resourceGroup().location]",
"copy": {
  "name": "virtualMachineLoop",
  "count": "[parameters('numberOfInstances')]"
}
```

iterazione corrente di Hello della funzione di copia hello accessibili con hello `copyIndex()` (funzione). il valore di Hello della funzione di hello copia indice può essere utilizzato tooname le macchine virtuali e altre risorse. Ad esempio, se vengono distribuite due istanze di una macchina virtuale, queste devono avere nomi diversi. Hello `copyIndex()` funzione può essere utilizzata come parte della macchina virtuale hello Nome toocreate un nome univoco. Un esempio di hello `copyindex()` funzione utilizzata per scopi di denominazione può essere visualizzati in hello risorsa di macchina virtuale. In questo caso, il nome di computer hello è una concatenazione di hello `vmName` parametro e hello `copyIndex()` (funzione). 

Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [funzione indice copia](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319). 

```json
"osProfile": {
  "computerName": "[concat(parameters('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "linuxConfiguration": {
    "disablePasswordAuthentication": "true",
    "ssh": {
      "publicKeys": [
        {
          "path": "[variables('sshKeyPath')]",
          "keyData": "[parameters('sshKeyData')]"
        }
      ]
    }
  }
}
```

Hello `copyIndex` funzione viene utilizzata più volte nel modello di esempio hello Negozio. Utilizzo di funzioni e risorse `copyIndex` includono tooa nulla specifica una singola istanza di macchina virtuale hello come interfaccia di rete, regole di bilanciamento del carico, e qualsiasi dipende da funzioni. 

Per ulteriori informazioni sulla funzione di copia hello, vedere [creare più istanze delle risorse in Azure Resource Manager](../../resource-group-create-multiple.md).

## <a name="next-step"></a>Passaggio successivo
<hr>

[Passaggio 4: Distribuzione di applicazioni con i modelli di Azure Resource Manager](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

