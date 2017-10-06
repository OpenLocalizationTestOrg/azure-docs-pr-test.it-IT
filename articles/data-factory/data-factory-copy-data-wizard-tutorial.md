---
title: 'Esercitazione: Creare una pipeline usando la Copia guidata | Documentazione Microsoft'
description: "In questa esercitazione è creare una pipeline di Data Factory di Azure con un'attività di copia utilizzando hello Copia guidata supportati da Data Factory"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 567b89e7a54c245c134cd0674690e6f3499b46d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a>Esercitazione: Creare una pipeline con l'attività di copia usando la Copia guidata di Data Factory
> [!div class="op_single_selector"]
> * [Panoramica e prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Copia guidata](data-factory-copy-data-wizard-tutorial.md)
> * [Portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Modello di Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

In questa esercitazione illustra come hello toouse **Copia guidata** toocopy dati da un database di SQL Azure tooan di archiviazione blob di Azure. 

Hello Azure Data Factory **Copia guidata** consente tooquickly creare una pipeline di dati che copia i dati da un archivio dati di origine supportata dati archivio tooa supportato destinazione. È pertanto consigliabile utilizzare la procedura guidata hello come un toocreate passaggio prima una pipeline di esempio per lo scenario lo spostamento dei dati. Per un elenco degli archivi dati supportati come origini e come destinazioni, vedere gli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).  

Questa esercitazione viene illustrato come toocreate una data factory di Azure, hello avviare Copia guidata, passare a una serie di informazioni di tooprovide passaggi lo scenario di inserimento o lo spostamento dei dati. Al termine della procedura guidata hello, la procedura guidata hello crea automaticamente una pipeline con dati di toocopy un attività di copia da un database di SQL Azure tooan di archiviazione blob di Azure. Per altre informazioni sull'attività di copia, vedere le [attività di spostamento dei dati](data-factory-data-movement-activities.md).

## <a name="prerequisites"></a>Prerequisiti
Completare i prerequisiti elencati in hello [esercitazione Panoramica](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) articolo prima di eseguire questa esercitazione.

## <a name="create-data-factory"></a>Creare un'istanza di Data Factory
In questo passaggio, si usa hello toocreate portale Azure una data factory di Azure denominato **ADFTutorialDataFactory**.

