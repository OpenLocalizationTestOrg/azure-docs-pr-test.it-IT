---
title: dati aaaAnalyze con Azure Machine Learning | Documenti Microsoft
description: Utilizzare Azure Machine Learning toobuild un stima modello di machine learning basato sui dati archiviati in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 95635460-150f-4a50-be9c-5ddc5797f8a9
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 03/02/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 337a2cd77aaad4467683827c56e5015b262b2554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a>Analizzare i dati con Azure Machine Learning
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Questa esercitazione Usa Azure Machine Learning toobuild un stima modello di machine learning basato sui dati archiviati in Azure SQL Data Warehouse. In particolare, si compila una campagna di marketing di Adventure Works, shop bike hello, per stimare se un cliente è toobuy probabilmente una bicicletta o non.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a>Prerequisiti
toostep di questa esercitazione, è necessario:

* Un'istanza di SQL Data Warehouse in cui sia precaricato il database di esempio AdventureWorksDW. tooprovision questa operazione, vedere [creare un Data Warehouse SQL] [ Create a SQL Data Warehouse] e selezionare i dati di esempio hello tooload. Se si ha già un data warehouse, ma non i dati di esempio, è possibile [caricare manualmente i dati di esempio][load sample data manually].

## <a name="1-get-hello-data"></a>1. Ottenere dati hello
dati Hello sono nella visualizzazione dbo.vTargetMail hello nel database AdventureWorksDW hello. tooread dati:

1. Accedere ad [Azure Machine Learning Studio][Azure Machine Learning studio] e fare clic sugli esperimenti personali.
2. Fare clic su **+NEW** e selezionare **Esperimento vuoto**.
3. Immettere un nome per l'esperimento: Marketing mirato.
4. Hello trascinare **lettore** modulo dal riquadro moduli hello in canvas hello.
5. Specificare i dettagli di hello del database di SQL Data Warehouse nel riquadro Proprietà hello.
6. Specificare il database di hello **query** dati hello tooread di interesse.

```sql
SELECT [CustomerKey]
  ,[GeographyKey]
  ,[CustomerAlternateKey]
  ,[MaritalStatus]
  ,[Gender]
  ,cast ([YearlyIncome] as int) as SalaryYear
  ,[TotalChildren]
  ,[NumberChildrenAtHome]
  ,[EnglishEducation]
  ,[EnglishOccupation]
  ,[HouseOwnerFlag]
  ,[NumberCarsOwned]
  ,[CommuteDistance]
  ,[Region]
  ,[Age]
  ,[BikeBuyer]
FROM [dbo].[vTargetMail]
```

Eseguire l'esperimento hello facendo **eseguire** sotto l'area di disegno di hello esperimento.
![Eseguire l'esperimento hello][1]

Al termine esperimento hello eseguite correttamente, fare clic sulla porta di output di hello nella parte inferiore di hello del modulo del lettore hello e selezionare **Visualizza** toosee hello importati i dati.
![Visualizzare i dati importati][3]

## <a name="2-clean-hello-data"></a>2. Dati hello pulita
dati hello tooclean, eliminare alcune colonne non rilevanti per il modello di hello. toodo questo:

1. Hello trascinare **Project Columns** modulo nell'area di disegno hello.
2. Fare clic su **selettore di colonna avvio** in hello proprietà riquadro toospecify le colonne che si desidera toodrop.
   ![Project Columns][4]
3. Escludere due colonne: CustomerAlternateKey e GeographyKey.
   ![Rimuovere le colonne non necessarie][5]

## <a name="3-build-hello-model"></a>3. Compilare il modello di hello
Si suddividerà hello dati 80: 20: 80% tootrain un modello di machine learning e 20% tootest hello modello. Verrà utilizzare algoritmi di "Two-Class" hello per questo problema di classificazione binaria.

1. Hello trascinare **Split** modulo nell'area di disegno hello.
2. Immettere 0,8 per la frazione di righe in hello primo output set di dati nel riquadro Proprietà hello.
   ![Dividere i dati in set di traning e di test][6]
3. Hello trascinare **Two-Class Boosted Decision Tree** modulo nell'area di disegno hello.
4. Hello trascinare **Train Model** modulo in hello area di disegno e specificare gli input hello. Quindi, fare clic su **selettore di colonna avvio** nel riquadro Proprietà hello.
   * Primo input: algoritmo ML.
   * Secondo input: algoritmo hello tootrain dei dati in.
     ![Connettersi modulo Train Model hello][7]
5. Seleziona hello **BikeBuyer** colonna come colonna toopredict hello.
   ![Selezionare una colonna toopredict][8]

## <a name="4-score-hello-model"></a>4. Modello di punteggio hello
A questo punto, si testerà il modello di hello esegue sui dati di test. Confronteremo algoritmo hello scelto con un algoritmo diverso di toosee che offre prestazioni migliori.

1. Trascinare **Score Model** modulo nell'area di disegno hello.
    Primo input: training del modello secondo input: dati di Test ![Score model hello][9]
2. Hello trascinare **Two-Class Bayes Point Machine** nell'area di disegno di hello esperimento. Confronteremo modalità di funzionamento di questo algoritmo in confronto toohello Two-Class Boosted Decision Tree.
3. Copia e Incolla hello moduli Train Model e Score Model hello area di disegno.
4. Hello trascinare **Evaluate Model** modulo negli algoritmi di hello canvas toocompare hello due.
5. **Eseguire** hello esperimento.
   ![Eseguire l'esperimento hello][10]
6. Fare clic sulla porta di output di hello nella parte inferiore di hello del modulo Evaluate Model hello e fare clic su Visualizza.
   ![Visualizzare i risultati della valutazione][11]

metriche Hello fornite sono curve ROC hello, precisione, richiamo diagramma e accuratezza curva. Analizzando queste metriche, possiamo vedere che primo modello hello eseguita meglio di hello secondo. toolook in hello cosa hello primo modello previsto, fare clic sulla porta di output di hello Score Model e fare clic su Visualizza.
![Visualizzare i risultati di punteggio][12]

Verrà visualizzato che il set di test tooyour di aggiunto altre due colonne.

* Probabilità con punteggi: probabilità hello che un cliente è un acquirente di biciclette.
* Etichette con punteggio: hello classificazione eseguita dal modello hello – acquirente di biciclette (1) o non (0). Questa soglia di probabilità per le etichette è impostata too50% e può essere modificata.

Confronto tra la colonna hello BikeBuyer (effettivo) con hello Scored Labels (stima), è possibile visualizzare l'accuratezza modello di hello è ha eseguito. Come passaggi successivi, è possibile utilizzare le stime toomake questo modello per i nuovi clienti e pubblicare questo modello come un servizio web o scrivere risultati indietro tooSQL Data Warehouse.

## <a name="next-steps"></a>Passaggi successivi
toolearn creazione predittivo modelli di machine learning, vedere troppo[tooMachine introduzione di apprendimento in Azure][Introduction tooMachine Learning on Azure].

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img1_reader.png
[2]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img2_visualize.png
[3]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img3_readerdata.png
[4]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img4_projectcolumns.png
[5]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img5_columnselector.png
[6]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img6_split.png
[7]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img7_train.png
[8]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img8_traincolumnselector.png
[9]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img9_score.png
[10]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img10_evaluate.png
[11]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img11_evalresults.png
[12]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img12_scoreresults.png


<!--Article references-->
[Azure Machine Learning studio]:https://studio.azureml.net/
[Introduction tooMachine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
