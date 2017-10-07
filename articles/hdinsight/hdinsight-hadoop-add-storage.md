---
title: account di archiviazione di Azure aggiuntivi aaaAdd tooHDInsight | Documenti Microsoft
description: Informazioni su come archiviazione di Azure aggiuntivi tooadd account cluster HDInsight esistente tooan.
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: ce5acfa4b61bf7e83b1fb374d64a1eaa3182fbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-additional-storage-accounts-toohdinsight"></a>Aggiungere ulteriore spazio di archiviazione account tooHDInsight

Informazioni su come toouse script azioni tooadd aggiuntive Azure storage account tooHDInsight. Hello passaggi descritti in questo documento aggiungere un cluster di HDInsight basati su Linux esistente storage account tooan.

> [!IMPORTANT]
> informazioni di Hello in questo documento sono informazioni sull'aggiunta di cluster tooa ulteriore spazio di archiviazione dopo che è stato creato. Per informazioni sull'aggiunta di account di archiviazione durante la creazione del cluster, vedere [Configurare cluster in HDInsight con Hadoop, Spark, Kafka e altro](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="how-it-works"></a>Funzionamento

Questo script accetta hello seguenti parametri:

* __Nome dell'account di archiviazione Azure__: nome hello del cluster di HDInsight toohello hello storage account tooadd. Dopo l'esecuzione di script hello, HDInsight può leggere e scrivere dati archiviati in questo account di archiviazione.

* __Chiave dell'account di archiviazione di Azure__: una chiave che concede l'accesso toohello account di archiviazione.

* __-p__ (facoltativo): se specificato, chiave hello non è crittografato e viene archiviato nel file core-Site.XML hello come testo normale.

Durante l'elaborazione, lo script di hello esegue hello seguenti azioni:

* Se hello account di archiviazione esiste già nella configurazione core-Site.XML hello per cluster hello, hello script viene chiuso e che non vengano eseguite ulteriori azioni.

* Verifica che l'account di archiviazione hello esiste e sono accessibili mediante chiave hello.

* Crittografa la chiave di hello utilizzando credenziali cluster hello.

* Aggiunge il file core-Site.XML toohello di hello storage account.

* Arresta e riavvia i servizi di Oozie, YARN, MapReduce2 e HDFS hello. Arrestare e avviare questi servizi, tali dati toouse hello nuovo account di archiviazione.

> [!WARNING]
> Non è supportato l'utilizzo di un account di archiviazione in un percorso diverso da quello del cluster HDInsight hello.

## <a name="hello-script"></a>script Hello

__Percorso dello script__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)

__Requisiti__:

* script Hello deve essere applicato a hello __nodi Head__.

## <a name="toouse-hello-script"></a>script hello toouse

Questo script può essere utilizzato da hello portale di Azure, Azure PowerShell, o hello Azure CLI 1.0. Per ulteriori informazioni, vedere hello [ai cluster HDInsight basati su Linux personalizzare mediante l'azione di script](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) documento.

> [!IMPORTANT]
> Quando si utilizza la procedura hello descritta nel documento personalizzazione hello, utilizzare questo script hello tooapply le informazioni seguenti:
>
> * Sostituire qualsiasi azione di script di esempio URI con hello URI per questo script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).
> * Sostituire i parametri di esempio con nome di account di archiviazione di Azure hello e la chiave del cluster di hello archiviazione account toobe toohello aggiunto. Se tramite hello portale di Azure, questi parametri devono essere separati da uno spazio.
> * Non è necessario toomark questo script come __Persisted__, come aggiorna direttamente configurazione Ambari hello per cluster hello.

## <a name="known-issues"></a>Problemi noti

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a>Account di archiviazione non visualizzati nel portale di Azure o negli strumenti

Quando la visualizzazione hello HDInsight cluster in hello portale di Azure, la selezione di hello __gli account di archiviazione__ voce __proprietà__ non vengono visualizzati gli account di archiviazione aggiunti tramite questa azione di script. Azure PowerShell e CLI di Azure non visualizzano di account di archiviazione aggiuntivo hello.

non vengono visualizzate informazioni sull'archiviazione Hello perché script hello modifica solo una configurazione di core-Site.XML hello per cluster hello. Queste informazioni non vengono utilizzate durante il recupero delle informazioni del cluster hello utilizzando le API di gestione di Azure.

