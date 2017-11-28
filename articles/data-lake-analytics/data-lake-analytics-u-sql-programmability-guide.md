---
title: "Guida di programmabilità aaaU-SQL per Azure Data Lake | Documenti Microsoft"
description: Informazioni sui set hello di servizi di Azure Data Lake che consentono di toocreate una piattaforma big data basato sul cloud.
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
ms.assetid: 63be271e-7c44-4d19-9897-c2913ee9599d
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: saveenr
ms.openlocfilehash: cc8f126234c6106a0dc633ce85a1d9ab1e634e30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-programmability-guide"></a><span data-ttu-id="68a11-103">Guida alla programmabilità di U-SQL</span><span class="sxs-lookup"><span data-stu-id="68a11-103">U-SQL programmability guide</span></span>

<span data-ttu-id="68a11-104">U-SQL è un linguaggio di query progettato per carichi di lavoro di tipo Big Data.</span><span class="sxs-lookup"><span data-stu-id="68a11-104">U-SQL is a query language that's designed for big data-type of workloads.</span></span> <span data-ttu-id="68a11-105">Una delle funzionalità specifiche di hello dell'U-SQL è costituito di hello hello dichiarativa linguaggio relativi all'estensibilità di hello e programmabilità fornita da c#.</span><span class="sxs-lookup"><span data-stu-id="68a11-105">One of hello unique features of U-SQL is hello combination of hello SQL-like declarative language with hello extensibility and programmability that's provided by C#.</span></span> <span data-ttu-id="68a11-106">In questa Guida, vengono presi in considerazione hello estensibilità e programmabilità del linguaggio di hello U-SQL che è abilitato per c#.</span><span class="sxs-lookup"><span data-stu-id="68a11-106">In this guide, we concentrate on hello extensibility and programmability of hello U-SQL language that's enabled by C#.</span></span>

## <a name="requirements"></a><span data-ttu-id="68a11-107">Requisiti</span><span class="sxs-lookup"><span data-stu-id="68a11-107">Requirements</span></span>

<span data-ttu-id="68a11-108">Scaricare e installare [Strumenti Azure Data Lake per Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="68a11-108">Download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="get-started-with-u-sql"></a><span data-ttu-id="68a11-109">Introduzione a U-SQL</span><span class="sxs-lookup"><span data-stu-id="68a11-109">Get started with U-SQL</span></span>  

<span data-ttu-id="68a11-110">Diamo un'occhiata hello lo script U-SQL seguente:</span><span class="sxs-lookup"><span data-stu-id="68a11-110">Let’s look at hello following U-SQL script:</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso",   1500.0, "2017-03-39"),
            ("Woodgrove", 2700.0, "2017-04-10")
        ) AS 
              D( customer, amount );
@results =
    SELECT
        customer,
    amount,
    date
    FROM @a;    
```

<span data-ttu-id="68a11-111">Definisce un set di righe chiamato @a e crea un set di righe chiamato @results da @a.</span><span class="sxs-lookup"><span data-stu-id="68a11-111">It defines a RowSet called @a and creates a RowSet called @results from @a.</span></span>

## <a name="c-types-and-expressions-in-u-sql-script"></a><span data-ttu-id="68a11-112">Tipi ed espressioni C# in uno script U-SQL</span><span class="sxs-lookup"><span data-stu-id="68a11-112">C# types and expressions in U-SQL script</span></span>

<span data-ttu-id="68a11-113">Un'espressione U-SQL è un'espressione C# combinata con operazioni logiche U-SQL quali `AND`, `OR` e `NOT`.</span><span class="sxs-lookup"><span data-stu-id="68a11-113">A U-SQL Expression is a C# expression combined with U-SQL logical operations such `AND`, `OR`, and `NOT`.</span></span> <span data-ttu-id="68a11-114">Le espressioni U-SQL possono essere utilizzate con l'istruzione SELECT, EXTRACT, WHERE, HAVING, GROUP BY e DECLARE.</span><span class="sxs-lookup"><span data-stu-id="68a11-114">U-SQL Expressions can be used with SELECT, EXTRACT, WHERE, HAVING, GROUP BY and DECLARE.</span></span>

<span data-ttu-id="68a11-115">Ad esempio, un valore DateTime nella clausola SELECT hello hello lo script seguente analizza una stringa.</span><span class="sxs-lookup"><span data-stu-id="68a11-115">For example, hello following script parses a string a DateTime value in hello SELECT clause.</span></span>

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

<span data-ttu-id="68a11-116">Hello lo script seguente analizza una stringa di un valore DateTime in un'istruzione DECLARE.</span><span class="sxs-lookup"><span data-stu-id="68a11-116">hello following script parses a string a DateTime value in a DECLARE statement.</span></span>

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a><span data-ttu-id="68a11-117">Usare espressioni C# per conversioni del tipo di dati</span><span class="sxs-lookup"><span data-stu-id="68a11-117">Use C# expressions for data type conversions</span></span>
<span data-ttu-id="68a11-118">Hello di esempio seguente viene illustrato come si una conversione di dati datetime utilizzando espressioni di c#.</span><span class="sxs-lookup"><span data-stu-id="68a11-118">hello following example demonstrates how you can do a datetime data conversion by using C# expressions.</span></span> <span data-ttu-id="68a11-119">In questo particolare scenario, dati di stringa datetime sono datetime convertito toostandard con notazione ora 00:00:00 di mezzanotte.</span><span class="sxs-lookup"><span data-stu-id="68a11-119">In this particular scenario, string datetime data is converted toostandard datetime with midnight 00:00:00 time notation.</span></span>

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a><span data-ttu-id="68a11-120">Usare espressioni C# per la data odierna</span><span class="sxs-lookup"><span data-stu-id="68a11-120">Use C# expressions for today’s date</span></span>
<span data-ttu-id="68a11-121">toopull data, è possibile utilizzare hello espressione c# seguente:</span><span class="sxs-lookup"><span data-stu-id="68a11-121">toopull today’s date, we can use hello following C# expression:</span></span>

```
DateTime.Now.ToString("M/d/yyyy")
```

<span data-ttu-id="68a11-122">Di seguito è riportato un esempio di come toouse questa espressione in uno script:</span><span class="sxs-lookup"><span data-stu-id="68a11-122">Here's an example of how toouse this expression in a script:</span></span>

```
@rs1 =
    SELECT
        MAX(guid) AS start_id,
        MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        user,
        des
    FROM @rs0
    GROUP BY user, des;
