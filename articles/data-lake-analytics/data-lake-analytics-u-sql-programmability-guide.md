---
title: "Guida alla programmabilità di U-SQL per Azure Data Lake | Microsoft Docs"
description: Informazioni sul set di servizi di Azure Data Lake che consente di creare una piattaforma Big Data basata sul cloud.
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
ms.openlocfilehash: e4e298475d7be7d51c8bd55be498371ed6ce77a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="u-sql-programmability-guide"></a><span data-ttu-id="59430-103">Guida alla programmabilità di U-SQL</span><span class="sxs-lookup"><span data-stu-id="59430-103">U-SQL programmability guide</span></span>

<span data-ttu-id="59430-104">U-SQL è un linguaggio di query progettato per carichi di lavoro di tipo Big Data.</span><span class="sxs-lookup"><span data-stu-id="59430-104">U-SQL is a query language that's designed for big data-type of workloads.</span></span> <span data-ttu-id="59430-105">Una delle caratteristiche esclusive di U-SQL è la combinazione tra linguaggio dichiarativo di tipo SQL e funzionalità di estendibilità e programmabilità del linguaggio C#.</span><span class="sxs-lookup"><span data-stu-id="59430-105">One of the unique features of U-SQL is the combination of the SQL-like declarative language with the extensibility and programmability that's provided by C#.</span></span> <span data-ttu-id="59430-106">Questa guida è incentrata sulle funzionalità di estendibilità e programmabilità del linguaggio U-SQL supportate da C#.</span><span class="sxs-lookup"><span data-stu-id="59430-106">In this guide, we concentrate on the extensibility and programmability of the U-SQL language that's enabled by C#.</span></span>

## <a name="requirements"></a><span data-ttu-id="59430-107">Requisiti</span><span class="sxs-lookup"><span data-stu-id="59430-107">Requirements</span></span>

