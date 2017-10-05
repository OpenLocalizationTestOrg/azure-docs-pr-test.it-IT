---
title: Visualizzare i log dei flussi dei gruppi di sicurezza di rete di Azure Network Watcher con strumenti open source | Microsoft Docs
description: Questa pagina illustra come usare strumenti open source per visualizzare i log dei flussi dei gruppi di sicurezza di rete.
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
ms.openlocfilehash: 20f60ccd9108a7473705c2368f28d3152d0dd614
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a><span data-ttu-id="95151-103">Visualizzare i log dei flussi dei gruppi di sicurezza di rete di Azure Network Watcher con strumenti open source</span><span class="sxs-lookup"><span data-stu-id="95151-103">Visualize Azure Network Watcher NSG flow logs using open source tools</span></span>

<span data-ttu-id="95151-104">I log dei flussi dei gruppi di sicurezza di rete contengono informazioni utili per comprendere il traffico IP in ingresso e in uscita nei gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="95151-104">Network Security Group flow logs provide information that can be used understand ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="95151-105">Questi log mostrano i flussi in ingresso e in uscita in base alle regole, alla scheda di interfaccia di rete a cui si applica il flusso, a informazioni a 5 tuple sul flusso (IP di origine/destinazione, porta di origine/destinazione e protocollo) e al fatto che il traffico sia stato consentito o rifiutato.</span><span class="sxs-lookup"><span data-stu-id="95151-105">These flow logs show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5 tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="95151-106">Analizzare manualmente i log dei flussi e ottenerne informazioni significative può essere difficile.</span><span class="sxs-lookup"><span data-stu-id="95151-106">These flow logs can be difficult to manually parse and gain insights from.</span></span> <span data-ttu-id="95151-107">Esistono tuttavia diversi strumenti open source che possono semplificare la visualizzazione di questi dati.</span><span class="sxs-lookup"><span data-stu-id="95151-107">However, there are several open source tools that can help visualize this data.</span></span> <span data-ttu-id="95151-108">Questo articolo presenta una soluzione per visualizzare questi log con Elastic Stack, che consentirà di indicizzare e visualizzare rapidamente i log dei flussi in un dashboard Kibana.</span><span class="sxs-lookup"><span data-stu-id="95151-108">This article will provide a solution to visualize these logs using the Elastic Stack, which will allow you to quickly index and visualize your flow logs on a Kibana dashboard.</span></span>

## <a name="scenario"></a><span data-ttu-id="95151-109">Scenario</span><span class="sxs-lookup"><span data-stu-id="95151-109">Scenario</span></span>

<span data-ttu-id="95151-110">In questo articolo si configurerà una soluzione che consentirà di visualizzare i log dei flussi dei gruppi di sicurezza di rete con Elastic Stack.</span><span class="sxs-lookup"><span data-stu-id="95151-110">In this article, we will set up a solution that will allow you to visualize Network Security Group flow logs using the Elastic Stack.</span></span>  <span data-ttu-id="95151-111">Un plug-in di input Logstash otterrà i log dei flussi direttamente dal BLOB del servizio di archiviazione configurato per contenerli.</span><span class="sxs-lookup"><span data-stu-id="95151-111">A Logstash input plugin will obtain the flow logs directly from the storage blob configured for containing the flow logs.</span></span> <span data-ttu-id="95151-112">Successivamente, con Elastic Stack, i log dei flussi verranno indicizzati e usati per creare un dashboard Kibana per visualizzare le informazioni.</span><span class="sxs-lookup"><span data-stu-id="95151-112">Then, using the Elastic Stack, the flow logs will be indexed and used to create a Kibana dashboard to visualize the information.</span></span>

![scenario][scenario]

## <a name="steps"></a><span data-ttu-id="95151-114">Passi</span><span class="sxs-lookup"><span data-stu-id="95151-114">Steps</span></span>