```



## <a name="using-net-assemblies"></a><span data-ttu-id="68a11-123">Uso di assembly .NET</span><span class="sxs-lookup"><span data-stu-id="68a11-123">Using .NET assemblies</span></span>
<span data-ttu-id="68a11-124">Modello di estendibilità U-SQL si basa fortemente su codice personalizzato di hello possibilità tooadd.</span><span class="sxs-lookup"><span data-stu-id="68a11-124">U-SQL’s extensibility model relies heavily on hello ability tooadd custom code.</span></span> <span data-ttu-id="68a11-125">Attualmente, U-SQL fornisce semplici modi tooadd proprio Microsoft. Codice basato su rete (in particolare, in c#).</span><span class="sxs-lookup"><span data-stu-id="68a11-125">Currently, U-SQL provides you with easy ways tooadd your own Microsoft .NET-based code (in particular, C#).</span></span> <span data-ttu-id="68a11-126">È anche possibile, tuttavia, aggiungere codice personalizzato scritto in altri linguaggi .NET, come VB.NET o F#.</span><span class="sxs-lookup"><span data-stu-id="68a11-126">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span></span> 

### <a name="register-a-net-assembly"></a><span data-ttu-id="68a11-127">Registrare un assembly .NET</span><span class="sxs-lookup"><span data-stu-id="68a11-127">Register a .NET assembly</span></span>

<span data-ttu-id="68a11-128">Utilizzare tooplace di istruzione CREATE ASSEMBLY hello un assembly .NET in un Database U-SQL.</span><span class="sxs-lookup"><span data-stu-id="68a11-128">Use hello CREATE ASSEMBLY statement tooplace a .NET assembly into a U-SQL Database.</span></span> <span data-ttu-id="68a11-129">Una volta un assembly in un database, gli script U-SQL è possono utilizzare tali assembly utilizzando l'istruzione di ASSEMBLY di riferimento hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-129">Once an assembly is in a database, U-SQL scripts can use those assemblies by using hello REFERENCE ASSEMBLY statement.</span></span> 

<span data-ttu-id="68a11-130">Hello seguente codice mostra come tooregister un assembly:</span><span class="sxs-lookup"><span data-stu-id="68a11-130">hello following code shows how tooregister an assembly:</span></span>

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

<span data-ttu-id="68a11-131">Hello seguente codice mostra come tooreference un assembly:</span><span class="sxs-lookup"><span data-stu-id="68a11-131">hello following code shows how tooreference an assembly:</span></span>

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

<span data-ttu-id="68a11-132">Consultare hello [le istruzioni di registrazione assembly](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) che descrive in dettaglio in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="68a11-132">Consult hello [assembly registration instructions](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) that covers this topic in greater detail.</span></span>


### <a name="use-assembly-versioning"></a><span data-ttu-id="68a11-133">Usare il controllo delle versioni degli assembly</span><span class="sxs-lookup"><span data-stu-id="68a11-133">Use assembly versioning</span></span>
<span data-ttu-id="68a11-134">Attualmente, U-SQL Usa hello .NET Framework versione 4.5.</span><span class="sxs-lookup"><span data-stu-id="68a11-134">Currently, U-SQL uses hello .NET Framework version 4.5.</span></span> <span data-ttu-id="68a11-135">Verificare che siano compatibili con tale versione del runtime di hello assembly personalizzati.</span><span class="sxs-lookup"><span data-stu-id="68a11-135">So ensure that your own assemblies are compatible with that version of hello runtime.</span></span>

<span data-ttu-id="68a11-136">Come indicato in precedenza, U-SQL esegue il codice in un formato a 64 bit (x64).</span><span class="sxs-lookup"><span data-stu-id="68a11-136">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span></span> <span data-ttu-id="68a11-137">Verificare pertanto che il codice viene compilato toorun su x64.</span><span class="sxs-lookup"><span data-stu-id="68a11-137">So make sure that your code is compiled toorun on x64.</span></span> <span data-ttu-id="68a11-138">In caso contrario, viene visualizzato errore di formato non corretto di hello illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="68a11-138">Otherwise you get hello incorrect format error shown earlier.</span></span>

<span data-ttu-id="68a11-139">Ogni DLL di assembly e file di risorse caricato (ad esempio un diverso runtime, un assembly nativo o un file di configurazione) può essere al massimo di 400 MB.</span><span class="sxs-lookup"><span data-stu-id="68a11-139">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span></span> <span data-ttu-id="68a11-140">dimensioni totali di Hello risorse distribuiti, tramite la risorsa di distribuire o tramite tooassemblies riferimenti e i file aggiuntivi, non possono superare i 3 GB.</span><span class="sxs-lookup"><span data-stu-id="68a11-140">hello total size of deployed resources, either via DEPLOY RESOURCE or via references tooassemblies and their additional files, cannot exceed 3 GB.</span></span>

<span data-ttu-id="68a11-141">Si noti infine che ogni database U-SQL può contenere solo una versione di un determinato assembly.</span><span class="sxs-lookup"><span data-stu-id="68a11-141">Finally, note that each U-SQL database can only contain one version of any given assembly.</span></span> <span data-ttu-id="68a11-142">Ad esempio, se è necessario sia versione 7 e 8 di hello NewtonSoft Json.Net libreria, è necessario tooregister usarle in due database diversi.</span><span class="sxs-lookup"><span data-stu-id="68a11-142">For example, if you need both version 7 and version 8 of hello NewtonSoft Json.Net library, you need tooregister them in two different databases.</span></span> <span data-ttu-id="68a11-143">Inoltre, ogni script può fare riferimento solo tooone versione di un determinato assembly DLL.</span><span class="sxs-lookup"><span data-stu-id="68a11-143">Furthermore, each script can only refer tooone version of a given assembly DLL.</span></span> <span data-ttu-id="68a11-144">In questo senso, U-SQL semantica hello c# assembly gestione e controllo delle versioni.</span><span class="sxs-lookup"><span data-stu-id="68a11-144">In this respect, U-SQL follows hello C# assembly management and versioning semantics.</span></span>


## <a name="use-user-defined-functions-udf"></a><span data-ttu-id="68a11-145">Usare funzioni definite dall'utente (UDF)</span><span class="sxs-lookup"><span data-stu-id="68a11-145">Use user-defined functions: UDF</span></span>
<span data-ttu-id="68a11-146">Funzioni definite dall'utente U-SQL o funzione definita dall'utente, programmazione routine che accettano parametri, eseguono un'azione (ad esempio un calcolo complesso) e restituiscono il risultato di hello di azione come valore.</span><span class="sxs-lookup"><span data-stu-id="68a11-146">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return hello result of that action as a value.</span></span> <span data-ttu-id="68a11-147">Hello restituiti valore della funzione definita dall'utente può essere solo un singolo valore scalare.</span><span class="sxs-lookup"><span data-stu-id="68a11-147">hello return value of UDF can only be a single scalar.</span></span> <span data-ttu-id="68a11-148">Una funzione UDF di U-SQL può essere chiamata nello script di base di U-SQL come qualsiasi altra funzione scalare di C#.</span><span class="sxs-lookup"><span data-stu-id="68a11-148">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span></span>

<span data-ttu-id="68a11-149">È consigliabile inizializzare le funzioni definite dall'utente di U-SQL come **public** e **static**.</span><span class="sxs-lookup"><span data-stu-id="68a11-149">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span></span>

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

<span data-ttu-id="68a11-150">Primo diamo un'occhiata hello semplice esempio di creazione di una funzione definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="68a11-150">First let’s look at hello simple example of creating a UDF.</span></span>

<span data-ttu-id="68a11-151">In questo scenario di caso d'uso, è necessario toodetermine hello periodo fiscale, tra cui trimestre fiscale hello e mese fiscale di hello prima Accedi per utente specifico di hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-151">In this use-case scenario, we need toodetermine hello fiscal period, including hello fiscal quarter and fiscal month of hello first sign-in for hello specific user.</span></span> <span data-ttu-id="68a11-152">Hello primo mese fiscale dell'anno hello in questo scenario è giugno.</span><span class="sxs-lookup"><span data-stu-id="68a11-152">hello first fiscal month of hello year in our scenario is June.</span></span>

<span data-ttu-id="68a11-153">periodo fiscale toocalculate, si introduce hello funzione c# seguente:</span><span class="sxs-lookup"><span data-stu-id="68a11-153">toocalculate fiscal period, we introduce hello following C# function:</span></span>

```
public static string GetFiscalPeriod(DateTime dt)
{
    int FiscalMonth=0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter=0;
    if (FiscalMonth >=1 && FiscalMonth<=3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return "Q" + FiscalQuarter.ToString() + ":P" + FiscalMonth.ToString();
}
```

<span data-ttu-id="68a11-154">In questo modo vengono semplicemente calcolati il mese e il trimestre fiscali e viene restituito un valore stringa.</span><span class="sxs-lookup"><span data-stu-id="68a11-154">It simply calculates fiscal month and quarter and returns a string value.</span></span> <span data-ttu-id="68a11-155">Del mese di giugno, hello primo mese del hello primo trimestre fiscale, utilizziamo "Q1:P1".</span><span class="sxs-lookup"><span data-stu-id="68a11-155">For June, hello first month of hello first fiscal quarter, we use "Q1:P1".</span></span> <span data-ttu-id="68a11-156">per luglio "Q1:P2" e così via.</span><span class="sxs-lookup"><span data-stu-id="68a11-156">For July, we use "Q1:P2", and so on.</span></span>

<span data-ttu-id="68a11-157">Si tratta di una normale funzione c# che stiamo toouse continua nel progetto U-SQL.</span><span class="sxs-lookup"><span data-stu-id="68a11-157">This is a regular C# function that we are going toouse in our U-SQL project.</span></span>

<span data-ttu-id="68a11-158">Di seguito è illustrato l'aspetto di sezione di codice hello in questo scenario:</span><span class="sxs-lookup"><span data-stu-id="68a11-158">Here is how hello code-behind section looks in this scenario:</span></span>

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        public static string GetFiscalPeriod(DateTime dt)
        {
            int FiscalMonth=0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter=0;
            if (FiscalMonth >=1 && FiscalMonth<=3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return "Q" + FiscalQuarter.ToString() + ":" + FiscalMonth.ToString();
        }

    }

}
```

<span data-ttu-id="68a11-159">A questo punto verrà toocall questa funzione dallo script U-SQL di base hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-159">Now we are going toocall this function from hello base U-SQL script.</span></span> <span data-ttu-id="68a11-160">toodo, abbiamo tooprovide un nome completo per la funzione hello, tra cui hello dello spazio dei nomi, in questo caso NameSpace.Class.Function(parameter).</span><span class="sxs-lookup"><span data-stu-id="68a11-160">toodo this, we have tooprovide a fully qualified name for hello function, including hello namespace, which in this case is NameSpace.Class.Function(parameter).</span></span>

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

<span data-ttu-id="68a11-161">Di seguito è hello effettivo U-SQL script di base:</span><span class="sxs-lookup"><span data-stu-id="68a11-161">Following is hello actual U-SQL base script:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt DateTime,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

DECLARE @default_dt DateTime = Convert.ToDateTime("06/01/2016");

@rs1 =
    SELECT
        MAX(guid) AS start_id,
    MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        user,
        des
    FROM @rs0
    GROUP BY user, des;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="68a11-162">Di seguito è hello i file di output dell'esecuzione dello script hello:</span><span class="sxs-lookup"><span data-stu-id="68a11-162">Following is hello output file of hello script execution:</span></span>

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

<span data-ttu-id="68a11-163">In questo esempio viene illustrato un uso semplificato della funzione UDF inline in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="68a11-163">This example demonstrates a simple usage of inline UDF in U-SQL.</span></span>

### <a name="keep-state-between-udf-invocations"></a><span data-ttu-id="68a11-164">Mantenere lo stato tra chiamate di funzioni definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="68a11-164">Keep state between UDF invocations</span></span>
<span data-ttu-id="68a11-165">Gli oggetti di programmazione c# U-SQL possono essere più sofisticati, che utilizzano interattività tramite le variabili globali di codice hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-165">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through hello code-behind global variables.</span></span> <span data-ttu-id="68a11-166">Diamo un'occhiata hello segue scenario di caso d'uso di business.</span><span class="sxs-lookup"><span data-stu-id="68a11-166">Let’s look at hello following business use-case scenario.</span></span>

<span data-ttu-id="68a11-167">Nelle grandi organizzazioni gli utenti possono accedere a svariate applicazioni interne,</span><span class="sxs-lookup"><span data-stu-id="68a11-167">In large organizations, users can switch between varieties of internal applications.</span></span> <span data-ttu-id="68a11-168">ad esempio Microsoft Dynamics CRM, Power BI e così via.</span><span class="sxs-lookup"><span data-stu-id="68a11-168">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span></span> <span data-ttu-id="68a11-169">I clienti potrebbe essere necessario tooapply un'analisi di dati di telemetria di come gli utenti passare tra applicazioni diverse, quali utilizzo hello tendenze sono e così via.</span><span class="sxs-lookup"><span data-stu-id="68a11-169">Customers might want tooapply a telemetry analysis of how users switch between different applications, what hello usage trends are, and so on.</span></span> <span data-ttu-id="68a11-170">obiettivo Hello per le aziende hello è l'utilizzo dell'applicazione toooptimize.</span><span class="sxs-lookup"><span data-stu-id="68a11-170">hello goal for hello business is toooptimize application usage.</span></span> <span data-ttu-id="68a11-171">Si potrebbe essere inoltre toocombine diverse applicazioni o routine di accesso specifiche.</span><span class="sxs-lookup"><span data-stu-id="68a11-171">They also might want toocombine different applications or specific sign-on routines.</span></span>

<span data-ttu-id="68a11-172">tooachieve questo obiettivo, abbiamo toodetermine ID di sessione e il tempo di ritardo tra hello ultima sessione che si sono verificati.</span><span class="sxs-lookup"><span data-stu-id="68a11-172">tooachieve this goal, we have toodetermine session IDs and lag time between hello last session that occurred.</span></span>

<span data-ttu-id="68a11-173">È necessario toofind una precedente Accedi e quindi assegnare questo sessioni di accesso tooall che vengono generato toohello stessa applicazione.</span><span class="sxs-lookup"><span data-stu-id="68a11-173">We need toofind a previous sign-in and then assign this sign-in tooall sessions that are being generated toohello same application.</span></span> <span data-ttu-id="68a11-174">primo test hello è che uno script di base U-SQL non consente i calcoli tooapply su colonne calcolate già con funzione LAG.</span><span class="sxs-lookup"><span data-stu-id="68a11-174">hello first challenge is that U-SQL base script doesn't allow us tooapply calculations over already-calculated columns with LAG function.</span></span> <span data-ttu-id="68a11-175">Hello seconda situazione è che abbiamo sessione specifica di hello tookeep per tutte le sessioni in hello stesso periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="68a11-175">hello second challenge is that we have tookeep hello specific session for all sessions within hello same time period.</span></span>

<span data-ttu-id="68a11-176">toosolve questo problema, è utilizzare una variabile globale all'interno di una sezione di codice: `static public string globalSession;`.</span><span class="sxs-lookup"><span data-stu-id="68a11-176">toosolve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span></span>

<span data-ttu-id="68a11-177">Questa variabile globale è applicato toohello intero set di righe durante l'esecuzione dello script.</span><span class="sxs-lookup"><span data-stu-id="68a11-177">This global variable is applied toohello entire rowset during our script execution.</span></span>

<span data-ttu-id="68a11-178">Di seguito è una sezione di codice hello di questo programma U-SQL:</span><span class="sxs-lookup"><span data-stu-id="68a11-178">Here is hello code-behind section of our U-SQL program:</span></span>

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQLApplication21
{
    public class UserSession
    {
        static public string globalSession;
        static public string StampUserSession(string eventTime, string PreviousRow, string Session)
        {

            if (!string.IsNullOrEmpty(PreviousRow))
            {
                double timeGap = Convert.ToDateTime(eventTime).Subtract(Convert.ToDateTime(PreviousRow)).TotalMinutes;
                if (timeGap <= 60) {return Session;}
                else {return Guid.NewGuid().ToString();}
            }
            else {return Guid.NewGuid().ToString();}

        }

        static public string getStampUserSession(string Session)
        {
            if (Session != globalSession && !string.IsNullOrEmpty(Session)) { globalSession = Session; }
            return globalSession;
        }

    }
}
```

<span data-ttu-id="68a11-179">In questo esempio mostra hello (variabile globale) `static public string globalSession;` utilizzata all'interno di hello `getStampUserSession` (funzione) e il recupero reinizializzare ogni hello ora sessione parametro viene modificato.</span><span class="sxs-lookup"><span data-stu-id="68a11-179">This example shows hello global variable `static public string globalSession;` used inside hello `getStampUserSession` function and getting reinitialized each time hello Session parameter is changed.</span></span>

<span data-ttu-id="68a11-180">Hello U-SQL script di base è la seguente:</span><span class="sxs-lookup"><span data-stu-id="68a11-180">hello U-SQL base script is as follows:</span></span>

```
DECLARE @in string = @"\UserSession\test1.tsv";
DECLARE @out1 string = @"\UserSession\Out1.csv";
DECLARE @out2 string = @"\UserSession\Out2.csv";
DECLARE @out3 string = @"\UserSession\Out3.csv";

@records =
    EXTRACT DataId string,
            EventDateTime string,           
            UserName string,
            UserSessionTimestamp string

    FROM @in
    USING Extractors.Tsv();

@rs1 =
    SELECT 
        EventDateTime,
        UserName,
    LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,          
        string.IsNullOrEmpty(LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,           
        USQLApplication21.UserSession.StampUserSession
           (
            EventDateTime,
            LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC),
            LAG(UserSessionTimestamp, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)
           ) AS UserSessionTimestamp
    FROM @records;

@rs2 =
    SELECT 
        EventDateTime,
        UserName,
        LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,
        string.IsNullOrEmpty( LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,
        USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp) AS UserSessionTimestamp
    FROM @rs1
    WHERE UserName != "UserName";

OUTPUT @rs2
    too@out2
    ORDER BY UserName, EventDateTime ASC
    USING Outputters.Csv();
```

<span data-ttu-id="68a11-181">Funzione `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` viene chiamato qui durante il calcolo di hello secondo memoria set di righe.</span><span class="sxs-lookup"><span data-stu-id="68a11-181">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during hello second memory rowset calculation.</span></span> <span data-ttu-id="68a11-182">Passa hello `UserSessionTimestamp` colonna e restituisce hello valore fino a quando `UserSessionTimestamp` è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="68a11-182">It passes hello `UserSessionTimestamp` column and returns hello value until `UserSessionTimestamp` has changed.</span></span>

<span data-ttu-id="68a11-183">file di output di Hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="68a11-183">hello output file is as follows:</span></span>

```
"2016-02-19T07:32:36.8420000-08:00","User1",,True,"72a0660e-22df-428e-b672-e0977007177f"
"2016-02-17T11:52:43.6350000-08:00","User2",,True,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-17T11:59:08.8320000-08:00","User2","2016-02-17T11:52:43.6350000-08:00",False,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-11T07:04:17.2630000-08:00","User3",,True,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-11T07:10:33.9720000-08:00","User3","2016-02-11T07:04:17.2630000-08:00",False,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-15T21:27:41.8210000-08:00","User3","2016-02-11T07:10:33.9720000-08:00",False,"4d2bc48d-bdf3-4591-a9c1-7b15ceb8e074"
"2016-02-16T05:48:49.6360000-08:00","User3","2016-02-15T21:27:41.8210000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-16T06:22:43.6390000-08:00","User3","2016-02-16T05:48:49.6360000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-17T16:29:53.2280000-08:00","User3","2016-02-16T06:22:43.6390000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T16:39:07.2430000-08:00","User3","2016-02-17T16:29:53.2280000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T17:20:39.3220000-08:00","User3","2016-02-17T16:39:07.2430000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-19T05:23:54.5710000-08:00","User3","2016-02-17T17:20:39.3220000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T05:48:37.7510000-08:00","User3","2016-02-19T05:23:54.5710000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T06:40:27.4830000-08:00","User3","2016-02-19T05:48:37.7510000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T07:27:37.7550000-08:00","User3","2016-02-19T06:40:27.4830000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T19:35:40.9450000-08:00","User3","2016-02-19T07:27:37.7550000-08:00",False,"3f385f0b-3e68-4456-ac74-ff6cef093674"
"2016-02-20T00:07:37.8250000-08:00","User3","2016-02-19T19:35:40.9450000-08:00",False,"685f76d5-ca48-4c58-b77d-bd3a9ddb33da"
"2016-02-11T09:01:33.9720000-08:00","User4",,True,"9f0cf696-c8ba-449a-8d5f-1ca6ed8f2ee8"
"2016-02-17T06:30:38.6210000-08:00","User4","2016-02-11T09:01:33.9720000-08:00",False,"8b11fd2a-01bf-4a5e-a9af-3c92c4e4382a"
"2016-02-17T22:15:26.4020000-08:00","User4","2016-02-17T06:30:38.6210000-08:00",False,"4e1cb707-3b5f-49c1-90c7-9b33b86ca1f4"
"2016-02-18T14:37:27.6560000-08:00","User4","2016-02-17T22:15:26.4020000-08:00",False,"f4e44400-e837-40ed-8dfd-2ea264d4e338"
"2016-02-19T01:20:31.4800000-08:00","User4","2016-02-18T14:37:27.6560000-08:00",False,"2136f4cf-7c7d-43c1-8ae2-08f4ad6a6e08"
```

<span data-ttu-id="68a11-184">In questo esempio viene illustrato uno scenario di caso d'uso più complesso in cui viene utilizzata una variabile globale all'interno di una sezione di codice che viene applicato toohello memoria intero set di righe.</span><span class="sxs-lookup"><span data-stu-id="68a11-184">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied toohello entire memory rowset.</span></span>

## <a name="use-user-defined-types-udt"></a><span data-ttu-id="68a11-185">Usare tipi definiti dall'utente (UDT)</span><span class="sxs-lookup"><span data-stu-id="68a11-185">Use user-defined types: UDT</span></span>
<span data-ttu-id="68a11-186">I tipi definiti dall'utente (UDT) sono un'altra funzionalità di programmabilità di U-SQL.</span><span class="sxs-lookup"><span data-stu-id="68a11-186">User-defined types, or UDT, is another programmability feature of U-SQL.</span></span> <span data-ttu-id="68a11-187">L'UDT U-SQL funziona come un normale tipo definito dall'utente C#.</span><span class="sxs-lookup"><span data-stu-id="68a11-187">U-SQL UDT acts like a regular C# user-defined type.</span></span> <span data-ttu-id="68a11-188">In c# è un linguaggio fortemente tipizzato che consente l'utilizzo di hello di tipi incorporati e personalizzati definiti dall'utente.</span><span class="sxs-lookup"><span data-stu-id="68a11-188">C# is a strongly typed language that allows hello use of built-in and custom user-defined types.</span></span>

<span data-ttu-id="68a11-189">U-SQL in modo implicito è in grado di serializzare o deserializzare i tipi definiti dall'utente non autorizzato quando hello tipo definito dall'utente viene passato tra vertici nei set di righe.</span><span class="sxs-lookup"><span data-stu-id="68a11-189">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when hello UDT is passed between vertices in rowsets.</span></span> <span data-ttu-id="68a11-190">Ciò significa che l'utente hello ha tooprovide un formattatore esplicito tramite l'interfaccia IFormatter hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-190">This means that hello user has tooprovide an explicit formatter by using hello IFormatter interface.</span></span> <span data-ttu-id="68a11-191">In questo modo U-SQL di hello serializzare e deserializzare i metodi per hello tipo definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="68a11-191">This provides U-SQL with hello serialize and de-serialize methods for hello UDT.</span></span>

> [!NOTE]
> <span data-ttu-id="68a11-192">Estrattori incorporati e outputters U-SQL attualmente non è possibile serializzare o deserializzare tooor di dati di tipo definito dall'utente dai file anche con hello IFormatter set.</span><span class="sxs-lookup"><span data-stu-id="68a11-192">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data tooor from files even with hello IFormatter set.</span></span> <span data-ttu-id="68a11-193">Pertanto, quando si scrive il file di tooa dati di tipo definito dall'utente con l'istruzione di OUTPUT di hello o leggerlo con un'utilità di estrazione, si dispone di toopass come una stringa o matrice di byte.</span><span class="sxs-lookup"><span data-stu-id="68a11-193">So when you're writing UDT data tooa file with hello OUTPUT statement, or reading it with an extractor, you have toopass it as a string or byte array.</span></span> <span data-ttu-id="68a11-194">Quindi chiamare serializzazione hello e la deserializzazione di codice (ovvero, il metodo ToString () dell'UDT hello) in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="68a11-194">Then you call hello serialization and deserialization code (that is, hello UDT’s ToString() method) explicitly.</span></span> <span data-ttu-id="68a11-195">Estrattori definito dall'utente outputters, in altri hello mano, possono leggere e scrivere tipi definiti dall'utente.</span><span class="sxs-lookup"><span data-stu-id="68a11-195">User-defined extractors and outputters, on hello other hand, can read and write UDTs.</span></span>

<span data-ttu-id="68a11-196">Se si tenta di toouse UDT in estrazione o OUTPUTTER (non selezionare precedente), come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="68a11-196">If we try toouse UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span></span>

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="68a11-197">È stata ricevuta hello errore seguente:</span><span class="sxs-lookup"><span data-stu-id="68a11-197">We receive hello following error:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINOUTPUTTER: Outputters.Text was used toooutput column myfield of type
MyNameSpace.Myfunction_Returning_UDT.

Description:

Outputters.Text only supports built-in types.

Resolution:

Implement a custom outputter that knows how tooserialize this type, or call a serialization method on hello type in
hello preceding SELECT. C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\
USQL-Programmability\Types.usql 52  1   USQL-Programmability
```

<span data-ttu-id="68a11-198">toowork in outputter con tipo definito dall'utente, è necessario tooserialize è toostring con hello metodo ToString () o creare un outputter personalizzato.</span><span class="sxs-lookup"><span data-stu-id="68a11-198">toowork with UDT in outputter, we either have tooserialize it toostring with hello ToString() method or create a custom outputter.</span></span>

<span data-ttu-id="68a11-199">Al momento non è possibile usare UDT in GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="68a11-199">UDTs currently cannot be used in GROUP BY.</span></span> <span data-ttu-id="68a11-200">Se il tipo definito dall'utente viene utilizzata in GROUP BY, viene generata un'eccezione hello errore seguente:</span><span class="sxs-lookup"><span data-stu-id="68a11-200">If UDT is used in GROUP BY, hello following error is thrown:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINCLAUSE: GROUP BY doesn't support type MyNameSpace.Myfunction_Returning_UDT
for column myfield

Description:

GROUP BY doesn't support UDT or Complex types.

Resolution:

Add a SELECT statement where you can project a scalar column that you want toouse with GROUP BY.
C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\USQL-Programmability\Types.usql
62  5   USQL-Programmability
```

<span data-ttu-id="68a11-201">toodefine un tipo definito dall'utente, è necessario:</span><span class="sxs-lookup"><span data-stu-id="68a11-201">toodefine a UDT, we have to:</span></span>

* <span data-ttu-id="68a11-202">Aggiungere i seguenti spazi dei nomi hello:</span><span class="sxs-lookup"><span data-stu-id="68a11-202">Add hello following namespaces:</span></span>

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* <span data-ttu-id="68a11-203">Aggiungere `Microsoft.Analytics.Interfaces`, che è necessario per le interfacce di tipo definito dall'utente hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-203">Add `Microsoft.Analytics.Interfaces`, which is required for hello UDT interfaces.</span></span> <span data-ttu-id="68a11-204">Inoltre, `System.IO` potrebbe essere necessario toodefine hello IFormatter interfaccia.</span><span class="sxs-lookup"><span data-stu-id="68a11-204">In addition, `System.IO` might be needed toodefine hello IFormatter interface.</span></span>

* <span data-ttu-id="68a11-205">Definire un tipo definito dall'utente con l'attributo SqlUserDefinedType.</span><span class="sxs-lookup"><span data-stu-id="68a11-205">Define a used-defined type with SqlUserDefinedType attribute.</span></span>

<span data-ttu-id="68a11-206">**SqlUserDefinedType** è toomark utilizzata una definizione di tipo in un assembly come un tipo definito dall'utente (UDT) in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="68a11-206">**SqlUserDefinedType** is used toomark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span></span> <span data-ttu-id="68a11-207">proprietà Hello attributo hello riflettono caratteristiche fisiche di hello di hello tipo definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="68a11-207">hello properties on hello attribute reflect hello physical characteristics of hello UDT.</span></span> <span data-ttu-id="68a11-208">Questa classe non può essere ereditata.</span><span class="sxs-lookup"><span data-stu-id="68a11-208">This class cannot be inherited.</span></span>

<span data-ttu-id="68a11-209">SqlUserDefinedType è un attributo obbligatorio per la definizione dell'UDT.</span><span class="sxs-lookup"><span data-stu-id="68a11-209">SqlUserDefinedType is a required attribute for UDT definition.</span></span>

<span data-ttu-id="68a11-210">costruttore Hello della classe hello:</span><span class="sxs-lookup"><span data-stu-id="68a11-210">hello constructor of hello class:</span></span>  

* <span data-ttu-id="68a11-211">SqlUserDefinedTypeAttribute (formattatore di tipo)</span><span class="sxs-lookup"><span data-stu-id="68a11-211">SqlUserDefinedTypeAttribute (type formatter)</span></span>

* <span data-ttu-id="68a11-212">Formattatore Type: richiesto parametro toodefine un formattatore di tipo definito dall'utente, in particolare, tipo di hello hello `IFormatter` interfaccia deve essere passata in questo caso.</span><span class="sxs-lookup"><span data-stu-id="68a11-212">Type formatter: Required parameter toodefine an UDT formatter--specifically, hello type of hello `IFormatter` interface must be passed here.</span></span>

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* <span data-ttu-id="68a11-213">Tipo definito dall'utente tipico richiede inoltre definizione dell'interfaccia IFormatter hello, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="68a11-213">Typical UDT also requires definition of hello IFormatter interface, as shown in hello following example:</span></span>

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

<span data-ttu-id="68a11-214">Hello `IFormatter` interfaccia serializza e deserializza un oggetto grafico con il tipo di radice hello di \<typeparamref name = "T" >.</span><span class="sxs-lookup"><span data-stu-id="68a11-214">hello `IFormatter` interface serializes and de-serializes an object graph with hello root type of \<typeparamref name="T">.</span></span>

<span data-ttu-id="68a11-215">\<typeparam name = "T" > tipo radice per hello oggetto grafico tooserialize hello e deserializzare.</span><span class="sxs-lookup"><span data-stu-id="68a11-215">\<typeparam name="T">hello root type for hello object graph tooserialize and de-serialize.</span></span>

* <span data-ttu-id="68a11-216">**Deserializzare**: deserializzata dati hello sul flusso fornito hello e ricostruisce grafico hello degli oggetti.</span><span class="sxs-lookup"><span data-stu-id="68a11-216">**Deserialize**: De-serializes hello data on hello provided stream and reconstitutes hello graph of objects.</span></span>

* <span data-ttu-id="68a11-217">**Serializzare**: serializza un oggetto o un grafico degli oggetti, con hello dato flusso toohello fornito radice.</span><span class="sxs-lookup"><span data-stu-id="68a11-217">**Serialize**: Serializes an object, or graph of objects, with hello given root toohello provided stream.</span></span>

<span data-ttu-id="68a11-218">`MyType`istanza: istanza del tipo di hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-218">`MyType` instance: Instance of hello type.</span></span>  
<span data-ttu-id="68a11-219">`IColumnWriter`writer / `IColumnReader` lettore: hello sottostante il flusso di colonna.</span><span class="sxs-lookup"><span data-stu-id="68a11-219">`IColumnWriter` writer / `IColumnReader` reader: hello underlying column stream.</span></span>  
<span data-ttu-id="68a11-220">`ISerializationContext`contesto: enumerazione che definisce un set di flag che specifica il contesto di origine o destinazione hello per flusso hello durante la serializzazione.</span><span class="sxs-lookup"><span data-stu-id="68a11-220">`ISerializationContext` context: Enum that defines a set of flags that specifies hello source or destination context for hello stream during serialization.</span></span>

* <span data-ttu-id="68a11-221">**Intermedio**: Specifica il contesto di origine o destinazione hello non è un archivio permanente.</span><span class="sxs-lookup"><span data-stu-id="68a11-221">**Intermediate**: Specifies that hello source or destination context is not a persisted store.</span></span>

* <span data-ttu-id="68a11-222">**Persistenza**: Specifica il contesto di origine o destinazione hello è un archivio permanente.</span><span class="sxs-lookup"><span data-stu-id="68a11-222">**Persistence**: Specifies that hello source or destination context is a persisted store.</span></span>

<span data-ttu-id="68a11-223">Come un normale tipo C#, la definizione di un tipo definito dall'utente di U-SQL può includere override per operatori come +/==/!= e così via.</span><span class="sxs-lookup"><span data-stu-id="68a11-223">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span></span> <span data-ttu-id="68a11-224">Può anche includere metodi statici.</span><span class="sxs-lookup"><span data-stu-id="68a11-224">It can also include static methods.</span></span> <span data-ttu-id="68a11-225">Ad esempio, se si stabilirà toouse questo tipo definito dall'utente come tooa un parametro funzione di aggregazione MIN U-SQL, abbiamo toodefine < operatore override.</span><span class="sxs-lookup"><span data-stu-id="68a11-225">For example, if we are going toouse this UDT as a parameter tooa U-SQL MIN aggregate function, we have toodefine < operator override.</span></span>

<span data-ttu-id="68a11-226">In questa Guida, è illustrato un esempio di identificazione del periodo fiscale da data specifica di hello in formato hello Qn:Pn (Q1:P10).</span><span class="sxs-lookup"><span data-stu-id="68a11-226">Earlier in this guide, we demonstrated an example for fiscal period identification from hello specific date in hello format Qn:Pn (Q1:P10).</span></span> <span data-ttu-id="68a11-227">Hello di esempio seguente viene illustrato come toodefine digitare un oggetto personalizzato per i valori del periodo fiscali.</span><span class="sxs-lookup"><span data-stu-id="68a11-227">hello following example shows how toodefine a custom type for fiscal period values.</span></span>

<span data-ttu-id="68a11-228">Di seguito è riportato un esempio di sezione code-behind con tipo definito dall'utente e interfaccia IFormatter personalizzati:</span><span class="sxs-lookup"><span data-stu-id="68a11-228">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span></span>

```
[SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
public struct FiscalPeriod
{
    public int Quarter { get; private set; }

    public int Month { get; private set; }

    public FiscalPeriod(int quarter, int month):this()
    {
    this.Quarter = quarter;
    this.Month = month;
    }

    public override bool Equals(object obj)
    {
    if (ReferenceEquals(null, obj))
    {
        return false;
    }

    return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
    }

    public bool Equals(FiscalPeriod other)
    {
return this.Quarter.Equals(other.Quarter) && this.Month.Equals(other.Month);
    }

    public bool GreaterThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
    }

    public bool LessThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
    }

    public override int GetHashCode()
    {
    unchecked
    {
        return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
    }
    }

    public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
    {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
    }

    public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.Equals(c2);
    }

    public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
    {
    return !c1.Equals(c2);
    }
    public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.GreaterThan(c2);
    }
    public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.LessThan(c2);
    }
    public override string ToString()
    {
    return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
    }

}

