---
title: aaaUse vuoto nodi periferici nel cluster Hadoop in HDInsight - Azure | Documenti Microsoft
description: "Come tooadd tooan di nodo un bordo vuoto HDInsight cluster che può essere utilizzato come un client e quindi/host di test delle applicazioni di HDInsight."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: cdc7d1b4-15d7-4d4d-a13f-c7d3a694b4fb
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: 9c910905b51f2fe92e6e5d47d86a32bd5247c2cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-empty-edge-nodes-on-hadoop-clusters-in-hdinsight"></a>Usare i nodi perimetrali vuoti sui cluster Hadoop in HDInsight

Informazioni su come tooadd vuota bordo cluster HDInsight tooan di nodo. Un nodo del bordo vuoto è una macchina virtuale Linux con hello stessi strumenti client installato e configurato come headnodes hello, ma senza servizi Hadoop in esecuzione. È possibile utilizzare il nodo di edge hello per l'accesso a cluster hello, il testing delle applicazioni client e l'hosting di applicazioni client. 

Quando si crea il cluster hello, è possibile aggiungere un cluster HDInsight esistente di un bordo vuoto nodo tooan, tooa nuovo cluster. L'aggiunta di un nodo perimetrale vuoto si esegue usando un modello di Azure Resource Manager.  Hello seguente esempio viene illustrato come questa operazione viene eseguita utilizzando un modello:

    "resources": [
        {
            "name": "[concat(parameters('clusterName'),'/', variables('applicationName'))]",
            "type": "Microsoft.HDInsight/clusters/applications",
            "apiVersion": "2015-03-01-preview",
            "dependsOn": [ "[concat('Microsoft.HDInsight/clusters/',parameters('clusterName'))]" ],
            "properties": {
                "marketPlaceIdentifier": "EmptyNode",
                "computeProfile": {
                    "roles": [{
                        "name": "edgenode",
                        "targetInstanceCount": 1,
                        "hardwareProfile": {
                            "vmSize": "Standard_D3"
                        }
                    }]
                },
                "installScriptActions": [{
                    "name": "[concat('emptynode','-' ,uniquestring(variables('applicationName')))]",
                    "uri": "[parameters('installScriptAction')]",
                    "roles": ["edgenode"]
                }],
                "uninstallScriptActions": [],
                "httpsEndpoints": [],
                "applicationType": "CustomApplication"
            }
        }
    ],

Come illustrato nell'esempio hello, è possibile chiamare un [script azione](hdinsight-hadoop-customize-cluster-linux.md) tooperform un'ulteriore configurazione, ad esempio l'installazione [tonalità Apache](hdinsight-hadoop-hue-linux.md) nel nodo edge hello. script dell'azione script Hello deve essere accessibile pubblicamente in web hello.  Ad esempio, se lo script hello è archiviato in archiviazione di Azure, utilizzare contenitori pubblici o BLOB pubblici.

dimensioni della macchina virtuale nodo edge Hello devono soddisfare hello HDInsight cluster lavoro nodo vm dimensioni. Per hello consigliato lavoro dimensioni delle macchine virtuali di nodo, vedere [cluster creare Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).

Dopo aver creato un nodo del bordo, è possibile connettere il nodo di edge toohello tramite SSH ed eseguire client cluster di strumenti tooaccess hello Hadoop in HDInsight.