### <a name="enable-network-security-group-flow-logging"></a><span data-ttu-id="95151-115">Abilitare la registrazione dei flussi dei gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="95151-115">Enable Network Security Group flow logging</span></span>
<span data-ttu-id="95151-116">Per questo scenario, è necessario abilitare la registrazione dei flussi dei gruppi di sicurezza di rete in almeno un gruppo di sicurezza di rete nel proprio account.</span><span class="sxs-lookup"><span data-stu-id="95151-116">For this scenario, you must have Network Security Group Flow Logging enabled on at least one Network Security Group in your account.</span></span> <span data-ttu-id="95151-117">Per istruzioni in proposito, vedere [Introduzione alla registrazione dei flussi per i gruppi di sicurezza di rete](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="95151-117">For instructions on enabling Network Security Flow Logs, refer to the following article [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>


### <a name="set-up-the-elastic-stack"></a><span data-ttu-id="95151-118">Configurare Elastic Stack</span><span class="sxs-lookup"><span data-stu-id="95151-118">Set up the Elastic Stack</span></span>
<span data-ttu-id="95151-119">Connettendo i log dei flussi dei gruppi di sicurezza di rete con Elastic Stack, è possibile creare un dashboard Kibana che consente di eseguire ricerche e analisi, creare grafici e ottenere informazioni significative dai log.</span><span class="sxs-lookup"><span data-stu-id="95151-119">By connecting NSG flow logs with the Elastic Stack, we can create a Kibana dashboard what allows us to search, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="95151-120">Installare Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="95151-120">Install Elasticsearch</span></span>

1. <span data-ttu-id="95151-121">Elastic Stack versione 5.0 e successive richiede Java 8.</span><span class="sxs-lookup"><span data-stu-id="95151-121">The Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="95151-122">Eseguire il comando `java -version` per controllare la versione in uso.</span><span class="sxs-lookup"><span data-stu-id="95151-122">Run the command `java -version` to check your version.</span></span> <span data-ttu-id="95151-123">Se Java non è installato, vedere la documentazione sul [sito Web Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="95151-123">If you do not have java install, refer to documentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="95151-124">Scaricare il pacchetto binario corretto per il proprio sistema:</span><span class="sxs-lookup"><span data-stu-id="95151-124">Download the correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="95151-125">Per altri metodi di installazione, vedere [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html) (Installazione di Elasticsearch)</span><span class="sxs-lookup"><span data-stu-id="95151-125">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="95151-126">Verificare che Elasticsearch sia in esecuzione con questo comando:</span><span class="sxs-lookup"><span data-stu-id="95151-126">Verify that Elasticsearch is running with the command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="95151-127">La risposta visualizzata sarà simile a questa:</span><span class="sxs-lookup"><span data-stu-id="95151-127">You should see a response similar to this:</span></span>

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

<span data-ttu-id="95151-128">Per altre istruzioni sull'installazione di Elasticsearch, vedere la pagina [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html) (Installazione)</span><span class="sxs-lookup"><span data-stu-id="95151-128">For further instructions on installing Elastic search, refer to the page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="95151-129">Installare Logstash</span><span class="sxs-lookup"><span data-stu-id="95151-129">Install Logstash</span></span>

1. <span data-ttu-id="95151-130">Per installare Logstash, eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="95151-130">To install Logstash run the following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="95151-131">Successivamente è necessario configurare Logstash per accedere ai log dei flussi e analizzarli.</span><span class="sxs-lookup"><span data-stu-id="95151-131">Next we need to configure Logstash to access and parse the flow logs.</span></span> <span data-ttu-id="95151-132">Creare un file logstash.conf usando:</span><span class="sxs-lookup"><span data-stu-id="95151-132">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="95151-133">Aggiungere il contenuto seguente al file:</span><span class="sxs-lookup"><span data-stu-id="95151-133">Add the following content to the file:</span></span>

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

<span data-ttu-id="95151-134">Per altre istruzioni sull'installazione di Logstash, vedere la [documentazione ufficiale](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="95151-134">For further instructions on installing Logstash, refer to the [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-the-logstash-input-plugin-for-azure-blob-storage"></a><span data-ttu-id="95151-135">Installare il plug-in di input Logstash per l'archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="95151-135">Install the Logstash input plugin for Azure blob storage</span></span>

<span data-ttu-id="95151-136">Questo plug-in Logstash consentirà di accedere direttamente ai log dei flussi dall'account di archiviazione designato.</span><span class="sxs-lookup"><span data-stu-id="95151-136">This Logstash plugin will allow you to directly access the flow logs from their designated storage account.</span></span> <span data-ttu-id="95151-137">Per installare questo plug-in, nella directory di installazione Logstash predefinita (in questo caso /usr/share/logstash/bin) eseguire il comando:</span><span class="sxs-lookup"><span data-stu-id="95151-137">To install this plugin, from the default Logstash installation directory (in this case /usr/share/logstash/bin) run the command:</span></span>

```
logstash-plugin install logstash-input-azureblob
```

<span data-ttu-id="95151-138">Per avviare Logstash, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="95151-138">To start Logstash run the command:</span></span>

```
sudo /etc/init.d/logstash start
```

<span data-ttu-id="95151-139">Per altre informazioni sul plug-in, vedere la documentazione [qui](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span><span class="sxs-lookup"><span data-stu-id="95151-139">For more information about this plugin, refer to documentation [here](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="95151-140">Installare Kibana</span><span class="sxs-lookup"><span data-stu-id="95151-140">Install Kibana</span></span>

1. <span data-ttu-id="95151-141">Eseguire questi comandi per installare Kibana:</span><span class="sxs-lookup"><span data-stu-id="95151-141">Run the following commands to install Kibana:</span></span>

  ```
  curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
  tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
  ```

1. <span data-ttu-id="95151-142">Per eseguire Kibana, usare questi comandi:</span><span class="sxs-lookup"><span data-stu-id="95151-142">To run Kibana use the commands:</span></span>

  ```
  cd kibana-5.2.0-linux-x86_64/
  ./bin/kibana
  ```

1. <span data-ttu-id="95151-143">Per visualizzare l'interfaccia Web di Kibana, passare a `http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="95151-143">To view your Kibana web interface, navigate to `http://localhost:5601`</span></span>
1. <span data-ttu-id="95151-144">Per questo scenario, il modello di indice usato per i log dei flussi è "nsg-flow-logs".</span><span class="sxs-lookup"><span data-stu-id="95151-144">For this scenario, the index pattern used for the flow logs is "nsg-flow-logs".</span></span> <span data-ttu-id="95151-145">È possibile modificare il modello di indice nella sezione "output" del file logstash.conf.</span><span class="sxs-lookup"><span data-stu-id="95151-145">You may change the index pattern in the "output" section of your logstash.conf file.</span></span>

1. <span data-ttu-id="95151-146">Per visualizzare il dashboard Kibana in remoto, creare una regola dei gruppi di sicurezza di rete in ingresso che consenta l'accesso alla **porta 5601**.</span><span class="sxs-lookup"><span data-stu-id="95151-146">If you want to view the Kibana dashboard remotely, create an inbound NSG rule allowing access to **port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="95151-147">Creare un dashboard Kibana</span><span class="sxs-lookup"><span data-stu-id="95151-147">Create a Kibana dashboard</span></span>

<span data-ttu-id="95151-148">Per questo articolo, è stato fornito un dashboard di esempio per visualizzare tendenze e dettagli degli avvisi.</span><span class="sxs-lookup"><span data-stu-id="95151-148">For this article, we have provided a sample dashboard for you to view trends and details in your alerts.</span></span>

![Figura 1][1]

1. <span data-ttu-id="95151-150">Scaricare il file del dashboard [qui](https://aka.ms/networkwatchernsgflowlogdashboard), il file delle visualizzazioni [qui](https://aka.ms/networkwatchernsgflowlogvisualizations) e il file della ricerca salvata [qui](https://aka.ms/networkwatchernsgflowlogsearch).</span><span class="sxs-lookup"><span data-stu-id="95151-150">Download the dashboard file [here](https://aka.ms/networkwatchernsgflowlogdashboard), the visualization file [here](https://aka.ms/networkwatchernsgflowlogvisualizations), and the saved search file [here](https://aka.ms/networkwatchernsgflowlogsearch).</span></span>

1. <span data-ttu-id="95151-151">Nella scheda **Management** (Gestione) di Kibana passare a **Saved Objects** (Oggetti salvati) e importare tutti e tre i file.</span><span class="sxs-lookup"><span data-stu-id="95151-151">Under the **Management** tab of Kibana, navigate to **Saved Objects** and import all three files.</span></span> <span data-ttu-id="95151-152">Dalla scheda **Dashboard** è quindi possibile aprire e caricare il dashboard di esempio.</span><span class="sxs-lookup"><span data-stu-id="95151-152">Then from the **Dashboard** tab you can open and load the sample dashboard.</span></span>

<span data-ttu-id="95151-153">È anche possibile creare visualizzazioni e dashboard personalizzati per le metriche a cui si è interessati.</span><span class="sxs-lookup"><span data-stu-id="95151-153">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="95151-154">Per altre informazioni sulla creazione di visualizzazioni Kibana, vedere la [documentazione ufficiale](https://www.elastic.co/guide/en/kibana/current/visualize.html) di Kibana.</span><span class="sxs-lookup"><span data-stu-id="95151-154">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

### <a name="visualize-nsg-flow-logs"></a><span data-ttu-id="95151-155">Visualizzare i log dei flussi dei gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="95151-155">Visualize NSG flow logs</span></span>

<span data-ttu-id="95151-156">Il dashboard di esempio offre diverse visualizzazioni dei log dei flussi.</span><span class="sxs-lookup"><span data-stu-id="95151-156">The sample dashboard provides several visualizations of the flow logs:</span></span>

1. <span data-ttu-id="95151-157">Flussi per decisione/direzione nel tempo: grafici di serie temporali che mostrano il numero dei flussi nel periodo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="95151-157">Flows by Decision/Direction Over Time - time series graphs showing the number of flows over the time period.</span></span> <span data-ttu-id="95151-158">È possibile modificare l'unità di tempo e l'intervallo di entrambe queste visualizzazioni.</span><span class="sxs-lookup"><span data-stu-id="95151-158">You can edit the unit of time and span of both these visualizations.</span></span> <span data-ttu-id="95151-159">Il grafico dei flussi per decisione mostra la proporzione tra le decisioni di consentire e di rifiutare il traffico che sono state prese, mentre quello dei flussi per direzione mostra la proporzione tra traffico in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="95151-159">Flows by Decision shows the proportion of allow or deny decisions made, while Flows by Direction shows the proportion of inbound and outbound traffic.</span></span> <span data-ttu-id="95151-160">Questi oggetti visivi consentono di esaminare le tendenze del traffico nel tempo e individuare eventuali picchi o modelli insoliti.</span><span class="sxs-lookup"><span data-stu-id="95151-160">With these visuals you can examine traffic trends over time and look for any spikes or unusual patterns.</span></span>

  ![Figura 2][2]

1. <span data-ttu-id="95151-162">Flussi per porta di origine/destinazione: grafici a torta che mostrano la suddivisione dei flussi sulle rispettive porte.</span><span class="sxs-lookup"><span data-stu-id="95151-162">Flows by Destination/Source Port – pie charts showing the breakdown of flows to their respective ports.</span></span> <span data-ttu-id="95151-163">Questa visualizzazione consente di verificare le porte più usate.</span><span class="sxs-lookup"><span data-stu-id="95151-163">With this view you can see your most commonly used ports.</span></span> <span data-ttu-id="95151-164">Facendo clic su una porta specifica nel grafico a torta, il resto del dashboard viene filtrato in modo da visualizzare i flussi di tale porta.</span><span class="sxs-lookup"><span data-stu-id="95151-164">If you click on a specific port within the pie chart, the rest of the dashboard will filter down to flows of that port.</span></span>

  ![Figura 3][3]

1. <span data-ttu-id="95151-166">Numero di flussi e data e ora del primo log: metriche che mostrano il numero di flussi registrato e la data del primo log acquisito.</span><span class="sxs-lookup"><span data-stu-id="95151-166">Number of Flows and Earliest Log Time – metrics showing you the number of flows recorded and the date of the earliest log captured.</span></span>

  ![Figura 4][4]

1. <span data-ttu-id="95151-168">Flussi per gruppo di sicurezza di rete e regola: grafico a barre che mostra la distribuzione dei flussi in ogni gruppo di sicurezza di rete nonché la distribuzione delle regole all'interno di ogni gruppo.</span><span class="sxs-lookup"><span data-stu-id="95151-168">Flows by NSG and Rule – a bar graph showing you the distribution of flows within each NSG, as well as the distribution of rules within each NSG.</span></span> <span data-ttu-id="95151-169">Questo grafico consente di determinare il gruppo di sicurezza di rete e le regole che hanno generato la maggiore quantità di traffico.</span><span class="sxs-lookup"><span data-stu-id="95151-169">From here you can see which NSG and rules generated the most traffic.</span></span>

  ![Figura 5][5]

1. <span data-ttu-id="95151-171">10 principali IP di origine/destinazione: grafici a barre che mostrano i 10 principali indirizzi IP di origine e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="95151-171">Top 10 Source/Destination IPs – bar charts showing the top 10 source and destination IPs.</span></span> <span data-ttu-id="95151-172">È possibile modificare i grafici in modo da visualizzare un numero maggiore o minore di indirizzi IP principali.</span><span class="sxs-lookup"><span data-stu-id="95151-172">You can adjust these charts to show more or less top IPs.</span></span> <span data-ttu-id="95151-173">Questi grafici consentono di rilevare gli indirizzi IP più ricorrenti nonché le decisioni di consentire o rifiutare il traffico prese nei confronti di ogni IP.</span><span class="sxs-lookup"><span data-stu-id="95151-173">From here you can see the most commonly occurring IPs as well as the traffic decision (allow or deny) being made towards each IP.</span></span>

  ![Figura 6][6]

1. <span data-ttu-id="95151-175">Tuple dei flussi: questa tabella mostra le informazioni contenute in ogni tupla dei flussi, nonché il gruppo di sicurezza di rete e la regola corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="95151-175">Flow Tuples – this table shows you the information contained within each flow tuple, as well as its corresponding NGS and rule.</span></span>

  ![Figura 7][7]

<span data-ttu-id="95151-177">Usando la barra per le query nella parte superiore è possibile filtrare il dashboard in base a qualsiasi parametro dei flussi, come ID sottoscrizione, gruppi di risorse, regola o qualsiasi altra variabile a cui si è interessati.</span><span class="sxs-lookup"><span data-stu-id="95151-177">Using the query bar at the top of the dashboard, you can filter down the dashboard based on any parameter of the flows, such as subscription ID, resource groups, rule, or any other variable of interest.</span></span> <span data-ttu-id="95151-178">Per altre informazioni su query e filtri di Kibana, vedere la [documentazione ufficiale](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span><span class="sxs-lookup"><span data-stu-id="95151-178">For more about Kibana's queries and filters, refer to the [official documentation](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span></span>

## <a name="conclusion"></a><span data-ttu-id="95151-179">Conclusione</span><span class="sxs-lookup"><span data-stu-id="95151-179">Conclusion</span></span>

<span data-ttu-id="95151-180">Combinando i log dei flussi dei gruppi di sicurezza di rete con Elastic Stack, si è ottenuto uno strumento personalizzabile ed efficace per visualizzare il traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="95151-180">By combining the Network Security Group flow logs with the Elastic Stack, we have come up with powerful and customizable way to visualize our network traffic.</span></span> <span data-ttu-id="95151-181">Questi dashboard consentono di ottenere e condividere rapidamente informazioni significative sul traffico di rete, nonché di applicare filtri e ricercare potenziali anomalie.</span><span class="sxs-lookup"><span data-stu-id="95151-181">These dashboards allow you to quickly gain and share insights about your network traffic, as well as filter down and investigate on any potential anomalies.</span></span> <span data-ttu-id="95151-182">Usando Kibana, è possibile personalizzare i dashboard e creare visualizzazioni specifiche per soddisfare qualsiasi esigenza in termini di sicurezza, controllo e conformità.</span><span class="sxs-lookup"><span data-stu-id="95151-182">Using Kibana, you can tailor these dashboards and create specific visualizations to meet any security, audit, and compliance needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95151-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="95151-183">Next steps</span></span>

<span data-ttu-id="95151-184">Per informazioni su come visualizzare i log dei flussi dei gruppi di sicurezza di rete con Power BI, vedere [Visualizzare i log dei flussi dei gruppi di sicurezza di rete con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="95151-184">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