public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
{
    public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
    {
    using (var binaryWriter = new BinaryWriter(writer.BaseStream))
    {
        binaryWriter.Write(instance.Quarter);
        binaryWriter.Write(instance.Month);
        binaryWriter.Flush();
    }
    }

    public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
    {
    using (var binaryReader = new BinaryReader(reader.BaseStream))
    {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
        return result;
    }
    }
}
```

<span data-ttu-id="68a11-229">tipo definito Hello include due numeri: trimestre e mese.</span><span class="sxs-lookup"><span data-stu-id="68a11-229">hello defined type includes two numbers: quarter and month.</span></span> <span data-ttu-id="68a11-230">Qui sono definiti gli operatori ==/!=/>/< e il metodo statico ToString ().</span><span class="sxs-lookup"><span data-stu-id="68a11-230">Operators ==/!=/>/< and static method ToString() are defined here.</span></span>

<span data-ttu-id="68a11-231">Come indicato in precedenza, il tipo definito dall'utente può essere usato nelle espressioni SELECT, ma non in OUTPUTTER/EXTRACTOR senza serializzazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="68a11-231">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span></span> <span data-ttu-id="68a11-232">Include sia toobe serializzato come una stringa con ToString () o con un OUTPUTTER/estrazione personalizzato.</span><span class="sxs-lookup"><span data-stu-id="68a11-232">It either has toobe serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span></span>

<span data-ttu-id="68a11-233">Ora esaminiamo l'uso dell'UDT.</span><span class="sxs-lookup"><span data-stu-id="68a11-233">Now let’s discuss usage of UDT.</span></span> <span data-ttu-id="68a11-234">In una sezione di codice, sono stati modificati i seguenti di toohello GetFiscalPeriod funzione:</span><span class="sxs-lookup"><span data-stu-id="68a11-234">In a code-behind section, we changed our GetFiscalPeriod function toohello following:</span></span>

```
public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
{
    int FiscalMonth = 0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter = 0;
    if (FiscalMonth >= 1 && FiscalMonth <= 3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return new FiscalPeriod(FiscalQuarter, FiscalMonth);
}
```

<span data-ttu-id="68a11-235">Come si può notare, restituisce il valore di hello di questo tipo FiscalPeriod.</span><span class="sxs-lookup"><span data-stu-id="68a11-235">As you can see, it returns hello value of our FiscalPeriod type.</span></span>

<span data-ttu-id="68a11-236">Qui è fornito un esempio di come toouse venga ulteriormente nello script di base U-SQL.</span><span class="sxs-lookup"><span data-stu-id="68a11-236">Here we provide an example of how toouse it further in U-SQL base script.</span></span> <span data-ttu-id="68a11-237">Questo esempio illustra diverse forme di chiamata del tipo definito dall'utente dallo script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="68a11-237">This example demonstrates different forms of UDT invocation from U-SQL script.</span></span>

```
DECLARE @input_file string = @"c:\work\cosmos\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"c:\work\cosmos\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        guid string,
        dt DateTime,
        user String,
        des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT 
        guid AS start_id,
        dt,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Quarter AS fiscalquarter,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Month AS fiscalmonth,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt) + new USQL_Programmability.CustomFunctions.FiscalPeriod(1,7) AS fiscalperiod_adjusted,
        user,
        des
    FROM @rs0;

@rs2 =
    SELECT 
           start_id,
           dt,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           fiscalquarter,
           fiscalmonth,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS fiscalperiod,

       // This user-defined type was created in hello prior SELECT.  Passing hello UDT toothis subsequent SELECT would have failed if hello UDT was not annotated with an IFormatter.
           fiscalperiod_adjusted.ToString() AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="68a11-238">Ecco un esempio di una sezione code-behind completa:</span><span class="sxs-lookup"><span data-stu-id="68a11-238">Here's an example of a full code-behind section:</span></span>

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        static public DateTime? ToDateTime(string dt)
        {
            DateTime dtValue;

            if (!DateTime.TryParse(dt, out dtValue))
                return Convert.ToDateTime(dt);
            else
                return null;
        }

        public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
        {
            int FiscalMonth = 0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter = 0;
            if (FiscalMonth >= 1 && FiscalMonth <= 3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return new FiscalPeriod(FiscalQuarter, FiscalMonth);
        }



        [SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
        public struct FiscalPeriod
        {
            public int Quarter { get; private set; }

            public int Month { get; private set; }

            public FiscalPeriod(int quarter, int month):this()
            {
                this.Quarter = quarter;
                this.Month = month;
            }

            public override bool Equals(object obj)
            {
                if (ReferenceEquals(null, obj))
                {
                    return false;
                }

                return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
            }

            public bool Equals(FiscalPeriod other)
            {
return this.Quarter.Equals(other.Quarter) &&    this.Month.Equals(other.Month);
            }

            public bool GreaterThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
            }

            public bool LessThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
            }

            public override int GetHashCode()
            {
                unchecked
                {
                    return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
                }
            }

            public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
            {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
            }

            public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.Equals(c2);
            }

            public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
            {
                return !c1.Equals(c2);
            }
            public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.GreaterThan(c2);
            }
            public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.LessThan(c2);
            }
            public override string ToString()
            {
                return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
            }

        }

        public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
        {
public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
            {
                using (var binaryWriter = new BinaryWriter(writer.BaseStream))
                {
                    binaryWriter.Write(instance.Quarter);
                    binaryWriter.Write(instance.Month);
                    binaryWriter.Flush();
                }
            }

public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
            {
                using (var binaryReader = new BinaryReader(reader.BaseStream))
                {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
                    return result;
                }
            }
        }
    }
}
```

## <a name="use-user-defined-aggregates-udagg"></a><span data-ttu-id="68a11-239">Usare aggregazioni definite dall'utente (UDAGG)</span><span class="sxs-lookup"><span data-stu-id="68a11-239">Use user-defined aggregates: UDAGG</span></span>
<span data-ttu-id="68a11-240">Le aggregazioni definite dall'utente sono funzioni correlate all'aggregazione che non sono già incluse in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="68a11-240">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span></span> <span data-ttu-id="68a11-241">esempio Hello può essere un'aggregazione tooperform matematiche personalizzate calcoli concatenazioni di stringa, le modifiche con le stringhe e così via.</span><span class="sxs-lookup"><span data-stu-id="68a11-241">hello example can be an aggregate tooperform custom math calculations, string concatenations, manipulations with strings, and so on.</span></span>

<span data-ttu-id="68a11-242">definizione di classe di base aggregazione definita dall'utente Hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="68a11-242">hello user-defined aggregate base class definition is as follows:</span></span>

```c#
    [SqlUserDefinedAggregate]
    public abstract class IAggregate<T1, T2, TResult> : IAggregate
    {
        protected IAggregate();

        public abstract void Accumulate(T1 t1, T2 t2);
        public abstract void Init();
        public abstract TResult Terminate();
    }
