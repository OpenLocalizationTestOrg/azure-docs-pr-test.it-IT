---
title: aaaInstall RStudio con R Server in HDInsight - Azure | Documenti Microsoft
description: Come tooinstall RStudio con R Server in HDInsight.
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 918abb0d-8248-4bc5-98dc-089c0e007d49
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: b3a23021fcf99217e8f551f8b2e89bf1f1e5b967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a>Installazione di RStudio con R Server su HDInsight

In questo articolo viene descritto come tooinstall hello community (gratuito) versione [RStudio Server](https://www.rstudio.com/products/rstudio-server/) nel nodo di hello del bordo di un cluster utilizzando uno script personalizzato. RStudio Server offre un IDE basato sul browser per l'uso da parte di client remoti ed è ampiamente usato su Linux. Ad oggi esistono più ambienti di sviluppo integrato (IDE) disponibili per R, tra cui:

- [R Tools per Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS) di Microsoft 
- [RStudio Server](https://www.rstudio.com/products/rstudio-server/) 
- [StatET](http://www.walware.de/goto/statet), basato su Eclipse, di Walware.

Il vantaggio di Hello di installare RStudio Server nel nodo di hello del bordo di un cluster HDInsight è che fornisce un'esperienza IDE completa per lo sviluppo di hello e l'esecuzione di script R con R Server nel cluster hello. Questa configurazione può essere notevolmente più produttiva rispetto all'utilizzo della Console di R hello predefinito.

> [!NOTE]
> procedura di Hello descritta in questo articolo è rilevante solo se non è stata selezionata tooinstall edizione community RStudio Server durante il provisioning del cluster. Se è stato aggiunto durante il provisioning, quindi tooaccess si fa clic su hello **R Server dashboard** riquadro nella voce del portale di Azure per il cluster, quindi scegliere hello hello **R Studio Server** riquadro. 

Se si preferisce toouse hello commercialmente con licenza Pro versione del RStudio Server, è necessario seguire le istruzioni di installazione hello da [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).

> [!NOTE]
> Se si utilizza un cluster di HDInsight per cui R è stato installato utilizzando hello [installare R genera Script azione](hdinsight-hadoop-r-scripts-linux.md), passaggi hello in questo documento non funzionerà correttamente in quanto richiedono un Server R nel cluster HDInsight hello.
>
> 

## <a name="prerequisites"></a>Prerequisiti

* Un cluster Azure HDInsight con R Server Per istruzioni, vedere [Introduzione all'uso di R Server in cluster HDInsight](hdinsight-hadoop-r-server-get-started.md).
* Un client SSH. Per distribuzioni di Linux e Unix o Macintosh OS X, hello `ssh` comando viene fornito con sistema operativo hello. Per Windows, è consigliabile [Cygwin](http://www.redhat.com/services/custom/cygwin/) con hello [opzione OpenSSH](https://www.youtube.com/watch?v=CwYSvvGaiWU), o [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).  

## <a name="install-rstudio-on-hello-cluster-using-a-custom-script"></a>Installare RStudio nel cluster hello utilizzando uno script personalizzato

Ecco i passaggi di hello:

1. Identificare nodo del cluster hello bordo hello. Per un cluster di HDInsight con R Server, ecco convenzione di denominazione hello per il nodo head e bordo.
   * Nodo head `CLUSTERNAME-ssh.azurehdinsight.net`
   * Nodo perimetrale `CLUSTERNAME-ed-ssh.azurehdinsight.net` 

2. SSH nel nodo del cluster di hello utilizzando il modello di denominazione hello fornito nel passaggio 1 bordo hello. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Una volta connessi, diventare un utente root nel cluster hello. Nella sessione SSH hello, utilizzare hello comando seguente:

        sudo su -

4. Scaricare uno script personalizzato di hello tooinstall RStudio. Utilizzare hello comando seguente:

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. Modificare le autorizzazioni di hello nel file di script personalizzato hello ed eseguire script hello. Utilizzare hello seguenti comandi:

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. Se una password SSH è stata utilizzata durante la creazione di un cluster HDInsight con R Server, è possibile ignorare questo passaggio e procedere toohello successivamente. Se invece si utilizza una chiave SSH cluster hello toocreate, è necessario impostare una password per l'utente SSH. È necessario specificare tale password quando ci si connette tooRStudio. Eseguire hello seguenti comandi:

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. Quando viene richiesto di immettere la **password Kerberos corrente**, premere **INVIO**.  Si noti che è necessario sostituire `USERNAME` con un utente SSH per il cluster HDInsight. Se la password è impostata correttamente, verrà visualizzato hello seguente messaggio:

        passwd: password updated successfully

    Uscire dalla sessione SSH hello.

8. Creare un cluster di toohello tunnel SSH eseguendo il mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` sul hello HDInsight cluster computer client toohello. Prima di aprire una nuova sessione del browser, è necessario creare un tunnel SSH.

   * In un client Linux o in un client Windows con [Cygwin](http://www.redhat.com/services/custom/cygwin/), aprire una sessione terminal e utilizzare hello comando seguente:

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       Sostituire **USERNAME** con un utente SSH per il cluster HDInsight e sostituire **CLUSTERNAME** con nome hello del cluster HDInsight.
       È possibile anche usare una chiave SSH anziché una password mediante l'aggiunta di `-i id_rsa_key`.        
   * Se si utilizza un client Windows con PuTTY:

     1. Aprire PuTTY e immettere le informazioni di connessione.
     2. In hello **categoria** toohello sezione a sinistra della finestra di dialogo hello, espandere **connessione**, espandere **SSH**, quindi selezionare **tunnel**.
     3. Fornire le seguenti informazioni su hello hello **opzioni che controllano SSH inoltro alla porta** form:

        * **Porta di origine** -hello porta sul client hello che si desidera tooforward. Ad esempio **8787**.
        * **Destinazione** : hello destinazione che deve essere eseguito il mapping di computer client locale toohello. Ad esempio **localhost:8787**.

            ![Creare un tunnel SSH](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Creare un tunnel SSH")

     4. Fare clic su **Aggiungi** tooadd hello impostazioni e quindi fare clic su **aprire** tooopen una connessione SSH.
     5. Quando richiesto, accedere toohello server tooestablish un tunnel SSH sessione e abilitare hello.

9. Aprire un web browser e immettere l'URL basato su porta hello che immesso per il tunnel hello seguente hello:

        http://localhost:8787/ 

10. Si è richiesta tooenter hello SSH nome utente e password tooconnect toohello cluster. Se una chiave SSH è stata utilizzata durante la creazione di cluster hello, è necessario immettere la password di hello creato nel passaggio 5.

    ![Connettersi tooR Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "creare un tunnel SSH")

11. tootest se hello RStudio installazione ha avuto esito positivo, è possibile eseguire uno script di test che esegue i processi MapReduce e Spark basati su R sul cluster hello. toodownload hello test script toorun in RStudio, tornare indietro toohello SSH console e immettere hello seguenti comandi:

    *    Se è stato creato un cluster Hadoop con R, usare questo comando:

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r
    *    Se è stato creato un cluster Spark con R, usare questo comando:

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r

12. In RStudio, vedrai hello è stato scaricato lo script di test. Fare doppio clic su hello tooopen di file, selezionare il contenuto di hello del file hello e quindi fare clic su **eseguire**. Verrà visualizzato l'output di hello in hello **Console** riquadro:

   ![Testare l'installazione di hello](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "installazione hello di Test")

Un'altra opzione sarebbe tootype `source(testhdi.r)` o `source(testhdi_spark.r)` script hello tooexecute.

## <a name="see-also"></a>Vedere anche

* [Opzioni del contesto di calcolo per R Server in cluster HDInsight](hdinsight-hadoop-r-server-compute-contexts.md)
* [Opzioni di Archiviazione di Azure per R Server su HDInsight](hdinsight-hadoop-r-server-storage.md)

