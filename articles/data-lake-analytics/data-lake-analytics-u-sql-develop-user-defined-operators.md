---
title: Sviluppare operatori U-SQL definiti dall'utente (UDO) | Microsoft Docs
description: 'Informazioni su come sviluppare operatori definiti dall''utente da usare e riutilizzare nei processi di Data Lake Analytics. '
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: e5189e4e-9438-46d1-8686-ed4836bf3356
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: fdee02fb60b633c26704fc1774dfc3a7825b5e0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="develop-u-sql-user-defined-operators-udos"></a><span data-ttu-id="84be8-103">Sviluppare operatori U-SQL definiti dall'utente (UDO)</span><span class="sxs-lookup"><span data-stu-id="84be8-103">Develop U-SQL user-defined operators (UDOs)</span></span>
<span data-ttu-id="84be8-104">Informazioni su come sviluppare operatori definiti dall'utente per elaborare i dati in un processo U-SQL.</span><span class="sxs-lookup"><span data-stu-id="84be8-104">Learn how to develop user-defined operators to process data in a U-SQL job.</span></span>

<span data-ttu-id="84be8-105">Per istruzioni sullo sviluppo di assembly per utilizzo generico per U-SQL, vedere [Sviluppare assembly U-SQL per processi di Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md)</span><span class="sxs-lookup"><span data-stu-id="84be8-105">For instructions on developing general-purpose assemblies for U-SQL, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md)</span></span>

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a><span data-ttu-id="84be8-106">Definire e usare un operatore definito dall'utente in U-SQL</span><span class="sxs-lookup"><span data-stu-id="84be8-106">Define and use a user-defined operator in U-SQL</span></span>
<span data-ttu-id="84be8-107">**Per creare e inviare un processo di U-SQL**</span><span class="sxs-lookup"><span data-stu-id="84be8-107">**To create and submit a U-SQL job**</span></span>

1. <span data-ttu-id="84be8-108">In Visual Studio selezionare **File > Nuovo > Progetto > U-SQL Project** (Progetto U-SQL).</span><span class="sxs-lookup"><span data-stu-id="84be8-108">From the Visual Studio select **File > New > Project > U-SQL Project**.</span></span>
2. <span data-ttu-id="84be8-109">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="84be8-109">Click **OK**.</span></span> <span data-ttu-id="84be8-110">Visual Studio crea una soluzione con un file Script.usql.</span><span class="sxs-lookup"><span data-stu-id="84be8-110">Visual Studio creates a solution with a Script.usql file.</span></span>
3. <span data-ttu-id="84be8-111">In **Esplora soluzioni** espandere Script.usql e fare doppio clic su **Script.usql.cs**.</span><span class="sxs-lookup"><span data-stu-id="84be8-111">From **Solution Explorer**, expand Script.usql, and then double-click **Script.usql.cs**.</span></span>
4. <span data-ttu-id="84be8-112">Incollare il seguente codice nel file:</span><span class="sxs-lookup"><span data-stu-id="84be8-112">Paste the following code into the file:</span></span>

        using Microsoft.Analytics.Interfaces;
        using System.Collections.Generic;

        namespace USQL_UDO
        {
            public class CountryName : IProcessor
            {
                private static IDictionary<string, string> CountryTranslation = new Dictionary<string, string>
                {
                    {
                        "Deutschland", "Germany"
                    },
                    {
                        "Suisse", "Switzerland"
                    },
                    {
                        "UK", "United Kingdom"
                    },
                    {
                        "USA", "United States of America"
                    },
                    {
                        "中国", "PR China"
                    }
                };

                public override IRow Process(IRow input, IUpdatableRow output)
                {

                    string UserID = input.Get<string>("UserID");
                    string Name = input.Get<string>("Name");
                    string Address = input.Get<string>("Address");
                    string City = input.Get<string>("City");
                    string State = input.Get<string>("State");
                    string PostalCode = input.Get<string>("PostalCode");
                    string Country = input.Get<string>("Country");
                    string Phone = input.Get<string>("Phone");

                    if (CountryTranslation.Keys.Contains(Country))
                    {
                        Country = CountryTranslation[Country];
                    }
                    output.Set<string>(0, UserID);
                    output.Set<string>(1, Name);
                    output.Set<string>(2, Address);
                    output.Set<string>(3, City);
                    output.Set<string>(4, State);
                    output.Set<string>(5, PostalCode);
                    output.Set<string>(6, Country);
                    output.Set<string>(7, Phone);

                    return output.AsReadOnly();
                }
            }
        }
