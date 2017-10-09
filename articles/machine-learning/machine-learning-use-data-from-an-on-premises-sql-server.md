---
title: un Server SQL locale in Azure Machine Learning aaaUse | Documenti Microsoft
description: Utilizzare i dati da un analitica di tooperform avanzate database di SQL Server locale con Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 08e4610d-02b6-4071-aad7-a2340ad8e2ea
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: garye;krishnan
ms.openlocfilehash: c0e9908e296b97b31611ef0192744a59073acd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-analytics-with-azure-machine-learning-using-data-from-an-on-premises-sql-server-database"></a>Eseguire analisi avanzate con Azure Machine Learning usando i dati di un database SQL Server locale

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

Spesso le aziende che funzionano con dati locali sarebbe tootake vantaggio della scala hello e flessibilità dei cloud hello per loro machine learning i carichi di lavoro. Ma che non vogliono toodisrupt i processi di business corrente e i flussi di lavoro spostando cloud toohello dati locale. Azure Machine Learning supporta ora la lettura dei dati da un database SQL Server locale e, successivamente, il processo di formazione e assegnazione di punteggi a un modello avvalendosi di questi dati. Non è più necessario toomanually copiare e sincronizzazione hello dati tra cloud hello e il server locale. Invece, hello **l'importazione dei dati** modulo in Azure Machine Learning Studio possibile leggerne direttamente dal database di SQL Server locale per il training e assegnazione dei punteggi di processi.

In questo articolo viene fornita una panoramica di come tooingress locale dati di SQL server in Azure Machine Learning. Presuppone la conoscenza dei concetti di base di Azure Machine Learning, come aree di lavoro, moduli, set di dati, esperimenti *e così via*.

> [!NOTE]
> Questa funzionalità non è disponibile per le aree di lavoro gratuite. Per altre informazioni sui prezzi e sui piani tariffari di Machine Learning, vedere [Azure Machine Learning Pricing](https://azure.microsoft.com/pricing/details/machine-learning/)(Prezzi di Azure Machine Learning).
>
>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="install-hello-microsoft-data-management-gateway"></a>Installare il Gateway di gestione dati Microsoft hello
tooaccess un database di SQL Server locale in Azure Machine Learning, è necessario toodownload e hello di installare il Gateway di gestione dati Microsoft. Quando si configura una connessione al gateway hello in Machine Learning Studio, si ha l'opportunità di hello per scaricare e installare il gateway di hello tramite hello **Download e il gateway di dati di registro** finestra di dialogo descritte di seguito.

È possibile installare il Gateway di gestione di dati di hello anticipatamente, scaricare ed eseguire il pacchetto di installazione MSI hello da hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).
Scegliere una versione più recente di hello, selezionando i 32 bit o 64 bit come appropriato per il computer. Hello MSI può anche essere utilizzati tooupgrade una Gateway di gestione dati toohello più recente versione esistente, con tutte le impostazioni mantenute.

gateway Hello è hello seguenti prerequisiti:

* versioni del sistema operativo Windows Hello supportato sono Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012 e Windows Server 2012 R2.
* Hello consigliato di configurazione per il computer gateway hello è di almeno 2 GHz, 4 core, 8GB di RAM e dischi di 80GB.
* Se il computer host hello entra in sospensione, gateway hello risponderà toodata richieste. Pertanto, è possibile configurare un risparmio di energia appropriato nel computer di hello prima di installare gateway hello. Se il computer di hello è toohibernate configurato, installazione del gateway hello Visualizza un messaggio.
* Poiché l'attività di copia avviene in base alla frequenza specifica, hello utilizzo delle risorse (CPU, memoria) nel computer di hello segue inoltre hello stesso modello con ore di punta e periodi di inattività. Utilizzo delle risorse anche dipende molto quantità hello di spostamento dei dati. Quando sono in corso più processi di copia, l'utilizzo delle risorse aumenta durante i periodi di picco. Sebbene hello minimi di configurazione elencati in precedenza è tecnicamente sufficienti, è consigliabile toohave una configurazione con più risorse rispetto alla configurazione minima hello a seconda del carico specifico per lo spostamento dei dati.

Tenere presente hello segue durante l'installazione e utilizzo di un Gateway di gestione dati:

