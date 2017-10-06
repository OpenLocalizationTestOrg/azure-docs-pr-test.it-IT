---
title: aaaLoad bilanciare Kubernetes contenitori in Azure | Documenti Microsoft
description: "Connettersi esternamente e bilanciare il carico tra più contenitori in un cluster Kubernetes nel servizio contenitore di Azure."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenitori, microservizi, Kubernetes, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 8073c8d3a015a53a532c326749571cb2582e1bac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a>Bilanciare il carico dei contenitori in un cluster Kubernetes nel servizio contenitore di Azure 
In questo articolo viene presentato come bilanciare il carico in un cluster Kubernetes nel servizio contenitore di Azure. Bilanciamento del carico fornisce un indirizzo IP accessibile dall'esterno per il servizio di hello e distribuisce il traffico di rete tra POD hello in esecuzione nell'agente di macchine virtuali.

È possibile impostare un toouse servizio Kubernetes [bilanciamento del carico di Azure](../../load-balancer/load-balancer-overview.md) toomanage il traffico di rete (TCP) esterni. Con una configurazione aggiuntiva, è possibile eseguire il bilanciamento del carico e il routing del traffico HTTP o HTTPS o anche scenari più avanzati.

## <a name="prerequisites"></a>Prerequisiti
* [Distribuire un cluster Kubernetes](container-service-kubernetes-walkthrough.md) nel servizio contenitore di Azure
* [Connettere il proprio client](../container-service-connect.md) tooyour cluster

## <a name="azure-load-balancer"></a>Servizio di bilanciamento del carico di Azure

Per impostazione predefinita, un cluster Kubernetes distribuito nel servizio contenitore di Azure include un bilanciamento del carico di Azure con connessione Internet per agente hello macchine virtuali. (Una risorsa di bilanciamento del carico separata è configurata per master hello macchine virtuali). Il servizio di bilanciamento del carico di Azure è di livello 4. Servizio di bilanciamento del carico hello attualmente supporta solo il traffico TCP in Kubernetes.

Quando si crea un servizio Kubernetes, è possibile configurare automaticamente hello Azure tooallow accesso toohello servizio. bilanciamento del carico di tooconfigure hello, servizio hello set `type` troppo`LoadBalancer`. servizio di bilanciamento del carico Hello crea una regola toomap un indirizzo IP pubblico e il numero di porta di ingresso del servizio traffico toohello indirizzi IP privati e i numeri di porta di POD hello nell'agente di macchine virtuali (e viceversa per il traffico di risposta). 

 Di seguito sono riportati due esempi che mostra come tooset hello servizio Kubernetes `type` troppo`LoadBalancer`. (Dopo esempi hello durante il tentativo, eliminare le distribuzioni di hello se non è più necessario).

### <a name="example-use-hello-kubectl-expose-command"></a>Esempio: Hello utilizzo `kubectl expose` comando 
Hello [procedura dettagliata Kubernetes](container-service-kubernetes-walkthrough.md) include un esempio di come un servizio con hello tooexpose `kubectl expose` comando e il relativo `--type=LoadBalancer` flag. Ecco i passaggi di hello:

