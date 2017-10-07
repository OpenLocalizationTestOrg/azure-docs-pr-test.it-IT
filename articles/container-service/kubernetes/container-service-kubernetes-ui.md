---
title: aaaManage Kubernetes Azure cluster con interfaccia utente web | Documenti Microsoft
description: Utilizzo di hello Kubernetes web dell'interfaccia utente nel servizio contenitore di Azure
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a>Utilizzo di hello Kubernetes web dell'interfaccia utente con il servizio contenitore di Azure

## <a name="prerequisites"></a>Prerequisiti
Si presume che questa procedura dettagliata abbia [creato un cluster Kubernetes mediante il servizio contenitore di Azure](container-service-kubernetes-walkthrough.md).


Si presuppone inoltre di aver hello Azure CLI 2.0 e `kubectl` installati gli strumenti.

È possibile verificare se si dispone di hello `az` strumento installato eseguendo:

```console
$ az --version
```

Se non si dispone di hello `az` strumento installato, non esistono istruzioni [qui](https://github.com/azure/azure-cli#installation).

È possibile verificare se si dispone di hello `kubectl` strumento installato eseguendo:

```console
$ kubectl version
```

Se `kubectl` non è installato, è possibile eseguire:

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a>Panoramica

### <a name="connect-toohello-web-ui"></a>Connettere l'interfaccia utente web toohello
È possibile avviare l'interfaccia utente web di Kubernetes hello eseguendo:

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

Verrà aperto un web browser configurato tootalk tooa proxy sicuro connessione web Kubernetes toohello computer locale dell'interfaccia utente.

### <a name="create-and-expose-a-service"></a>Creare ed esporre un servizio
1. Nell'interfaccia utente web di Kubernetes hello, fare clic su **crea** pulsante nella finestra di destra superiore hello.

    ![Interfaccia utente di creazione Kubernetes](./media/container-service-kubernetes-ui/create.png)

    Viene visualizzata una finestra di dialogo in cui è possibile iniziare a creare l'applicazione.

2. Assegnargli il nome di hello `hello-nginx`. Hello utilizzare [ `nginx` contenitore da Docker](https://hub.docker.com/_/nginx/) e distribuire i tre repliche di questo servizio web.

    ![Finestra di dialogo Pod Create Kubernetes (Crea podcast Kubernetes)](./media/container-service-kubernetes-ui/nginx.png)

3. In **Service** (Servizio) selezionare **External** (Esterno) e inserire la porta 80.

    Questa impostazione di bilanciamento del carico tre repliche di traffico toohello.

    ![Finestra di dialogo Kubernetes Service Create (Crea servizio Kubernetes)](./media/container-service-kubernetes-ui/service.png)

4. Fare clic su **Distribuisci** toodeploy questi contenitori e i servizi.

    ![Distribuzione di Kubernetes](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a>Visualizzare i contenitori
Dopo aver fatto clic **Distribuisci**, hello dell'interfaccia utente mostra una visualizzazione del servizio, come la distribuzione:

![Stato di Kubernetes](./media/container-service-kubernetes-ui/status.png)

È possibile visualizzare lo stato di hello di ciascun oggetto Kubernetes cerchio hello nella parte sinistra dell'interfaccia utente, hello in **POD**. Se è un cerchio completo parzialmente, oggetto hello comunque la distribuzione. Quando un oggetto è completamente distribuito, viene visualizzato un segno di spunta verde:

![Kubernetes distribuito](./media/container-service-kubernetes-ui/deployed.png)

Una volta tutto ciò che è in esecuzione, fare clic su uno dei tuoi toosee POD su hello in esecuzione il servizio web.

![Podcast Kubernetes](./media/container-service-kubernetes-ui/pods.png)

In hello **POD** , è possibile visualizzare informazioni sui contenitori di hello pod hello, nonché le risorse di CPU e memoria hello utilizzate da tali contenitori:

![Risorse Kubernetes](./media/container-service-kubernetes-ui/resources.png)

Se le risorse di hello non viene visualizzata, potrebbe essere toowait alcuni minuti per hello toopropagate dati di monitoraggio.

toosee hello log per il contenitore, fare clic su **visualizzare log**.

![Log Kubernetes](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a>Visualizzazione del servizio
In aggiunta toorunning ai contenitori, hello Kubernetes UI ha creato un riferimento esterno `Service` che esegue il provisioning di un carico del servizio di bilanciamento toobring traffico toohello contenitori il cluster.

Nel riquadro di spostamento a sinistra di hello, fare clic su **servizi** tooview tutti i servizi (deve essere presente solo uno).

![Servizi Kubernetes](./media/container-service-kubernetes-ui/service-deployed.png)

In tale visualizzazione, verrà visualizzato un endpoint esterno (indirizzo IP) che è stato allocato il servizio tooyour.
Se si fa clic su tale indirizzo IP, si noterà il contenitore Nginx in esecuzione dietro il bilanciamento del carico.

![Visualizzazione di nginx](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a>Ridimensionamento del servizio
In aggiunta tooviewing degli oggetti in hello dell'interfaccia utente, è possibile modificare e aggiornare gli oggetti API Kubernetes hello.

In primo luogo, fare clic su **distribuzioni** in hello lasciato navigazione riquadro toosee hello la distribuzione per il servizio.

Una volta in tale visualizzazione, fare clic sul set di repliche hello e quindi fare clic su **modifica** nella barra di spostamento superiore hello:

![Modifica di Kubernetes](./media/container-service-kubernetes-ui/edit.png)

Modifica hello `spec.replicas` campo toobe `2`, fare clic su **aggiornamento**.

In questo modo il numero di hello di repliche toodrop tootwo eliminando una del POD.

 

