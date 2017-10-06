---
title: flusso di controllo di rete di Azure aaaVisualize registra utilizzando strumenti open source | Documenti Microsoft
description: "Questa pagina vengono descritti come modalità di apertura di log del flusso di origine strumenti toovisualize NSG toouse."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e9b2dcad-4da4-4d6b-aee2-6d0afade0cb8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 47cb529d4a1e00e8c4c0fa6885cbf72aed3e74c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a><span data-ttu-id="a2695-103">Visualizzare i log dei flussi dei gruppi di sicurezza di rete di Azure Network Watcher con strumenti open source</span><span class="sxs-lookup"><span data-stu-id="a2695-103">Visualize Azure Network Watcher NSG flow logs using open source tools</span></span>

<span data-ttu-id="a2695-104">I log dei flussi dei gruppi di sicurezza di rete contengono informazioni utili per comprendere il traffico IP in ingresso e in uscita nei gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="a2695-104">Network Security Group flow logs provide information that can be used understand ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="a2695-105">Questi log flusso mostrano in uscita e i flussi in ingresso per ogni regola, hello flusso hello NIC applica, 5 tuple informazioni flusso hello (origine/destinazione IP, porta di origine/destinazione, Protocol), e se il traffico hello consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="a2695-105">These flow logs show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5 tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="a2695-106">Questi registri di flusso possono essere difficile toomanually analisi e ottenere informazioni approfondite.</span><span class="sxs-lookup"><span data-stu-id="a2695-106">These flow logs can be difficult toomanually parse and gain insights from.</span></span> <span data-ttu-id="a2695-107">Esistono tuttavia diversi strumenti open source che possono semplificare la visualizzazione di questi dati.</span><span class="sxs-lookup"><span data-stu-id="a2695-107">However, there are several open source tools that can help visualize this data.</span></span> <span data-ttu-id="a2695-108">In questo articolo verrà fornite toovisualize una soluzione di questi log tramite hello elastico Stack, che consentono di indice tooquickly e visualizzare i log di flusso in un dashboard Kibana.</span><span class="sxs-lookup"><span data-stu-id="a2695-108">This article will provide a solution toovisualize these logs using hello Elastic Stack, which will allow you tooquickly index and visualize your flow logs on a Kibana dashboard.</span></span>

## <a name="scenario"></a><span data-ttu-id="a2695-109">Scenario</span><span class="sxs-lookup"><span data-stu-id="a2695-109">Scenario</span></span>

<span data-ttu-id="a2695-110">In questo articolo, si imposterà una soluzione che consentirà di registri di flusso di gruppo di sicurezza di rete toovisualize mediante hello Stack elastico.</span><span class="sxs-lookup"><span data-stu-id="a2695-110">In this article, we will set up a solution that will allow you toovisualize Network Security Group flow logs using hello Elastic Stack.</span></span>  <span data-ttu-id="a2695-111">Un plug-in di input Logstash otterrà registri flusso hello direttamente dal blob di archiviazione hello configurato per contenente i registri del flusso di hello.</span><span class="sxs-lookup"><span data-stu-id="a2695-111">A Logstash input plugin will obtain hello flow logs directly from hello storage blob configured for containing hello flow logs.</span></span> <span data-ttu-id="a2695-112">Quindi, utilizza hello Stack elastico, hello flusso registri verranno indicizzati e utilizzato toocreate una Kibana toovisualize hello le informazioni relative.</span><span class="sxs-lookup"><span data-stu-id="a2695-112">Then, using hello Elastic Stack, hello flow logs will be indexed and used toocreate a Kibana dashboard toovisualize hello information.</span></span>

![scenario][scenario]

## <a name="steps"></a><span data-ttu-id="a2695-114">Passi</span><span class="sxs-lookup"><span data-stu-id="a2695-114">Steps</span></span>

