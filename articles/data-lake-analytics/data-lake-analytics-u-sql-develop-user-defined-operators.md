---
title: gli operatori definiti dall'utente aaaDevelop U-SQL (UDO) | Documenti Microsoft
description: 'Scopri utilizzato e riutilizzate in Data Lake Analitica processi toodevelop toobe di operatori definiti dall''utente. '
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
ms.openlocfilehash: 6b86618efd3751cd9a5e91875879d7dd6d6a7b02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-user-defined-operators-udos"></a><span data-ttu-id="870eb-103">Sviluppare operatori U-SQL definiti dall'utente (UDO)</span><span class="sxs-lookup"><span data-stu-id="870eb-103">Develop U-SQL user-defined operators (UDOs)</span></span>
<span data-ttu-id="870eb-104">Informazioni su come toodevelop definito dall'utente dati tooprocess operatori in un processo U-SQL.</span><span class="sxs-lookup"><span data-stu-id="870eb-104">Learn how toodevelop user-defined operators tooprocess data in a U-SQL job.</span></span>

<span data-ttu-id="870eb-105">Per istruzioni sullo sviluppo di assembly per utilizzo generico per U-SQL, vedere [Sviluppare assembly U-SQL per processi di Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md)</span><span class="sxs-lookup"><span data-stu-id="870eb-105">For instructions on developing general-purpose assemblies for U-SQL, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md)</span></span>

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a><span data-ttu-id="870eb-106">Definire e usare un operatore definito dall'utente in U-SQL</span><span class="sxs-lookup"><span data-stu-id="870eb-106">Define and use a user-defined operator in U-SQL</span></span>
<span data-ttu-id="870eb-107">**toocreate e inviare un processo U-SQL**</span><span class="sxs-lookup"><span data-stu-id="870eb-107">**toocreate and submit a U-SQL job**</span></span>

1. <span data-ttu-id="870eb-108">Hello Visual Studio selezionare **File > Nuovo > progetto > progetto U-SQL**.</span><span class="sxs-lookup"><span data-stu-id="870eb-108">From hello Visual Studio select **File > New > Project > U-SQL Project**.</span></span>
2. <span data-ttu-id="870eb-109">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="870eb-109">Click **OK**.</span></span> <span data-ttu-id="870eb-110">Visual Studio crea una soluzione con un file Script.usql.</span><span class="sxs-lookup"><span data-stu-id="870eb-110">Visual Studio creates a solution with a Script.usql file.</span></span>
3. <span data-ttu-id="870eb-111">In **Esplora soluzioni** espandere Script.usql e fare doppio clic su **Script.usql.cs**.</span><span class="sxs-lookup"><span data-stu-id="870eb-111">From **Solution Explorer**, expand Script.usql, and then double-click **Script.usql.cs**.</span></span>
4. <span data-ttu-id="870eb-112">Incollare hello seguente codice nel file hello:</span><span class="sxs-lookup"><span data-stu-id="870eb-112">Paste hello following code into hello file:</span></span>

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
6. <span data-ttu-id="870eb-113">Aprire **Script.usql**, e Incolla hello seguendo script U-SQL:</span><span class="sxs-lookup"><span data-stu-id="870eb-113">Open **Script.usql**, and paste hello following U-SQL script:</span></span>

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
            too"/Samples/Outputs/Drivers.csv"
            USING Outputters.Csv(Encoding.Unicode);
7. <span data-ttu-id="870eb-114">Specificare l'account Data Lake Analitica hello, Database e dello Schema.</span><span class="sxs-lookup"><span data-stu-id="870eb-114">Specify hello Data Lake Analytics account, Database, and Schema.</span></span>
8. <span data-ttu-id="870eb-115">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Script.usql** e quindi scegliere **Build Script** (Compila script).</span><span class="sxs-lookup"><span data-stu-id="870eb-115">From **Solution Explorer**, right-click **Script.usql**, and then click **Build Script**.</span></span>
9. <span data-ttu-id="870eb-116">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Script.usql** e quindi scegliere **Submit Script** (Invia script).</span><span class="sxs-lookup"><span data-stu-id="870eb-116">From **Solution Explorer**, right-click **Script.usql**, and then click **Submit Script**.</span></span>
10. <span data-ttu-id="870eb-117">Se si non sono stati connessi tooyour sottoscrizione di Azure, è necessario essere tooenter richieste le credenziali dell'account Azure.</span><span class="sxs-lookup"><span data-stu-id="870eb-117">If you haven't connected tooyour Azure subscription, you will be prompted tooenter your Azure account credentials.</span></span>
11. <span data-ttu-id="870eb-118">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="870eb-118">Click **Submit**.</span></span> <span data-ttu-id="870eb-119">Risultati di invio e il collegamento di processo sono disponibili nella finestra Risultati hello quando viene completato l'invio di hello.</span><span class="sxs-lookup"><span data-stu-id="870eb-119">Submission results and job link are available in hello Results window when hello submission is completed.</span></span>
12. <span data-ttu-id="870eb-120">Fare clic su hello **aggiornamento** pulsante toosee hello più recente processo lo stato e aggiornamento schermata Ciao.</span><span class="sxs-lookup"><span data-stu-id="870eb-120">Click hello **Refresh** button toosee hello latest job status and refresh hello screen.</span></span>

<span data-ttu-id="870eb-121">**output di hello toosee**</span><span class="sxs-lookup"><span data-stu-id="870eb-121">**toosee hello output**</span></span>

1. <span data-ttu-id="870eb-122">Da **Esplora Server**, espandere **Azure**, espandere **Data Lake Analitica**, espandere l'account Data Lake Analitica **gliaccountdiarchiviazione**, fare doppio clic su hello archiviazione predefinito e quindi fare clic su **Esplora**.</span><span class="sxs-lookup"><span data-stu-id="870eb-122">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click hello Default Storage, and then click **Explorer**.</span></span>
2. <span data-ttu-id="870eb-123">Espandere esempi, espandere gli output e quindi fare doppio clic su **Drivers.csv**.</span><span class="sxs-lookup"><span data-stu-id="870eb-123">Expand Samples, expand Outputs, and then double-click **Drivers.csv**.</span></span>

## <a name="see-also"></a><span data-ttu-id="870eb-124">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="870eb-124">See also</span></span>
* [<span data-ttu-id="870eb-125">Introduzione ad Analisi Data Lake di Azure mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="870eb-125">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="870eb-126">Introduzione a Data Lake Analitica utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="870eb-126">Get started with Data Lake Analytics using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="870eb-127">Utilizzare gli strumenti Data Lake per Visual Studio per lo sviluppo di applicazioni U-SQL</span><span class="sxs-lookup"><span data-stu-id="870eb-127">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
