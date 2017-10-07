---
title: aaaQuickstart - cluster Kubernetes di Azure per Linux | Documenti Microsoft
description: Consente di capire velocemente toocreate un cluster Kubernetes per i contenitori di Linux nel servizio contenitore di Azure con hello CLI di Azure.
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 8b0d7a803148c1cbf329f4b76f2e99b4b7e14983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-linux-containers"></a>Distribuire cluster Kubernetes per contenitori Linux

In questa Guida introduttiva viene distribuito un cluster di Kubernetes utilizzando hello CLI di Azure. Un'applicazione multi-contenitore composta da front-end web e un'istanza di Redis viene quindi distribuita e in esecuzione nel cluster hello. Una volta completato, un'applicazione hello è accessibile tramite internet hello. 

applicazione di esempio Hello utilizzata in questo documento viene scritto in Python. concetti Hello e i passaggi descritti in questa sezione possono essere utilizzati toodeploy qualsiasi contenitore di immagini in un cluster Kubernetes. Hello codice, Dockerfile e progetto toothis correlati di pre-creato Kubernetes file manifesto sono disponibili sul [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).

![Immagine di esplorazione tooAzure voto](media/container-service-kubernetes-walkthrough/azure-vote.png)

Questa Guida introduttiva presuppone una conoscenza di base dei concetti Kubernetes, per informazioni dettagliate sul Kubernetes vedere hello [Kubernetes documentazione]( https://kubernetes.io/docs/home/).

Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, questa Guida rapida richiede che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando. Un gruppo di risorse di Azure è un gruppo logico in cui le risorse di Azure vengono distribuite e gestite. 

esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *westeurope* percorso.

```azurecli-interactive 
az group create --name myResourceGroup --location westeurope
```

Output:

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westeurope",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-kubernetes-cluster"></a>Creare un cluster Kubernetes

Creare un cluster di Kubernetes nel servizio contenitore di Azure con hello [az acs creare](/cli/azure/acs#create) comando. esempio Hello crea un cluster denominato *myK8sCluster* con uno Linux master nodo e i tre nodi di agente di Linux.

```azurecli-interactive 
az acs create --orchestrator-type kubernetes --resource-group myResourceGroup --name myK8sCluster --generate-ssh-keys 
```

Dopo alcuni minuti, il comando hello completa e restituisce informazioni in formato json sul cluster di hello. 

## <a name="connect-toohello-cluster"></a>Connettere il cluster toohello

Utilizzare un cluster, Kubernetes toomanage [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), client di hello Kubernetes della riga di comando. 

Se si usa Azure CloudShell, kubectl è già installato. Se si desidera tooinstall in locale, può utilizzare hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) comando.

tooconfigure kubectl tooconnect tooyour Kubernetes cluster, eseguire hello [az acs kubernetes get-credenziali](/cli/azure/acs/kubernetes#get-credentials) comando. Questo passaggio Scarica le credenziali e configura hello toouse Kubernetes CLI li.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

tooverify hello connessione tooyour cluster utilizzare hello [kubectl ottenere](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando tooreturn un elenco di nodi del cluster hello.

```azurecli-interactive
kubectl get nodes
```

Output:

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-14ad53a1-0    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-1    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-2    Ready                      10m       v1.6.6
k8s-master-14ad53a1-0   Ready,SchedulingDisabled   10m       v1.6.6
```

## <a name="run-hello-application"></a>Eseguire un'applicazione hello

Un file manifesto Kubernetes definisce uno stato desiderato per il cluster hello, incluse le immagini contenitore devono essere in esecuzione. Per questo esempio, un manifesto è toocreate utilizzati tutti gli oggetti necessari toorun hello applicazione Azure voto. 

Creare un file denominato `azure-vote.yml` copia al suo interno e hello seguenti YAML. Se si usa Azure Cloud Shell, questo file può essere creato usando vi o Nano come se si usasse un sistema virtuale o fisico.

```yaml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-back
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-back
    spec:
      containers:
      - name: azure-vote-back
        image: redis
        ports:
        - containerPort: 6379
          name: redis
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-back
spec:
  ports:
  - port: 6379
  selector:
    app: azure-vote-back
---
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-front
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-front
    spec:
      containers:
      - name: azure-vote-front
        image: microsoft/azure-vote-front:redis-v1
        ports:
        - containerPort: 80
        env:
        - name: REDIS
          value: "azure-vote-back"
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: azure-vote-front
```

Hello utilizzare [kubectl creare](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) comando applicazione hello toorun.

```azurecli-interactive
kubectl create -f azure-vote.yml
```

Output:

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-hello-application"></a>Testare l'applicazione hello

Durante l'esecuzione di un'applicazione hello, un [Kubernetes servizio](https://kubernetes.io/docs/concepts/services-networking/service/) viene creato che espone hello applicazione front-end toohello internet. Questo processo può richiedere alcuni minuti toocomplete. 

lo stato di avanzamento toomonitor, utilizzare hello [kubectl ottenere servizio](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) con hello `--watch` argomento.

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

Inizialmente hello **esterno IP** per hello *azure voto-anteriore* servizio viene visualizzato come *in sospeso*. Una volta che l'indirizzo IP esterno hello è stato modificato da *in sospeso* tooan *indirizzo IP*, utilizzare `CTRL-C` processo di controllo kubectl toostop hello. 
  
```bash
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

È ora possibile esplorare toohello esterno IP indirizzo toosee hello Azure voto App.

![Immagine di esplorazione tooAzure voto](media/container-service-kubernetes-walkthrough/azure-vote.png)  

## <a name="delete-cluster"></a>Eliminare il cluster
Quando il cluster hello non è più necessario, è possibile utilizzare hello [eliminazione gruppo az](/cli/azure/group#delete) comandi gruppo di risorse hello tooremove, il servizio contenitore e tutte le relative risorse.

```azurecli-interactive 
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a>Ottenere il codice hello

In questa Guida introduttiva, le immagini contenitore creato in precedenza sono stati utilizzati toocreate una distribuzione Kubernetes. Hello correlati Dockerfile, codice dell'applicazione e file manifesto Kubernetes sono disponibili su GitHub.

[https://github.com/Azure-Samples/azure-voting-app-redis](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a>Passaggi successivi

In questa Guida introduttiva è distribuito un cluster Kubernetes e distribuito tooit un'applicazione multi-contenitore. 

toolearn ulteriori informazioni su servizio di contenitore di Azure e procedura per un esempio di toodeployment di codice completo, continuare l'esercitazione di toohello Kubernetes cluster.

> [!div class="nextstepaction"]
> [Gestire un cluster Kubernetes ACS](./container-service-tutorial-kubernetes-prepare-app.md)
