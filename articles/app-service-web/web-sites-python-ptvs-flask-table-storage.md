---
title: aaaFlask e l'archiviazione tabelle di Azure in Azure con Python Tools 2.2 per Visual Studio
description: Informazioni su come toouse hello Python Tools per Visual Studio toocreate un'app web pallone che archivia i dati nell'archiviazione tabelle di Azure e distribuirlo tooAzure App del servizio Web App.
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: d8e70a29-aca1-4010-95f5-cfe769e3be06
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1a09d4cc78078a00492ba4fe7e2075df96fb0380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="flask-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a>Flask e archiviazione tabelle di Azure con Python Tools 2.2 per Visual Studio
In questa esercitazione si userà [Python Tools per Visual Studio] toocreate una semplice app web utilizzando uno dei modelli di esempio hello PTVS esegue il polling. Questa esercitazione è anche disponibile in formato [video](https://www.youtube.com/watch?v=qUtZWtPwbTk).

app web viene eseguito il polling di Hello definisce un'astrazione per il relativo repository, pertanto è possibile passare facilmente tra diversi tipi di repository (In memoria, archiviazione tabelle di Azure, MongoDB).

Si apprenderà come account di toocreate una risorsa di archiviazione di Azure, come tooconfigure hello web app toouse archiviazione tabelle di Azure e come toopublish hello app web troppo[App Web di servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

Vedere hello [Centro per sviluppatori Python] per ulteriori articoli che coprono lo sviluppo di App del servizio Web App di Azure con PTVS utilizzando Bottle pallone e Django web Framework, con i servizi di MongoDB, archiviazione tabelle di Azure, MySQL e SQL Database. Durante questo articolo è incentrato sul servizio App, i passaggi di hello sono simili durante lo sviluppo di [servizi Cloud di Azure].

## <a name="prerequisites"></a>Prerequisiti
* Visual Studio 2015
* [Python Tools 2.2 per Visual Studio]
* [Python Tools 2.2 per Visual Studio esempi VSIX]
* [Strumenti di Azure SDK per Visual Studio 2015]
* [Python 2.7 a 32 bit] o [Python 3.4 a 32 bit]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="create-hello-project"></a>Creare hello progetto
In questa sezione verrà creato un progetto di Visual Studio usando un modello di esempio. Verrà creato un ambiente virtuale e verranno installati i pacchetti necessari. Viene quindi eseguito localmente utilizzando i repository di hello predefinito in memoria un'applicazione hello.

1. In Visual Studio selezionare **File**, **Nuovo progetto**.
2. modelli di progetto da hello Hello [Python Tools 2.2 per Visual Studio esempi VSIX] sono disponibili in **Python**, **esempi**. Selezionare **progetto Web di polling pallone** e fare clic su OK toocreate hello progetto.
   
     ![Finestra di dialogo Nuovo progetto](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskNewProject.png)
3. Sarà richiesto tooinstall i pacchetti esterni. Selezionare **Installa in un ambiente virtuale**.
   
     ![Finestra di dialogo dei pacchetti esterni](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskExternalPackages.png)
4. Selezionare **Python 2.7** o **Python 3.4** come interprete base hello.
   
     ![Finestra di dialogo Aggiungi ambiente virtuale](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAddVirtualEnv.png)
5. Verificare che l'applicazione hello funzioni premendo `F5`. Per impostazione predefinita, un'applicazione hello utilizza un archivio in memoria che non richiede alcuna configurazione. Tutti i dati viene persa quando hello del server web.
6. Fare clic su **Crea sondaggio di esempio**, quindi fare clic su un sondaggio e su un voto.
   
     ![Web browser](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a>Creare un account di Archiviazione di Azure
le operazioni di archiviazione toouse, è necessario un account di archiviazione di Azure. Per creare un account di archiviazione, attenersi alla procedura riportata di seguito

1. Accedere al hello [portale Azure](https://portal.azure.com/).
2. Fare clic su hello **New** sull'icona nella parte superiore di hello a sinistra della hello portale, quindi fare clic su **dati e archiviazione** > **Account di archiviazione**. Fare clic su **crea**, quindi assegnare un nome univoco di account di archiviazione hello e creare un nuovo [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) relativo.
   
      ![Quick Create](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageCreate.png)
   
    Quando è stato creato l'account di archiviazione hello, hello **notifiche** pulsante farà lampeggiare una verde **esito positivo** ed è aperto il pannello dell'account di archiviazione hello gruppo tooshow appartiene toohello nuova risorsa creato.
3. Fare clic su hello **chiavi di accesso** parte nel pannello hello account di archiviazione. Prendere nota del nome dell'account hello e key1 hello.
   
      ![Chiavi](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageKeys.png)
   
    È necessario questo tooconfigure informazioni nella sezione successiva hello del progetto.

## <a name="configure-hello-project"></a>Configurare hello progetto
In questa sezione, è possibile configurare l'account di archiviazione applicazione toouse hello che appena creato. Si noterà come le impostazioni di connessione tooobtain hello portale di Azure. Quindi verrà eseguito in locale un'applicazione hello.

1. In Visual Studio fare clic con il pulsante destro del mouse sul nodo del progetto in Esplora soluzioni e scegliere **Proprietà**. Fare clic su hello **Debug** scheda.
   
     ![Impostazioni di debug del progetto](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageProjectDebugSettings.png)
2. Impostare i valori hello delle variabili di ambiente richieste da un'applicazione hello in **comando Server Debug**, **ambiente**.
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   Questo verrà impostato le variabili di ambiente hello quando si **Avvia debug**. Se si desidera hello variabili toobe imposta quando si **Avvia senza eseguire debug**, hello set stessi valori in **esecuzione del comando Server** anche.
   
   In alternativa, è possibile definire variabili di ambiente utilizzando il pannello di controllo di Windows hello. Si tratta di un'opzione migliore se si desidera archiviare le credenziali nel codice sorgente tooavoid o file di progetto. Si noti che è necessario per nuovo ambiente valori toobe toohello disponibile un'applicazione hello toorestart Visual Studio.
3. codice Hello che implementa il repository di archiviazione tabelle di Azure hello è **models/azuretablestorage.py**. Vedere hello [documentazione] per ulteriori informazioni su come toouse del servizio tabelle da Python.
4. Eseguire un'applicazione hello con `F5`. Esegue il polling creati con **creare sondaggi esempio** e dati hello inviati dai voti verranno serializzati nell'archiviazione tabelle di Azure.
   
   > [!NOTE]
   > Ambiente virtuale di Python 2.7 Hello può causare un'interruzione di eccezioni in Visual Studio.  Premere `F5` toocontinue durante il caricamento di progetto web hello.
   > 
   > 
5. Sfoglia toohello **su** tooverify pagina che hello applicazione utilizza hello **archiviazione tabelle di Azure** repository.
   
     ![Web browser](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a>Esplorare hello archiviazione tabelle di Azure
È facile tooview e modificare le tabelle di archiviazione con Cloud Explorer in Visual Studio. In questa sezione si userà contenuto hello tooview di Esplora Server delle tabelle di applicazione hello viene eseguito il polling.

> [!NOTE]
> Questo richiede toobe strumenti di Microsoft Azure installato, che sono disponibili come parte di hello [Azure SDK per .NET].
> 
> 

1. Aprire **Cloud Explorer**. Espandere **Account di archiviazione**, l'account di archiviazione di riferimento e quindi **Tabelle**.
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. Fare doppio clic su hello **sondaggi** o **scelte** contenuto hello tooview della tabella hello in una finestra del documento, nonché aggiungere, rimuovere o modificare entità di tabella.
   
     ![Risultati della query relativa alla tabella](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a>Pubblicare hello web app tooAzure servizio App
Hello Azure .NET SDK fornisce un modo semplice di toodeploy il tooAzure app web del servizio App.

1. In **Esplora**, fare clic sul nodo del progetto hello e selezionare **pubblica**.
   
     ![Finestra di dialogo Pubblica sito Web](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. Fare clic su **App Web di Microsoft Azure**.
3. Fare clic su **New** toocreate una nuova app web.
4. Compilare hello seguente i campi e fare clic su **crea**.
   
   * **Nome dell'app Web**
   * **Piano di servizio app**
   * **Gruppo di risorse**
   * **Area**
   * Lasciare **server di Database** impostare troppo**alcun database**
5. Accettare tutte le altre impostazioni predefinite e fare clic su **Pubblica**.
6. Web browser verrà aperto automaticamente toohello pubblicato web app. Se si seleziona toohello sulla pagina, si noterà che usa hello **In memoria** repository, non hello **archiviazione tabelle di Azure** repository.
   
   Ciò accade perché le variabili di ambiente hello non sono impostate nell'istanza di hello App Web nel servizio App di Azure, pertanto utilizza valori predefiniti di hello specificati **settings.py**.

## <a name="configure-hello-web-apps-instance"></a>Configurare l'istanza di hello App Web
In questa sezione, è possibile configurare le variabili di ambiente per istanza di hello App Web.

1. In [portale Azure](https://portal.azure.com), aprire il pannello dell'app web hello facendo **Sfoglia** > **servizi App** > nome dell'app web.
2. Nel pannello dell'app Web fare clic su **Tutte le impostazioni** e quindi su **Impostazioni applicazione**.
3. Scorrere verso il basso toohello **impostazioni App** sezione e impostare i valori hello **REPOSITORY\_nome**, **archiviazione\_nome** e  **ARCHIVIAZIONE\_chiave** come descritto in hello **progetto hello configura** sezione precedente.
   
     ![Impostazioni app](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. Fare clic su **Save**. Dopo aver ricevuto le notifiche di hello che sono state applicate le modifiche di hello, fare clic su **Sfoglia** dal pannello principale di hello Web app.
5. Dovrebbe essere funzionante di hello web app come previsto, utilizzando hello **archiviazione tabelle di Azure** repository.
   
   Congratulazioni.
   
     ![Web browser](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureBrowser.png)

## <a name="next-steps"></a>Passaggi successivi
Seguire questi toolearn collegamenti ulteriori informazioni sugli strumenti Python per Visual Studio, pallone e archiviazione tabelle di Azure.

* [Documentazione di Python Tools per Visual Studio]
  * [Progetti Web]
  * [Progetti servizio cloud]
  * [Debug remoto in Microsoft Azure]
* [Documentazione di Flask]
* [Archiviazione di Azure]
* [Azure SDK per Python]
* [Come tooUse hello del servizio di archiviazione di tabelle da Python]

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Centro per sviluppatori Python]: /develop/python/
[servizi Cloud di Azure]: ../cloud-services/cloud-services-python-ptvs.md
[documentazione]:../cosmos-db/table-storage-how-to-use-python.md
[Come tooUse hello del servizio di archiviazione di tabelle da Python]:../cosmos-db/table-storage-how-to-use-python.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Azure SDK per .NET]: http://azure.microsoft.com/downloads/
[Python Tools per Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 per Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 per Visual Studio esempi VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Strumenti di Azure SDK per Visual Studio 2015]: http://go.microsoft.com/fwlink/?linkid=518003
[Python 2.7 a 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 a 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517191
[Documentazione di Python Tools per Visual Studio]: http://aka.ms/ptvsdocs
[Documentazione di Flask]: http://flask.pocoo.org/
[Debug remoto in Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Progetti Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Progetti servizio cloud]: http://go.microsoft.com/fwlink/?LinkId=624028
[Archiviazione di Azure]: http://azure.microsoft.com/documentation/services/storage/
[Azure SDK per Python]: https://github.com/Azure/azure-sdk-for-python