6. <span data-ttu-id="84be8-113">Aprire **Script.usql** e incollare lo script U-SQL seguente:</span><span class="sxs-lookup"><span data-stu-id="84be8-113">Open **Script.usql**, and paste the following U-SQL script:</span></span>

        @drivers =
            EXTRACT UserID      string,
                    Name        string,
                    Address     string,
                    City        string,
                    State       string,
                    PostalCode  string,
                    Country     string,
                    Phone       string
            FROM "/Samples/Data/AmbulanceData/Drivers.txt"
            USING Extractors.Tsv(Encoding.Unicode);

        @drivers_CountryName =
            PROCESS @drivers
            PRODUCE UserID string,
                    Name string,
                    Address string,
                    City string,
                    State string,
                    PostalCode string,
                    Country string,
                    Phone string
            USING new USQL_UDO.CountryName();    

        OUTPUT @drivers_CountryName
            TO "/Samples/Outputs/Drivers.csv"
            USING Outputters.Csv(Encoding.Unicode);
7. <span data-ttu-id="84be8-114">Specificare l'account di Analisi Data Lake, il database e lo schema.</span><span class="sxs-lookup"><span data-stu-id="84be8-114">Specify the Data Lake Analytics account, Database, and Schema.</span></span>
8. <span data-ttu-id="84be8-115">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Script.usql** e quindi scegliere **Build Script** (Compila script).</span><span class="sxs-lookup"><span data-stu-id="84be8-115">From **Solution Explorer**, right-click **Script.usql**, and then click **Build Script**.</span></span>
9. <span data-ttu-id="84be8-116">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Script.usql** e quindi scegliere **Submit Script** (Invia script).</span><span class="sxs-lookup"><span data-stu-id="84be8-116">From **Solution Explorer**, right-click **Script.usql**, and then click **Submit Script**.</span></span>
10. <span data-ttu-id="84be8-117">Se non ci si è ancora connessi alla sottoscrizione di Azure, verrà richiesto di immettere le credenziali dell'account Azure.</span><span class="sxs-lookup"><span data-stu-id="84be8-117">If you haven't connected to your Azure subscription, you will be prompted to enter your Azure account credentials.</span></span>
11. <span data-ttu-id="84be8-118">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="84be8-118">Click **Submit**.</span></span> <span data-ttu-id="84be8-119">Al termine della procedura di invio, nella finestra dei risultati saranno disponibili i risultati dell'operazione di invio e il collegamento al processo.</span><span class="sxs-lookup"><span data-stu-id="84be8-119">Submission results and job link are available in the Results window when the submission is completed.</span></span>
12. <span data-ttu-id="84be8-120">Per visualizzare lo stato attuale del processo, fare clic sul pulsante **Aggiorna** per aggiornare la schermata.</span><span class="sxs-lookup"><span data-stu-id="84be8-120">Click the **Refresh** button to see the latest job status and refresh the screen.</span></span>

<span data-ttu-id="84be8-121">**Per visualizzare l'output**</span><span class="sxs-lookup"><span data-stu-id="84be8-121">**To see the output**</span></span>

1. <span data-ttu-id="84be8-122">Da **Esplora server** espandere **Azure**, quindi **Data Lake Analytics**, l'account Data Lake Analytics e infine **Account di archiviazione**. Fare clic con il pulsante destro del mouse su Archivio predefinito e quindi scegliere **Esplora**.</span><span class="sxs-lookup"><span data-stu-id="84be8-122">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click the Default Storage, and then click **Explorer**.</span></span>
2. <span data-ttu-id="84be8-123">Espandere esempi, espandere gli output e quindi fare doppio clic su **Drivers.csv**.</span><span class="sxs-lookup"><span data-stu-id="84be8-123">Expand Samples, expand Outputs, and then double-click **Drivers.csv**.</span></span>

## <a name="see-also"></a><span data-ttu-id="84be8-124">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="84be8-124">See also</span></span>
* [<span data-ttu-id="84be8-125">Introduzione ad Analisi Data Lake di Azure mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="84be8-125">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="84be8-126">Introduzione ad Analisi Data Lake mediante il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="84be8-126">Get started with Data Lake Analytics using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="84be8-127">Utilizzare gli strumenti Data Lake per Visual Studio per lo sviluppo di applicazioni U-SQL</span><span class="sxs-lookup"><span data-stu-id="84be8-127">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