```

<span data-ttu-id="68a11-243">**SqlUserDefinedAggregate** indica che il tipo di hello deve essere registrato come una funzione di aggregazione definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="68a11-243">**SqlUserDefinedAggregate** indicates that hello type should be registered as a user-defined aggregate.</span></span> <span data-ttu-id="68a11-244">Questa classe non può essere ereditata.</span><span class="sxs-lookup"><span data-stu-id="68a11-244">This class cannot be inherited.</span></span>

<span data-ttu-id="68a11-245">L'attributo SqlUserDefinedType è **facoltativo** per la definizione di aggregazioni definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="68a11-245">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span></span>


<span data-ttu-id="68a11-246">Hello classe di base consente parametri astratti toopass tre: due parametri di input e una come risultato di hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-246">hello base class allows you toopass three abstract parameters: two as input parameters and one as hello result.</span></span> <span data-ttu-id="68a11-247">tipi di dati Hello sono variabili e devono essere definiti durante l'ereditarietà della classe.</span><span class="sxs-lookup"><span data-stu-id="68a11-247">hello data types are variable and should be defined during class inheritance.</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    { … }

    public override void Accumulate(string guid, string user)
    { … }

    public override string Terminate()
    { … }
}
```

* <span data-ttu-id="68a11-248">**Init** esegue la chiamata una volta per ogni gruppo durante il calcolo.</span><span class="sxs-lookup"><span data-stu-id="68a11-248">**Init** invokes once for each group during computation.</span></span> <span data-ttu-id="68a11-249">Fornisce la routine di inizializzazione per ogni gruppo di aggregazione.</span><span class="sxs-lookup"><span data-stu-id="68a11-249">It provides an initialization routine for each aggregation group.</span></span>  
* <span data-ttu-id="68a11-250">**Accumulate** viene eseguito una volta per ogni valore.</span><span class="sxs-lookup"><span data-stu-id="68a11-250">**Accumulate** is executed once for each value.</span></span> <span data-ttu-id="68a11-251">Fornisce funzionalità principali di hello per l'algoritmo di aggregazione hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-251">It provides hello main functionality for hello aggregation algorithm.</span></span> <span data-ttu-id="68a11-252">Può essere utilizzato tooaggregate valori con vari tipi di dati che vengono definiti durante l'ereditarietà della classe.</span><span class="sxs-lookup"><span data-stu-id="68a11-252">It can be used tooaggregate values with various data types that are defined during class inheritance.</span></span> <span data-ttu-id="68a11-253">Può accettare due parametri di tipi di dati della variabile.</span><span class="sxs-lookup"><span data-stu-id="68a11-253">It can accept two parameters of variable data types.</span></span>
* <span data-ttu-id="68a11-254">**Terminare** viene eseguita una volta per ogni gruppo di aggregazione alla fine hello elaborare toooutput hello risultato per ogni gruppo.</span><span class="sxs-lookup"><span data-stu-id="68a11-254">**Terminate** is executed once per aggregation group at hello end of processing toooutput hello result for each group.</span></span>

<span data-ttu-id="68a11-255">input corretto toodeclare e tipi di dati di output, utilizzare la definizione di classe hello come segue:</span><span class="sxs-lookup"><span data-stu-id="68a11-255">toodeclare correct input and output data types, use hello class definition as follows:</span></span>

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* <span data-ttu-id="68a11-256">T1: Tooaccumulate parametro prima</span><span class="sxs-lookup"><span data-stu-id="68a11-256">T1: First parameter tooaccumulate</span></span>
* <span data-ttu-id="68a11-257">T2: Primo parametro tooaccumulate</span><span class="sxs-lookup"><span data-stu-id="68a11-257">T2: First parameter tooaccumulate</span></span>
* <span data-ttu-id="68a11-258">TResult: tipo restituito di Terminate</span><span class="sxs-lookup"><span data-stu-id="68a11-258">TResult: Return type of terminate</span></span>

<span data-ttu-id="68a11-259">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="68a11-259">For example:</span></span>

```
public class GuidAggregate : IAggregate<string, int, int>
```

<span data-ttu-id="68a11-260">oppure</span><span class="sxs-lookup"><span data-stu-id="68a11-260">or</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a><span data-ttu-id="68a11-261">Usare aggregazioni definite dall'utente in U-SQL</span><span class="sxs-lookup"><span data-stu-id="68a11-261">Use UDAGG in U-SQL</span></span>
<span data-ttu-id="68a11-262">Innanzitutto, toouse aggregazione definita dall'utente, definito nel codice o farvi riferimento da programmabilità esistente hello DLL come indicato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="68a11-262">toouse UDAGG, first define it in code-behind or reference it from hello existent programmability DLL as discussed earlier.</span></span>

<span data-ttu-id="68a11-263">Utilizzare quindi hello la seguente sintassi:</span><span class="sxs-lookup"><span data-stu-id="68a11-263">Then use hello following syntax:</span></span>

```
AGG<UDAGG_functionname>(param1,param2)
```

<span data-ttu-id="68a11-264">Di seguito è riportato un esempio di aggregazione definita dall'utente:</span><span class="sxs-lookup"><span data-stu-id="68a11-264">Here is an example of UDAGG:</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    {
        guid_agg = "";
    }

    public override void Accumulate(string guid, string user)
    {
        if (user.ToUpper()== "USER1")
        {
        guid_agg += "{" + guid + "}";
        }
    }

    public override string Terminate()
    {
        return guid_agg;
    }

}
```

<span data-ttu-id="68a11-265">Ecco lo script U-SQL di base:</span><span class="sxs-lookup"><span data-stu-id="68a11-265">And base U-SQL script:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @" \usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    SELECT
        user,
        AGG<USQL_Programmability.GuidAggregate>(guid,user) AS guid_list
    FROM @rs0
    GROUP BY user;

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

<span data-ttu-id="68a11-266">In questo scenario, in caso di utilizzo vengono concatenati i GUID di classe per utenti specifici di hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-266">In this use-case scenario, we concatenate class GUIDs for hello specific users.</span></span>

## <a name="use-user-defined-objects-udo"></a><span data-ttu-id="68a11-267">Usare oggetti definiti dall'utente (UDO)</span><span class="sxs-lookup"><span data-stu-id="68a11-267">Use user-defined objects: UDO</span></span>
<span data-ttu-id="68a11-268">U-SQL consente gli oggetti di programmabilità personalizzato toodefine, che vengono chiamati gli oggetti definiti dall'utente o l'operatore definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="68a11-268">U-SQL enables you toodefine custom programmability objects, which are called user-defined objects or UDO.</span></span>

<span data-ttu-id="68a11-269">Hello seguito è riportato un elenco di operatore definito dall'utente in U-SQL:</span><span class="sxs-lookup"><span data-stu-id="68a11-269">hello following is a list of UDO in U-SQL:</span></span>

* <span data-ttu-id="68a11-270">Estrattori definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="68a11-270">User-defined extractors</span></span>
    * <span data-ttu-id="68a11-271">Estrazione riga per riga</span><span class="sxs-lookup"><span data-stu-id="68a11-271">Extract row by row</span></span>
    * <span data-ttu-id="68a11-272">Utilizzato tooimplement estrazione dei dati dal file strutturati personalizzati</span><span class="sxs-lookup"><span data-stu-id="68a11-272">Used tooimplement data extraction from custom structured files</span></span>

* <span data-ttu-id="68a11-273">Outputter definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="68a11-273">User-defined outputters</span></span>
    * <span data-ttu-id="68a11-274">Output riga per riga</span><span class="sxs-lookup"><span data-stu-id="68a11-274">Output row by row</span></span>
    * <span data-ttu-id="68a11-275">Utilizzare i tipi di dati personalizzati toooutput o formati di file personalizzati</span><span class="sxs-lookup"><span data-stu-id="68a11-275">Used toooutput custom data types or custom file formats</span></span>

* <span data-ttu-id="68a11-276">Elaboratori definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="68a11-276">User-defined processors</span></span>
    * <span data-ttu-id="68a11-277">Viene usato per richiedere una riga e produrre una riga</span><span class="sxs-lookup"><span data-stu-id="68a11-277">Take one row and produce one row</span></span>
    * <span data-ttu-id="68a11-278">Tooreduce usato hello numero di colonne o creare nuove colonne con valori derivati da un set di colonna esistente</span><span class="sxs-lookup"><span data-stu-id="68a11-278">Used tooreduce hello number of columns or produce new columns with values that are derived from an existing column set</span></span>

* <span data-ttu-id="68a11-279">Oggetti di applicazione definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="68a11-279">User-defined appliers</span></span>
    * <span data-ttu-id="68a11-280">Richiedere una riga e produrre 0 righe toon</span><span class="sxs-lookup"><span data-stu-id="68a11-280">Take one row and produce 0 toon rows</span></span>
    * <span data-ttu-id="68a11-281">Viene usato con OUTER/CROSS APPLY</span><span class="sxs-lookup"><span data-stu-id="68a11-281">Used with OUTER/CROSS APPLY</span></span>

* <span data-ttu-id="68a11-282">Combinatori definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="68a11-282">User-defined combiners</span></span>
    * <span data-ttu-id="68a11-283">Combinano set di righe (JOIN definiti dall'utente)</span><span class="sxs-lookup"><span data-stu-id="68a11-283">Combines rowsets--user-defined JOINs</span></span>

* <span data-ttu-id="68a11-284">Riduttori definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="68a11-284">User-defined reducers</span></span>
    * <span data-ttu-id="68a11-285">Serve a richiedere n righe e produrre una riga</span><span class="sxs-lookup"><span data-stu-id="68a11-285">Take n rows and produce one row</span></span>
    * <span data-ttu-id="68a11-286">Utilizzato tooreduce hello numero di righe</span><span class="sxs-lookup"><span data-stu-id="68a11-286">Used tooreduce hello number of rows</span></span>

<span data-ttu-id="68a11-287">Operatore definito dall'utente viene in genere chiamato in modo esplicito nello script U-SQL come parte di hello istruzioni U-SQL seguente:</span><span class="sxs-lookup"><span data-stu-id="68a11-287">UDO is typically called explicitly in U-SQL script as part of hello following U-SQL statements:</span></span>

* <span data-ttu-id="68a11-288">EXTRACT</span><span class="sxs-lookup"><span data-stu-id="68a11-288">EXTRACT</span></span>
* <span data-ttu-id="68a11-289">OUTPUT</span><span class="sxs-lookup"><span data-stu-id="68a11-289">OUTPUT</span></span>
* <span data-ttu-id="68a11-290">PROCESS</span><span class="sxs-lookup"><span data-stu-id="68a11-290">PROCESS</span></span>
* <span data-ttu-id="68a11-291">COMBINE</span><span class="sxs-lookup"><span data-stu-id="68a11-291">COMBINE</span></span>
* <span data-ttu-id="68a11-292">REDUCE</span><span class="sxs-lookup"><span data-stu-id="68a11-292">REDUCE</span></span>

> [!NOTE]  
> <span data-ttu-id="68a11-293">Operatore definito dall'utente sono limitate tooconsume 0,5 Gb memoria.</span><span class="sxs-lookup"><span data-stu-id="68a11-293">UDO’s are limited tooconsume 0.5Gb memory.</span></span>  <span data-ttu-id="68a11-294">Questa limitazione di memoria non è applicabile toolocal esecuzioni.</span><span class="sxs-lookup"><span data-stu-id="68a11-294">This memory limitation does not apply toolocal executions.</span></span>

## <a name="use-user-defined-extractors"></a><span data-ttu-id="68a11-295">Usare estrattori definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="68a11-295">Use user-defined extractors</span></span>
<span data-ttu-id="68a11-296">U-SQL consente di dati esterni tooimport utilizzando un'istruzione di estrazione.</span><span class="sxs-lookup"><span data-stu-id="68a11-296">U-SQL allows you tooimport external data by using an EXTRACT statement.</span></span> <span data-ttu-id="68a11-297">L'istruzione EXTRACT consente di usare estrattori UDO predefiniti.</span><span class="sxs-lookup"><span data-stu-id="68a11-297">An EXTRACT statement can use built-in UDO extractors:</span></span>  

* <span data-ttu-id="68a11-298">*Extractors.Text()*: consente di estrarre da file di testo delimitati di varie codifiche.</span><span class="sxs-lookup"><span data-stu-id="68a11-298">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span></span>

* <span data-ttu-id="68a11-299">*Extractors.Csv()*: consente di estrarre da file di testo delimitati da virgole (CSV) di varie codifiche.</span><span class="sxs-lookup"><span data-stu-id="68a11-299">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span></span>

* <span data-ttu-id="68a11-300">*Extractors.Tsv()*: consente di estrarre da file di testo delimitati da tabulazioni (TSV) di varie codifiche.</span><span class="sxs-lookup"><span data-stu-id="68a11-300">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="68a11-301">Può essere utile toodevelop un'utilità di estrazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="68a11-301">It can be useful toodevelop a custom extractor.</span></span> <span data-ttu-id="68a11-302">Ciò può essere utile durante l'importazione di dati se si desidera toodo che hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="68a11-302">This can be helpful during data import if we want toodo any of hello following tasks:</span></span>

* <span data-ttu-id="68a11-303">Modificare i dati di input suddividendo le colonne e modificando singoli valori.</span><span class="sxs-lookup"><span data-stu-id="68a11-303">Modify input data by splitting columns and modifying individual values.</span></span> <span data-ttu-id="68a11-304">funzionalità del processore Hello è migliore per la combinazione di colonne.</span><span class="sxs-lookup"><span data-stu-id="68a11-304">hello PROCESSOR functionality is better for combining columns.</span></span>
* <span data-ttu-id="68a11-305">Analizzare dati non strutturati, come pagine Web e messaggi di posta elettronica, o dati parzialmente non strutturati, ad esempio XML/JSON.</span><span class="sxs-lookup"><span data-stu-id="68a11-305">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span></span>
* <span data-ttu-id="68a11-306">Analizzare dati in una codifica non supportata.</span><span class="sxs-lookup"><span data-stu-id="68a11-306">Parse data in unsupported encoding.</span></span>

<span data-ttu-id="68a11-307">toodefine un'utilità di estrazione definite dall'utente, o UDI, dobbiamo toocreate un `IExtractor` interfaccia.</span><span class="sxs-lookup"><span data-stu-id="68a11-307">toodefine a user-defined extractor, or UDE, we need toocreate an `IExtractor` interface.</span></span> <span data-ttu-id="68a11-308">Estrazione toohello parametri, tutti di input, come delimitatori di colonna o la riga e la codifica, devono toobe definita nel costruttore hello della classe hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-308">All input parameters toohello extractor, such as column/row delimiters, and encoding, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="68a11-309">Hello `IExtractor` interfaccia deve inoltre contenere una definizione per hello `IEnumerable<IRow>` override come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="68a11-309">hello `IExtractor`  interface should also contain a definition for hello `IEnumerable<IRow>` override as follows:</span></span>

```
[SqlUserDefinedExtractor]
public class SampleExtractor : IExtractor
{
     public SampleExtractor(string row_delimiter, char col_delimiter)
     { … }

