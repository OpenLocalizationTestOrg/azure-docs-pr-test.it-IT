---
title: "un set di scalabilità di macchine virtuali Linux in Azure aaaCreate | Documenti Microsoft"
description: "Creare e distribuire un'applicazione a disponibilità elevata in macchine virtuali Linux usando un set di scalabilità di macchine virtuali"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.openlocfilehash: 00dd81043f9be46ef2dc6dfe97eefdb20944ee13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a>Creare un set di scalabilità di macchine virtuali e distribuire un'app a disponibilità elevata in Linux
Un set di scalabilità della macchina virtuale consente toodeploy e gestire un set di macchine virtuali identiche e la scalabilità automatica. È possibile ridimensionare manualmente numero hello di macchine virtuali nel set di scalabilità hello o definire tooautoscale regole in base all'utilizzo della CPU, la richiesta di memoria o il traffico di rete. In questa esercitazione viene distribuito un set di scalabilità di macchine virtuali in Azure. Si apprenderà come:

> [!div class="checklist"]
> * Utilizzare cloud init toocreate tooscale un'app
> * Creare un set di scalabilità di macchine virtuali
> * Aumentare o diminuire il numero di hello di istanze in un set di scalabilità
> * Visualizzare le informazioni di connessione per le istanze del set di scalabilità
> * Usare dischi di dati in un set di scalabilità


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="scale-set-overview"></a>Informazioni generali sui set di scalabilità
Un set di scalabilità della macchina virtuale consente toodeploy e gestire un set di macchine virtuali identiche e la scalabilità automatica. Scala imposta utilizzare hello stessi componenti come sono state descritte nell'esercitazione precedente hello troppo[creare macchine virtuali a disponibilità elevata](tutorial-availability-sets.md). Le macchine virtuali di un set di scalabilità vengono create in un set di disponibilità e distribuite in domini logici di errore e di aggiornamento.

Le macchine virtuali vengono create in base alle esigenze in un set di scalabilità. Definire toocontrol le regole di scalabilità automatica come e quando le macchine virtuali vengono aggiunti o rimossi dal set di scalabilità hello. Queste regole possono essere attivate in base a determinate metriche, ad esempio il carico della CPU, l'utilizzo della memoria o il traffico di rete.

Scala imposta supporto backup too1, 000 macchine virtuali quando si utilizza un'immagine della piattaforma Azure. Per i carichi di lavoro, è preferibile troppo[creare un'immagine di macchina virtuale personalizzata](tutorial-custom-images.md). È possibile creare le macchine virtuali too100 in una scala impostata quando si utilizza un'immagine personalizzata.


## <a name="create-an-app-tooscale"></a>Creare un'app tooscale
Per la produzione, è preferibile troppo[creare un'immagine di macchina virtuale personalizzata](tutorial-custom-images.md) che include l'applicazione installata e configurata. Per questa esercitazione consente di personalizzare le macchine virtuali di primo avvio tooquickly vedere una scala in azione hello.

In un'esercitazione precedente, si è appreso [come una macchina virtuale Linux al primo avvio toocustomize](tutorial-automate-vm-deployment.md) con cloud init. È possibile utilizzare hello stesso tooinstall file di configurazione cloud init NGINX ed eseguire una semplice app Node.js 'Hello World'. 

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


## <a name="create-a-scale-set"></a>Creare un set di scalabilità
Per poter creare un set di scalabilità, è prima necessario creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create). esempio Hello crea un gruppo di risorse denominato *myResourceGroupScaleSet* in hello *eastus* percorso:

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

