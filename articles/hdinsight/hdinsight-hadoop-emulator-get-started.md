---
title: "Informazioni sull’uso di una sandbox di Hadoop - emulatore - Azure HDInsight | Documentazione Microsoft"
description: "Per iniziare ad apprendere l'uso dell'ecosistema Handoop, è possibile impostare un ambiente sandbox Hadoop di Hortonworks in una macchina virtuale Azure. "
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
ms.openlocfilehash: b701879464205860edd1c097651b532f87bae388
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a><span data-ttu-id="e0504-104">Introduzione a una sandbox di Hadoop, un emulatore in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e0504-104">Get started with a Hadoop sandbox, an emulator on a virtual machine</span></span>

<span data-ttu-id="e0504-105">Informazioni su come installare l'ambiente sandbox Hadoop da Hortonworks in una macchina virtuale per acquisire familiarità con l'ecosistema di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e0504-105">Learn how to install the Hadoop sandbox from Hortonworks on a virtual machine to learn about the Hadoop ecosystem.</span></span> <span data-ttu-id="e0504-106">L'ambiente sandbox è un ambiente di sviluppo locale per informazioni su Hadoop, Hadoop Distributed File System (HDFS) e l'invio di processi.</span><span class="sxs-lookup"><span data-stu-id="e0504-106">The sandbox provides a local development environment to learn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span></span> <span data-ttu-id="e0504-107">Dopo aver acquisito familiarità con Hadoop è possibile iniziare a usare Hadoop in Azure creando un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e0504-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span></span> <span data-ttu-id="e0504-108">Per altre informazioni sulle attività iniziali, vedere l'articolo [Introduzione all'uso di Hadoop basato su Linux in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e0504-108">For more information on how to get started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0504-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e0504-109">Prerequisites</span></span>
* <span data-ttu-id="e0504-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span><span class="sxs-lookup"><span data-stu-id="e0504-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span></span> <span data-ttu-id="e0504-111">Scaricare e installare l'app da [qui](https://www.virtualbox.org/wiki/Downloads).</span><span class="sxs-lookup"><span data-stu-id="e0504-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span></span>