<span data-ttu-id="59430-108">Scaricare e installare [Strumenti Azure Data Lake per Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="59430-108">Download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="get-started-with-u-sql"></a><span data-ttu-id="59430-109">Introduzione a U-SQL</span><span class="sxs-lookup"><span data-stu-id="59430-109">Get started with U-SQL</span></span>  

<span data-ttu-id="59430-110">Verrà ora esaminato il seguente script U-SQL:</span><span class="sxs-lookup"><span data-stu-id="59430-110">Let’s look at the following U-SQL script:</span></span>

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

<span data-ttu-id="59430-111">Definisce un set di righe chiamato @a e crea un set di righe chiamato @results da @a.</span><span class="sxs-lookup"><span data-stu-id="59430-111">It defines a RowSet called @a and creates a RowSet called @results from @a.</span></span>

## <a name="c-types-and-expressions-in-u-sql-script"></a><span data-ttu-id="59430-112">Tipi ed espressioni C# in uno script U-SQL</span><span class="sxs-lookup"><span data-stu-id="59430-112">C# types and expressions in U-SQL script</span></span>

<span data-ttu-id="59430-113">Un'espressione U-SQL è un'espressione C# combinata con operazioni logiche U-SQL quali `AND`, `OR` e `NOT`.</span><span class="sxs-lookup"><span data-stu-id="59430-113">A U-SQL Expression is a C# expression combined with U-SQL logical operations such `AND`, `OR`, and `NOT`.</span></span> <span data-ttu-id="59430-114">Le espressioni U-SQL possono essere utilizzate con l'istruzione SELECT, EXTRACT, WHERE, HAVING, GROUP BY e DECLARE.</span><span class="sxs-lookup"><span data-stu-id="59430-114">U-SQL Expressions can be used with SELECT, EXTRACT, WHERE, HAVING, GROUP BY and DECLARE.</span></span>

<span data-ttu-id="59430-115">Ad esempio, lo script seguente analizza una stringa di un valore DateTime nella clausola SELECT.</span><span class="sxs-lookup"><span data-stu-id="59430-115">For example, the following script parses a string a DateTime value in the SELECT clause.</span></span>

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

<span data-ttu-id="59430-116">Lo script seguente analizza una stringa di un valore DateTime in un'istruzione DECLARE.</span><span class="sxs-lookup"><span data-stu-id="59430-116">The following script parses a string a DateTime value in a DECLARE statement.</span></span>

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a><span data-ttu-id="59430-117">Usare espressioni C# per conversioni del tipo di dati</span><span class="sxs-lookup"><span data-stu-id="59430-117">Use C# expressions for data type conversions</span></span>
<span data-ttu-id="59430-118">L'esempio seguente illustra come effettuare una conversione di dati di tipo datetime usando espressioni C#.</span><span class="sxs-lookup"><span data-stu-id="59430-118">The following example demonstrates how you can do a datetime data conversion by using C# expressions.</span></span> <span data-ttu-id="59430-119">In questo particolare scenario, i dati della stringa datetime vengono convertiti in datetime standard con la notazione dell'ora 00:00:00.</span><span class="sxs-lookup"><span data-stu-id="59430-119">In this particular scenario, string datetime data is converted to standard datetime with midnight 00:00:00 time notation.</span></span>

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a><span data-ttu-id="59430-120">Usare espressioni C# per la data odierna</span><span class="sxs-lookup"><span data-stu-id="59430-120">Use C# expressions for today’s date</span></span>
<span data-ttu-id="59430-121">Per effettuare il pull della data odierna, è possibile usare l'espressione C# seguente:</span><span class="sxs-lookup"><span data-stu-id="59430-121">To pull today’s date, we can use the following C# expression:</span></span>

```
DateTime.Now.ToString("M/d/yyyy")
```

<span data-ttu-id="59430-122">Di seguito è riportato un esempio di come usare questa espressione in uno script:</span><span class="sxs-lookup"><span data-stu-id="59430-122">Here's an example of how to use this expression in a script:</span></span>

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



## <a name="using-net-assemblies"></a><span data-ttu-id="59430-123">Uso di assembly .NET</span><span class="sxs-lookup"><span data-stu-id="59430-123">Using .NET assemblies</span></span>
<span data-ttu-id="59430-124">Il modello di estendibilità di U-SQL dipende in larga misura dalla possibilità di aggiungere codice personalizzato.</span><span class="sxs-lookup"><span data-stu-id="59430-124">U-SQL’s extensibility model relies heavily on the ability to add custom code.</span></span> <span data-ttu-id="59430-125">Attualmente, U-SQL consente di aggiungere facilmente codice basato su Microsoft .NET (in particolare C#).</span><span class="sxs-lookup"><span data-stu-id="59430-125">Currently, U-SQL provides you with easy ways to add your own Microsoft .NET-based code (in particular, C#).</span></span> <span data-ttu-id="59430-126">È anche possibile, tuttavia, aggiungere codice personalizzato scritto in altri linguaggi .NET, come VB.NET o F#.</span><span class="sxs-lookup"><span data-stu-id="59430-126">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span></span> 

### <a name="register-a-net-assembly"></a><span data-ttu-id="59430-127">Registrare un assembly .NET</span><span class="sxs-lookup"><span data-stu-id="59430-127">Register a .NET assembly</span></span>

<span data-ttu-id="59430-128">Utilizzare l'istruzione CREATE ASSEMBLY per inserire un assembly .NET in un database U-SQL.</span><span class="sxs-lookup"><span data-stu-id="59430-128">Use the CREATE ASSEMBLY statement to place a .NET assembly into a U-SQL Database.</span></span> <span data-ttu-id="59430-129">Dopo il posizionamento di un assembly in un database, gli script U-SQL possono utilizzare tali assembly per mezzo dell'istruzione REFERENCE ASSEMBLY.</span><span class="sxs-lookup"><span data-stu-id="59430-129">Once an assembly is in a database, U-SQL scripts can use those assemblies by using the REFERENCE ASSEMBLY statement.</span></span> 

<span data-ttu-id="59430-130">Nel codice seguente viene illustrato come registrare un assembly:</span><span class="sxs-lookup"><span data-stu-id="59430-130">The following code shows how to register an assembly:</span></span>

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

<span data-ttu-id="59430-131">Nel codice seguente viene illustrato come referenziare un assembly:</span><span class="sxs-lookup"><span data-stu-id="59430-131">The following code shows how to reference an assembly:</span></span>

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

<span data-ttu-id="59430-132">Consultare la [le istruzioni di registrazione assembly](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) che descrivono nel dettaglio questo argomento.</span><span class="sxs-lookup"><span data-stu-id="59430-132">Consult the [assembly registration instructions](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) that covers this topic in greater detail.</span></span>


### <a name="use-assembly-versioning"></a><span data-ttu-id="59430-133">Usare il controllo delle versioni degli assembly</span><span class="sxs-lookup"><span data-stu-id="59430-133">Use assembly versioning</span></span>
<span data-ttu-id="59430-134">Attualmente, U-SQL usa .NET Framework versione 4.5.</span><span class="sxs-lookup"><span data-stu-id="59430-134">Currently, U-SQL uses the .NET Framework version 4.5.</span></span> <span data-ttu-id="59430-135">Verificare quindi che i propri assembly siano compatibili con tale versione di runtime.</span><span class="sxs-lookup"><span data-stu-id="59430-135">So ensure that your own assemblies are compatible with that version of the runtime.</span></span>

<span data-ttu-id="59430-136">Come indicato in precedenza, U-SQL esegue il codice in un formato a 64 bit (x64).</span><span class="sxs-lookup"><span data-stu-id="59430-136">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span></span> <span data-ttu-id="59430-137">Verificare quindi che il codice venga compilato per l'esecuzione su x64.</span><span class="sxs-lookup"><span data-stu-id="59430-137">So make sure that your code is compiled to run on x64.</span></span> <span data-ttu-id="59430-138">In caso contrario verrà visualizzato l'errore di formato non corretto riportato sopra.</span><span class="sxs-lookup"><span data-stu-id="59430-138">Otherwise you get the incorrect format error shown earlier.</span></span>

<span data-ttu-id="59430-139">Ogni DLL di assembly e file di risorse caricato (ad esempio un diverso runtime, un assembly nativo o un file di configurazione) può essere al massimo di 400 MB.</span><span class="sxs-lookup"><span data-stu-id="59430-139">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span></span> <span data-ttu-id="59430-140">Le dimensioni totali delle risorse distribuite, tramite DEPLOY RESOURCE o riferimenti agli assembly e ai relativi file aggiuntivi, non possono superare 3 GB.</span><span class="sxs-lookup"><span data-stu-id="59430-140">The total size of deployed resources, either via DEPLOY RESOURCE or via references to assemblies and their additional files, cannot exceed 3 GB.</span></span>

<span data-ttu-id="59430-141">Si noti infine che ogni database U-SQL può contenere solo una versione di un determinato assembly.</span><span class="sxs-lookup"><span data-stu-id="59430-141">Finally, note that each U-SQL database can only contain one version of any given assembly.</span></span> <span data-ttu-id="59430-142">Se sono necessarie entrambe le versioni 7 e 8 della libreria NewtonSoft Json.Net, si devono registrare in due database diversi.</span><span class="sxs-lookup"><span data-stu-id="59430-142">For example, if you need both version 7 and version 8 of the NewtonSoft Json.Net library, you need to register them in two different databases.</span></span> <span data-ttu-id="59430-143">Ogni script, inoltre, può fare riferimento a una sola versione di una determinata DLL di assembly.</span><span class="sxs-lookup"><span data-stu-id="59430-143">Furthermore, each script can only refer to one version of a given assembly DLL.</span></span> <span data-ttu-id="59430-144">A tale riguardo, U-SQL segue la semantica di gestione e controllo delle versioni degli assembly di C#.</span><span class="sxs-lookup"><span data-stu-id="59430-144">In this respect, U-SQL follows the C# assembly management and versioning semantics.</span></span>


## <a name="use-user-defined-functions-udf"></a><span data-ttu-id="59430-145">Usare funzioni definite dall'utente (UDF)</span><span class="sxs-lookup"><span data-stu-id="59430-145">Use user-defined functions: UDF</span></span>
<span data-ttu-id="59430-146">Le funzioni definite dall'utente (UDF) di U-SQL sono routine di programmazione che accettano parametri, eseguono un'azione, ad esempio un calcolo complesso, e restituiscono il risultato di tale azione come valore.</span><span class="sxs-lookup"><span data-stu-id="59430-146">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return the result of that action as a value.</span></span> <span data-ttu-id="59430-147">Il valore restituito della funzione UDF può essere solo un valore scalare singolo.</span><span class="sxs-lookup"><span data-stu-id="59430-147">The return value of UDF can only be a single scalar.</span></span> <span data-ttu-id="59430-148">Una funzione UDF di U-SQL può essere chiamata nello script di base di U-SQL come qualsiasi altra funzione scalare di C#.</span><span class="sxs-lookup"><span data-stu-id="59430-148">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span></span>

<span data-ttu-id="59430-149">È consigliabile inizializzare le funzioni definite dall'utente di U-SQL come **public** e **static**.</span><span class="sxs-lookup"><span data-stu-id="59430-149">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span></span>

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

<span data-ttu-id="59430-150">Per prima cosa verrà esaminato il semplice esempio della creazione di una funzione definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59430-150">First let’s look at the simple example of creating a UDF.</span></span>

<span data-ttu-id="59430-151">Nello scenario di questo caso d'uso, è necessario determinare il periodo fiscale, ovvero il trimestre fiscale e il mese fiscale, del primo accesso dell'utente specifico.</span><span class="sxs-lookup"><span data-stu-id="59430-151">In this use-case scenario, we need to determine the fiscal period, including the fiscal quarter and fiscal month of the first sign-in for the specific user.</span></span> <span data-ttu-id="59430-152">In questo scenario, il primo mese dell'anno fiscale è giugno.</span><span class="sxs-lookup"><span data-stu-id="59430-152">The first fiscal month of the year in our scenario is June.</span></span>

<span data-ttu-id="59430-153">Per calcolare il periodo fiscale, si introduce la funzione C# seguente:</span><span class="sxs-lookup"><span data-stu-id="59430-153">To calculate fiscal period, we introduce the following C# function:</span></span>

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

<span data-ttu-id="59430-154">In questo modo vengono semplicemente calcolati il mese e il trimestre fiscali e viene restituito un valore stringa.</span><span class="sxs-lookup"><span data-stu-id="59430-154">It simply calculates fiscal month and quarter and returns a string value.</span></span> <span data-ttu-id="59430-155">Per giugno (primo mese del primo trimestre fiscale), si usa "Q1:P1",</span><span class="sxs-lookup"><span data-stu-id="59430-155">For June, the first month of the first fiscal quarter, we use "Q1:P1".</span></span> <span data-ttu-id="59430-156">per luglio "Q1:P2" e così via.</span><span class="sxs-lookup"><span data-stu-id="59430-156">For July, we use "Q1:P2", and so on.</span></span>

<span data-ttu-id="59430-157">Si tratta di una normale funzione C# che verrà usata nel progetto U-SQL.</span><span class="sxs-lookup"><span data-stu-id="59430-157">This is a regular C# function that we are going to use in our U-SQL project.</span></span>

<span data-ttu-id="59430-158">Di seguito è illustrato l'aspetto della sezione code-behind in questo scenario:</span><span class="sxs-lookup"><span data-stu-id="59430-158">Here is how the code-behind section looks in this scenario:</span></span>

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

<span data-ttu-id="59430-159">Ora si procede a chiamare la funzione dallo script U-SQL di base.</span><span class="sxs-lookup"><span data-stu-id="59430-159">Now we are going to call this function from the base U-SQL script.</span></span> <span data-ttu-id="59430-160">A tale scopo, è necessario specificare un nome completo per la funzione, includendo lo spazio dei nomi, in questo caso SpazioDeiNomi.Classe.Funzione(parametro).</span><span class="sxs-lookup"><span data-stu-id="59430-160">To do this, we have to provide a fully qualified name for the function, including the namespace, which in this case is NameSpace.Class.Function(parameter).</span></span>

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

<span data-ttu-id="59430-161">Di seguito è riportato l'effettivo script U-SQL di base:</span><span class="sxs-lookup"><span data-stu-id="59430-161">Following is the actual U-SQL base script:</span></span>

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
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="59430-162">Di seguito è riportato il file di output dell'esecuzione dello script:</span><span class="sxs-lookup"><span data-stu-id="59430-162">Following is the output file of the script execution:</span></span>

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

<span data-ttu-id="59430-163">In questo esempio viene illustrato un uso semplificato della funzione UDF inline in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="59430-163">This example demonstrates a simple usage of inline UDF in U-SQL.</span></span>

### <a name="keep-state-between-udf-invocations"></a><span data-ttu-id="59430-164">Mantenere lo stato tra chiamate di funzioni definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="59430-164">Keep state between UDF invocations</span></span>
<span data-ttu-id="59430-165">Gli oggetti di programmabilità C# in U-SQL possono essere resi più sofisticati introducendo l'interattività tramite variabili code-behind globali.</span><span class="sxs-lookup"><span data-stu-id="59430-165">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through the code-behind global variables.</span></span> <span data-ttu-id="59430-166">Verrà esaminato lo scenario del caso d'uso aziendale descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="59430-166">Let’s look at the following business use-case scenario.</span></span>

<span data-ttu-id="59430-167">Nelle grandi organizzazioni gli utenti possono accedere a svariate applicazioni interne,</span><span class="sxs-lookup"><span data-stu-id="59430-167">In large organizations, users can switch between varieties of internal applications.</span></span> <span data-ttu-id="59430-168">ad esempio Microsoft Dynamics CRM, Power BI e così via.</span><span class="sxs-lookup"><span data-stu-id="59430-168">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span></span> <span data-ttu-id="59430-169">I clienti potrebbero voler applicare un'analisi dei dati di telemetria relativamente al modo in cui gli utenti passano da un'applicazione all'altra, alle tendenze di utilizzo e così via.</span><span class="sxs-lookup"><span data-stu-id="59430-169">Customers might want to apply a telemetry analysis of how users switch between different applications, what the usage trends are, and so on.</span></span> <span data-ttu-id="59430-170">L'obiettivo per l'azienda è ottimizzare l'utilizzo delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="59430-170">The goal for the business is to optimize application usage.</span></span> <span data-ttu-id="59430-171">ed eventualmente combinare anche diverse applicazioni o specifiche routine di accesso.</span><span class="sxs-lookup"><span data-stu-id="59430-171">They also might want to combine different applications or specific sign-on routines.</span></span>

<span data-ttu-id="59430-172">Per raggiungere tale obiettivo, è necessario determinare gli ID sessione e l'intervallo di tempo rispetto all'ultima sessione eseguita.</span><span class="sxs-lookup"><span data-stu-id="59430-172">To achieve this goal, we have to determine session IDs and lag time between the last session that occurred.</span></span>

<span data-ttu-id="59430-173">È necessario trovare un accesso precedente e quindi assegnare tale accesso a tutte le sessioni generate per la stessa applicazione.</span><span class="sxs-lookup"><span data-stu-id="59430-173">We need to find a previous sign-in and then assign this sign-in to all sessions that are being generated to the same application.</span></span> <span data-ttu-id="59430-174">Il primo problema è che lo script U-SQL di base non consente di applicare calcoli sulle colonne già calcolate con la funzione LAG.</span><span class="sxs-lookup"><span data-stu-id="59430-174">The first challenge is that U-SQL base script doesn't allow us to apply calculations over already-calculated columns with LAG function.</span></span> <span data-ttu-id="59430-175">Il secondo problema è che è necessario mantenere la sessione specifica per tutte le sessioni incluse nello stesso periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="59430-175">The second challenge is that we have to keep the specific session for all sessions within the same time period.</span></span>

<span data-ttu-id="59430-176">Per risolvere questo problema, viene usata una variabile globale all'interno di una sezione code-behind: `static public string globalSession;`.</span><span class="sxs-lookup"><span data-stu-id="59430-176">To solve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span></span>

<span data-ttu-id="59430-177">Questa variabile globale viene applicata all'intero set di righe durante l'esecuzione dello script.</span><span class="sxs-lookup"><span data-stu-id="59430-177">This global variable is applied to the entire rowset during our script execution.</span></span>

<span data-ttu-id="59430-178">Di seguito è riportata la sezione code-behind del programma U-SQL:</span><span class="sxs-lookup"><span data-stu-id="59430-178">Here is the code-behind section of our U-SQL program:</span></span>

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

<span data-ttu-id="59430-179">Questo esempio illustra la variabile globale `static public string globalSession;` usata nella funzione `getStampUserSession` e reinizializzata a ogni modifica del parametro di sessione.</span><span class="sxs-lookup"><span data-stu-id="59430-179">This example shows the global variable `static public string globalSession;` used inside the `getStampUserSession` function and getting reinitialized each time the Session parameter is changed.</span></span>

<span data-ttu-id="59430-180">Lo script U-SQL di base è il seguente:</span><span class="sxs-lookup"><span data-stu-id="59430-180">The U-SQL base script is as follows:</span></span>

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
    TO @out2
    ORDER BY UserName, EventDateTime ASC
    USING Outputters.Csv();
```

<span data-ttu-id="59430-181">La funzione `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` viene chiamata durante il secondo calcolo del set di righe della memoria.</span><span class="sxs-lookup"><span data-stu-id="59430-181">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during the second memory rowset calculation.</span></span> <span data-ttu-id="59430-182">Passa la colonna `UserSessionTimestamp` e restituisce il valore finché non viene modificato `UserSessionTimestamp`.</span><span class="sxs-lookup"><span data-stu-id="59430-182">It passes the `UserSessionTimestamp` column and returns the value until `UserSessionTimestamp` has changed.</span></span>

<span data-ttu-id="59430-183">Il file di output è il seguente:</span><span class="sxs-lookup"><span data-stu-id="59430-183">The output file is as follows:</span></span>

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

<span data-ttu-id="59430-184">Questo esempio illustra lo scenario di un caso d'uso più complesso in cui si usa una variabile globale in una sezione code-behind applicata all'intero set di righe della memoria.</span><span class="sxs-lookup"><span data-stu-id="59430-184">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied to the entire memory rowset.</span></span>

## <a name="use-user-defined-types-udt"></a><span data-ttu-id="59430-185">Usare tipi definiti dall'utente (UDT)</span><span class="sxs-lookup"><span data-stu-id="59430-185">Use user-defined types: UDT</span></span>
<span data-ttu-id="59430-186">I tipi definiti dall'utente (UDT) sono un'altra funzionalità di programmabilità di U-SQL.</span><span class="sxs-lookup"><span data-stu-id="59430-186">User-defined types, or UDT, is another programmability feature of U-SQL.</span></span> <span data-ttu-id="59430-187">L'UDT U-SQL funziona come un normale tipo definito dall'utente C#.</span><span class="sxs-lookup"><span data-stu-id="59430-187">U-SQL UDT acts like a regular C# user-defined type.</span></span> <span data-ttu-id="59430-188">C# è un linguaggio fortemente tipizzato che consente l'uso di tipi incorporati e personalizzati definiti dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59430-188">C# is a strongly typed language that allows the use of built-in and custom user-defined types.</span></span>

<span data-ttu-id="59430-189">U-SQL non può serializzare o deserializzare implicitamente tipi definiti dall'utente arbitrari quando il tipo definito dall'utente viene passato tra i vertici nei set di righe.</span><span class="sxs-lookup"><span data-stu-id="59430-189">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when the UDT is passed between vertices in rowsets.</span></span> <span data-ttu-id="59430-190">Di conseguenza, l'utente deve specificare un formattatore esplicito usando l'interfaccia IFormatter.</span><span class="sxs-lookup"><span data-stu-id="59430-190">This means that the user has to provide an explicit formatter by using the IFormatter interface.</span></span> <span data-ttu-id="59430-191">Questo fornisce a U-SQL i metodi di serializzazione e deserializzazione per il tipo definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59430-191">This provides U-SQL with the serialize and de-serialize methods for the UDT.</span></span>

> [!NOTE]
> <span data-ttu-id="59430-192">Gli outputter e gli estrattori predefiniti di U-SQL non possono attualmente serializzare o deserializzare i dati UDT da o verso i file anche con l'impostazione di IFormatter.</span><span class="sxs-lookup"><span data-stu-id="59430-192">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data to or from files even with the IFormatter set.</span></span> <span data-ttu-id="59430-193">Di conseguenza, quando si scrivono dati UDT in un file con l'istruzione OUTPUT o si leggono tali dati con un estrattore, è necessario passare i dati come stringa o matrice di byte.</span><span class="sxs-lookup"><span data-stu-id="59430-193">So when you're writing UDT data to a file with the OUTPUT statement, or reading it with an extractor, you have to pass it as a string or byte array.</span></span> <span data-ttu-id="59430-194">Si chiama quindi in modo esplicito il codice di serializzazione o deserializzazione, ossia il metodo ToString() del tipo definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59430-194">Then you call the serialization and deserialization code (that is, the UDT’s ToString() method) explicitly.</span></span> <span data-ttu-id="59430-195">Gli outputter e gli estrattori definiti dall'utente, invece, possono leggere e scrivere i tipi definiti dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59430-195">User-defined extractors and outputters, on the other hand, can read and write UDTs.</span></span>

<span data-ttu-id="59430-196">Se si prova a usare il tipo definito dall'utente in EXTRACTOR o OUTPUTTER, fuori dall'istruzione SELECT precedente, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="59430-196">If we try to use UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span></span>

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="59430-197">viene visualizzato l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="59430-197">We receive the following error:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINOUTPUTTER: Outputters.Text was used to output column myfield of type
MyNameSpace.Myfunction_Returning_UDT.

Description:

Outputters.Text only supports built-in types.

Resolution:

Implement a custom outputter that knows how to serialize this type, or call a serialization method on the type in
the preceding SELECT.   C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\
USQL-Programmability\Types.usql 52  1   USQL-Programmability
```

<span data-ttu-id="59430-198">Per usare il tipo definito dall'utente nell'outputter, è necessario serializzarlo in stringa con il metodo ToString() e creare un outputter personalizzato.</span><span class="sxs-lookup"><span data-stu-id="59430-198">To work with UDT in outputter, we either have to serialize it to string with the ToString() method or create a custom outputter.</span></span>

<span data-ttu-id="59430-199">Al momento non è possibile usare UDT in GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="59430-199">UDTs currently cannot be used in GROUP BY.</span></span> <span data-ttu-id="59430-200">Se si usa l'UDT in GROUP BY, viene generato l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="59430-200">If UDT is used in GROUP BY, the following error is thrown:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINCLAUSE: GROUP BY doesn't support type MyNameSpace.Myfunction_Returning_UDT
for column myfield

Description:

GROUP BY doesn't support UDT or Complex types.

Resolution:

Add a SELECT statement where you can project a scalar column that you want to use with GROUP BY.
C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\USQL-Programmability\Types.usql
62  5   USQL-Programmability
```

<span data-ttu-id="59430-201">Per definire un UDT, è necessario:</span><span class="sxs-lookup"><span data-stu-id="59430-201">To define a UDT, we have to:</span></span>

* <span data-ttu-id="59430-202">Aggiungere gli spazi dei nomi seguenti:</span><span class="sxs-lookup"><span data-stu-id="59430-202">Add the following namespaces:</span></span>

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* <span data-ttu-id="59430-203">Aggiungere `Microsoft.Analytics.Interfaces`, obbligatorio per le interfacce per i tipi definiti dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59430-203">Add `Microsoft.Analytics.Interfaces`, which is required for the UDT interfaces.</span></span> <span data-ttu-id="59430-204">Per definire l'interfaccia IFormatter potrebbe essere necessario anche `System.IO`.</span><span class="sxs-lookup"><span data-stu-id="59430-204">In addition, `System.IO` might be needed to define the IFormatter interface.</span></span>

* <span data-ttu-id="59430-205">Definire un tipo definito dall'utente con l'attributo SqlUserDefinedType.</span><span class="sxs-lookup"><span data-stu-id="59430-205">Define a used-defined type with SqlUserDefinedType attribute.</span></span>

<span data-ttu-id="59430-206">**SqlUserDefinedType** è usato per contrassegnare la definizione di un tipo in un assembly come tipo definito dall'utente (UDT) in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="59430-206">**SqlUserDefinedType** is used to mark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span></span> <span data-ttu-id="59430-207">Le proprietà dell'attributo corrispondono alle caratteristiche fisiche dell'UDT.</span><span class="sxs-lookup"><span data-stu-id="59430-207">The properties on the attribute reflect the physical characteristics of the UDT.</span></span> <span data-ttu-id="59430-208">Questa classe non può essere ereditata.</span><span class="sxs-lookup"><span data-stu-id="59430-208">This class cannot be inherited.</span></span>

<span data-ttu-id="59430-209">SqlUserDefinedType è un attributo obbligatorio per la definizione dell'UDT.</span><span class="sxs-lookup"><span data-stu-id="59430-209">SqlUserDefinedType is a required attribute for UDT definition.</span></span>

<span data-ttu-id="59430-210">Il costruttore della classe:</span><span class="sxs-lookup"><span data-stu-id="59430-210">The constructor of the class:</span></span>  

* <span data-ttu-id="59430-211">SqlUserDefinedTypeAttribute (formattatore di tipo)</span><span class="sxs-lookup"><span data-stu-id="59430-211">SqlUserDefinedTypeAttribute (type formatter)</span></span>

* <span data-ttu-id="59430-212">Formattatore di tipo: parametro obbligatorio per definire un formattatore UDT. Nello specifico, qui deve essere passato il tipo dell'interfaccia `IFormatter`.</span><span class="sxs-lookup"><span data-stu-id="59430-212">Type formatter: Required parameter to define an UDT formatter--specifically, the type of the `IFormatter` interface must be passed here.</span></span>

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* <span data-ttu-id="59430-213">Un tipo definito dall'utente richiede in genere anche la definizione dell'interfaccia IFormatter, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="59430-213">Typical UDT also requires definition of the IFormatter interface, as shown in the following example:</span></span>

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

<span data-ttu-id="59430-214">L'interfaccia `IFormatter` serializza e deserializza un oggetto grafico con il tipo radice \<typeparamref name="T">.</span><span class="sxs-lookup"><span data-stu-id="59430-214">The `IFormatter` interface serializes and de-serializes an object graph with the root type of \<typeparamref name="T">.</span></span>

<span data-ttu-id="59430-215">\<typeparam name="T"> il tipo radice per l'oggetto grafico da serializzare e deserializzare.</span><span class="sxs-lookup"><span data-stu-id="59430-215">\<typeparam name="T">The root type for the object graph to serialize and de-serialize.</span></span>

* <span data-ttu-id="59430-216">**Deserialize**: deserializza i dati nel flusso fornito e ricostruisce il grafico degli oggetti.</span><span class="sxs-lookup"><span data-stu-id="59430-216">**Deserialize**: De-serializes the data on the provided stream and reconstitutes the graph of objects.</span></span>

* <span data-ttu-id="59430-217">**Serialize**: serializza un oggetto o un grafico di oggetti con la radice specificata nel flusso fornito.</span><span class="sxs-lookup"><span data-stu-id="59430-217">**Serialize**: Serializes an object, or graph of objects, with the given root to the provided stream.</span></span>

<span data-ttu-id="59430-218">`MyType` instance: istanza del tipo.</span><span class="sxs-lookup"><span data-stu-id="59430-218">`MyType` instance: Instance of the type.</span></span>  
<span data-ttu-id="59430-219">`IColumnWriter` writer/`IColumnReader` reader: flusso di colonna sottostante.</span><span class="sxs-lookup"><span data-stu-id="59430-219">`IColumnWriter` writer / `IColumnReader` reader: The underlying column stream.</span></span>  
<span data-ttu-id="59430-220">`ISerializationContext` context: enumerazione che definisce un set di flag che specifica il contesto di origine o di destinazione per il flusso durante la serializzazione.</span><span class="sxs-lookup"><span data-stu-id="59430-220">`ISerializationContext` context: Enum that defines a set of flags that specifies the source or destination context for the stream during serialization.</span></span>

* <span data-ttu-id="59430-221">**Intermediate**: specifica che il contesto di origine o di destinazione non è un archivio permanente.</span><span class="sxs-lookup"><span data-stu-id="59430-221">**Intermediate**: Specifies that the source or destination context is not a persisted store.</span></span>

* <span data-ttu-id="59430-222">**Persistence**: specifica che il contesto di origine o di destinazione è un archivio permanente.</span><span class="sxs-lookup"><span data-stu-id="59430-222">**Persistence**: Specifies that the source or destination context is a persisted store.</span></span>

<span data-ttu-id="59430-223">Come un normale tipo C#, la definizione di un tipo definito dall'utente di U-SQL può includere override per operatori come +/==/!= e così via.</span><span class="sxs-lookup"><span data-stu-id="59430-223">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span></span> <span data-ttu-id="59430-224">Può anche includere metodi statici.</span><span class="sxs-lookup"><span data-stu-id="59430-224">It can also include static methods.</span></span> <span data-ttu-id="59430-225">Ad esempio, se si intende usare il tipo definito dall'utente come parametro per una funzione di aggregazione MIN U-SQL, è necessario definire l'override dell'operatore <.</span><span class="sxs-lookup"><span data-stu-id="59430-225">For example, if we are going to use this UDT as a parameter to a U-SQL MIN aggregate function, we have to define < operator override.</span></span>

<span data-ttu-id="59430-226">In precedenza in questa guida è stato illustrato un esempio di identificazione del periodo fiscale dalla data specifica nel formato Qn:Pn (Q1:P10).</span><span class="sxs-lookup"><span data-stu-id="59430-226">Earlier in this guide, we demonstrated an example for fiscal period identification from the specific date in the format Qn:Pn (Q1:P10).</span></span> <span data-ttu-id="59430-227">Nell'esempio seguente viene illustrato come definire un tipo personalizzato per i valori del periodo fiscale.</span><span class="sxs-lookup"><span data-stu-id="59430-227">The following example shows how to define a custom type for fiscal period values.</span></span>

<span data-ttu-id="59430-228">Di seguito è riportato un esempio di sezione code-behind con tipo definito dall'utente e interfaccia IFormatter personalizzati:</span><span class="sxs-lookup"><span data-stu-id="59430-228">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span></span>

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

<span data-ttu-id="59430-229">Il tipo definito include due numeri, corrispondenti a trimestre e mese.</span><span class="sxs-lookup"><span data-stu-id="59430-229">The defined type includes two numbers: quarter and month.</span></span> <span data-ttu-id="59430-230">Qui sono definiti gli operatori ==/!=/>/< e il metodo statico ToString ().</span><span class="sxs-lookup"><span data-stu-id="59430-230">Operators ==/!=/>/< and static method ToString() are defined here.</span></span>

<span data-ttu-id="59430-231">Come indicato in precedenza, il tipo definito dall'utente può essere usato nelle espressioni SELECT, ma non in OUTPUTTER/EXTRACTOR senza serializzazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="59430-231">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span></span> <span data-ttu-id="59430-232">Deve essere serializzato come stringa con ToString () oppure essere usato con un elemento OUTPUTTER/EXTRACTOR personalizzato.</span><span class="sxs-lookup"><span data-stu-id="59430-232">It either has to be serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span></span>

<span data-ttu-id="59430-233">Ora esaminiamo l'uso dell'UDT.</span><span class="sxs-lookup"><span data-stu-id="59430-233">Now let’s discuss usage of UDT.</span></span> <span data-ttu-id="59430-234">In una sezione code-behind, la funzione GetFiscalPeriod è stata modificata come segue:</span><span class="sxs-lookup"><span data-stu-id="59430-234">In a code-behind section, we changed our GetFiscalPeriod function to the following:</span></span>

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

<span data-ttu-id="59430-235">Come si può notare, restituisce il valore del tipo FiscalPeriod.</span><span class="sxs-lookup"><span data-stu-id="59430-235">As you can see, it returns the value of our FiscalPeriod type.</span></span>

<span data-ttu-id="59430-236">Di seguito è riportato un esempio dell'ulteriore uso nello script U-SQL di base.</span><span class="sxs-lookup"><span data-stu-id="59430-236">Here we provide an example of how to use it further in U-SQL base script.</span></span> <span data-ttu-id="59430-237">Questo esempio illustra diverse forme di chiamata del tipo definito dall'utente dallo script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="59430-237">This example demonstrates different forms of UDT invocation from U-SQL script.</span></span>

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

       // This user-defined type was created in the prior SELECT.  Passing the UDT to this subsequent SELECT would have failed if the UDT was not annotated with an IFormatter.
           fiscalperiod_adjusted.ToString() AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="59430-238">Ecco un esempio di una sezione code-behind completa:</span><span class="sxs-lookup"><span data-stu-id="59430-238">Here's an example of a full code-behind section:</span></span>

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

## <a name="use-user-defined-aggregates-udagg"></a><span data-ttu-id="59430-239">Usare aggregazioni definite dall'utente (UDAGG)</span><span class="sxs-lookup"><span data-stu-id="59430-239">Use user-defined aggregates: UDAGG</span></span>
<span data-ttu-id="59430-240">Le aggregazioni definite dall'utente sono funzioni correlate all'aggregazione che non sono già incluse in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="59430-240">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span></span> <span data-ttu-id="59430-241">Può trattarsi ad esempio di una funzione di aggregazione per eseguire calcoli matematici personalizzati, concatenazioni di stringa o modifiche con stringhe e così via.</span><span class="sxs-lookup"><span data-stu-id="59430-241">The example can be an aggregate to perform custom math calculations, string concatenations, manipulations with strings, and so on.</span></span>

<span data-ttu-id="59430-242">La definizione della classe base delle aggregazioni definite dall'utente è la seguente:</span><span class="sxs-lookup"><span data-stu-id="59430-242">The user-defined aggregate base class definition is as follows:</span></span>

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

<span data-ttu-id="59430-243">**SqlUserDefinedAggregate** indica che il tipo deve essere registrato come aggregazione definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59430-243">**SqlUserDefinedAggregate** indicates that the type should be registered as a user-defined aggregate.</span></span> <span data-ttu-id="59430-244">Questa classe non può essere ereditata.</span><span class="sxs-lookup"><span data-stu-id="59430-244">This class cannot be inherited.</span></span>

<span data-ttu-id="59430-245">L'attributo SqlUserDefinedType è **facoltativo** per la definizione di aggregazioni definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59430-245">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span></span>


<span data-ttu-id="59430-246">La classe base consente di passare tre parametri astratti: due come parametri di input e uno come risultato.</span><span class="sxs-lookup"><span data-stu-id="59430-246">The base class allows you to pass three abstract parameters: two as input parameters and one as the result.</span></span> <span data-ttu-id="59430-247">I tipi di dati sono variabili e devono essere definiti quando viene ereditata la classe.</span><span class="sxs-lookup"><span data-stu-id="59430-247">The data types are variable and should be defined during class inheritance.</span></span>

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

* <span data-ttu-id="59430-248">**Init** esegue la chiamata una volta per ogni gruppo durante il calcolo.</span><span class="sxs-lookup"><span data-stu-id="59430-248">**Init** invokes once for each group during computation.</span></span> <span data-ttu-id="59430-249">Fornisce la routine di inizializzazione per ogni gruppo di aggregazione.</span><span class="sxs-lookup"><span data-stu-id="59430-249">It provides an initialization routine for each aggregation group.</span></span>  
* <span data-ttu-id="59430-250">**Accumulate** viene eseguito una volta per ogni valore.</span><span class="sxs-lookup"><span data-stu-id="59430-250">**Accumulate** is executed once for each value.</span></span> <span data-ttu-id="59430-251">Fornisce la funzionalità principale per l'algoritmo di aggregazione.</span><span class="sxs-lookup"><span data-stu-id="59430-251">It provides the main functionality for the aggregation algorithm.</span></span> <span data-ttu-id="59430-252">Consente di aggregare valori con vari tipi di dati che vengono definiti quando viene ereditata la classe.</span><span class="sxs-lookup"><span data-stu-id="59430-252">It can be used to aggregate values with various data types that are defined during class inheritance.</span></span> <span data-ttu-id="59430-253">Può accettare due parametri di tipi di dati della variabile.</span><span class="sxs-lookup"><span data-stu-id="59430-253">It can accept two parameters of variable data types.</span></span>
* <span data-ttu-id="59430-254">**Terminate** viene eseguito una volta per ogni gruppo di aggregazione al termine dell'elaborazione per restituire il risultato per ogni gruppo.</span><span class="sxs-lookup"><span data-stu-id="59430-254">**Terminate** is executed once per aggregation group at the end of processing to output the result for each group.</span></span>

<span data-ttu-id="59430-255">Per dichiarare tipi di dati di input e output corretti, usare la definizione di classe come segue:</span><span class="sxs-lookup"><span data-stu-id="59430-255">To declare correct input and output data types, use the class definition as follows:</span></span>

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* <span data-ttu-id="59430-256">T1: primo parametro per Accumulate</span><span class="sxs-lookup"><span data-stu-id="59430-256">T1: First parameter to accumulate</span></span>
* <span data-ttu-id="59430-257">T2: primo parametro per Accumulate</span><span class="sxs-lookup"><span data-stu-id="59430-257">T2: First parameter to accumulate</span></span>
* <span data-ttu-id="59430-258">TResult: tipo restituito di Terminate</span><span class="sxs-lookup"><span data-stu-id="59430-258">TResult: Return type of terminate</span></span>

<span data-ttu-id="59430-259">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="59430-259">For example:</span></span>

```
public class GuidAggregate : IAggregate<string, int, int>
```

<span data-ttu-id="59430-260">oppure</span><span class="sxs-lookup"><span data-stu-id="59430-260">or</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a><span data-ttu-id="59430-261">Usare aggregazioni definite dall'utente in U-SQL</span><span class="sxs-lookup"><span data-stu-id="59430-261">Use UDAGG in U-SQL</span></span>
<span data-ttu-id="59430-262">Per usare un'aggregazione definita dall'utente, per prima cosa è necessario definirla nel code-behind oppure farvi riferimento dalla DLL di programmabilità esistente, come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="59430-262">To use UDAGG, first define it in code-behind or reference it from the existent programmability DLL as discussed earlier.</span></span>

<span data-ttu-id="59430-263">Usare quindi la sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="59430-263">Then use the following syntax:</span></span>

```
AGG<UDAGG_functionname>(param1,param2)
```

<span data-ttu-id="59430-264">Di seguito è riportato un esempio di aggregazione definita dall'utente:</span><span class="sxs-lookup"><span data-stu-id="59430-264">Here is an example of UDAGG:</span></span>

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

<span data-ttu-id="59430-265">Ecco lo script U-SQL di base:</span><span class="sxs-lookup"><span data-stu-id="59430-265">And base U-SQL script:</span></span>

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

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="59430-266">Nello scenario di questo caso d'uso, vengono concatenati GUID di classe per gli utenti specifici.</span><span class="sxs-lookup"><span data-stu-id="59430-266">In this use-case scenario, we concatenate class GUIDs for the specific users.</span></span>

## <a name="use-user-defined-objects-udo"></a><span data-ttu-id="59430-267">Usare oggetti definiti dall'utente (UDO)</span><span class="sxs-lookup"><span data-stu-id="59430-267">Use user-defined objects: UDO</span></span>
<span data-ttu-id="59430-268">U-SQL consente di definire oggetti di programmabilità personalizzati, denominati oggetti definiti dall'utente (UDO).</span><span class="sxs-lookup"><span data-stu-id="59430-268">U-SQL enables you to define custom programmability objects, which are called user-defined objects or UDO.</span></span>

<span data-ttu-id="59430-269">Di seguito è riportato un elenco degli oggetti definiti dall'utente in U-SQL:</span><span class="sxs-lookup"><span data-stu-id="59430-269">The following is a list of UDO in U-SQL:</span></span>

* <span data-ttu-id="59430-270">Estrattori definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="59430-270">User-defined extractors</span></span>
    * <span data-ttu-id="59430-271">Estrazione riga per riga</span><span class="sxs-lookup"><span data-stu-id="59430-271">Extract row by row</span></span>
    * <span data-ttu-id="59430-272">Vengono usati per implementare l'estrazione di dati da file strutturati personalizzati</span><span class="sxs-lookup"><span data-stu-id="59430-272">Used to implement data extraction from custom structured files</span></span>

* <span data-ttu-id="59430-273">Outputter definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="59430-273">User-defined outputters</span></span>
    * <span data-ttu-id="59430-274">Output riga per riga</span><span class="sxs-lookup"><span data-stu-id="59430-274">Output row by row</span></span>
    * <span data-ttu-id="59430-275">Vengono usati per tipi di dati di output o formati di file personalizzati</span><span class="sxs-lookup"><span data-stu-id="59430-275">Used to output custom data types or custom file formats</span></span>

* <span data-ttu-id="59430-276">Elaboratori definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="59430-276">User-defined processors</span></span>
    * <span data-ttu-id="59430-277">Viene usato per richiedere una riga e produrre una riga</span><span class="sxs-lookup"><span data-stu-id="59430-277">Take one row and produce one row</span></span>
    * <span data-ttu-id="59430-278">Vengono usati per ridurre il numero di colonne o produrre nuove colonne con valori derivati da un set di colonne esistente</span><span class="sxs-lookup"><span data-stu-id="59430-278">Used to reduce the number of columns or produce new columns with values that are derived from an existing column set</span></span>

* <span data-ttu-id="59430-279">Oggetti di applicazione definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="59430-279">User-defined appliers</span></span>
    * <span data-ttu-id="59430-280">Serve a richiedere una riga e produrre da 0 a n righe</span><span class="sxs-lookup"><span data-stu-id="59430-280">Take one row and produce 0 to n rows</span></span>
    * <span data-ttu-id="59430-281">Viene usato con OUTER/CROSS APPLY</span><span class="sxs-lookup"><span data-stu-id="59430-281">Used with OUTER/CROSS APPLY</span></span>

* <span data-ttu-id="59430-282">Combinatori definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="59430-282">User-defined combiners</span></span>
    * <span data-ttu-id="59430-283">Combinano set di righe (JOIN definiti dall'utente)</span><span class="sxs-lookup"><span data-stu-id="59430-283">Combines rowsets--user-defined JOINs</span></span>

* <span data-ttu-id="59430-284">Riduttori definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="59430-284">User-defined reducers</span></span>
    * <span data-ttu-id="59430-285">Serve a richiedere n righe e produrre una riga</span><span class="sxs-lookup"><span data-stu-id="59430-285">Take n rows and produce one row</span></span>
    * <span data-ttu-id="59430-286">Vengono usati per ridurre il numero di righe</span><span class="sxs-lookup"><span data-stu-id="59430-286">Used to reduce the number of rows</span></span>

<span data-ttu-id="59430-287">Un oggetto definito dall'utente viene in genere chiamato in modo esplicito negli script U-SQL come parte delle istruzioni U-SQL seguenti:</span><span class="sxs-lookup"><span data-stu-id="59430-287">UDO is typically called explicitly in U-SQL script as part of the following U-SQL statements:</span></span>

* <span data-ttu-id="59430-288">EXTRACT</span><span class="sxs-lookup"><span data-stu-id="59430-288">EXTRACT</span></span>
* <span data-ttu-id="59430-289">OUTPUT</span><span class="sxs-lookup"><span data-stu-id="59430-289">OUTPUT</span></span>
* <span data-ttu-id="59430-290">PROCESS</span><span class="sxs-lookup"><span data-stu-id="59430-290">PROCESS</span></span>
* <span data-ttu-id="59430-291">COMBINE</span><span class="sxs-lookup"><span data-stu-id="59430-291">COMBINE</span></span>
* <span data-ttu-id="59430-292">REDUCE</span><span class="sxs-lookup"><span data-stu-id="59430-292">REDUCE</span></span>

> [!NOTE]  
> <span data-ttu-id="59430-293">Gli oggetti definiti dall'utente sono limitati per occupare 0,5 GB di memoria.</span><span class="sxs-lookup"><span data-stu-id="59430-293">UDO’s are limited to consume 0.5Gb memory.</span></span>  <span data-ttu-id="59430-294">Questa limitazione di memoria non è applicabile alle esecuzioni locali.</span><span class="sxs-lookup"><span data-stu-id="59430-294">This memory limitation does not apply to local executions.</span></span>

## <a name="use-user-defined-extractors"></a><span data-ttu-id="59430-295">Usare estrattori definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="59430-295">Use user-defined extractors</span></span>
<span data-ttu-id="59430-296">U-SQL consente di importare dati esterni con un'istruzione EXTRACT.</span><span class="sxs-lookup"><span data-stu-id="59430-296">U-SQL allows you to import external data by using an EXTRACT statement.</span></span> <span data-ttu-id="59430-297">L'istruzione EXTRACT consente di usare estrattori UDO predefiniti.</span><span class="sxs-lookup"><span data-stu-id="59430-297">An EXTRACT statement can use built-in UDO extractors:</span></span>  

* <span data-ttu-id="59430-298">*Extractors.Text()*: consente di estrarre da file di testo delimitati di varie codifiche.</span><span class="sxs-lookup"><span data-stu-id="59430-298">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span></span>

* <span data-ttu-id="59430-299">*Extractors.Csv()*: consente di estrarre da file di testo delimitati da virgole (CSV) di varie codifiche.</span><span class="sxs-lookup"><span data-stu-id="59430-299">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span></span>

* <span data-ttu-id="59430-300">*Extractors.Tsv()*: consente di estrarre da file di testo delimitati da tabulazioni (TSV) di varie codifiche.</span><span class="sxs-lookup"><span data-stu-id="59430-300">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="59430-301">Può essere utile per sviluppare un estrattore personalizzato.</span><span class="sxs-lookup"><span data-stu-id="59430-301">It can be useful to develop a custom extractor.</span></span> <span data-ttu-id="59430-302">Questo può essere opportuno durante un'importazione di dati, se si vuole eseguire una o più delle attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="59430-302">This can be helpful during data import if we want to do any of the following tasks:</span></span>

* <span data-ttu-id="59430-303">Modificare i dati di input suddividendo le colonne e modificando singoli valori.</span><span class="sxs-lookup"><span data-stu-id="59430-303">Modify input data by splitting columns and modifying individual values.</span></span> <span data-ttu-id="59430-304">Per la combinazione di colonne è preferibile la funzionalità PROCESSOR.</span><span class="sxs-lookup"><span data-stu-id="59430-304">The PROCESSOR functionality is better for combining columns.</span></span>
* <span data-ttu-id="59430-305">Analizzare dati non strutturati, come pagine Web e messaggi di posta elettronica, o dati parzialmente non strutturati, ad esempio XML/JSON.</span><span class="sxs-lookup"><span data-stu-id="59430-305">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span></span>
* <span data-ttu-id="59430-306">Analizzare dati in una codifica non supportata.</span><span class="sxs-lookup"><span data-stu-id="59430-306">Parse data in unsupported encoding.</span></span>

<span data-ttu-id="59430-307">Per definire un estrattore definito dall'utente (UDE), è necessario creare un'interfaccia `IExtractor`.</span><span class="sxs-lookup"><span data-stu-id="59430-307">To define a user-defined extractor, or UDE, we need to create an `IExtractor` interface.</span></span> <span data-ttu-id="59430-308">Tutti i parametri di input per l'estrattore, come i delimitatori di riga/colonna e la codifica, devono essere definiti nel costruttore della classe.</span><span class="sxs-lookup"><span data-stu-id="59430-308">All input parameters to the extractor, such as column/row delimiters, and encoding, need to be defined in the constructor of the class.</span></span> <span data-ttu-id="59430-309">L'interfaccia `IExtractor` deve contenere anche una definizione per l'override `IEnumerable<IRow>`, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="59430-309">The `IExtractor`  interface should also contain a definition for the `IEnumerable<IRow>` override as follows:</span></span>

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

<span data-ttu-id="59430-310">L'attributo **SqlUserDefinedExtractor** indica che il tipo deve essere registrato come estrattore definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59430-310">The **SqlUserDefinedExtractor** attribute indicates that the type should be registered as a user-defined extractor.</span></span> <span data-ttu-id="59430-311">Questa classe non può essere ereditata.</span><span class="sxs-lookup"><span data-stu-id="59430-311">This class cannot be inherited.</span></span>

<span data-ttu-id="59430-312">SqlUserDefinedExtractor è un attributo facoltativo per la definizione di UDE,</span><span class="sxs-lookup"><span data-stu-id="59430-312">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span></span> <span data-ttu-id="59430-313">che consente di definire la proprietà AtomicFileProcessing dell'oggetto UDE.</span><span class="sxs-lookup"><span data-stu-id="59430-313">It used to define AtomicFileProcessing property for the UDE object.</span></span>

* <span data-ttu-id="59430-314">bool     AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="59430-314">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="59430-315">**true** indica che l'estrattore richiede file di input atomici (JSON, XML e così via)</span><span class="sxs-lookup"><span data-stu-id="59430-315">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span></span>
* <span data-ttu-id="59430-316">**false** indica che l'estrattore può gestire file suddivisi/distribuiti (CSV, SEQ e così via)</span><span class="sxs-lookup"><span data-stu-id="59430-316">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="59430-317">I principali oggetti di programmabilità UDE sono **input** e **output**.</span><span class="sxs-lookup"><span data-stu-id="59430-317">The main UDE programmability objects are **input** and **output**.</span></span> <span data-ttu-id="59430-318">L'oggetto di input viene usato per enumerare i dati di input come `IUnstructuredReader`.</span><span class="sxs-lookup"><span data-stu-id="59430-318">The input object is used to enumerate input data as `IUnstructuredReader`.</span></span> <span data-ttu-id="59430-319">L'oggetto di output viene usato per impostare i dati di output come risultato dell'attività di estrazione.</span><span class="sxs-lookup"><span data-stu-id="59430-319">The output object is used to set output data as a result of the extractor activity.</span></span>

<span data-ttu-id="59430-320">I dati di input sono accessibili tramite `System.IO.Stream` e `System.IO.StreamReader`.</span><span class="sxs-lookup"><span data-stu-id="59430-320">The input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span></span>

<span data-ttu-id="59430-321">Per l'enumerazione delle colonne di input, per prima cosa si suddivide il flusso di input con un delimitatore di riga.</span><span class="sxs-lookup"><span data-stu-id="59430-321">For input columns enumeration, we first split the input stream by using a row delimiter.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

<span data-ttu-id="59430-322">Quindi, la riga di input viene ulteriormente suddivisa nelle parti di una colonna.</span><span class="sxs-lookup"><span data-stu-id="59430-322">Then, further split input row into column parts.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

<span data-ttu-id="59430-323">Per impostare i dati di output, si usa il metodo `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="59430-323">To set output data, we use the `output.Set` method.</span></span>

<span data-ttu-id="59430-324">È importante comprendere che l'estrattore personalizzato restituisce solo le colonne e i valori definiti con l'output.</span><span class="sxs-lookup"><span data-stu-id="59430-324">It's important to understand that the custom extractor only outputs columns and values that are defined with the output.</span></span> <span data-ttu-id="59430-325">il metodo di chiamata output.Set.</span><span class="sxs-lookup"><span data-stu-id="59430-325">Set method call.</span></span>

```
output.Set<string>(count, part);
```

<span data-ttu-id="59430-326">L'output effettivo dell'estrattore viene attivato chiamando `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="59430-326">The actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="59430-327">Di seguito è riportato l'esempio di estrattore:</span><span class="sxs-lookup"><span data-stu-id="59430-327">Following is the extractor example:</span></span>

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
         //Read the input line by line
         foreach (Stream current in input.Split(_encoding.GetBytes("\r\n")))
         {
        using (System.IO.StreamReader streamReader = new StreamReader(current, this._encoding))
         {
             line = streamReader.ReadToEnd().Trim();
             //Split the input by the column delimiter
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
                 // for column “user”, convert to UPPER case
                 output.Set<string>(count, part.ToUpper());

             }
             else
             {
                 // keep the rest of the columns as-is
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

<span data-ttu-id="59430-328">Nello scenario di questo caso d'uso, l'estrattore rigenera il GUID per la colonna "guid" e converte i valori della colonna "user" in lettere maiuscole.</span><span class="sxs-lookup"><span data-stu-id="59430-328">In this use-case scenario, the extractor regenerates the GUID for “guid” column and converts the values of “user” column to upper case.</span></span> <span data-ttu-id="59430-329">Gli estrattori personalizzati possono produrre risultati più complessi analizzando e modificando i dati di input.</span><span class="sxs-lookup"><span data-stu-id="59430-329">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span></span>

<span data-ttu-id="59430-330">Di seguito è riportato uno script U-SQL di base che usa un estrattore personalizzato:</span><span class="sxs-lookup"><span data-stu-id="59430-330">Following is base U-SQL script that uses a custom extractor:</span></span>

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

OUTPUT @rs0 TO @output_file USING Outputters.Text();
```

## <a name="use-user-defined-outputters"></a><span data-ttu-id="59430-331">Usare outputter definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="59430-331">Use user-defined outputters</span></span>
<span data-ttu-id="59430-332">L'outputter definito dall'utente è un altro oggetto definito dall'utente di U-SQL che consente di estendere una funzionalità predefinita di U-SQL.</span><span class="sxs-lookup"><span data-stu-id="59430-332">User-defined outputter is another U-SQL UDO that allows you to extend built-in U-SQL functionality.</span></span> <span data-ttu-id="59430-333">Come per l'estrattore, esistono diversi outputter integrati.</span><span class="sxs-lookup"><span data-stu-id="59430-333">Similar to the extractor, there are several built-in outputters.</span></span>

* <span data-ttu-id="59430-334">*Outputters.Text()*: scrive i dati in file di testo delimitati di codifiche diverse.</span><span class="sxs-lookup"><span data-stu-id="59430-334">*Outputters.Text()*: Writes data to delimited text files of different encodings.</span></span>
* <span data-ttu-id="59430-335">*Outputters.Csv()*: scrive i dati in file di testo delimitati da virgole (CSV) di codifiche diverse.</span><span class="sxs-lookup"><span data-stu-id="59430-335">*Outputters.Csv()*: Writes data to comma-separated value (CSV) files of different encodings.</span></span>
* <span data-ttu-id="59430-336">*Outputters.Tsv()*: scrive i dati in file di testo delimitati da tabulazioni (TSV) di codifiche diverse.</span><span class="sxs-lookup"><span data-stu-id="59430-336">*Outputters.Tsv()*: Writes data to tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="59430-337">L'outputter personalizzato consente di scrivere i dati in un formato definito personalizzato.</span><span class="sxs-lookup"><span data-stu-id="59430-337">Custom outputter allows you to write data in a custom defined format.</span></span> <span data-ttu-id="59430-338">Questo può essere utile per le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="59430-338">This can be useful for the following tasks:</span></span>

* <span data-ttu-id="59430-339">Scrittura di i dati in file non strutturati o semistrutturati</span><span class="sxs-lookup"><span data-stu-id="59430-339">Writing data to semi-structured or unstructured files.</span></span>
* <span data-ttu-id="59430-340">Scrittura di dati in codifiche non supportate</span><span class="sxs-lookup"><span data-stu-id="59430-340">Writing data not supported encodings.</span></span>
* <span data-ttu-id="59430-341">Modifica dei dati di output o aggiunta di attributi personalizzati</span><span class="sxs-lookup"><span data-stu-id="59430-341">Modifying output data or adding custom attributes.</span></span>

<span data-ttu-id="59430-342">Per definire outputter definiti dall'utente, è necessario creare l'interfaccia `IOutputter`.</span><span class="sxs-lookup"><span data-stu-id="59430-342">To define user-defined outputter, we need to create the `IOutputter` interface.</span></span>

<span data-ttu-id="59430-343">Di seguito è riportata l'implementazione della classe `IOutputter` di base:</span><span class="sxs-lookup"><span data-stu-id="59430-343">Following is the base `IOutputter` class implementation:</span></span>

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

<span data-ttu-id="59430-344">Tutti i parametri di input per l'outputter, come i delimitatori di riga/colonna, la codifica e così via, devono essere definiti nel costruttore della classe.</span><span class="sxs-lookup"><span data-stu-id="59430-344">All input parameters to the outputter, such as column/row delimiters, encoding, and so on, need to be defined in the constructor of the class.</span></span> <span data-ttu-id="59430-345">L'interfaccia `IOutputter` deve contenere anche una definizione per l'override `void Output`.</span><span class="sxs-lookup"><span data-stu-id="59430-345">The `IOutputter` interface should also contain a definition for `void Output` override.</span></span> <span data-ttu-id="59430-346">L'attributo `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` può essere facoltativamente impostato per l'elaborazione di file atomici.</span><span class="sxs-lookup"><span data-stu-id="59430-346">The attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span></span> <span data-ttu-id="59430-347">Per altre informazioni, vedere i dettagli riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="59430-347">For more information, see the following details.</span></span>

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

* <span data-ttu-id="59430-348">`Output` viene chiamato per ogni riga di input.</span><span class="sxs-lookup"><span data-stu-id="59430-348">`Output` is called for each input row.</span></span> <span data-ttu-id="59430-349">Restituisce il set di righe `IUnstructuredWriter output`.</span><span class="sxs-lookup"><span data-stu-id="59430-349">It returns the `IUnstructuredWriter output` rowset.</span></span>
* <span data-ttu-id="59430-350">La classe del costruttore viene usata per passare parametri all'outputter definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59430-350">The Constructor class is used to pass parameters to the user-defined outputter.</span></span>
* <span data-ttu-id="59430-351">`Close` viene usato per eseguire facoltativamente l'override per rilasciare uno stato dispendioso o determinare quando è stata scritta l'ultima riga.</span><span class="sxs-lookup"><span data-stu-id="59430-351">`Close` is used to optionally override to release expensive state or determine when the last row was written.</span></span>

<span data-ttu-id="59430-352">L'attributo **SqlUserDefinedOutputter** indica che il tipo deve essere registrato come outputter definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59430-352">**SqlUserDefinedOutputter** attribute indicates that the type should be registered as a user-defined outputter.</span></span> <span data-ttu-id="59430-353">Questa classe non può essere ereditata.</span><span class="sxs-lookup"><span data-stu-id="59430-353">This class cannot be inherited.</span></span>

<span data-ttu-id="59430-354">SqlUserDefinedOutputter è un attributo facoltativo per la definizione di un outputter definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59430-354">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span></span> <span data-ttu-id="59430-355">Viene usato per definire la proprietà AtomicFileProcessing.</span><span class="sxs-lookup"><span data-stu-id="59430-355">It's used to define the AtomicFileProcessing property.</span></span>

* <span data-ttu-id="59430-356">bool     AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="59430-356">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="59430-357">**true** indica che l'outputter richiede file di output atomici (JSON, XML e così via)</span><span class="sxs-lookup"><span data-stu-id="59430-357">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span></span>
* <span data-ttu-id="59430-358">**false** indica che l'outputter può gestire file suddivisi/distribuiti (CSV, SEQ e così via)</span><span class="sxs-lookup"><span data-stu-id="59430-358">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="59430-359">I principali oggetti di programmabilità sono **row** e **output**.</span><span class="sxs-lookup"><span data-stu-id="59430-359">The main programmability objects are **row** and **output**.</span></span> <span data-ttu-id="59430-360">L'oggetto **row** viene usato per enumerare i dati di output come interfaccia `IRow`.</span><span class="sxs-lookup"><span data-stu-id="59430-360">The **row** object is used to enumerate output data as `IRow` interface.</span></span> <span data-ttu-id="59430-361">**Output** viene usato per impostare i dati di output sul file di destinazione.</span><span class="sxs-lookup"><span data-stu-id="59430-361">**Output** is used to set output data to the target file.</span></span>

<span data-ttu-id="59430-362">I dati di output sono accessibili tramite l'interfaccia `IRow`.</span><span class="sxs-lookup"><span data-stu-id="59430-362">The output data is accessed through the `IRow` interface.</span></span> <span data-ttu-id="59430-363">I dati di output vengono trasmessi una riga alla volta.</span><span class="sxs-lookup"><span data-stu-id="59430-363">Output data is passed a row at a time.</span></span>

<span data-ttu-id="59430-364">I singoli valori vengono enumerati chiamando il metodo Get dell'interfaccia IRow:</span><span class="sxs-lookup"><span data-stu-id="59430-364">The individual values are enumerated by calling the Get method of the IRow interface:</span></span>

```
row.Get<string>("column_name")
```

<span data-ttu-id="59430-365">I nomi delle singole colonne possono essere determinati chiamando `row.Schema`:</span><span class="sxs-lookup"><span data-stu-id="59430-365">Individual column names can be determined by calling `row.Schema`:</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="59430-366">Questo approccio consente di compilare un outputter flessibile per qualsiasi schema di metadati.</span><span class="sxs-lookup"><span data-stu-id="59430-366">This approach enables you to build a flexible outputter for any metadata schema.</span></span>

<span data-ttu-id="59430-367">I dati di output vengono scritti in un file usando `System.IO.StreamWriter`.</span><span class="sxs-lookup"><span data-stu-id="59430-367">The output data is written to file by using `System.IO.StreamWriter`.</span></span> <span data-ttu-id="59430-368">Il parametro di flusso viene impostato su `output.BaseStrea` come parte di `IUnstructuredWriter output`.</span><span class="sxs-lookup"><span data-stu-id="59430-368">The stream parameter is set to `output.BaseStrea` as part of `IUnstructuredWriter output`.</span></span>

<span data-ttu-id="59430-369">Si noti che è importante scaricare il buffer dei dati nel file dopo ogni iterazione di riga.</span><span class="sxs-lookup"><span data-stu-id="59430-369">Note that it's important to flush the data buffer to the file after each row iteration.</span></span> <span data-ttu-id="59430-370">L'oggetto `StreamWriter`, inoltre, deve essere usato con l'attributo Disposable abilitato (impostazione predefinita) e con la parola chiave **using**:</span><span class="sxs-lookup"><span data-stu-id="59430-370">In addition, the `StreamWriter` object must be used with the Disposable attribute enabled (default) and with the **using** keyword:</span></span>

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

<span data-ttu-id="59430-371">In alternativa, chiamare il metodo Flush() in modo esplicito dopo ogni iterazione,</span><span class="sxs-lookup"><span data-stu-id="59430-371">Otherwise, call Flush() method explicitly after each iteration.</span></span> <span data-ttu-id="59430-372">come illustrato nell'esempio riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="59430-372">We show this in the following example.</span></span>

### <a name="set-headers-and-footers-for-user-defined-outputter"></a><span data-ttu-id="59430-373">Impostare intestazioni e piè di pagina per l'outputter definito dall'utente</span><span class="sxs-lookup"><span data-stu-id="59430-373">Set headers and footers for user-defined outputter</span></span>
<span data-ttu-id="59430-374">Per impostare un'intestazione, usare il flusso di esecuzione dell'iterazione singola.</span><span class="sxs-lookup"><span data-stu-id="59430-374">To set a header, use single iteration execution flow.</span></span>

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

<span data-ttu-id="59430-375">Il codice nel primo blocco `if (isHeaderRow)` viene eseguito una sola volta.</span><span class="sxs-lookup"><span data-stu-id="59430-375">The code in the first `if (isHeaderRow)` block is executed only once.</span></span>

<span data-ttu-id="59430-376">Per il piè di pagina, usare il riferimento all'istanza dell'oggetto `System.IO.Stream` (`output.BaseStream`).</span><span class="sxs-lookup"><span data-stu-id="59430-376">For the footer, use the reference to the instance of `System.IO.Stream` object (`output.BaseStream`).</span></span> <span data-ttu-id="59430-377">Scrivere il piè di pagina nel metodo Close() dell'interfaccia `IOutputter`.</span><span class="sxs-lookup"><span data-stu-id="59430-377">Write the footer in the Close() method of the `IOutputter` interface.</span></span>  <span data-ttu-id="59430-378">Per altre informazioni, vedere l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="59430-378">(For more information, see the following example.)</span></span>

<span data-ttu-id="59430-379">Di seguito è riportato un esempio di outputter definito dall'utente:</span><span class="sxs-lookup"><span data-stu-id="59430-379">Following is an example of a user-defined outputter:</span></span>

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

    // The Close method is used to write the footer to the file. It's executed only once, after all rows
    public override void Close().
    {
    //Reference to IO.Stream object - g_writer
    StreamWriter streamWriter = new StreamWriter(g_writer, this.encoding);
    streamWriter.Write("</table>");
    streamWriter.Flush();
    streamWriter.Close();
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
    System.IO.StreamWriter streamWriter = new StreamWriter(output.BaseStream, this.encoding);

    // Metadata schema initialization to enumerate column names
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
        // Data type enumeration--required to match the distinct list of types from OUTPUT statement
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
    // Reference to the instance of the IO.Stream object for footer generation
    g_writer = output.BaseStream;
    streamWriter.Flush();
    }
}

// Define the factory classes
public static class Factory
{
    public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    return new HTMLOutputter(isHeader, encoding);
    }
}
```

<span data-ttu-id="59430-380">Ecco lo script U-SQL di base:</span><span class="sxs-lookup"><span data-stu-id="59430-380">And U-SQL base script:</span></span>

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
    TO @output_file 
    USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="59430-381">Questo è un outputter HTML che crea un file HTML con dati di tabella.</span><span class="sxs-lookup"><span data-stu-id="59430-381">This is an HTML outputter, which creates an HTML file with table data.</span></span>

### <a name="call-outputter-from-u-sql-base-script"></a><span data-ttu-id="59430-382">Chiamare l'outputter dallo script U-SQL di base</span><span class="sxs-lookup"><span data-stu-id="59430-382">Call outputter from U-SQL base script</span></span>
<span data-ttu-id="59430-383">Per chiamare un outputter personalizzato dallo script U-SQL di base, è necessario creare la nuova istanza dell'oggetto outputter.</span><span class="sxs-lookup"><span data-stu-id="59430-383">To call a custom outputter from the base U-SQL script, the new instance of the outputter object has to be created.</span></span>

```sql
OUTPUT @rs0 TO @output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="59430-384">Per evitare di creare un'istanza dell'oggetto nello script di base, è possibile creare un wrapper di funzione, come illustrato nell'esempio precedente:</span><span class="sxs-lookup"><span data-stu-id="59430-384">To avoid creating an instance of the object in base script, we can create a function wrapper, as shown in our earlier example:</span></span>

