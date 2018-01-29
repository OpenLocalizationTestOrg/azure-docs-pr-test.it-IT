---
title: Gestire un cluster Azure Kubernetes con l'interfaccia utente Web
description: Uso del dashboard Kubernetes nel servizio contenitore di Azure
services: container-service
author: neilpeterson
manager: timlt
ms.service: container-service
ms.topic: article
ms.date: 11/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ca828dab7bdb47e41596be2717598cfe828953ca
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2017
---
# <a name="kubernetes-dashboard-with-azure-container-service-aks"></a>Dashboard di Kubernetes con il servizio contenitore di Azure

Per avviare il dashboard di Kubernetes, è possibile usare l'interfaccia della riga di comando di Azure. Questo documento illustra la procedura per avviare il dashboard di Kubernetes con l'interfaccia della riga di comando di Azure, oltre ad alcune operazioni di base con il dashboard. Per ulteriori informazioni, vedere dashboard Kubernetes [Dashboard dell'interfaccia utente Web di Kubernetes][kubernetes-dashboard].

## <a name="before-you-begin"></a>Prima di iniziare

I passaggi dettagliati contenuti in questo documento presuppongono che sia stato creato un cluster del servizio contenitore di Azure e che sia stata stabilita una connessione kubectl al cluster. Se è necessario di questi elementi, vedere il [delle Guide rapide AKS][aks-quickstart].

È anche necessario che sia installata e configurata l'interfaccia della riga di comando di Azure versione 2.0.21 o successiva. Eseguire az --version per trovare la versione. Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure][install-azure-cli].

## <a name="start-kubernetes-dashboard"></a>Avviare il dashboard di Kubernetes

Usare il comando `az aks browse` per avviare il dashboard di Kubernetes. Quando si esegue questo comando, sostituire il nome del gruppo di risorse e del cluster.

```azurecli
az aks browse --resource-group myResourceGroup --name myK8SCluster
```

Questo comando crea un proxy tra il sistema di sviluppo e l'API Kubernetes e apre il dashboard di Kubernetes in un Web browser.

## <a name="run-an-application"></a>Eseguire un'applicazione

Nel dashboard di Kubernetes fare clic sul pulsante **Create** (Crea) nella finestra in alto a destra. Assegnare il nome `nginx` alla distribuzione e immettere `nginx:latest` per il nome delle immagini. In **Service** (Servizio) selezionare **External** (External) e immettere `80` sia per la porta che per la porta di destinazione.

Quando si è pronti, fare clic su **Deploy** (Distribuisci) per creare la distribuzione.

![Finestra di dialogo Kubernetes Service Create (Crea servizio Kubernetes)](./media/container-service-kubernetes-ui/create-deployment.png)

## <a name="view-the-application"></a>Visualizzare l'applicazione

Lo stato dell'applicazione può essere visualizzato nel dashboard di Kubernetes. Quando l'applicazione è in esecuzione, accanto a ogni componente compare una casella di controllo verde.

![Podcast Kubernetes](./media/container-service-kubernetes-ui/complete-deployment.png)

Per altre informazioni sui pod delle applicazioni, fare clic su **Pods** (Pod) nel menu a sinistra e quindi selezionare il pod **NGINX**. Qui è possibile visualizzare informazioni specifiche del pod, come il consumo di risorse.

![Risorse Kubernetes](./media/container-service-kubernetes-ui/running-pods.png)

Per trovare l'indirizzo IP dell'applicazione, fare clic su **Services** (Servizi) nel menu a sinistra e quindi selezionare il servizio **NGINX**.

![Visualizzazione di nginx](./media/container-service-kubernetes-ui/nginx-service.png)

## <a name="edit-the-application"></a>Modificare l'applicazione

Oltre che per la creazione e la visualizzazione di applicazioni, è possibile usare il dashboard di Kubernetes per modificare e aggiornare le distribuzioni delle applicazioni.

Per modificare una distribuzione, fare clic su **Deployments** (Distribuzioni) nel menu a sinistra e quindi selezionare la distribuzione **NGINX**. Infine, selezionare **Modifica** nella barra di spostamento in alto a destra.

![Modifica di Kubernetes](./media/container-service-kubernetes-ui/view-deployment.png)

Individuare il valore `spec.replica`, che dovrebbe essere 1, e modificarlo in 3. In questo modo, il conteggio di repliche della distribuzione NGINX viene aumentato da 1 a 3.

Selezionare **Update** (Aggiorna) al termine.

![Modifica di Kubernetes](./media/container-service-kubernetes-ui/edit-deployment.png)

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sul dashboard di Kubernetes, vedere la documentazione di Kubernetes.

> [!div class="nextstepaction"]
> [Dashboard dell'interfaccia utente Web Kubernetes][kubernetes-dashboard]

<!-- LINKS - external -->
[kubernetes-dashboard]: https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/

<!-- LINKS - internal -->
[aks-quickstart]: ./kubernetes-walkthrough.md
[install-azure-cli]: /cli/azure/install-azure-cli