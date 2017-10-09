---
title: gli assembly aaaDevelop U-SQL per i processi di Azure Data Lake Analitica | Documenti Microsoft
description: 'Informazioni su come toodevelop assembly toobe utilizzato e riutilizzate in Data Lake Analitica processi. '
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/30/2016
ms.author: jejiang
ms.openlocfilehash: 86dd17b25e0967306ed36bb5b7f3178d9409d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a>Sviluppare assembly U-SQL per processi di Azure Data Lake Analytics
Informazioni su come tooturn codice nell'assembly toobe utilizzato e riutilizzati in processi di Data Lake Analitica. 

U-SQL rende facile tooadd personalizzati di codice in linguaggi .net, ad esempio c#, Visual Basic.NET o F #. È anche possibile distribuire la propria toosupport runtime altri linguaggi.

codice personalizzato di Hello più semplice modo toouse è toouse hello Data Lake Tools per la funzionalità di codice di Visual Studio. Per altre informazioni, vedere [Esercitazione: Sviluppare script U-SQL tramite Strumenti di Data Lake per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md). L'uso di code-behind presenta alcuni svantaggi:

- codice sorgente Hello viene caricato per l'invio di ogni script.
- Non è possibile condividere code-behind con altri processi.

tooaddress questi svantaggi, è possibile attivare codice negli assembly e registrare catalogo di hello assembly toohello Data Lake Analitica.

## <a name="prerequisites"></a>Prerequisiti
* Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 aggiornamento 4 o Visual Studio 2012 con Visual C++ installato
* Microsoft Azure SDK per .NET versione 2.5 o successiva.  Installazione mediante Installazione guidata piattaforma Web di hello o programma di installazione di Visual Studio
* Un account di Analisi Data Lake.  Vedere [Introduzione ad Azure Data Lake Analytics con il Portale di Azure](data-lake-analytics-get-started-portal.md).
* Seguire i passaggi hello [Guida introduttiva di Azure Data Lake Analitica U-SQL Studio](data-lake-analytics-u-sql-get-started.md) esercitazione.
* Connettersi tooAzure.
* Caricare i dati di origine hello, vedere [Guida introduttiva di Azure Data Lake Analitica U-SQL Studio](data-lake-analytics-u-sql-get-started.md). 

## <a name="develop-assemblies-for-u-sql"></a>Sviluppare assembly per U-SQL

**toocreate e inviare un processo U-SQL**

1. Da hello **File** menu, fare clic su **New**, quindi fare clic su **progetto**.
2. Espandere **installato**, **modelli**, **Azure Data Lake**, **U-SQL(ADLA)**selezionare hello **libreria di classi (per U-SQL Applicazione)** modello e quindi fare clic su **OK**.
3. Scrivere il codice in Class1.cs.  di seguito Hello è un esempio di codice.

        using Microsoft.Analytics.Interfaces;

        namespace USQLApplication_codebehind
        {
            [SqlUserDefinedProcessor]
            public class MyProcessor : IProcessor
            {
                public override IRow Process(IRow input, IUpdatableRow output)
                {
                    output.Set(0, input.Get<string>(0));
                    output.Set(0, input.Get<string>(0));
                    return output.AsReadOnly();
                }
            }
        }
4. Fare clic su hello **compilare** menu e quindi fare clic su **Compila soluzione** toocreate hello dll.

## <a name="register-assemblies"></a>Registrazione di assembly

Vedere [Usare il catalogo Data Lake Analytics(U-SQL)](data-lake-analytics-use-u-sql-catalog.md).


## <a name="use-hello-assemblies"></a>Utilizzare assembly hello

Vedere [utilizzare hello Azure Data Lake Tools per Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).

## <a name="see-also"></a>Vedere anche
* [Introduzione ad Analisi Data Lake di Azure mediante Azure PowerShell](data-lake-analytics-get-started-powershell.md)
* [Introduzione a Data Lake Analitica utilizzando hello portale di Azure](data-lake-analytics-get-started-portal.md)
* [Utilizzare gli strumenti Data Lake per Visual Studio per lo sviluppo di applicazioni U-SQL](data-lake-analytics-data-lake-tools-get-started.md)
* [Usare il catalogo Data Lake Analytics(U-SQL)](data-lake-analytics-use-u-sql-catalog.md)
* [Utilizzare hello Azure Data Lake Tools per Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md)