```c#
        // Define the factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

<span data-ttu-id="59430-385">In questo caso, la chiamata originale si presenta come segue:</span><span class="sxs-lookup"><span data-stu-id="59430-385">In this case, the original call looks like the following:</span></span>

```
OUTPUT @rs0 
TO @output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a><span data-ttu-id="59430-386">Usare elaboratori definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="59430-386">Use user-defined processors</span></span>
<span data-ttu-id="59430-387">Un elaboratore definito dall'utente (UDP) è un tipo di oggetto definito dall'utente di U-SQL che consente di elaborare le righe in ingresso applicando funzionalità di programmabilità.</span><span class="sxs-lookup"><span data-stu-id="59430-387">User-defined processor, or UDP, is a type of U-SQL UDO that enables you to process the incoming rows by applying programmability features.</span></span> <span data-ttu-id="59430-388">Un elaboratore definito dall'utente consente di combinare colonne, modificare valori e aggiungere nuove colonne, se necessario.</span><span class="sxs-lookup"><span data-stu-id="59430-388">UDP enables you to combine columns, modify values, and add new columns if necessary.</span></span> <span data-ttu-id="59430-389">Essenzialmente, consente di elaborare un set di righe per produrre gli elementi dati necessari.</span><span class="sxs-lookup"><span data-stu-id="59430-389">Basically, it helps to process a rowset to produce required data elements.</span></span>

