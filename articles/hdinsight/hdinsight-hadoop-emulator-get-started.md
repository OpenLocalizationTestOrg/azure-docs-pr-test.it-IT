---
title: utilizzando una sandbox di Hadoop - emulator - Azure HDInsight aaaLearn | Documenti Microsoft
description: "toostart sull'utilizzo di apprendimento salve ecosistema di Hadoop, è possibile impostare un ambiente sandbox Hadoop da Hortonworks in una macchina virtuale di Azure. "
keywords: emulatore hadoop, sandbox hadoop
editor: cgronlun
manager: jhubbard
services: hdinsight
author: nitinme
documentationcenter: 
tags: azure-portal
ms.assetid: 6ad5bb58-8215-4e3d-a07f-07fcd8839cc6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 91e74f0823fd02e9bb812155a7d09357a77b0736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a><span data-ttu-id="67cbd-104">Introduzione a una sandbox di Hadoop, un emulatore in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="67cbd-104">Get started with a Hadoop sandbox, an emulator on a virtual machine</span></span>

<span data-ttu-id="67cbd-105">Informazioni su come tooinstall hello sandbox Hadoop da Hortonworks in una macchina virtuale di toolearn sull'ecosistema di Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="67cbd-105">Learn how tooinstall hello Hadoop sandbox from Hortonworks on a virtual machine toolearn about hello Hadoop ecosystem.</span></span> <span data-ttu-id="67cbd-106">sandbox Hello fornisce un toolearn ambiente di sviluppo locale su Hadoop, Hadoop Distributed File System (HDFS) e l'invio di processi.</span><span class="sxs-lookup"><span data-stu-id="67cbd-106">hello sandbox provides a local development environment toolearn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span></span> <span data-ttu-id="67cbd-107">Dopo aver acquisito familiarità con Hadoop è possibile iniziare a usare Hadoop in Azure creando un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="67cbd-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span></span> <span data-ttu-id="67cbd-108">Per ulteriori informazioni sulla modalità di avvio tooget, vedere [introduzione Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="67cbd-108">For more information on how tooget started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67cbd-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="67cbd-109">Prerequisites</span></span>
* <span data-ttu-id="67cbd-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span><span class="sxs-lookup"><span data-stu-id="67cbd-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span></span> <span data-ttu-id="67cbd-111">Scaricare e installare l'app da [qui](https://www.virtualbox.org/wiki/Downloads).</span><span class="sxs-lookup"><span data-stu-id="67cbd-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span></span>



