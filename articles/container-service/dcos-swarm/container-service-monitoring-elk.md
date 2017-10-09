---
title: un cluster di controller di dominio o sistema operativo di Azure - stack ELK aaaMonitor | Documenti Microsoft
description: Monitorare un cluster DC/OS nel cluster del servizio contenitore di Azure con ELK (Elasticsearch, Logstash e Kibana).
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: Contenitori, DC/OS, Azure, monitoraggio, ELK
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 8d81c5342616ec14880d38803cdf95f5845a669b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a>Monitorare un cluster del servizio contenitore di Azure con ELK
In questo articolo viene illustrato come stack di chiamate toodeploy hello ELK (Elasticsearch, Logstash, Kibana) su un cluster di controller di dominio o del sistema operativo contenitore nel servizio di Azure. 

## <a name="prerequisites"></a>Prerequisiti
[Distribuire](container-service-deployment.md) e [connettere](../container-service-connect.md) un cluster DC/OS configurato dal servizio contenitore di Azure. Esplorare il dashboard di controller di dominio/OS hello e servizi maratona [qui](container-service-mesos-marathon-ui.md). Installare anche hello [bilanciamento del carico maratona](container-service-load-balancing.md).


## <a name="elk-elasticsearch-logstash-kibana"></a>ELK (Elasticsearch, Logstash, Kibana)
Stack ELK è una combinazione di Elasticsearch, Logstash, Kibana che fornisce uno stack tooend end che può essere utilizzati toomonitor e analizzare i log del cluster.

## <a name="configure-hello-elk-stack-on-a-dcos-cluster"></a>Configurare stack ELK hello in un cluster di controller di dominio o del sistema operativo
Accedere all'interfaccia del controller di dominio o del sistema operativo tramite [http://localhost:80 /](http://localhost:80/) una volta nell'interfaccia utente di controller di dominio/OS passare troppo hello**universo**. Cercare e installare Elasticsearch Logstash e Kibana da hello l'universo dei controller di dominio o del sistema operativo e in tale ordine specifico. Ulteriori informazioni sulla configurazione se si passa toohello **installazione avanzata** collegamento.

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

Una volta hello contenitori ELK e vengono aggiornato e in esecuzione, è necessario tooenable Kibana toobe tramite maratona LB. Passare troppo **servizi** > **kibana**, fare clic su **modifica** come illustrato di seguito.

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


Attivare o disattivare troppo**modalità JSON** e scorrere verso il basso sezione etichette toohello.
È necessario tooadd un `"HAPROXY_GROUP": "external"` voce qui come mostrato di seguito.
Dopo avere fatto clic su **Distribuisci modifiche**, il contenitore viene riavviato.

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


Se si desidera tooverify che Kibana viene registrato come un servizio nel dashboard HAPROXY hello, è necessario che sia tooopen porta 9090 nel cluster agente hello HAPROXY eseguita sulla porta 9090.
Per impostazione predefinita, si apre le porte 80, 8080 e 443 in hello cluster agente controller di dominio o del sistema operativo.
Istruzioni tooopen una porta e fornire pubblico valutare forniti [qui](container-service-enable-public-access.md).

tooaccess hello dashboard dell'interfaccia di amministrazione aprire hello maratona LB in HAPROXY: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.
Quando ci si sposta toohello URL, dashboard HAPROXY hello verrà visualizzato come illustrato di seguito, viene visualizzata una voce di servizio per Kibana.

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


tooaccess hello Kibana dashboard in cui viene distribuito sulla porta 5601, è necessario tooopen porta 5601. Seguire le istruzioni [qui](container-service-enable-public-access.md). Quindi aprire il dashboard Kibana hello in: `http://localhost:5601`.

## <a name="next-steps"></a>Passaggi successivi

* Per l'inoltro e la configurazione del log di sistema e dell'applicazione, vedere [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/) (Gestione log nel controller di dominio o sistema operativo con ELK).

* vedere i log toofilter, [registri dei filtri con ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/). 

 

