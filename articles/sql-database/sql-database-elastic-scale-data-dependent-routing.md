---
title: aaaData dipendente routing con il Database SQL di Azure | Documenti Microsoft
description: "Come toouse hello ShardMapManager classe nelle applicazioni .NET per una funzionalità di database partizionati nel Database di SQL Azure routing dipendente dai dati"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: cad09e15-5561-4448-aa18-b38f54cda004
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: ddove
ms.openlocfilehash: 34014508ae01905686791fe096bb275cb84f53b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-dependent-routing"></a>Routing dipendente dei dati
**Routing dipendente dai dati** hello possibilità toouse hello dati in un query tooroute hello richiesta tooan database appropriato. Questo costituisce un criterio fondamentale quando si usano database partizionati. contesto della richiesta Hello può essere richiesta hello tooroute utilizzato, soprattutto se la chiave di partizionamento orizzontale hello non fa parte di query hello. Ogni query specifica o la transazione in un'applicazione che utilizza il routing dipendente dai dati è limitato tooaccessing un singolo database per ogni richiesta. Strumenti di Azure SQL Database elastico hello, questo ciclo viene eseguito con hello  **[ShardMapManager classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)**  nelle applicazioni ADO.NET.

un'applicazione Hello non è necessario tootrack diverse stringhe di connessione o percorsi DB associati a diversi intervalli di dati nell'ambiente partizionato hello. In alternativa, hello [gestore mappe partizioni](sql-database-elastic-scale-shard-map-management.md) apre le connessioni toohello database corretti quando necessario, in base ai dati hello mappa partizioni hello e il valore di hello della chiave di partizionamento orizzontale hello hello destinazione della richiesta dell'applicazione hello. chiave di Hello è in genere hello *customer_id*, *tenant_id*, *date_key*, o un altro identificatore specifico che è un parametro di richiesta di database hello fondamentale). 

Per altre informazioni, vedere la pagina relativa [all'aumento del numero di istanze di SQL Server con il routing dipendente dai dati](https://technet.microsoft.com/library/cc966448.aspx).

## <a name="download-hello-client-library"></a>Scaricare la libreria client di hello
classe hello tooget, installare hello [libreria Client di Database elastico](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). 

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a>Uso di ShardMapManager in un'applicazione di routing dipendente dai dati
Le applicazioni devono creare un'istanza di hello **ShardMapManager** durante l'inizializzazione, tramite chiamata factory hello  **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**. In questo esempio, viene eseguita l'inizializzazione sia di **ShardMapManager** che una **ShardMap** specifica in essa contenuta. In questo esempio mostra hello GetSqlShardMapManager e [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) metodi.

    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, 
                      ShardMapManagerLoadPolicy.Lazy);
    RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 

### <a name="use-lowest-privilege-credentials-possible-for-getting-hello-shard-map"></a>Utilizzare credenziali con privilegi più basse possibile per ottenere una mappa partizioni hello
Se un'applicazione non è la manipolazione dei mappa partizioni hello stesso, le credenziali di hello utilizzate nel metodo factory hello devono disporre di autorizzazioni solo di sola lettura in hello **globale mappa partizioni** database. Queste credenziali sono solitamente diverse da gestore mappe partizioni di credenziali utilizzate tooopen connessioni toohello. Vedere anche [utilizzate le credenziali della libreria client di Database elastico hello tooaccess](sql-database-elastic-scale-manage-credentials.md). 

## <a name="call-hello-openconnectionforkey-method"></a>Chiamare il metodo OpenConnectionForKey hello
Hello  **[ShardMap.OpenConnectionForKey metodo](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)**  restituisce una connessione ADO.Net pronto per il rilascio di comandi toohello appropriate del database in base al valore di hello di hello **chiave**parametro. Informazioni di partizione memorizzati nella cache in un'applicazione hello hello **ShardMapManager**, pertanto queste richieste non in genere dovuti a una ricerca di database in hello **globale mappa partizioni** database. 

    // Syntax: 
    public SqlConnection OpenConnectionForKey<TKey>(
        TKey key,
        string connectionString,
        ConnectionOptions options
    )


* Hello **chiave** parametro viene utilizzato come chiave di ricerca nel database appropriato di hello partizioni mappa toodetermine hello per richiesta hello. 
* Hello **connectionString** è toopass utilizzate solo le credenziali utente hello per connessione hello desiderato. Nessun nome di database o server sono inclusi in questo *connectionString* poiché il metodo hello determinerà database hello e server mediante hello **ShardMap**. 
* Hello  **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)**  deve essere impostato troppo**ConnectionOptions.Validate** può modificare un ambiente in cui esegue il mapping di partizione e righe possono spostare i database tooother un risultato di operazioni di divisione o di unione. L'operazione comporta una mappa di partizioni locale toohello breve query nel database di destinazione hello (non mappa partizioni globale toohello) prima della connessione hello viene recapitato toohello applicazione. 

