---
title: aaaInstall Hadoop applicazioni personalizzate in Azure HDInsight | Documenti Microsoft
description: Informazioni su come applicazioni di HDInsight tooinstall in applicazioni di HDInsight.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e556b29c-8176-4bc5-a90b-aa01abfd3aee
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ed3148f2c4d4d2b568d84e44fa6d76bb5a001902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-custom-hadoop-applications-on-azure-hdinsight"></a>Installare applicazioni Hadoop personalizzate in Azure HDInsight

In questo articolo si apprenderà come tooinstall un'applicazione di Hadoop in HDInsight di Azure, non è stato pubblicato toohello portale di Azure. un'applicazione Hello verrà installato in questo articolo è [tonalità](http://gethue.com/).

Un'applicazione HDInsight è un'applicazione che gli utenti possono installare in un cluster HDInsight basato su Linux.  Queste applicazioni possono essere sviluppate da Microsoft, da fornitori di software indipendenti (ISV) o dall'utente.  

Altri articoli correlati:

* [Installare le applicazioni di HDInsight](hdinsight-apps-install-applications.md): informazioni su come tooinstall un tooyour applicazione HDInsight cluster.
* [Pubblicare applicazioni HDInsight](hdinsight-apps-publish-applications.md): informazioni su come toopublish il tooAzure di applicazioni personalizzate HDInsight Marketplace.
* [MSDN: Installare un'applicazione di HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): informazioni su come toodefine HDInsight applicazioni.

## <a name="prerequisites"></a>Prerequisiti
Se si desidera tooinstall HDInsight applicazioni su un cluster HDInsight esistente, è necessario disporre di un cluster HDInsight. toocreate uno, vedere [creare cluster](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). È anche possibile installare applicazioni HDInsight quando si crea un cluster HDInsight.

## <a name="install-hdinsight-applications"></a>Installare applicazioni HDInsight
Applicazioni di HDInsight possono essere installate quando si crea un cluster o cluster HDInsight esistente tooan. Per definire i modelli di Azure Resource Manager, vedere [MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx)(MSDN: Installare un'applicazione HDInsight).

file Hello necessari per la distribuzione dell'applicazione (tonalità):

* [azuredeploy.JSON](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/azuredeploy.json): modello di gestione risorse di hello per l'installazione dell'applicazione di HDInsight. Per sviluppare il proprio modello di Azure Resource Manager, vedere [MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx) (MSDN: Installare un'applicazione HDInsight).
* [tonalità install_v0.sh](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/scripts/Hue-install_v0.sh): hello genera Script azione richiamata dal modello di gestione risorse di hello per la configurazione del nodo di hello del bordo.
* [tonalità binaries.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): il file binario di hello tonalità chiamato da hui install_v0.sh.
* [tonalità-file binari di-14-04.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): il file binario di hello tonalità chiamato da hui install_v0.sh.
* [webwasb-tomcat.tar.gz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/webwasb-tomcat.tar.gz): applicazione Web di esempio (Tomcat) chiamata da hui-install_v0.sh.

**cluster HDInsight esistente di tooinstall tonalità tooan**

1. Fare clic su hello seguente immagine toosign in tooAzure e il modello di gestione risorse hello Apri nel portale di Azure hello.

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2FIaas-Applications%2Fmaster%2FHue%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    Apre un modello di gestione delle risorse nel portale di Azure hello.  Hello modello Resource Manager si trova in [https://github.com/hdinsight/Iaas-Applications/tree/master/Hue](https://github.com/hdinsight/Iaas-Applications/tree/master/Hue).  toolearn come toowrite questo modello di gestione delle risorse, vedere [MSDN: installare un'applicazione di HDInsight](https://msdn.microsoft.com/library/mt706515.aspx).
2. Da hello **parametri** pannello immettere hello seguenti:

   * **ClusterName**: immettere il nome di hello del cluster di hello in cui si desidera un'applicazione hello tooinstall. Deve essere un cluster esistente.
3. Fare clic su **OK** parametri hello toosave.
4. Da hello **distribuzione personalizzata** pannello immettere **gruppo di risorse**.  gruppo di risorse Hello è un contenitore che raggruppa cluster hello, account di archiviazione dipendenti hello e altre risorse. È necessario toouse hello stesso gruppo di risorse cluster hello.
5. Fare clic su **Note legali** e quindi su **Crea**.
6. Verificare hello **Pin toodashboard** casella di controllo è selezionata e quindi fare clic su **crea**. È possibile visualizzare lo stato di installazione hello dal dashboard del portale toohello bloccati hello riquadro e notifica tramite il portale hello (fare clic sull'icona di campanello hello nella parte superiore di hello del portale hello).  Accetta un'applicazione hello tooinstall circa 10 minuti.

**tooinstall tonalità durante la creazione di un cluster**

1. Fare clic su hello seguente immagine toosign in tooAzure e il modello di gestione risorse hello Apri nel portale di Azure hello.

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhdinsightapps%2Fcreate-linux-based-hadoop-cluster-in-hdinsight.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    Apre un modello di gestione delle risorse nel portale di Azure hello.  Hello modello Resource Manager si trova in [https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json](https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json).  toolearn come toowrite questo modello di gestione delle risorse, vedere [MSDN: installare un'applicazione di HDInsight](https://msdn.microsoft.com/library/mt706515.aspx).
2. Installare tonalità segue hello istruzione toocreate cluster. Per altre informazioni sulla creazione di cluster HDInsight, vedere [Creare cluster Hadoop basati su Linux in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

Inoltre toohello portale di Azure, è inoltre possibile utilizzare [Azure PowerShell](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-powershell) e [CLI di Azure](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-cli) toocall modelli di gestione risorse.

## <a name="validate-hello-installation"></a>Convalidare l'installazione di hello
È possibile controllare lo stato dell'applicazione hello in hello installazione dell'applicazione hello toovalidate portale Azure. Inoltre, è inoltre possibile convalidare tutti fornito di endpoint HTTP backup come previsto e delle pagine Web hello se è presente:

**portale di tonalità hello tooopen**

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **cluster HDInsight** nel menu a sinistra di hello.  Se non è visualizzato, fare clic su **Esplora** e quindi su **Cluster HDInsight**.
3. Fare clic su cluster hello in cui è installata un'applicazione hello.
4. Da hello **impostazioni** pannello, fare clic su **applicazioni** in hello **generale** categoria. Verrà visualizzata **tonalità** elencati in hello **App installate** blade.
5. Fare clic su **tonalità** dalle proprietà di hello elenco toolist hello.  
6. Fare clic su hello pagina Web collegamento toovalidate hello del sito Web; Aprire l'endpoint HTTP hello in un browser toovalidate hello tonalità interfaccia utente web, endpoint SSH hello aperto tramite SSH. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="troubleshoot-hello-installation"></a>Risoluzione dei problemi di installazione di hello
È possibile controllare lo stato di installazione applicazione hello dalla notifica tramite il portale hello (fare clic sull'icona di campanello hello nella parte superiore di hello del portale hello).

Se l'installazione di un'applicazione non riuscita, è possibile vedere i messaggi di errore hello e informazioni di 3 posizioni di debug:

* Applicazioni HDInsight: informazioni generali sull'errore.

    Aprire il cluster hello dal portale di hello e fare clic su applicazioni dal pannello impostazioni hello:

    ![applicazioni HDInsight errore di installazione dell'applicazione](./media/hdinsight-apps-install-applications/hdinsight-apps-error.png)
* HDInsight genera script azione: se il messaggio di errore hello HDInsight applicazioni indica un errore di azione di script, verranno visualizzati nel riquadro azioni di script hello maggiori dettagli sull'errore di script hello.

    Fare clic su Genera Script azione dal pannello impostazioni hello. Cronologia dell'azione script Mostra messaggi di errore hello

    ![applicazioni HDInsight errore di azione script](./media/hdinsight-apps-install-applications/hdinsight-apps-script-action-error.png)
* Ambari Web dell'interfaccia utente: Se uno script di installazione di hello causa hello dell'errore di hello, utilizzare i log completi dell'interfaccia utente Web Ambari toocheck sugli script di installazione di hello.

    Per altre informazioni, vedere [Risoluzione dei problemi](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting).

## <a name="remove-hdinsight-applications"></a>Rimuovere applicazioni HDInsight
Esistono diversi modi toodelete HDInsight applicazioni.

### <a name="use-portal"></a>Usare il portale
**tooremove un'applicazione tramite il portale di hello**

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **cluster HDInsight** nel menu a sinistra di hello.  Se non è visualizzato, fare clic su **Esplora** e quindi su **Cluster HDInsight**.
3. Fare clic su cluster hello in cui è installata un'applicazione hello.
4. Da hello **impostazioni** pannello, fare clic su **applicazioni** in hello **generale** categoria. Verrà visualizzato un elenco di applicazioni installate. Per questa esercitazione, **tonalità** elencati in hello **App installate** blade.
5. Fare doppio clic su un'applicazione hello desidera tooremove e quindi fare clic su **eliminare**.
6. Fare clic su **Sì** tooconfirm.

Dal portale di hello, è possibile anche eliminare cluster hello o gruppo di risorse hello che contiene l'applicazione hello.

### <a name="use-azure-powershell"></a>Uso di Azure PowerShell
Con Azure PowerShell, è possibile eliminare il cluster hello o eliminare il gruppo di risorse hello. Vedere [Eliminare cluster usando Azure PowerShell](hdinsight-administer-use-powershell.md#delete-clusters).

### <a name="use-azure-cli"></a>Utilizzare l'interfaccia della riga di comando di Azure
Usando l'interfaccia CLI di Azure, è possibile eliminare il cluster hello o eliminare il gruppo di risorse hello. Vedere [Eliminare cluster usando l'interfaccia della riga di comando di Azure](hdinsight-administer-use-command-line.md#delete-clusters).

## <a name="next-steps"></a>Passaggi successivi
* [MSDN: Installare un'applicazione di HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): informazioni su come toodevelop i modelli di gestione risorse per la distribuzione di applicazioni di HDInsight.
* [Installare le applicazioni di HDInsight](hdinsight-apps-install-applications.md): informazioni su come tooinstall un tooyour applicazione HDInsight cluster.
* [Pubblicare applicazioni HDInsight](hdinsight-apps-publish-applications.md): informazioni su come toopublish il tooAzure di applicazioni personalizzate HDInsight Marketplace.
* [Personalizzazione dei cluster HDInsight basati su Linux con azione Script](hdinsight-hadoop-customize-cluster-linux.md): informazioni su come applicazioni aggiuntive di toouse genera Script azione tooinstall.
* [Creare i cluster basati su Linux, Hadoop in HDInsight mediante modelli di gestione risorse](hdinsight-hadoop-create-linux-clusters-arm-templates.md): informazioni su come toocreate modelli tramite Gestione risorse toocall HDInsight cluster.
* [Usare i nodi del bordo vuoto in HDInsight](hdinsight-apps-use-edge-node.md): informazioni su come toouse vuota bordo nodo per l'accesso a cluster HDInsight, testing delle applicazioni di HDInsight e hosting di applicazioni di HDInsight.