<span data-ttu-id="59430-390">Per definire un elaboratore definito dall'utente, è necessario creare un'interfaccia `IProcessor` con l'attributo `SqlUserDefinedProcessor`, che per gli elaboratori definiti dall'utente è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="59430-390">To define a UDP, we need to create an `IProcessor` interface with the `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span></span>

<span data-ttu-id="59430-391">L'interfaccia deve contenere la definizione per l'override dei set di righe dell'interfaccia `IRow`, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="59430-391">This interface should contain the definition for the `IRow` interface rowset override, as shown in the following example:</span></span>

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

<span data-ttu-id="59430-392">**SqlUserDefinedProcessor** indica che il tipo deve essere registrato come Processor definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59430-392">**SqlUserDefinedProcessor** indicates that the type should be registered as a user-defined processor.</span></span> <span data-ttu-id="59430-393">Questa classe non può essere ereditata.</span><span class="sxs-lookup"><span data-stu-id="59430-393">This class cannot be inherited.</span></span>

<span data-ttu-id="59430-394">Per la definizione degli elaboratori definiti dall'utente, l'attributo SqlUserDefinedProcessor è **facoltativo**.</span><span class="sxs-lookup"><span data-stu-id="59430-394">The SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span></span>

<span data-ttu-id="59430-395">I principali oggetti di programmabilità sono **input** e **output**.</span><span class="sxs-lookup"><span data-stu-id="59430-395">The main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="59430-396">L'oggetto di input viene usato per enumerare le colonne di input e l'output e per impostare i dati di output come risultato dell'attività di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="59430-396">The input object is used to enumerate input columns and output, and to set output data as a result of the processor activity.</span></span>

<span data-ttu-id="59430-397">Per l'enumerazione delle colonne di input, si usa il metodo `input.Get`.</span><span class="sxs-lookup"><span data-stu-id="59430-397">For input columns enumeration, we use the `input.Get` method.</span></span>

```
string column_name = input.Get<string>("column_name");
```

<span data-ttu-id="59430-398">Il parametro per il metodo `input.Get` è una colonna passata come parte della clausola `PRODUCE` dell'istruzione `PROCESS` dello script U-SQL di base.</span><span class="sxs-lookup"><span data-stu-id="59430-398">The parameter for `input.Get` method is a column that's passed as part of the `PRODUCE` clause of the `PROCESS` statement of the U-SQL base script.</span></span> <span data-ttu-id="59430-399">In questo caso è necessario usare il tipo di dati corretto.</span><span class="sxs-lookup"><span data-stu-id="59430-399">We need to use the correct data type here.</span></span>

<span data-ttu-id="59430-400">Per l'output, usare il metodo `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="59430-400">For output, use the `output.Set` method.</span></span>

