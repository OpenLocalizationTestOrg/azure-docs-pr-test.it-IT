---
title: "funzionalità di SQL Database JSON aaaAzure | Documenti Microsoft"
description: Database SQL di Azure permette di tooparse, query e dati in formato in notazione JavaScript Object Notation (JSON).
services: sql-database
documentationcenter: 
author: jovanpop-msft
manager: jhubbard
editor: 
ms.assetid: 55860105-2f5f-4b10-87a0-99faa32b5653
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.date: 11/15/2016
ms.author: jovanpop
ms.workload: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 30a31a1b01482ec276646b6fd6ca0c1f581168d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-json-features-in-azure-sql-database"></a>Introduzione alle funzionalità JSON nel database SQL di Azure
Il database SQL di Azure consente di analizzare ed eseguire query sui dati rappresentati in formato JavaScript Object Notation [(JSON)](http://www.json.org/) e di esportare i dati relazionali come testo JSON.

JSON è un formato di dati diffuso usato per scambiare dati nelle moderne applicazioni Web e per dispositivi mobili. JSON è usato anche per archiviare dati semistrutturati nei file di log o nei database NoSQL come [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/). Molti servizi Web REST restituiscono risultati formattati come testo JSON o accettano dati formattati come JSON. La maggior parte dei servizi di Azure come [Ricerca di Azure](https://azure.microsoft.com/services/search/), [Archiviazione di Azure](https://azure.microsoft.com/services/storage/) e [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) presentano endpoint REST che restituiscono o usano JSON.

Il database SQL di Azure consente di lavorare facilmente con dati JSON e integrare il database con i servizi moderni.

## <a name="overview"></a>Panoramica
Database SQL di Azure fornisce hello seguenti funzioni per l'utilizzo con i dati JSON:

![Funzioni di JSON](./media/sql-database-json-features/image_1.png)

Se si dispone di testo JSON, è possibile estrarre dati da JSON o verificare che JSON viene formattato correttamente tramite le funzioni predefinite di hello [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), e [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx) . Hello [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) funzione consente di aggiornare valore all'interno del testo JSON. Per query e analisi più avanzate, la funzione [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) può trasformare un array di oggetti JSON in un set di righe. Qualsiasi query SQL può essere eseguito in hello restituito set di risultati. Infine, è disponibile una clausola [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) che consente di formattare i dati archiviati nelle tabelle relazionali come testo JSON.

## <a name="formatting-relational-data-in-json-format"></a>Formattazione di dati relazionali in formato JSON
Se si dispone di un servizio web che richiede dati dal database hello dei livelli e fornisce una risposta in JSON formattare o sul lato client Framework o librerie JavaScript che accettano dati formattati come JSON, è possibile formattare il contenuto del database nel formato JSON direttamente in una query SQL. Non sono più codice di applicazione toowrite che formatta i risultati dal Database di SQL Azure come JSON, o includere alcuni risultati delle query tabulari tooconvert libreria serializzazione JSON e quindi serializzare formato tooJSON oggetti. In alternativa, è possibile utilizzare hello dei risultati della query SQL tooformat clausola JSON in formato JSON in Database SQL di Azure e utilizzarlo direttamente nell'applicazione.

Nell'esempio seguente di hello, le righe dalla tabella Sales. Customer hello sono formattate come JSON tramite la clausola FOR JSON hello:

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

clausola FOR JSON PATH Hello formatta i risultati di hello di hello query come testo JSON. I nomi di colonna vengono utilizzati come chiavi, mentre i valori delle celle hello vengono generati come valori JSON:

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

set di risultati Hello viene formattato come matrice JSON in cui ogni riga viene formattato come un oggetto JSON separato.

PERCORSO indica che è possibile personalizzare il formato di output hello il risultato JSON tramite la notazione del punto nell'alias di colonna. Ciao seguente query cambia hello nome della chiave "CustomerName" hello in formato JSON output di hello e inserisce i numeri di telefono e fax in hello "Contact" sotto-oggetto:

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

output di Hello di questa query è simile al seguente:

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

In questo esempio viene restituito un singolo oggetto JSON invece di una matrice specificando hello [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) opzione. È possibile usare questa opzione se è noto che si sta restituendo un oggetto singolo come risultato della query.

valore principale Hello hello clausola FOR JSON è che consente di restituire i dati gerarchici complessi dal database formattato come oggetti JSON annidati o matrici. Hello nel seguente esempio viene illustrato come tooinclude ordini appartenenti a clienti toohello come una matrice annidata di ordini:

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

Anziché inviare i dati dei clienti tooget query separate e quindi toofetch un elenco di ordini correlati, è possibile ottenere tutti i dati necessari hello con una singola query, come illustrato nel seguente esempio di output di hello:

```
{
  "Name":"Nada Jovanovic",
  "Phone":"(215) 555-0100",
  "Fax":"(215) 555-0101",
  "Orders":[
    {"OrderID":382,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":395,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":1657,"OrderDate":"2013-01-31","ExpectedDeliveryDate":"2013-02-01"}
]
}
```

## <a name="working-with-json-data"></a>Uso dei dati JSON
Se non è rigorosamente strutturato di dati, se si dispone di oggetti secondari complessi, matrici o i dati gerarchici, o se le strutture di dati cambiano nel tempo, il formato JSON hello consentono toorepresent qualsiasi struttura di dati complessi.

JSON è un formato testuale che può essere usato come qualsiasi altro tipo di stringa nel database SQL di Azure. È possibile inviare o archiviare i dati JSON come NVARCHAR standard:

```
CREATE TABLE Products (
  Id int identity primary key,
  Title nvarchar(200),
  Data nvarchar(max)
)
go
CREATE PROCEDURE InsertProduct(@title nvarchar(200), @json nvarchar(max))
AS BEGIN
    insert into Products(Title, Data)
    values(@title, @json)
END
```

Hello dati JSON utilizzati in questo esempio è rappresentato con tipo di hello nvarchar (max). JSON può essere inserita in questa tabella o fornito come argomento di routine di hello archiviato utilizzando la sintassi Transact-SQL standard, come illustrato nell'esempio seguente hello:

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

Qualsiasi lingua o raccolta client-side compatibile con i dati della stringa nel database SQL di Azure è compatibile anche con i dati JSON. JSON possono essere archiviati in qualsiasi tabella che supporta i tipi NVARCHAR di hello, ad esempio una tabella con ottimizzazione per la memoria o una tabella con controllo delle versioni del sistema. JSON non introduce alcun vincolo nel codice sul lato client hello o nel livello di database hello.

## <a name="querying-json-data"></a>Query sui dati JSON
Se si dispone di dati formattati come JSON archiviati in tabelle SQL di Azure, le funzioni JSON consentono di usare i dati in qualsiasi query SQL.

Le funzioni JSON disponibili nel database SQL di Azure consentono di trattare i dati formattati come JSON come qualsiasi altro tipo di dati SQL. È facilmente possibile estrarre i valori dal testo JSON hello e utilizzare i dati JSON in qualsiasi query:

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

funzione JSON_VALUE Hello estrae un valore dal testo JSON è archiviato nella colonna di dati hello. Questa funzione utilizza tooreference un percorso di tipo JavaScript valore tooextract testo JSON. il valore di Hello estratto può essere utilizzato in qualsiasi parte della query SQL.

funzione JSON_QUERY Hello è tooJSON_VALUE simile. A differenza di JSON_VALUE, questa funzione estrae l'oggetto secondario complesso, ad esempio array o oggetti che vengono inseriti nel testo JSON.

funzione JSON_MODIFY Hello consente di specificare il percorso di hello del valore di hello in testo JSON hello che deve essere aggiornato, nonché un nuovo valore sovrascriverà hello precedente. In questo modo è possibile aggiornare facilmente testo JSON senza vuoti intera struttura hello.

Poiché JSON è archiviato in un testo standard, non vi sono garanzie che sono formattati correttamente i valori di hello archiviati nelle colonne di testo. È possibile verificare che il testo archiviato nella colonna JSON sia formattato correttamente utilizzando standard i vincoli check di Database SQL di Azure e la funzione ISJSON hello:

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

Se il testo di input hello è formattato correttamente JSON, hello funzione ISJSON restituisce il valore di hello 1. A ogni inserimento o aggiornamento della colonna JSON, questo vincolo verificherà che nuovo valore di testo non sia un formato JSON non corretto.

## <a name="transforming-json-into-tabular-format"></a>Trasformazione del formato JSON in formato tabulare
Il database SQL di Azure consente anche di trasformare gli insiemi JSON in formato tabulare e di caricare o eseguire query sui dati JSON.

OPENJSON è una funzione con valori di tabella che analizza il testo JSON, individua una matrice di oggetti JSON, scorre hello gli elementi della matrice hello e restituisce una riga nel risultato di output di hello per ogni elemento della matrice hello.

![JSON tabulare](./media/sql-database-json-features/image_2.png)

Nell'esempio hello sopra, è possibile specificare dove toolocate hello matrice JSON che deve essere aperte (in $ hello. Il percorso di ordini), le colonne devono essere restituite come risultato e dove toofind hello valori JSON che verranno restituiti come celle.

È possibile trasformare una matrice JSON in hello @orders variabile in un set di righe, analizzare il set di risultati o inserire righe in una tabella standard:

```
CREATE PROCEDURE InsertOrders(@orders nvarchar(max))
AS BEGIN

    insert into Orders(Number, Date, Customer, Quantity)
    select Number, Date, Customer, Quantity
    OPENJSON (@orders)
     WITH (
            Number varchar(200),
            Date datetime,
            Customer varchar(200),
            Quantity int
     )

END
```
raccolta di Hello di ordini formattato come matrice JSON e fornito come una stored procedure toohello archiviato parametro può essere analizzata e inserita nella tabella Orders hello.

## <a name="next-steps"></a>Passaggi successivi
toolearn come toointegrate JSON nell'applicazione, vedere queste risorse:

* [Blog di TechNet](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [Documentazione di MSDN](https://msdn.microsoft.com/library/dn921897.aspx)
* [Video di Channel 9](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

toolearn sui vari scenari per l'integrazione JSON nell'applicazione, vedere demo hello in questo [video di Channel 9](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) o trovare uno scenario che corrisponde al caso di utilizzo in [post di Blog JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).

