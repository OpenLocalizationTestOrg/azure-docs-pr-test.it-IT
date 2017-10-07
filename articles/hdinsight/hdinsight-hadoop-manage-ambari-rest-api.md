---
title: aaaMonitor e gestire Hadoop con l'API REST Ambari - HDInsight di Azure | Documenti Microsoft
description: "Informazioni su come toouse Ambari toomonitor e gestire i cluster Hadoop in HDInsight di Azure. In questo documento, si apprenderà come cluster di hello toouse API REST Ambari incluso in HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2400530f-92b3-47b7-aa48-875f028765ff
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 1866a77c8e402231bccbcfba7174253aca41339b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-rest-api"></a>Gestire cluster HDInsight con Ambari REST API hello

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

Informazioni su come toouse hello toomanage Ambari REST API e monitorare i cluster Hadoop in HDInsight di Azure.

Ambari Apache semplifica la gestione hello e monitoraggio di un cluster Hadoop fornendo un web toouse semplice interfaccia utente e REST API. Ambari è incluso nel cluster HDInsight che utilizzano il sistema operativo Linux di hello. È possibile utilizzare cluster di hello toomonitor Ambari e apportare modifiche alla configurazione.

## <a id="whatis"></a>Informazioni su Ambari

[Ambari Apache](http://ambari.apache.org) fornisce un'interfaccia utente che può essere utilizzato tooprovision, gestire e monitorare i cluster Hadoop. Gli sviluppatori possono integrare queste funzionalità nelle proprie applicazioni utilizzando hello [API REST Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

Ambari viene fornito per impostazione predefinita con i cluster HDInsight basati su Linux.

## <a name="how-toouse-hello-ambari-rest-api"></a>Come toouse hello API REST Ambari

> [!IMPORTANT]
> Hello informazioni ed esempi in questo documento richiedono un cluster HDInsight che utilizza il sistema operativo Linux. Per altre informazioni, vedere [Guida introduttiva di HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).

vengono forniti esempi di Hello in questo documento per shell Bonaldi hello (bash) e PowerShell. bash Hello esempi sono stati testati con GNU bash 4.3.11, ma dovrebbe funzionare con altre shell Unix. esempi di PowerShell Hello sono stati testati con PowerShell 5.0, ma dovrebbero funzionare con PowerShell 3.0 o versione successiva.

Se si utilizza hello __shell Bonaldi__ (Bash), è necessario disporre delle seguenti hello installato:

* [cURL](http://curl.haxx.se/): cURL è un'utilità che può essere utilizzati toowork con le API REST dalla riga di comando hello. In questo documento è toocommunicate utilizzato con l'API REST Ambari hello.

Sia con bash che con PowerShell è necessario che sia installato anche [jq](https://stedolan.github.io/jq/). Jq è un'utilità per lavorare con documenti JSON. Viene utilizzato in **tutti** esempi Bash, hello e **uno** degli esempi di PowerShell hello.

### <a name="base-uri-for-ambari-rest-api"></a>URI di base per l'API REST Ambari

URI di base per l'API REST Ambari in HDInsight hello Hello è https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, in cui **CLUSTERNAME** hello nome del cluster.

> [!IMPORTANT]
> Mentre il nome del cluster hello in hello completo parte di nome (FQDN) del dominio di hello URI (CLUSTERNAME.azurehdinsight.net) è tra maiuscole e minuscole, le altre occorrenze in hello URI tra maiuscole e minuscole. Ad esempio, se il cluster è denominato `MyCluster`, hello di seguito è URI validi:
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> esempio Hello URI restituito un errore perché hello seconda occorrenza di nome hello è non hello correzione case.
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a>Autenticazione

Connessione tooAmbari in HDInsight richiede HTTPS. Nome dell'account admin hello utilizzare (valore predefinito di hello è **admin**) e la password fornita durante la creazione del cluster.

## <a name="examples-authentication-and-parsing-json"></a>Esempi: autenticazione e analisi di JSON

Hello seguenti esempi illustrano come una richiesta GET hello toomake base Ambari REST API:

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> esempi di Bash Hello in questo documento apportare hello seguenti presupposti:
>
> * nome di accesso Hello per cluster hello è il valore predefinito hello di `admin`.
> * `$PASSWORD`contiene la password di hello per hello comando account di accesso di HDInsight. È possibile impostare questo valore usando `PASSWORD='mypassword'`.
> * `$CLUSTERNAME`contiene il nome di hello del cluster di hello. È possibile impostare questo valore usando `set CLUSTERNAME='clustername'`

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> esempi di PowerShell Hello in questo documento apportare hello seguenti presupposti:
>
> * `$creds`è un oggetto credenziali che contiene l'account di accesso amministratore hello e una password per il cluster hello. È possibile impostare questo valore utilizzando `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` fornendo credenziali hello quando richiesto.
> * `$clusterName`è una stringa che contiene il nome di hello del cluster di hello. È possibile impostare questo valore usando `$clusterName="clustername"`.

Entrambi gli esempi di restituire un documento JSON che inizia con l'esempio seguente la toohello simile informazioni:

```json
{
"href" : "http://10.0.0.10:8080/api/v1/clusters/CLUSTERNAME",
"Clusters" : {
    "cluster_id" : 2,
    "cluster_name" : "CLUSTERNAME",
    "health_report" : {
    "Host/stale_config" : 0,
    "Host/maintenance_state" : 0,
    "Host/host_state/HEALTHY" : 7,
    "Host/host_state/UNHEALTHY" : 0,
    "Host/host_state/HEARTBEAT_LOST" : 0,
    "Host/host_state/INIT" : 0,
    "Host/host_status/HEALTHY" : 7,
    "Host/host_status/UNHEALTHY" : 0,
    "Host/host_status/UNKNOWN" : 0,
    "Host/host_status/ALERT" : 0
    ...
```

### <a name="parsing-json-data"></a>Analisi dei dati JSON

Hello seguente utilizza `jq` tooparse hello documento di risposta JSON e visualizzare solo il messaggio hello `health_report` informazioni dai risultati di hello.

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

PowerShell 3.0 e versioni successive fornisce hello `ConvertFrom-Json` cmdlet, che converte i documenti JSON hello in un oggetto che è più facile toowork con da PowerShell. Hello seguente utilizza `ConvertFrom-Json` toodisplay solo hello `health_report` informazioni dai risultati di hello.

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> Durante la maggior parte degli esempi di questo documento viene utilizzato `ConvertFrom-Json` toodisplay elementi dal documento di risposta hello, hello [Ambari aggiornamento configurazione](#example-update-ambari-configuration) esempio Usa jq. Jq tooconstruct in questo esempio viene utilizzato un nuovo modello da un documento di risposta JSON hello.

Per un riferimento completo di hello API REST, vedere [Ambari API riferimento V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

## <a name="example-get-hello-fqdn-of-cluster-nodes"></a>Esempio: Ottenere hello FQDN di nodi del cluster

Quando si lavora con HDInsight, potrebbe essere necessario tooknow nome di dominio completo hello (FQDN) di un nodo del cluster. È possibile recuperare facilmente hello FQDN per hello vari nodi inclusi nel cluster hello hello seguono esempi di utilizzo:

* **Tutti i nodi**

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" \
    | jq '.items[].Hosts.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.Hosts.host_name
    ```

* **Nodi head**

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HDFS/components/NAMENODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/NAMENODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* **Nodi di lavoro**

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/DATANODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/DATANODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* **Nodi Zookeeper**

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

## <a name="example-get-hello-internal-ip-address-of-cluster-nodes"></a>Esempio: Ottenere l'indirizzo IP interno hello dei nodi del cluster

> [!IMPORTANT]
> gli indirizzi IP di Hello restituiti da esempi di hello in questa sezione sono non direttamente accessibile su internet di hello. Ovvero sono accessibili solo all'interno di rete virtuale di Azure che contiene il cluster di HDInsight hello hello.
>
> Per altre informazioni sull'uso di HDInsight e delle reti virtuali vedere [Estendere le funzionalità di HDInsight usando una rete virtuale di Azure personalizzata](hdinsight-extend-hadoop-virtual-network.md).

indirizzo IP di hello toofind, è necessario conoscere il nome di dominio completo interno hello (FQDN) di hello nodi del cluster. Dopo aver creato hello FQDN, è possibile ottenere quindi l'indirizzo IP hello dell'host hello. Hello negli esempi seguenti vengono innanzitutto query Ambari per nome di dominio completo di tutti i nodi host hello hello, quindi eseguire una query Ambari per indirizzo IP hello di ogni host.

```bash
for HOSTNAME in $(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" | jq -r '.items[].Hosts.host_name')
do
    IP=$(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts/$HOSTNAME" | jq -r '.Hosts.ip')
  echo "$HOSTNAME <--> $IP"
done
```

```powershell
$uri = "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts"
$resp = Invoke-WebRequest -Uri $uri -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
foreach($item in $respObj.items) {
    $hostName = [string]$item.Hosts.host_name
    $hostInfoResp = Invoke-WebRequest -Uri "$uri/$hostName" `
        -Credential $creds
    $hostInfoObj = ConvertFrom-Json $hostInfoResp 
    $hostIp = $hostInfoObj.Hosts.ip
    "$hostName <--> $hostIp"
}
```

## <a name="example-get-hello-default-storage"></a>Esempio: Ottenere spazio di archiviazione predefinito hello

Quando si crea un cluster HDInsight, è necessario utilizzare un Account di archiviazione Azure o di un archivio Data Lake come spazio di archiviazione predefinito hello per cluster hello. È possibile utilizzare queste informazioni Ambari tooretrieve dopo aver creato il cluster hello. Ad esempio, se si desidera che il contenitore di toohello tooread/scrittura dati all'esterno di HDInsight.

Hello negli esempi seguenti recupero hello archiviazione configurazione predefinita dal cluster hello:

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
| jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'
```

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties.'fs.defaultFS'
```

> [!IMPORTANT]
> Questi esempi vengono restituiti hello prima configurazione applicata toohello server (`service_config_version=1`) che contiene queste informazioni. Se si recupera un valore che è stato modificato dopo la creazione del cluster, è possibile necessarie toolist hello configurazione versioni e recuperare hello più recente.

valore restituito di Hello è tooone simile di hello seguono esempi:

* `wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`-Questo valore indica che tale cluster hello viene utilizzato un account di archiviazione di Azure per spazio di archiviazione predefinito. Hello `ACCOUNTNAME` valore è il nome di hello hello dell'account di archiviazione. Hello `CONTAINER` parte è il nome di hello del contenitore blob hello nell'account di archiviazione hello. contenitore di Hello è radice hello di archiviazione compatibili di HDFS per cluster hello hello.

* `adl://home`-Questo valore indica che tale cluster hello utilizza un archivio Azure Data Lake per spazio di archiviazione predefinito.

    nome dell'account archivio Data Lake hello toofind, utilizzare hello seguono esempi:

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.hostname'
    ```

    Hello valore restituito è simile troppo`ACCOUNTNAME.azuredatalakestore.net`, dove `ACCOUNTNAME` è il nome di hello di hello account archivio Data Lake.

    directory di hello toofind all'interno di archivio Data Lake contenente archiviazione hello per cluster hello, utilizzare hello seguono esempi:

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.mountpoint'
    ```

    Hello valore restituito è simile troppo`/clusters/CLUSTERNAME/`. Questo valore è un percorso all'interno di hello account archivio Data Lake. Questo percorso è la radice hello di hello HDFS compatibile file system per il cluster hello. 

> [!NOTE]
> Hello `Get-AzureRmHDInsightCluster` cmdlet forniti da [Azure PowerShell](/powershell/azure/overview) anche restituisce hello informazioni sull'archiviazione per cluster hello.


## <a name="example-get-configuration"></a>Esempio: ottenere una configurazione

1. Ottenere le configurazioni di hello che sono disponibili per il cluster.

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    Questo esempio viene restituito un documento JSON che contiene la configurazione corrente di hello (identificato da hello *tag* valore) per i componenti di hello installati nel cluster hello. Hello esempio seguente è tratto da dati hello restituiti da un tipo di cluster Spark.
   
   ```json
   "spark-metrics-properties" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-fairscheduler" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-sparkconf" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   }
   ```

2. Ottenere la configurazione di hello per componente hello che si è interessati. In hello seguente esempio, sostituire `INITIAL` con il valore di tag hello restituito dalla richiesta precedente hello.

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    Questo esempio viene restituito un documento JSON che contiene la configurazione corrente di hello per hello `core-site` componente.

## <a name="example-update-configuration"></a>Esempio: aggiornare la configurazione

1. Ottenere la configurazione corrente di hello cui Ambari vengono archiviate come hello "DCM":

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    Questo esempio viene restituito un documento JSON che contiene la configurazione corrente di hello (identificato da hello *tag* valore) per i componenti di hello installati nel cluster hello. Hello esempio seguente è tratto da dati hello restituiti da un tipo di cluster Spark.
   
    ```json
    "spark-metrics-properties" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-fairscheduler" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-sparkconf" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    }
    ```
   
    Da questo elenco, è necessario il nome hello toocopy del componente hello (ad esempio, **spark\_thrift\_sparkconf** hello e **tag** valore.

2. Recuperare la configurazione di hello per componente hello e tag tramite hello seguenti comandi:
   
    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=spark-thrift-sparkconf&tag=INITIAL" \
    | jq --arg newtag $(echo version$(date +%s%N)) '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    ```powershell
    $epoch = Get-Date -Year 1970 -Month 1 -Day 1 -Hour 0 -Minute 0 -Second 0
    $now = Get-Date
    $unixTimeStamp = [math]::truncate($now.ToUniversalTime().Subtract($epoch).TotalMilliSeconds)
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=spark-thrift-sparkconf&tag=INITIAL" `
        -Credential $creds
    $resp.Content | jq --arg newtag "version$unixTimeStamp" '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    > [!NOTE]
    > Sostituire **spark-thrift-sparkconf** e **iniziale** con tag che si desidera tooretrieve hello configurazione per e componente hello.
   
    Jq è dati hello tooturn utilizzati recuperati dal HDInsight in un nuovo modello di configurazione. In particolare, questi esempi eseguono hello seguenti azioni:
   
    * Crea un valore univoco contenente hello stringa "version" e la data di hello, che viene archiviato in `newtag`.

    * Crea un documento radice per la nuova configurazione desiderato di hello.

    * Ottiene hello contenuto di hello `.items[]` della matrice e lo aggiunge in hello **desired_config** elemento.

    * Eliminazioni hello `href`, `version`, e `Config` elementi, mentre gli elementi non sono necessari toosubmit una nuova configurazione.

    * Aggiunge un elemento `tag` con un valore di `version#################`. la parte numerica di Hello è basata su hello data corrente. Ogni configurazione deve avere un tag univoco.
     
    Infine, i dati hello viene salvati toohello `newconfig.json` documento. struttura del documento Hello dovrebbe apparire simile toohello esempio seguente:
     
     ```json
    {
        "Clusters": {
            "desired_config": {
            "tag": "version1459260185774265400",
            "type": "spark-thrift-sparkconf",
            "properties": {
                ....
            },
            "properties_attributes": {
                ....
            }
        }
    }
    ```

3. Aprire hello `newconfig.json` documento e modificare o aggiungere valori hello `properties` oggetto. modifiche di esempio seguenti Hello hello valore `"spark.yarn.am.memory"` da `"1g"` troppo`"3g"`. Aggiunge anche `"spark.kryoserializer.buffer.max"` con un valore di `"256m"`.
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    Dopo aver eseguito le modifiche, salvare file hello.

4. Utilizzare i seguenti comandi toosubmit hello aggiornato configurazione tooAmbari hello.
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" -X PUT -d @newconfig.json "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
    ```

    ```powershell
    $newConfig = Get-Content .\newconfig.json
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body $newConfig
    $resp.Content
    ```
   
    Questi comandi inviare contenuto hello di hello **newconfig.json** toohello cluster di file desiderato hello nuova configurazione. richiesta di Hello restituisce un documento JSON. Hello **versionTag** elemento in questo documento deve corrispondere una versione di hello inviato e hello **configurazioni** oggetto contiene le modifiche alla configurazione hello richiesto.

### <a name="example-restart-a-service-component"></a>Esempio: Riavviare un componente del servizio

A questo punto, se si osserva hello Ambari web dell'interfaccia utente, hello servizio Spark indica che riavviato per rendere effettive nuova configurazione hello toobe. Utilizzare i passaggi toorestart hello servizio hello.

1. Utilizzare hello tooenable la modalità di manutenzione per hello servizio Spark seguenti:

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}'
    $resp.Content
    ```
   
    Questi comandi inviano un server di toohello documento JSON che attiva la modalità di manutenzione. È possibile verificare che il servizio di hello è ora in modalità di manutenzione utilizzando hello seguito richiesta:
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK" \
    | jq .ServiceInfo.maintenance_state
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK2" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.ServiceInfo.maintenance_state
    ```
   
    Hello valore restituito è `ON`.

2. Successivamente, utilizzare hello tooturn servizio hello seguenti:

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}'
    $resp.Content
    ```
    
    risposta Hello è simile toohello esempio seguente:
   
    ```json
    {
        "href" : "http://10.0.0.18:8080/api/v1/clusters/CLUSTERNAME/requests/29",
        "Requests" : {
            "id" : 29,
            "status" : "Accepted"
        }
    }
    ```
    
    > [!IMPORTANT]
    > Hello `href` valore restituito da questo URI Usa indirizzo IP interno hello hello di nodo del cluster. toouse dall'esterno del cluster di hello, sostituire parte hello '10.0.0.18:8080' con FQDN del cluster hello hello. 
    
    Hello seguenti comandi di recupera lo stato di hello della richiesta di hello:

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/requests/29" \
    | jq .Requests.request_status
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/requests/29" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.Requests.request_status
    ```

    Una risposta di `COMPLETED` indica che la richiesta hello è stata completata.

3. Una volta completata la richiesta precedente hello, utilizzare hello toostart hello servizio.
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```
   
    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}'
    ```
    servizio Hello ora utilizza hello nuova configurazione.

4. Infine, utilizzare hello seguente tooturn la modalità di manutenzione.
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}'
    ```

## <a name="next-steps"></a>Passaggi successivi

Per un riferimento completo di hello API REST, vedere [Ambari API riferimento V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