> [!WARNING] 
> L’utilizzo di un nodo perimetrale vuoto con HDInsight è attualmente in anteprima. I componenti personalizzati che vengono installati in nodo edge hello ricevano supporto commercialmente ragionevole da Microsoft. Ciò può portare alla risoluzione dei problemi riscontrati. Oppure è possibile che le risorse di cui viene fatto riferimento toocommunity per ulteriore assistenza. esempio Hello è riportate alcune hello la maggior parte dei siti attivi per il recupero della Guida dalla community di hello:
>
> * [Forum MSDN per HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)
> * [http://stackoverflow.com](http://stackoverflow.com).
>
> Se si utilizza una tecnologia di Apache, potrebbe essere in grado di toofind assistenza tramite hello siti del progetto di Apache nel [http://apache.org](http://apache.org), ad esempio hello [Hadoop](http://hadoop.apache.org/) sito.

## <a name="add-an-edge-node-tooan-existing-cluster"></a>Aggiungere un cluster esistente di nodo tooan bordo
In questa sezione, utilizzare un tooadd modello di gestione delle risorse cluster HDInsight esistente un bordo nodo tooan.  il modello di gestione risorse di Hello è reperibile [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/). il modello di gestione risorse di Hello chiama un'azione di script che si trova in https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh. script Hello non eseguire alcuna azione.  È toodemonstrate chiamata dell'azione di script da un modello di gestione risorse.

**tooadd un cluster esistente di nodo tooan bordo vuoto**

1. Creare un cluster HDInsight, se non ne è ancora disponibile uno.  Vedere [Esercitazione su Hadoop: introduzione all'uso di Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).
2. Fare clic su hello seguente immagine toosign in tooAzure e modello di gestione risorse di Azure aprire hello in hello portale di Azure. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-add-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. Configurare hello le proprietà seguenti:
   
   * **Sottoscrizione**: selezionare una sottoscrizione di Azure usata per la creazione di cluster hello.
   * **Gruppo di risorse**: gruppo di risorse selezionare hello utilizzato per il cluster HDInsight esistente hello.
   * **Percorso**: selezionare il percorso di hello del cluster HDInsight esistente hello.
   * **Nome del cluster**: immettere il nome di hello di un cluster HDInsight esistente.
   * **Bordo nodo dimensioni**: selezionare una delle dimensioni delle macchine Virtuali di hello. dimensioni della macchina virtuale Hello devono soddisfare hello lavoro nodo vm dimensioni. Per hello consigliato lavoro dimensioni delle macchine virtuali di nodo, vedere [cluster creare Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).
   * **Bordo nodo prefisso**: valore predefinito di hello è **nuova**.  Usa valore predefinito di hello, nome del nodo perimetrale hello è **nuova edgenode**.  È possibile personalizzare il prefisso hello dal portale hello. È anche possibile personalizzare nome completo di hello dal modello hello.

4. Controllare **accetto le condizioni indicate in precedenza toohello**, quindi fare clic su **acquisto** nodo di toocreate hello del bordo.

>[!IMPORTANT]
> Creare gruppo di risorse di Azure hello tooselect che per il cluster HDInsight esistente hello.  In caso contrario, viene visualizzato errore di hello messaggio "Impossibile eseguire l'operazione richiesta sulla risorsa annidata. La risorsa padre '&lt;NomeCluster>' non è stata trovata".

## <a name="add-an-edge-node-when-creating-a-cluster"></a>Aggiungere un nodo perimetrale durante la creazione di un cluster
In questa sezione, si utilizza un cluster di HDInsight toocreate di modello di gestione delle risorse con un nodo del bordo.  il modello di gestione risorse di Hello è reperibile in hello [raccolta di modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/). il modello di gestione risorse di Hello chiama un'azione di script che si trova in https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh. script Hello non eseguire alcuna azione.  È toodemonstrate chiamata dell'azione di script da un modello di gestione risorse.

**tooadd un cluster esistente di nodo tooan bordo vuoto**

1. Creare un cluster HDInsight, se non ne è ancora disponibile uno.  Vedere [Introduzione all'uso di Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).
2. Fare clic su hello seguente immagine toosign in tooAzure e modello di gestione risorse di Azure aprire hello in hello portale di Azure. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. Configurare hello le proprietà seguenti:
   
   * **Sottoscrizione**: selezionare una sottoscrizione di Azure usata per la creazione di cluster hello.
   * **Gruppo di risorse**: creare un nuovo gruppo di risorse utilizzato per il cluster di hello.
   * **Percorso**: selezionare un percorso per il gruppo di risorse hello.
   * **Nome del cluster**: immettere un nome per toocreate di hello nuovo cluster.
   * **Nome utente di accesso del cluster**: immettere nome utente di Hadoop HTTP hello.  nome predefinito Hello è **admin**.
   * **Password di account di accesso cluster**: immettere la password utente di Hadoop HTTP hello.
   * **SSH nome utente**: nome utente di hello SSH. nome predefinito Hello è **sshuser**.
   * **SSH Password**: immettere una password dell'utente SSH hello.
   * **Installare l'azione di Script**: mantenere il valore predefinito hello per passare attraverso questa esercitazione.
     
     Alcune proprietà sono stati impostati come hardcoded nel modello hello: tipo di Cluster, numero di nodi di lavoro del Cluster, la dimensione del nodo contorno e nome del nodo perimetrale.
4. Controllare **accetto le condizioni indicate in precedenza toohello**, quindi fare clic su **acquisto** cluster hello toocreate con nodo di hello del bordo.

## <a name="access-an-edge-node"></a>Accedere a un nodo perimetrale
nodo del bordo Hello ssh endpoint è &lt;EdgeNodeName >.&lt; Nome cluster >-ssh.azurehdinsight.net:22.  Ad esempio, new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.

nodo di Hello del bordo viene visualizzato come un'applicazione nel portale di Azure hello.  Consente di portale Hello hello hello tooaccess informazioni edge nodo utilizzando SSH.

**endpoint di tooverify hello edge nodo SSH**

1. Accesso toohello [portale di Azure](https://portal.azure.com).
2. Aprire il cluster di HDInsight hello con un nodo del bordo.
3. Fare clic su **applicazioni** dal pannello cluster hello. Verrà visualizzato il nodo di edge hello.  nome predefinito Hello è **nuova edgenode**.
4. Fare clic sul nodo di edge hello. Vedrai endpoint SSH hello.

**toouse Hive nel nodo edge hello**

1. Usare SSH tooconnect toohello bordo nodo. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Dopo aver connesso il nodo di edge toohello tramite SSH, utilizzare hello console di Hive hello tooopen dei comandi seguenti:
   
        hive
3. Eseguire hello le tabelle di Hive tooshow comando cluster hello seguenti:
   
        show tables;

## <a name="delete-an-edge-node"></a>Eliminare un nodo perimetrale
È possibile eliminare un nodo del bordo da hello portale di Azure.

**tooaccess un nodo del bordo**

1. Accesso toohello [portale di Azure](https://portal.azure.com).
2. Aprire il cluster di HDInsight hello con un nodo del bordo.
3. Fare clic su **applicazioni** dal pannello cluster hello. Verrà visualizzato un elenco di nodi perimetrali.  
4. Il nodo del bordo hello pulsante destro del mouse si desidera toodelete e quindi fare clic su **eliminare**.
5. Fare clic su **Sì** tooconfirm.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo, si è appreso come tooadd un nodo del bordo e come tooaccess hello nodo del bordo. toolearn informazioni, vedere hello seguenti articoli:

* [Installare le applicazioni di HDInsight](hdinsight-apps-install-applications.md): informazioni su come tooinstall un tooyour applicazione HDInsight cluster.
* [Installare le applicazioni personalizzate HDInsight](hdinsight-apps-install-custom-applications.md): informazioni su come toodeploy un tooHDInsight di applicazione non pubblicata di HDInsight.
* [Pubblicare applicazioni HDInsight](hdinsight-apps-publish-applications.md): informazioni su come toopublish il tooAzure di applicazioni personalizzate HDInsight Marketplace.
* [MSDN: Installare un'applicazione di HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): informazioni su come toodefine HDInsight applicazioni.
* [Personalizzazione dei cluster HDInsight basati su Linux con azione Script](hdinsight-hadoop-customize-cluster-linux.md): informazioni su come applicazioni aggiuntive di toouse genera Script azione tooinstall.
* [Creare i cluster basati su Linux, Hadoop in HDInsight mediante modelli di gestione risorse](hdinsight-hadoop-create-linux-clusters-arm-templates.md): informazioni su come toocreate modelli tramite Gestione risorse toocall HDInsight cluster.