informazioni sull'account di archiviazione tooview aggiunto toohello cluster tramite questo script, utilizzare hello Ambari REST API. Utilizzare queste informazioni di hello tooretrieve i comandi seguenti per il cluster:

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter hello cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> Impostare `$clusterName` toohello nome del cluster HDInsight hello. Impostare `$storageAccountName` toohello nome dell'account di archiviazione hello. Quando richiesto, immettere l'account di accesso cluster hello (amministratore) e la password.

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> Impostare `$PASSWORD` password dell'account di accesso (amministrazione) di toohello cluster. Impostare `$CLUSTERNAME` toohello nome del cluster HDInsight hello. Impostare `$STORAGEACCOUNTNAME` toohello nome dell'account di archiviazione hello.
>
> Questo esempio viene utilizzato [curl (http://curl.haxx.se/)](http://curl.haxx.se/) e [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve e analizzare i dati JSON.

Quando si utilizza questo comando, sostituire __CLUSTERNAME__ con nome hello del cluster HDInsight hello. Sostituire __PASSWORD__ con password di accesso hello HTTP per cluster hello. Sostituire __STORAGEACCOUNT__ con nome hello hello dell'account di archiviazione aggiunti mediante l'azione di script. Le informazioni restituite da questo comando viene visualizzata toohello simile, il testo seguente:

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

Questo testo è un esempio di una chiave crittografata, che viene utilizzato tooaccess hello account di archiviazione.

### <a name="unable-tooaccess-storage-after-changing-key"></a>Non è possibile tooaccess archiviazione dopo la modifica chiave

Se si modifica la chiave hello per un account di archiviazione, HDInsight non può accedere non è più account di archiviazione hello. HDInsight utilizza una copia della chiave memorizzata nella cache in core-Site.XML hello per cluster hello. Questa copia memorizzata nella cache deve essere una nuova chiave di hello toomatch aggiornato.

Esecuzione azione di script hello nuovamente __non__ aggiornare la chiave di hello, come script hello controlla toosee se esiste già una voce per l'account di archiviazione hello. Se esiste già una voce, non viene apportata alcuna modifica.

toowork questo problema, è necessario rimuovere una voce hello hello account di archiviazione. Utilizzare hello entrata passaggi tooremove hello esistente:

1. In un web browser, aprire hello Ambari Web UI per il cluster HDInsight. Hello URI è https://CLUSTERNAME.azurehdinsight.net. Sostituire __CLUSTERNAME__ con nome hello del cluster.

    Quando richiesto, immettere l'account di accesso HTTP hello e una password per il cluster.

2. Selezionare nell'elenco dei servizi a sinistra di hello della pagina hello hello __HDFS__. Selezionare quindi hello __configurazioni__ scheda centro hello della pagina di hello.

3. In hello __filtro...__  immettere un valore di __fs.azure.account__. Restituisce le voci relative agli account di archiviazione aggiuntivi che sono stati aggiunti toohello cluster. Sono disponibili due tipi di voci, ovvero __keyprovider__ e __key__. Entrambi contengono il nome di hello hello dell'account di archiviazione come parte del nome della chiave hello.

    di seguito Hello sono voci di esempio per un account di archiviazione denominato __la risorsa mystorage__:

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. Dopo aver identificato le chiavi di hello hello account di archiviazione è necessario tooremove, utilizzare hello rosso '-' icona toohello diritto di hello voce toodelete è. Utilizzare quindi hello __salvare__ pulsante toosave le modifiche.

5. Dopo che sono state salvate le modifiche, utilizzare account di archiviazione hello tooadd azione script hello e cluster di toohello nuovo valore della chiave.

### <a name="poor-performance"></a>Prestazioni non ottimali

Se l'account di archiviazione hello è in un'area diversa rispetto al cluster HDInsight hello, si potrebbe influire negativamente sulle prestazioni. L'accesso ai dati in un'area diversa invia il traffico di rete all'esterno di hello internazionali data center di Azure e attraverso hello internet pubblico, che può provocare latenza.

> [!WARNING]
> Non è possibile utilizzare un account di archiviazione in un'area diversa rispetto al cluster HDInsight hello.

### <a name="additional-charges"></a>Costi aggiuntivi

Se l'account di archiviazione hello è in un'area diversa rispetto a hello cluster HDInsight, è possibile riscontrare costi di uscita aggiuntive sulla fatturazione di Azure. Viene applicato un addebito di uscita quando i dati escono dal data center di un'area, L'addebito viene applicato anche se il traffico di hello è destinato a un altro data center di Azure in un'area diversa.

> [!WARNING]
> Non è possibile utilizzare un account di archiviazione in un'area diversa rispetto al cluster HDInsight hello.

## <a name="next-steps"></a>Passaggi successivi

Si è appreso come account del cluster HDInsight esistente tooan tooadd ulteriore spazio di archiviazione. Per altre informazioni sulle azioni script, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md)
