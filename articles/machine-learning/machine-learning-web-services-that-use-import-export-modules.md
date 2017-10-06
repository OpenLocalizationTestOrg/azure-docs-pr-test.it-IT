---
title: aaaUsing importazione/esportazione di dati nei servizi web di Azure Machine Learning | Documenti Microsoft
description: Informazioni su come toouse hello toosend moduli dati di importazione ed esportazione di dati e ricevere dati da un servizio web.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3a7ac351-ebd3-43a1-8c5d-18223903d08e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 176380259b15cb338ede61c7f28ba2296b35dd52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a>Distribuzione di servizi di Web Azure ML che usano i moduli Import Data ed Export Data

Quando si crea un esperimento predittivo, si aggiunge in genere un input e un output del servizio Web. Quando si distribuisce l'esperimento hello, i consumer possono inviare e ricevere dati dal servizio web hello tramite hello input e output. Per alcune applicazioni, i dati del consumer possono essere disponibili da un feed di dati o risiedere già in un'origine dati esterna, ad esempio archiviazione BLOB di Azure. In questi casi non è necessario leggere e scrivere dati usando gli input e gli output del servizio Web . Possono, in alternativa, utilizzare dati tooread di hello servizio esecuzione Batch (BES) dall'origine dati hello mediante un modulo di importazione dei dati e scrivere hello punteggio percorso dati diversi tooa mediante un modulo di esportare dati di risultati.

Hello l'importazione dei dati e i moduli di dati di esportazione, possono leggere e scrivere dati toovarious forniscono percorsi, ad esempio un URL Web tramite HTTP, una Query Hive, un database SQL di Azure, archiviazione tabelle di Azure, archiviazione Blob di Azure, un Feed di dati o un database SQL locale.

In questo argomento utilizza hello "esempio 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" di esempio e presuppone che il dataset hello è già stato caricato in una tabella di SQL Azure denominata censusdata.

## <a name="create-hello-training-experiment"></a>Creare l'esperimento di training hello
Quando si apre hello "esempio 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" esempio di set di dati utilizza hello campione la classificazione binaria per adulti Census reddito. Ed esperimento hello nell'area di disegno hello avrà un aspetto simile toohello seguente immagine:

![Configurazione iniziale di sperimentazione hello.](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

dati di hello tooread dalla tabella di SQL Azure hello:

1. Eliminare il modulo di hello set di dati.
2. Nella casella di ricerca di componenti hello, tipo di importazione.
3. Dall'elenco dei risultati di hello, aggiungere un *l'importazione dei dati* toohello modulo provare l'area di disegno.
4. Connettere l'output di hello *l'importazione dei dati* input hello modulo di hello *Clean Missing Data* modulo.
5. Nel riquadro Proprietà selezionare **Database SQL di Azure** in hello **origine dati** elenco a discesa.
6. In hello **nome server Database**, **nome del Database**, **nome utente**, e **Password** campi, immettere le informazioni appropriate per hello il database.
7. Nel campo della query Database hello immettere hello seguente query.
   
     select [age],
   
        [workclass],
        [fnlwgt],
        [education],
        [education-num],
        [marital-status],
        [occupation],
        [relationship],
        [race],
        [sex],
        [capital-gain],
        [capital-loss],
        [hours-per-week],
        [native-country],
        [income]
     from dbo.censusdata;
8. Nella parte inferiore di hello dell'area di disegno esperimento hello, fare clic su **eseguire**.

## <a name="create-hello-predictive-experiment"></a>Creare l'esperimento predittiva hello
Successivamente impostare esperimento predittiva di hello da cui si distribuisce il servizio web.

1. Nella parte inferiore di hello dell'area di disegno esperimento hello, fare clic su **di servizio Web** e selezionare **predittiva servizio Web (scelta consigliata)**.
2. Rimuovere hello *Input del servizio Web* e *moduli di Output del servizio Web* da esperimento predittiva hello. 
3. Nella casella di ricerca di componenti hello, tipo di esportazione.
4. Dall'elenco dei risultati di hello, aggiungere un *Esporta dati* toohello modulo provare l'area di disegno.
5. Connettere l'output di hello *Score Model* input hello modulo di hello *Esporta dati* modulo. 
6. Nel riquadro Proprietà selezionare **Database SQL di Azure** nell'elenco a discesa destinazione di dati hello.
7. In hello **nome server Database**, **nome del Database**, **nome dell'account utente Server**, e **password dell'account utente Server** immettere informazioni appropriate Hello per il database.
8. In hello **elenco delimitato da virgole di colonne toobe salvato** digitare Scored Labels.
9. In hello **campo Nome tabella di dati**, digitare dbo. ScoredLabels. Se la tabella hello non esiste, viene creato quando viene eseguito l'esperimento hello o servizio web hello viene chiamato.
10. In hello **elenco delimitato da virgole delle colonne di datatable** campo digitare ScoredLabels.

Quando si scrive un'applicazione che chiama hello servizio web finale, è opportuno toospecify un'altra tabella di query o di destinazione input in fase di esecuzione. tooconfigure questi input e output, utilizzare hello tooset funzionalità parametri del servizio Web di hello *l'importazione dei dati* modulo *origine dati* proprietà e hello *Esporta dati* modalità proprietà destinazione dei dati.  Per ulteriori informazioni sui parametri di servizio Web, vedere hello [voce parametri del servizio Web Azure ml](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) hello Intelligence Cortana e Blog di Machine Learning.

per le query di importazione hello e tabella di destinazione hello tooconfigure hello parametri del servizio Web:

1. Nel riquadro Proprietà hello hello *l'importazione dei dati* modulo, fare clic sull'icona hello hello in alto a destra di hello **query Database** campo e selezionare **come parametro di servizio web**.
2. Nel riquadro Proprietà hello hello *Esporta dati* modulo, fare clic sull'icona hello hello in alto a destra di hello **nome della tabella dati** campo e selezionare **come parametro di servizio web**.
3. Nella parte inferiore di hello di hello *Esporta dati* hello riquadro Proprietà modulo **parametri del servizio Web** sezione, fare clic su query di Database e rinominare la cartella Query.
4. Fare clic su **Data table name** (Nome tabella dati) e rinominare in **Table** (Tabella).

Al termine, l'esperimento dovrebbe essere simile toohello seguente immagine:

![Risultato finale dell'esperimento.](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

È ora possibile distribuire hello esperimento come servizio web.

## <a name="deploy-hello-web-service"></a>Distribuzione di servizio web hello
È possibile distribuire tooeither un servizio web classica o nuovo.

### <a name="deploy-a-classic-web-service"></a>Distribuire un servizio Web classico
toodeploy come servizio Web classico e creare un'applicazione tooconsume è:

1. Nella parte inferiore di hello dell'area di disegno esperimento hello, fare clic su Esegui.
2. Al termine dell'esecuzione hello, fare clic su **distribuzione servizio Web** e selezionare **distribuzione di un servizio Web [classica]**.
3. Nel dashboard del servizio web hello, individuare la chiave API. Copiare e salvarlo toouse in un secondo momento.
4. In hello **Endpoint predefinito** tabella, fare clic su hello **esecuzione Batch** hello tooopen collegamento pagina della Guida di API.
5. In Visual Studio creare un'applicazione console C#. A tale scopo, selezionare **Nuovo** > **Progetto** > **Visual C#** > **Desktop classico di Windows** > **Applicazione console (.NET Framework)**.
6. Nella pagina della Guida API hello, trovare hello **codice di esempio** sezione hello parte inferiore della pagina hello.
7. Copiare e incollare hello c# il codice di esempio nel file Program.cs e rimuovere tutti gli archivi blob toohello di riferimenti.
8. Aggiornare il valore di hello di hello *apiKey* variabile con la chiave API hello salvato in precedenza.
9. Individuare hello richiesta dichiarazione e l'aggiornamento hello valori dei parametri del servizio Web che vengono passati toohello *l'importazione dei dati* e *Esporta dati* moduli. In questo caso, utilizzare la query originale hello ma definire un nuovo nome di tabella.
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. Eseguire un'applicazione hello. 

Al termine dell'esecuzione di hello, database toohello contenente i risultati di punteggio hello è aggiunto a una nuova tabella.

### <a name="deploy-a-new-web-service"></a>Distribuire un servizio Web nuovo

> [!NOTE] 
> un nuovo servizio web deve disporre di autorizzazioni sufficienti in hello toowhich di sottoscrizione per la distribuzione del servizio web hello toodeploy. Per ulteriori informazioni, vedere [gestire un servizio Web tramite il portale di servizi Web di Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

toodeploy come un nuovo servizio Web e creare un'applicazione tooconsume è:

1. Nella parte inferiore di hello dell'area di disegno esperimento hello, fare clic su **eseguire**.
2. Al termine dell'esecuzione hello, fare clic su **distribuzione servizio Web** e selezionare **distribuzione servizio Web [New]**.
3. Selezionare un piano tariffario, nella pagina di distribuire esperimento hello, immettere un nome per il servizio web, quindi fare clic su **Distribuisci**.
4. In hello **delle Guide rapide** pagina, fare clic su **consumare**.
5. In hello **codice di esempio** fare clic su **Batch**.
6. In Visual Studio creare un'applicazione console C#. A tale scopo, selezionare **Nuovo** > **Progetto** > **Visual C#** > **Desktop classico di Windows** > **Applicazione console (.NET Framework)**.
7. Copiare e incollare codice di esempio hello c# nel file Program.cs.
8. Aggiornare il valore di hello di hello *apiKey* variabile con hello **chiave primaria** si trova in hello **informazioni di base al consumo** sezione.
9. Individuare hello *scoreRequest* dichiarazione e aggiornare i valori hello dei parametri del servizio Web che vengono passati toohello *l'importazione dei dati* e *Esporta dati* moduli. In questo caso, utilizzare la query originale hello ma definire un nuovo nome di tabella.
   
        var scoreRequest = new
        {       
            Inputs = new Dictionary<string, StringTable>()
            {
            },
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable3" },
            }
        };
10. Eseguire un'applicazione hello. 

