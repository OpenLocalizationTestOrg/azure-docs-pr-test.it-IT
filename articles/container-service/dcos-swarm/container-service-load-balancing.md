---
title: contenitori di saldo aaaLoad nel cluster di controller di dominio o sistema operativo di Azure | Documenti Microsoft
description: "Bilanciare il carico tra più contenitori in un cluster DC/OS del servizio contenitore di Azure."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenitori, Micro-Service, controller di dominio/sistema operativo, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 2249cb06880cdb7e9a3aa94c0750c6a27316d349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a>Bilanciare il carico dei contenitori in un cluster DC/OS del servizio contenitore di Azure
In questo articolo esamineremo come il servizio di contenitore di Azure utilizzando maratona LB gestito toocreate un bilanciamento del carico interno in un controller di dominio o sistema operativo. Questa configurazione consente di tooscale le applicazioni in senso orizzontale. Consente inoltre tootake sfruttare cluster agente pubbliche e private hello inserendo i servizi di bilanciamento del carico sul cluster pubblica hello e i contenitori di applicazioni in cluster privata hello. In questa esercitazione:

> [!div class="checklist"]
> * Configurare un servizio di bilanciamento del carico Marathon
> * Distribuire un'applicazione con bilanciamento del carico hello
> * Configurare Azure Load Balancer

È necessario un ACS controller di dominio o sistema operativo hello toocomplete cluster i passaggi in questa esercitazione. Se necessario, questo [script di esempio](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) può crearne uno appositamente.

Questa esercitazione richiede hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooupgrade, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a>Panoramica del bilanciamento del carico

In un cluster DC/OS del servizio contenitore di Azure esistono due livelli di bilanciamento del carico: 

**Il bilanciamento del carico Azure** fornisce punti di ingresso pubblico (quelli che gli utenti finali accesso Buongiorno). Un LB Azure viene fornito automaticamente dal servizio di contenitore di Azure ed è, per impostazione predefinita, tooexpose configurata la porta 80, 443 e 8080.

**servizio di bilanciamento del carico maratona (maratona lb) Hello** route in ingresso istanze toocontainer le richieste che queste richieste. Come si scala contenitori hello che fornisce il servizio web, si adatta dinamicamente hello maratona kg. Impostazione predefinita nel servizio contenitore non è disponibile il bilanciamento del carico, ma è facile tooinstall.

## <a name="configure-marathon-load-balancer"></a>Configurare il servizio di bilanciamento del carico Marathon

Servizio di bilanciamento del carico maratona dinamicamente riconfigura basato sui contenitori di hello che sono stati distribuiti. È inoltre toohello resilienti perdita di un contenitore o un agente - se questo errore si verifica, Mesos Apache riavvia altrove contenitore hello e maratona lb adatta.

Eseguire hello successivo comando tooinstall hello maratona bilanciamento del carico nel cluster dell'agente di hello pubblico.

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a>Distribuire un'applicazione con bilanciamento del carico

Ora che abbiamo pacchetto maratona lb hello, è possibile distribuire un contenitore di applicazione che si desidera bilanciare tooload. 

Innanzitutto, ottenere hello FQDN di agenti hello esposto pubblicamente.

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

Successivamente, creare un file denominato *hello web.json* e copia in hello seguendo contenuto. Hello `HAPROXY_0_VHOST` etichetta deve toobe aggiornato con FQDN di agenti di controller di dominio/OS hello hello. 

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}
```

Utilizzare un'applicazione hello toorun hello CLI di controller di dominio o del sistema operativo. Per impostazione predefinita maratona distribuisce hello hello applicazione toohello privata del cluster. Ciò significa che hello di sopra di distribuzione è accessibile solo tramite il servizio di bilanciamento del carico, che corrisponde in genere il comportamento di hello desiderato.

```azurecli-interactive
dcos marathon app add hello-web.json
```

Dopo la distribuzione di un'applicazione hello, esplorare toohello FQDN di un'applicazione hello agente cluster tooview con carico bilanciato.

![Immagine dell'applicazione con bilanciamento del carico](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a>Configurare Azure Load Balancer

Per impostazione predefinita, Azure Load Balancer espone le porte 80, 8080 e 443. Se si utilizza uno di questi tre porte (come in hello esempio precedente), quindi non c'è niente che occorre toodo. Dovrebbe essere in grado di toohit FQDN del servizio di bilanciamento di carico dell'agente e ogni volta che si aggiorna, si verificherà uno dei server web di tre in uno schema round-robin. 

Se si utilizza una porta diversa, è necessario un round-robin tooadd regola e un probe di bilanciamento del carico hello per porta hello usata. È possibile farlo da hello [CLI di Azure](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), con i comandi di hello `azure network lb rule create` e `azure network lb probe create`.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, illustrando il bilanciamento del carico in ACS con hello maratona e carico di Azure tra cui bilanciamento hello seguenti azioni:

> [!div class="checklist"]
> * Configurare un servizio di bilanciamento del carico Marathon
> * Distribuire un'applicazione con bilanciamento del carico hello
> * Configurare Azure Load Balancer

Spostare toohello Avanti toolearn esercitazione sull'integrazione di archiviazione di Azure con controller di dominio o del sistema operativo in Azure.

> [!div class="nextstepaction"]
> [Montare una condivisione file di Azure nel cluster DC/OS](container-service-dcos-fileshare.md)