## <a name="download-and-install-the-virtual-machine"></a><span data-ttu-id="e0504-112">Scaricare e installare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e0504-112">Download and install the virtual machine</span></span>
1. <span data-ttu-id="e0504-113">Passare ai [download di Hortonworks](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="e0504-113">Browse to the [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span></span>

2. <span data-ttu-id="e0504-114">Fare clic su **DOWNLOAD FOR VIRTUALBOX** per scaricare la versione più recente di Hortonworks Sandbox in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e0504-114">Click **DOWNLOAD FOR VIRTUALBOX** to download the latest Hortonworks Sandbox on a VM.</span></span> <span data-ttu-id="e0504-115">È necessario registrarsi con Hortonworks prima di avviare il download.</span><span class="sxs-lookup"><span data-stu-id="e0504-115">You are prompted to register with Hortonworks before the download begins.</span></span> <span data-ttu-id="e0504-116">Il download può richiedere da una a due ore a seconda della velocità della rete.</span><span class="sxs-lookup"><span data-stu-id="e0504-116">It takes one to two hours to download depending on your network speed.</span></span>
   
    ![Immagine di collegamento per scaricare Sandbox di Hortonworks per VirtualBox](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. <span data-ttu-id="e0504-118">Nella stessa pagina Web, fare clic sul collegamento **Import on Virtual Box** per scaricare un file PDF contenente le istruzioni di installazione per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e0504-118">From the same web page, click the **Import on Virtual Box** link to download a PDF containing installation instructions for the virtual machine.</span></span>

<span data-ttu-id="e0504-119">Per scaricare una versione precedente di sandbox HDP, espandere l'archivio:</span><span class="sxs-lookup"><span data-stu-id="e0504-119">To download an older HDP version sandbox, expand the archive:</span></span>

![Archivio Hortonworks Sandbox](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-the-virtual-machine"></a><span data-ttu-id="e0504-121">Avviare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e0504-121">Start the virtual machine</span></span>

1. <span data-ttu-id="e0504-122">Aprire Oracle VM VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="e0504-122">Open Oracle VM VirtualBox.</span></span>
2. <span data-ttu-id="e0504-123">Scegliere **Import Appliance** dal menu **File** e quindi specificare l'immagine di Hortonworks Sandbox.</span><span class="sxs-lookup"><span data-stu-id="e0504-123">From the **File** menu, click **Import Appliance**, and then specify the Hortonworks Sandbox image.</span></span>
1. <span data-ttu-id="e0504-124">Selezionare Hortonworks Sandbox, fare clic su **Start** e quindi su **Normal Start**.</span><span class="sxs-lookup"><span data-stu-id="e0504-124">Select the Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span></span> <span data-ttu-id="e0504-125">Al termine del processo di avvio della macchina virtuale, vengono visualizzate le istruzioni di accesso.</span><span class="sxs-lookup"><span data-stu-id="e0504-125">Once the virtual machine has finished the boot process, it displays login instructions.</span></span>
   
    ![Avvio normale](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. <span data-ttu-id="e0504-127">Aprire un Web browser e passare all'URL visualizzato, in genere http://127.0.0.1:8888.</span><span class="sxs-lookup"><span data-stu-id="e0504-127">Open a web browser and navigate to the URL displayed (usually http://127.0.0.1:8888).</span></span>

## <a name="set-sandbox-passwords"></a><span data-ttu-id="e0504-128">Impostare le password Sandbox</span><span class="sxs-lookup"><span data-stu-id="e0504-128">Set Sandbox passwords</span></span>

1. <span data-ttu-id="e0504-129">Dal passaggio **introduttivo** della pagina di Sandbox di Hortonworks, selezionare **View Advanced Options** (Visualizza opzioni avanzate).</span><span class="sxs-lookup"><span data-stu-id="e0504-129">From the **get started** step of the Hortonworks Sandbox page, select **View Advanced Options**.</span></span> <span data-ttu-id="e0504-130">Utilizzare le informazioni in questa pagina per accedere alla sandbox con SSH.</span><span class="sxs-lookup"><span data-stu-id="e0504-130">Use the information on this page to log in to the sandbox using SSH.</span></span> <span data-ttu-id="e0504-131">Utilizzare il nome e la password forniti.</span><span class="sxs-lookup"><span data-stu-id="e0504-131">Use the name and password provided.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e0504-132">Se non è stato installato un client SSH, è possibile usare l'SSH basato sul Web fornito dalla macchina virtuale all'indirizzo **http://localhost:4200/**.</span><span class="sxs-lookup"><span data-stu-id="e0504-132">If you do not have an SSH client installed, you can use the web-based SSH provided at by the virtual machine at **http://localhost:4200/**.</span></span>
   > 
   
    <span data-ttu-id="e0504-133">Al primo collegamento tramite SSH viene richiesto di cambiare la password per l'account radice.</span><span class="sxs-lookup"><span data-stu-id="e0504-133">The first time you connect using SSH, you are prompted to change the password for the root account.</span></span> <span data-ttu-id="e0504-134">Immettere una nuova password da usare quando si accede tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="e0504-134">Enter a new password, which you use when you log in using SSH.</span></span>

2. <span data-ttu-id="e0504-135">Dopodiché immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0504-135">Once logged in, enter the following command:</span></span>
   
        ambari-admin-password-reset
   
    <span data-ttu-id="e0504-136">Quando richiesto, fornire una password per l'account di amministratore di Ambari.</span><span class="sxs-lookup"><span data-stu-id="e0504-136">When prompted, provide a password for the Ambari admin account.</span></span> <span data-ttu-id="e0504-137">Questo viene utilizzato quando si accede all'interfaccia utente Web di Ambari.</span><span class="sxs-lookup"><span data-stu-id="e0504-137">This is used when you access the Ambari Web UI.</span></span>

## <a name="use-hive-commands"></a><span data-ttu-id="e0504-138">Usare i comandi Hive</span><span class="sxs-lookup"><span data-stu-id="e0504-138">Use Hive commands</span></span>

1. <span data-ttu-id="e0504-139">Da una connessione SSH a Sandbox, utilizzare il comando seguente per avviare la shell di Hive:</span><span class="sxs-lookup"><span data-stu-id="e0504-139">From an SSH connection to the sandbox, use the following command to start the Hive shell:</span></span>
   
        hive
2. <span data-ttu-id="e0504-140">Una volta avviata la shell, utilizzarla per visualizzare le tabelle fornite con Sandbox:</span><span class="sxs-lookup"><span data-stu-id="e0504-140">Once the shell has started, use the following to view the tables that are provided with the sandbox:</span></span>
   
        show tables;
3. <span data-ttu-id="e0504-141">Usare il codice seguente per recuperare 10 righe dalla tabella `sample_07` :</span><span class="sxs-lookup"><span data-stu-id="e0504-141">Use the following to retrieve 10 rows from the `sample_07` table:</span></span>
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a><span data-ttu-id="e0504-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e0504-142">Next steps</span></span>
* [<span data-ttu-id="e0504-143">Informazioni su come utilizzare Visual Studio con Sandbox di Hortonworks</span><span class="sxs-lookup"><span data-stu-id="e0504-143">Learn how to use Visual Studio with the Hortonworks Sandbox</span></span>](hdinsight-hadoop-emulator-visual-studio.md)
* [<span data-ttu-id="e0504-144">Acquisire dimestichezza con Sandbox di Hortonworks</span><span class="sxs-lookup"><span data-stu-id="e0504-144">Learning the ropes of the Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="e0504-145">Esercitazione di Hadoop: introduzione a HDP</span><span class="sxs-lookup"><span data-stu-id="e0504-145">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

