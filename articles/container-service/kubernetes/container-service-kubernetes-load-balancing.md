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
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="4abdc-104">Bilanciare il carico dei contenitori in un cluster Kubernetes nel servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="4abdc-104">Load balance containers in a Kubernetes cluster in Azure Container Service</span></span> 
<span data-ttu-id="4abdc-105">In questo articolo viene presentato come bilanciare il carico in un cluster Kubernetes nel servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="4abdc-105">This article introduces load balancing in a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="4abdc-106">Bilanciamento del carico fornisce un indirizzo IP accessibile dall'esterno per il servizio di hello e distribuisce il traffico di rete tra POD hello in esecuzione nell'agente di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4abdc-106">Load balancing provides an externally accessible IP address for hello service and distributes network traffic among hello pods running in agent VMs.</span></span>

<span data-ttu-id="4abdc-107">È possibile impostare un toouse servizio Kubernetes [bilanciamento del carico di Azure](../../load-balancer/load-balancer-overview.md) toomanage il traffico di rete (TCP) esterni.</span><span class="sxs-lookup"><span data-stu-id="4abdc-107">You can set up a Kubernetes service toouse [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) toomanage external network (TCP) traffic.</span></span> <span data-ttu-id="4abdc-108">Con una configurazione aggiuntiva, è possibile eseguire il bilanciamento del carico e il routing del traffico HTTP o HTTPS o anche scenari più avanzati.</span><span class="sxs-lookup"><span data-stu-id="4abdc-108">With additional configuration, load balancing and routing of HTTP or HTTPS traffic or more advanced scenarios are possible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4abdc-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4abdc-109">Prerequisites</span></span>
* <span data-ttu-id="4abdc-110">[Distribuire un cluster Kubernetes](container-service-kubernetes-walkthrough.md) nel servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="4abdc-110">[Deploy a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>
* <span data-ttu-id="4abdc-111">[Connettere il proprio client](../container-service-connect.md) tooyour cluster</span><span class="sxs-lookup"><span data-stu-id="4abdc-111">[Connect your client](../container-service-connect.md) tooyour cluster</span></span>

## <a name="azure-load-balancer"></a><span data-ttu-id="4abdc-112">Servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="4abdc-112">Azure load balancer</span></span>

<span data-ttu-id="4abdc-113">Per impostazione predefinita, un cluster Kubernetes distribuito nel servizio contenitore di Azure include un bilanciamento del carico di Azure con connessione Internet per agente hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4abdc-113">By default, a Kubernetes cluster deployed in Azure Container Service includes an Internet-facing Azure load balancer for hello agent VMs.</span></span> <span data-ttu-id="4abdc-114">(Una risorsa di bilanciamento del carico separata è configurata per master hello macchine virtuali). Il servizio di bilanciamento del carico di Azure è di livello 4.</span><span class="sxs-lookup"><span data-stu-id="4abdc-114">(A separate load balancer resource is configured for hello master VMs.) Azure load balancer is a Layer 4 load balancer.</span></span> <span data-ttu-id="4abdc-115">Servizio di bilanciamento del carico hello attualmente supporta solo il traffico TCP in Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="4abdc-115">Currently, hello load balancer only supports TCP traffic in Kubernetes.</span></span>

<span data-ttu-id="4abdc-116">Quando si crea un servizio Kubernetes, è possibile configurare automaticamente hello Azure tooallow accesso toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="4abdc-116">When creating a Kubernetes service, you can automatically configure hello Azure load balancer tooallow access toohello service.</span></span> <span data-ttu-id="4abdc-117">bilanciamento del carico di tooconfigure hello, servizio hello set `type` troppo`LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="4abdc-117">tooconfigure hello load balancer, set hello service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="4abdc-118">servizio di bilanciamento del carico Hello crea una regola toomap un indirizzo IP pubblico e il numero di porta di ingresso del servizio traffico toohello indirizzi IP privati e i numeri di porta di POD hello nell'agente di macchine virtuali (e viceversa per il traffico di risposta).</span><span class="sxs-lookup"><span data-stu-id="4abdc-118">hello load balancer creates a rule toomap a public IP address and port number of incoming service traffic toohello private IP addresses and port numbers of hello pods in agent VMs (and vice versa for response traffic).</span></span> 

 <span data-ttu-id="4abdc-119">Di seguito sono riportati due esempi che mostra come tooset hello servizio Kubernetes `type` troppo`LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="4abdc-119">Following are two examples showing how tooset hello Kubernetes service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="4abdc-120">(Dopo esempi hello durante il tentativo, eliminare le distribuzioni di hello se non è più necessario).</span><span class="sxs-lookup"><span data-stu-id="4abdc-120">(After trying hello examples, delete hello deployments if you no longer need them.)</span></span>

### <a name="example-use-hello-kubectl-expose-command"></a><span data-ttu-id="4abdc-121">Esempio: Hello utilizzo `kubectl expose` comando</span><span class="sxs-lookup"><span data-stu-id="4abdc-121">Example: Use hello `kubectl expose` command</span></span> 
<span data-ttu-id="4abdc-122">Hello [procedura dettagliata Kubernetes](container-service-kubernetes-walkthrough.md) include un esempio di come un servizio con hello tooexpose `kubectl expose` comando e il relativo `--type=LoadBalancer` flag.</span><span class="sxs-lookup"><span data-stu-id="4abdc-122">hello [Kubernetes walkthrough](container-service-kubernetes-walkthrough.md) includes an example of how tooexpose a service with hello `kubectl expose` command and its `--type=LoadBalancer` flag.</span></span> <span data-ttu-id="4abdc-123">Ecco i passaggi di hello:</span><span class="sxs-lookup"><span data-stu-id="4abdc-123">Here are hello steps :</span></span>

1. <span data-ttu-id="4abdc-124">Avviare una nuova distribuzione di contenitori.</span><span class="sxs-lookup"><span data-stu-id="4abdc-124">Start a new container deployment.</span></span> <span data-ttu-id="4abdc-125">Ad esempio, hello seguente comando avvia una nuova distribuzione chiamata `mynginx`.</span><span class="sxs-lookup"><span data-stu-id="4abdc-125">For example, hello following command starts a new deployment called `mynginx`.</span></span> <span data-ttu-id="4abdc-126">distribuzione di Hello è costituita da tre contenitori basati su hello Docker immagine per il server web Nginx hello.</span><span class="sxs-lookup"><span data-stu-id="4abdc-126">hello deployment consists of three containers based on hello Docker image for hello Nginx web server.</span></span>

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. <span data-ttu-id="4abdc-127">Verificare che i contenitori di hello siano in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="4abdc-127">Verify that hello containers are running.</span></span> <span data-ttu-id="4abdc-128">Ad esempio, se si esegue una query per i contenitori di hello con `kubectl get pods`, viene visualizzato il seguente toohello simili di output:</span><span class="sxs-lookup"><span data-stu-id="4abdc-128">For example, if you query for hello containers with `kubectl get pods`, you see output similar toohello following:</span></span>

    ![Avviare i contenitori Nginx](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. <span data-ttu-id="4abdc-130">tooconfigure hello carico bilanciamento tooaccept traffico esterno toohello distribuzione, eseguire `kubectl expose` con `--type=LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="4abdc-130">tooconfigure hello load balancer tooaccept external traffic toohello deployment, run `kubectl expose` with `--type=LoadBalancer`.</span></span> <span data-ttu-id="4abdc-131">Hello comando espone server Nginx hello sulla porta 80:</span><span class="sxs-lookup"><span data-stu-id="4abdc-131">hello following command exposes hello Nginx server on port 80:</span></span>

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. <span data-ttu-id="4abdc-132">Tipo `kubectl get svc` stato hello toosee dei servizi cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="4abdc-132">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="4abdc-133">Mentre il servizio di bilanciamento del carico hello Configura regola hello, hello `EXTERNAL-IP` di hello servizio viene visualizzato come `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="4abdc-133">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello service appears as `<pending>`.</span></span> <span data-ttu-id="4abdc-134">Dopo alcuni minuti, è configurato un indirizzo IP esterno hello:</span><span class="sxs-lookup"><span data-stu-id="4abdc-134">After a few minutes, hello external IP address is configured:</span></span> 

    ![Configurare il servizio di bilanciamento del carico di Azure](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. <span data-ttu-id="4abdc-136">Verificare che sia possibile accedere servizio hello all'indirizzo IP esterno hello.</span><span class="sxs-lookup"><span data-stu-id="4abdc-136">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="4abdc-137">Ad esempio, aprire un web browser toohello IP mostrato.</span><span class="sxs-lookup"><span data-stu-id="4abdc-137">For example, open a web browser toohello IP address shown.</span></span> <span data-ttu-id="4abdc-138">browser Hello Mostra i server web Nginx di hello in esecuzione in uno dei contenitori di hello.</span><span class="sxs-lookup"><span data-stu-id="4abdc-138">hello browser shows hello Nginx web server running in one of hello containers.</span></span> <span data-ttu-id="4abdc-139">In alternativa, eseguire hello `curl` o `wget` comando.</span><span class="sxs-lookup"><span data-stu-id="4abdc-139">Or, run hello `curl` or `wget` command.</span></span> <span data-ttu-id="4abdc-140">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4abdc-140">For example:</span></span>

    ```
    curl 13.82.93.130
    ```

    <span data-ttu-id="4abdc-141">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="4abdc-141">You should see output similar to:</span></span>

    ![Accesso a Nginx con il comando curl](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. <span data-ttu-id="4abdc-143">configurazione di hello toosee di bilanciamento del carico di Azure di hello, andare toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4abdc-143">toosee hello configuration of hello Azure load balancer, go toohello [Azure portal](https://portal.azure.com).</span></span>

7. <span data-ttu-id="4abdc-144">Cerca il gruppo di risorse hello per il cluster del servizio contenitore e selezionare bilanciamento del carico di hello per agente hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4abdc-144">Browse for hello resource group for your container service cluster, and select hello load balancer for hello agent VMs.</span></span> <span data-ttu-id="4abdc-145">Il nome deve essere hello uguale a servizio di contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="4abdc-145">Its name should be hello same as hello container service.</span></span> <span data-ttu-id="4abdc-146">(Non scegliere servizio di bilanciamento del carico hello per nodi master hello, hello uno cui nome include **master lb**.)</span><span class="sxs-lookup"><span data-stu-id="4abdc-146">(Don't choose hello load balancer for hello master nodes, hello one whose name includes **master-lb**.)</span></span> 

    ![Servizio di bilanciamento del carico nel gruppo di risorse](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. <span data-ttu-id="4abdc-148">Fare clic su Dettagli hello toosee di configurazione di bilanciamento del carico hello, **regole di bilanciamento del carico** e hello il nome della regola hello che è stato configurato.</span><span class="sxs-lookup"><span data-stu-id="4abdc-148">toosee hello details of hello load balancer configuration, click **Load balancing rules** and hello name of hello rule that was configured.</span></span>

    ![Regole del servizio di bilanciamento del carico](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-hello-service-configuration-file"></a><span data-ttu-id="4abdc-150">Esempio: Specificare `type: LoadBalancer` nel file di configurazione del servizio hello</span><span class="sxs-lookup"><span data-stu-id="4abdc-150">Example: Specify `type: LoadBalancer` in hello service configuration file</span></span>

<span data-ttu-id="4abdc-151">Se si distribuisce un'applicazione contenitore Kubernetes da un YAML o JSON [file di configurazione del servizio](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), specificare un bilanciamento del carico esterno aggiungendo hello specifica del servizio toohello riga seguente:</span><span class="sxs-lookup"><span data-stu-id="4abdc-151">If you deploy a Kubernetes container app from a YAML or JSON [service configuration file](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), specify an external load balancer by adding hello following line toohello service specification:</span></span>

```YAML
 "type": "LoadBalancer"
``` 



<span data-ttu-id="4abdc-152">i passaggi seguenti Hello usano hello Kubernetes [visitatori esempio](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span><span class="sxs-lookup"><span data-stu-id="4abdc-152">hello following steps use hello Kubernetes [Guestbook example](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span></span> <span data-ttu-id="4abdc-153">Questo esempio è un'app Web multi-livello basata su immagini Redis e PHP Docker.</span><span class="sxs-lookup"><span data-stu-id="4abdc-153">This example is a multi-tier web app based on  Redis and PHP Docker images.</span></span> <span data-ttu-id="4abdc-154">È possibile specificare nel file di configurazione del servizio hello che server front-end PHP hello Usa servizio di bilanciamento del carico di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4abdc-154">You can specify in hello service configuration file that hello frontend PHP server uses hello Azure load balancer.</span></span>

1. <span data-ttu-id="4abdc-155">Scaricare il file hello `guestbook-all-in-one.yaml` da [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span><span class="sxs-lookup"><span data-stu-id="4abdc-155">Download hello file `guestbook-all-in-one.yaml` from [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span></span> 
2. <span data-ttu-id="4abdc-156">Cerca hello `spec` per hello `frontend` servizio.</span><span class="sxs-lookup"><span data-stu-id="4abdc-156">Browse for hello `spec` for hello `frontend` service.</span></span>
3. <span data-ttu-id="4abdc-157">Rimuovere il commento riga hello `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="4abdc-157">Uncomment hello line `type: LoadBalancer`.</span></span>

    ![Servizio di bilanciamento durante la configurazione del servizio](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. <span data-ttu-id="4abdc-159">Salvare il file hello e distribuire l'applicazione hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4abdc-159">Save hello file, and deploy hello app by running hello following command:</span></span>

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. <span data-ttu-id="4abdc-160">Tipo `kubectl get svc` stato hello toosee dei servizi cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="4abdc-160">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="4abdc-161">Mentre il servizio di bilanciamento del carico hello Configura regola hello, hello `EXTERNAL-IP` di hello `frontend` servizio viene visualizzato come `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="4abdc-161">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello `frontend` service appears as `<pending>`.</span></span> <span data-ttu-id="4abdc-162">Dopo alcuni minuti, è configurato un indirizzo IP esterno hello:</span><span class="sxs-lookup"><span data-stu-id="4abdc-162">After a few minutes, hello external IP address is configured:</span></span> 

    ![Configurare il servizio di bilanciamento del carico di Azure](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. <span data-ttu-id="4abdc-164">Verificare che sia possibile accedere servizio hello all'indirizzo IP esterno hello.</span><span class="sxs-lookup"><span data-stu-id="4abdc-164">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="4abdc-165">Ad esempio, è possibile aprire un web browser toohello indirizzo IP esterno del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="4abdc-165">For example, you can open a web browser toohello external IP address of hello service.</span></span>

    ![Accedere al guestbook dall'esterno](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    <span data-ttu-id="4abdc-167">È possibile aggiungere voci del guestbook.</span><span class="sxs-lookup"><span data-stu-id="4abdc-167">You can add guestbook entries.</span></span>

7. <span data-ttu-id="4abdc-168">configurazione di hello toosee di bilanciamento del carico di Azure di hello, cercare per la risorsa del servizio di bilanciamento carico di hello cluster hello in hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4abdc-168">toosee hello configuration of hello Azure load balancer, browse for hello load balancer resource for hello cluster in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4abdc-169">Vedere i passaggi nell'esempio precedente hello hello.</span><span class="sxs-lookup"><span data-stu-id="4abdc-169">See hello steps in hello previous example.</span></span>

### <a name="considerations"></a><span data-ttu-id="4abdc-170">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="4abdc-170">Considerations</span></span>

* <span data-ttu-id="4abdc-171">Creazione di una regola di bilanciamento del carico hello viene eseguito in modo asincrono e informazioni su Bilanciamento hello il provisioning viene pubblicate nel servizio di hello `status.loadBalancer` campo.</span><span class="sxs-lookup"><span data-stu-id="4abdc-171">Creation of hello load balancer rule happens asynchronously, and information about hello provisioned balancer is published in hello service’s `status.loadBalancer` field.</span></span>
* <span data-ttu-id="4abdc-172">Ogni servizio viene assegnato automaticamente il proprio indirizzo IP virtuale nel bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="4abdc-172">Every service is automatically assigned its own virtual IP address in hello load balancer.</span></span>
* <span data-ttu-id="4abdc-173">Se si desidera bilanciamento del carico di hello tooreach da un nome DNS, lavorare con toocreate di provider del servizio del dominio un nome DNS per l'indirizzo IP della regola hello.</span><span class="sxs-lookup"><span data-stu-id="4abdc-173">If you want tooreach hello load balancer by a DNS name, work with your domain service provider toocreate a DNS name for hello rule's IP address.</span></span>

## <a name="http-or-https-traffic"></a><span data-ttu-id="4abdc-174">Traffico HTTP o HTTPS</span><span class="sxs-lookup"><span data-stu-id="4abdc-174">HTTP or HTTPS traffic</span></span>

<span data-ttu-id="4abdc-175">Saldo tooload HTTP o HTTPS traffico toocontainer web App e gestire i certificati di sicurezza di livello di trasporto (TLS), è possibile usare hello Kubernetes [in ingresso](https://kubernetes.io/docs/user-guide/ingress/) risorse.</span><span class="sxs-lookup"><span data-stu-id="4abdc-175">tooload balance HTTP or HTTPS traffic toocontainer web apps and manage certificates for transport layer security (TLS), you can use hello Kubernetes [Ingress](https://kubernetes.io/docs/user-guide/ingress/) resource.</span></span> <span data-ttu-id="4abdc-176">Un in ingresso è una raccolta di regole che consentono le connessioni in ingresso ai servizi di cluster di tooreach hello.</span><span class="sxs-lookup"><span data-stu-id="4abdc-176">An Ingress is a collection of rules that allow inbound connections tooreach hello cluster services.</span></span> <span data-ttu-id="4abdc-177">Per un toowork di risorse in ingresso, hello Kubernetes cluster deve disporre di un [controller in ingresso](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="4abdc-177">For an Ingress resource toowork, hello Kubernetes cluster must have an [Ingress controller](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) running.</span></span>

<span data-ttu-id="4abdc-178">Il servizio contenitore di Azure non implementa automaticamente un controller di Ingress di Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="4abdc-178">Azure Container Service does not implement a Kubernetes Ingress controller automatically.</span></span> <span data-ttu-id="4abdc-179">Sono disponibili diverse implementazioni di controller.</span><span class="sxs-lookup"><span data-stu-id="4abdc-179">Several controller implementations are available.</span></span> <span data-ttu-id="4abdc-180">Attualmente, hello [controller in ingresso Nginx](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) è consigliabile regole in entrata tooconfigure e bilanciamento del carico del traffico HTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4abdc-180">Currently, hello [Nginx Ingress controller](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) is recommended tooconfigure Ingress rules and load balance HTTP and HTTPS traffic.</span></span> 

<span data-ttu-id="4abdc-181">Per ulteriori informazioni, vedere hello [documentazione relativa al controller in ingresso Nginx](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span><span class="sxs-lookup"><span data-stu-id="4abdc-181">For more information, see hello [Nginx Ingress controller documentation](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4abdc-182">Quando si utilizza hello controller Nginx ingresso nel servizio contenitore di Azure, è necessario esporre la distribuzione di controller hello come un servizio con `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="4abdc-182">When using hello Nginx Ingress controller in Azure Container Service, you must expose hello controller deployment as a service with `type: LoadBalancer`.</span></span> <span data-ttu-id="4abdc-183">Consente di configurare hello Azure bilanciamento tooroute traffico toohello controller del carico.</span><span class="sxs-lookup"><span data-stu-id="4abdc-183">This configures hello Azure load balancer tooroute traffic toohello controller.</span></span> <span data-ttu-id="4abdc-184">Per ulteriori informazioni, vedere la sezione precedente di hello.</span><span class="sxs-lookup"><span data-stu-id="4abdc-184">For more information, see hello previous section.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4abdc-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4abdc-185">Next steps</span></span>

* <span data-ttu-id="4abdc-186">Vedere hello [Kubernetes LoadBalancer documentazione](https://kubernetes.io/docs/user-guide/load-balancer/)</span><span class="sxs-lookup"><span data-stu-id="4abdc-186">See hello [Kubernetes LoadBalancer documentation](https://kubernetes.io/docs/user-guide/load-balancer/)</span></span>
* <span data-ttu-id="4abdc-187">Altre informazioni su [Ingress di Kubernetes e controller di Ingress](https://kubernetes.io/docs/user-guide/ingress/)</span><span class="sxs-lookup"><span data-stu-id="4abdc-187">Learn more about [Kubernetes Ingress and Ingress controllers](https://kubernetes.io/docs/user-guide/ingress/)</span></span>
* <span data-ttu-id="4abdc-188">Vedere [esempi di Kubernetes](https://github.com/kubernetes/kubernetes/tree/master/examples)</span><span class="sxs-lookup"><span data-stu-id="4abdc-188">See [Kubernetes examples](https://github.com/kubernetes/kubernetes/tree/master/examples)</span></span>

