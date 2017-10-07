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
# <a name="u-sql-programmability-guide"></a>Guida alla programmabilità di U-SQL

U-SQL è un linguaggio di query progettato per carichi di lavoro di tipo Big Data. Una delle funzionalità specifiche di hello dell'U-SQL è costituito di hello hello dichiarativa linguaggio relativi all'estensibilità di hello e programmabilità fornita da c#. In questa Guida, vengono presi in considerazione hello estensibilità e programmabilità del linguaggio di hello U-SQL che è abilitato per c#.

## <a name="requirements"></a>Requisiti

Scaricare e installare [Strumenti Azure Data Lake per Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).

## <a name="get-started-with-u-sql"></a>Introduzione a U-SQL  

Diamo un'occhiata hello lo script U-SQL seguente:

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

Definisce un set di righe chiamato @a e crea un set di righe chiamato @results da @a.

## <a name="c-types-and-expressions-in-u-sql-script"></a>Tipi ed espressioni C# in uno script U-SQL

Un'espressione U-SQL è un'espressione C# combinata con operazioni logiche U-SQL quali `AND`, `OR` e `NOT`. Le espressioni U-SQL possono essere utilizzate con l'istruzione SELECT, EXTRACT, WHERE, HAVING, GROUP BY e DECLARE.

Ad esempio, un valore DateTime nella clausola SELECT hello hello lo script seguente analizza una stringa.

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

Hello lo script seguente analizza una stringa di un valore DateTime in un'istruzione DECLARE.

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a>Usare espressioni C# per conversioni del tipo di dati
Hello di esempio seguente viene illustrato come si una conversione di dati datetime utilizzando espressioni di c#. In questo particolare scenario, dati di stringa datetime sono datetime convertito toostandard con notazione ora 00:00:00 di mezzanotte.

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a>Usare espressioni C# per la data odierna
toopull data, è possibile utilizzare hello espressione c# seguente:

```
DateTime.Now.ToString("M/d/yyyy")
```

Di seguito è riportato un esempio di come toouse questa espressione in uno script:

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



