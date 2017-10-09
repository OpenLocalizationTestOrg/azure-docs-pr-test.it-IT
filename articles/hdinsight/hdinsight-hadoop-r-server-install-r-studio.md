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
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a><span data-ttu-id="7bf75-103">Installazione di RStudio con R Server su HDInsight</span><span class="sxs-lookup"><span data-stu-id="7bf75-103">Installing RStudio with R Server on HDInsight</span></span>

<span data-ttu-id="7bf75-104">In questo articolo viene descritto come tooinstall hello community (gratuito) versione [RStudio Server](https://www.rstudio.com/products/rstudio-server/) nel nodo di hello del bordo di un cluster utilizzando uno script personalizzato.</span><span class="sxs-lookup"><span data-stu-id="7bf75-104">This article describes how tooinstall hello community (free) version of [RStudio Server](https://www.rstudio.com/products/rstudio-server/) on hello edge node of a cluster using a custom script.</span></span> <span data-ttu-id="7bf75-105">RStudio Server offre un IDE basato sul browser per l'uso da parte di client remoti ed è ampiamente usato su Linux.</span><span class="sxs-lookup"><span data-stu-id="7bf75-105">RStudio Server provides a browser-based IDE for use by remote clients and is widely used on Linux.</span></span> <span data-ttu-id="7bf75-106">Ad oggi esistono più ambienti di sviluppo integrato (IDE) disponibili per R, tra cui:</span><span class="sxs-lookup"><span data-stu-id="7bf75-106">There are multiple integrated development environments (IDEs) available for R today, including:</span></span>

- <span data-ttu-id="7bf75-107">[R Tools per Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS) di Microsoft</span><span class="sxs-lookup"><span data-stu-id="7bf75-107">Microsoft’s  [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span></span> 
- [<span data-ttu-id="7bf75-108">RStudio Server</span><span class="sxs-lookup"><span data-stu-id="7bf75-108">RStudio Server</span></span>](https://www.rstudio.com/products/rstudio-server/) 
- <span data-ttu-id="7bf75-109">[StatET](http://www.walware.de/goto/statet), basato su Eclipse, di Walware.</span><span class="sxs-lookup"><span data-stu-id="7bf75-109">Walware’s Eclipse-based [StatET](http://www.walware.de/goto/statet).</span></span>

<span data-ttu-id="7bf75-110">Il vantaggio di Hello di installare RStudio Server nel nodo di hello del bordo di un cluster HDInsight è che fornisce un'esperienza IDE completa per lo sviluppo di hello e l'esecuzione di script R con R Server nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7bf75-110">hello advantage of installing RStudio Server on hello edge node of an HDInsight cluster is that it provides a full IDE experience for hello development and execution of R scripts with R Server on hello cluster.</span></span> <span data-ttu-id="7bf75-111">Questa configurazione può essere notevolmente più produttiva rispetto all'utilizzo della Console di R hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="7bf75-111">This configuration can be considerably more productive than default use of hello R Console.</span></span>

> [!NOTE]
> <span data-ttu-id="7bf75-112">procedura di Hello descritta in questo articolo è rilevante solo se non è stata selezionata tooinstall edizione community RStudio Server durante il provisioning del cluster.</span><span class="sxs-lookup"><span data-stu-id="7bf75-112">hello procedure described in this article is only relevant if you did not select tooinstall RStudio Server community edition when provisioning your cluster.</span></span> <span data-ttu-id="7bf75-113">Se è stato aggiunto durante il provisioning, quindi tooaccess si fa clic su hello **R Server dashboard** riquadro nella voce del portale di Azure per il cluster, quindi scegliere hello hello **R Studio Server** riquadro.</span><span class="sxs-lookup"><span data-stu-id="7bf75-113">If you added it during provisioning, then tooaccess it you click on hello **R Server Dashboards** tile in hello Azure portal entry for your cluster, then on hello **R Studio Server** tile.</span></span> 

<span data-ttu-id="7bf75-114">Se si preferisce toouse hello commercialmente con licenza Pro versione del RStudio Server, è necessario seguire le istruzioni di installazione hello da [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span><span class="sxs-lookup"><span data-stu-id="7bf75-114">If you prefer toouse hello commercially licensed Pro version of RStudio Server, you must follow hello installation instructions from [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span></span>

> [!NOTE]
> <span data-ttu-id="7bf75-115">Se si utilizza un cluster di HDInsight per cui R è stato installato utilizzando hello [installare R genera Script azione](hdinsight-hadoop-r-scripts-linux.md), passaggi hello in questo documento non funzionerà correttamente in quanto richiedono un Server R nel cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="7bf75-115">If you are using an HDInsight cluster for which R was installed using hello [Install R Script Action](hdinsight-hadoop-r-scripts-linux.md), hello steps in this document will not work correctly as they require an R Server on hello HDInsight cluster.</span></span>
>
> 

## <a name="prerequisites"></a><span data-ttu-id="7bf75-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7bf75-116">Prerequisites</span></span>

* <span data-ttu-id="7bf75-117">Un cluster Azure HDInsight con R Server</span><span class="sxs-lookup"><span data-stu-id="7bf75-117">An Azure HDInsight cluster with R Server installed.</span></span> <span data-ttu-id="7bf75-118">Per istruzioni, vedere [Introduzione all'uso di R Server in cluster HDInsight](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7bf75-118">For instructions, see [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md).</span></span>
* <span data-ttu-id="7bf75-119">Un client SSH.</span><span class="sxs-lookup"><span data-stu-id="7bf75-119">An SSH client.</span></span> <span data-ttu-id="7bf75-120">Per distribuzioni di Linux e Unix o Macintosh OS X, hello `ssh` comando viene fornito con sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="7bf75-120">For Linux and Unix distributions or Macintosh OS X, hello `ssh` command is provided with hello operating system.</span></span> <span data-ttu-id="7bf75-121">Per Windows, è consigliabile [Cygwin](http://www.redhat.com/services/custom/cygwin/) con hello [opzione OpenSSH](https://www.youtube.com/watch?v=CwYSvvGaiWU), o [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="7bf75-121">For Windows, we recommend [Cygwin](http://www.redhat.com/services/custom/cygwin/) with hello [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), or [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>  

## <a name="install-rstudio-on-hello-cluster-using-a-custom-script"></a><span data-ttu-id="7bf75-122">Installare RStudio nel cluster hello utilizzando uno script personalizzato</span><span class="sxs-lookup"><span data-stu-id="7bf75-122">Install RStudio on hello cluster using a custom script</span></span>

<span data-ttu-id="7bf75-123">Ecco i passaggi di hello:</span><span class="sxs-lookup"><span data-stu-id="7bf75-123">Here are hello steps:</span></span>

1. <span data-ttu-id="7bf75-124">Identificare nodo del cluster hello bordo hello.</span><span class="sxs-lookup"><span data-stu-id="7bf75-124">Identify hello edge node of hello cluster.</span></span> <span data-ttu-id="7bf75-125">Per un cluster di HDInsight con R Server, ecco convenzione di denominazione hello per il nodo head e bordo.</span><span class="sxs-lookup"><span data-stu-id="7bf75-125">For an HDInsight cluster with R Server, following is hello naming convention for head node and edge node.</span></span>
   * <span data-ttu-id="7bf75-126">Nodo head `CLUSTERNAME-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="7bf75-126">Head node `CLUSTERNAME-ssh.azurehdinsight.net`</span></span>
   * <span data-ttu-id="7bf75-127">Nodo perimetrale `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="7bf75-127">Edge node `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span></span> 

2. <span data-ttu-id="7bf75-128">SSH nel nodo del cluster di hello utilizzando il modello di denominazione hello fornito nel passaggio 1 bordo hello.</span><span class="sxs-lookup"><span data-stu-id="7bf75-128">SSH into hello edge node of hello cluster using hello naming pattern provided in step 1.</span></span> <span data-ttu-id="7bf75-129">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7bf75-129">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="7bf75-130">Una volta connessi, diventare un utente root nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7bf75-130">Once you are connected, become a root user on hello cluster.</span></span> <span data-ttu-id="7bf75-131">Nella sessione SSH hello, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7bf75-131">In hello SSH session, use hello following command:</span></span>

        sudo su -

4. <span data-ttu-id="7bf75-132">Scaricare uno script personalizzato di hello tooinstall RStudio.</span><span class="sxs-lookup"><span data-stu-id="7bf75-132">Download hello custom script tooinstall RStudio.</span></span> <span data-ttu-id="7bf75-133">Utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7bf75-133">Use hello following command:</span></span>

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. <span data-ttu-id="7bf75-134">Modificare le autorizzazioni di hello nel file di script personalizzato hello ed eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="7bf75-134">Change hello permissions on hello custom script file and run hello script.</span></span> <span data-ttu-id="7bf75-135">Utilizzare hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="7bf75-135">Use hello following commands:</span></span>

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. <span data-ttu-id="7bf75-136">Se una password SSH è stata utilizzata durante la creazione di un cluster HDInsight con R Server, è possibile ignorare questo passaggio e procedere toohello successivamente.</span><span class="sxs-lookup"><span data-stu-id="7bf75-136">If you used an SSH password while creating an HDInsight cluster with R Server, you can skip this step and proceed toohello next.</span></span> <span data-ttu-id="7bf75-137">Se invece si utilizza una chiave SSH cluster hello toocreate, è necessario impostare una password per l'utente SSH.</span><span class="sxs-lookup"><span data-stu-id="7bf75-137">If you used an SSH key instead toocreate hello cluster, you must set a password for your SSH user.</span></span> <span data-ttu-id="7bf75-138">È necessario specificare tale password quando ci si connette tooRStudio.</span><span class="sxs-lookup"><span data-stu-id="7bf75-138">You need this password when connecting tooRStudio.</span></span> <span data-ttu-id="7bf75-139">Eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="7bf75-139">Run hello following commands:</span></span>

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. <span data-ttu-id="7bf75-140">Quando viene richiesto di immettere la **password Kerberos corrente**, premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="7bf75-140">When prompted for **Current Kerberos password**, press **ENTER**.</span></span>  <span data-ttu-id="7bf75-141">Si noti che è necessario sostituire `USERNAME` con un utente SSH per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7bf75-141">Note that you must replace `USERNAME` with an SSH user for your HDInsight cluster.</span></span> <span data-ttu-id="7bf75-142">Se la password è impostata correttamente, verrà visualizzato hello seguente messaggio:</span><span class="sxs-lookup"><span data-stu-id="7bf75-142">If your password is successfully set, you should see hello following message:</span></span>

        passwd: password updated successfully

    <span data-ttu-id="7bf75-143">Uscire dalla sessione SSH hello.</span><span class="sxs-lookup"><span data-stu-id="7bf75-143">Exit hello SSH session.</span></span>

8. <span data-ttu-id="7bf75-144">Creare un cluster di toohello tunnel SSH eseguendo il mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` sul hello HDInsight cluster computer client toohello.</span><span class="sxs-lookup"><span data-stu-id="7bf75-144">Create an SSH tunnel toohello cluster by mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` on hello HDInsight cluster toohello client machine.</span></span> <span data-ttu-id="7bf75-145">Prima di aprire una nuova sessione del browser, è necessario creare un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="7bf75-145">You must create an SSH tunnel before opening a new browser session.</span></span>

   * <span data-ttu-id="7bf75-146">In un client Linux o in un client Windows con [Cygwin](http://www.redhat.com/services/custom/cygwin/), aprire una sessione terminal e utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7bf75-146">On a Linux client or a Windows client with [Cygwin](http://www.redhat.com/services/custom/cygwin/), open a terminal session and use hello following command:</span></span>

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       <span data-ttu-id="7bf75-147">Sostituire **USERNAME** con un utente SSH per il cluster HDInsight e sostituire **CLUSTERNAME** con nome hello del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7bf75-147">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>
       <span data-ttu-id="7bf75-148">È possibile anche usare una chiave SSH anziché una password mediante l'aggiunta di `-i id_rsa_key`.</span><span class="sxs-lookup"><span data-stu-id="7bf75-148">You can also use an SSH key rather than a password by adding `-i id_rsa_key`.</span></span>        
   * <span data-ttu-id="7bf75-149">Se si utilizza un client Windows con PuTTY:</span><span class="sxs-lookup"><span data-stu-id="7bf75-149">If using a Windows client with PuTTY then</span></span>

     1. <span data-ttu-id="7bf75-150">Aprire PuTTY e immettere le informazioni di connessione.</span><span class="sxs-lookup"><span data-stu-id="7bf75-150">Open PuTTY, and enter your connection information.</span></span>
     2. <span data-ttu-id="7bf75-151">In hello **categoria** toohello sezione a sinistra della finestra di dialogo hello, espandere **connessione**, espandere **SSH**, quindi selezionare **tunnel**.</span><span class="sxs-lookup"><span data-stu-id="7bf75-151">In hello **Category** section toohello left of hello dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>
     3. <span data-ttu-id="7bf75-152">Fornire le seguenti informazioni su hello hello **opzioni che controllano SSH inoltro alla porta** form:</span><span class="sxs-lookup"><span data-stu-id="7bf75-152">Provide hello following information on hello **Options controlling SSH port forwarding** form:</span></span>

        * <span data-ttu-id="7bf75-153">**Porta di origine** -hello porta sul client hello che si desidera tooforward.</span><span class="sxs-lookup"><span data-stu-id="7bf75-153">**Source port** - hello port on hello client that you wish tooforward.</span></span> <span data-ttu-id="7bf75-154">Ad esempio **8787**.</span><span class="sxs-lookup"><span data-stu-id="7bf75-154">For example, **8787**.</span></span>
        * <span data-ttu-id="7bf75-155">**Destinazione** : hello destinazione che deve essere eseguito il mapping di computer client locale toohello.</span><span class="sxs-lookup"><span data-stu-id="7bf75-155">**Destination** - hello destination that must be mapped toohello local client machine.</span></span> <span data-ttu-id="7bf75-156">Ad esempio **localhost:8787**.</span><span class="sxs-lookup"><span data-stu-id="7bf75-156">For example, **localhost:8787**.</span></span>

            <span data-ttu-id="7bf75-157">![Creare un tunnel SSH](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Creare un tunnel SSH")</span><span class="sxs-lookup"><span data-stu-id="7bf75-157">![Create an SSH tunnel](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Create an SSH tunnel")</span></span>

     4. <span data-ttu-id="7bf75-158">Fare clic su **Aggiungi** tooadd hello impostazioni e quindi fare clic su **aprire** tooopen una connessione SSH.</span><span class="sxs-lookup"><span data-stu-id="7bf75-158">Click **Add** tooadd hello settings, and then click **Open** tooopen an SSH connection.</span></span>
     5. <span data-ttu-id="7bf75-159">Quando richiesto, accedere toohello server tooestablish un tunnel SSH sessione e abilitare hello.</span><span class="sxs-lookup"><span data-stu-id="7bf75-159">When prompted, log in toohello server tooestablish an SSH session and enable hello tunnel.</span></span>

9. <span data-ttu-id="7bf75-160">Aprire un web browser e immettere l'URL basato su porta hello che immesso per il tunnel hello seguente hello:</span><span class="sxs-lookup"><span data-stu-id="7bf75-160">Open a web browser and enter hello following URL based on hello port you entered for hello tunnel:</span></span>

        http://localhost:8787/ 

10. <span data-ttu-id="7bf75-161">Si è richiesta tooenter hello SSH nome utente e password tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="7bf75-161">You are prompted tooenter hello SSH username and password tooconnect toohello cluster.</span></span> <span data-ttu-id="7bf75-162">Se una chiave SSH è stata utilizzata durante la creazione di cluster hello, è necessario immettere la password di hello creato nel passaggio 5.</span><span class="sxs-lookup"><span data-stu-id="7bf75-162">If you used an SSH key while creating hello cluster, you must enter hello password you created in step 5.</span></span>

    <span data-ttu-id="7bf75-163">![Connettersi tooR Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "creare un tunnel SSH")</span><span class="sxs-lookup"><span data-stu-id="7bf75-163">![Connect tooR Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Create an SSH tunnel")</span></span>

11. <span data-ttu-id="7bf75-164">tootest se hello RStudio installazione ha avuto esito positivo, è possibile eseguire uno script di test che esegue i processi MapReduce e Spark basati su R sul cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7bf75-164">tootest whether hello RStudio installation was successful, you can run a test script that executes R-based MapReduce and Spark jobs on hello cluster.</span></span> <span data-ttu-id="7bf75-165">toodownload hello test script toorun in RStudio, tornare indietro toohello SSH console e immettere hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="7bf75-165">toodownload hello test script toorun in RStudio, go back toohello SSH console and enter hello following commands:</span></span>

    *    <span data-ttu-id="7bf75-166">Se è stato creato un cluster Hadoop con R, usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="7bf75-166">If you created a Hadoop cluster with R, use this command:</span></span>

            <span data-ttu-id="7bf75-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span><span class="sxs-lookup"><span data-stu-id="7bf75-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span></span>
    *    <span data-ttu-id="7bf75-168">Se è stato creato un cluster Spark con R, usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="7bf75-168">If you created a Spark cluster with R, use this command:</span></span>

            <span data-ttu-id="7bf75-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span><span class="sxs-lookup"><span data-stu-id="7bf75-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span></span>

12. <span data-ttu-id="7bf75-170">In RStudio, vedrai hello è stato scaricato lo script di test.</span><span class="sxs-lookup"><span data-stu-id="7bf75-170">In RStudio, you see hello test script you downloaded.</span></span> <span data-ttu-id="7bf75-171">Fare doppio clic su hello tooopen di file, selezionare il contenuto di hello del file hello e quindi fare clic su **eseguire**.</span><span class="sxs-lookup"><span data-stu-id="7bf75-171">Double-click hello file tooopen it, select hello contents of hello file, and then click **Run**.</span></span> <span data-ttu-id="7bf75-172">Verrà visualizzato l'output di hello in hello **Console** riquadro:</span><span class="sxs-lookup"><span data-stu-id="7bf75-172">You should see hello output in hello **Console** pane:</span></span>

   <span data-ttu-id="7bf75-173">![Testare l'installazione di hello](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "installazione hello di Test")</span><span class="sxs-lookup"><span data-stu-id="7bf75-173">![Test hello installation](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test hello installation")</span></span>

<span data-ttu-id="7bf75-174">Un'altra opzione sarebbe tootype `source(testhdi.r)` o `source(testhdi_spark.r)` script hello tooexecute.</span><span class="sxs-lookup"><span data-stu-id="7bf75-174">Another option would be tootype `source(testhdi.r)` or `source(testhdi_spark.r)` tooexecute hello script.</span></span>

## <a name="see-also"></a><span data-ttu-id="7bf75-175">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7bf75-175">See also</span></span>

* [<span data-ttu-id="7bf75-176">Opzioni del contesto di calcolo per R Server in cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="7bf75-176">Compute context options for R Server on HDInsight clusters</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="7bf75-177">Opzioni di Archiviazione di Azure per R Server su HDInsight</span><span class="sxs-lookup"><span data-stu-id="7bf75-177">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)