<span data-ttu-id="59430-401">È importante notare che il producer personalizzato restituisce solo le colonne e i valori definiti con la chiamata al metodo `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="59430-401">It's important to note that custom producer only outputs columns and values that are defined with the `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", mycolumn);
```

<span data-ttu-id="59430-402">L'output effettivo dell'elaboratore viene attivato chiamando `return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="59430-402">The actual processor output is triggered by calling `return output.AsReadOnly();`.</span></span>

<span data-ttu-id="59430-403">Di seguito è riportato un esempio di elaboratore:</span><span class="sxs-lookup"><span data-stu-id="59430-403">Following is a processor example:</span></span>

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

<span data-ttu-id="59430-404">Nello scenario di questo caso d'uso, l'elaboratore genera una nuova colonna denominata "full_description" combinando le colonne esistenti, in questo caso "user" in lettere maiuscole e "des".</span><span class="sxs-lookup"><span data-stu-id="59430-404">In this use-case scenario, the processor is generating a new column called “full_description” by combining the existing columns--in this case, “user” in upper case, and “des”.</span></span> <span data-ttu-id="59430-405">Rigenera anche un GUID e restituisce il nuovo valore GUID e quello originale.</span><span class="sxs-lookup"><span data-stu-id="59430-405">It also regenerates a GUID and returns the original and new GUID values.</span></span>

