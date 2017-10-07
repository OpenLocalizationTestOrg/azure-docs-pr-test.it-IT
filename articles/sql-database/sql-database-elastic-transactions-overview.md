---
title: aaaDistributed transazioni tra database cloud
description: Panoramica delle transazioni di database elastico con il database SQL di Azure
services: sql-database
documentationcenter: 
author: torsteng
manager: jhubbard
editor: torsteng
ms.assetid: e14df7a3-7788-4cfb-bcd1-7ad6433ef1f9
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: sql-database
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 9a18f2749108d337bf115b3dc21dd0c7828dd9c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="distributed-transactions-across-cloud-databases"></a>Transazioni distribuite in database cloud
Le transazioni di database elastico per il Database SQL di Azure (database SQL) consentono toorun transazioni che si estendono su più database nel database di SQL Server. Le transazioni di database elastico per il database SQL sono disponibili per le applicazioni .NET tramite ADO .NET e integrate con hello familiarità esperienza di programmazione utilizzando hello [System. Transaction](https://msdn.microsoft.com/library/system.transactions.aspx) classi. libreria di hello tooget, vedere [.NET Framework 4.6.1 (Web Installer)](https://www.microsoft.com/download/details.aspx?id=49981).

In locale questo scenario richiede in genere l'esecuzione di Microsoft Distributed Transaction Coordinator (MSDTC). Poiché MSDTC non è disponibile per l'applicazione Platform-as-a-Service in Azure, transazioni toocoordinate distributed possibilità di hello è ora stato integrato direttamente nel database di SQL Server. Le applicazioni possono connettersi le transazioni toolaunch distribuita di Database SQL tooany e uno dei database hello verrà coordinare in modo trasparente la transazione distribuita hello, come illustrato nella seguente illustrazione hello. 

  ![Transazioni distribuite con il database SQL di Azure tramite transazioni di database elastico ][1]

## <a name="common-scenarios"></a>Scenari comuni
Le transazioni di database elastico per il database SQL di abilitare applicazioni toomake modifiche specifiche toodata archiviato in diversi database SQL. Anteprima di Hello è incentrata sul lato client di sviluppo in c# e .NET. Un'esperienza sul lato server con T-SQL è prevista per un momento successivo.  
Hello di database elastico transazioni destinazioni seguenti scenari:

* Applicazioni con più database in Azure: con questo scenario i dati sono partizionati verticalmente in più database nel database SQL, in modo che diversi tipi di dati risiedano in database diversi. Alcune operazioni sono necessarie modifiche toodata che viene mantenuto in due o più database. un'applicazione Hello utilizza le modifiche di database elastico transazioni toocoordinate hello tra database e garantire l'atomicità.
* Applicazioni di database partizionato in Azure: con questo scenario, il livello di dati hello utilizza hello [libreria client di Database elastico](sql-database-elastic-database-client-library.md) o partizionamento orizzontale automatico toohorizontally partizionare i dati hello tra molti database nel database di SQL Server. Un caso di utilizzo principali è hello necessità tooperform atomica delle modifiche per un'applicazione multi-tenant partizionata quando le modifiche span tenant. Si pensi ad esempio un trasferimento da un unico tenant tooanother, sia che si trovano in database diversi. Un secondo caso è partizionamento orizzontale granulari per le esigenze di capacità tooaccommodate per un tenant di grandi dimensioni che a sua volta in genere implica che alcune toostretch esigenze di operazioni atomiche su più database utilizzati per hello stesso tenant. Un terzo caso è dati tooreference aggiornamenti atomici che vengono replicati tra database. Operazioni atomiche, transazionali, falsariga possono ora essere coordinate tra diversi database utilizzando anteprima hello.
  Le transazioni di database elastico utilizzano atomicità transazione di commit in due fasi tooensure tra database. È una scelta ideale per le transazioni che coinvolgono meno di 100 database alla volta in una singola transazione. Questi limiti non vengono applicati, ma uno aspettarsi prestazioni e le percentuali di successo per toosuffer le transazioni di database elastico quando supera questi limiti.

## <a name="installation-and-migration"></a>Installazione e migrazione
funzionalità di Hello per le transazioni di database elastico in database di SQL Server sono fornite tramite le librerie .NET toohello aggiornamenti System.Data.dll e System.Transactions.dll. Hello DLL assicurarsi che il protocollo 2PC viene utilizzato laddove necessario tooensure atomicità. installare toostart lo sviluppo di applicazioni utilizzando le transazioni di database elastici, [.NET Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981) o versione successiva. Quando si esegue in una versione precedente di .NET framework di hello, transazioni non riusciranno toopromote tooa distribuita transaction e verrà generata un'eccezione.

Dopo l'installazione, è possibile utilizzare la transazione distribuita hello API in System. Transactions con connessioni tooSQL DB. Se si dispone di applicazioni di MSDTC utilizzano queste API, semplicemente ricompilare le applicazioni esistenti in .NET 4.6 dopo l'installazione di hello 4.6.1 Framework. Se i progetti destinati a .NET 4.6, verrà utilizzato automaticamente DLL hello aggiornato dalla nuova versione del Framework hello e chiamate API di transazione distribuita in combinazione con le connessioni tooSQL che DB avranno ora esito positivo.

Tenere presente che le transazioni di database elastico non richiedono l'installazione di MSDTC. Al contrario, le transazioni di database elastico sono gestite direttamente e internamente dal database SQL. Ciò semplifica notevolmente scenari cloud poiché una distribuzione di MSDTC non è necessario toouse distribuita transazioni con database di SQL Server. Sezione 4 viene illustrato in dettaglio come hello e le transazioni di database elastico toodeploy richiesto .NET framework con il tooAzure applicazioni cloud.

## <a name="development-experience"></a>Esperienza di sviluppo
### <a name="multi-database-applications"></a>Applicazioni con più database
Hello codice di esempio seguente usa esperienza di programmazione familiare hello con .NET System. Transactions. classe TransactionScope Hello stabilisce una transazione di ambiente in .NET. (Una "transazione di ambiente" è quello che si trova nel thread corrente hello.) Tutte le connessioni aperte all'interno di hello TransactionScope partecipano a transazioni hello. Se fa parte di un database diverso, transazione hello è automaticamente con privilegi elevati tooa distribuita transaction. risultato di Hello della transazione hello è controllata dall'impostazione hello ambito toocomplete tooindicate un commit.

    using (var scope = new TransactionScope())
    {
        using (var conn1 = new SqlConnection(connStrDb1))
        {
            conn1.Open();
            SqlCommand cmd1 = conn1.CreateCommand();
            cmd1.CommandText = string.Format("insert into T1 values(1)");
            cmd1.ExecuteNonQuery();
        }

        using (var conn2 = new SqlConnection(connStrDb2))
        {
            conn2.Open();
            var cmd2 = conn2.CreateCommand();
            cmd2.CommandText = string.Format("insert into T2 values(2)");
            cmd2.ExecuteNonQuery();
        }

        scope.Complete();
    }

### <a name="sharded-database-applications"></a>Applicazioni di database partizionato
Le transazioni di database elastico per il database SQL supportano inoltre coordinare le transazioni distribuite in cui utilizzare hello OpenConnectionForKey metodo hello elastico client libreria tooopen di connessioni di database per i dati di scalabilità livello. Considerare i casi in cui è necessario tooguarantee la consistenza delle transazioni per le modifiche tra i diversi valori di chiave di partizionamento orizzontale diverso. Partizioni toohello connessioni hosting valori di chiave di partizionamento orizzontale diversi hello sono negoziate utilizzando OpenConnectionForKey. Nel caso generale hello, connessioni hello possono essere toodifferent partizioni in modo che garantire garanzie transazionale richiede una transazione distribuita. Questo approccio viene illustrato nell'esempio di codice seguente Hello. Si presuppone che una variabile denominata shardmap toorepresent usato dalla libreria client di database elastico hello eseguire il mapping di una partizione:

    using (var scope = new TransactionScope())
    {
        using (var conn1 = shardmap.OpenConnectionForKey(tenantId1, credentialsStr))
        {
            conn1.Open();
            SqlCommand cmd1 = conn1.CreateCommand();
            cmd1.CommandText = string.Format("insert into T1 values(1)");
            cmd1.ExecuteNonQuery();
        }

        using (var conn2 = shardmap.OpenConnectionForKey(tenantId2, credentialsStr))
        {
            conn2.Open();
            var cmd2 = conn2.CreateCommand();
            cmd2.CommandText = string.Format("insert into T1 values(2)");
            cmd2.ExecuteNonQuery();
        }

        scope.Complete();
    }


## <a name="net-installation-for-azure-cloud-services"></a>Installazione di .NET per i servizi cloud di Azure
Azure offre diverse offerte di applicazioni .NET toohost. È disponibile in un confronto delle diverse offerte hello [servizio App di Azure, servizi Cloud e macchine virtuali confronto](../app-service-web/choose-web-site-cloud-service-vm.md). Se hello sistema operativo guest dell'offerta hello è inferiore a .NET 4.6.1 richiesto per le transazioni elastiche, è necessario too4.6.1 del sistema operativo guest di tooupgrade hello. 

Per i servizi di App di Azure, Aggiorna guest toohello che sistema operativo non è attualmente supportato. Macchine virtuali di Azure, è sufficiente accedere hello VM ed eseguire hello programma di installazione per .NET framework più recente di hello. Servizi Cloud di Azure, è necessario installazione di hello tooinclude di una versione più recente di .NET in attività di avvio hello della distribuzione. Hello concetti e le procedure sono documentate in [installare .NET su un ruolo del servizio Cloud](../cloud-services/cloud-services-dotnet-install-dotnet.md).  

Si noti che hello programma di installazione per .NET 4.6.1 potrebbe richiedere più spazio di archiviazione temporaneo durante l'avvio di processo nei servizi cloud Azure del programma di installazione per .NET 4.6 hello hello. tooensure una corretta installazione, è necessario tooincrease di archiviazione temporanea per il servizio cloud di Azure nel file servicedefinition. Csdef sezione LocalResources hello e le impostazioni di ambiente hello dell'attività di avvio, come illustrato nell'esempio hello esempio:

    <LocalResources>
    ...
        <LocalStorage name="TEMP" sizeInMB="5000" cleanOnRoleRecycle="false" />
        <LocalStorage name="TMP" sizeInMB="5000" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
        <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
            <Environment>
        ...
                <Variable name="TEMP">
                    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='TEMP']/@path" />
                </Variable>
                <Variable name="TMP">
                    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='TMP']/@path" />
                </Variable>
            </Environment>
        </Task>
    </Startup>

