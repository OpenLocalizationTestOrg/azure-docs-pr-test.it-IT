---
title: aaaFix un errore di connessione SQL, errore temporaneo | Documenti Microsoft
description: 'Informazioni su come tootroubleshoot, diagnosticare ed evitare un errore di connessione SQL o temporanei nel Database di SQL Azure. '
keywords: "connessione sql,stringa di connessione,problemi di connettività,errore temporaneo,errore di connessione"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: efb35451-3fed-4264-bf86-72b350f67d50
ms.service: sql-database
ms.custom: develop apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: d225e610b9e88170ab53ca16d615bd07220603cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a>Risolvere, diagnosticare ed evitare gli errori di connessione SQL e gli errori temporanei per il database SQL
In questo articolo viene descritto come tooprevent, risolvere, diagnosticare e risolvere gli errori di connessione e gli errori temporanei che nell'applicazione client viene rilevato quando interagisce con il Database SQL di Azure. Informazioni su come tooconfigure la logica di riesecuzione, compilare la stringa di connessione hello e modificare altre impostazioni di connessione.

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a>Errori temporanei
Un errore temporaneo è un errore la cui causa sottostante si risolverà automaticamente in modo rapido. Una causa di errori temporanei occasionale è quando hello sistema Azure scorre rapidamente hardware risorse toobetter il bilanciamento del carico diversi carichi di lavoro. La maggior parte di questi eventi di riconfigurazione spesso viene completata in meno di 60 secondi. Durante questo intervallo di riconfigurazione, è possibile connettività problemi tooAzure Database SQL. Applicazioni che si connettono tooAzure Database SQL deve essere compilato tooexpect questi errori temporanei, li implementando la logica nel codice anziché superfici li toousers come errori dell'applicazione di tentativi di handle.

Se il programma client utilizza ADO.NET, il programma verrà comunicato sull'errore temporaneo hello da throw hello di un **SqlException**. Hello **numero** proprietà può essere confrontata con l'elenco di hello di errori temporanei parte superiore di hello di argomento hello: [codici di errore SQL per le applicazioni client di Database SQL](sql-database-develop-error-messages.md).

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a>Confronto tra connessione e comando
Si tentare la connessione a SQL hello oppure stabilire nuovamente, a seconda delle operazioni seguenti hello:

* **Si verifica un errore temporaneo durante un tentativo di connessione**: connessione hello deve essere riprovata dopo il ritardo per alcuni secondi.
* **Si verifica un errore temporaneo durante un comando di query SQL**: comando hello non deve essere riprovata immediatamente. Al contrario, dopo un ritardo, hello deve appena stabilire la connessione. È possibile ritentare quindi il comando hello.

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a>Logica di ripetizione dei tentativi per errori temporanei
I programmi client in cui occasionalmente si verifica un errore temporaneo sono più affidabili se contengono una logica di ripetizione dei tentativi.

Quando il programma comunica con il Database di SQL Azure tramite un middleware di parti 3rd, verificare con il fornitore hello se middleware hello contiene la logica di tentativi per errori temporanei.

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a>Principi per la ripetizione dei tentativi
* Se l'errore hello è temporaneo, è necessario riprovare un tooopen tentativo di una connessione.
* Non è consigliabile riprovare direttamente a eseguire un'istruzione SQL SELECT non riuscita con un errore temporaneo.
  
  * Al contrario, definire una nuova connessione e ripetere hello selezionare.
* Quando un'istruzione SQL UPDATE ha esito negativo con un errore temporaneo, una nuova connessione deve essere stabilita prima hello che nuovo tentativo di aggiornamento.
  
  * logica di riesecuzione Hello è necessario assicurarsi che transazione intero database hello completata o dell'intera transazione che hello viene eseguito il rollback.

#### <a name="other-considerations-for-retry"></a>Altre considerazioni per la ripetizione dei tentativi
* Un file batch che viene avviato automaticamente dopo l'orario di lavoro, e che verranno completati prima mattino, è possibile concedere toovery paziente con intervalli di tempo lunghi tra il numero di tentativi.
* Un programma dell'interfaccia utente devono tener conto hello tendenza umano toogive backup dopo troppo tempo di attesa.
  
  * Tuttavia, soluzione hello non deve essere tooretry ogni pochi secondi, perché tale criterio può riempire sistema hello con le richieste.

#### <a name="interval-increase-between-retries"></a>Incremento dell'intervallo tra i tentativi
È consigliabile attendere 5 secondi prima di riprovare. Nuovo tentativo dopo un ritardo inferiore a 5 secondi rischi in termini di servizio cloud di hello impegnativo. Per ogni tentativo successivo ritardo hello aumentino in modo esponenziale, backup tooa massimo di 60 secondi.