Se la convalida di hello rispetto a mappa di partizioni locale hello non riesce (che indica che non è corretta della cache di hello), hello gestore mappe partizioni richiederà hello partizioni globale mappa tooobtain hello nuovo valore corretto per la ricerca di hello, aggiornare la cache di hello e ottenere e restituiscono hello connessione al database appropriato. 

Usare **ConnectionOptions.None** solo se non sono previste modifiche al mapping delle partizioni mentre l'applicazione è online. In tal caso, i valori memorizzati nella cache di hello possano presupporre tooalways sia corretto e database di destinazione toohello chiamata hello convalida completa il round trip aggiuntivo può essere ignorata in modo sicuro. Ciò riduce il traffico del database. Hello **connectionOptions** può essere impostato tramite un valore in un tooindicate di file di configurazione anche se sono previste modifiche di partizionamento orizzontale o meno eseguito durante un periodo di tempo.  

Questo esempio viene utilizzato il valore di hello di una chiave integer **CustomerID**, usando un **ShardMap** oggetto denominato **customerShardMap**.  

    int customerId = 12345; 
    int newPersonId = 4321; 

    // Connect toohello shard for that customer ID. No need toocall a SqlConnection 
    // constructor followed by hello Open method.
    using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId, 
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
    { 
        // Execute a simple command. 
        SqlCommand cmd = conn.CreateCommand(); 
        cmd.CommandText = @"UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID"; 

        cmd.Parameters.AddWithValue("@customerID", customerId); 
        cmd.Parameters.AddWithValue("@newPersonID", newPersonId); 
        cmd.ExecuteNonQuery(); 
    }  

Hello **OpenConnectionForKey** il metodo restituisce un nuovo database corretto toohello di connessione già aperta. Le connessioni usate in questo modo usufruiscono comunque del pool di connessioni ADO.Net. Fino a quando le transazioni e le richieste possono essere soddisfatti da una partizione alla volta, deve essere modifica solo hello necessaria in un'applicazione ADO.Net già in uso. 

Hello  **[OpenConnectionForKeyAsync metodo](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)**  disponibile anche se l'applicazione esegue la programmazione asincrona di utilizzo con ADO.Net. Il comportamento corrispondente non dati hello dipendenti routing equivalente di ADO. Del NET  **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)**  metodo.

## <a name="integrating-with-transient-fault-handling"></a>Integrazione con la gestione degli errori temporanei
Consigliata per lo sviluppo di applicazioni di accesso ai dati nel cloud hello è tooensure che gli errori temporanei vengono intercettati da app hello e che le operazioni di hello sono dopo diversi tentativi prima di generare un errore. La gestione degli errori temporanei per le applicazioni cloud è illustrata nella pagina relativa alla [gestione degli errori temporanei](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx). 

Gestione degli errori temporanei possono coesistere naturalmente con modello di Routing dipendente dai dati hello. il requisito principale Hello è tooretry richiesta di accesso tutti i dati hello inclusi hello **utilizzando** blocco ottenuto connessione di routing dipendente dai dati hello. esempio Hello precedente potrebbe essere riscritto come segue (notare modifiche evidenziato). 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a>Esempio: routing dipendente dai dati con gestione degli errori temporanei
<pre><code>int customerId = 12345; 
int newPersonId = 4321; 

<span style="background-color:  #FFFF00">Configuration.SqlRetryPolicy.ExecuteAction(() =&gt; </span> 
<span style="background-color:  #FFFF00">    { </span>
        // Connect toohello shard for a customer ID. 
        using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId,  
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
        { 
            // Execute a simple command 
            SqlCommand cmd = conn.CreateCommand(); 

            cmd.CommandText = @&quot;UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID&quot;; 

            cmd.Parameters.AddWithValue(&quot;@customerID&quot;, customerId); 
            cmd.Parameters.AddWithValue(&quot;@newPersonID&quot;, newPersonId); 
            cmd.ExecuteNonQuery(); 

            Console.WriteLine(&quot;Update completed&quot;); 
        } 
<span style="background-color:  #FFFF00">    }); </span> 
</code></pre>


Pacchetti di gestione degli errori temporanei tooimplement necessarie vengono scaricati automaticamente quando si compila l'applicazione di esempio hello database elastico. I pacchetti sono disponibili anche separatamente nella pagina relativa al [blocco di applicazioni di gestione degli errori temporanei nella libreria Enterprise](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/). Usare la versione 6.0 o successiva. 

## <a name="transactional-consistency"></a>Coerenza delle transazioni
Le proprietà di transazione vengono garantite per tutte le partizioni tooa locale di operazioni. Ad esempio, le transazioni inviate tramite il routing dipendente dai dati eseguito entro l'ambito di hello della partizione di destinazione hello per connessione hello. Al momento, non sono disponibili funzionalità per l'inserimento di più connessioni in una transazione e pertanto non esistono garanzie transazionale per le operazioni eseguite tra partizioni.

## <a name="next-steps"></a>Passaggi successivi
vedere toodetach una partizione o una partizione, tooreattach [utilizzando i problemi di mappa partizioni toofix classe RecoveryManager hello](sql-database-elastic-database-recovery-manager.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