Si può ora creare un set di scalabilità di macchine virtuali con il comando [az vmss create](/cli/azure/vmss#create). esempio Hello crea un set denominato di scalabilità *myScaleSet*, utilizza hello toocustomize di file cloud init hello VM e genera le chiavi SSH se non sono presenti:

```azurecli-interactive 
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

Accetta toocreate di pochi minuti e configurare tutti i set di hello scalabilità delle risorse e le macchine virtuali. Sono presenti attività in background che continuare toorun dopo hello CLI di Azure restituisce toohello prompt. Potrebbe essere un altro paio di minuti prima di poter accedere app hello.


## <a name="allow-web-traffic"></a>Consentire il traffico Web
Un servizio di bilanciamento del carico è stato creato automaticamente come parte del set di scalabilità della macchina virtuale hello. servizio di bilanciamento del carico Hello distribuisce il traffico tra un set di macchine virtuali definite utilizzando regole di bilanciamento del carico. Maggiori informazioni su concetti del servizio di bilanciamento carico e la configurazione nella prossima esercitazione hello, [come tooload bilanciare le macchine virtuali in Azure](tutorial-load-balancer.md).

tooallow traffico tooreach hello web app, creare una regola con [creare una regola lb rete az](/cli/azure/network/lb/rule#create). esempio Hello crea una regola denominata *myLoadBalancerRuleWeb*:

```azurecli-interactive 
az network lb rule create \
  --resource-group myResourceGroupScaleSet \
  --name myLoadBalancerRuleWeb \
  --lb-name myScaleSetLB \
  --backend-pool-name myScaleSetLBBEPool \
  --backend-port 80 \
  --frontend-ip-name loadBalancerFrontEnd \
  --frontend-port 80 \
  --protocol tcp
```

## <a name="test-your-app"></a>Test dell'app
toosee l'app di Node.js nel web hello, ottenere l'indirizzo IP pubblico di hello del servizio di bilanciamento del carico con [Mostra public-ip di rete az](/cli/azure/network/public-ip#show). esempio Hello Ottiene hello di indirizzo IP per *myScaleSetLBPublicIP* creati come parte del set di scalabilità hello:

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

Immettere l'indirizzo IP pubblico hello nel browser web tooa. viene visualizzata, Hello app, inclusi hostname hello di hello VM che hello il carico del traffico di bilanciamento del carico distribuito per:

![Esecuzione dell'app Node.js](./media/tutorial-create-vmss/running-nodejs-app.png)

toosee set nell'azione di scalabilità hello, è possibile forza l'aggiornamento del carico di web browser toosee hello distribuire il servizio di bilanciamento del traffico tra tutte le macchine virtuali hello esegue l'app.


## <a name="management-tasks"></a>Attività di gestione
Nel ciclo di vita hello del set di scalabilità di hello, potrebbe essere necessario toorun uno o più attività di gestione. Inoltre, è consigliabile toocreate script che automatizzano le varie attività di ciclo di vita. Hello Azure CLI 2.0 fornisce toodo un modo rapido alle attività. Di seguito vengono illustrate alcune attività comuni.

### <a name="view-vms-in-a-scale-set"></a>Visualizzare le macchine virtuali in un set di scalabilità
imposta un elenco di macchine virtuali in esecuzione nella scala tooview, utilizzare [istanze di elenco di az vmss](/cli/azure/vmss#list-instances) come indicato di seguito:

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

Hello l'output è simile toohello seguente esempio:

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a>Aumentare o diminuire le istanze delle macchine virtuali
numero di hello toosee di istanze attualmente in una scala impostate, utilizzare [Mostra vmss az](/cli/azure/vmss#show) ed eseguire query su *sku.capacity*:

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

È possibile quindi manualmente aumentare o diminuire il numero di hello di macchine virtuali in hello set di scalabilità con [scala vmss az](/cli/azure/vmss#scale). Hello che segue viene impostato il numero di hello di macchine virtuali la scala impostata troppo*5*:

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

Le regole di scalabilità automatica consentono di definire come tooscale verso l'alto o verso il basso numero hello di macchine virtuali nella scala è impostata nella risposta toodemand, ad esempio il traffico di rete o l'utilizzo della CPU. Non è attualmente possibile impostare queste regole nell'interfaccia della riga di comando di Azure 2.0. Hello utilizzare [portale di Azure](https://portal.azure.com) scalabilità automatica tooconfigure.

### <a name="get-connection-info"></a>Ottenere informazioni sulla connessione
informazioni di connessione tooobtain circa hello macchine virtuali nel set di scalabilità, utilizzare [az vmss elenco--connessione-informazioni sull'istanza](/cli/azure/vmss#list-instance-connection-info). Questo comando restituisce l'indirizzo IP pubblico hello e la porta per ogni macchina virtuale che consente di tooconnect con SSH:

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a>Usare dischi di dati con set di scalabilità
È possibile creare e usare dischi di dati con set di scalabilità. In un'esercitazione precedente, si è appreso come troppo[dischi gestire Azure](tutorial-manage-disks.md) che strutture hello procedure consigliate e i miglioramenti delle prestazioni per la compilazione di applicazioni nei dischi dati, anziché disco hello del sistema operativo.

### <a name="create-scale-set-with-data-disks"></a>Creare un set di scalabilità con dischi di dati
toocreate scala impostata e collegare dischi dati, aggiungere hello `--data-disk-sizes-gb` parametro toohello [vmss az creare](/cli/azure/vmss#create) comando. esempio Hello crea un set di scalabilità con *50*Gb i dischi dati collegati tooeach istanza:

```azurecli-interactive 
az vmss create \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetDisks \
    --image UbuntuLTS \
    --upgrade-policy-mode automatic \
    --custom-data cloud-init.txt \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50
```

Quando le istanze vengono rimosse da un set di scalabilità, vengono rimossi anche tutti i dischi di dati collegati.

### <a name="add-data-disks"></a>Aggiungere dischi di dati
impostare un tooinstances disco dati la scala tooadd, utilizzare [collega disco vmss az](/cli/azure/vmss/disk#attach). Hello seguente viene aggiunto un *50*istanza tooeach del disco Gb:

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a>Scollegare dischi di dati
impostare un tooinstances disco dati la scala tooremove, utilizzare [Scollega disco vmss az](/cli/azure/vmss/disk#detach). esempio Hello rimuove il disco dati hello nel LUN *2* da ogni istanza di:

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione è stato creato un set di scalabilità di macchine virtuali. Si è appreso come:

> [!div class="checklist"]
> * Utilizzare cloud init toocreate tooscale un'app
> * Creare un set di scalabilità di macchine virtuali
> * Aumentare o diminuire il numero di hello di istanze in un set di scalabilità
> * Visualizzare le informazioni di connessione per le istanze del set di scalabilità
> * Usare dischi di dati in un set di scalabilità

Spostare toolearn esercitazione successiva toohello ulteriori informazioni su concetti per le macchine virtuali di bilanciamento del carico.

> [!div class="nextstepaction"]
> [Bilanciare il carico di macchine virtuali](tutorial-load-balancer.md)