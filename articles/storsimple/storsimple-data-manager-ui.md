---
title: Azure StorSimple Manager dati UI aaaMicrosoft | Documenti Microsoft
description: Viene descritto come toouse servizio StorSimple Manager di dati dell'interfaccia utente (anteprima privata)
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: b0ee12b3e495400b54e48eb1a98c68b1af2e5f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-using-hello-storsimple-data-manager-service-ui-private-preview"></a>Gestire con il servizio di gestione di dati di StorSimple hello dell'interfaccia utente (anteprima privata)

In questo articolo viene illustrato come utilizzare la trasformazione dei dati di gestione di dati di StorSimple UI tooperform hello sui dati che si trovano in dispositivi della serie StorSimple 8000 hello. Hello dati trasformati possono quindi essere utilizzati da altri servizi di Azure, ad esempio servizi multimediali di Azure, HDInsight di Azure, Azure Machine Learning e ricerca di Azure. 


## <a name="use-storsimple-data-transformation"></a>Usare la trasformazione dati di StorSimple

Hello StorSimple Data Manager è risorsa hello entro il quale è possibile creare istanze la trasformazione dei dati. Hello Data Transformation service consente di spostare i dati dal tooblobs di dispositivo StorSimple locale nell'archiviazione di Azure. Di conseguenza, nel flusso di lavoro è necessario dettagli hello toospecify sui dati di dispositivo e hello di StorSimple di interesse che si desidera toomove toohello account di archiviazione.

### <a name="create-a-storsimple-data-manager-service"></a>Creare un servizio StorSimple Data Manager

Eseguire hello seguendo i passaggi toocreate un servizio dati di StorSimple Manager.

1. toocreate un servizio dati di StorSimple Manager, andare troppo[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)

2. Fare clic su hello  **+**  icona e cercare dati StorSimple Manager. Fare clic sul servizio StorSimple Data Manager, quindi su **Crea**.