<span data-ttu-id="59430-406">Come si può notare nell'esempio precedente, è possibile chiamare metodi C# durante la chiamata al metodo `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="59430-406">As you can see from the previous example, you can call C# methods during `output.Set` method call.</span></span>

<span data-ttu-id="59430-407">Di seguito è riportato un esempio di script U-SQL di base che usa un elaboratore personalizzato:</span><span class="sxs-lookup"><span data-stu-id="59430-407">Following is an example of base U-SQL script that uses a custom processor:</span></span>

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

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

## <a name="use-user-defined-appliers"></a><span data-ttu-id="59430-408">Usare oggetti di applicazione definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="59430-408">Use user-defined appliers</span></span>
<span data-ttu-id="59430-409">Un oggetto di applicazione definito dall'utente di U-SQL consente di richiamare una funzione C# personalizzata per ogni riga restituita dall'espressione di tabella esterna di una query.</span><span class="sxs-lookup"><span data-stu-id="59430-409">A U-SQL user-defined applier enables you to invoke a custom C# function for each row that's returned by the outer table expression of a query.</span></span> <span data-ttu-id="59430-410">L'input di destra viene valutato per ogni riga dell'input di sinistra e le righe prodotte vengono combinate per l'output finale.</span><span class="sxs-lookup"><span data-stu-id="59430-410">The right input is evaluated for each row from the left input, and the rows that are produced are combined for the final output.</span></span> <span data-ttu-id="59430-411">L'elenco delle colonne prodotte dall'operatore APPLY è la combinazione del set di colonne dell'input di destra e di sinistra.</span><span class="sxs-lookup"><span data-stu-id="59430-411">The list of columns that are produced by the APPLY operator are the combination of the set of columns in the left and the right input.</span></span>