Una discussione di hello *il periodo di blocco* per i client che usano ADO.NET è disponibile in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).

È inoltre possibile tooset un numero massimo di tentativi prima della chiusura automatica dell'applicazione hello.

#### <a name="code-samples-with-retry-logic"></a>Esempi di codice con logica di ripetizione dei tentativi
Esempi di codice con logica di ripetizione dei tentativi in diversi linguaggi di programmazione sono disponibili in:

* [Raccolte di connessioni per database SQL e Server SQL](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a>Eseguire test sulla logica di ripetizione tentativi
tootest la logica di tentativi, è necessario simulare o provocare un errore che possono essere corretti, mentre il programma è ancora in esecuzione.

##### <a name="test-by-disconnecting-from-hello-network"></a>Per testare la disconnessione dalla rete hello
È possibile testare la logica di ripetizione è toodisconnect computer client da hello di rete durante l'esecuzione programma hello. Errore Hello sarà:

* **SqlException.Number** = 11001
* Messaggio: "Host sconosciuto"

Come parte di hello innanzitutto nuovo tentativo, il programma può correggere l'errore di ortografia hello e quindi tentare tooconnect.

toomake questo pratici, si scollega il computer dalla rete hello prima di avviare il programma. Quindi il programma riconosce un parametro runtime che causa hello programma:

1. Aggiungere temporaneamente 11001 tooits elenco di errori tooconsider come oggetto temporaneo.
2. Tentativo della prima connessione come di consueto.
3. Dopo aver hello viene rilevato l'errore, rimuovere 11001 dall'elenco di hello.
4. Visualizzare un messaggio che indica i computer di hello hello utente tooplug rete hello.
   * Sospendere l'esecuzione ulteriormente utilizzando entrambi hello **ReadLine** metodo o una finestra di dialogo con un pulsante OK. Hello utente preme hello INVIO dopo hello computer collegato in rete hello.
5. Tentare nuovamente tooconnect, prevede l'esito positivo.

##### <a name="test-by-misspelling-hello-database-name-when-connecting"></a>Test in base al nome di database hello errore di ortografia durante la connessione
Il programma può intenzionalmente in modo errato il nome utente hello prima il primo tentativo di connessione hello. Errore Hello sarà:

* **SqlException.Number** = 18456
* Messaggio: "Accesso non riuscito per l'utente 'WRONG_MyUserName'."

Come parte di hello innanzitutto nuovo tentativo, il programma può correggere l'errore di ortografia hello e quindi tentare tooconnect.

toomake questo pratica, il programma può riconoscere un parametro runtime che causa hello programma:

1. Aggiungere temporaneamente 18456 tooits elenco di errori tooconsider come oggetto temporaneo.
2. Aggiungere intenzionalmente nome utente di toohello 'WRONG_'.
3. Dopo aver hello viene rilevato l'errore, rimuovere 18456 dall'elenco di hello.
4. Rimuovere 'WRONG_' da nome utente hello.
5. Tentare nuovamente tooconnect, prevede l'esito positivo.

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a>Parametri di SqlConnection di .NET per nuovi tentativi di connessione
Se il programma client si connette tootooAzure Database SQL tramite la classe di .NET Framework hello **SqlConnection**, è necessario utilizzare .NET 4.6.1 o versioni successive (o .NET Core) in modo è possibile sfruttare la funzionalità di tentativi di connessione. I dettagli della funzionalità hello sono [qui](http://go.microsoft.com/fwlink/?linkid=393996).

<!--
2015-11-30, FwLink 393996 points toodn632678.aspx, which links tooa downloadable .docx related tooSqlClient and SQL Server 2014.
-->


Quando si compila hello [stringa di connessione](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) per il **SqlConnection** dell'oggetto, è necessario coordinare valori hello tra hello seguenti parametri:

* ConnectRetryCount &nbsp;&nbsp;*(Il valore predefinito è 1. L'intervallo consentito è tra 0 e 255.)*
* ConnectRetryInterval &nbsp;&nbsp;*(Il valore predefinito è 1 secondo. L'intervallo consentito è tra 1 e 60.)*
* Timeout di connessione &nbsp;&nbsp;*(Il valore predefinito è 15 secondi. L'intervallo consentito è tra 0 e 2147483647)*

In particolare, i valori scelti devono apportare hello seguente uguaglianza true:

* Timeout di connessione = ConnectRetryCount * ConnectionRetryInterval

Ad esempio, se hello count = 3 e l'intervallo = 10 secondi, un timeout di solo 29 secondi non abbastanza concederebbe sistema hello tempo sufficiente per il 3 e l'ultimo attendere e riprovare la connessione: 29 < 3 * 10.

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a>Confronto tra connessione e comando
Hello **ConnectRetryCount** e **ConnectRetryInterval** parametri consentono il **SqlConnection** hello tentativi oggetto operazione di connessione senza indicare o richiedere l'intervento del programma, ad esempio la restituzione tooyour programma del controllo. tentativi di Hello possono verificarsi nelle seguenti situazioni hello:

* Chiamata al metodo mySqlConnection.Open
* Chiamata al metodo mySqlConnection.Execute

È importante sottolineare che, Se si verifica un errore temporaneo durante la *query* è in esecuzione, il **SqlConnection** operazione di connessione non tentativi hello e certamente non ripetere la query dell'oggetto. Tuttavia, **SqlConnection** molto rapidamente controlli hello connessione prima di inviare la query per l'esecuzione. Se il controllo rapido hello rileva un problema di connessione, **SqlConnection** hello tentativi operazione di connessione. Se i tentativi di hello ha esito positivo, si eseguono query viene inviata per l'esecuzione.

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a>Opportunità di combinare ConnectRetryCount con la logica di ripetizione dei tentativi nell'applicazione
Si supponga che l'applicazione disponga di una logica di ripetizione dei tentativi particolarmente avanzata, È possibile ripetere hello operazione di connessione 4 volte. Se si aggiungono **ConnectRetryInterval** e **ConnectRetryCount** = stringa di connessione tooyour 3, si aumenterà hello tentativi conteggio too4 * 3 = 12 tentativi. Un numero così elevato di tentativi potrebbe non essere consigliabile.

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-tooazure-sql-database"></a>Connessioni tooAzure Database SQL
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a>Connessione: stringa di connessione
stringa di connessione Hello necessario per la connessione tooAzure Database SQL è leggermente diverso da stringa hello per la connessione tooMicrosoft SQL Server. È possibile copiare la stringa di connessione hello per il database da hello [portale di Azure](https://portal.azure.com/).

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a>Connessione: indirizzo IP
È necessario configurare hello Database di SQL server tooaccept comunicazione dall'indirizzo IP hello del computer hello che ospita il programma client. A tale scopo, la modifica delle impostazioni del firewall hello tramite hello [portale di Azure](https://portal.azure.com/).

Se si dimentica l'indirizzo IP tooconfigure hello, il programma avrà esito negativo con un messaggio di errore utile indicante l'indirizzo IP hello necessaria.

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

Per altre informazioni, vedere [Procedura: Configurare le impostazioni del firewall nel database SQL](sql-database-configure-firewall-settings.md)

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a>Connessione: porte
In genere è necessario solo che la porta 1433 è aperta per le comunicazioni in uscita, computer che ospita l'applicazione client si hello tooensure.

Ad esempio, quando il programma client è ospitato in un computer Windows, hello Windows Firewall nell'host di hello consente tooopen porta 1433:

1. Aprire Pannello di controllo hello
2. &gt; Tutti gli elementi del Pannello di controllo
3. &gt; Windows Firewall
4. &gt; Impostazioni avanzate
5. &gt; Regole in uscita
6. &gt; Azioni
7. &gt; Nuova regola

Se il programma client è ospitato in una macchina virtuale (VM) di Azure, vedere <br/>[Porte superiori a 1433 per ADO.NET 4.5 e il database SQL](sql-database-develop-direct-route-ports-adonet-v12.md).

Per informazioni generali sulla configurazione di porte e indirizzi IP, vedere [Firewall del database SQL di Azure](sql-database-firewall-configure.md)

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a>Connessione: ADO.NET 4.6.1
Se il programma utilizza le classi di ADO.NET come **SqlConnection** tooconnect tooAzure Database SQL, è consigliabile utilizzare .NET Framework versione 4.6.1 o versioni successive.

ADO.NET 4.6.1:

* Database SQL di Azure, è maggiore affidabilità quando si apre una connessione con hello **SqlConnection.Open** metodo. Hello **aprire** metodo incorpora una migliore meccanismi sforzo retry negli errori tootransient risposta, per alcuni errori entro il periodo di Timeout di connessione hello.
* Supporta il pool di connessioni, Sono inclusi una verifica efficiente che hello connessione oggetto offre il programma è in esecuzione.

Quando si utilizza un oggetto connessione da un pool di connessioni, è consigliabile che il programma chiudere temporaneamente connessione hello in uso non immediatamente. Aprire di nuovo una connessione non è dispendiosa è modo di hello creando una nuova connessione.

Se si sta utilizzando ADO.NET 4.0 o versioni precedenti, si consiglia di eseguire l'aggiornamento toohello ADO.NET più recente.

* A partire da novembre 2015, è possibile [scaricare ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a>Diagnostica
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a>Diagnostica: verificare se le utilità si possono connettere
Se il programma non riesce tooconnect tooAzure Database SQL, un'opzione di diagnostica è tooconnect tootry con un programma di utilità. In teoria utilità hello si connetterà utilizzando hello stessa libreria che utilizza il programma.

In qualsiasi computer Windows è possibile provare queste utilità:

* SQL Server Management Studio (ssms.exe), che si connette tramite ADO.NET.
* sqlcmd.exe, che si connette tramite [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).

Dopo la connessione, verificare il funzionamento di una breve query SQL SELECT.

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-hello-open-ports"></a>Diagnostica: Controllare le porte aperte hello
Si supponga che si ritiene che i tentativi di connessione hanno esito negativo a causa di problemi di tooport. Il computer è possibile eseguire un'utilità che consenta di segnalare le configurazioni delle porte hello.

In Linux hello utilità seguenti potrebbero risultare utili:

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * (Modifica hello esempio valore toobe l'indirizzo IP.)

In Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) può risultare utile. Ecco un'esecuzione di esempio che query situazione porta hello in un server di Database SQL di Azure e che è stato eseguito in un computer portatile:

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting tooresolve name tooIP address...
Name resolved too23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a>Diagnostica: registrare gli errori
La diagnosi di un problema intermittente è spesso agevolata dal rilevamento di uno schema generale nel corso di giorni o settimane.

Il client può supportare l'analisi tramite la registrazione di tutti gli errori rilevati. Potrebbe essere in grado di toocorrelate voci di log hello con i dati di errore di Database SQL di Azure stesso internamente.

Enterprise Library 6 (EntLib60) offre tooassist classi gestite .NET con la registrazione:

* [5 - come semplice come fallback disattivazione di un Log: utilizzando hello blocco applicazione per la registrazione](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a>Diagnostica: cercare errori nei log di sistema
Ecco alcune istruzioni Transact-SQL SELECT che eseguono query nei log alla ricerca di errori e di altre informazioni.

| Query di un log | Descrizione |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |Hello [Sys. event_log](http://msdn.microsoft.com/library/dn270018.aspx) Vista offre informazioni sui singoli eventi, inclusi alcuni che possono causare errori temporanei o gli errori di connettività.<br/><br/>In teoria è possibile correlare hello **start_time** o **end_time** valori con le informazioni quando il programma client si sono verificati problemi.<br/><br/>**Suggerimento:** è necessario connettersi toohello **master** database toorun questo. |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |Hello [Sys. database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) visualizzazione offre i conteggi aggregati di tipi di evento, per ulteriori operazioni di diagnostica.<br/><br/>**Suggerimento:** è necessario connettersi toohello **master** database toorun questo. |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-hello-sql-database-log"></a>Diagnostica: Ricerca gli eventi di problemi nel Registro di Database SQL di hello
È possibile cercare le voci relative a eventi problema nel registro eventi di hello del Database SQL di Azure. Provare a hello seguente istruzione Transact-SQL SELECT in hello **master** database:

```
SELECT
   object_name
  ,CAST(f.event_data as XML).value
      ('(/event/@timestamp)[1]', 'datetime2')                      AS [timestamp]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="error"]/value)[1]', 'int')             AS [error]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="state"]/value)[1]', 'int')             AS [state]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="is_success"]/value)[1]', 'bit')        AS [is_success]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="database_name"]/value)[1]', 'sysname') AS [database_name]
FROM
  sys.fn_xe_telemetry_blob_target_read_file('el', null, null, null) AS f
WHERE
  object_name != 'login_event'  -- Login events are numerous.
  and
  '2015-06-21' < CAST(f.event_data as XML).value
        ('(/event/@timestamp)[1]', 'datetime2')
ORDER BY
  [timestamp] DESC
;
```


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a>Alcune righe restituite da sys.fn_xe_telemetry_blob_target_read_file
Una riga restituita avrà un aspetto analogo al seguente. i valori null di Hello illustrati sono spesso non null in altre righe.

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a>Enterprise Library 6
Enterprise Library 6 (EntLib60) è un framework di classi .NET che consente di implementare un client affidabile di servizi cloud, uno dei quali è il servizio di Database SQL di Azure hello. È possibile individuare l'area tooeach dedicato di argomenti in cui EntLib60 può fornire supporto visitando prima:

* [Enterprise Library 6 - Aprile 2013](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

Logica di ripetizione dei tentativi per la gestione degli errori temporanei è un'area in cui EntLib60 può essere utile:

* [4 - perseverance, segreto del luogo tutti: utilizzando hello Transient Fault Handling Application Block](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> Hello codice sorgente per EntLib60 è disponibile per public [scaricare](http://go.microsoft.com/fwlink/p/?LinkID=290898). Microsoft non dispone di alcuna funzionalità di piani toomake ulteriori aggiornamenti o manutenzione aggiornamenti tooEntLib.
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a>Classi di EntLib60 per errori temporanei e ripetizione dei tentativi
le seguenti classi EntLib60 Hello sono particolarmente utile per la logica di ripetizione. Tutti questi sono in, o sotto, hello dello spazio dei nomi **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:

*Nello spazio dei nomi hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*

* **RetryPolicy**
  
  * **ExecuteAction**
* **ExponentialBackoff**
* **SqlDatabaseTransientErrorDetectionStrategy**
* **ReliableSqlConnection**
  
  * **ExecuteCommand**

Nello spazio dei nomi hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:

* **AlwaysTransientErrorDetectionStrategy**
* **NeverTransientErrorDetectionStrategy**

Di seguito sono collegamenti tooinformation su EntLib60:

* Libera [Download della Rubrica: tooMicrosoft Guida per gli sviluppatori Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)
* Procedure consigliate: [Indicazioni generali per la ripetizione di tentativi](../best-practices-retry-general.md) offre un'eccellente discussione approfondita della logica di ripetizione dei tentativi.
* Download NuGet di [Enterprise Library - Blocco applicazione per la gestione di errori temporanei 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-hello-logging-block"></a>EntLib60: blocco di registrazione hello
* blocco di registrazione Hello è una soluzione estremamente flessibile e configurabile che consente di:
  
  * Creare e archiviare messaggi di log in diverse posizioni.
  * Classificare e filtrare i messaggi.
  * Raccogliere informazioni contestuali utili per il debug e la traccia, oltre che per i requisiti di controllo e di registrazione generale.
* blocco registrazione Hello astrae hello la funzionalità di registrazione dalla destinazione del log hello in modo che il codice dell'applicazione hello è coerenza, indipendentemente dalla posizione hello e il tipo di archivio di registrazione di destinazione hello.

Per informazioni dettagliate, vedere: [5 - come semplice come fallback disattivazione di un Log: utilizzando hello blocco applicazione per la registrazione](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a>Codice sorgente del metodo IsTransient di EntLib60
Successivamente, da hello **SqlDatabaseTransientErrorDetectionStrategy** classe, è il codice sorgente c# hello per hello **IsTransient** metodo. codice sorgente Hello chiarisce gli errori sono stati considerati toobe temporaneo e richiedere un nuovo tentativo, a partire da aprile 2013.

Numerosi **//comment** righe sono state rimosse da questo leggibilità tooemphasize copia.

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in hello exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // hello service is currently busy. Retry hello request after 10 seconds.
            // Code: (reason code toobe decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode hello reason code from hello error message to
            // determine hello grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach hello decoded values as additional attributes to
            // hello original SQL exception.
            sqlException.Data[condition.ThrottlingMode.GetType().Name] =
              condition.ThrottlingMode.ToString();
            sqlException.Data[condition.GetType().Name] = condition;

            return true;

          case 10928:
          case 10929:
          case 10053:
          case 10054:
          case 10060:
          case 40197:
          case 40540:
          case 40613:
          case 40143:
          case 233:
          case 64:
            // DBNETLIB Error Code: 20
            // hello instance of SQL Server you attempted tooconnect to
            // does not support encryption.
          case (int)ProcessNetLibErrorCode.EncryptionNotSupported:
            return true;
        }
      }
    }
    else if (ex is TimeoutException)
    {
      return true;
    }
    else
    {
      EntityException entityException;
      if ((entityException = ex as EntityException) != null)
      {
        return this.IsTransient(entityException.InnerException);
      }
    }
  }

  return false;
}
```


## <a name="next-steps"></a>Passaggi successivi
* Per risolvere altri problemi di connessione Database SQL di Azure, visitare [connessione di risolvere i problemi tooAzure Database SQL](sql-database-troubleshoot-common-connection-issues.md).
* [Pool di connessioni di SQL Server (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [*Nuovo tentativo* è generica nuovo tentativo di libreria, scritta in una licenza di Apache 2.0 **Python**, attività hello toosimplify aggiunta toojust comportamento di ripetizione su un valore.](https://pypi.python.org/pypi/retrying)