     public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
     { … }
}
```

<span data-ttu-id="68a11-310">Hello **SqlUserDefinedExtractor** attributo indica che il tipo di hello deve essere registrato come una tabella definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="68a11-310">hello **SqlUserDefinedExtractor** attribute indicates that hello type should be registered as a user-defined extractor.</span></span> <span data-ttu-id="68a11-311">Questa classe non può essere ereditata.</span><span class="sxs-lookup"><span data-stu-id="68a11-311">This class cannot be inherited.</span></span>

<span data-ttu-id="68a11-312">SqlUserDefinedExtractor è un attributo facoltativo per la definizione di UDE,</span><span class="sxs-lookup"><span data-stu-id="68a11-312">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span></span> <span data-ttu-id="68a11-313">Proprietà AtomicFileProcessing toodefine e utilizzato per l'oggetto UDI hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-313">It used toodefine AtomicFileProcessing property for hello UDE object.</span></span>

* <span data-ttu-id="68a11-314">bool     AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="68a11-314">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="68a11-315">**true** indica che l'estrattore richiede file di input atomici (JSON, XML e così via)</span><span class="sxs-lookup"><span data-stu-id="68a11-315">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span></span>
* <span data-ttu-id="68a11-316">**false** indica che l'estrattore può gestire file suddivisi/distribuiti (CSV, SEQ e così via)</span><span class="sxs-lookup"><span data-stu-id="68a11-316">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="68a11-317">sono oggetti di programmabilità UDI principali Hello **input** e **output**.</span><span class="sxs-lookup"><span data-stu-id="68a11-317">hello main UDE programmability objects are **input** and **output**.</span></span> <span data-ttu-id="68a11-318">oggetto di input Hello è tooenumerate utilizzati i dati di input come `IUnstructuredReader`.</span><span class="sxs-lookup"><span data-stu-id="68a11-318">hello input object is used tooenumerate input data as `IUnstructuredReader`.</span></span> <span data-ttu-id="68a11-319">oggetto di output di Hello è tooset utilizzati dati di output come risultato delle attività di estrazione hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-319">hello output object is used tooset output data as a result of hello extractor activity.</span></span>

<span data-ttu-id="68a11-320">accesso ai dati di input Hello tramite `System.IO.Stream` e `System.IO.StreamReader`.</span><span class="sxs-lookup"><span data-stu-id="68a11-320">hello input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span></span>

<span data-ttu-id="68a11-321">Per l'enumerazione delle colonne di input, è innanzitutto la divisione di flusso di input hello utilizzando un delimitatore di riga.</span><span class="sxs-lookup"><span data-stu-id="68a11-321">For input columns enumeration, we first split hello input stream by using a row delimiter.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

<span data-ttu-id="68a11-322">Quindi, la riga di input viene ulteriormente suddivisa nelle parti di una colonna.</span><span class="sxs-lookup"><span data-stu-id="68a11-322">Then, further split input row into column parts.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

<span data-ttu-id="68a11-323">i dati di output tooset, utilizziamo hello `output.Set` metodo.</span><span class="sxs-lookup"><span data-stu-id="68a11-323">tooset output data, we use hello `output.Set` method.</span></span>

<span data-ttu-id="68a11-324">È importante toounderstand che hello estrazione personalizzato restituisce solo le colonne e i valori che sono definiti con l'output di hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-324">It's important toounderstand that hello custom extractor only outputs columns and values that are defined with hello output.</span></span> <span data-ttu-id="68a11-325">il metodo di chiamata output.Set.</span><span class="sxs-lookup"><span data-stu-id="68a11-325">Set method call.</span></span>

```
output.Set<string>(count, part);
```

<span data-ttu-id="68a11-326">output di Hello estrazione effettivo viene attivato chiamando `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="68a11-326">hello actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="68a11-327">Di seguito è riportato estrazione hello:</span><span class="sxs-lookup"><span data-stu-id="68a11-327">Following is hello extractor example:</span></span>

```
[SqlUserDefinedExtractor(AtomicFileProcessing = true)]
public class FullDescriptionExtractor : IExtractor
{
     private Encoding _encoding;
     private byte[] _row_delim;
     private char _col_delim;

    public FullDescriptionExtractor(Encoding encoding, string row_delim = "\r\n", char col_delim = '\t')
    {
         this._encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
         this._row_delim = this._encoding.GetBytes(row_delim);
         this._col_delim = col_delim;

    }

    public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
    {
         string line;
         //Read hello input line by line
         foreach (Stream current in input.Split(_encoding.GetBytes("\r\n")))
         {
        using (System.IO.StreamReader streamReader = new StreamReader(current, this._encoding))
         {
             line = streamReader.ReadToEnd().Trim();
             //Split hello input by hello column delimiter
             string[] parts = line.Split(this._col_delim);
             int count = 0; // start with first column
             foreach (string part in parts)
             {
    if (count == 0)
             {  // for column “guid”, re-generated guid
                 Guid new_guid = Guid.NewGuid();
                 output.Set<Guid>(count, new_guid);
             }
             else if (count == 2)
             {
                 // for column “user”, convert tooUPPER case
                 output.Set<string>(count, part.ToUpper());

             }
             else
             {
                 // keep hello rest of hello columns as-is
                 output.Set<string>(count, part);
             }
             count += 1;
             }

         }
         yield return output.AsReadOnly();
         }
         yield break;
     }
}
```

<span data-ttu-id="68a11-328">In questo scenario di caso d'uso, estrazione hello Rigenera hello GUID per la colonna "guid" e converte i valori hello del case tooupper di colonna "user".</span><span class="sxs-lookup"><span data-stu-id="68a11-328">In this use-case scenario, hello extractor regenerates hello GUID for “guid” column and converts hello values of “user” column tooupper case.</span></span> <span data-ttu-id="68a11-329">Gli estrattori personalizzati possono produrre risultati più complessi analizzando e modificando i dati di input.</span><span class="sxs-lookup"><span data-stu-id="68a11-329">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span></span>

<span data-ttu-id="68a11-330">Di seguito è riportato uno script U-SQL di base che usa un estrattore personalizzato:</span><span class="sxs-lookup"><span data-stu-id="68a11-330">Following is base U-SQL script that uses a custom extractor:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file
        USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-outputters"></a><span data-ttu-id="68a11-331">Usare outputter definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="68a11-331">Use user-defined outputters</span></span>
<span data-ttu-id="68a11-332">Outputter definito dall'utente è un altro operatore definito dall'utente U-SQL che consente di tooextend funzionalità U-SQL.</span><span class="sxs-lookup"><span data-stu-id="68a11-332">User-defined outputter is another U-SQL UDO that allows you tooextend built-in U-SQL functionality.</span></span> <span data-ttu-id="68a11-333">Estrazione toohello simile, esistono diverse outputters incorporato.</span><span class="sxs-lookup"><span data-stu-id="68a11-333">Similar toohello extractor, there are several built-in outputters.</span></span>

* <span data-ttu-id="68a11-334">*Outputters.Text()*: scrive dati toodelimited file di testo di codifiche differenti.</span><span class="sxs-lookup"><span data-stu-id="68a11-334">*Outputters.Text()*: Writes data toodelimited text files of different encodings.</span></span>
* <span data-ttu-id="68a11-335">*Outputters.Csv()*: consente di scrivere dati toocomma delimitati da virgole (CSV) file di codifiche differenti.</span><span class="sxs-lookup"><span data-stu-id="68a11-335">*Outputters.Csv()*: Writes data toocomma-separated value (CSV) files of different encodings.</span></span>
* <span data-ttu-id="68a11-336">*Outputters.Tsv()*: consente di scrivere dati tootab delimitati da virgole (TSV) file di codifiche differenti.</span><span class="sxs-lookup"><span data-stu-id="68a11-336">*Outputters.Tsv()*: Writes data tootab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="68a11-337">Outputter personalizzato consente toowrite dati in un formato definito personalizzato.</span><span class="sxs-lookup"><span data-stu-id="68a11-337">Custom outputter allows you toowrite data in a custom defined format.</span></span> <span data-ttu-id="68a11-338">Ciò può risultare utile per hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="68a11-338">This can be useful for hello following tasks:</span></span>

* <span data-ttu-id="68a11-339">Scrittura di file di dati strutturati toosemi o non strutturati.</span><span class="sxs-lookup"><span data-stu-id="68a11-339">Writing data toosemi-structured or unstructured files.</span></span>
* <span data-ttu-id="68a11-340">Scrittura di dati in codifiche non supportate</span><span class="sxs-lookup"><span data-stu-id="68a11-340">Writing data not supported encodings.</span></span>
* <span data-ttu-id="68a11-341">Modifica dei dati di output o aggiunta di attributi personalizzati</span><span class="sxs-lookup"><span data-stu-id="68a11-341">Modifying output data or adding custom attributes.</span></span>

<span data-ttu-id="68a11-342">toodefine definito dall'utente outputter, dobbiamo hello toocreate `IOutputter` interfaccia.</span><span class="sxs-lookup"><span data-stu-id="68a11-342">toodefine user-defined outputter, we need toocreate hello `IOutputter` interface.</span></span>

<span data-ttu-id="68a11-343">Di seguito è hello base `IOutputter` implementazione della classe:</span><span class="sxs-lookup"><span data-stu-id="68a11-343">Following is hello base `IOutputter` class implementation:</span></span>

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