<span data-ttu-id="59430-412">Un oggetto di applicazione definito dall'utente viene richiamato come parte dell'espressione SELECT di U-SQL.</span><span class="sxs-lookup"><span data-stu-id="59430-412">User-defined applier is being invoked as part of the USQL SELECT expression.</span></span>

<span data-ttu-id="59430-413">La chiamata tipica all'oggetto di applicazione definito dall'utente si presenta come segue:</span><span class="sxs-lookup"><span data-stu-id="59430-413">The typical call to the user-defined applier looks like the following:</span></span>

```
SELECT …
FROM …
CROSS APPLYis used to pass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

<span data-ttu-id="59430-414">Per altre informazioni sull'uso di oggetti di applicazione in un'espressione SELECT, vedere [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx) (Selezione con SELECT di U-SQL da CROSS APPLY e OUTER APPLY).</span><span class="sxs-lookup"><span data-stu-id="59430-414">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span></span>

<span data-ttu-id="59430-415">La definizione della classe base degli oggetti di applicazione definiti dall'utente è la seguente:</span><span class="sxs-lookup"><span data-stu-id="59430-415">The user-defined applier base class definition is as follows:</span></span>

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

<span data-ttu-id="59430-416">Per definire un oggetto di applicazione definito dall'utente, è necessario creare l'interfaccia `IApplier` con l'attributo [`SqlUserDefinedApplier`], che per la definizione di un oggetto di applicazione definito dall'utente è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="59430-416">To define a user-defined applier, we need to create the `IApplier` interface with the [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span></span>

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

* <span data-ttu-id="59430-417">Apply viene chiamato per ogni riga della tabella esterna.</span><span class="sxs-lookup"><span data-stu-id="59430-417">Apply is called for each row of the outer table.</span></span> <span data-ttu-id="59430-418">Restituisce il set di righe di output di `IUpdatableRow`.</span><span class="sxs-lookup"><span data-stu-id="59430-418">It returns the `IUpdatableRow` output rowset.</span></span>
* <span data-ttu-id="59430-419">La classe del costruttore viene usata per passare parametri all'oggetto di applicazione definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59430-419">The Constructor class is used to pass parameters to the user-defined applier.</span></span>

<span data-ttu-id="59430-420">**SqlUserDefinedApplier** indica che il tipo deve essere registrato come oggetto di applicazione definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59430-420">**SqlUserDefinedApplier** indicates that the type should be registered as a user-defined applier.</span></span> <span data-ttu-id="59430-421">Questa classe non può essere ereditata.</span><span class="sxs-lookup"><span data-stu-id="59430-421">This class cannot be inherited.</span></span>

<span data-ttu-id="59430-422">**SqlUserDefinedApplier** è **facoltativo** per la definizione di un oggetto di applicazione definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59430-422">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span></span>


<span data-ttu-id="59430-423">I principali oggetti di programmabilità sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="59430-423">The main programmability objects are as follows:</span></span>

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

<span data-ttu-id="59430-424">I set di righe di input vengono passati come input `IRow`.</span><span class="sxs-lookup"><span data-stu-id="59430-424">Input rowsets are passed as `IRow` input.</span></span> <span data-ttu-id="59430-425">Le righe di output vengono generate come interfaccia di output `IUpdatableRow`.</span><span class="sxs-lookup"><span data-stu-id="59430-425">The output rows are generated as `IUpdatableRow` output interface.</span></span>

<span data-ttu-id="59430-426">I nomi delle singole colonne possono essere determinati chiamando il metodo dello schema `IRow`.</span><span class="sxs-lookup"><span data-stu-id="59430-426">Individual column names can be determined by calling the `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="59430-427">Per ottenere i valori di dati effettivi da `IRow` in ingresso, si usa il metodo Get() dell'interfaccia `IRow`.</span><span class="sxs-lookup"><span data-stu-id="59430-427">To get the actual data values from the incoming `IRow`, we use the Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="59430-428">In alternativa, si usa il nome di colonna dello schema:</span><span class="sxs-lookup"><span data-stu-id="59430-428">Or we use the schema column name:</span></span>

```
row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="59430-429">I valori di output devono essere impostati con l'output di `IUpdatableRow`:</span><span class="sxs-lookup"><span data-stu-id="59430-429">The output values must be set with `IUpdatableRow` output:</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="59430-430">È importante comprendere che gli oggetti di applicazione personalizzati restituiscono solo le colonne o i valori definiti con la chiamata al metodo `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="59430-430">It is important to understand that custom appliers only output columns and values that are defined with `output.Set` method call.</span></span>

<span data-ttu-id="59430-431">L'output effettivo viene attivato chiamando `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="59430-431">The actual output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="59430-432">I parametri dell'oggetto di applicazione definito dall'utente possono essere passati al costruttore.</span><span class="sxs-lookup"><span data-stu-id="59430-432">The user-defined applier parameters can be passed to the constructor.</span></span> <span data-ttu-id="59430-433">L'oggetto di applicazione può restituire un numero variabile di colonne da definire durante la chiamata all'oggetto di applicazione nello script U-SQL di base.</span><span class="sxs-lookup"><span data-stu-id="59430-433">Applier can return a variable number of columns that need to be defined during the applier call in base U-SQL Script.</span></span>

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

<span data-ttu-id="59430-434">Di seguito è riportato un esempio di oggetto di applicazione definito dall'utente:</span><span class="sxs-lookup"><span data-stu-id="59430-434">Here is the user-defined applier example:</span></span>

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

<span data-ttu-id="59430-435">Di seguito è riportato lo script U-SQL di base per questo oggetto di applicazione definito dall'utente:</span><span class="sxs-lookup"><span data-stu-id="59430-435">Following is the base U-SQL script for this user-defined applier:</span></span>

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

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="59430-436">Nello scenario di questo caso d'uso, l'oggetto di applicazione definito dall'utente funge da parser di valori delimitati da virgole per le proprietà del parco auto.</span><span class="sxs-lookup"><span data-stu-id="59430-436">In this use case scenario, user-defined applier acts as a comma-delimited value parser for the car fleet properties.</span></span> <span data-ttu-id="59430-437">Le righe del file di input si presentano come segue:</span><span class="sxs-lookup"><span data-stu-id="59430-437">The input file rows look like the following:</span></span>

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

<span data-ttu-id="59430-438">Si tratta di un normale file con valori delimitati da tabulazioni (TSV) con una colonna di proprietà contenente le proprietà delle automobili, come marca e modello.</span><span class="sxs-lookup"><span data-stu-id="59430-438">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span></span> <span data-ttu-id="59430-439">Tali proprietà devono essere analizzate rispetto alle colonne della tabella.</span><span class="sxs-lookup"><span data-stu-id="59430-439">Those properties must be parsed to the table columns.</span></span> <span data-ttu-id="59430-440">L'oggetto di applicazione specificato consente di generare un numero dinamico di proprietà nel set di righe, in base al parametro passato.</span><span class="sxs-lookup"><span data-stu-id="59430-440">The applier that's provided also enables you to generate a dynamic number of properties in the result rowset, based on the parameter that's passed.</span></span> <span data-ttu-id="59430-441">È possibile generare tutte le proprietà o solo uno specifico set di proprietà.</span><span class="sxs-lookup"><span data-stu-id="59430-441">You can generate either all properties or a specific set of properties only.</span></span>

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

<span data-ttu-id="59430-442">L'oggetto di applicazione definito dall'utente può essere chiamato come nuova istanza dell'oggetto di applicazione:</span><span class="sxs-lookup"><span data-stu-id="59430-442">The user-defined applier can be called as a new instance of applier object:</span></span>

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

<span data-ttu-id="59430-443">In alternativa, è possibile usare la chiamata a un metodo factory wrapper:</span><span class="sxs-lookup"><span data-stu-id="59430-443">Or with the invocation of a wrapper factory method:</span></span>

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a><span data-ttu-id="59430-444">Usare combinatori definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="59430-444">Use user-defined combiners</span></span>
<span data-ttu-id="59430-445">Un combinatore definito dall'utente (UDC) consente di combinare le righe dei set di sinistra e di destra, in base a logica personalizzata.</span><span class="sxs-lookup"><span data-stu-id="59430-445">User-defined combiner, or UDC, enables you to combine rows from left and right rowsets, based on custom logic.</span></span> <span data-ttu-id="59430-446">Il combinatore definito dall'utente viene usato con l'espressione COMBINE.</span><span class="sxs-lookup"><span data-stu-id="59430-446">User-defined combiner is used with COMBINE expression.</span></span>

<span data-ttu-id="59430-447">Un combinatore viene richiamato con l'espressione COMBINE, che specifica le informazioni necessarie su entrambi i set di righe di input, le colonne di raggruppamento e lo schema dei risultati previsto e informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="59430-447">A combiner is being invoked with the COMBINE expression that provides the necessary information about both the input rowsets, the grouping columns, the expected result schema, and additional information.</span></span>

<span data-ttu-id="59430-448">Per chiamare un combinatore in uno script U-SQL di base, si usa la sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="59430-448">To call a combiner in a base U-SQL script, we use the following syntax:</span></span>

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

<span data-ttu-id="59430-449">Per altre informazioni, vedere [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx) (Espressione COMBINE (U-SQL)).</span><span class="sxs-lookup"><span data-stu-id="59430-449">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span></span>