## <a name="download-and-install-hello-virtual-machine"></a><span data-ttu-id="67cbd-112">Scaricare e installare una macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="67cbd-112">Download and install hello virtual machine</span></span>
1. <span data-ttu-id="67cbd-113">Sfoglia toohello [Hortonworks Scarica](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="67cbd-113">Browse toohello [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span></span>

2. <span data-ttu-id="67cbd-114">Fare clic su **scaricare per VIRTUALBOX** toodownload hello Hortonworks Sandbox più recenti in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="67cbd-114">Click **DOWNLOAD FOR VIRTUALBOX** toodownload hello latest Hortonworks Sandbox on a VM.</span></span> <span data-ttu-id="67cbd-115">Si è richiesta tooregister con Hortonworks prima di iniziare il download di hello.</span><span class="sxs-lookup"><span data-stu-id="67cbd-115">You are prompted tooregister with Hortonworks before hello download begins.</span></span> <span data-ttu-id="67cbd-116">Accetta una toodownload di ore tootwo a seconda della velocità di rete.</span><span class="sxs-lookup"><span data-stu-id="67cbd-116">It takes one tootwo hours toodownload depending on your network speed.</span></span>
   
    ![Immagine di collegamento per scaricare Sandbox di Hortonworks per VirtualBox](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. <span data-ttu-id="67cbd-118">Da hello stessa pagina web, fare clic su hello **importazione su Virtual Box** collegamento toodownload un file PDF che contiene le istruzioni di installazione per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="67cbd-118">From hello same web page, click hello **Import on Virtual Box** link toodownload a PDF containing installation instructions for hello virtual machine.</span></span>

<span data-ttu-id="67cbd-119">toodownload un sandbox di versione HDP precedente, espandere l'archivio hello:</span><span class="sxs-lookup"><span data-stu-id="67cbd-119">toodownload an older HDP version sandbox, expand hello archive:</span></span>

![Archivio Hortonworks Sandbox](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-hello-virtual-machine"></a><span data-ttu-id="67cbd-121">Avviare la macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="67cbd-121">Start hello virtual machine</span></span>

1. <span data-ttu-id="67cbd-122">Aprire Oracle VM VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="67cbd-122">Open Oracle VM VirtualBox.</span></span>
2. <span data-ttu-id="67cbd-123">Da hello **File** menu, fare clic su **dello strumento di importazione**, quindi specificare hello immagine Hortonworks Sandbox.</span><span class="sxs-lookup"><span data-stu-id="67cbd-123">From hello **File** menu, click **Import Appliance**, and then specify hello Hortonworks Sandbox image.</span></span>
1. <span data-ttu-id="67cbd-124">Fare clic su Hortonworks Sandbox, seleziona hello **avviare**e quindi **normale avviare**.</span><span class="sxs-lookup"><span data-stu-id="67cbd-124">Select hello Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span></span> <span data-ttu-id="67cbd-125">Al termine il processo di avvio hello macchina virtuale hello, Visualizza le istruzioni di account di accesso.</span><span class="sxs-lookup"><span data-stu-id="67cbd-125">Once hello virtual machine has finished hello boot process, it displays login instructions.</span></span>
   
    ![Avvio normale](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. <span data-ttu-id="67cbd-127">Aprire un web browser e passare l'URL toohello visualizzato (in genere http://127.0.0.1:8888).</span><span class="sxs-lookup"><span data-stu-id="67cbd-127">Open a web browser and navigate toohello URL displayed (usually http://127.0.0.1:8888).</span></span>

## <a name="set-sandbox-passwords"></a><span data-ttu-id="67cbd-128">Impostare le password Sandbox</span><span class="sxs-lookup"><span data-stu-id="67cbd-128">Set Sandbox passwords</span></span>

1. <span data-ttu-id="67cbd-129">Da hello **iniziare** passaggio di hello pagina Hortonworks Sandbox, selezionare **opzioni avanzate vista**.</span><span class="sxs-lookup"><span data-stu-id="67cbd-129">From hello **get started** step of hello Hortonworks Sandbox page, select **View Advanced Options**.</span></span> <span data-ttu-id="67cbd-130">Utilizzare le informazioni di hello in toolog questa pagina in sandbox toohello tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="67cbd-130">Use hello information on this page toolog in toohello sandbox using SSH.</span></span> <span data-ttu-id="67cbd-131">Utilizzare il nome di hello e la password fornita.</span><span class="sxs-lookup"><span data-stu-id="67cbd-131">Use hello name and password provided.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="67cbd-132">Se non si dispone di un client SSH installato, è possibile utilizzare hello SSH basata sul web fornito da macchina virtuale hello in **http://localhost:4200 /**.</span><span class="sxs-lookup"><span data-stu-id="67cbd-132">If you do not have an SSH client installed, you can use hello web-based SSH provided at by hello virtual machine at **http://localhost:4200/**.</span></span>
   > 
   
    <span data-ttu-id="67cbd-133">Hello prima volta che ci si connette tramite SSH, sono toochange richiesta hello password per l'account radice hello.</span><span class="sxs-lookup"><span data-stu-id="67cbd-133">hello first time you connect using SSH, you are prompted toochange hello password for hello root account.</span></span> <span data-ttu-id="67cbd-134">Immettere una nuova password da usare quando si accede tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="67cbd-134">Enter a new password, which you use when you log in using SSH.</span></span>

2. <span data-ttu-id="67cbd-135">Una volta effettuato l'accesso, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="67cbd-135">Once logged in, enter hello following command:</span></span>
   
        ambari-admin-password-reset
   
    <span data-ttu-id="67cbd-136">Quando richiesto, specificare una password per l'account amministratore Ambari hello.</span><span class="sxs-lookup"><span data-stu-id="67cbd-136">When prompted, provide a password for hello Ambari admin account.</span></span> <span data-ttu-id="67cbd-137">Viene utilizzato quando si accede a hello dell'interfaccia utente Web Ambari.</span><span class="sxs-lookup"><span data-stu-id="67cbd-137">This is used when you access hello Ambari Web UI.</span></span>

## <a name="use-hive-commands"></a><span data-ttu-id="67cbd-138">Usare i comandi Hive</span><span class="sxs-lookup"><span data-stu-id="67cbd-138">Use Hive commands</span></span>

1. <span data-ttu-id="67cbd-139">Da una sandbox di toohello connessione SSH, utilizzare hello shell dei comandi toostart hello Hive seguenti:</span><span class="sxs-lookup"><span data-stu-id="67cbd-139">From an SSH connection toohello sandbox, use hello following command toostart hello Hive shell:</span></span>
   
        hive
2. <span data-ttu-id="67cbd-140">Una volta avviata la shell hello, utilizzare le tabelle di hello tooview forniti con sandbox hello seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="67cbd-140">Once hello shell has started, use hello following tooview hello tables that are provided with hello sandbox:</span></span>
   
        show tables;
3. <span data-ttu-id="67cbd-141">Hello utilizzare seguenti tooretrieve 10 righe dagli hello `sample_07` tabella:</span><span class="sxs-lookup"><span data-stu-id="67cbd-141">Use hello following tooretrieve 10 rows from hello `sample_07` table:</span></span>
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a><span data-ttu-id="67cbd-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="67cbd-142">Next steps</span></span>
* [<span data-ttu-id="67cbd-143">Informazioni su come toouse Visual Studio con hello Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="67cbd-143">Learn how toouse Visual Studio with hello Hortonworks Sandbox</span></span>](hdinsight-hadoop-emulator-visual-studio.md)
* [<span data-ttu-id="67cbd-144">Cavi hello di apprendimento di hello Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="67cbd-144">Learning hello ropes of hello Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="67cbd-145">Esercitazione di Hadoop: introduzione a HDP</span><span class="sxs-lookup"><span data-stu-id="67cbd-145">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