3. Se la sottoscrizione è abilitata per la creazione di questo servizio, si noterà hello seguente blade.

    ![Creare una risorsa StorSimple Data Manager](./media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. Immettere gli input hello e fare clic su **crea**. Hello è specificata la posizione deve essere hello che ospita gli account di archiviazione e il servizio StorSimple Manager. Attualmente sono supportate solo le aree Europa occidentale e Stati Uniti occidentali. Di conseguenza, il servizio StorSimple Manager, il servizio di gestione dati e hello account di archiviazione associato deve essere in aree hello precedente è supportato. Richiede circa un servizio di hello toocreate minuti.

### <a name="create-a-data-transformation-job-definition"></a>Creare una definizione di processo di trasformazione dati

All'interno di un servizio di gestione di dati di StorSimple, è necessario toocreate la definizione di un processo di trasformazione di dati. Definizione di un processo specifica i dettagli dei dati di hello che si sono interessati lo spostamento in un account di archiviazione in formato nativo hello. 

Eseguire hello seguendo i passaggi toocreate una nuova definizione di processo di trasformazione di dati.

1.  Passare toohello servizio creato. Fare clic su **+ Job Definition** (+ Definizione processo).

    ![Fare clic su + Definizione processo](./media/storsimple-data-manager-ui/click-add-job-definition.png)

2. Apre il pannello nuova processo definizione Hello. Assegnare un nome alla definizione di processo e fare clic su **Origine**. In hello **Configura origine dati** pannello, specificare i dettagli di hello del dispositivo StorSimple e hello dati di interesse.

    ![Creare la definizione di processo](./media/storsimple-data-manager-ui//create-new-job-deifnition.png)

3. Poiché si tratta di un nuovo servizio Data Manager, non sono presenti repository di dati configurati. il servizio StorSimple Manager come archivio dati, fare clic su tooadd **Aggiungi nuovo** in hello elenco a discesa del repository di dati e quindi fare clic su **Aggiungi Repository di dati**.

4. Scegliere **StorSimple serie 8000 Manager** come repository di hello digitare e immettere le proprietà di hello del **StorSimple Manager**. Per hello **Id risorsa** campo, è necessario tooenter hello numero prima hello **:** nella chiave di registrazione hello del servizio StorSimple manager.

    ![Creare un'origine dati](./media/storsimple-data-manager-ui/create-new-data-source.png)

5.  Fare clic su **OK** al termine dell'operazione. In questo modo sarà possibile salvare il repository di dati e usare questo servizio StorSimple Manager in altre definizioni di processo senza dover immettere nuovamente tali parametri. Sono necessari alcuni secondi dopo aver fatto clic **OK** per hello tooshow StorSimple Manager di hello dall'elenco a discesa.

6.  In hello **Configura origine dati** pannello, immettere il nome di dispositivo hello e hello nome del volume contenente i dati di interesse.

7.  In hello **filtro** sottosezione, immettere una directory radice hello che contiene i dati di interesse (in questo campo deve iniziare con un `\`). È inoltre possibile aggiungere qualsiasi filtro file qui.

8.  servizio di trasformazione dati Hello funziona sui dati hello viene inviati fino toohello Azure tramite gli snapshot. Quando si esegue questo processo, è possibile scegliere tootake un backup ogni volta che questo processo viene eseguito (toowork sui dati più recenti) o toouse hello ultimo backup esistente nel cloud hello (se si lavora con alcuni dati archiviati).

    ![Dettagli nuova origine dati](./media/storsimple-data-manager-ui/new-data-source-details.png)

9. Successivamente, le impostazioni della destinazione hello necessario toobe configurato. Sono previsti 2 tipi di destinazioni supportate: account di Archiviazione di Azure e account di Servizi multimediali di Azure. Scegliere gli account di archiviazione di file tooput in BLOB in tale account. Scegliere account di servizi multimediali tooput file nelle risorse in tale account. Nuovamente, è necessario tooadd un repository. Nell'elenco a discesa hello, selezionare **Aggiungi nuovo** e quindi **configurare le impostazioni**.

    ![Creare un sink dati](./media/storsimple-data-manager-ui/create-new-data-sink.png)

10. In questo caso, è possibile selezionare il tipo di hello del repository che si desidera tooadd e hello altri parametri associati repository hello. In entrambi i casi, viene creata una coda di archiviazione quando viene eseguito il processo di hello. Questa coda viene popolata con i messaggi relativi ai BLOB trasformati non appena pronti. nome Hello di questa coda è hello corrisponde al nome hello hello della definizione del processo. Se si seleziona **servizi multimediali** come tipo di repository hello, quindi è possibile anche immettere le credenziali dell'account di archiviazione in cui viene creata la coda hello.

    ![Dettagli nuovo sink dati](./media/storsimple-data-manager-ui/new-data-sink-details.png)

11. Dopo aver aggiunto i repository di dati hello (che richiede alcuni secondi), si noterà repository hello nell'elenco a discesa hello in hello **nome account di destinazione**.  Scegli destinazione hello che è necessario.

12. Fare clic su **OK** definizione del processo toocreate hello. La definizione di processo è ora impostata. È possibile utilizzare questa definizione di processo più volte tramite hello dell'interfaccia utente.

    ![Aggiungere una nuova definizione di processo](./media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-hello-job-definition"></a>Eseguire la definizione di processo hello

Ogni volta che è necessario toomove dati dall'account di archiviazione StorSimple toohello specificate nella definizione di processo hello, sarà necessario tooinvoke è. È prevista una certa flessibilità nella modifica dei parametri di hello ogni volta che si chiama il processo di hello. come indicato di seguito sono riportati i passaggi di Hello:

1. Selezionare il servizio dati di StorSimple Manager e passare troppo**monitoraggio**. Fare clic su **Esegui adesso**.

    ![Attivare la definizione di processo](./media/storsimple-data-manager-ui/run-now.png)

2. Scegliere la definizione di processo hello che si desidera toorun. Fare clic su **impostazioni esecuzione test** toomodify tutte le impostazioni che è possibile toochange per l'esecuzione del processo.

    ![Impostazioni di esecuzione del processo](./media/storsimple-data-manager-ui/run-settings.png)

3. Fare clic su **OK** e quindi fare clic su **eseguire** toolaunch il processo. toomonitor questo processo, passa toohello **processi** pagina nella gestione di dati di StorSimple.

    ![Elenco e stato dei processi](./media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. In aggiunta toomonitoring in hello **processi** pannello, può anche restare in attesa nella coda di archiviazione hello in cui viene aggiunto un messaggio ogni volta che un file viene spostato dall'account di archiviazione StorSimple toohello.


## <a name="next-steps"></a>Passaggi successivi

[Utilizzare i processi di gestione di dati di StorSimple toolaunch .NET SDK](storsimple-data-manager-dotnet-jobs.md).