1. Accedi troppo[portale di Azure](https://portal.azure.com).
2. Fare clic su **+ nuovo** dall'angolo superiore sinistro di hello, fare clic su **dati + analitica**, fare clic su **Data Factory**. 
   
   ![Nuovo->DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. In hello **nuova data factory** pannello:
   
   1. Immettere **ADFTutorialDataFactory** per hello **nome**.
       nome Hello di hello Azure data factory deve essere globalmente univoco. Se viene visualizzato l'errore hello: `Data factory name “ADFTutorialDataFactory” is not available`, modificare il nome di hello di hello data factory (ad esempio, yournameADFTutorialDataFactoryYYYYMMDD) e provare a creare di nuovo. Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .  
      
       ![Nome di data factory non disponibile](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. Selezionare la **sottoscrizione**di Azure.
   3. Per il gruppo di risorse, effettuare una delle hello alla procedura seguente: 
      
      - Selezionare **utilizzare esistente** tooselect un gruppo di risorse esistente.
      - Selezionare **Crea nuovo** tooenter un nome per un gruppo di risorse.
          
        Alcuni dei passaggi di hello in questa esercitazione si presuppone che venga utilizzato il nome di hello: **ADFTutorialResourceGroup** per il gruppo di risorse hello. toolearn sui gruppi di risorse, vedere [utilizzando risorse gruppi di risorse di Azure toomanage](../azure-resource-manager/resource-group-overview.md).
   4. Selezionare un **percorso** per data factory di hello.
   5. Selezionare **toodashboard Pin** casella di controllo nella parte inferiore di hello del pannello hello.  
   6. Fare clic su **Crea**.
      
       ![Pannello Nuova data factory](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. Una volta completata la creazione di hello, vedrai hello **Data Factory** pannello, come illustrato nella seguente immagine hello:
   
   ![Home page di Data factory](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a>Avviare la Copia guidata
1. Nel Pannello di Data Factory hello, fare clic su **copia dei dati [anteprima]** toolaunch hello **Copia guidata**. 
   
   > [!NOTE]
   > Se viene visualizzato il browser web hello è bloccata su "Autorizzazione …", disabilitare o deselezionare **bloccare i cookie di terze parti e i dati del sito** impostazione consentiva di mantenere le impostazioni del browser hello (o) e creare un'eccezione per  **Login.microsoftonline.com** e quindi provare ad avviare la procedura guidata hello nuovamente.
2. In hello **proprietà** pagina:
   
   1. Immettere **CopyFromBlobToAzureSql** per **Nome attività**.
   2. Immettere una **descrizione** (facoltativo).
   3. Hello modifica **data ora di inizio** hello e **data e ora fine** in modo che la data di fine hello impostare tootoday e avviare data toofive giorno.  
   4. Fare clic su **Avanti**.  
      
      ![Strumento di copia - Pagina Proprietà](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. In hello **archivio dati di origine** pagina, fare clic su **archiviazione Blob di Azure** riquadro. Usare l'archivio dati di origine di pagina toospecify hello per attività di copia hello. 
   
    ![Strumento di copia - Pagina Archivio dati di origine](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. In hello **specificare account di archiviazione Blob di Azure hello** pagina:
   
   1. Immettere **AzureStorageLinkedService** per **Nome del servizio collegato**.
   2. Verificare che in **Account selection method** (Metodo di selezione dell'account) sia selezionata l'opzione **From Azure subscriptions** (Da sottoscrizioni di Azure).
   3. Selezionare la **sottoscrizione**di Azure.  
   4. Selezionare un **account di archiviazione Azure** da hello account disponibile nella sottoscrizione selezionata hello l'elenco di archiviazione di Azure. È anche possibile scegliere tooenter impostazioni dell'account di archiviazione manualmente selezionando **immettere manualmente** opzione per hello **metodo di selezione dell'Account**, quindi fare clic su **Avanti**. 
      
      ![Strumento Copia: specificare l'account di archiviazione Blob di Azure hello](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. In **cartella o file di input hello scegliere** pagina:
   
   1. Fare doppio clic sulla cartella **adftutorial**.
   2. Selezionare **emp.txt** e fare clic su **Scegli**.
      
      ![Strumento Copia - scegliere i file di input hello o cartella](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. In hello **cartella o file di input hello scegliere** pagina, fare clic su **Avanti**. Non selezionare **Binary copy**(Copia binaria). 
   
    ![Strumento Copia - scegliere i file di input hello o cartella](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. In hello **impostazioni del File di formato** visualizzata delimitatori hello e lo schema di hello che viene rilevata automaticamente dalla procedura guidata hello mediante l'analisi di file hello. È anche possibile immettere manualmente i delimitatori di hello per hello Copia guidata toostop il rilevamento automatico o toooverride. Fare clic su **Avanti** dopo aver esaminato i delimitatori di hello e anteprima dei dati. 
   
    ![Strumento di copia - Impostazioni di formattazioni del file](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. In dati di destinazione hello archivio di pagina, selezionare **Database SQL di Azure**, fare clic su **Avanti**.
   
    ![Strumento di copia - Scegliere l'archivio di destinazione](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. In **database SQL di Azure di hello specificare** pagina:
   
   1. Immettere **AzureSqlLinkedService** per hello **nome connessione** campo.
   2. Verificare che in **Server / database selection method** (Metodo di selezione del server/database) sia selezionata l'opzione **From Azure subscriptions** (Da sottoscrizioni di Azure).
   3. Selezionare la **sottoscrizione**di Azure.  
   4. Selezionare **Nome server** e **Database**.
   5. Immettere un **Nome utente** e una **Password**.
   6. Fare clic su **Avanti**.  
      
      ![Strumento di copia - Specificare il database SQL di Azure](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. In hello **mapping della tabella** selezionare **emp** per hello **destinazione** campo dall'elenco a discesa hello, fare clic su **freccia giù** (facoltativo) toosee hello dati dello schema e toopreview hello.
    
     ![Strumento di copia - Mapping tabella](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. In hello **mapping dello Schema** pagina, fare clic su **Avanti**.
    
    ![Strumento di copia - Mapping dello schema](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. In hello **le impostazioni delle prestazioni** pagina, fare clic su **Avanti**. 
    
    ![Strumento di copia - Impostazioni relative alle prestazioni](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. Esaminare le informazioni nella hello **riepilogo** pagina e fare clic su **fine**. procedura guidata di Hello crea due servizi collegati, due set di dati (input e output) e una pipeline in data factory di hello (dalla quale è stata avviata la procedura guidata copia hello). 
    
    ![Strumento di copia - Impostazioni relative alle prestazioni](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a>Avviare l'applicazione di monitoraggio e gestione
1. In hello **distribuzione** pagina, fare clic sul collegamento hello: `Click here toomonitor copy pipeline`.
   
   ![Strumento di copia - La distribuzione è riuscita](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. monitoraggio dell'applicazione Hello viene avviata in una scheda separata nel web browser.   
   
   ![App di monitoraggio](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. Fare clic su stato più recente di hello toosee delle sezioni orarie, **aggiornare** pulsante hello **attività WINDOWS** elenco nella parte inferiore di hello. Sarà possibile visualizzare finestre di cinque attività cinque giorni tra l'ora di inizio e fine per la pipeline di hello. elenco di Hello non vengono aggiornata automaticamente, in modo da poter necessario tooclick aggiorna un paio di volte prima di visualizzare tutte le finestre attività hello nello stato Ready hello. 
4. Selezionare una finestra attività nell'elenco di hello. Vedere i dettagli di hello su di esso nella hello **attività finestra Esplora** su hello destra.

    ![Dettagli finestra attività](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    Si noti che le date di hello 11, 12, 13, 14 e 15 sono in colore verde, il che significa che sono già stati prodotti hello le sezioni di output giornaliera per queste date. Inoltre, vedere questa codifica a colori nella pipeline hello e set di dati di output nella vista diagramma hello hello. Nel passaggio precedente hello, si noti che due sezioni sono già stati prodotti una sezione è in corso di elaborazione e hello altre due sono in attesa toobe elaborati (basato su codifica a colori hello). 

    Per altre informazioni sull'uso di questa applicazione, vedere l'articolo [Monitorare e gestire le pipeline di Azure Data Factory con l'app di monitoraggio e gestione](data-factory-monitor-manage-app.md).

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione sono stati usati l'archivio BLOB di Azure come archivio dati di origine e un database SQL di Azure come archivio dati di destinazione in un'operazione di copia. Hello nella tabella seguente fornisce un elenco di archivi di dati supportato come origini e destinazioni da attività di copia hello: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

Per informazioni dettagliate sui campi/proprietà visualizzate nella procedura guidata copia hello per un archivio dati, fare clic sul collegamento di hello per hello archivio di dati nella tabella hello. 
