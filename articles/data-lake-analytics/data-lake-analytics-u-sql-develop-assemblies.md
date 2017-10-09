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
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a><span data-ttu-id="30270-103">Sviluppare assembly U-SQL per processi di Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="30270-103">Develop U-SQL assemblies for Azure Data Lake Analytics jobs</span></span>
<span data-ttu-id="30270-104">Informazioni su come tooturn codice nell'assembly toobe utilizzato e riutilizzati in processi di Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="30270-104">Learn how tooturn code-behind into assemblies toobe used and reused in Data Lake Analytics jobs.</span></span> 

<span data-ttu-id="30270-105">U-SQL rende facile tooadd personalizzati di codice in linguaggi .net, ad esempio c#, Visual Basic.NET o F #.</span><span class="sxs-lookup"><span data-stu-id="30270-105">U-SQL makes it easy tooadd your own custom code in .Net languages, such as C#, VB.Net or F#.</span></span> <span data-ttu-id="30270-106">È anche possibile distribuire la propria toosupport runtime altri linguaggi.</span><span class="sxs-lookup"><span data-stu-id="30270-106">You can even deploy your own runtime toosupport other languages.</span></span>

<span data-ttu-id="30270-107">codice personalizzato di Hello più semplice modo toouse è toouse hello Data Lake Tools per la funzionalità di codice di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="30270-107">hello easiest way toouse custom code is toouse hello Data Lake Tools for Visual Studio’s code-behind capabilities.</span></span> <span data-ttu-id="30270-108">Per altre informazioni, vedere [Esercitazione: Sviluppare script U-SQL tramite Strumenti di Data Lake per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="30270-108">For more information, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="30270-109">L'uso di code-behind presenta alcuni svantaggi:</span><span class="sxs-lookup"><span data-stu-id="30270-109">There are a few drawbacks of using code-behind:</span></span>

- <span data-ttu-id="30270-110">codice sorgente Hello viene caricato per l'invio di ogni script.</span><span class="sxs-lookup"><span data-stu-id="30270-110">hello source code gets uploaded for every script submission.</span></span>
- <span data-ttu-id="30270-111">Non è possibile condividere code-behind con altri processi.</span><span class="sxs-lookup"><span data-stu-id="30270-111">code-behind cannot be shared with other jobs.</span></span>

<span data-ttu-id="30270-112">tooaddress questi svantaggi, è possibile attivare codice negli assembly e registrare catalogo di hello assembly toohello Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="30270-112">tooaddress these drawbacks, you can turn code-behind into assemblies, and register hello assemblies toohello Data Lake Analytics catalog.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30270-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="30270-113">Prerequisites</span></span>
* <span data-ttu-id="30270-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 aggiornamento 4 o Visual Studio 2012 con Visual C++ installato</span><span class="sxs-lookup"><span data-stu-id="30270-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span></span>
* <span data-ttu-id="30270-115">Microsoft Azure SDK per .NET versione 2.5 o successiva.</span><span class="sxs-lookup"><span data-stu-id="30270-115">Microsoft Azure SDK for .NET version 2.5 or above.</span></span>  <span data-ttu-id="30270-116">Installazione mediante Installazione guidata piattaforma Web di hello o programma di installazione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="30270-116">Install it using hello Web platform installer or Visual Studio Installer</span></span>
* <span data-ttu-id="30270-117">Un account di Analisi Data Lake.</span><span class="sxs-lookup"><span data-stu-id="30270-117">A Data Lake Analytics account.</span></span>  <span data-ttu-id="30270-118">Vedere [Introduzione ad Azure Data Lake Analytics con il Portale di Azure](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="30270-118">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="30270-119">Seguire i passaggi hello [Guida introduttiva di Azure Data Lake Analitica U-SQL Studio](data-lake-analytics-u-sql-get-started.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="30270-119">Go through hello [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span></span>
* <span data-ttu-id="30270-120">Connettersi tooAzure.</span><span class="sxs-lookup"><span data-stu-id="30270-120">Connect tooAzure.</span></span>
* <span data-ttu-id="30270-121">Caricare i dati di origine hello, vedere [Guida introduttiva di Azure Data Lake Analitica U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="30270-121">Upload hello source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span></span> 

## <a name="develop-assemblies-for-u-sql"></a><span data-ttu-id="30270-122">Sviluppare assembly per U-SQL</span><span class="sxs-lookup"><span data-stu-id="30270-122">Develop assemblies for U-SQL</span></span>

<span data-ttu-id="30270-123">**toocreate e inviare un processo U-SQL**</span><span class="sxs-lookup"><span data-stu-id="30270-123">**toocreate and submit a U-SQL job**</span></span>

1. <span data-ttu-id="30270-124">Da hello **File** menu, fare clic su **New**, quindi fare clic su **progetto**.</span><span class="sxs-lookup"><span data-stu-id="30270-124">From hello **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="30270-125">Espandere **installato**, **modelli**, **Azure Data Lake**, **U-SQL(ADLA)**selezionare hello **libreria di classi (per U-SQL Applicazione)** modello e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="30270-125">Expand **Installed**, **Templates**, **Azure Data Lake**, **U-SQL(ADLA)**, select hello **Class Library (For U-SQL Application)** template, and then click **OK**.</span></span>
3. <span data-ttu-id="30270-126">Scrivere il codice in Class1.cs.</span><span class="sxs-lookup"><span data-stu-id="30270-126">Write your code in Class1.cs.</span></span>  <span data-ttu-id="30270-127">di seguito Hello è un esempio di codice.</span><span class="sxs-lookup"><span data-stu-id="30270-127">hello following is a code sample.</span></span>

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
4. <span data-ttu-id="30270-128">Fare clic su hello **compilare** menu e quindi fare clic su **Compila soluzione** toocreate hello dll.</span><span class="sxs-lookup"><span data-stu-id="30270-128">Click hello **Build** menu, and then click **Build Solution** toocreate hello dll.</span></span>

## <a name="register-assemblies"></a><span data-ttu-id="30270-129">Registrazione di assembly</span><span class="sxs-lookup"><span data-stu-id="30270-129">Register assemblies</span></span>

<span data-ttu-id="30270-130">Vedere [Usare il catalogo Data Lake Analytics(U-SQL)](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="30270-130">See [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>


## <a name="use-hello-assemblies"></a><span data-ttu-id="30270-131">Utilizzare assembly hello</span><span class="sxs-lookup"><span data-stu-id="30270-131">Use hello assemblies</span></span>

<span data-ttu-id="30270-132">Vedere [utilizzare hello Azure Data Lake Tools per Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="30270-132">See [Use hello Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="30270-133">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="30270-133">See also</span></span>
* [<span data-ttu-id="30270-134">Introduzione ad Analisi Data Lake di Azure mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="30270-134">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="30270-135">Introduzione a Data Lake Analitica utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="30270-135">Get started with Data Lake Analytics using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="30270-136">Utilizzare gli strumenti Data Lake per Visual Studio per lo sviluppo di applicazioni U-SQL</span><span class="sxs-lookup"><span data-stu-id="30270-136">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="30270-137">Usare il catalogo Data Lake Analytics(U-SQL)</span><span class="sxs-lookup"><span data-stu-id="30270-137">Use Data Lake Analytics(U-SQL) catalog</span></span>](data-lake-analytics-use-u-sql-catalog.md)
* [<span data-ttu-id="30270-138">Utilizzare hello Azure Data Lake Tools per Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="30270-138">Use hello Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