* In un computer può essere installata una sola istanza di Gateway di gestione dati.
* È possibile usare un singolo gateway per più origini dati locali.
* È possibile connettere più gateway su computer diversi toohello stessa origine dati locale.
* È possibile configurare un gateway per una sola area di lavoro alla volta. Attualmente i gateway non possono essere condivisi tra più aree di lavoro.
* È possibile configurare più gateway per una singola area di lavoro. Ad esempio, è consigliabile toouse un gateway in origini dati di test tooyour connesso durante lo sviluppo e un gateway di produzione quando si è pronti toooperationalize.
* gateway Hello non è necessario toobe su hello stesso computer come origine dati hello. Ma sempre più vicino toohello origine dati riduce il tempo di hello per origine dati di hello gateway tooconnect toohello. Si consiglia di installare gateway hello in un computer diverso da hello una origine dati locale hello host in modo che hello gateway e l'origine dati non si contendono le risorse.
* Se nel computer è già installato un gateway per uno scenario Power BI o Azure Data Factory, installare un gateway separato per Azure Machine Learning in un altro computer.

  > [!NOTE]
  > È possibile eseguire il Gateway di gestione di dati e di Gateway di Power BI in hello stesso computer.
  >
  >
* È necessario toouse hello Gateway di gestione dati per Azure Machine Learning, anche se si utilizza Azure ExpressRoute per altri dati. Considerare l'origine dati come origine dati locale, ovvero protetta da firewall, anche quando si usa ExpressRoute. Usare la connettività di tooestablish hello Gateway di gestione di dati tra l'origine dati hello e di Machine Learning.

È possibile trovare informazioni dettagliate sui prerequisiti di installazione, i passaggi di installazione e risoluzione dei problemi dell'articolo hello [Gateway di gestione dati](../data-factory/data-factory-data-management-gateway.md).

## <a name="span-idusing-the-data-gateway-step-by-step-walk-classanchorspan-idtoc450838866-classanchorspanspaningress-data-from-your-on-premises-sql-server-database-into-azure-machine-learning"></a><span id="using-the-data-gateway-step-by-step-walk" class="anchor"><span id="_Toc450838866" class="anchor"></span></span>Inserire dati del database SQL Server locale in Azure Machine Learning
In questa procedura dettagliata si installerà Gateway di gestione dati in un'area di lavoro di Azure Machine Learning, lo si configurerà e quindi si leggeranno i dati da un database SQL Server locale.