## <a name="using-net-assemblies"></a>Uso di assembly .NET
Modello di estendibilità U-SQL si basa fortemente su codice personalizzato di hello possibilità tooadd. Attualmente, U-SQL fornisce semplici modi tooadd proprio Microsoft. Codice basato su rete (in particolare, in c#). È anche possibile, tuttavia, aggiungere codice personalizzato scritto in altri linguaggi .NET, come VB.NET o F#. 

### <a name="register-a-net-assembly"></a>Registrare un assembly .NET

Utilizzare tooplace di istruzione CREATE ASSEMBLY hello un assembly .NET in un Database U-SQL. Una volta un assembly in un database, gli script U-SQL è possono utilizzare tali assembly utilizzando l'istruzione di ASSEMBLY di riferimento hello. 

Hello seguente codice mostra come tooregister un assembly:

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

Hello seguente codice mostra come tooreference un assembly:

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

Consultare hello [le istruzioni di registrazione assembly](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) che descrive in dettaglio in questo argomento.


### <a name="use-assembly-versioning"></a>Usare il controllo delle versioni degli assembly
Attualmente, U-SQL Usa hello .NET Framework versione 4.5. Verificare che siano compatibili con tale versione del runtime di hello assembly personalizzati.

Come indicato in precedenza, U-SQL esegue il codice in un formato a 64 bit (x64). Verificare pertanto che il codice viene compilato toorun su x64. In caso contrario, viene visualizzato errore di formato non corretto di hello illustrato in precedenza.

Ogni DLL di assembly e file di risorse caricato (ad esempio un diverso runtime, un assembly nativo o un file di configurazione) può essere al massimo di 400 MB. dimensioni totali di Hello risorse distribuiti, tramite la risorsa di distribuire o tramite tooassemblies riferimenti e i file aggiuntivi, non possono superare i 3 GB.

Si noti infine che ogni database U-SQL può contenere solo una versione di un determinato assembly. Ad esempio, se è necessario sia versione 7 e 8 di hello NewtonSoft Json.Net libreria, è necessario tooregister usarle in due database diversi. Inoltre, ogni script può fare riferimento solo tooone versione di un determinato assembly DLL. In questo senso, U-SQL semantica hello c# assembly gestione e controllo delle versioni.


## <a name="use-user-defined-functions-udf"></a>Usare funzioni definite dall'utente (UDF)
Funzioni definite dall'utente U-SQL o funzione definita dall'utente, programmazione routine che accettano parametri, eseguono un'azione (ad esempio un calcolo complesso) e restituiscono il risultato di hello di azione come valore. Hello restituiti valore della funzione definita dall'utente può essere solo un singolo valore scalare. Una funzione UDF di U-SQL può essere chiamata nello script di base di U-SQL come qualsiasi altra funzione scalare di C#.

È consigliabile inizializzare le funzioni definite dall'utente di U-SQL come **public** e **static**.

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

Primo diamo un'occhiata hello semplice esempio di creazione di una funzione definita dall'utente.

In questo scenario di caso d'uso, è necessario toodetermine hello periodo fiscale, tra cui trimestre fiscale hello e mese fiscale di hello prima Accedi per utente specifico di hello. Hello primo mese fiscale dell'anno hello in questo scenario è giugno.

periodo fiscale toocalculate, si introduce hello funzione c# seguente:

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

In questo modo vengono semplicemente calcolati il mese e il trimestre fiscali e viene restituito un valore stringa. Del mese di giugno, hello primo mese del hello primo trimestre fiscale, utilizziamo "Q1:P1". per luglio "Q1:P2" e così via.

Si tratta di una normale funzione c# che stiamo toouse continua nel progetto U-SQL.

Di seguito è illustrato l'aspetto di sezione di codice hello in questo scenario:

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

A questo punto verrà toocall questa funzione dallo script U-SQL di base hello. toodo, abbiamo tooprovide un nome completo per la funzione hello, tra cui hello dello spazio dei nomi, in questo caso NameSpace.Class.Function(parameter).

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

Di seguito è hello effettivo U-SQL script di base:

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

Di seguito è hello i file di output dell'esecuzione dello script hello:

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

In questo esempio viene illustrato un uso semplificato della funzione UDF inline in U-SQL.

### <a name="keep-state-between-udf-invocations"></a>Mantenere lo stato tra chiamate di funzioni definite dall'utente
Gli oggetti di programmazione c# U-SQL possono essere più sofisticati, che utilizzano interattività tramite le variabili globali di codice hello. Diamo un'occhiata hello segue scenario di caso d'uso di business.

Nelle grandi organizzazioni gli utenti possono accedere a svariate applicazioni interne, ad esempio Microsoft Dynamics CRM, Power BI e così via. I clienti potrebbe essere necessario tooapply un'analisi di dati di telemetria di come gli utenti passare tra applicazioni diverse, quali utilizzo hello tendenze sono e così via. obiettivo Hello per le aziende hello è l'utilizzo dell'applicazione toooptimize. Si potrebbe essere inoltre toocombine diverse applicazioni o routine di accesso specifiche.

tooachieve questo obiettivo, abbiamo toodetermine ID di sessione e il tempo di ritardo tra hello ultima sessione che si sono verificati.

È necessario toofind una precedente Accedi e quindi assegnare questo sessioni di accesso tooall che vengono generato toohello stessa applicazione. primo test hello è che uno script di base U-SQL non consente i calcoli tooapply su colonne calcolate già con funzione LAG. Hello seconda situazione è che abbiamo sessione specifica di hello tookeep per tutte le sessioni in hello stesso periodo di tempo.

toosolve questo problema, è utilizzare una variabile globale all'interno di una sezione di codice: `static public string globalSession;`.

Questa variabile globale è applicato toohello intero set di righe durante l'esecuzione dello script.

Di seguito è una sezione di codice hello di questo programma U-SQL:

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

In questo esempio mostra hello (variabile globale) `static public string globalSession;` utilizzata all'interno di hello `getStampUserSession` (funzione) e il recupero reinizializzare ogni hello ora sessione parametro viene modificato.

Hello U-SQL script di base è la seguente:

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

Funzione `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` viene chiamato qui durante il calcolo di hello secondo memoria set di righe. Passa hello `UserSessionTimestamp` colonna e restituisce hello valore fino a quando `UserSessionTimestamp` è stato modificato.

file di output di Hello è come segue:

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

In questo esempio viene illustrato uno scenario di caso d'uso più complesso in cui viene utilizzata una variabile globale all'interno di una sezione di codice che viene applicato toohello memoria intero set di righe.

## <a name="use-user-defined-types-udt"></a>Usare tipi definiti dall'utente (UDT)
I tipi definiti dall'utente (UDT) sono un'altra funzionalità di programmabilità di U-SQL. L'UDT U-SQL funziona come un normale tipo definito dall'utente C#. In c# è un linguaggio fortemente tipizzato che consente l'utilizzo di hello di tipi incorporati e personalizzati definiti dall'utente.

U-SQL in modo implicito è in grado di serializzare o deserializzare i tipi definiti dall'utente non autorizzato quando hello tipo definito dall'utente viene passato tra vertici nei set di righe. Ciò significa che l'utente hello ha tooprovide un formattatore esplicito tramite l'interfaccia IFormatter hello. In questo modo U-SQL di hello serializzare e deserializzare i metodi per hello tipo definito dall'utente.

> [!NOTE]
> Estrattori incorporati e outputters U-SQL attualmente non è possibile serializzare o deserializzare tooor di dati di tipo definito dall'utente dai file anche con hello IFormatter set. Pertanto, quando si scrive il file di tooa dati di tipo definito dall'utente con l'istruzione di OUTPUT di hello o leggerlo con un'utilità di estrazione, si dispone di toopass come una stringa o matrice di byte. Quindi chiamare serializzazione hello e la deserializzazione di codice (ovvero, il metodo ToString () dell'UDT hello) in modo esplicito. Estrattori definito dall'utente outputters, in altri hello mano, possono leggere e scrivere tipi definiti dall'utente.

Se si tenta di toouse UDT in estrazione o OUTPUTTER (non selezionare precedente), come illustrato di seguito:

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

È stata ricevuta hello errore seguente:

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

toowork in outputter con tipo definito dall'utente, è necessario tooserialize è toostring con hello metodo ToString () o creare un outputter personalizzato.

Al momento non è possibile usare UDT in GROUP BY. Se il tipo definito dall'utente viene utilizzata in GROUP BY, viene generata un'eccezione hello errore seguente:

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

toodefine un tipo definito dall'utente, è necessario:

* Aggiungere i seguenti spazi dei nomi hello:

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* Aggiungere `Microsoft.Analytics.Interfaces`, che è necessario per le interfacce di tipo definito dall'utente hello. Inoltre, `System.IO` potrebbe essere necessario toodefine hello IFormatter interfaccia.

* Definire un tipo definito dall'utente con l'attributo SqlUserDefinedType.

**SqlUserDefinedType** è toomark utilizzata una definizione di tipo in un assembly come un tipo definito dall'utente (UDT) in U-SQL. proprietà Hello attributo hello riflettono caratteristiche fisiche di hello di hello tipo definito dall'utente. Questa classe non può essere ereditata.

SqlUserDefinedType è un attributo obbligatorio per la definizione dell'UDT.

costruttore Hello della classe hello:  

* SqlUserDefinedTypeAttribute (formattatore di tipo)

* Formattatore Type: richiesto parametro toodefine un formattatore di tipo definito dall'utente, in particolare, tipo di hello hello `IFormatter` interfaccia deve essere passata in questo caso.

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* Tipo definito dall'utente tipico richiede inoltre definizione dell'interfaccia IFormatter hello, come illustrato nell'esempio seguente hello:

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

Hello `IFormatter` interfaccia serializza e deserializza un oggetto grafico con il tipo di radice hello di \<typeparamref name = "T" >.

\<typeparam name = "T" > tipo radice per hello oggetto grafico tooserialize hello e deserializzare.

* **Deserializzare**: deserializzata dati hello sul flusso fornito hello e ricostruisce grafico hello degli oggetti.

* **Serializzare**: serializza un oggetto o un grafico degli oggetti, con hello dato flusso toohello fornito radice.

`MyType`istanza: istanza del tipo di hello.  
`IColumnWriter`writer / `IColumnReader` lettore: hello sottostante il flusso di colonna.  
`ISerializationContext`contesto: enumerazione che definisce un set di flag che specifica il contesto di origine o destinazione hello per flusso hello durante la serializzazione.

* **Intermedio**: Specifica il contesto di origine o destinazione hello non è un archivio permanente.

* **Persistenza**: Specifica il contesto di origine o destinazione hello è un archivio permanente.

Come un normale tipo C#, la definizione di un tipo definito dall'utente di U-SQL può includere override per operatori come +/==/!= e così via. Può anche includere metodi statici. Ad esempio, se si stabilirà toouse questo tipo definito dall'utente come tooa un parametro funzione di aggregazione MIN U-SQL, abbiamo toodefine < operatore override.

In questa Guida, è illustrato un esempio di identificazione del periodo fiscale da data specifica di hello in formato hello Qn:Pn (Q1:P10). Hello di esempio seguente viene illustrato come toodefine digitare un oggetto personalizzato per i valori del periodo fiscali.

Di seguito è riportato un esempio di sezione code-behind con tipo definito dall'utente e interfaccia IFormatter personalizzati:

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

tipo definito Hello include due numeri: trimestre e mese. Qui sono definiti gli operatori ==/!=/>/< e il metodo statico ToString ().

Come indicato in precedenza, il tipo definito dall'utente può essere usato nelle espressioni SELECT, ma non in OUTPUTTER/EXTRACTOR senza serializzazione personalizzata. Include sia toobe serializzato come una stringa con ToString () o con un OUTPUTTER/estrazione personalizzato.

Ora esaminiamo l'uso dell'UDT. In una sezione di codice, sono stati modificati i seguenti di toohello GetFiscalPeriod funzione:

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

Come si può notare, restituisce il valore di hello di questo tipo FiscalPeriod.

Qui è fornito un esempio di come toouse venga ulteriormente nello script di base U-SQL. Questo esempio illustra diverse forme di chiamata del tipo definito dall'utente dallo script U-SQL.

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

Ecco un esempio di una sezione code-behind completa:

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

## <a name="use-user-defined-aggregates-udagg"></a>Usare aggregazioni definite dall'utente (UDAGG)
Le aggregazioni definite dall'utente sono funzioni correlate all'aggregazione che non sono già incluse in U-SQL. esempio Hello può essere un'aggregazione tooperform matematiche personalizzate calcoli concatenazioni di stringa, le modifiche con le stringhe e così via.

definizione di classe di base aggregazione definita dall'utente Hello è come segue:

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

**SqlUserDefinedAggregate** indica che il tipo di hello deve essere registrato come una funzione di aggregazione definita dall'utente. Questa classe non può essere ereditata.

L'attributo SqlUserDefinedType è **facoltativo** per la definizione di aggregazioni definite dall'utente.


Hello classe di base consente parametri astratti toopass tre: due parametri di input e una come risultato di hello. tipi di dati Hello sono variabili e devono essere definiti durante l'ereditarietà della classe.

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

* **Init** esegue la chiamata una volta per ogni gruppo durante il calcolo. Fornisce la routine di inizializzazione per ogni gruppo di aggregazione.  
* **Accumulate** viene eseguito una volta per ogni valore. Fornisce funzionalità principali di hello per l'algoritmo di aggregazione hello. Può essere utilizzato tooaggregate valori con vari tipi di dati che vengono definiti durante l'ereditarietà della classe. Può accettare due parametri di tipi di dati della variabile.
* **Terminare** viene eseguita una volta per ogni gruppo di aggregazione alla fine hello elaborare toooutput hello risultato per ogni gruppo.

input corretto toodeclare e tipi di dati di output, utilizzare la definizione di classe hello come segue:

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* T1: Tooaccumulate parametro prima
* T2: Primo parametro tooaccumulate
* TResult: tipo restituito di Terminate

Ad esempio:

```
public class GuidAggregate : IAggregate<string, int, int>
```

oppure

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a>Usare aggregazioni definite dall'utente in U-SQL
Innanzitutto, toouse aggregazione definita dall'utente, definito nel codice o farvi riferimento da programmabilità esistente hello DLL come indicato in precedenza.

Utilizzare quindi hello la seguente sintassi:

```
AGG<UDAGG_functionname>(param1,param2)
```

Di seguito è riportato un esempio di aggregazione definita dall'utente:

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

Ecco lo script U-SQL di base:

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

In questo scenario, in caso di utilizzo vengono concatenati i GUID di classe per utenti specifici di hello.

## <a name="use-user-defined-objects-udo"></a>Usare oggetti definiti dall'utente (UDO)
U-SQL consente gli oggetti di programmabilità personalizzato toodefine, che vengono chiamati gli oggetti definiti dall'utente o l'operatore definito dall'utente.

Hello seguito è riportato un elenco di operatore definito dall'utente in U-SQL:

* Estrattori definiti dall'utente
    * Estrazione riga per riga
    * Utilizzato tooimplement estrazione dei dati dal file strutturati personalizzati

* Outputter definiti dall'utente
    * Output riga per riga
    * Utilizzare i tipi di dati personalizzati toooutput o formati di file personalizzati

* Elaboratori definiti dall'utente
    * Viene usato per richiedere una riga e produrre una riga
    * Tooreduce usato hello numero di colonne o creare nuove colonne con valori derivati da un set di colonna esistente

* Oggetti di applicazione definiti dall'utente
    * Richiedere una riga e produrre 0 righe toon
    * Viene usato con OUTER/CROSS APPLY

* Combinatori definiti dall'utente
    * Combinano set di righe (JOIN definiti dall'utente)

* Riduttori definiti dall'utente
    * Serve a richiedere n righe e produrre una riga
    * Utilizzato tooreduce hello numero di righe

Operatore definito dall'utente viene in genere chiamato in modo esplicito nello script U-SQL come parte di hello istruzioni U-SQL seguente:

* EXTRACT
* OUTPUT
* PROCESS
* COMBINE
* REDUCE

> [!NOTE]  
> Operatore definito dall'utente sono limitate tooconsume 0,5 Gb memoria.  Questa limitazione di memoria non è applicabile toolocal esecuzioni.

## <a name="use-user-defined-extractors"></a>Usare estrattori definiti dall'utente
U-SQL consente di dati esterni tooimport utilizzando un'istruzione di estrazione. L'istruzione EXTRACT consente di usare estrattori UDO predefiniti.  

* *Extractors.Text()*: consente di estrarre da file di testo delimitati di varie codifiche.

* *Extractors.Csv()*: consente di estrarre da file di testo delimitati da virgole (CSV) di varie codifiche.

* *Extractors.Tsv()*: consente di estrarre da file di testo delimitati da tabulazioni (TSV) di varie codifiche.

Può essere utile toodevelop un'utilità di estrazione personalizzata. Ciò può essere utile durante l'importazione di dati se si desidera toodo che hello seguenti attività:

* Modificare i dati di input suddividendo le colonne e modificando singoli valori. funzionalità del processore Hello è migliore per la combinazione di colonne.
* Analizzare dati non strutturati, come pagine Web e messaggi di posta elettronica, o dati parzialmente non strutturati, ad esempio XML/JSON.
* Analizzare dati in una codifica non supportata.

toodefine un'utilità di estrazione definite dall'utente, o UDI, dobbiamo toocreate un `IExtractor` interfaccia. Estrazione toohello parametri, tutti di input, come delimitatori di colonna o la riga e la codifica, devono toobe definita nel costruttore hello della classe hello. Hello `IExtractor` interfaccia deve inoltre contenere una definizione per hello `IEnumerable<IRow>` override come indicato di seguito:

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

Hello **SqlUserDefinedExtractor** attributo indica che il tipo di hello deve essere registrato come una tabella definita dall'utente. Questa classe non può essere ereditata.

SqlUserDefinedExtractor è un attributo facoltativo per la definizione di UDE, Proprietà AtomicFileProcessing toodefine e utilizzato per l'oggetto UDI hello.

* bool     AtomicFileProcessing   

* **true** indica che l'estrattore richiede file di input atomici (JSON, XML e così via)
* **false** indica che l'estrattore può gestire file suddivisi/distribuiti (CSV, SEQ e così via)

sono oggetti di programmabilità UDI principali Hello **input** e **output**. oggetto di input Hello è tooenumerate utilizzati i dati di input come `IUnstructuredReader`. oggetto di output di Hello è tooset utilizzati dati di output come risultato delle attività di estrazione hello.

accesso ai dati di input Hello tramite `System.IO.Stream` e `System.IO.StreamReader`.

Per l'enumerazione delle colonne di input, è innanzitutto la divisione di flusso di input hello utilizzando un delimitatore di riga.

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

Quindi, la riga di input viene ulteriormente suddivisa nelle parti di una colonna.

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

i dati di output tooset, utilizziamo hello `output.Set` metodo.

È importante toounderstand che hello estrazione personalizzato restituisce solo le colonne e i valori che sono definiti con l'output di hello. il metodo di chiamata output.Set.

```
output.Set<string>(count, part);
```

output di Hello estrazione effettivo viene attivato chiamando `yield return output.AsReadOnly();`.

Di seguito è riportato estrazione hello:

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

In questo scenario di caso d'uso, estrazione hello Rigenera hello GUID per la colonna "guid" e converte i valori hello del case tooupper di colonna "user". Gli estrattori personalizzati possono produrre risultati più complessi analizzando e modificando i dati di input.

Di seguito è riportato uno script U-SQL di base che usa un estrattore personalizzato:

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

## <a name="use-user-defined-outputters"></a>Usare outputter definiti dall'utente
Outputter definito dall'utente è un altro operatore definito dall'utente U-SQL che consente di tooextend funzionalità U-SQL. Estrazione toohello simile, esistono diverse outputters incorporato.

* *Outputters.Text()*: scrive dati toodelimited file di testo di codifiche differenti.
* *Outputters.Csv()*: consente di scrivere dati toocomma delimitati da virgole (CSV) file di codifiche differenti.
* *Outputters.Tsv()*: consente di scrivere dati tootab delimitati da virgole (TSV) file di codifiche differenti.

Outputter personalizzato consente toowrite dati in un formato definito personalizzato. Ciò può risultare utile per hello seguenti attività:

* Scrittura di file di dati strutturati toosemi o non strutturati.
* Scrittura di dati in codifiche non supportate
* Modifica dei dati di output o aggiunta di attributi personalizzati

toodefine definito dall'utente outputter, dobbiamo hello toocreate `IOutputter` interfaccia.

Di seguito è hello base `IOutputter` implementazione della classe:

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

Tutti i parametri toohello outputter, di input, come delimitatori di colonna, la codifica e così via, devono toobe definita nel costruttore hello della classe hello. Hello `IOutputter` interfaccia deve inoltre contenere una definizione per `void Output` eseguire l'override. attributo Hello `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` , facoltativamente, è possibile impostare per l'elaborazione di file atomico. Per ulteriori informazioni, vedere hello seguenti dettagli.

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

* `Output` viene chiamato per ogni riga di input. Restituisce hello `IUnstructuredWriter output` set di righe.
* classe costruttore Hello viene utilizzata la outputter toopass parametri toohello definito dall'utente.
* `Close`viene utilizzato toooptionally eseguire l'override dello stato costosa toorelease o determinare quando è stato scritto ultima riga hello.

**SqlUserDefinedOutputter** attributo indica che il tipo di hello deve essere registrato come un outputter definito dall'utente. Questa classe non può essere ereditata.

SqlUserDefinedOutputter è un attributo facoltativo per la definizione di un outputter definito dall'utente. Proprietà di AtomicFileProcessing toodefine hello è utilizzato.

* bool     AtomicFileProcessing   

* **true** indica che l'outputter richiede file di output atomici (JSON, XML e così via)
* **false** indica che l'outputter può gestire file suddivisi/distribuiti (CSV, SEQ e così via)

gli oggetti di programmabilità principale Hello sono **riga** e **output**. Hello **riga** tooenumerate utilizzati dati di output come rappresenta `IRow` interfaccia. **Output** è tooset utilizzati dati toohello destinazione di output.

Hello output dati si accede tramite hello `IRow` interfaccia. I dati di output vengono trasmessi una riga alla volta.

i singoli valori Hello vengono enumerati chiamando il metodo Get hello dell'interfaccia IRow hello:

```
row.Get<string>("column_name")
```

I nomi delle singole colonne possono essere determinati chiamando `row.Schema`:

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

Questo approccio consente toobuild un outputter flessibile per qualsiasi schema dei metadati.

Hello dati di output viene scritto toofile utilizzando `System.IO.StreamWriter`. parametro di flusso Hello è impostato troppo`output.BaseStrea` come parte di `IUnstructuredWriter output`.

Si noti che il file toohello buffer di tooflush importante hello dati dopo ogni iterazione di riga. Inoltre, hello `StreamWriter` oggetto deve essere utilizzato con hello Disposable attributo abilitato (impostazione predefinita) e con hello **utilizzando** (parola chiave):

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

In alternativa, chiamare il metodo Flush() in modo esplicito dopo ogni iterazione, Illustrare nell'esempio seguente hello.

### <a name="set-headers-and-footers-for-user-defined-outputter"></a>Impostare intestazioni e piè di pagina per l'outputter definito dall'utente
tooset un'intestazione, utilizzare il flusso di esecuzione singola iterazione.

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

Hello codice hello innanzitutto `if (isHeaderRow)` blocco viene eseguito una sola volta.

Per il piè di pagina hello, utilizzare hello riferimento toohello istanza `System.IO.Stream` oggetto (`output.BaseStream`). Scrivere un piè di pagina hello in hello metodo Close () di hello `IOutputter` interfaccia.  (Per ulteriori informazioni, vedere hello di esempio seguente).

Di seguito è riportato un esempio di outputter definito dall'utente:

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

Ecco lo script U-SQL di base:

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

Questo è un outputter HTML che crea un file HTML con dati di tabella.

### <a name="call-outputter-from-u-sql-base-script"></a>Chiamare l'outputter dallo script U-SQL di base
toocall un outputter personalizzato dallo script U-SQL di base hello, hello nuova istanza dell'oggetto outputter hello presenta toobe creato.

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

creazione di un'istanza di hello tooavoid oggetto nello script di base, è possibile creare un wrapper di funzione, come illustrato nell'esempio precedente:

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

In questo caso, la chiamata originale hello aspetto hello seguenti:

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a>Usare elaboratori definiti dall'utente
Processore definito dall'utente o UDP, è un tipo di operatore definito dall'utente U-SQL che consente le righe in ingresso di hello tooprocess applicando le funzionalità di programmabilità. UDP consente toocombine colonne, modificare i valori e aggiungere nuove colonne, se necessario. In pratica, è utile tooprocess gli elementi di dati tooproduce richiesto un set di righe.

toodefine UDP, è necessario toocreate un `IProcessor` interfaccia con hello `SqlUserDefinedProcessor` attributo, che è facoltativo per UDP.

Questa interfaccia deve contenere la definizione di hello per hello `IRow` interfaccia rowset esegue l'override, come illustrato nell'esempio seguente hello:

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

**SqlUserDefinedProcessor** indica che il tipo di hello deve essere registrato come un processore definito dall'utente. Questa classe non può essere ereditata.

attributo SqlUserDefinedProcessor Hello è **facoltativo** per la definizione di UDP.

gli oggetti di programmabilità principale Hello sono **input** e **output**. oggetto di input Hello è tooenumerate utilizzate colonne di input e output e tooset i dati di output come risultato dell'attività del processore hello.

Per l'enumerazione delle colonne di input, utilizziamo hello `input.Get` metodo.

```
string column_name = input.Get<string>("column_name");
```

parametro per Hello `input.Get` metodo è una colonna che viene passata come parte di hello `PRODUCE` clausola di hello `PROCESS` istruzione dello script di base hello U-SQL. È necessario toouse il tipo di dati corretto hello è qui.

Per l'output, utilizzare hello `output.Set` metodo.

È importante solo toonote che produttore personalizzato restituisce le colonne e i valori che sono definiti con hello `output.Set` chiamata al metodo.

```
output.Set<string>("mycolumn", mycolumn);
```

output di Hello effettiva del processore è attivato chiamando `return output.AsReadOnly();`.

Di seguito è riportato un esempio di elaboratore:

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

In questo scenario, in caso di utilizzo processore hello genera una nuova colonna denominata "full_description" combinando hello colonne esistenti, in questo caso, "user" in lettere maiuscole e "des". Inoltre, rigenera un GUID e restituisce i valori GUID hello originali e quello nuovi.

Come si può vedere dal hello precedente esempio, è possibile chiamare metodi c# durante `output.Set` chiamata al metodo.

Di seguito è riportato un esempio di script U-SQL di base che usa un elaboratore personalizzato:

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

## <a name="use-user-defined-appliers"></a>Usare oggetti di applicazione definiti dall'utente
Un oggetto di applicazione U-SQL definita dall'utente consente la funzione tooinvoke personalizzata in c# per ogni riga restituita dall'espressione di tabella esterna hello di una query. input di destra Hello viene valutata per ogni riga dall'input di sinistra hello e le righe di hello che sono state prodotte vengono combinate per l'output di hello finale. elenco di Hello colonne generate dall'operatore APPLY hello sono combinazione hello di set di hello di colonne a sinistra di hello e hello input di destra.

Oggetto di applicazione definito dall'utente viene richiamato come parte dell'espressione SELECT USQL hello.

Hello tipica chiamata toohello definito dall'utente dell'oggetto di applicazione ha un aspetto simile hello seguenti:

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

Per altre informazioni sull'uso di oggetti di applicazione in un'espressione SELECT, vedere [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx) (Selezione con SELECT di U-SQL da CROSS APPLY e OUTER APPLY).

definizione Hello definito dall'utente dell'oggetto di applicazione della classe base è la seguente:

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

toodefine un oggetto di applicazione definito dall'utente, è necessario hello toocreate `IApplier` interfaccia con hello [`SqlUserDefinedApplier`] attributo, che è facoltativo per una definizione di applicazione modifiche definite dall'utente.

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

* Applicare viene chiamato per ogni riga della tabella esterna hello. Restituisce hello `IUpdatableRow` set di righe di output.
* classe di costruttore Hello è oggetto di applicazione modifiche definite dall'utente di toopass utilizzati parametri toohello.

**SqlUserDefinedApplier** indica che il tipo di hello deve essere registrato come un oggetto di applicazione definito dall'utente. Questa classe non può essere ereditata.

**SqlUserDefinedApplier** è **facoltativo** per la definizione di un oggetto di applicazione definito dall'utente.


gli oggetti di programmabilità principale Hello sono i seguenti:

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

I set di righe di input vengono passati come input `IRow`. Hello righe di output vengono generate come `IUpdatableRow` interfaccia output.

Nomi delle singole colonne può essere determinati dal chiamante hello `IRow` metodo dello Schema.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

valori dei dati effettivi da hello in arrivo tooget hello `IRow`, viene utilizzato il metodo Get () hello di `IRow` interfaccia.

```
mycolumn = row.Get<int>("mycolumn")
```

O utilizziamo nome di colonna dello schema hello:

```
row.Get<int>(row.Schema[0].Name)
```

Hello valori di output devono essere impostati con `IUpdatableRow` output:

```
output.Set<int>("mycolumn", mycolumn)
```

È importante toounderstand appliers personalizzato output solo le colonne e i valori che sono definiti con `output.Set` chiamata al metodo.

output di Hello effettivo viene attivato chiamando `yield return output.AsReadOnly();`.

parametri di Hello definiti dall'utente dell'oggetto di applicazione possono essere passati toohello costruttore. Oggetto di applicazione può restituire un numero variabile di colonne che devono toobe definiti durante la chiamata dell'oggetto di applicazione di hello in base uno Script U-SQL.

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

Ecco hello definito dall'utente dell'oggetto di applicazione esempio:

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

Di seguito è script U-SQL base hello per questo oggetto di applicazione definito dall'utente:

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

In questo scenario di caso di utilizzo definiti dall'utente dell'oggetto di applicazione funge da un parser delimitato da virgole per auto hello flotta proprietà. le righe di file di input Hello aspetto hello seguenti:

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

Si tratta di un normale file con valori delimitati da tabulazioni (TSV) con una colonna di proprietà contenente le proprietà delle automobili, come marca e modello. Tali proprietà devono essere analizzati toohello le colonne della tabella. oggetto di applicazione Hello fornito consente inoltre toogenerate dinamico alcune proprietà in hello generare set di righe, in base a un parametro hello viene passato. È possibile generare tutte le proprietà o solo uno specifico set di proprietà.

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

oggetto di applicazione definito dall'utente Hello può essere chiamato come una nuova istanza dell'oggetto dell'oggetto di applicazione:

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

O con la chiamata di un metodo factory wrapper hello:

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a>Usare combinatori definiti dall'utente
Funzione di combinazione definita dall'utente o UDC, consente toocombine righe dal set di righe sinistro e destro, in base alla logica personalizzata. Il combinatore definito dall'utente viene usato con l'espressione COMBINE.

Viene richiamato una funzione di combinazione di espressioni COMBINARE hello che fornisce le informazioni necessarie su entrambi i set di righe input hello hello, raggruppamento di colonne, hello hello previsto schema di risultati e informazioni aggiuntive.

toocall una funzione di combinazione di uno script U-SQL di base, utilizziamo hello la seguente sintassi:

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

Per altre informazioni, vedere [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx) (Espressione COMBINE (U-SQL)).

toodefine una funzione di combinazione definita dall'utente, è necessario hello toocreate `ICombiner` interfaccia con hello [`SqlUserDefinedCombiner`] attributo, che è facoltativo per una definizione di funzione di combinazione definita dall'utente.

Definizione della classe `ICombiner` di base:

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

Hello implementazione personalizzata di un `ICombiner` interfaccia deve contenere la definizione di hello per un `IEnumerable<IRow>` combinare override.

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

Hello **SqlUserDefinedCombiner** attributo indica che il tipo di hello deve essere registrato come una funzione di combinazione definita dall'utente. Questa classe non può essere ereditata.

**SqlUserDefinedCombiner** è proprietà della modalità di combinazione canali hello toodefine utilizzato. È un attributo facoltativo per la definizione di un combinatore definito dall'utente.

Modalità     CombinerMode

Enumerazione CombinerMode può assumere hello seguenti valori:

* Full (0) di da che ogni riga di output dipende potenzialmente da tutte le righe di input hello sinistra e destra con hello stesso valore della chiave.

* A sinistra (1) ogni riga di output dipende da una singola riga di input da sinistra hello (e potenzialmente tutte le righe da hello destra con hello stesso valore della chiave).

* Right (2) ogni riga di output dipende da una singola riga di input da hello destra (e potenzialmente tutte le righe da sinistra hello con hello stesso valore della chiave).

* Riga interna (3) ogni riga di output dipende da un singolo input da sinistra e destra con hello stesso valore.

Esempio:     [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]


oggetti di programmabilità principale Hello sono:

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

I set di righe di input vengono passati come tipo di interfaccia `IRowset` a **sinistra** e a **destra**. Entrambi i set di righe devono essere enumerati per l'elaborazione. È solo possibile enumerare ogni interfaccia di una volta, sono tooenumerate e memorizzarlo nella cache se necessario.

Per la memorizzazione nella cache, è possibile creare un tipo di struttura di memoria List\<T\> come risultato dell'esecuzione di una query LINQ, specificamente List<`IRow`>. tipo di dati anonimi Hello può essere utilizzato durante l'enumerazione anche.

Vedere [introduzione tooLINQ query (c#)](https://msdn.microsoft.com/library/bb397906.aspx) per ulteriori informazioni sulle query LINQ, e [IEnumerable\<T\> interfaccia](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) per ulteriori informazioni su IEnumerable\<T\> interfaccia.

valori dei dati effettivi da hello in arrivo tooget hello `IRowset`, viene utilizzato il metodo Get () hello di `IRow` interfaccia.

```
mycolumn = row.Get<int>("mycolumn")
```

Nomi delle singole colonne può essere determinati dal chiamante hello `IRow` metodo dello Schema.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

O con nome di colonna dello schema hello:

```
c# row.Get<int>(row.Schema[0].Name)
```

Enumerazione generale di Hello con LINQ è simile hello seguenti:

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

Dopo l'enumerazione di entrambi i set di righe, verrà tooloop in tutte le righe. Per ogni riga nel set di righe a sinistra di hello, verrà toofind tutte le righe che soddisfano la condizione hello della funzione di combinazione.

Hello valori di output devono essere impostati con `IUpdatableRow` output.

```
output.Set<int>("mycolumn", mycolumn)
```

output di Hello effettivo viene attivato chiamando troppo`yield return output.AsReadOnly();`.

Di seguito è riportato un esempio di combinatore:

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

In questo scenario, in caso di utilizzo che si sta creando un report di analitica rivenditore hello. obiettivo di Hello è toofind tutti i prodotti che costano più di 20.000 $ e che vendono tramite sito Web di hello più veloce tramite rivenditore di regolare hello all'interno di un determinato periodo di tempo.

Di seguito è riportato uno script U-SQL di base hello. È possibile confrontare la logica di hello tra un JOIN normale e una funzione di combinazione:

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

Una funzione di combinazione definita dall'utente può essere chiamato come una nuova istanza dell'oggetto dell'oggetto di applicazione hello:

```
USING new MyNameSpace.MyCombiner();
```


O con la chiamata di un metodo factory wrapper hello:

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a>Usare riduttori definiti dall'utente

U-SQL consente toowrite riduttori di set di righe personalizzata in c# tramite framework di estendibilità di hello operatore definito dall'utente e l'implementazione di un'interfaccia IReducer.

Riduttore definito dall'utente o UDR, possono essere utilizzati tooeliminate le righe non necessarie durante l'estrazione di dati (importazione). Inoltre può essere utilizzato toomanipulate e valutare le righe e colonne. In base alla logica di programmazione, inoltre possibile definire quali righe devono toobe estratti.

una classe UDR toodefine, dobbiamo toocreate un `IReducer` interfaccia con un parametro facoltativo `SqlUserDefinedReducer` attributo.

Questa interfaccia di classe deve contenere una definizione per hello `IEnumerable` eseguire l'override di set di righe di interfaccia.

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

Hello **SqlUserDefinedReducer** attributo indica che il tipo di hello deve essere registrato come un riduttore definito dall'utente. Questa classe non può essere ereditata.
**SqlUserDefinedReducer** è un attributo facoltativo per la definizione di un riduttore definito dall'utente. Proprietà IsRecursive toodefine è utilizzato.

* bool     IsRecursive    
* **true**  = indica se il riduttore è idempotente

gli oggetti di programmabilità principale Hello sono **input** e **output**. oggetto di input Hello è tooenumerate utilizzato le righe di input. L'output è usato tooset righe di output in seguito a ridurre l'attività.

Per l'enumerazione delle righe di input, utilizziamo hello `Row.Get` metodo.

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

parametro per hello Hello `Row.Get` metodo è una colonna che viene passata come parte di hello `PRODUCE` classe di hello `REDUCE` istruzione dello script di base hello U-SQL. È necessario toouse hello tipo di dati corretto qui anche.

Per l'output, utilizzare hello `output.Set` metodo.

È importante toounderstand che valori di output solo riduttore personalizzati che sono definiti con hello `output.Set` chiamata al metodo.

```
output.Set<string>("mycolumn", guid);
```

output di Hello riduttore effettivo viene attivato chiamando `yield return output.AsReadOnly();`.

Di seguito è riportato un esempio di riduttore:

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

In questo scenario, in caso di utilizzo riduttore hello ignora le righe con un nome utente vuoto. Per ogni riga nel set di righe, legge ogni colonna richiesta, quindi restituisce la lunghezza hello del nome utente hello. Restituisce la riga effettiva hello solo se lunghezza del valore nome utente è maggiore di 0.

Di seguito è riportato uno script U-SQL di base che usa un riduttore personalizzato:

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
