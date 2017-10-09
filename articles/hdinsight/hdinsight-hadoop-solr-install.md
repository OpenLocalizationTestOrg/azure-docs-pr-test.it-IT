---
title: aaaUse genera Script azione tooinstall Solr nel cluster Hadoop - Azure | Documenti Microsoft
description: Informazioni su come cluster di HDInsight toocustomize con Solr mediante l'azione di Script.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a>Installare e usare Solr nei cluster HDInsight basati su Windows

Informazioni su come toocustomize HDInsight basati su Windows cluster con Solr mediante l'azione di Script e come toouse Solr toosearch dati.

> [!IMPORTANT]
> Hello passaggi di questa operazione solo documenti con i cluster HDInsight basati su Windows. HDInsight è disponibile in Windows solo per le versioni precedenti a HDInsight 3.4. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Per informazioni sull'uso di Solr con un cluster basato su Linux, vedere [Installare e usare Solr nei cluster Hadoop HDInsight (Linux)](hdinsight-hadoop-solr-install-linux.md).


È possibile installare Solr in qualsiasi tipo di cluster (Hadoop, Storm, HBase, Spark) su Azure HDInsight usando *Script azione*. Un tooinstall di script di esempio Solr in un cluster HDInsight è disponibile da un blob di archiviazione di Azure di sola lettura in [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

script di esempio Hello funziona solo con versione 3.1 del cluster HDInsight. Per altre informazioni sulle versioni dei cluster HDInsight, vedere [Versioni cluster HDInsight](hdinsight-component-versioning.md).

script di esempio Hello utilizzato in questo argomento crea un cluster basato su Windows Solr con una configurazione specifica. Se si desidera che tooconfigure hello Solr cluster con raccolte diverse, le partizioni, schemi, le repliche, e così via, è necessario modificare di conseguenza script hello e file binari di Solr.

**Articoli correlati**

* [Installare e usare Solr nei cluster Hadoop di HDInsight (Linux)](hdinsight-hadoop-solr-install-linux.md)
* [Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md): informazioni generali sulla creazione di cluster HDInsight
* [Personalizzare cluster HDInsight mediante l'azione Script][hdinsight-cluster-customize]: informazioni generali sulla personalizzazione di cluster HDInsight tramite Azione script.
* [Sviluppare script di Azione script per HDInsight](hdinsight-hadoop-script-actions.md)

## <a name="what-is-solr"></a>Che cos'è Solr?
<a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> è una piattaforma di ricerca aziendale che permette di eseguire ricerche full-text avanzate sui dati. Mentre Hadoop consente di archiviare e gestire grandi quantità di dati, Solr Apache fornisce funzionalità di ricerca di hello tooquickly recuperare i dati hello.

## <a name="install-solr-using-portal"></a>Installare Solr utilizzando il portale
1. Avviare la creazione di un cluster tramite hello **creazione personalizzata** opzione, come descritto in [cluster creare Hadoop in HDInsight](hdinsight-provision-clusters.md).
2. In hello **azioni Script** pagina della procedura guidata hello, fare clic su **aggiungere script azione** tooprovide i dettagli sulla azione script hello, come illustrato di seguito:

    ![Utilizzare l'azione Script toocustomize un cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "toocustomize azione Script Usa un cluster")

    <table border='1'>
        <tr><th>Proprietà</th><th>Valore</th></tr>
        <tr><td>Nome</td>
            <td>Specificare un nome per l'azione script hello. Ad esempio, <b>Install Solr</b>.</td></tr>
        <tr><td>URI script</td>
            <td>Specificare hello Uniform Resource Identifier (URI) toohello script che è richiamato toocustomize hello cluster. Ad esempio, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></td></tr>
        <tr><td>Tipo di nodo</td>
            <td>Specificare i nodi di hello in cui viene eseguito uno script di personalizzazione di hello. È possibile scegliere <b>Tutti i nodi</b>, <b>Solo nodi head</b> o <b>Solo nodi di lavoro</b>.
        <tr><td>parameters</td>
            <td>Specificare i parametri di hello, se richiesti dallo script hello. Hello script tooinstall Solr non richiede alcun parametro, pertanto è possibile lasciare vuoto questo.</td></tr>
    </table>

    È possibile aggiungere più di uno script azione tooinstall più componenti nel cluster hello. Dopo aver aggiunto gli script hello, fare clic su hello segno di spunta toostart la creazione di cluster hello.

## <a name="use-solr"></a>Utilizzare Solr
È prima di tutto necessario indicizzare Solr con alcuni file di dati. Quindi, è possibile utilizzare le query di ricerca di Solr toorun sui dati hello indicizzato. Eseguire hello seguendo i passaggi toouse Solr in un cluster HDInsight:

1. **Utilizzare tooremote Remote Desktop Protocol (RDP) in cluster di HDInsight hello con Solr installato**. Dal portale di Azure hello, abilitare Desktop remoto per il cluster hello che è stato creato con cluster hello installato e quindi remoto in Solr. Per istruzioni, vedere [connettersi tooHDInsight cluster tramite RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).
2. **Indicizzare Solr mediante il caricamento di file di dati**. Quando si indicizzano Solr, inserire i documenti che potrebbe essere necessario toosearch in. tooindex Solr, utilizzare il protocollo RDP tooremote in cluster hello, passare toohello desktop, aprire hello Hadoop riga di comando e passare troppo**C:\apps\dist\solr-4.7.2\example\exampledocs**. Eseguire hello comando seguente:

        java -jar post.jar solr.xml monitor.xml

    Si noterà hello seguente output sulla console hello:

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    utilità post.jar Hello indicizzati Solr con due documenti di esempio, **solr.xml** e **monitor.xml**. utilità post.jar Hello e documenti di esempio hello sono disponibili con l'installazione di Solr.
3. **Utilizzare hello Solr dashboard toosearch all'interno di hello indicizzata documenti**. In hello RDP sessione toohello HDInsight del cluster, aprire Internet Explorer e avviare il dashboard di Solr hello in **http://headnodehost:8983/solr / #/**. Dal riquadro sinistro di hello, da hello **selettore Core** elenco a discesa, selezionare **collection1**, all'interno di esso, fare clic su **Query**. Un esempio, tooselect e restituire tutti i documenti di hello Solr, fornire hello seguenti valori:

   * In hello **q** testo immettere  **\*:**\*. Ciò restituirà tutti i documenti indicizzati hello in Solr. Se si desidera toosearch una stringa specifica all'interno dei documenti hello, è possibile immettere qui la stringa.
   * In hello **wt** casella di testo, il formato di output di hello selezionare. Il valore predefinito è **json**. Fare clic su **Esegui query**.

     ![Utilizzare l'azione Script toocustomize un cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "eseguire una query su dashboard Solr")

     output di Hello restituisce hello due documenti che è stata utilizzata per l'indicizzazione di Solr. output di Hello analogo al seguente hello:

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }
4. **Consigliato: Eseguire il backup hello indicizzata dati da Solr tooAzure archiviazione Blob associato al cluster HDInsight hello**. È buona norma, è consigliabile eseguire backup dati hello indicizzato dai nodi di cluster Solr hello in archiviazione Blob di Azure. Eseguire hello seguendo i passaggi toodo pertanto:

   1. Dalla sessione RDP hello, aprire Internet Explorer e toohello punto URL seguente:

           http://localhost:8983/solr/replication?command=backup

       Viene visualizzata una risposta simile alla seguente:

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. Nella sessione remota hello, passare troppo {SOLR_HOME}\{raccolta} \data. Per cluster hello creati tramite script di esempio hello, deve essere **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**. In questa posizione, si dovrebbe essere una cartella snapshot creata con un nome simile troppo**snapshot.* timestamp** *.
   3. Codice postale cartella snapshot hello e caricarlo nell'archiviazione Blob tooAzure. Dalla riga di comando hello Hadoop, passare toohello percorso della cartella snapshot hello utilizzando hello comando seguente:

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       Questo comando copia hello dati dello snapshot troppo/esempio / / nel contenitore hello all'interno di predefinito hello Storage account associato hello cluster.

## <a name="install-solr-using-aure-powershell"></a>Installare Solr tramite Aure PowerShell
Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  esempio Hello viene illustrato come tooinstall Spark con Azure PowerShell. È necessario toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

## <a name="install-solr-using-net-sdk"></a>Installare Solr tramite .NET SDK
Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). esempio Hello viene illustrato come tooinstall Spark usando hello .NET SDK. È necessario toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

## <a name="see-also"></a>Vedere anche
* [Installare e usare Solr nei cluster Hadoop di HDInsight (Linux)](hdinsight-hadoop-solr-install-linux.md)
* [Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md): informazioni generali sulla creazione di cluster HDInsight
* [Personalizzare cluster HDInsight mediante l'azione Script][hdinsight-cluster-customize]: informazioni generali sulla personalizzazione di cluster HDInsight tramite Azione script.
* [Sviluppare script di Azione script per HDInsight](hdinsight-hadoop-script-actions.md)
* [Installare e usare Spark nei cluster HDInsight][hdinsight-install-spark]: esempio di azione script sull'installazione di Spark.
* [Installare R nei cluster HDInsight][hdinsight-install-r]: esempio di azione script sull'installazione di R.
* [Installare e usare Spark nei cluster HDInsight](hdinsight-hadoop-giraph-install.md): esempio di Script azione sull'installazione di Giraph

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