<span data-ttu-id="68a11-344">Tutti i parametri toohello outputter, di input, come delimitatori di colonna, la codifica e così via, devono toobe definita nel costruttore hello della classe hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-344">All input parameters toohello outputter, such as column/row delimiters, encoding, and so on, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="68a11-345">Hello `IOutputter` interfaccia deve inoltre contenere una definizione per `void Output` eseguire l'override.</span><span class="sxs-lookup"><span data-stu-id="68a11-345">hello `IOutputter` interface should also contain a definition for `void Output` override.</span></span> <span data-ttu-id="68a11-346">attributo Hello `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` , facoltativamente, è possibile impostare per l'elaborazione di file atomico.</span><span class="sxs-lookup"><span data-stu-id="68a11-346">hello attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span></span> <span data-ttu-id="68a11-347">Per ulteriori informazioni, vedere hello seguenti dettagli.</span><span class="sxs-lookup"><span data-stu-id="68a11-347">For more information, see hello following details.</span></span>

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class MyOutputter : IOutputter
{

    public MyOutputter(myparam1, myparam2)
    {
      …
    }

    public override void Close()
    {
      …
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
      …
    }
}
```

* <span data-ttu-id="68a11-348">`Output` viene chiamato per ogni riga di input.</span><span class="sxs-lookup"><span data-stu-id="68a11-348">`Output` is called for each input row.</span></span> <span data-ttu-id="68a11-349">Restituisce hello `IUnstructuredWriter output` set di righe.</span><span class="sxs-lookup"><span data-stu-id="68a11-349">It returns hello `IUnstructuredWriter output` rowset.</span></span>
* <span data-ttu-id="68a11-350">classe costruttore Hello viene utilizzata la outputter toopass parametri toohello definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="68a11-350">hello Constructor class is used toopass parameters toohello user-defined outputter.</span></span>
* <span data-ttu-id="68a11-351">`Close`viene utilizzato toooptionally eseguire l'override dello stato costosa toorelease o determinare quando è stato scritto ultima riga hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-351">`Close` is used toooptionally override toorelease expensive state or determine when hello last row was written.</span></span>

<span data-ttu-id="68a11-352">**SqlUserDefinedOutputter** attributo indica che il tipo di hello deve essere registrato come un outputter definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="68a11-352">**SqlUserDefinedOutputter** attribute indicates that hello type should be registered as a user-defined outputter.</span></span> <span data-ttu-id="68a11-353">Questa classe non può essere ereditata.</span><span class="sxs-lookup"><span data-stu-id="68a11-353">This class cannot be inherited.</span></span>

<span data-ttu-id="68a11-354">SqlUserDefinedOutputter è un attributo facoltativo per la definizione di un outputter definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="68a11-354">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span></span> <span data-ttu-id="68a11-355">Proprietà di AtomicFileProcessing toodefine hello è utilizzato.</span><span class="sxs-lookup"><span data-stu-id="68a11-355">It's used toodefine hello AtomicFileProcessing property.</span></span>

* <span data-ttu-id="68a11-356">bool     AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="68a11-356">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="68a11-357">**true** indica che l'outputter richiede file di output atomici (JSON, XML e così via)</span><span class="sxs-lookup"><span data-stu-id="68a11-357">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span></span>
* <span data-ttu-id="68a11-358">**false** indica che l'outputter può gestire file suddivisi/distribuiti (CSV, SEQ e così via)</span><span class="sxs-lookup"><span data-stu-id="68a11-358">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="68a11-359">gli oggetti di programmabilità principale Hello sono **riga** e **output**.</span><span class="sxs-lookup"><span data-stu-id="68a11-359">hello main programmability objects are **row** and **output**.</span></span> <span data-ttu-id="68a11-360">Hello **riga** tooenumerate utilizzati dati di output come rappresenta `IRow` interfaccia.</span><span class="sxs-lookup"><span data-stu-id="68a11-360">hello **row** object is used tooenumerate output data as `IRow` interface.</span></span> <span data-ttu-id="68a11-361">**Output** è tooset utilizzati dati toohello destinazione di output.</span><span class="sxs-lookup"><span data-stu-id="68a11-361">**Output** is used tooset output data toohello target file.</span></span>

<span data-ttu-id="68a11-362">Hello output dati si accede tramite hello `IRow` interfaccia.</span><span class="sxs-lookup"><span data-stu-id="68a11-362">hello output data is accessed through hello `IRow` interface.</span></span> <span data-ttu-id="68a11-363">I dati di output vengono trasmessi una riga alla volta.</span><span class="sxs-lookup"><span data-stu-id="68a11-363">Output data is passed a row at a time.</span></span>

<span data-ttu-id="68a11-364">i singoli valori Hello vengono enumerati chiamando il metodo Get hello dell'interfaccia IRow hello:</span><span class="sxs-lookup"><span data-stu-id="68a11-364">hello individual values are enumerated by calling hello Get method of hello IRow interface:</span></span>

```
row.Get<string>("column_name")
```

<span data-ttu-id="68a11-365">I nomi delle singole colonne possono essere determinati chiamando `row.Schema`:</span><span class="sxs-lookup"><span data-stu-id="68a11-365">Individual column names can be determined by calling `row.Schema`:</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="68a11-366">Questo approccio consente toobuild un outputter flessibile per qualsiasi schema dei metadati.</span><span class="sxs-lookup"><span data-stu-id="68a11-366">This approach enables you toobuild a flexible outputter for any metadata schema.</span></span>

<span data-ttu-id="68a11-367">Hello dati di output viene scritto toofile utilizzando `System.IO.StreamWriter`.</span><span class="sxs-lookup"><span data-stu-id="68a11-367">hello output data is written toofile by using `System.IO.StreamWriter`.</span></span> <span data-ttu-id="68a11-368">parametro di flusso Hello è impostato troppo`output.BaseStrea` come parte di `IUnstructuredWriter output`.</span><span class="sxs-lookup"><span data-stu-id="68a11-368">hello stream parameter is set too`output.BaseStrea` as part of `IUnstructuredWriter output`.</span></span>

<span data-ttu-id="68a11-369">Si noti che il file toohello buffer di tooflush importante hello dati dopo ogni iterazione di riga.</span><span class="sxs-lookup"><span data-stu-id="68a11-369">Note that it's important tooflush hello data buffer toohello file after each row iteration.</span></span> <span data-ttu-id="68a11-370">Inoltre, hello `StreamWriter` oggetto deve essere utilizzato con hello Disposable attributo abilitato (impostazione predefinita) e con hello **utilizzando** (parola chiave):</span><span class="sxs-lookup"><span data-stu-id="68a11-370">In addition, hello `StreamWriter` object must be used with hello Disposable attribute enabled (default) and with hello **using** keyword:</span></span>

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

<span data-ttu-id="68a11-371">In alternativa, chiamare il metodo Flush() in modo esplicito dopo ogni iterazione,</span><span class="sxs-lookup"><span data-stu-id="68a11-371">Otherwise, call Flush() method explicitly after each iteration.</span></span> <span data-ttu-id="68a11-372">Illustrare nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-372">We show this in hello following example.</span></span>

### <a name="set-headers-and-footers-for-user-defined-outputter"></a><span data-ttu-id="68a11-373">Impostare intestazioni e piè di pagina per l'outputter definito dall'utente</span><span class="sxs-lookup"><span data-stu-id="68a11-373">Set headers and footers for user-defined outputter</span></span>
<span data-ttu-id="68a11-374">tooset un'intestazione, utilizzare il flusso di esecuzione singola iterazione.</span><span class="sxs-lookup"><span data-stu-id="68a11-374">tooset a header, use single iteration execution flow.</span></span>

```
public override void Output(IRow row, IUnstructuredWriter output)
{
 …
if (isHeaderRow)
{
    …                
}

 …
if (isHeaderRow)
{
    isHeaderRow = false;
}
 …
}
}
```

<span data-ttu-id="68a11-375">Hello codice hello innanzitutto `if (isHeaderRow)` blocco viene eseguito una sola volta.</span><span class="sxs-lookup"><span data-stu-id="68a11-375">hello code in hello first `if (isHeaderRow)` block is executed only once.</span></span>

<span data-ttu-id="68a11-376">Per il piè di pagina hello, utilizzare hello riferimento toohello istanza `System.IO.Stream` oggetto (`output.BaseStream`).</span><span class="sxs-lookup"><span data-stu-id="68a11-376">For hello footer, use hello reference toohello instance of `System.IO.Stream` object (`output.BaseStream`).</span></span> <span data-ttu-id="68a11-377">Scrivere un piè di pagina hello in hello metodo Close () di hello `IOutputter` interfaccia.</span><span class="sxs-lookup"><span data-stu-id="68a11-377">Write hello footer in hello Close() method of hello `IOutputter` interface.</span></span>  <span data-ttu-id="68a11-378">(Per ulteriori informazioni, vedere hello di esempio seguente).</span><span class="sxs-lookup"><span data-stu-id="68a11-378">(For more information, see hello following example.)</span></span>

<span data-ttu-id="68a11-379">Di seguito è riportato un esempio di outputter definito dall'utente:</span><span class="sxs-lookup"><span data-stu-id="68a11-379">Following is an example of a user-defined outputter:</span></span>

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class HTMLOutputter : IOutputter
{
    // Local variables initialization
    private string row_delimiter;
    private char col_delimiter;
    private bool isHeaderRow;
    private Encoding encoding;
    private bool IsTableHeader = true;
    private Stream g_writer;

    // Parameters definition            
    public HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    this.isHeaderRow = isHeader;
    this.encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
    }

    // hello Close method is used toowrite hello footer toohello file. It's executed only once, after all rows
    public override void Close().
    {
    //Reference tooIO.Stream object - g_writer
    StreamWriter streamWriter = new StreamWriter(g_writer, this.encoding);
    streamWriter.Write("</table>");
    streamWriter.Flush();
    streamWriter.Close();
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
    System.IO.StreamWriter streamWriter = new StreamWriter(output.BaseStream, this.encoding);

    // Metadata schema initialization tooenumerate column names
    ISchema schema = row.Schema;

    // This is a data-independent header--HTML table definition
    if (IsTableHeader)
    {
        streamWriter.Write("<table border=1>");
        IsTableHeader = false;
    }

    // HTML table attributes
    string header_wrapper_on = "<th>";
    string header_wrapper_off = "</th>";
    string data_wrapper_on = "<td>";
    string data_wrapper_off = "</td>";

    // Header row output--runs only once
    if (isHeaderRow)
    {
        streamWriter.Write("<tr>");
        for (int i = 0; i < schema.Count(); i++)
        {
        var col = schema[i];
        streamWriter.Write(header_wrapper_on + col.Name + header_wrapper_off);
        }
        streamWriter.Write("</tr>");
    }

    // Data row output
    streamWriter.Write("<tr>");                
    for (int i = 0; i < schema.Count(); i++)
    {
        var col = schema[i];
        string val = "";
        try
        {
        // Data type enumeration--required toomatch hello distinct list of types from OUTPUT statement
        switch (col.Type.Name.ToString().ToLower())
        {
            case "string": val = row.Get<string>(col.Name).ToString(); break;
            case "guid": val = row.Get<Guid>(col.Name).ToString(); break;
            default: break;
        }
        }
        // Handling NULL values--keeping them empty
        catch (System.NullReferenceException)
        {
        }
        streamWriter.Write(data_wrapper_on + val + data_wrapper_off);
    }
    streamWriter.Write("</tr>");

    if (isHeaderRow)
    {
        isHeaderRow = false;
    }
    // Reference toohello instance of hello IO.Stream object for footer generation
    g_writer = output.BaseStream;
    streamWriter.Flush();
    }
}

// Define hello factory classes
public static class Factory
{
    public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    return new HTMLOutputter(isHeader, encoding);
    }
}
```

<span data-ttu-id="68a11-380">Ecco lo script U-SQL di base:</span><span class="sxs-lookup"><span data-stu-id="68a11-380">And U-SQL base script:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.html";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
         FROM @input_file
         USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 
    too@output_file 
    USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="68a11-381">Questo è un outputter HTML che crea un file HTML con dati di tabella.</span><span class="sxs-lookup"><span data-stu-id="68a11-381">This is an HTML outputter, which creates an HTML file with table data.</span></span>

### <a name="call-outputter-from-u-sql-base-script"></a><span data-ttu-id="68a11-382">Chiamare l'outputter dallo script U-SQL di base</span><span class="sxs-lookup"><span data-stu-id="68a11-382">Call outputter from U-SQL base script</span></span>
<span data-ttu-id="68a11-383">toocall un outputter personalizzato dallo script U-SQL di base hello, hello nuova istanza dell'oggetto outputter hello presenta toobe creato.</span><span class="sxs-lookup"><span data-stu-id="68a11-383">toocall a custom outputter from hello base U-SQL script, hello new instance of hello outputter object has toobe created.</span></span>

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="68a11-384">creazione di un'istanza di hello tooavoid oggetto nello script di base, è possibile creare un wrapper di funzione, come illustrato nell'esempio precedente:</span><span class="sxs-lookup"><span data-stu-id="68a11-384">tooavoid creating an instance of hello object in base script, we can create a function wrapper, as shown in our earlier example:</span></span>

```c#
        // Define hello factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

<span data-ttu-id="68a11-385">In questo caso, la chiamata originale hello aspetto hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="68a11-385">In this case, hello original call looks like hello following:</span></span>

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a><span data-ttu-id="68a11-386">Usare elaboratori definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="68a11-386">Use user-defined processors</span></span>
<span data-ttu-id="68a11-387">Processore definito dall'utente o UDP, è un tipo di operatore definito dall'utente U-SQL che consente le righe in ingresso di hello tooprocess applicando le funzionalità di programmabilità.</span><span class="sxs-lookup"><span data-stu-id="68a11-387">User-defined processor, or UDP, is a type of U-SQL UDO that enables you tooprocess hello incoming rows by applying programmability features.</span></span> <span data-ttu-id="68a11-388">UDP consente toocombine colonne, modificare i valori e aggiungere nuove colonne, se necessario.</span><span class="sxs-lookup"><span data-stu-id="68a11-388">UDP enables you toocombine columns, modify values, and add new columns if necessary.</span></span> <span data-ttu-id="68a11-389">In pratica, è utile tooprocess gli elementi di dati tooproduce richiesto un set di righe.</span><span class="sxs-lookup"><span data-stu-id="68a11-389">Basically, it helps tooprocess a rowset tooproduce required data elements.</span></span>

<span data-ttu-id="68a11-390">toodefine UDP, è necessario toocreate un `IProcessor` interfaccia con hello `SqlUserDefinedProcessor` attributo, che è facoltativo per UDP.</span><span class="sxs-lookup"><span data-stu-id="68a11-390">toodefine a UDP, we need toocreate an `IProcessor` interface with hello `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span></span>

<span data-ttu-id="68a11-391">Questa interfaccia deve contenere la definizione di hello per hello `IRow` interfaccia rowset esegue l'override, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="68a11-391">This interface should contain hello definition for hello `IRow` interface rowset override, as shown in hello following example:</span></span>

```
[SqlUserDefinedProcessor]
public class MyProcessor: IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
        …
 }
}
```

<span data-ttu-id="68a11-392">**SqlUserDefinedProcessor** indica che il tipo di hello deve essere registrato come un processore definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="68a11-392">**SqlUserDefinedProcessor** indicates that hello type should be registered as a user-defined processor.</span></span> <span data-ttu-id="68a11-393">Questa classe non può essere ereditata.</span><span class="sxs-lookup"><span data-stu-id="68a11-393">This class cannot be inherited.</span></span>

<span data-ttu-id="68a11-394">attributo SqlUserDefinedProcessor Hello è **facoltativo** per la definizione di UDP.</span><span class="sxs-lookup"><span data-stu-id="68a11-394">hello SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span></span>

<span data-ttu-id="68a11-395">gli oggetti di programmabilità principale Hello sono **input** e **output**.</span><span class="sxs-lookup"><span data-stu-id="68a11-395">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="68a11-396">oggetto di input Hello è tooenumerate utilizzate colonne di input e output e tooset i dati di output come risultato dell'attività del processore hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-396">hello input object is used tooenumerate input columns and output, and tooset output data as a result of hello processor activity.</span></span>

<span data-ttu-id="68a11-397">Per l'enumerazione delle colonne di input, utilizziamo hello `input.Get` metodo.</span><span class="sxs-lookup"><span data-stu-id="68a11-397">For input columns enumeration, we use hello `input.Get` method.</span></span>

```
string column_name = input.Get<string>("column_name");
```

<span data-ttu-id="68a11-398">parametro per Hello `input.Get` metodo è una colonna che viene passata come parte di hello `PRODUCE` clausola di hello `PROCESS` istruzione dello script di base hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="68a11-398">hello parameter for `input.Get` method is a column that's passed as part of hello `PRODUCE` clause of hello `PROCESS` statement of hello U-SQL base script.</span></span> <span data-ttu-id="68a11-399">È necessario toouse il tipo di dati corretto hello è qui.</span><span class="sxs-lookup"><span data-stu-id="68a11-399">We need toouse hello correct data type here.</span></span>

<span data-ttu-id="68a11-400">Per l'output, utilizzare hello `output.Set` metodo.</span><span class="sxs-lookup"><span data-stu-id="68a11-400">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="68a11-401">È importante solo toonote che produttore personalizzato restituisce le colonne e i valori che sono definiti con hello `output.Set` chiamata al metodo.</span><span class="sxs-lookup"><span data-stu-id="68a11-401">It's important toonote that custom producer only outputs columns and values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", mycolumn);
```

<span data-ttu-id="68a11-402">output di Hello effettiva del processore è attivato chiamando `return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="68a11-402">hello actual processor output is triggered by calling `return output.AsReadOnly();`.</span></span>

<span data-ttu-id="68a11-403">Di seguito è riportato un esempio di elaboratore:</span><span class="sxs-lookup"><span data-stu-id="68a11-403">Following is a processor example:</span></span>

```
[SqlUserDefinedProcessor]
public class FullDescriptionProcessor : IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
     string user = input.Get<string>("user");
     string des = input.Get<string>("des");
     string full_description = user.ToUpper() + "=>" + des;
     output.Set<string>("dt", input.Get<string>("dt"));
     output.Set<string>("full_description", full_description);
     output.Set<Guid>("new_guid", Guid.NewGuid());
     output.Set<Guid>("guid", input.Get<Guid>("guid"));
     return output.AsReadOnly();
 }
}
```

<span data-ttu-id="68a11-404">In questo scenario, in caso di utilizzo processore hello genera una nuova colonna denominata "full_description" combinando hello colonne esistenti, in questo caso, "user" in lettere maiuscole e "des".</span><span class="sxs-lookup"><span data-stu-id="68a11-404">In this use-case scenario, hello processor is generating a new column called “full_description” by combining hello existing columns--in this case, “user” in upper case, and “des”.</span></span> <span data-ttu-id="68a11-405">Inoltre, rigenera un GUID e restituisce i valori GUID hello originali e quello nuovi.</span><span class="sxs-lookup"><span data-stu-id="68a11-405">It also regenerates a GUID and returns hello original and new GUID values.</span></span>

<span data-ttu-id="68a11-406">Come si può vedere dal hello precedente esempio, è possibile chiamare metodi c# durante `output.Set` chiamata al metodo.</span><span class="sxs-lookup"><span data-stu-id="68a11-406">As you can see from hello previous example, you can call C# methods during `output.Set` method call.</span></span>

<span data-ttu-id="68a11-407">Di seguito è riportato un esempio di script U-SQL di base che usa un elaboratore personalizzato:</span><span class="sxs-lookup"><span data-stu-id="68a11-407">Following is an example of base U-SQL script that uses a custom processor:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
     PROCESS @rs0
     PRODUCE dt String,
             full_description String,
             guid Guid,
             new_guid Guid
     USING new USQL_Programmability.FullDescriptionProcessor();

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-appliers"></a><span data-ttu-id="68a11-408">Usare oggetti di applicazione definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="68a11-408">Use user-defined appliers</span></span>
<span data-ttu-id="68a11-409">Un oggetto di applicazione U-SQL definita dall'utente consente la funzione tooinvoke personalizzata in c# per ogni riga restituita dall'espressione di tabella esterna hello di una query.</span><span class="sxs-lookup"><span data-stu-id="68a11-409">A U-SQL user-defined applier enables you tooinvoke a custom C# function for each row that's returned by hello outer table expression of a query.</span></span> <span data-ttu-id="68a11-410">input di destra Hello viene valutata per ogni riga dall'input di sinistra hello e le righe di hello che sono state prodotte vengono combinate per l'output di hello finale.</span><span class="sxs-lookup"><span data-stu-id="68a11-410">hello right input is evaluated for each row from hello left input, and hello rows that are produced are combined for hello final output.</span></span> <span data-ttu-id="68a11-411">elenco di Hello colonne generate dall'operatore APPLY hello sono combinazione hello di set di hello di colonne a sinistra di hello e hello input di destra.</span><span class="sxs-lookup"><span data-stu-id="68a11-411">hello list of columns that are produced by hello APPLY operator are hello combination of hello set of columns in hello left and hello right input.</span></span>

<span data-ttu-id="68a11-412">Oggetto di applicazione definito dall'utente viene richiamato come parte dell'espressione SELECT USQL hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-412">User-defined applier is being invoked as part of hello USQL SELECT expression.</span></span>

<span data-ttu-id="68a11-413">Hello tipica chiamata toohello definito dall'utente dell'oggetto di applicazione ha un aspetto simile hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="68a11-413">hello typical call toohello user-defined applier looks like hello following:</span></span>

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