## <a name="transactions-across-multiple-servers"></a>Transazioni tra più server
Le transazioni di database elastici sono supportate in diversi server logici del database SQL di Azure. Quando le transazioni superano i limiti di server logico, i server che partecipa hello è innanzitutto necessario toobe immessi in una relazione di comunicazione reciproca. Una volta stabilita la relazione di comunicazione hello, qualsiasi database in uno dei due server può partecipare alle transazioni elastiche di database da hello hello altri server. Con le transazioni che si estende su più di due server logici, una relazione di comunicazione deve toobe sul posto per qualsiasi coppia di server logici.

Utilizzare hello relazioni di comunicazione tra server toomanage cmdlet PowerShell per le transazioni di database elastici seguenti:

* **Nuovo AzureRmSqlServerCommunicationLink**: utilizzare questo toocreate cmdlet una nuova relazione di comunicazione tra due server logico nel database di SQL Azure. relazione Hello è simmetrica, ovvero che entrambi i server possono avviare le transazioni con hello altri server.
* **Get-AzureRmSqlServerCommunicationLink**: utilizzare questo cmdlet tooretrieve la comunicazione esistente relazioni e le relative proprietà.
* **Remove-AzureRmSqlServerCommunicationLink**: utilizzare questo tooremove cmdlet una relazione di comunicazione. 

