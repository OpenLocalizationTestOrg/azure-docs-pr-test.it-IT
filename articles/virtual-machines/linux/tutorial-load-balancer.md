---
title: aaaHow tooload bilanciare macchine virtuali Linux in Azure | Documenti Microsoft
description: "Informazioni su come il carico bilanciamento toocreate un'applicazione a elevata disponibilità e sicura tra tre macchine virtuali Linux toouse hello Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: f01752c3caec3489ee13e63000775769f3236e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-linux-virtual-machines-in-azure-toocreate-a-highly-available-application"></a>Come tooload bilanciare macchine virtuali Linux in Azure toocreate applicazioni a disponibilità elevata
Il bilanciamento del carico offre un livello più elevato di disponibilità distribuendo le richieste in ingresso tra più macchine virtuali. In questa esercitazione apprendere hello diversi componenti del servizio di bilanciamento del carico di Azure hello che distribuisce il traffico e garantire disponibilità elevata. Si apprenderà come:

> [!div class="checklist"]
> * Creare un servizio di bilanciamento del carico di Azure
> * Creare un probe di integrità per il servizio di bilanciamento del carico
> * Creare regole del traffico di bilanciamento del carico
> * Utilizzare cloud init toocreate un'app Node.js di base
> * Creare macchine virtuali e collegare bilanciamento del carico tooa
> * Visualizzare un bilanciamento del carico in azione
> * Aggiungere e rimuovere macchine virtuali da un bilanciamento del carico


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="azure-load-balancer-overview"></a>Panoramica di Azure Load Balancer
Azure Load Balancer è un bilanciamento del carico di livello 4 (TCP, UDP) che offre disponibilità elevata mediante la distribuzione del traffico in ingresso nelle macchine virtuali integre. Un probe di integrità di bilanciamento del carico consente di monitorare una determinata porta in ogni macchina virtuale e vengono distribuiti solo il traffico tooan operativo VM.

Definire una configurazione IP front-end che contenga uno o più indirizzi IP pubblici. Questa configurazione IP front-end consente il toobe di applicazioni e del servizio di bilanciamento del carico accessibile tramite Internet hello. 

Le macchine virtuali connesse tooa bilanciamento del carico utilizzando la scheda di interfaccia di rete virtuale (NIC). toodistribute traffico toohello macchine virtuali, un pool di indirizzi back-end contiene indirizzi IP hello di hello virtuale (NIC) connesse toohello bilanciamento del carico.

flusso di hello toocontrol del traffico, definire regole di bilanciamento del carico per porte specifiche e protocolli che eseguono il mapping delle macchine virtuali tooyour.

Se è stato eseguito troppo esercitazione precedente hello[creare un set di scalabilità della macchina virtuale](tutorial-create-vmss.md), è stato creato un servizio di bilanciamento del carico. Tutti questi componenti sono stati configurati per l'utente come parte del set di scalabilità hello.