<span data-ttu-id="68a11-414">Per altre informazioni sull'uso di oggetti di applicazione in un'espressione SELECT, vedere [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx) (Selezione con SELECT di U-SQL da CROSS APPLY e OUTER APPLY).</span><span class="sxs-lookup"><span data-stu-id="68a11-414">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span></span>

<span data-ttu-id="68a11-415">definizione Hello definito dall'utente dell'oggetto di applicazione della classe base è la seguente:</span><span class="sxs-lookup"><span data-stu-id="68a11-415">hello user-defined applier base class definition is as follows:</span></span>

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

<span data-ttu-id="68a11-416">toodefine un oggetto di applicazione definito dall'utente, è necessario hello toocreate `IApplier` interfaccia con hello [`SqlUserDefinedApplier`] attributo, che è facoltativo per una definizione di applicazione modifiche definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="68a11-416">toodefine a user-defined applier, we need toocreate hello `IApplier` interface with hello [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span></span>

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
    public ParserApplier()
    {
        …
    }

    public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
    {
        …
    }
}
```

* <span data-ttu-id="68a11-417">Applicare viene chiamato per ogni riga della tabella esterna hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-417">Apply is called for each row of hello outer table.</span></span> <span data-ttu-id="68a11-418">Restituisce hello `IUpdatableRow` set di righe di output.</span><span class="sxs-lookup"><span data-stu-id="68a11-418">It returns hello `IUpdatableRow` output rowset.</span></span>
* <span data-ttu-id="68a11-419">classe di costruttore Hello è oggetto di applicazione modifiche definite dall'utente di toopass utilizzati parametri toohello.</span><span class="sxs-lookup"><span data-stu-id="68a11-419">hello Constructor class is used toopass parameters toohello user-defined applier.</span></span>

<span data-ttu-id="68a11-420">**SqlUserDefinedApplier** indica che il tipo di hello deve essere registrato come un oggetto di applicazione definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="68a11-420">**SqlUserDefinedApplier** indicates that hello type should be registered as a user-defined applier.</span></span> <span data-ttu-id="68a11-421">Questa classe non può essere ereditata.</span><span class="sxs-lookup"><span data-stu-id="68a11-421">This class cannot be inherited.</span></span>

<span data-ttu-id="68a11-422">**SqlUserDefinedApplier** è **facoltativo** per la definizione di un oggetto di applicazione definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="68a11-422">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span></span>


<span data-ttu-id="68a11-423">gli oggetti di programmabilità principale Hello sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="68a11-423">hello main programmability objects are as follows:</span></span>

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

<span data-ttu-id="68a11-424">I set di righe di input vengono passati come input `IRow`.</span><span class="sxs-lookup"><span data-stu-id="68a11-424">Input rowsets are passed as `IRow` input.</span></span> <span data-ttu-id="68a11-425">Hello righe di output vengono generate come `IUpdatableRow` interfaccia output.</span><span class="sxs-lookup"><span data-stu-id="68a11-425">hello output rows are generated as `IUpdatableRow` output interface.</span></span>

<span data-ttu-id="68a11-426">Nomi delle singole colonne può essere determinati dal chiamante hello `IRow` metodo dello Schema.</span><span class="sxs-lookup"><span data-stu-id="68a11-426">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="68a11-427">valori dei dati effettivi da hello in arrivo tooget hello `IRow`, viene utilizzato il metodo Get () hello di `IRow` interfaccia.</span><span class="sxs-lookup"><span data-stu-id="68a11-427">tooget hello actual data values from hello incoming `IRow`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="68a11-428">O utilizziamo nome di colonna dello schema hello:</span><span class="sxs-lookup"><span data-stu-id="68a11-428">Or we use hello schema column name:</span></span>

```
row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="68a11-429">Hello valori di output devono essere impostati con `IUpdatableRow` output:</span><span class="sxs-lookup"><span data-stu-id="68a11-429">hello output values must be set with `IUpdatableRow` output:</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="68a11-430">È importante toounderstand appliers personalizzato output solo le colonne e i valori che sono definiti con `output.Set` chiamata al metodo.</span><span class="sxs-lookup"><span data-stu-id="68a11-430">It is important toounderstand that custom appliers only output columns and values that are defined with `output.Set` method call.</span></span>

<span data-ttu-id="68a11-431">output di Hello effettivo viene attivato chiamando `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="68a11-431">hello actual output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="68a11-432">parametri di Hello definiti dall'utente dell'oggetto di applicazione possono essere passati toohello costruttore.</span><span class="sxs-lookup"><span data-stu-id="68a11-432">hello user-defined applier parameters can be passed toohello constructor.</span></span> <span data-ttu-id="68a11-433">Oggetto di applicazione può restituire un numero variabile di colonne che devono toobe definiti durante la chiamata dell'oggetto di applicazione di hello in base uno Script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="68a11-433">Applier can return a variable number of columns that need toobe defined during hello applier call in base U-SQL Script.</span></span>

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

<span data-ttu-id="68a11-434">Ecco hello definito dall'utente dell'oggetto di applicazione esempio:</span><span class="sxs-lookup"><span data-stu-id="68a11-434">Here is hello user-defined applier example:</span></span>

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
private string parsingPart;

public ParserApplier(string parsingPart)
{
    if (parsingPart.ToUpper().Contains("ALL")
    || parsingPart.ToUpper().Contains("MAKE")
    || parsingPart.ToUpper().Contains("MODEL")
    || parsingPart.ToUpper().Contains("YEAR")
    || parsingPart.ToUpper().Contains("TYPE")
    || parsingPart.ToUpper().Contains("MILLAGE")
    )
    {
    this.parsingPart = parsingPart;
    }
    else
    {
    throw new ArgumentException("Incorrect parameter. Please use: 'ALL[MAKE|MODEL|TYPE|MILLAGE]'");
    }
}

public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
{

    string[] properties = input.Get<string>("properties").Split(',');

    //  only process with correct number of properties
    if (properties.Count() == 5)
    {

    string make = properties[0];
    string model = properties[1];
    string year = properties[2];
    string type = properties[3];
    int millage = -1;

    // Only return millage if it is number, otherwise, -1
    if (!int.TryParse(properties[4], out millage))
    {
        millage = -1;
    }

    if (parsingPart.ToUpper().Contains("MAKE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("make", make);
    if (parsingPart.ToUpper().Contains("MODEL") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("model", model);
    if (parsingPart.ToUpper().Contains("YEAR") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("year", year);
    if (parsingPart.ToUpper().Contains("TYPE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("type", type);
    if (parsingPart.ToUpper().Contains("MILLAGE") || parsingPart.ToUpper().Contains("ALL")) output.Set<int>("millage", millage);
    }
    yield return output.AsReadOnly();            
}
}
```

<span data-ttu-id="68a11-435">Di seguito è script U-SQL base hello per questo oggetto di applicazione definito dall'utente:</span><span class="sxs-lookup"><span data-stu-id="68a11-435">Following is hello base U-SQL script for this user-defined applier:</span></span>

```
DECLARE @input_file string = @"c:\usql-programmability\car_fleet.tsv";
DECLARE @output_file string = @"c:\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        stocknumber int,
        vin String,
        properties String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT
        r.stocknumber,
        r.vin,
        properties.make,
        properties.model,
        properties.year,
        properties.type,
        properties.millage
    FROM @rs0 AS r
    CROSS APPLY
    new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

<span data-ttu-id="68a11-436">In questo scenario di caso di utilizzo definiti dall'utente dell'oggetto di applicazione funge da un parser delimitato da virgole per auto hello flotta proprietà.</span><span class="sxs-lookup"><span data-stu-id="68a11-436">In this use case scenario, user-defined applier acts as a comma-delimited value parser for hello car fleet properties.</span></span> <span data-ttu-id="68a11-437">le righe di file di input Hello aspetto hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="68a11-437">hello input file rows look like hello following:</span></span>

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

<span data-ttu-id="68a11-438">Si tratta di un normale file con valori delimitati da tabulazioni (TSV) con una colonna di proprietà contenente le proprietà delle automobili, come marca e modello.</span><span class="sxs-lookup"><span data-stu-id="68a11-438">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span></span> <span data-ttu-id="68a11-439">Tali proprietà devono essere analizzati toohello le colonne della tabella.</span><span class="sxs-lookup"><span data-stu-id="68a11-439">Those properties must be parsed toohello table columns.</span></span> <span data-ttu-id="68a11-440">oggetto di applicazione Hello fornito consente inoltre toogenerate dinamico alcune proprietà in hello generare set di righe, in base a un parametro hello viene passato.</span><span class="sxs-lookup"><span data-stu-id="68a11-440">hello applier that's provided also enables you toogenerate a dynamic number of properties in hello result rowset, based on hello parameter that's passed.</span></span> <span data-ttu-id="68a11-441">È possibile generare tutte le proprietà o solo uno specifico set di proprietà.</span><span class="sxs-lookup"><span data-stu-id="68a11-441">You can generate either all properties or a specific set of properties only.</span></span>

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

<span data-ttu-id="68a11-442">oggetto di applicazione definito dall'utente Hello può essere chiamato come una nuova istanza dell'oggetto dell'oggetto di applicazione:</span><span class="sxs-lookup"><span data-stu-id="68a11-442">hello user-defined applier can be called as a new instance of applier object:</span></span>

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

<span data-ttu-id="68a11-443">O con la chiamata di un metodo factory wrapper hello:</span><span class="sxs-lookup"><span data-stu-id="68a11-443">Or with hello invocation of a wrapper factory method:</span></span>

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a><span data-ttu-id="68a11-444">Usare combinatori definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="68a11-444">Use user-defined combiners</span></span>
<span data-ttu-id="68a11-445">Funzione di combinazione definita dall'utente o UDC, consente toocombine righe dal set di righe sinistro e destro, in base alla logica personalizzata.</span><span class="sxs-lookup"><span data-stu-id="68a11-445">User-defined combiner, or UDC, enables you toocombine rows from left and right rowsets, based on custom logic.</span></span> <span data-ttu-id="68a11-446">Il combinatore definito dall'utente viene usato con l'espressione COMBINE.</span><span class="sxs-lookup"><span data-stu-id="68a11-446">User-defined combiner is used with COMBINE expression.</span></span>

<span data-ttu-id="68a11-447">Viene richiamato una funzione di combinazione di espressioni COMBINARE hello che fornisce le informazioni necessarie su entrambi i set di righe input hello hello, raggruppamento di colonne, hello hello previsto schema di risultati e informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="68a11-447">A combiner is being invoked with hello COMBINE expression that provides hello necessary information about both hello input rowsets, hello grouping columns, hello expected result schema, and additional information.</span></span>

<span data-ttu-id="68a11-448">toocall una funzione di combinazione di uno script U-SQL di base, utilizziamo hello la seguente sintassi:</span><span class="sxs-lookup"><span data-stu-id="68a11-448">toocall a combiner in a base U-SQL script, we use hello following syntax:</span></span>

```
Combine_Expression :=
    'COMBINE' Combine_Input
    'WITH' Combine_Input
    Join_On_Clause
    Produce_Clause
    [Readonly_Clause]
    [Required_Clause]
    USING_Clause.
```

<span data-ttu-id="68a11-449">Per altre informazioni, vedere [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx) (Espressione COMBINE (U-SQL)).</span><span class="sxs-lookup"><span data-stu-id="68a11-449">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span></span>

<span data-ttu-id="68a11-450">toodefine una funzione di combinazione definita dall'utente, è necessario hello toocreate `ICombiner` interfaccia con hello [`SqlUserDefinedCombiner`] attributo, che è facoltativo per una definizione di funzione di combinazione definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="68a11-450">toodefine a user-defined combiner, we need toocreate hello `ICombiner` interface with hello [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span></span>

<span data-ttu-id="68a11-451">Definizione della classe `ICombiner` di base:</span><span class="sxs-lookup"><span data-stu-id="68a11-451">Base `ICombiner` class definition:</span></span>

```
public abstract class ICombiner : IUserDefinedOperator
{
protected ICombiner();
public virtual IEnumerable<IRow> Combine(List<IRowset> inputs,
       IUpdatableRow output);
public abstract IEnumerable<IRow> Combine(IRowset left, IRowset right,
       IUpdatableRow output);
}
```

<span data-ttu-id="68a11-452">Hello implementazione personalizzata di un `ICombiner` interfaccia deve contenere la definizione di hello per un `IEnumerable<IRow>` combinare override.</span><span class="sxs-lookup"><span data-stu-id="68a11-452">hello custom implementation of an `ICombiner` interface should contain hello definition for an `IEnumerable<IRow>` Combine override.</span></span>

```
[SqlUserDefinedCombiner]
public class MyCombiner : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    …
}
}
```

<span data-ttu-id="68a11-453">Hello **SqlUserDefinedCombiner** attributo indica che il tipo di hello deve essere registrato come una funzione di combinazione definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="68a11-453">hello **SqlUserDefinedCombiner** attribute indicates that hello type should be registered as a user-defined combiner.</span></span> <span data-ttu-id="68a11-454">Questa classe non può essere ereditata.</span><span class="sxs-lookup"><span data-stu-id="68a11-454">This class cannot be inherited.</span></span>

<span data-ttu-id="68a11-455">**SqlUserDefinedCombiner** è proprietà della modalità di combinazione canali hello toodefine utilizzato.</span><span class="sxs-lookup"><span data-stu-id="68a11-455">**SqlUserDefinedCombiner** is used toodefine hello Combiner mode property.</span></span> <span data-ttu-id="68a11-456">È un attributo facoltativo per la definizione di un combinatore definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="68a11-456">It is an optional attribute for a user-defined combiner definition.</span></span>

<span data-ttu-id="68a11-457">Modalità     CombinerMode</span><span class="sxs-lookup"><span data-stu-id="68a11-457">CombinerMode     Mode</span></span>

<span data-ttu-id="68a11-458">Enumerazione CombinerMode può assumere hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="68a11-458">CombinerMode enum can take hello following values:</span></span>

* <span data-ttu-id="68a11-459">Full (0) di da che ogni riga di output dipende potenzialmente da tutte le righe di input hello sinistra e destra con hello stesso valore della chiave.</span><span class="sxs-lookup"><span data-stu-id="68a11-459">Full  (0) Every output row potentially depends on all hello input rows from left and right       with hello same key value.</span></span>

* <span data-ttu-id="68a11-460">A sinistra (1) ogni riga di output dipende da una singola riga di input da sinistra hello (e potenzialmente tutte le righe da hello destra con hello stesso valore della chiave).</span><span class="sxs-lookup"><span data-stu-id="68a11-460">Left  (1) Every output row depends on a single input row from hello left (and potentially all rows       from hello right with hello same key value).</span></span>

* <span data-ttu-id="68a11-461">Right (2) ogni riga di output dipende da una singola riga di input da hello destra (e potenzialmente tutte le righe da sinistra hello con hello stesso valore della chiave).</span><span class="sxs-lookup"><span data-stu-id="68a11-461">Right (2)     Every output row depends on a single input row from hello right (and potentially all rows       from hello left with hello same key value).</span></span>

* <span data-ttu-id="68a11-462">Riga interna (3) ogni riga di output dipende da un singolo input da sinistra e destra con hello stesso valore.</span><span class="sxs-lookup"><span data-stu-id="68a11-462">Inner (3) Every output row depends on a single input row from left and right with hello same value.</span></span>

<span data-ttu-id="68a11-463">Esempio:     [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span><span class="sxs-lookup"><span data-stu-id="68a11-463">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span></span>


<span data-ttu-id="68a11-464">oggetti di programmabilità principale Hello sono:</span><span class="sxs-lookup"><span data-stu-id="68a11-464">hello main programmability objects are:</span></span>

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

<span data-ttu-id="68a11-465">I set di righe di input vengono passati come tipo di interfaccia `IRowset` a **sinistra** e a **destra**.</span><span class="sxs-lookup"><span data-stu-id="68a11-465">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span></span> <span data-ttu-id="68a11-466">Entrambi i set di righe devono essere enumerati per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="68a11-466">Both rowsets must be enumerated for processing.</span></span> <span data-ttu-id="68a11-467">È solo possibile enumerare ogni interfaccia di una volta, sono tooenumerate e memorizzarlo nella cache se necessario.</span><span class="sxs-lookup"><span data-stu-id="68a11-467">You can only enumerate each interface once, so we have tooenumerate and cache it if necessary.</span></span>

<span data-ttu-id="68a11-468">Per la memorizzazione nella cache, è possibile creare un tipo di struttura di memoria List\<T\> come risultato dell'esecuzione di una query LINQ, specificamente List<`IRow`>.</span><span class="sxs-lookup"><span data-stu-id="68a11-468">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span></span> <span data-ttu-id="68a11-469">tipo di dati anonimi Hello può essere utilizzato durante l'enumerazione anche.</span><span class="sxs-lookup"><span data-stu-id="68a11-469">hello anonymous data type can be used during enumeration as well.</span></span>

<span data-ttu-id="68a11-470">Vedere [introduzione tooLINQ query (c#)](https://msdn.microsoft.com/library/bb397906.aspx) per ulteriori informazioni sulle query LINQ, e [IEnumerable\<T\> interfaccia](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) per ulteriori informazioni su IEnumerable\<T\> interfaccia.</span><span class="sxs-lookup"><span data-stu-id="68a11-470">See [Introduction tooLINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span></span>

<span data-ttu-id="68a11-471">valori dei dati effettivi da hello in arrivo tooget hello `IRowset`, viene utilizzato il metodo Get () hello di `IRow` interfaccia.</span><span class="sxs-lookup"><span data-stu-id="68a11-471">tooget hello actual data values from hello incoming `IRowset`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="68a11-472">Nomi delle singole colonne può essere determinati dal chiamante hello `IRow` metodo dello Schema.</span><span class="sxs-lookup"><span data-stu-id="68a11-472">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="68a11-473">O con nome di colonna dello schema hello:</span><span class="sxs-lookup"><span data-stu-id="68a11-473">Or by using hello schema column name:</span></span>

```
c# row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="68a11-474">Enumerazione generale di Hello con LINQ è simile hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="68a11-474">hello general enumeration with LINQ looks like hello following:</span></span>

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