> [!TIP]
> Prima di iniziare, disabilitare il blocco popup del browser per `studio.azureml.net`. Se si utilizza hello browser Google Chrome, scaricare e installare uno dei hello più plug-in disponibile in Google Chrome WebStore [fare clic su una sola volta dell'estensione App](https://chrome.google.com/webstore/search/clickonce?_category=extensions).
>
>

### <a name="step-1-create-a-gateway"></a>Passaggio 1: Creare un gateway
primo passaggio Hello è toocreate e imposta hello gateway tooaccess il database SQL locale.

1. Accedi troppo[Azure Machine Learning Studio](https://studio.azureml.net/Home/) hello selezionare area di lavoro che si desidera toowork in e.
2. Fare clic su hello **impostazioni** pannello nel hello a sinistra e quindi fare clic su hello **gateway dati** scheda nella parte superiore di hello.
3. Fare clic su **nuovo GATEWAY dati** in basso hello hello.

    ![Nuovo gateway dati](media/machine-learning-use-data-from-an-on-premises-sql-server/new-data-gateway-button.png)
4. In hello **nuovo gateway dati** finestra di dialogo immettere hello **nome del Gateway** e, facoltativamente, aggiungere un **descrizione**. Fare clic sulla freccia di hello hello in basso a destra toogo toohello successivo passaggio della configurazione hello.

    ![Immettere un nome e una descrizione per il gateway](media/machine-learning-use-data-from-an-on-premises-sql-server/new-data-gateway-dialog-enter-name.png)
5. In hello scaricare e registrare dati gateway finestra di dialogo Appunti toohello chiave di registrazione GATEWAY hello di copia.

    ![Scaricare e registrare il gateway dati](media/machine-learning-use-data-from-an-on-premises-sql-server/download-and-register-data-gateway.png)
6. <span id="note-1" class="anchor"></span>Se si dispone non ancora scaricato e installato hello Gateway di gestione dati di Microsoft, quindi fare clic su **gateway di gestione dati Download**. Visualizzata è toothe Microsoft Download Center in cui è possibile selezionare versione del gateway hello è necessario scaricarlo e installarlo. È possibile trovare informazioni dettagliate sui prerequisiti di installazione, i passaggi di installazione e risoluzione dei problemi nelle sezioni di hello inizio dell'articolo hello [spostare dati tra origini locali e cloud con il Gateway di gestione dati](../data-factory/data-factory-move-data-between-onprem-and-cloud.md).
7. Dopo aver installato il gateway di hello, hello Gestione configurazione di Gateway di gestione dati verrà aperto e hello **registro gateway** viene visualizzata una finestra di dialogo. Hello Incolla **chiave di registrazione del Gateway** copiato negli Appunti toohello e fare clic su **registrare**.
8. Se si dispone già di un gateway installato, eseguire hello Gestione configurazione di Gateway di gestione di dati. Fare clic su **Modifica chiave**, incollare il **chiave di registrazione del Gateway** copiato negli Appunti toohello nel passaggio precedente hello e fare clic su **OK**.
9. Una volta completato, installazione hello hello **registro gateway** visualizzazione finestra di dialogo per Microsoft Data Management Gateway Configuration Manager. Incollare hello chiave di registrazione del GATEWAY che è stato copiato negli Appunti hello in un passaggio precedente, quindi fare clic su **registrare**.

    ![Registrare il gateway](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-register-gateway.png)
10. Hello configurazione del gateway è completa quando hello seguente i valori impostato sull'hello **Home** scheda in Microsoft Data Management Gateway Configuration Manager:

    * **Nome del gateway** e **nome dell'istanza** impostati toohello nome del gateway hello.
    * **Registrazione** è troppo**registrati**.
    * **Stato** è troppo**Started**.
    * barra di stato Hello in viene visualizzato nella parte inferiore di hello **tooData servizio Cloud Gateway di gestione connesso** con un segno di spunta verde.

      ![Gestione del gateway di gestione dati](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-registered.png)

      Inoltre, Azure Machine Learning Studio viene aggiornato quando hello registrazione ha esito positivo.

    ![Registrazione del gateway completata](media/machine-learning-use-data-from-an-on-premises-sql-server/gateway-registered.png)
11. In hello **scaricare e registrare il gateway dati** finestra di dialogo, fare clic su installazione di hello toocomplete il segno di spunta. Hello **impostazioni** pagina Visualizza lo stato del gateway come "Online". Nel riquadro di destra hello, sono disponibili informazioni sullo stato e altre informazioni utili.

    ![Impostazioni del gateway](media/machine-learning-use-data-from-an-on-premises-sql-server/gateway-status.png)
12. In Gestione configurazione di Microsoft Data Management Gateway hello passare toohello **certificato** certificato hello scheda specificato in questa scheda è credenziali tooencrypt/decrittografia utilizzati per archivio di dati locale hello specificato nel portale di hello. Questo certificato è certificato predefinito hello. È consigliabile modificare questo certificato proprio tooyour che il backup nel sistema di gestione del certificato. Fare clic su **modifica** toouse il proprio certificato invece.

    ![Cambiare il certificato del gateway](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-certificate.png)
13. (facoltativo) Se si desidera tooenable la registrazione dettagliata per risolvere problemi relativi al gateway hello, in Gestione configurazione di Microsoft Data Management Gateway hello passare toothe **diagnostica** e controllare hello **abilitare la registrazione dettagliata per la risoluzione dei problemi** opzione. Hello informazioni di registrazione è reperibile nel Visualizzatore eventi di Windows di hello in hello **registri applicazioni e servizi**  - &gt; **Gateway di gestione dati** nodo. È inoltre possibile utilizzare hello **diagnostica** scheda tootest hello tooan locale origine dati di connessione tramite gateway hello.

    ![Abilitare la registrazione dettagliata](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-verbose-logging.png)

Il processo di installazione di gateway di hello in Azure Machine Learning completato.
Si è ora pronto toouse dei dati in locale.

In Studio è possibile creare e configurare più gateway per ogni area di lavoro. Ad esempio, potrebbe essere un gateway che si desidera origini dati di test tooyour tooconnect durante lo sviluppo e un gateway diversi per le origini dati di produzione. Azure Machine Learning offre la flessibilità tooset di più gateway in base all'ambiente aziendale. Attualmente, tuttavia, non è possibile condividere un gateway tra più aree di lavoro e in un computer è possibile installare un solo gateway. Per altre informazioni, vedere [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](../data-factory/data-factory-move-data-between-onprem-and-cloud.md).

### <a name="step-2-use-hello-gateway-tooread-data-from-an-on-premises-data-source"></a>Passaggio 2: Utilizzare hello gateway tooread dati da un'origine dati locale
Dopo aver configurato il gateway di hello, è possibile aggiungere un **l'importazione dei dati** modulo da un esperimento che inserisce dati hello dal database di SQL Server on-premise hello.

1. In Machine Learning Studio, selezionare hello **ESPERIMENTI** scheda, fare clic su **+ nuovo** in hello angolo inferiore sinistro e selezionare **esperimento vuoto** (o selezionare una delle diverse di esempio esperimenti disponibili).
2. Individuare e trascinare hello **l'importazione dei dati** toohello modulo provare l'area di disegno.
3. Fare clic su **salvare come** sotto l'area di disegno hello. Immettere "Azure Machine Learning locale esercitazione su SQL Server" per il nome di hello esperimento, selezionare l'area di lavoro e fare clic su hello **OK** segno di spunta.

   ![Salvare l'esperimento con un nuovo nome](media/machine-learning-use-data-from-an-on-premises-sql-server/experiment-save-as.png)
4. Fare clic su hello **l'importazione dei dati** tooselect modulo, quindi nella **proprietà** toohello riquadro a destra dell'area di disegno hello, selezionare "Database SQL locale" hello **origine dati** elenco a discesa.
5. Seleziona hello **gateway dati** è stato installato e registrato. È possibile configurare un altro gateway selezionando l'opzione che consente di aggiungere un nuovo gateway dati.

   ![Selezionare il gateway dati per il modulo Import Data](media/machine-learning-use-data-from-an-on-premises-sql-server/import-data-select-on-premises-data-source.png)
6. Immettere hello SQL **nome server Database** e **nome del Database**, insieme a hello SQL **query Database** desiderato tooexecute.
7. Fare clic su **Enter values** (Immetti valori) in **User name and password** (Nome utente e password) e specificare le credenziali del database. È possibile usare Autenticazione integrata di Windows o Autenticazione di SQL Server, in base al tipo di configurazione del database SQL Server locale.

   ![Immettere le credenziali del database](media/machine-learning-use-data-from-an-on-premises-sql-server/database-credentials.png)

   messaggio Hello modifiche "valori richiesti" troppo "valori impostati" con un segno di spunta verde. È necessario solo credenziali hello tooenter una volta a meno che non cambia password o informazioni sul database hello. Azure Machine Learning Usa certificato hello specificato durante l'installazione le credenziali di hello hello gateway tooencrypt nel cloud hello. Azure non archivia mai credenziali locali senza crittografia.

   ![Proprietà del modulo Import Data](media/machine-learning-use-data-from-an-on-premises-sql-server/import-data-properties-entered.png)
8. Fare clic su **eseguire** esperimento hello toorun.

Una volta esperimento hello al termine dell'esecuzione, è possibile visualizzare dati hello importati dal database hello facendo hello porta di output di hello **l'importazione dei dati** modulo e selezionando **Visualizza**.

Dopo aver completato lo sviluppo dell'esperimento, è possibile distribuire il modello e renderlo operativo. Utilizzando hello servizio esecuzione Batch, i dati dal database di SQL Server on-premise hello configurato in hello **l'importazione dei dati** modulo verrà letti e utilizzato per il punteggio. Sebbene sia possibile utilizzare hello servizio risposta richiesta per l'assegnazione dei punteggi dei dati locali, Microsoft consiglia di usare il [il componente aggiuntivo Excel](machine-learning-excel-add-in-for-web-services.md) invece. Attualmente, la scrittura tooan locale il database di SQL Server tramite **Esporta dati** non servizi web è supportata in esperimenti o pubblicato.