## <a name="monitoring-transaction-status"></a>Monitoraggio dello stato delle transazioni
Utilizzare viste a gestione dinamica (DMV) nel database di SQL Server toomonitor stato e l'avanzamento delle operazioni di database elastico in corso. Tootransactions correlati di tutte le viste a gestione dinamica sono rilevanti per le transazioni distribuite nel database di SQL Server. È possibile trovare hello corrispondente elenco di viste a gestione dinamica: [transazione correlati viste a gestione dinamica e funzioni (Transact-SQL)](https://msdn.microsoft.com/library/ms178621.aspx).

Queste viste a gestione dinamica sono particolarmente utili:

* **sys.dm\_tran\_active\_transactions**: elenca le transazioni attualmente attive e il relativo stato. Hello colonna UOW (Unit Of Work) consente di identificare hello figlio diverse transazioni appartenenti toohello stessa transazione distribuita. Tutte le transazioni all'interno di hello stessa transazione distribuita eseguire hello stesso valore UOW. Vedere hello [documentazione DMV](https://msdn.microsoft.com/library/ms174302.aspx) per altri dettagli.
* **Sys.dm\_tran\_database\_transazioni**: fornisce informazioni aggiuntive sulle transazioni, ad esempio la selezione della transazione hello log hello. Vedere hello [documentazione DMV](https://msdn.microsoft.com/library/ms186957.aspx) per altri dettagli.
* **Sys.dm\_tran\_blocchi**: fornisce informazioni sui blocchi hello che sono correntemente utilizzati dalle transazioni in corso. Vedere hello [documentazione DMV](https://msdn.microsoft.com/library/ms190345.aspx) per altri dettagli.

## <a name="limitations"></a>Limitazioni
Hello limitazioni seguenti attualmente si applica le transazioni di database tooelastic nel database di SQL Server:

* Sono supportate solo le transazioni tra database nel database SQL. Altri provider di risorse [X/Open XA](https://en.wikipedia.org/wiki/X/Open_XA) e database al di fuori del database SQL non possono partecipare alle transazioni di database elastico. Ciò significa che le transazioni di database elastico non possono estendersi in locale al database SQL Server e al database SQL di Azure. Per le transazioni distribuite in locale, continuare toouse MSDTC. 
* Sono supportate solo le transazioni coordinate tramite client da un'applicazione .NET. Il supporto sul lato server per T-SQL, ad esempio BEGIN DISTRIBUTED TRANSACTION, è pianificato, ma non ancora disponibile. 
* Le transazioni tra i servizi WCF non sono supportate. Ad esempio, si dispone di un metodo del servizio WCF che esegue una transazione. Inclusione hello chiamata all'interno di un ambito di transazione avrà esito negativo come una [ProtocolException](https://msdn.microsoft.com/library/system.servicemodel.protocolexception).

## <a name="next-steps"></a>Passaggi successivi
Per domande, rivolgersi toous su hello [forum di Database SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) e per le richieste di funzionalità, aggiungerli toohello [forum sul feedback su Database SQL](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-transactions-overview/distributed-transactions.png