1. Avviare una nuova distribuzione di contenitori. Ad esempio, hello seguente comando avvia una nuova distribuzione chiamata `mynginx`. distribuzione di Hello è costituita da tre contenitori basati su hello Docker immagine per il server web Nginx hello.

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. Verificare che i contenitori di hello siano in esecuzione. Ad esempio, se si esegue una query per i contenitori di hello con `kubectl get pods`, viene visualizzato il seguente toohello simili di output:

    ![Avviare i contenitori Nginx](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. tooconfigure hello carico bilanciamento tooaccept traffico esterno toohello distribuzione, eseguire `kubectl expose` con `--type=LoadBalancer`. Hello comando espone server Nginx hello sulla porta 80:

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. Tipo `kubectl get svc` stato hello toosee dei servizi cluster hello hello. Mentre il servizio di bilanciamento del carico hello Configura regola hello, hello `EXTERNAL-IP` di hello servizio viene visualizzato come `<pending>`. Dopo alcuni minuti, è configurato un indirizzo IP esterno hello: 

    ![Configurare il servizio di bilanciamento del carico di Azure](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. Verificare che sia possibile accedere servizio hello all'indirizzo IP esterno hello. Ad esempio, aprire un web browser toohello IP mostrato. browser Hello Mostra i server web Nginx di hello in esecuzione in uno dei contenitori di hello. In alternativa, eseguire hello `curl` o `wget` comando. ad esempio:

    ```
    curl 13.82.93.130
    ```

    Verrà visualizzato un output simile al seguente:

    ![Accesso a Nginx con il comando curl](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. configurazione di hello toosee di bilanciamento del carico di Azure di hello, andare toohello [portale di Azure](https://portal.azure.com).

7. Cerca il gruppo di risorse hello per il cluster del servizio contenitore e selezionare bilanciamento del carico di hello per agente hello macchine virtuali. Il nome deve essere hello uguale a servizio di contenitore hello. (Non scegliere servizio di bilanciamento del carico hello per nodi master hello, hello uno cui nome include **master lb**.) 

    ![Servizio di bilanciamento del carico nel gruppo di risorse](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. Fare clic su Dettagli hello toosee di configurazione di bilanciamento del carico hello, **regole di bilanciamento del carico** e hello il nome della regola hello che è stato configurato.

    ![Regole del servizio di bilanciamento del carico](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-hello-service-configuration-file"></a>Esempio: Specificare `type: LoadBalancer` nel file di configurazione del servizio hello

Se si distribuisce un'applicazione contenitore Kubernetes da un YAML o JSON [file di configurazione del servizio](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), specificare un bilanciamento del carico esterno aggiungendo hello specifica del servizio toohello riga seguente:

```YAML
 "type": "LoadBalancer"
``` 



i passaggi seguenti Hello usano hello Kubernetes [visitatori esempio](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook). Questo esempio è un'app Web multi-livello basata su immagini Redis e PHP Docker. È possibile specificare nel file di configurazione del servizio hello che server front-end PHP hello Usa servizio di bilanciamento del carico di Azure hello.

1. Scaricare il file hello `guestbook-all-in-one.yaml` da [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one). 
2. Cerca hello `spec` per hello `frontend` servizio.
3. Rimuovere il commento riga hello `type: LoadBalancer`.

    ![Servizio di bilanciamento durante la configurazione del servizio](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. Salvare il file hello e distribuire l'applicazione hello eseguendo hello comando seguente:

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. Tipo `kubectl get svc` stato hello toosee dei servizi cluster hello hello. Mentre il servizio di bilanciamento del carico hello Configura regola hello, hello `EXTERNAL-IP` di hello `frontend` servizio viene visualizzato come `<pending>`. Dopo alcuni minuti, è configurato un indirizzo IP esterno hello: 

    ![Configurare il servizio di bilanciamento del carico di Azure](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. Verificare che sia possibile accedere servizio hello all'indirizzo IP esterno hello. Ad esempio, è possibile aprire un web browser toohello indirizzo IP esterno del servizio hello.

    ![Accedere al guestbook dall'esterno](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    È possibile aggiungere voci del guestbook.

7. configurazione di hello toosee di bilanciamento del carico di Azure di hello, cercare per la risorsa del servizio di bilanciamento carico di hello cluster hello in hello [portale di Azure](https://portal.azure.com). Vedere i passaggi nell'esempio precedente hello hello.

### <a name="considerations"></a>Considerazioni

* Creazione di una regola di bilanciamento del carico hello viene eseguito in modo asincrono e informazioni su Bilanciamento hello il provisioning viene pubblicate nel servizio di hello `status.loadBalancer` campo.
* Ogni servizio viene assegnato automaticamente il proprio indirizzo IP virtuale nel bilanciamento del carico hello.
* Se si desidera bilanciamento del carico di hello tooreach da un nome DNS, lavorare con toocreate di provider del servizio del dominio un nome DNS per l'indirizzo IP della regola hello.

## <a name="http-or-https-traffic"></a>Traffico HTTP o HTTPS

Saldo tooload HTTP o HTTPS traffico toocontainer web App e gestire i certificati di sicurezza di livello di trasporto (TLS), è possibile usare hello Kubernetes [in ingresso](https://kubernetes.io/docs/user-guide/ingress/) risorse. Un in ingresso è una raccolta di regole che consentono le connessioni in ingresso ai servizi di cluster di tooreach hello. Per un toowork di risorse in ingresso, hello Kubernetes cluster deve disporre di un [controller in ingresso](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) in esecuzione.

Il servizio contenitore di Azure non implementa automaticamente un controller di Ingress di Kubernetes. Sono disponibili diverse implementazioni di controller. Attualmente, hello [controller in ingresso Nginx](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) è consigliabile regole in entrata tooconfigure e bilanciamento del carico del traffico HTTP e HTTPS. 

Per ulteriori informazioni, vedere hello [documentazione relativa al controller in ingresso Nginx](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).

> [!IMPORTANT]
> Quando si utilizza hello controller Nginx ingresso nel servizio contenitore di Azure, è necessario esporre la distribuzione di controller hello come un servizio con `type: LoadBalancer`. Consente di configurare hello Azure bilanciamento tooroute traffico toohello controller del carico. Per ulteriori informazioni, vedere la sezione precedente di hello.


## <a name="next-steps"></a>Passaggi successivi

* Vedere hello [Kubernetes LoadBalancer documentazione](https://kubernetes.io/docs/user-guide/load-balancer/)
* Altre informazioni su [Ingress di Kubernetes e controller di Ingress](https://kubernetes.io/docs/user-guide/ingress/)
* Vedere [esempi di Kubernetes](https://github.com/kubernetes/kubernetes/tree/master/examples)

