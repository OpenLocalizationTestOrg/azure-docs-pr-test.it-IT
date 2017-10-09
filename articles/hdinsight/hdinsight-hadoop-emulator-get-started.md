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
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a>Introduzione a una sandbox di Hadoop, un emulatore in una macchina virtuale

Informazioni su come tooinstall hello sandbox Hadoop da Hortonworks in una macchina virtuale di toolearn sull'ecosistema di Hadoop hello. sandbox Hello fornisce un toolearn ambiente di sviluppo locale su Hadoop, Hadoop Distributed File System (HDFS) e l'invio di processi. Dopo aver acquisito familiarità con Hadoop è possibile iniziare a usare Hadoop in Azure creando un cluster HDInsight. Per ulteriori informazioni sulla modalità di avvio tooget, vedere [introduzione Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).

## <a name="prerequisites"></a>Prerequisiti
* [Oracle VirtualBox](https://www.virtualbox.org/). Scaricare e installare l'app da [qui](https://www.virtualbox.org/wiki/Downloads).



## <a name="download-and-install-hello-virtual-machine"></a>Scaricare e installare una macchina virtuale hello
1. Sfoglia toohello [Hortonworks Scarica](http://hortonworks.com/downloads/#sandbox).

2. Fare clic su **scaricare per VIRTUALBOX** toodownload hello Hortonworks Sandbox più recenti in una macchina virtuale. Si è richiesta tooregister con Hortonworks prima di iniziare il download di hello. Accetta una toodownload di ore tootwo a seconda della velocità di rete.
   
    ![Immagine di collegamento per scaricare Sandbox di Hortonworks per VirtualBox](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. Da hello stessa pagina web, fare clic su hello **importazione su Virtual Box** collegamento toodownload un file PDF che contiene le istruzioni di installazione per la macchina virtuale hello.

toodownload un sandbox di versione HDP precedente, espandere l'archivio hello:

![Archivio Hortonworks Sandbox](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-hello-virtual-machine"></a>Avviare la macchina virtuale hello

1. Aprire Oracle VM VirtualBox.
2. Da hello **File** menu, fare clic su **dello strumento di importazione**, quindi specificare hello immagine Hortonworks Sandbox.
1. Fare clic su Hortonworks Sandbox, seleziona hello **avviare**e quindi **normale avviare**. Al termine il processo di avvio hello macchina virtuale hello, Visualizza le istruzioni di account di accesso.
   
    ![Avvio normale](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. Aprire un web browser e passare l'URL toohello visualizzato (in genere http://127.0.0.1:8888).

## <a name="set-sandbox-passwords"></a>Impostare le password Sandbox

1. Da hello **iniziare** passaggio di hello pagina Hortonworks Sandbox, selezionare **opzioni avanzate vista**. Utilizzare le informazioni di hello in toolog questa pagina in sandbox toohello tramite SSH. Utilizzare il nome di hello e la password fornita.
   
   > [!NOTE]
   > Se non si dispone di un client SSH installato, è possibile utilizzare hello SSH basata sul web fornito da macchina virtuale hello in **http://localhost:4200 /**.
   > 
   
    Hello prima volta che ci si connette tramite SSH, sono toochange richiesta hello password per l'account radice hello. Immettere una nuova password da usare quando si accede tramite SSH.

2. Una volta effettuato l'accesso, immettere hello comando seguente:
   
        ambari-admin-password-reset
   
    Quando richiesto, specificare una password per l'account amministratore Ambari hello. Viene utilizzato quando si accede a hello dell'interfaccia utente Web Ambari.

## <a name="use-hive-commands"></a>Usare i comandi Hive

1. Da una sandbox di toohello connessione SSH, utilizzare hello shell dei comandi toostart hello Hive seguenti:
   
        hive
2. Una volta avviata la shell hello, utilizzare le tabelle di hello tooview forniti con sandbox hello seguenti hello:
   
        show tables;
3. Hello utilizzare seguenti tooretrieve 10 righe dagli hello `sample_07` tabella:
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a>Passaggi successivi
* [Informazioni su come toouse Visual Studio con hello Hortonworks Sandbox](hdinsight-hadoop-emulator-visual-studio.md)
* [Cavi hello di apprendimento di hello Hortonworks Sandbox](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [Esercitazione di Hadoop: introduzione a HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

