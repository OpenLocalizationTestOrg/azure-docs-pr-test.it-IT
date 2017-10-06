---
title: le librerie Hive aaaAdd durante HDInsight cluster creazione - Azure | Documenti Microsoft
description: Informazioni su come le librerie Hive tooadd (file jar), tooan HDInsight cluster durante la creazione del cluster.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 2fd74b8d-c006-45c6-a9e2-72ff5d2d978a
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 2e028a07c3248205def0789af2c262a0774a8f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a>Aggiungere librerie Hive personalizzate durante la creazione del cluster HDInsight

Se si dispongono di librerie di uso frequente con Hive in HDInsight, in questo documento contiene informazioni sull'utilizzo di librerie di hello toopre carico un'azione Script durante la creazione del cluster. Librerie aggiunte utilizzando i passaggi di hello in questo documento sono disponibili a livello globale nell'Hive, non c'è alcuna necessità toouse [aggiungere JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload li.

## <a name="how-it-works"></a>Funzionamento

Quando si crea un cluster, è possibile specificare facoltativamente un'azione che esegue uno script nei nodi del cluster hello durante la creazione di Script. script Hello in questo documento accetta un solo parametro, ovvero una posizione WASB contenente hello librerie (archiviate come file jar) toobe precaricati.

Durante la creazione del cluster script hello enumera i file hello, li copia toohello `/usr/lib/customhivelibs/` directory nei nodi head e di lavoro, quindi li aggiunge toohello `hive.aux.jars.path` proprietà hello `core-site.xml` file. Nei cluster basati su Linux, viene anche aggiornato hello `hive-env.sh` file con percorso hello del file hello.

> [!NOTE]
> Usando le azioni script hello in questo articolo, le librerie di hello rende disponibili in hello seguenti scenari:
>
> * **HDInsight basati su Linux** : quando l'utilizzo di un client di Hive, hello **WebHCat**, e **HiveServer2**.
> * **HDInsight basati su Windows** - quando si utilizza il client di Hive hello e **WebHCat**.

## <a name="hello-script"></a>script Hello

**Percorso dello script**

Per i **cluster basati su Linux**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)

Per i **cluster basati su Windows**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

**Requisiti**

* gli script Hello devono essere applicato tooboth hello **nodi Head** e **nodi di lavoro**.

* Hello JAR desiderato tooinstall devono essere archiviate nell'archiviazione Blob di Azure in un **singolo contenitore**.

* account di archiviazione Hello libreria hello dei file jar contenente **deve** essere cluster HDInsight toohello collegato durante la creazione. Deve essere account di archiviazione predefinito hello o un account aggiunto tramite __configurazione facoltativa__.

* Hello WASB percorso toohello contenitore deve essere specificato come un toohello parametro azione Script. Ad esempio, se hello JAR vengono archiviati in un contenitore denominato **librerie** su un account di archiviazione denominato **la risorsa mystorage**, il parametro hello sarebbe  **wasb://libs@mystorage.blob.core.windows.net/** .

  > [!NOTE]
  > Questo documento presuppone che hanno già crei un account di archiviazione, il contenitore blob e tooit file hello caricato.
  >
  > Se non è stato creato un account di archiviazione, è possibile farlo tramite hello [portale di Azure](https://portal.azure.com). È quindi possibile utilizzare un'utilità, ad esempio [Azure Storage Explorer](http://storageexplorer.com/) toocreate un contenitore nell'account di hello e caricamento file tooit.

## <a name="create-a-cluster-using-hello-script"></a>Creare un cluster utilizzando script hello

> [!NOTE]
> Hello alla procedura seguente crea un cluster HDInsight basati su Linux. Selezionare un cluster basato su Windows, toocreate **Windows** come hello cluster del sistema operativo durante la creazione di cluster hello e utilizzare script di Windows (PowerShell) hello anziché script bash hello.
>
> È inoltre possibile utilizzare Azure PowerShell o hello HDInsight .NET SDK toocreate un cluster utilizzando lo script. Per altre informazioni sull'uso di questi metodi, vedere [Personalizzare i cluster HDInsight con azioni script](hdinsight-hadoop-customize-cluster-linux.md).

1. Avviare il provisioning di un cluster attenendosi alla procedura hello in [cluster HDInsight di effettuare il provisioning in Linux](hdinsight-hadoop-provision-linux-clusters.md), ma non viene completato il provisioning.

2. In hello **configurazione facoltativa** pannello seleziona **azioni Script**e fornire hello le seguenti informazioni:

   * **NOME**: immettere un nome descrittivo per l'azione script hello.

   * **SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh

   * **HEAD**: selezionare questa opzione.

   * **LAVORO**: selezionare questa opzione.

   * **ZOOKEEPER**: lasciare vuoto questo campo.

   * **I parametri**: immettere hello WASB toohello contenitore e l'archiviazione account indirizzo contenente JAR hello. Ad esempio, **wasb://libs@mystorage.blob.core.windows.net/**.

3. Nella parte inferiore di hello di hello **azioni Script**, utilizzare hello **selezionare** configurazione hello toosave dei pulsanti.

4. In hello **configurazione facoltativa** pannello seleziona **account di archiviazione collegati** e seleziona hello **aggiungere una chiave di archiviazione** collegamento. Selezionare l'account di archiviazione hello contenente JAR hello e quindi utilizzare hello **selezionare** impostazioni toosave pulsanti e hello restituito **configurazione facoltativa** blade.

5. Hello utilizzare **selezionare** pulsante nella parte inferiore di hello di hello **configurazione facoltativa** informazioni di configurazione facoltativa hello toosave blade.

6. Continuano il provisioning del cluster di hello, come descritto in [cluster HDInsight di effettuare il provisioning in Linux](hdinsight-hadoop-provision-linux-clusters.md).

Al termine della creazione del cluster, si è in grado di toouse JAR di hello aggiunti tramite questo script dall'Hive senza hello toouse `ADD JAR` istruzione.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'uso di Hive, vedere l'articolo relativo all' [uso di Hive con HDInsight](hdinsight-use-hive.md)