## <a name="create-azure-load-balancer"></a>Creare un Azure Load Balancer
Questa sezione descrive come è possibile creare e configurare ciascun componente del servizio di bilanciamento del carico hello. Per poter creare un servizio di bilanciamento del carico, è prima necessario creare un gruppo di risorse con [az group create](/cli/azure/group#create). esempio Hello crea un gruppo di risorse denominato *myResourceGroupLoadBalancer* in hello *eastus* percorso:

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a>Creare un indirizzo IP pubblico
tooaccess l'app in hello Internet, è necessario un indirizzo IP pubblico di bilanciamento del carico hello. Creare un indirizzo IP pubblico con [az network public-ip create](/cli/azure/network/public-ip#create). esempio Hello crea un indirizzo IP pubblico denominato *myPublicIP* in hello *myResourceGroupLoadBalancer* gruppo di risorse:

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a>Creare un servizio di bilanciamento del carico
Creare un servizio di bilanciamento del carico con [az network lb create](/cli/azure/network/lb#create). esempio Hello crea un bilanciamento del carico denominato *myLoadBalancer* e assegna hello *myPublicIP* configurazione IP front-end dell'indirizzo toohello:

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a>Creare un probe di integrità
tooallow hello bilanciamento toomonitor hello stato di caricamento dell'app, utilizzare un probe di integrità. probe di integrità Hello dinamicamente aggiunge o rimuove le macchine virtuali dalla rotazione di bilanciamento del carico hello in base alle loro controlli toohealth di risposta. Per impostazione predefinita, una macchina virtuale viene rimosso dalla distribuzione del servizio di bilanciamento del carico hello dopo due tentativi consecutivi non riusciti a intervalli di 15 secondi. Un probe di integrità viene creato in base a un protocollo o una specifica pagina di controllo integrità per l'app. 

Hello di esempio seguente crea un probe TCP. È anche possibile creare probe HTTP personalizzati per i controlli di integrità con granularità fine. Quando si utilizza un probe HTTP personalizzato, è necessario creare pagina di controllo di integrità hello, ad esempio *healthcheck.js*. probe Hello deve restituire un **HTTP 200 OK** risposta per l'host hello carico bilanciamento tookeep hello nella rotazione.

toocreate un probe di integrità TCP, utilizzare [az di rete lb probe creare](/cli/azure/network/lb/probe#create). esempio Hello crea un probe di integrità denominato *myHealthProbe*:

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a>Creare una regola di bilanciamento del carico
Una regola di bilanciamento del carico è toodefine utilizzato come il traffico è toohello distribuita le macchine virtuali. Definire una configurazione IP front-end di hello per il traffico in ingresso hello e hello back-end pool tooreceive hello traffico IP, con origine necessari hello e porta di destinazione. toomake che solo le macchine virtuali integro ricevano il traffico, è inoltre definire toouse probe di integrità hello.

Creare una regola di bilanciamento del carico con [az network lb rule create](/cli/azure/network/lb/rule#create). esempio Hello crea una regola denominata *myLoadBalancerRule*, hello utilizza *myHealthProbe* probe di integrità e bilancia il traffico sulla porta *80*:

```azurecli-interactive 
az network lb rule create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe
```


## <a name="configure-virtual-network"></a>Configurare la rete virtuale
Prima di distribuire alcune macchine virtuali e possibile eseguire il servizio di bilanciamento del test, creare hello che supporta le risorse di rete virtuale. Per ulteriori informazioni sulle reti virtuali, vedere hello [gestire reti virtuali di Azure](tutorial-virtual-network.md) esercitazione.

### <a name="create-network-resources"></a>Creare risorse di rete
Creare una rete virtuale con [az network vnet create](/cli/azure/network/vnet#create). esempio Hello crea una rete virtuale denominata *myVnet* con una subnet denominata *mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

tooadd un gruppo di sicurezza di rete, utilizzare [rete az creare](/cli/azure/network/nsg#create). esempio Hello crea un gruppo di sicurezza di rete denominato *myNetworkSecurityGroup*:

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

Creare una regola del gruppo di sicurezza di rete con [az network nsg rule create](/cli/azure/network/nsg/rule#create). esempio Hello crea una regola di gruppo di sicurezza di rete denominata *myNetworkSecurityGroupRule*:

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

Le schede di interfaccia di rete virtuale vengono create con [az network nic create](/cli/azure/network/nic#create). Hello esempio crea tre schede di rete virtuale. (Una scheda di rete virtuale per ogni macchina virtuale viene creato per l'app in hello seguendo i passaggi). È possibile creare macchine virtuali e schede di rete virtuali aggiuntive in qualsiasi momento e aggiungerli toohello servizio di bilanciamento del carico:

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupLoadBalancer \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-virtual-machines"></a>Creare macchine virtuali

### <a name="create-cloud-init-config"></a>Creare una configurazione cloud-init
Nell'esercitazione precedente su [come toocustomize una macchina virtuale Linux al primo avvio](tutorial-automate-vm-deployment.md), si è appreso tooautomate personalizzazione con cloud init. È possibile utilizzare hello stesso tooinstall file di configurazione cloud init NGINX ed eseguire una semplice app Node.js 'Hello World'.

Nella shell corrente, creare un file denominato *cloud init.txt* e Incolla hello seguente configurazione. Ad esempio, creare file hello in hello Shell Cloud non presenti nel computer locale. Immettere `sensible-editor cloud-init.txt` toocreate hello file e visualizzare un elenco degli editor disponibili. Assicurarsi che tale file intero cloud-init hello viene copiato correttamente, soprattutto hello prima riga:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-virtual-machines"></a>Creare macchine virtuali
disponibilità elevata di hello tooimprove dell'app, posizionare le macchine virtuali in un set di disponibilità. Per ulteriori informazioni sui set di disponibilità, vedere hello precedente [come macchine virtuali a disponibilità elevata toocreate](tutorial-availability-sets.md) esercitazione.

Creare un set di disponibilità con [az vm availability-set create](/cli/azure/vm/availability-set#create). esempio Hello crea un set denominato di disponibilità *myAvailabilitySet*:

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

Ora è possibile creare le macchine virtuali hello con [creare vm az](/cli/azure/vm#create). Hello esempio crea tre macchine virtuali e genera le chiavi SSH se non esiste già:

```bash
for i in `seq 1 3`; do
    az vm create \
        --resource-group myResourceGroupLoadBalancer \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --nics myNic$i \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys \
        --custom-data cloud-init.txt \
        --no-wait
done
```

Sono presenti attività in background che continuare toorun dopo hello CLI di Azure restituisce toohello prompt. Hello `--no-wait` parametro non attendere tutti hello toocomplete di attività. Potrebbe essere un altro paio di minuti prima di poter accedere app hello. Hello probe di integrità di bilanciamento del carico rileva automaticamente quando l'applicazione hello è in esecuzione in ogni macchina virtuale. Dopo l'applicazione hello è in esecuzione, regola di bilanciamento del carico hello avvia toodistribute traffico.


## <a name="test-load-balancer"></a>Testare il bilanciamento del carico
Ottenere l'indirizzo IP pubblico di hello del servizio di bilanciamento del carico con [Mostra public-ip di rete az](/cli/azure/network/public-ip#show). esempio Hello Ottiene hello di indirizzo IP per *myPublicIP* creato in precedenza:

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

È quindi possibile immettere l'indirizzo IP pubblico hello nel browser web tooa. Nota: impiegato pochi minuti hello hello macchine virtuali toobe pronto prima dell'avvio di servizio di bilanciamento del carico hello toodistribute traffico toothem. Hello app viene visualizzata, inclusi hello nome host della macchina virtuale hello tale bilanciamento del carico hello distribuite tooas traffico nel seguente esempio hello:

![Esecuzione dell'app Node.js](./media/tutorial-load-balancer/running-nodejs-app.png)

servizio di bilanciamento del carico hello toosee distribuire il traffico tra tutte le tre macchine virtuali in esecuzione l'app, è possibile forza aggiornamento web browser.


## <a name="add-and-remove-vms"></a>aggiunta e rimozione di VM
È possibile la manutenzione tooperform hello macchine virtuali in esecuzione l'app, ad esempio l'installazione di aggiornamenti del sistema operativo. toodeal con un aumento del traffico tooyour app, potrebbe essere necessario tooadd altre macchine virtuali. In questa sezione illustra come tooremove o aggiungere una macchina virtuale dal servizio di bilanciamento del carico hello.

### <a name="remove-a-vm-from-hello-load-balancer"></a>Rimuovere una macchina virtuale dal servizio di bilanciamento del carico hello
È possibile rimuovere una macchina virtuale dal pool di indirizzi back-end hello con [az nic ip-config-pool di indirizzi rete rimuovere](/cli/azure/network/nic/ip-config/address-pool#remove). Hello seguente rimuove esempio hello schede di rete virtuale per **myVM2** da *myLoadBalancer*:

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

servizio di bilanciamento del carico hello toosee distribuire il traffico tra hello altre due macchine virtuali in esecuzione l'app è possibile forza aggiornamento web browser. È ora possibile eseguire la manutenzione in hello macchina virtuale, ad esempio l'installazione degli aggiornamenti del sistema operativo o l'esecuzione di un riavvio della VM.

### <a name="add-a-vm-toohello-load-balancer"></a>Aggiungere un bilanciamento del carico VM toohello
Dopo l'esecuzione della manutenzione di macchina virtuale, o se è necessario tooexpand capacità, è possibile aggiungere un pool di indirizzi back-end VM toohello con [az rete nic ip-config-pool di indirizzi di Aggiungi](/cli/azure/network/nic/ip-config/address-pool#add). esempio Hello aggiunge hello schede di rete virtuale per **myVM2** troppo*myLoadBalancer*:

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione è creato un servizio di bilanciamento del carico e collegato tooit macchine virtuali. Si è appreso come:

> [!div class="checklist"]
> * Creare un servizio di bilanciamento del carico di Azure
> * Creare un probe di integrità per il servizio di bilanciamento del carico
> * Creare regole del traffico di bilanciamento del carico
> * Utilizzare cloud init toocreate un'app Node.js di base
> * Creare macchine virtuali e collegare bilanciamento del carico tooa
> * Visualizzare un bilanciamento del carico in azione
> * Aggiungere e rimuovere macchine virtuali da un bilanciamento del carico

Spostare toolearn esercitazione successiva toohello ulteriori dettagli sui componenti di rete virtuale di Azure.

> [!div class="nextstepaction"]
> [Gestire le VM e le reti virtuali](tutorial-virtual-network.md)
