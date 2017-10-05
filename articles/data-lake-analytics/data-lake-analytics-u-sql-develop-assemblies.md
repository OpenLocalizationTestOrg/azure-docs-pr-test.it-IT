---
title: Sviluppare assembly U-SQL per processi Azure Data Lake Analytics | Microsoft Docs
description: "Informazioni su come sviluppare assembly da usare più volte in processi di Data Lake Analytics. "
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
ms.openlocfilehash: c49f80f8dcd330d7f46726241e7178351b9cc28f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a><span data-ttu-id="ca720-103">Sviluppare assembly U-SQL per processi di Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="ca720-103">Develop U-SQL assemblies for Azure Data Lake Analytics jobs</span></span>
<span data-ttu-id="ca720-104">Informazioni su come attivare code-behind negli assembly da usare più volte nei processi di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="ca720-104">Learn how to turn code-behind into assemblies to be used and reused in Data Lake Analytics jobs.</span></span> 

<span data-ttu-id="ca720-105">U-SQL semplifica l'aggiunta di codice personalizzato nei linguaggi .Net, ad esempio C#, VB.Net o F#.</span><span class="sxs-lookup"><span data-stu-id="ca720-105">U-SQL makes it easy to add your own custom code in .Net languages, such as C#, VB.Net or F#.</span></span> <span data-ttu-id="ca720-106">È anche possibile distribuire il proprio runtime per supportare altri linguaggi.</span><span class="sxs-lookup"><span data-stu-id="ca720-106">You can even deploy your own runtime to support other languages.</span></span>

<span data-ttu-id="ca720-107">Il modo più semplice per usare codice personalizzato consiste nello sfruttare gli strumenti di Data Lake per le funzionalità code-behind di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca720-107">The easiest way to use custom code is to use the Data Lake Tools for Visual Studio’s code-behind capabilities.</span></span> <span data-ttu-id="ca720-108">Per altre informazioni, vedere [Esercitazione: Sviluppare script U-SQL tramite Strumenti di Data Lake per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ca720-108">For more information, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="ca720-109">L'uso di code-behind presenta alcuni svantaggi:</span><span class="sxs-lookup"><span data-stu-id="ca720-109">There are a few drawbacks of using code-behind:</span></span>

- <span data-ttu-id="ca720-110">Il codice sorgente viene caricato per ogni invio di script.</span><span class="sxs-lookup"><span data-stu-id="ca720-110">The source code gets uploaded for every script submission.</span></span>
- <span data-ttu-id="ca720-111">Non è possibile condividere code-behind con altri processi.</span><span class="sxs-lookup"><span data-stu-id="ca720-111">code-behind cannot be shared with other jobs.</span></span>

