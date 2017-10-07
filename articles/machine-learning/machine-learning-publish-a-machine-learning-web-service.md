---
title: un servizio web Machine Learning aaaDeploy | Documenti Microsoft
description: Come tooconvert training provare tooa predittiva esperimento, prepararlo per la distribuzione, quindi distribuirla come servizio web di Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 73a3e9c6-00d0-41d4-8cf1-2ec87713867e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9cb7af637632b2c3688c11483f29cf24df8fd065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-machine-learning-web-service"></a>Distribuire un servizio Web di Azure Machine Learning
Azure Machine Learning consente toobuild, testare e distribuire soluzioni di analisi predittive.

In generale, questo avviene in tre passaggi:

* **[Creare un esperimento di training]**  -Azure Machine Learning Studio è un ambiente di sviluppo visivo collaborativo utilizzare tootrain e testare un analitica predittiva del modello utilizzando i dati di training fornito.
* **[Convertirlo esperimento predittiva tooa]**  : dopo il training del modello con i dati esistenti e si è pronti toouse è tooscore nuovi dati, la preparazione e semplificare l'esperimento per le stime.
* **[Distribuire come servizio Web]** - È possibile distribuire l'esperimento predittivo come servizio Web di Azure [nuovo] o [classico]. Gli utenti possono inviare modello tooyour dati e stime del modello di ricezione.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="create-a-training-experiment"></a>Creare un esperimento di training
tootrain un modello analitica predittiva, si utilizza Azure Machine Learning Studio toocreate un esperimento di training, in cui si includono dati di training tooload moduli diversi, preparare i dati di hello in base alle esigenze, applicano algoritmi di machine learning e valutare i risultati di hello . È possibile eseguire l'iterazione in un esperimento e provare diversi di machine learning toocompare algoritmi e valutare i risultati di hello.

Hello di creare e gestire esperimenti di training viene descritto in modo più approfondito in un' posizione. Per altre informazioni, vedere questi articoli:

* [Creare un semplice esperimento in Azure Machine Learning Studio](machine-learning-create-experiment.md)
* [Sviluppare una soluzione predittiva con Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)
* [Importare dati di training in Azure Machine Learning Studio](machine-learning-data-science-import-data.md)
* [Gestire iterazioni dell'esperimento in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md)

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a>Convertire l'esperimento predittiva tooa di hello esperimento di training
Dopo aver eseguito il training del modello, si è pronti tooconvert sperimentare il training in un esperimento predittiva tooscore nuovi dati.

Convertendo tooa predittiva sperimentare, si riceve il toobe pronto modello con training distribuito come un servizio web di assegnazione dei punteggi. Gli utenti del servizio web hello possono inviare dati di input tooyour modello e il modello invierà i risultati di stima hello indietro. Durante la conversione tooa predittiva sperimentare, tenere presenti come si prevede che il modello toobe usato da altri utenti.

tooconvert il tooa esperimento di training predittiva sperimentare, fare clic su **eseguire** nella parte inferiore di hello dell'area di disegno esperimento hello, fare clic su **di servizio Web**, quindi selezionare **predittiva servizio Web** .

![Convertire l'esperimento tooscoring](./media/machine-learning-publish-a-machine-learning-web-service/figure-1.png)

Per ulteriori informazioni su come tooperform questa conversione, vedere [come tooprepare il modello per la distribuzione in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).

Hello passaggi seguenti descrivono la distribuzione di un esperimento predittivo come un nuovo servizio web. È inoltre possibile distribuire hello esperimento come servizio web classica.

## <a name="deploy-it-as-a-web-service"></a>Distribuire l'esperimento predittivo come servizio Web

È possibile distribuire esperimento predittiva hello come un nuovo servizio web o come un servizio web classica.

### <a name="deploy-hello-predictive-experiment-as-a-new-web-service"></a>Distribuire l'esperimento predittiva hello come un nuovo servizio web
Ora che è stata preparata esperimento predittiva hello, è possibile distribuirlo come un nuovo servizio web di Azure. Usa servizio web hello, gli utenti possono inviare modello tooyour dati modello hello restituirà le previsioni.

toodeploy sperimentare il predittiva, fare clic su **eseguire** nella parte inferiore di hello di hello provare l'area di disegno. Al termine dell'esecuzione esperimento hello, fare clic su **distribuzione servizio Web** e selezionare **distribuzione servizio Web [New]**.  verrà visualizzata la pagina distribuzione Hello del portale di servizio Web di Machine Learning hello.

> [!NOTE] 
> un nuovo servizio web deve disporre di autorizzazioni sufficienti in hello toowhich di sottoscrizione per la distribuzione del servizio web hello toodeploy. Per ulteriori informazioni, vedere [gestire un servizio Web tramite il portale di servizi Web di Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

#### <a name="machine-learning-web-service-portal-deploy-experiment-page"></a>Pagina di distribuzione dell'esperimento del portale dei servizi Web di Machine Learning
Nella pagina distribuzione esperimento hello, immettere un nome per il servizio web hello.
Selezionare un piano tariffario. Se si dispone di un piano tariffario esistente che è possibile selezionarlo, in caso contrario è necessario creare un nuovo piano di prezzo per servizio hello.

1. In hello **prezzo piano** elenco a discesa, selezionare un piano esistente o hello **Seleziona nuovo piano** opzione.
2. In **nome piano**, digitare un nome che identifichi il piano di hello nella fattura.
3. Selezionare una delle hello **livelli di pianificazione mensile**. piano di Hello livelli predefinito toohello piani per l'area predefinita e il servizio web è distribuito toothat area.

Fare clic su **Distribuisci** hello e **delle Guide rapide** verrà visualizzata la pagina relativa al servizio web.

pagina avvio rapido del servizio web di Hello consente di ottenere accesso e informazioni aggiuntive sulle attività più comuni di hello che verranno eseguite dopo la creazione di un servizio web. Da qui è possibile accedere con facilità la pagina di prova hello e pagina di utilizzo.

<!-- ![Deploy hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)-->

#### <a name="test-your-new-web-service"></a>Testare il nuovo servizio Web
tootest il nuovo servizio web, fare clic su **testare il servizio web** nell'area attività comuni. Nella pagina di prova hello, è possibile testare il servizio web come un servizio di richiesta-risposta (RR) o un servizio esecuzione Batch (BES).

pagina di prova RR Hello Visualizza hello input, output e i parametri globali definiti per la prova di hello. servizio web di tootest hello, è possibile immettere manualmente i valori appropriati per input hello o immettere un file in formato CSV (valori) separati da virgole contenente i valori di test hello.

tootest tramite record di risorse, dalla modalità di visualizzazione elenco hello, immettere i valori appropriati per gli input hello e fare clic su **Test richiesta-risposta**. I risultati di stima vengono visualizzati nella hello toohello di colonna di output a sinistra.

![Distribuzione di servizio web hello](./media/machine-learning-publish-a-machine-learning-web-service/figure-5-test-request-response.png)

Fare clic su, il BES tootest **Batch**. Nella pagina di prova hello Batch, fare clic su Sfoglia sotto l'input dell'utente e selezionare un file CSV contenente i valori di esempio appropriato. Se non si dispone di un file CSV e che sia stato creato l'esperimento predittiva tramite Machine Learning Studio, è possibile scaricare il set di dati di hello per l'esperimento predittiva e utilizzarlo.

set di dati hello toodownload, aprire Machine Learning Studio. Aprire l'esperimento predittiva e fare clic con il pulsante destro input hello per l'esperimento. Selezionare il menu di scelta rapida hello **dataset** e quindi selezionare **scaricare**.

![Distribuzione di servizio web hello](./media/machine-learning-publish-a-machine-learning-web-service/figure-7-mls-download.png)

Fare clic su **Test**. stato di Hello del processo di esecuzione Batch Visualizza diritto toohello **processi Batch Test**.

![Distribuzione di servizio web hello](./media/machine-learning-publish-a-machine-learning-web-service/figure-6-test-batch-execution.png)

<!--![Test hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)-->

In hello **configurazione** pagina hello descrizione della modifica, title, aggiornare la chiave di account di archiviazione hello e abilitare i dati di esempio per il servizio web.

![Configurare il servizio web hello](./media/machine-learning-publish-a-machine-learning-web-service/figure-8-arm-configure.png)

Dopo aver distribuito il servizio di web hello, è possibile:

* **Accesso** tramite API del servizio web hello.
* **Gestire** tramite Azure Machine Learning portale di servizi web o hello portale di Azure classico.
* **Aggiornarlo** se il modello viene modificato.

#### <a name="access-your-new-web-service"></a>Accedere al nuovo servizio Web
Dopo aver distribuito il servizio web da Machine Learning Studio, è possibile servizio toohello dati di inviare e ricevere risposte a livello di codice.

Hello **consumare** pagina fornisce tutte le informazioni di hello tooaccess è necessario il servizio web. Ad esempio, chiave hello API viene fornita servizio toohello di accesso tooallow autorizzato.

Per ulteriori informazioni sull'accesso a un servizio web Machine Learning, vedere [come un servizio Web di Azure Machine Learning tooconsume](machine-learning-consume-web-services.md).

#### <a name="manage-your-new-web-service"></a>Gestire il nuovo servizio Web
È possibile gestire il portale dei servizi Web di Machine Learning per i nuovi servizi Web. Da hello [pagina principale del portale](https://services.azureml-test.net/), fare clic su **servizi Web**. Dalla pagina di servizi web di hello, è possibile eliminare o copiare un servizio. toomonitor un servizio specifico, fare clic su servizio hello e quindi fare clic su **Dashboard**. i processi batch toomonitor associati hello servizio web, fare clic su **Log richieste Batch**.

### <a name="deploy-hello-predictive-experiment-as-a-classic-web-service"></a>Distribuire l'esperimento predittiva hello come servizio web classica

Ora che esperimento predittiva hello sufficientemente preparato, è possibile distribuirlo come un servizio web di Azure classico. Usa servizio web hello, gli utenti possono inviare modello tooyour dati modello hello restituirà le previsioni.

toodeploy sperimentare il predittiva, fare clic su **eseguire** nella parte inferiore di hello di hello provare l'area di disegno e quindi fare clic su **distribuzione servizio Web**. servizio web di Hello sia configurato e inseriti nel dashboard del servizio web hello.

![Distribuzione di servizio web hello](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)

#### <a name="test-your-classic-web-service"></a>Testare il servizio Web classico

È possibile testare il servizio di web hello nel portale di servizi Web di Machine Learning hello o Machine Learning Studio.

hello tootest servizio web di risposta richiesta, fare clic su hello **Test** pulsante nel dashboard del servizio web hello. Una finestra di dialogo viene visualizzata tooask è per i dati di input per il servizio hello hello. Si tratta di colonne hello previste dagli hello esperimento di assegnazione dei punteggi. Immettere un set di dati e quindi fare clic su **OK**. risultati Hello generati dal servizio web hello vengono visualizzati nella parte inferiore di hello del dashboard hello.

È possibile fare clic su hello **Test** anteprima collegamento tootest il servizio nel portale di servizi Web di Azure Machine Learning hello, come illustrato in precedenza in hello nuova sezione di servizio web.

hello tootest servizio esecuzione Batch, fare clic su **Test** collegamento anteprima. Nella pagina di prova hello Batch, fare clic su Sfoglia sotto l'input dell'utente e selezionare un file CSV contenente i valori di esempio appropriato. Se non si dispone di un file CSV e che sia stato creato l'esperimento predittiva tramite Machine Learning Studio, è possibile scaricare il set di dati di hello per l'esperimento predittiva e utilizzarlo.

![Servizio web hello di test](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)

In hello **configurazione** pagina, è possibile modificare il nome visualizzato hello del servizio hello e assegnargli una descrizione. nome Hello e la descrizione viene visualizzata in hello [portale di Azure classico](http://manage.windowsazure.com/) in cui gestire i servizi web.

È anche possibile fornire una descrizione per i dati di input e output, nonché parametri del servizio Web immettendo una stringa per ogni colonna in **INPUT SCHEMA** (SCHEMA DI INPUT), **OUTPUT SCHEMA** (SCHEMA DI OUTPUT) e **Web SERVICE PARAMETER** (PARAMETRO SERVIZIO WEB). Queste descrizioni sono utilizzate nella documentazione di codice di esempio hello fornita per il servizio web hello.

È possibile abilitare la registrazione toodiagnose gli eventuali errori vengono visualizzati quando si accede a servizio web. Per altre informazioni, vedere [Abilitare la registrazione per i servizi Web di Machine Learning](machine-learning-web-services-logging.md).

![Configurare il servizio web hello](./media/machine-learning-publish-a-machine-learning-web-service/figure-4.png)

È inoltre possibile configurare gli endpoint di hello per il servizio web hello in hello servizi Web di Azure Machine Learning portale simile toohello procedura illustrata in precedenza in hello nuova sezione di servizio web. opzioni di Hello sono diverse, è possibile aggiungere o modificare una descrizione del servizio hello, abilitare la registrazione e attivare i dati di esempio per il test.

#### <a name="access-your-classic-web-service"></a>Accedere al servizio Web classico
Dopo aver distribuito il servizio web da Machine Learning Studio, è possibile servizio toohello dati di inviare e ricevere risposte a livello di codice.

dashboard Hello fornisce tutte le informazioni di hello tooaccess è necessario il servizio web. Ad esempio, la chiave API hello viene fornito tooallow autorizzato accesso toohello servizio e le pagine della Guida di API vengono fornite toohelp che iniziare la scrittura del codice.

Per ulteriori informazioni sull'accesso a un servizio web Machine Learning, vedere [come un servizio Web di Azure Machine Learning tooconsume](machine-learning-consume-web-services.md).

#### <a name="manage-your-classic-web-service"></a>Gestire il servizio Web classico
Esistono varie azioni è possibile eseguire toomonitor un servizio web. È possibile aggiornare il servizio ed eliminarlo. È anche possibile aggiungere altri endpoint tooa classica web servizio nell'endpoint di predefinito toohello aggiunta che viene creato quando viene distribuito.

Per ulteriori informazioni, vedere [gestire un'area di lavoro di Azure Machine Learning](machine-learning-manage-workspace.md) e [gestire un servizio web tramite il portale di servizi Web di Azure Machine Learning hello](machine-learning-manage-new-webservice.md).

<!-- When this article gets published, fix hello link and uncomment
For more information on how toomanage Azure Machine Learning web service endpoints using hello REST API, see **Azure machine learning web service endpoints**.
-->

## <a name="update-hello-web-service"></a>Aggiornare il servizio web hello
È possibile apportare modifiche di servizio web tooyour, ad esempio l'aggiornamento modello hello con dati di training aggiuntivi e distribuirlo di nuovo, sovrascrivendo il servizio web originale di hello.

servizio web di hello tooupdate, aprire esperimento predittiva di hello originale toodeploy hello web servizio è utilizzato e creare una copia modificabile facendo **SAVE AS**. Eseguire le modifiche e fare clic su **Distribuisci Servizio Web**.

Poiché questa sperimentazione prima di aver distribuito, viene chiesto se si desidera toooverwrite (servizio Web classico) o il servizio di aggiornamento (nuovo servizio web) hello esistente. Fare clic su **Sì** o **aggiornamento** Arresta servizio web esistente hello e distribuisce esperimento predittiva nuovo hello viene distribuito al suo posto.

> [!NOTE]
> Se sono state apportate modifiche di configurazione nel servizio web originale hello, ad esempio, immettere un nuovo nome o descrizione, è necessario tooenter tali valori nuovamente.
> 
> 

Una delle opzioni per l'aggiornamento del servizio web è il modello di hello tooretrain a livello di codice. Per altre informazioni, vedere [Ripetere il training dei modelli di Machine Learning a livello di codice](machine-learning-retrain-models-programmatically.md).

<!-- internal links -->
[Creare un esperimento di training]: #create-a-training-experiment
[Convertirlo esperimento predittiva tooa]: #convert-the-training-experiment-to-a-predictive-experiment
[Distribuire come servizio Web]: #deploy-it-as-a-web-service
[nuovo]: #deploy-the-predictive-experiment-as-a-new-Web-service
[classico]: #deploy-the-predictive-experiment-as-a-new-Web-service
[Access]: #access-the-Web-service
[Manage]: #manage-the-Web-service-in-the-azure-management-portal
[Update]: #update-the-Web-service
