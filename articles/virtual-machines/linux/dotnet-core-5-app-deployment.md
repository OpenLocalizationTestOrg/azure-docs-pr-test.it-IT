---
title: Distribuzione dell'applicazione con estensioni di macchine virtuali aaaAutomating | Documenti Microsoft
description: Macchine virtuali di Azure - Esercitazione DotNet Core
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 9fc8b1ba-60f5-410b-8190-9f1ff885e50e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 38a02a4271d6b9ba02a473a51794a7bd90ca3a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a>Distribuzione di applicazioni con i modelli di Azure Resource Manager per macchine virtuali Linux

Una volta tutti i requisiti infrastrutturali Azure sono stati identificati e convertiti in un modello di distribuzione, distribuzione di applicazione reale hello deve toobe risolti. Distribuzione dell'applicazione qui fa riferimento a file binari dell'applicazione effettivo hello tooinstalling su risorse di Azure. Per esempio negozio hello, .net Core e NGINX Supervisore necessario toobe installato e configurato in ogni macchina virtuale. Hello negozio file binari necessari toobe installato nella macchina virtuale hello e database dell'archivio di musica hello creato in precedenza.

Questo documento illustra in dettaglio come estensioni di macchine virtuali consente di automatizzare la distribuzione e configurazione tooAzure macchine virtuali dell'applicazione. Tutte le dipendenze e le configurazioni univoche sono evidenziate. Per un'esperienza ottimale hello, pre-distribuire un'istanza di hello soluzione tooyour sottoscrizione di Azure e di lavoro nel modello di gestione risorse di Azure hello. è disponibili qui: modello completa Hello [distribuzione archivio musica in Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

## <a name="configuration-script"></a>Script di configurazione
Estensioni di macchine virtuali sono programmi specializzati eseguite sui automazione configurazione tooprovide di macchine virtuali. Le estensioni sono disponibili per molti scopi specifici, ad esempio un programma antivirus, la configurazione della registrazione e la configurazione di Docker. Un'estensione script personalizzato può essere utilizzato toorun qualsiasi a fronte di una macchina virtuale. Con l'esempio hello Negozio, è backup di macchine virtuali toohello script personalizzato estensione tooconfigure hello Ubuntu e installare un'applicazione hello Negozio. 

Prima che riporta in dettaglio come estensioni di macchine virtuali vengono dichiarate in un modello di gestione risorse di Azure, esaminare script hello che viene eseguito. Questo script configura hello toohost di macchina virtuale Ubuntu hello applicazione Negozio. Durante l'esecuzione, script hello installa il software necessario tutte, installare un'applicazione hello musica archivio dal controllo del codice sorgente e preparare i database di hello. 

applicazione di base toolearn più sull'hosting di .net su Linux, vedere [ambiente di produzione Linux tooa pubblica](https://docs.asp.net/en/latest/publishing/linuxproduction.html).

> Questo esempio è fornito a scopo dimostrativo.
> 
> 

```bash
#!/bin/bash

# install dotnet core
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
sudo apt-get update
sudo apt-get install -y dotnet-dev-1.0.0-preview2-003121

# download application
sudo wget https://raw.github.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/music-store-azure-demo-pub.tar /
sudo mkdir /opt/music
sudo tar -xf music-store-azure-demo-pub.tar -C /opt/music

# install nginx, update config file
sudo apt-get install -y nginx
sudo service nginx start
sudo touch /etc/nginx/sites-available/default
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/nginx-config/default -O /etc/nginx/sites-available/default
sudo cp /opt/music/nginx-config/default /etc/nginx/sites-available/
sudo nginx -s reload

# update and secure music config file
sed -i "s/<replaceserver>/$1/g" /opt/music/config.json
sed -i "s/<replaceuser>/$2/g" /opt/music/config.json
sed -i "s/<replacepass>/$3/g" /opt/music/config.json
sudo chown $2 /opt/music/config.json
sudo chmod 0400 /opt/music/config.json

# config supervisor
sudo apt-get install -y supervisor
sudo touch /etc/supervisor/conf.d/music.conf
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/supervisor/music.conf -O /etc/supervisor/conf.d/music.conf
sudo service supervisor stop
sudo service supervisor start

# pre-create music store database
/usr/bin/dotnet /opt/music/MusicStore.dll &
```

## <a name="vm-script-extension"></a>Estensione script della macchina virtuale
Le estensioni VM possibile eseguire in una macchina virtuale in fase di compilazione con l'inclusione di risorse di estensione hello nel modello di gestione risorse di Azure hello. Hello estensione può essere aggiunta con hello Visual Studio Aggiunta guidata risorsa o tramite l'inserimento di un oggetto JSON valido nel modello hello. risorse di estensione dello Script Hello è annidata all'interno di hello risorsa macchina virtuale. può essere visto nell'esempio seguente hello.

Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [estensione della macchina virtuale Script](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359). 

Si noti che in hello seguito JSON che hello script viene archiviato in GitHub. Questo script può essere incluso anche nell'archiviazione BLOB di Azure. Inoltre, i modelli di gestione risorse di Azure consentono hello script esecuzione stringa tooconstructed in modo che i valori di parametri di modello possono essere usati come parametri per l'esecuzione dello script. In questo caso i dati vengono forniti durante la distribuzione di modelli di hello e questi valori possono quindi essere utilizzati durante l'esecuzione di script hello.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

Per ulteriori informazioni sull'uso delle estensioni hello script personalizzato, vedere [le estensioni degli script personalizzati con modelli di gestione risorse](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="next-step"></a>Passaggio successivo
<hr>

[Explore More Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates)