<span data-ttu-id="ca720-112">Per risolvere questi problemi, è possibile attivare code-behind in assembly e registrare gli assembly nel catalogo di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="ca720-112">To address these drawbacks, you can turn code-behind into assemblies, and register the assemblies to the Data Lake Analytics catalog.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca720-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ca720-113">Prerequisites</span></span>
* <span data-ttu-id="ca720-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 aggiornamento 4 o Visual Studio 2012 con Visual C++ installato</span><span class="sxs-lookup"><span data-stu-id="ca720-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span></span>
* <span data-ttu-id="ca720-115">Microsoft Azure SDK per .NET versione 2.5 o successiva.</span><span class="sxs-lookup"><span data-stu-id="ca720-115">Microsoft Azure SDK for .NET version 2.5 or above.</span></span>  <span data-ttu-id="ca720-116">Eseguire l'installazione usando il programma di installazione della piattaforma Web o il programma di installazione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ca720-116">Install it using the Web platform installer or Visual Studio Installer</span></span>
* <span data-ttu-id="ca720-117">Un account di Analisi Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ca720-117">A Data Lake Analytics account.</span></span>  <span data-ttu-id="ca720-118">Vedere [Introduzione ad Azure Data Lake Analytics con il Portale di Azure](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ca720-118">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="ca720-119">Seguire i passaggi dell’esercitazione [Introduzione a U-SQL Studio di Analisi Azure Data Lake](data-lake-analytics-u-sql-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="ca720-119">Go through the [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span></span>
* <span data-ttu-id="ca720-120">Connettersi ad Azure.</span><span class="sxs-lookup"><span data-stu-id="ca720-120">Connect to Azure.</span></span>
* <span data-ttu-id="ca720-121">Caricare i dati di origine, vedere [Introduzione a U-SQL Studio di Azure Data Lake Analytics](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ca720-121">Upload the source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span></span> 

## <a name="develop-assemblies-for-u-sql"></a><span data-ttu-id="ca720-122">Sviluppare assembly per U-SQL</span><span class="sxs-lookup"><span data-stu-id="ca720-122">Develop assemblies for U-SQL</span></span>

<span data-ttu-id="ca720-123">**Per creare e inviare un processo di U-SQL**</span><span class="sxs-lookup"><span data-stu-id="ca720-123">**To create and submit a U-SQL job**</span></span>

1. <span data-ttu-id="ca720-124">Scegliere **Nuovo** dal menu **File** e quindi fare clic su **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="ca720-124">From the **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="ca720-125">Espandere **Installato**, **Modelli**, **Azure Data Lake**, **U-SQL(ADLA)**, selezionare il modello **Class Library (For U-SQL Application)** (Libreria di classi - Per applicazioni U-SQL) e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ca720-125">Expand **Installed**, **Templates**, **Azure Data Lake**, **U-SQL(ADLA)**, select the **Class Library (For U-SQL Application)** template, and then click **OK**.</span></span>
3. <span data-ttu-id="ca720-126">Scrivere il codice in Class1.cs.</span><span class="sxs-lookup"><span data-stu-id="ca720-126">Write your code in Class1.cs.</span></span>  <span data-ttu-id="ca720-127">Di seguito è disponibile un esempio di codice.</span><span class="sxs-lookup"><span data-stu-id="ca720-127">The following is a code sample.</span></span>

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
4. <span data-ttu-id="ca720-128">Fare clic sul menu **Compila** e quindi fare clic su **Compila soluzione** per creare la dll.</span><span class="sxs-lookup"><span data-stu-id="ca720-128">Click the **Build** menu, and then click **Build Solution** to create the dll.</span></span>

## <a name="register-assemblies"></a><span data-ttu-id="ca720-129">Registrazione di assembly</span><span class="sxs-lookup"><span data-stu-id="ca720-129">Register assemblies</span></span>

<span data-ttu-id="ca720-130">Vedere [Usare il catalogo Data Lake Analytics(U-SQL)](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="ca720-130">See [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>


## <a name="use-the-assemblies"></a><span data-ttu-id="ca720-131">Usare gli assembly</span><span class="sxs-lookup"><span data-stu-id="ca720-131">Use the assemblies</span></span>

<span data-ttu-id="ca720-132">Vedere [Usare gli strumenti di Azure Data Lake per Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="ca720-132">See [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="ca720-133">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ca720-133">See also</span></span>
* [<span data-ttu-id="ca720-134">Introduzione ad Analisi Data Lake di Azure mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca720-134">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="ca720-135">Introduzione ad Analisi Data Lake mediante il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ca720-135">Get started with Data Lake Analytics using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="ca720-136">Utilizzare gli strumenti Data Lake per Visual Studio per lo sviluppo di applicazioni U-SQL</span><span class="sxs-lookup"><span data-stu-id="ca720-136">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="ca720-137">Usare il catalogo Data Lake Analytics(U-SQL)</span><span class="sxs-lookup"><span data-stu-id="ca720-137">Use Data Lake Analytics(U-SQL) catalog</span></span>](data-lake-analytics-use-u-sql-catalog.md)
* [<span data-ttu-id="ca720-138">Usare gli strumenti di Azure Data Lake per Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ca720-138">Use the Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)