<span data-ttu-id="68a11-475">Dopo l'enumerazione di entrambi i set di righe, verrà tooloop in tutte le righe.</span><span class="sxs-lookup"><span data-stu-id="68a11-475">After enumerating both rowsets, we are going tooloop through all rows.</span></span> <span data-ttu-id="68a11-476">Per ogni riga nel set di righe a sinistra di hello, verrà toofind tutte le righe che soddisfano la condizione hello della funzione di combinazione.</span><span class="sxs-lookup"><span data-stu-id="68a11-476">For each row in hello left rowset, we are going toofind all rows that satisfy hello condition of our combiner.</span></span>

<span data-ttu-id="68a11-477">Hello valori di output devono essere impostati con `IUpdatableRow` output.</span><span class="sxs-lookup"><span data-stu-id="68a11-477">hello output values must be set with `IUpdatableRow` output.</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="68a11-478">output di Hello effettivo viene attivato chiamando troppo`yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="68a11-478">hello actual output is triggered by calling too`yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="68a11-479">Di seguito è riportato un esempio di combinatore:</span><span class="sxs-lookup"><span data-stu-id="68a11-479">Following is a combiner example:</span></span>

```
[SqlUserDefinedCombiner]
public class CombineSales : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    var internetSales =
    (from row in left.Rows
          select new
          {
              ProductKey = row.Get<int>("ProductKey"),
              OrderDateKey = row.Get<int>("OrderDateKey"),
              SalesAmount = row.Get<decimal>("SalesAmount"),
              TaxAmt = row.Get<decimal>("TaxAmt")
          }).ToList();

    var resellerSales =
    (from row in right.Rows
     select new
     {
     ProductKey = row.Get<int>("ProductKey"),
     OrderDateKey = row.Get<int>("OrderDateKey"),
     SalesAmount = row.Get<decimal>("SalesAmount"),
     TaxAmt = row.Get<decimal>("TaxAmt")
     }).ToList();

    foreach (var row_i in internetSales)
    {
    foreach (var row_r in resellerSales)
    {

        if (
        row_i.OrderDateKey > 0
        && row_i.OrderDateKey < row_r.OrderDateKey
        && row_i.OrderDateKey == 20010701
        && (row_r.SalesAmount + row_r.TaxAmt) > 20000)
        {
        output.Set<int>("OrderDateKey", row_i.OrderDateKey);
        output.Set<int>("ProductKey", row_i.ProductKey);
        output.Set<decimal>("Internet_Sales_Amount", row_i.SalesAmount + row_i.TaxAmt);
        output.Set<decimal>("Reseller_Sales_Amount", row_r.SalesAmount + row_r.TaxAmt);
        }

    }
    }
    yield return output.AsReadOnly();
}
}
```

<span data-ttu-id="68a11-480">In questo scenario, in caso di utilizzo che si sta creando un report di analitica rivenditore hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-480">In this use-case scenario, we are building an analytics report for hello retailer.</span></span> <span data-ttu-id="68a11-481">obiettivo di Hello è toofind tutti i prodotti che costano più di 20.000 $ e che vendono tramite sito Web di hello più veloce tramite rivenditore di regolare hello all'interno di un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="68a11-481">hello goal is toofind all products that cost more than $20,000 and that sell through hello website faster than through hello regular retailer within a certain time frame.</span></span>

<span data-ttu-id="68a11-482">Di seguito è riportato uno script U-SQL di base hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-482">Here is hello base U-SQL script.</span></span> <span data-ttu-id="68a11-483">È possibile confrontare la logica di hello tra un JOIN normale e una funzione di combinazione:</span><span class="sxs-lookup"><span data-stu-id="68a11-483">You can compare hello logic between a regular JOIN and a combiner:</span></span>

```sql
DECLARE @LocalURI string = @"\usql-programmability\";

DECLARE @input_file_internet_sales string = @LocalURI+"FactInternetSales.txt";
DECLARE @input_file_reseller_sales string = @LocalURI+"FactResellerSales.txt";
DECLARE @output_file1 string = @LocalURI+"output_file1.tsv";
DECLARE @output_file2 string = @LocalURI+"output_file2.tsv";

@fact_internet_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    CustomerKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_internet_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@fact_reseller_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    ResellerKey int ,
    EmployeeKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_reseller_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@rs1 =
SELECT
    fis.OrderDateKey,
    fis.ProductKey,
    fis.SalesAmount+fis.TaxAmt AS Internet_Sales_Amount,
    frs.SalesAmount+frs.TaxAmt AS Reseller_Sales_Amount
FROM @fact_internet_sales AS fis
     INNER JOIN @fact_reseller_sales AS frs
     ON fis.ProductKey == frs.ProductKey
WHERE
    fis.OrderDateKey < frs.OrderDateKey
    AND fis.OrderDateKey == 20010701
    AND frs.SalesAmount+frs.TaxAmt > 20000;

@rs2 =
COMBINE @fact_internet_sales AS fis
WITH @fact_reseller_sales AS frs
ON fis.ProductKey == frs.ProductKey
PRODUCE OrderDateKey int,
        ProductKey int,
        Internet_Sales_Amount decimal,
        Reseller_Sales_Amount decimal
USING new USQL_Programmability.CombineSales();

OUTPUT @rs1 too@output_file1 USING Outputters.Tsv();
OUTPUT @rs2 too@output_file2 USING Outputters.Tsv();
```

<span data-ttu-id="68a11-484">Una funzione di combinazione definita dall'utente può essere chiamato come una nuova istanza dell'oggetto dell'oggetto di applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="68a11-484">A user-defined combiner can be called as a new instance of hello applier object:</span></span>

```
USING new MyNameSpace.MyCombiner();
```


<span data-ttu-id="68a11-485">O con la chiamata di un metodo factory wrapper hello:</span><span class="sxs-lookup"><span data-stu-id="68a11-485">Or with hello invocation of a wrapper factory method:</span></span>

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a><span data-ttu-id="68a11-486">Usare riduttori definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="68a11-486">Use user-defined reducers</span></span>

<span data-ttu-id="68a11-487">U-SQL consente toowrite riduttori di set di righe personalizzata in c# tramite framework di estendibilità di hello operatore definito dall'utente e l'implementazione di un'interfaccia IReducer.</span><span class="sxs-lookup"><span data-stu-id="68a11-487">U-SQL enables you toowrite custom rowset reducers in C# by using hello user-defined operator extensibility framework and implementing an IReducer interface.</span></span>

<span data-ttu-id="68a11-488">Riduttore definito dall'utente o UDR, possono essere utilizzati tooeliminate le righe non necessarie durante l'estrazione di dati (importazione).</span><span class="sxs-lookup"><span data-stu-id="68a11-488">User-defined reducer, or UDR, can be used tooeliminate unnecessary rows during data extraction (import).</span></span> <span data-ttu-id="68a11-489">Inoltre può essere utilizzato toomanipulate e valutare le righe e colonne.</span><span class="sxs-lookup"><span data-stu-id="68a11-489">It also can be used toomanipulate and evaluate rows and columns.</span></span> <span data-ttu-id="68a11-490">In base alla logica di programmazione, inoltre possibile definire quali righe devono toobe estratti.</span><span class="sxs-lookup"><span data-stu-id="68a11-490">Based on programmability logic, it can also define which rows need toobe extracted.</span></span>

<span data-ttu-id="68a11-491">una classe UDR toodefine, dobbiamo toocreate un `IReducer` interfaccia con un parametro facoltativo `SqlUserDefinedReducer` attributo.</span><span class="sxs-lookup"><span data-stu-id="68a11-491">toodefine a UDR class, we need toocreate an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span></span>

<span data-ttu-id="68a11-492">Questa interfaccia di classe deve contenere una definizione per hello `IEnumerable` eseguire l'override di set di righe di interfaccia.</span><span class="sxs-lookup"><span data-stu-id="68a11-492">This class interface should contain a definition for hello `IEnumerable` interface rowset override.</span></span>

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
        …
    }

}
```

<span data-ttu-id="68a11-493">Hello **SqlUserDefinedReducer** attributo indica che il tipo di hello deve essere registrato come un riduttore definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="68a11-493">hello **SqlUserDefinedReducer** attribute indicates that hello type should be registered as a user-defined reducer.</span></span> <span data-ttu-id="68a11-494">Questa classe non può essere ereditata.</span><span class="sxs-lookup"><span data-stu-id="68a11-494">This class cannot be inherited.</span></span>
<span data-ttu-id="68a11-495">**SqlUserDefinedReducer** è un attributo facoltativo per la definizione di un riduttore definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="68a11-495">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span></span> <span data-ttu-id="68a11-496">Proprietà IsRecursive toodefine è utilizzato.</span><span class="sxs-lookup"><span data-stu-id="68a11-496">It's used toodefine IsRecursive property.</span></span>

* <span data-ttu-id="68a11-497">bool     IsRecursive</span><span class="sxs-lookup"><span data-stu-id="68a11-497">bool     IsRecursive</span></span>    
* <span data-ttu-id="68a11-498">**true**  = indica se il riduttore è idempotente</span><span class="sxs-lookup"><span data-stu-id="68a11-498">**true**  = Indicates whether this Reducer is idempotent</span></span>

<span data-ttu-id="68a11-499">gli oggetti di programmabilità principale Hello sono **input** e **output**.</span><span class="sxs-lookup"><span data-stu-id="68a11-499">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="68a11-500">oggetto di input Hello è tooenumerate utilizzato le righe di input.</span><span class="sxs-lookup"><span data-stu-id="68a11-500">hello input object is used tooenumerate input rows.</span></span> <span data-ttu-id="68a11-501">L'output è usato tooset righe di output in seguito a ridurre l'attività.</span><span class="sxs-lookup"><span data-stu-id="68a11-501">Output is used tooset output rows as a result of reducing activity.</span></span>

<span data-ttu-id="68a11-502">Per l'enumerazione delle righe di input, utilizziamo hello `Row.Get` metodo.</span><span class="sxs-lookup"><span data-stu-id="68a11-502">For input rows enumeration, we use hello `Row.Get` method.</span></span>

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

<span data-ttu-id="68a11-503">parametro per hello Hello `Row.Get` metodo è una colonna che viene passata come parte di hello `PRODUCE` classe di hello `REDUCE` istruzione dello script di base hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="68a11-503">hello parameter for hello `Row.Get` method is a column that's passed as part of hello `PRODUCE` class of hello `REDUCE` statement of hello U-SQL base script.</span></span> <span data-ttu-id="68a11-504">È necessario toouse hello tipo di dati corretto qui anche.</span><span class="sxs-lookup"><span data-stu-id="68a11-504">We need toouse hello correct data type here as well.</span></span>

<span data-ttu-id="68a11-505">Per l'output, utilizzare hello `output.Set` metodo.</span><span class="sxs-lookup"><span data-stu-id="68a11-505">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="68a11-506">È importante toounderstand che valori di output solo riduttore personalizzati che sono definiti con hello `output.Set` chiamata al metodo.</span><span class="sxs-lookup"><span data-stu-id="68a11-506">It is important toounderstand that custom reducer only outputs values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", guid);
```

<span data-ttu-id="68a11-507">output di Hello riduttore effettivo viene attivato chiamando `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="68a11-507">hello actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="68a11-508">Di seguito è riportato un esempio di riduttore:</span><span class="sxs-lookup"><span data-stu-id="68a11-508">Following is a reducer example:</span></span>

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
    string guid;
    DateTime dt;
    string user;
    string des;

    foreach (IRow row in input.Rows)
    {
        guid = row.Get<string>("guid");
        dt = row.Get<DateTime>("dt");
        user = row.Get<string>("user");
        des = row.Get<string>("des");

        if (user.Length > 0)
        {
        output.Set<string>("guid", guid);
        output.Set<DateTime>("dt", dt);
        output.Set<string>("user", user);
        output.Set<string>("des", des);

        yield return output.AsReadOnly();
        }
    }
    }

}
```

<span data-ttu-id="68a11-509">In questo scenario, in caso di utilizzo riduttore hello ignora le righe con un nome utente vuoto.</span><span class="sxs-lookup"><span data-stu-id="68a11-509">In this use-case scenario, hello reducer is skipping rows with an empty user name.</span></span> <span data-ttu-id="68a11-510">Per ogni riga nel set di righe, legge ogni colonna richiesta, quindi restituisce la lunghezza hello del nome utente hello.</span><span class="sxs-lookup"><span data-stu-id="68a11-510">For each row in rowset, it reads each required column, then evaluates hello length of hello user name.</span></span> <span data-ttu-id="68a11-511">Restituisce la riga effettiva hello solo se lunghezza del valore nome utente è maggiore di 0.</span><span class="sxs-lookup"><span data-stu-id="68a11-511">It outputs hello actual row only if user name value length is more than 0.</span></span>

<span data-ttu-id="68a11-512">Di seguito è riportato uno script U-SQL di base che usa un riduttore personalizzato:</span><span class="sxs-lookup"><span data-stu-id="68a11-512">Following is base U-SQL script that uses a custom reducer:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file_reducer.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    REDUCE @rs0 PRESORT guid
    ON guid  
    PRODUCE guid string, dt DateTime, user String, des String
    USING new USQL_Programmability.EmptyUserReducer();

@rs2 =
    SELECT guid AS start_id,
           dt AS start_time,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS start_fiscalperiod,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    too@output_file 
    USING Outputters.Text();
```