### <a name="enable-network-security-group-flow-logging"></a><span data-ttu-id="a2695-115">Abilitare la registrazione dei flussi dei gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="a2695-115">Enable Network Security Group flow logging</span></span>
<span data-ttu-id="a2695-116">Per questo scenario, è necessario abilitare la registrazione dei flussi dei gruppi di sicurezza di rete in almeno un gruppo di sicurezza di rete nel proprio account.</span><span class="sxs-lookup"><span data-stu-id="a2695-116">For this scenario, you must have Network Security Group Flow Logging enabled on at least one Network Security Group in your account.</span></span> <span data-ttu-id="a2695-117">Per istruzioni su come abilitare i registri di flusso di sicurezza di rete, consultare toohello articolo seguente [registrazione tooflow introduzione per gruppi di sicurezza di rete](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2695-117">For instructions on enabling Network Security Flow Logs, refer toohello following article [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>


### <a name="set-up-hello-elastic-stack"></a><span data-ttu-id="a2695-118">Impostare hello Stack elastico</span><span class="sxs-lookup"><span data-stu-id="a2695-118">Set up hello Elastic Stack</span></span>
<span data-ttu-id="a2695-119">Connettendosi NSG flusso registri con hello Stack elastico, è possibile creare un dashboard Kibana cosa consente toosearch, grafico, analizzare e derivare informazioni dai nostri registri.</span><span class="sxs-lookup"><span data-stu-id="a2695-119">By connecting NSG flow logs with hello Elastic Stack, we can create a Kibana dashboard what allows us toosearch, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="a2695-120">Installare Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="a2695-120">Install Elasticsearch</span></span>

1. <span data-ttu-id="a2695-121">Hello Stack elastico dalla versione 5.0 e versioni successive richiede Java 8.</span><span class="sxs-lookup"><span data-stu-id="a2695-121">hello Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="a2695-122">Eseguire il comando hello `java -version` toocheck la versione in uso.</span><span class="sxs-lookup"><span data-stu-id="a2695-122">Run hello command `java -version` toocheck your version.</span></span> <span data-ttu-id="a2695-123">Se non si dispone java installare, vedere toodocumentation su [sito Web Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="a2695-123">If you do not have java install, refer toodocumentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="a2695-124">Scaricare hello pacchetto binario corretto per il sistema:</span><span class="sxs-lookup"><span data-stu-id="a2695-124">Download hello correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="a2695-125">Per altri metodi di installazione, vedere [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html) (Installazione di Elasticsearch)</span><span class="sxs-lookup"><span data-stu-id="a2695-125">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="a2695-126">Verificare che Elasticsearch sia in esecuzione con il comando hello:</span><span class="sxs-lookup"><span data-stu-id="a2695-126">Verify that Elasticsearch is running with hello command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="a2695-127">Verrà visualizzato un toothis simile risposta:</span><span class="sxs-lookup"><span data-stu-id="a2695-127">You should see a response similar toothis:</span></span>

    ```
    {
    "name" : "Angela Del Toro",
    "cluster_name" : "elasticsearch",
    "version" : {
        "number" : "5.2.0",
        "build_hash" : "8ff36d139e16f8720f2947ef62c8167a888992fe",
        "build_timestamp" : "2016-01-27T13:32:39Z",
        "build_snapshot" : false,
        "lucene_version" : "6.1.0"
    },
    "tagline" : "You Know, for Search"
    }
    ```

<span data-ttu-id="a2695-128">Per ulteriori istruzioni sull'installazione ricerca elastico, vedere la pagina toohello [installazione](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="a2695-128">For further instructions on installing Elastic search, refer toohello page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="a2695-129">Installare Logstash</span><span class="sxs-lookup"><span data-stu-id="a2695-129">Install Logstash</span></span>

1. <span data-ttu-id="a2695-130">tooinstall Logstash eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="a2695-130">tooinstall Logstash run hello following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="a2695-131">Successivamente è necessario tooconfigure Logstash tooaccess e analizzare i log di flusso hello.</span><span class="sxs-lookup"><span data-stu-id="a2695-131">Next we need tooconfigure Logstash tooaccess and parse hello flow logs.</span></span> <span data-ttu-id="a2695-132">Creare un file logstash.conf usando:</span><span class="sxs-lookup"><span data-stu-id="a2695-132">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="a2695-133">Aggiungere i seguenti file di contenuto toohello hello:</span><span class="sxs-lookup"><span data-stu-id="a2695-133">Add hello following content toohello file:</span></span>

  ```
    input {
      azureblob
        {
            storage_account_name => "mystorageaccount"
            storage_access_key => "storageaccesskey"
            container => "nsgflowlogContainerName"
            codec => "json"
        }
      }

      filter {
        split { field => "[records]" }
        split { field => "[records][properties][flows]"}
        split { field => "[records][properties][flows][flows]"}
        split { field => "[records][properties][flows][flows][flowTuples]"}

     mutate{
      split => { "[records][resourceId]" => "/"}
      add_field => {"Subscription" => "%{[records][resourceId][2]}"
                    "ResourceGroup" => "%{[records][resourceId][4]}"
                    "NetworkSecurityGroup" => "%{[records][resourceId][8]}"}
      convert => {"Subscription" => "string"}
      convert => {"ResourceGroup" => "string"}
      convert => {"NetworkSecurityGroup" => "string"}
      split => { "[records][properties][flows][flows][flowTuples]" => ","}
      add_field => {
                  "unixtimestamp" => "%{[records][properties][flows][flows][flowTuples][0]}"
                  "srcIp" => "%{[records][properties][flows][flows][flowTuples][1]}"
                  "destIp" => "%{[records][properties][flows][flows][flowTuples][2]}"
                  "srcPort" => "%{[records][properties][flows][flows][flowTuples][3]}"
                  "destPort" => "%{[records][properties][flows][flows][flowTuples][4]}"
                  "protocol" => "%{[records][properties][flows][flows][flowTuples][5]}"
                  "trafficflow" => "%{[records][properties][flows][flows][flowTuples][6]}"
                  "traffic" => "%{[records][properties][flows][flows][flowTuples][7]}"
                   }
      convert => {"unixtimestamp" => "integer"}
      convert => {"srcPort" => "integer"}
      convert => {"destPort" => "integer"}        
     }

     date{
       match => ["unixtimestamp" , "UNIX"]
     }
    }

    output {
      stdout { codec => rubydebug }
      elasticsearch {
        hosts => "localhost"
        index => "nsg-flow-logs"
      }
    }  

  ```

<span data-ttu-id="a2695-134">Per ulteriori istruzioni sull'installazione Logstash, consultare toohello [documentazione ufficiale](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="a2695-134">For further instructions on installing Logstash, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-hello-logstash-input-plugin-for-azure-blob-storage"></a><span data-ttu-id="a2695-135">Installare hello Logstash input del plug-in per l'archiviazione blob di Azure</span><span class="sxs-lookup"><span data-stu-id="a2695-135">Install hello Logstash input plugin for Azure blob storage</span></span>

<span data-ttu-id="a2695-136">Questo plug-in Logstash consentirà toodirectly accesso hello flusso registri il proprio account di archiviazione designate.</span><span class="sxs-lookup"><span data-stu-id="a2695-136">This Logstash plugin will allow you toodirectly access hello flow logs from their designated storage account.</span></span> <span data-ttu-id="a2695-137">tooinstall questo plug-in, dalla directory di installazione di Logstash hello predefinita (in questo caso /usr/share/logstash/bin) comando hello:</span><span class="sxs-lookup"><span data-stu-id="a2695-137">tooinstall this plugin, from hello default Logstash installation directory (in this case /usr/share/logstash/bin) run hello command:</span></span>

```
logstash-plugin install logstash-input-azureblob
```

<span data-ttu-id="a2695-138">eseguire il comando hello Logstash toostart:</span><span class="sxs-lookup"><span data-stu-id="a2695-138">toostart Logstash run hello command:</span></span>

```
sudo /etc/init.d/logstash start
```

<span data-ttu-id="a2695-139">Per ulteriori informazioni su questo plug-in, vedere toodocumentation [qui](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span><span class="sxs-lookup"><span data-stu-id="a2695-139">For more information about this plugin, refer toodocumentation [here](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="a2695-140">Installare Kibana</span><span class="sxs-lookup"><span data-stu-id="a2695-140">Install Kibana</span></span>

1. <span data-ttu-id="a2695-141">Eseguire i seguenti comandi tooinstall Kibana hello:</span><span class="sxs-lookup"><span data-stu-id="a2695-141">Run hello following commands tooinstall Kibana:</span></span>

  ```
  curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
  tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
  ```

1. <span data-ttu-id="a2695-142">toorun Kibana utilizzare i comandi di hello:</span><span class="sxs-lookup"><span data-stu-id="a2695-142">toorun Kibana use hello commands:</span></span>

  ```
  cd kibana-5.2.0-linux-x86_64/
  ./bin/kibana
  ```

1. <span data-ttu-id="a2695-143">tooview web Kibana interfaccia, passare troppo`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="a2695-143">tooview your Kibana web interface, navigate too`http://localhost:5601`</span></span>
1. <span data-ttu-id="a2695-144">Per questo scenario, il modello di indice hello usato per i log di flusso hello è "nsg-flusso di log".</span><span class="sxs-lookup"><span data-stu-id="a2695-144">For this scenario, hello index pattern used for hello flow logs is "nsg-flow-logs".</span></span> <span data-ttu-id="a2695-145">È possibile modificare il modello di indice hello nella sezione "output" hello del file logstash.conf.</span><span class="sxs-lookup"><span data-stu-id="a2695-145">You may change hello index pattern in hello "output" section of your logstash.conf file.</span></span>

1. <span data-ttu-id="a2695-146">Se si desidera dashboard Kibana di tooview hello in modalità remota, creare una regola di gruppo in ingresso che consente l'accesso troppo**porta 5601**.</span><span class="sxs-lookup"><span data-stu-id="a2695-146">If you want tooview hello Kibana dashboard remotely, create an inbound NSG rule allowing access too**port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="a2695-147">Creare un dashboard Kibana</span><span class="sxs-lookup"><span data-stu-id="a2695-147">Create a Kibana dashboard</span></span>

<span data-ttu-id="a2695-148">In questo articolo, Microsoft ha fornito un dashboard di esempio per consentire le tendenze tooview e i dettagli degli avvisi.</span><span class="sxs-lookup"><span data-stu-id="a2695-148">For this article, we have provided a sample dashboard for you tooview trends and details in your alerts.</span></span>

![Figura 1][1]

1. <span data-ttu-id="a2695-150">Scaricare il file dashboard hello [qui](https://aka.ms/networkwatchernsgflowlogdashboard), file di visualizzazione hello [qui](https://aka.ms/networkwatchernsgflowlogvisualizations)e i file di ricerca salvata hello [qui](https://aka.ms/networkwatchernsgflowlogsearch).</span><span class="sxs-lookup"><span data-stu-id="a2695-150">Download hello dashboard file [here](https://aka.ms/networkwatchernsgflowlogdashboard), hello visualization file [here](https://aka.ms/networkwatchernsgflowlogvisualizations), and hello saved search file [here](https://aka.ms/networkwatchernsgflowlogsearch).</span></span>

1. <span data-ttu-id="a2695-151">In hello **Management** scheda di Kibana, passare troppo**gli oggetti salvati** e importare tutti i tre file.</span><span class="sxs-lookup"><span data-stu-id="a2695-151">Under hello **Management** tab of Kibana, navigate too**Saved Objects** and import all three files.</span></span> <span data-ttu-id="a2695-152">Quindi dal hello **Dashboard** scheda è possibile aprire e carico hello dashboard di esempio.</span><span class="sxs-lookup"><span data-stu-id="a2695-152">Then from hello **Dashboard** tab you can open and load hello sample dashboard.</span></span>

<span data-ttu-id="a2695-153">È anche possibile creare visualizzazioni e dashboard personalizzati per le metriche a cui si è interessati.</span><span class="sxs-lookup"><span data-stu-id="a2695-153">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="a2695-154">Per altre informazioni sulla creazione di visualizzazioni Kibana, vedere la [documentazione ufficiale](https://www.elastic.co/guide/en/kibana/current/visualize.html) di Kibana.</span><span class="sxs-lookup"><span data-stu-id="a2695-154">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

### <a name="visualize-nsg-flow-logs"></a><span data-ttu-id="a2695-155">Visualizzare i log dei flussi dei gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="a2695-155">Visualize NSG flow logs</span></span>

<span data-ttu-id="a2695-156">dashboard di esempio Hello fornisce diverse visualizzazioni dei registri di flusso hello:</span><span class="sxs-lookup"><span data-stu-id="a2695-156">hello sample dashboard provides several visualizations of hello flow logs:</span></span>

1. <span data-ttu-id="a2695-157">I flussi dalla decisione/direzione nel tempo, i grafici di serie temporali che mostra il numero di hello di flussi su hello periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="a2695-157">Flows by Decision/Direction Over Time - time series graphs showing hello number of flows over hello time period.</span></span> <span data-ttu-id="a2695-158">È possibile modificare l'unità di hello di tempo e l'intervallo di entrambe queste visualizzazioni.</span><span class="sxs-lookup"><span data-stu-id="a2695-158">You can edit hello unit of time and span of both these visualizations.</span></span> <span data-ttu-id="a2695-159">Flussi di base delle decisioni Mostra hello proporzione di consentono o negare le decisioni prese, mentre i flussi da parte di hello Mostra direzione del traffico in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="a2695-159">Flows by Decision shows hello proportion of allow or deny decisions made, while Flows by Direction shows hello proportion of inbound and outbound traffic.</span></span> <span data-ttu-id="a2695-160">Questi oggetti visivi consentono di esaminare le tendenze del traffico nel tempo e individuare eventuali picchi o modelli insoliti.</span><span class="sxs-lookup"><span data-stu-id="a2695-160">With these visuals you can examine traffic trends over time and look for any spikes or unusual patterns.</span></span>

  ![Figura 2][2]

1. <span data-ttu-id="a2695-162">I flussi dalla porta di origine/destinazione: grafici a torta che mostra la suddivisione hello di flussi di tootheir rispettive porte.</span><span class="sxs-lookup"><span data-stu-id="a2695-162">Flows by Destination/Source Port – pie charts showing hello breakdown of flows tootheir respective ports.</span></span> <span data-ttu-id="a2695-163">Questa visualizzazione consente di verificare le porte più usate.</span><span class="sxs-lookup"><span data-stu-id="a2695-163">With this view you can see your most commonly used ports.</span></span> <span data-ttu-id="a2695-164">Se si fa clic su una porta specifica all'interno del grafico a torta hello, rest hello del dashboard hello filtrerà verso il basso tooflows di tale porta.</span><span class="sxs-lookup"><span data-stu-id="a2695-164">If you click on a specific port within hello pie chart, hello rest of hello dashboard will filter down tooflows of that port.</span></span>

  ![Figura 3][3]

1. <span data-ttu-id="a2695-166">Numero di flussi e ora Log meno recente: metriche mostrando hello numero di flussi registrato e data hello del log meno recente hello acquisiti.</span><span class="sxs-lookup"><span data-stu-id="a2695-166">Number of Flows and Earliest Log Time – metrics showing you hello number of flows recorded and hello date of hello earliest log captured.</span></span>

  ![Figura 4][4]

1. <span data-ttu-id="a2695-168">Flussi di gruppo e regola, un grafico a barre che mostra distribuzione hello dei flussi all'interno di ogni gruppo, nonché distribuzione hello di regole all'interno di ogni gruppo.</span><span class="sxs-lookup"><span data-stu-id="a2695-168">Flows by NSG and Rule – a bar graph showing you hello distribution of flows within each NSG, as well as hello distribution of rules within each NSG.</span></span> <span data-ttu-id="a2695-169">Da qui è possibile visualizzare il gruppo e le regole generati hello maggior parte del traffico.</span><span class="sxs-lookup"><span data-stu-id="a2695-169">From here you can see which NSG and rules generated hello most traffic.</span></span>

  ![Figura 5][5]

1. <span data-ttu-id="a2695-171">Primi 10 origine/destinazione IP: grafici a barre che mostra origine primi 10 hello e gli indirizzi IP di destinazione.</span><span class="sxs-lookup"><span data-stu-id="a2695-171">Top 10 Source/Destination IPs – bar charts showing hello top 10 source and destination IPs.</span></span> <span data-ttu-id="a2695-172">È possibile modificare questi tooshow grafici gli indirizzi IP superiore più o meno.</span><span class="sxs-lookup"><span data-stu-id="a2695-172">You can adjust these charts tooshow more or less top IPs.</span></span> <span data-ttu-id="a2695-173">Da qui è possibile vedere hello più di frequente che si verificano gli indirizzi IP, nonché hello decisione di traffico (Consenti o Nega) apportate a ogni IP.</span><span class="sxs-lookup"><span data-stu-id="a2695-173">From here you can see hello most commonly occurring IPs as well as hello traffic decision (allow or deny) being made towards each IP.</span></span>

  ![Figura 6][6]

1. <span data-ttu-id="a2695-175">Tuple di flusso: in questa tabella mostra le informazioni contenute all'interno di ogni tupla del flusso, nonché il relativo NGS corrispondente e regola hello.</span><span class="sxs-lookup"><span data-stu-id="a2695-175">Flow Tuples – this table shows you hello information contained within each flow tuple, as well as its corresponding NGS and rule.</span></span>

  ![Figura 7][7]

<span data-ttu-id="a2695-177">Usa barra query hello nella parte superiore di hello del dashboard hello, è possibile filtrare verso il basso dashboard hello in base a qualsiasi parametro di hello flussi, ad esempio l'ID sottoscrizione, i gruppi di risorse, regola o qualsiasi altra variabile di interesse.</span><span class="sxs-lookup"><span data-stu-id="a2695-177">Using hello query bar at hello top of hello dashboard, you can filter down hello dashboard based on any parameter of hello flows, such as subscription ID, resource groups, rule, or any other variable of interest.</span></span> <span data-ttu-id="a2695-178">Per ulteriori informazioni sulla query e i filtri del Kibana, consultare toohello [documentazione ufficiale](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span><span class="sxs-lookup"><span data-stu-id="a2695-178">For more about Kibana's queries and filters, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span></span>

## <a name="conclusion"></a><span data-ttu-id="a2695-179">Conclusioni</span><span class="sxs-lookup"><span data-stu-id="a2695-179">Conclusion</span></span>

<span data-ttu-id="a2695-180">Combinando i registri del flusso di hello il gruppo di sicurezza di rete con hello Stack elastico è stata ideare toovisualize sistema efficiente e personalizzabile il traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="a2695-180">By combining hello Network Security Group flow logs with hello Elastic Stack, we have come up with powerful and customizable way toovisualize our network traffic.</span></span> <span data-ttu-id="a2695-181">Questi dashboard consentono un miglioramento tooquickly e condividono informazioni dettagliate sul traffico di rete, nonché filtro verso il basso e analizzare in qualsiasi potenziali anomalie.</span><span class="sxs-lookup"><span data-stu-id="a2695-181">These dashboards allow you tooquickly gain and share insights about your network traffic, as well as filter down and investigate on any potential anomalies.</span></span> <span data-ttu-id="a2695-182">Utilizza Kibana, è possibile personalizzare questi dashboard e creare visualizzazioni specifiche toomeet eventuali esigenze di sicurezza, conformità e controllo.</span><span class="sxs-lookup"><span data-stu-id="a2695-182">Using Kibana, you can tailor these dashboards and create specific visualizations toomeet any security, audit, and compliance needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2695-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a2695-183">Next steps</span></span>

<span data-ttu-id="a2695-184">Informazioni su come toovisualize il flusso di gruppo Registra con Power BI visitando [NSG visualizzare flussi di log con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="a2695-184">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