<span data-ttu-id="59430-450">Per definire un combinatore definito dall'utente, è necessario creare l'interfaccia `ICombiner` con l'attributo [`SqlUserDefinedCombiner`], che per la definizione di un combinatore definito dall'utente è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="59430-450">To define a user-defined combiner, we need to create the `ICombiner` interface with the [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span></span>

<span data-ttu-id="59430-451">Definizione della classe `ICombiner` di base:</span><span class="sxs-lookup"><span data-stu-id="59430-451">Base `ICombiner` class definition:</span></span>

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

<span data-ttu-id="59430-452">L'implementazione personalizzata di un'interfaccia `ICombiner` deve contenere una definizione per un override `IEnumerable<IRow>` Combine.</span><span class="sxs-lookup"><span data-stu-id="59430-452">The custom implementation of an `ICombiner` interface should contain the definition for an `IEnumerable<IRow>` Combine override.</span></span>

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

<span data-ttu-id="59430-453">L'attributo **SqlUserDefinedCombiner** indica che il tipo deve essere registrato come combinatore definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59430-453">The **SqlUserDefinedCombiner** attribute indicates that the type should be registered as a user-defined combiner.</span></span> <span data-ttu-id="59430-454">Questa classe non può essere ereditata.</span><span class="sxs-lookup"><span data-stu-id="59430-454">This class cannot be inherited.</span></span>

<span data-ttu-id="59430-455">**SqlUserDefinedCombiner** viene usato per definire la proprietà della modalità di combinazione.</span><span class="sxs-lookup"><span data-stu-id="59430-455">**SqlUserDefinedCombiner** is used to define the Combiner mode property.</span></span> <span data-ttu-id="59430-456">È un attributo facoltativo per la definizione di un combinatore definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59430-456">It is an optional attribute for a user-defined combiner definition.</span></span>

<span data-ttu-id="59430-457">Modalità     CombinerMode</span><span class="sxs-lookup"><span data-stu-id="59430-457">CombinerMode     Mode</span></span>

<span data-ttu-id="59430-458">L'enumerazione CombinerMode può accettare i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="59430-458">CombinerMode enum can take the following values:</span></span>

* <span data-ttu-id="59430-459">Full (0): ogni riga di output dipende potenzialmente da tutte le righe di input di sinistra e di destra con lo stesso valore chiave.</span><span class="sxs-lookup"><span data-stu-id="59430-459">Full  (0) Every output row potentially depends on all the input rows from left and right       with the same key value.</span></span>

* <span data-ttu-id="59430-460">Left (1): ogni riga di output dipende da una singola riga di input di sinistra e potenzialmente da tutte le righe di destra con lo stesso valore chiave.</span><span class="sxs-lookup"><span data-stu-id="59430-460">Left  (1) Every output row depends on a single input row from the left (and potentially all rows       from the right with the same key value).</span></span>

* <span data-ttu-id="59430-461">Right (2): ogni riga di output dipende da una singola riga di input di destra e potenzialmente da tutte le righe di sinistra con lo stesso valore chiave.</span><span class="sxs-lookup"><span data-stu-id="59430-461">Right (2)     Every output row depends on a single input row from the right (and potentially all rows       from the left with the same key value).</span></span>

* <span data-ttu-id="59430-462">Inner (3): ogni riga di output dipende da una singola riga di input di sinistra e di destra con lo stesso valore.</span><span class="sxs-lookup"><span data-stu-id="59430-462">Inner (3) Every output row depends on a single input row from left and right with the same value.</span></span>

<span data-ttu-id="59430-463">Esempio:     [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span><span class="sxs-lookup"><span data-stu-id="59430-463">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span></span>


<span data-ttu-id="59430-464">I principali oggetti di programmabilità sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="59430-464">The main programmability objects are:</span></span>

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

<span data-ttu-id="59430-465">I set di righe di input vengono passati come tipo di interfaccia `IRowset` a **sinistra** e a **destra**.</span><span class="sxs-lookup"><span data-stu-id="59430-465">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span></span> <span data-ttu-id="59430-466">Entrambi i set di righe devono essere enumerati per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="59430-466">Both rowsets must be enumerated for processing.</span></span> <span data-ttu-id="59430-467">È possibile enumerare ogni interfaccia una sola volta, quindi deve essere enumerata e memorizzata nella cache, se necessario.</span><span class="sxs-lookup"><span data-stu-id="59430-467">You can only enumerate each interface once, so we have to enumerate and cache it if necessary.</span></span>

<span data-ttu-id="59430-468">Per la memorizzazione nella cache, è possibile creare un tipo di struttura di memoria List\<T\> come risultato dell'esecuzione di una query LINQ, specificamente List<`IRow`>.</span><span class="sxs-lookup"><span data-stu-id="59430-468">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span></span> <span data-ttu-id="59430-469">Durante l'enumerazione è possibile usare anche il tipo di dati anonimo.</span><span class="sxs-lookup"><span data-stu-id="59430-469">The anonymous data type can be used during enumeration as well.</span></span>

<span data-ttu-id="59430-470">Per altre informazioni su tali query, vedere l'[introduzione alle query LINQ (C#)](https://msdn.microsoft.com/library/bb397906.aspx). Per altre informazioni sull'interfaccia IEnumerable\<T\>, vedere [Interfaccia IEnumerable\<T\>](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="59430-470">See [Introduction to LINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span></span>

<span data-ttu-id="59430-471">Per ottenere i valori di dati effettivi da `IRowset` in ingresso, si usa il metodo Get() dell'interfaccia `IRow`.</span><span class="sxs-lookup"><span data-stu-id="59430-471">To get the actual data values from the incoming `IRowset`, we use the Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="59430-472">I nomi delle singole colonne possono essere determinati chiamando il metodo dello schema `IRow`.</span><span class="sxs-lookup"><span data-stu-id="59430-472">Individual column names can be determined by calling the `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="59430-473">In alternativa, è possibile usare il nome di colonna dello schema:</span><span class="sxs-lookup"><span data-stu-id="59430-473">Or by using the schema column name:</span></span>

```
c# row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="59430-474">L'enumerazione generale con LINQ si presenta come segue:</span><span class="sxs-lookup"><span data-stu-id="59430-474">The general enumeration with LINQ looks like the following:</span></span>

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

<span data-ttu-id="59430-475">Al termine dell'enumerazione di entrambi i set di righe, si scorreranno in ciclo tutte le righe.</span><span class="sxs-lookup"><span data-stu-id="59430-475">After enumerating both rowsets, we are going to loop through all rows.</span></span> <span data-ttu-id="59430-476">Per ogni riga del set di sinistra si troveranno tutte le righe che soddisfano la condizione del combinatore.</span><span class="sxs-lookup"><span data-stu-id="59430-476">For each row in the left rowset, we are going to find all rows that satisfy the condition of our combiner.</span></span>

<span data-ttu-id="59430-477">I valori di output devono essere impostati con l'output di `IUpdatableRow`.</span><span class="sxs-lookup"><span data-stu-id="59430-477">The output values must be set with `IUpdatableRow` output.</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="59430-478">L'output effettivo viene attivato chiamando `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="59430-478">The actual output is triggered by calling to `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="59430-479">Di seguito è riportato un esempio di combinatore:</span><span class="sxs-lookup"><span data-stu-id="59430-479">Following is a combiner example:</span></span>

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

<span data-ttu-id="59430-480">Nello scenario di questo caso d'uso, si crea un report analitico per il rivenditore.</span><span class="sxs-lookup"><span data-stu-id="59430-480">In this use-case scenario, we are building an analytics report for the retailer.</span></span> <span data-ttu-id="59430-481">L'obiettivo è trovare tutti i prodotti che costano più di 20.000 dollari e che in un dato intervallo di tempo vengono venduti più velocemente tramite il sito Web che non tramite il normale rivenditore.</span><span class="sxs-lookup"><span data-stu-id="59430-481">The goal is to find all products that cost more than $20,000 and that sell through the website faster than through the regular retailer within a certain time frame.</span></span>

<span data-ttu-id="59430-482">Di seguito è riportato lo script U-SQL di base,</span><span class="sxs-lookup"><span data-stu-id="59430-482">Here is the base U-SQL script.</span></span> <span data-ttu-id="59430-483">in cui è possibile confrontare la logica di un JOIN regolare e di un combinatore:</span><span class="sxs-lookup"><span data-stu-id="59430-483">You can compare the logic between a regular JOIN and a combiner:</span></span>

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

OUTPUT @rs1 TO @output_file1 USING Outputters.Tsv();
OUTPUT @rs2 TO @output_file2 USING Outputters.Tsv();
```

<span data-ttu-id="59430-484">Un combinatore definito dall'utente può essere chiamato come nuova istanza dell'oggetto di applicazione:</span><span class="sxs-lookup"><span data-stu-id="59430-484">A user-defined combiner can be called as a new instance of the applier object:</span></span>

```
USING new MyNameSpace.MyCombiner();
```


<span data-ttu-id="59430-485">In alternativa, è possibile usare la chiamata a un metodo factory wrapper:</span><span class="sxs-lookup"><span data-stu-id="59430-485">Or with the invocation of a wrapper factory method:</span></span>

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a><span data-ttu-id="59430-486">Usare riduttori definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="59430-486">Use user-defined reducers</span></span>

<span data-ttu-id="59430-487">U-SQL consente di scrivere riduttori di set di righe personalizzati in C# usando il framework di estendibilità degli operatori definito dall'utente e implementando un'interfaccia IReducer.</span><span class="sxs-lookup"><span data-stu-id="59430-487">U-SQL enables you to write custom rowset reducers in C# by using the user-defined operator extensibility framework and implementing an IReducer interface.</span></span>

<span data-ttu-id="59430-488">Un riduttore definito dall'utente (UDR) può essere usato per eliminare le righe non necessarie durante l'estrazione (importazione) di dati,</span><span class="sxs-lookup"><span data-stu-id="59430-488">User-defined reducer, or UDR, can be used to eliminate unnecessary rows during data extraction (import).</span></span> <span data-ttu-id="59430-489">nonché per modificare e valutare righe e colonne.</span><span class="sxs-lookup"><span data-stu-id="59430-489">It also can be used to manipulate and evaluate rows and columns.</span></span> <span data-ttu-id="59430-490">In base alla logica di programmabilità, può anche definire le righe da estrarre.</span><span class="sxs-lookup"><span data-stu-id="59430-490">Based on programmability logic, it can also define which rows need to be extracted.</span></span>

<span data-ttu-id="59430-491">Per definire una classe di riduttori definiti dall'utente, è necessario creare un'interfaccia `IReducer` con l'attributo `SqlUserDefinedReducer` facoltativo.</span><span class="sxs-lookup"><span data-stu-id="59430-491">To define a UDR class, we need to create an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span></span>

<span data-ttu-id="59430-492">Questa interfaccia di classe deve contenere una definizione per l'override dei set di righe dell'interfaccia `IEnumerable`.</span><span class="sxs-lookup"><span data-stu-id="59430-492">This class interface should contain a definition for the `IEnumerable` interface rowset override.</span></span>

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

<span data-ttu-id="59430-493">L'attributo **SqlUserDefinedReducer** indica che il tipo deve essere registrato come riduttore definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59430-493">The **SqlUserDefinedReducer** attribute indicates that the type should be registered as a user-defined reducer.</span></span> <span data-ttu-id="59430-494">Questa classe non può essere ereditata.</span><span class="sxs-lookup"><span data-stu-id="59430-494">This class cannot be inherited.</span></span>
<span data-ttu-id="59430-495">**SqlUserDefinedReducer** è un attributo facoltativo per la definizione di un riduttore definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59430-495">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span></span> <span data-ttu-id="59430-496">Viene usato per definire la proprietà IsRecursive.</span><span class="sxs-lookup"><span data-stu-id="59430-496">It's used to define IsRecursive property.</span></span>

* <span data-ttu-id="59430-497">bool     IsRecursive</span><span class="sxs-lookup"><span data-stu-id="59430-497">bool     IsRecursive</span></span>    
* <span data-ttu-id="59430-498">**true**  = indica se il riduttore è idempotente</span><span class="sxs-lookup"><span data-stu-id="59430-498">**true**  = Indicates whether this Reducer is idempotent</span></span>

<span data-ttu-id="59430-499">I principali oggetti di programmabilità sono **input** e **output**.</span><span class="sxs-lookup"><span data-stu-id="59430-499">The main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="59430-500">L'oggetto di input viene usato per enumerare le righe di input.</span><span class="sxs-lookup"><span data-stu-id="59430-500">The input object is used to enumerate input rows.</span></span> <span data-ttu-id="59430-501">L'output viene usato per impostare le righe di output come risultato dell'attività di riduzione.</span><span class="sxs-lookup"><span data-stu-id="59430-501">Output is used to set output rows as a result of reducing activity.</span></span>

<span data-ttu-id="59430-502">Per l'enumerazione delle righe di input, si usa il metodo `Row.Get`.</span><span class="sxs-lookup"><span data-stu-id="59430-502">For input rows enumeration, we use the `Row.Get` method.</span></span>

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

<span data-ttu-id="59430-503">Il parametro per il metodo `Row.Get` è una colonna passata come parte della classe `PRODUCE` dell'istruzione `REDUCE` dello script U-SQL di base.</span><span class="sxs-lookup"><span data-stu-id="59430-503">The parameter for the `Row.Get` method is a column that's passed as part of the `PRODUCE` class of the `REDUCE` statement of the U-SQL base script.</span></span> <span data-ttu-id="59430-504">Anche qui occorre usare il tipo di dati corretto.</span><span class="sxs-lookup"><span data-stu-id="59430-504">We need to use the correct data type here as well.</span></span>

<span data-ttu-id="59430-505">Per l'output, usare il metodo `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="59430-505">For output, use the `output.Set` method.</span></span>

<span data-ttu-id="59430-506">È importante comprendere che il riduttore personalizzato restituisce solo i valori definiti con la chiamata al metodo `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="59430-506">It is important to understand that custom reducer only outputs values that are defined with the `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", guid);
```

<span data-ttu-id="59430-507">L'output effettivo del riduttore viene attivato chiamando `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="59430-507">The actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="59430-508">Di seguito è riportato un esempio di riduttore:</span><span class="sxs-lookup"><span data-stu-id="59430-508">Following is a reducer example:</span></span>

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

<span data-ttu-id="59430-509">Nello scenario di questo caso d'uso, il riduttore ignora le righe con nome utente vuoto.</span><span class="sxs-lookup"><span data-stu-id="59430-509">In this use-case scenario, the reducer is skipping rows with an empty user name.</span></span> <span data-ttu-id="59430-510">Per ogni riga nel set, legge ogni colonna obbligatoria e quindi valuta la lunghezza del nome utente.</span><span class="sxs-lookup"><span data-stu-id="59430-510">For each row in rowset, it reads each required column, then evaluates the length of the user name.</span></span> <span data-ttu-id="59430-511">Restituisce la riga effettiva solo se il valore del nome utente ha una lunghezza superiore a 0.</span><span class="sxs-lookup"><span data-stu-id="59430-511">It outputs the actual row only if user name value length is more than 0.</span></span>

<span data-ttu-id="59430-512">Di seguito è riportato uno script U-SQL di base che usa un riduttore personalizzato:</span><span class="sxs-lookup"><span data-stu-id="59430-512">Following is base U-SQL script that uses a custom reducer:</span></span>

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
    TO @output_file 
    USING Outputters.Text();
```
