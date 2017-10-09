---
title: le prestazioni dell'applicazione Linux in OMS Log Analitica aaaCollect | Documenti Microsoft
description: Questo articolo fornisce informazioni dettagliate per la configurazione hello agente OMS per i contatori delle prestazioni di Linux toocollect per Apache HTTP Server e MySQL.
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 51105c6add5c7941a004570a76a4d94c02fc8a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="collect-performance-counters-for-linux-applications-in-log-analytics"></a>Raccogliere i contatori delle prestazioni per applicazioni Linux in Log Analytics 
Questo articolo fornisce informazioni dettagliate per la configurazione di hello [agente OMS per Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) toocollect contatori delle prestazioni per applicazioni specifiche.  le applicazioni di Hello incluse in questo articolo sono:  

- [MySQL](#MySQL)
- [Server HTTP Apache](#apache-http-server)

## <a name="mysql"></a>MySQL
Se il MySQL Server o MariaDB Server viene rilevato nel computer di hello quando viene installato l'agente OMS hello, verranno automaticamente installata un provider per il MySQL Server di monitoraggio delle prestazioni. Questo provider si connette toohello locale MySQL/MariaDB server tooexpose le statistiche sulle prestazioni. Le credenziali utente di MySQL devono essere configurate in modo che hello provider possa accedere hello MySQL Server.

### <a name="configure-mysql-credentials"></a>Configurare le credenziali di MySQL
Hello provider OMI MySQL richiede un utente di MySQL preconfigurato e installate le librerie client di MySQL in ordine tooquery hello informazioni sulle prestazioni e integrità dall'istanza di MySQL hello.  Queste credenziali vengono archiviate in un file di autenticazione che viene archiviato nell'agente Linux di hello.  file di autenticazione Hello specifica l'indirizzo di binding e l'istanza di MySQL hello porta è in ascolto e quali credenziali toouse toogather metriche.  

Durante l'installazione di hello agente OMS per Linux hello OMI MySQL provider analizzerà i file di configurazione my.cnf di MySQL (nei percorsi predefiniti) per indirizzo di binding e la porta e parzialmente hello set di file di autenticazione OMI MySQL.

file di autenticazione MySQL Hello è archiviato in `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`.


### <a name="authentication-file-format"></a>Formato del file di autenticazione
Di seguito è formato hello per hello file autenticazione OMI MySQL

    [Port]=[Bind-Address], [username], [Base64 encoded Password]
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    AutoUpdate=[true|false]

Nella hello nella tabella seguente sono descritte le voci di Hello nel file di autenticazione hello.

| Proprietà | Descrizione |
|:--|:--|
| Porta | Rappresenta hello di porta corrente hello MySQL istanza è in attesa. La porta 0 specifica proprietà hello seguenti vengono utilizzate per l'istanza predefinita. |
| Bind-address| Valore bind-address corrente di MySQL. |
| username| Istanza del server MySQL hello toomonitor toouse utilizzato l'utente di MySQL. |
| Password con codifica Base64| Password dell'utente di monitoraggio MySQL hello con codificata Base64. |
| AutoUpdate| Specifica se toorescan per le modifiche nel file my.cnf hello e sovrascrivere il file di autenticazione OMI MySQL hello quando hello Provider OMI MySQL è aggiornato. |

### <a name="default-instance"></a>Istanza predefinita
file di autenticazione OMI MySQL Hello è possibile definire un'istanza predefinita e toomake numero di porta la gestione di più istanze di MySQL in un singolo host Linux.  istanza predefinita di Hello è identificato da un'istanza con la porta 0. Tutte le istanze ereditano le proprietà impostate dall'istanza predefinita di hello, a meno che non si specificano valori diversi. Ad esempio, se viene aggiunto l'istanza di MySQL in ascolto sulla porta '3308', indirizzo di binding, username e password con codificata Base64 dell'istanza predefinita di hello verrà essere tootry utilizzato e monitorare hello istanza in ascolto sulla porta 3308. Se l'istanza di hello sulla porta 3308 è associata tooanother indirizzo e Usa hello stesso nome utente di MySQL è necessario password coppia solo hello indirizzo di binding e hello altre proprietà verrà ereditata.

Hello nella tabella seguente contiene le impostazioni di istanza di esempio 

| Descrizione | File |
|:--|:--|
| Istanza predefinita e istanza con porta 3308. | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=, ,`<br>`AutoUpdate=true` |
| Istanza predefinita e istanza con porta 3308 e nome e password diversi. | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=127.0.1.1, myuser2,cGluaGVhZA==`<br>`AutoUpdate=true` |


### <a name="mysql-omi-authentication-file-program"></a>Programma del file di autenticazione OMI MySQL
In installazione hello di hello OMI MySQL provider è incluso un programma del file autenticazione OMI MySQL che può essere file di autenticazione OMI MySQL hello tooedit utilizzato. programma del file autenticazione Hello è reperibile nella seguente posizione hello.

    /opt/microsoft/mysql-cimprov/bin/mycimprovauth

> [!NOTE]
> file delle credenziali Hello deve essere leggibile per l'account omsagent hello. È consigliabile eseguire comandi di hello mycimprovauth come omsgent.

Hello nella tabella seguente fornisce informazioni dettagliate sulla sintassi di hello per l'utilizzo mycimprovauth.

| Operazione | Esempio | Descrizione
|:--|:--|:--|
| autoupdate *false\|true* | mycimprovauth autoupdate false | Set di file di autenticazione hello o meno verrà aggiornate automaticamente nel riavviare o aggiornare. |
| default *bind-address nome utente password* | mycimprovauth default 127.0.0.1 root pwd | Set di hello istanza predefinita nel file di autenticazione OMI MySQL hello.<br>campo della password Hello deve essere immesso in testo normale - password hello nel file di autenticazione OMI MySQL hello saranno con codifica Base 64. |
| delete *predefinita\|num_port* | mycimprovauth 3308 | Elimina l'istanza specificata di hello per l'impostazione predefinita o al numero di porta. |
| help | mycimprov help | Stampa un elenco di comandi toouse. |
| print | mycimprov print | Stampa tooread un semplice file di autenticazione OMI MySQL. |
| update port_num *bind-address nome utente password* | mycimprov update 3307 127.0.0.1 root pwd | Aggiorna l'istanza specificata di hello o aggiunge un'istanza di hello se non esiste. |

Hello comandi dell'esempio seguente definiscono un account utente predefinito per il server MySQL hello in localhost.  campo della password Hello deve essere immesso in testo normale: password hello nel file di autenticazione OMI MySQL hello saranno con codifica Base 64

    sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>'
    sudo /opt/omi/bin/service_control restart

### <a name="database-permissions-required-for-mysql-performance-counters"></a>Autorizzazioni del database necessarie per i contatori delle prestazioni di MySQL
Utente di MySQL Hello richiede accesso toohello seguente query toocollect dati sulle prestazioni di MySQL Server. 

    SHOW GLOBAL STATUS;
    SHOW GLOBAL VARIABLES:


utente di MySQL Hello richiede l'accesso SELECT toohello le tabelle predefinite seguenti.

- information_schema
- mysql. 

È possibile concedere questi privilegi eseguendo i comandi grant seguenti hello.

    GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
    GRANT SELECT ON mysql.* too‘monuser’@’localhost’;


> [!NOTE]
> toogrant autorizzazioni tooa hello utente la concessione di monitoraggio di MySQL deve avere il privilegio 'GRANT option' hello nonché privilegio hello da concedere.

### <a name="define-performance-counters"></a>Definire i contatori delle prestazioni

Una volta configurato, hello agente OMS per Linux toosend dati tooLog Analitica, è necessario configurare toocollect i contatori delle prestazioni di hello.  Utilizzare la procedura hello in [origini di dati delle prestazioni Windows e Linux in Log Analitica](log-analytics-data-sources-windows-events.md) con contatori hello in hello nella tabella seguente.

| Nome oggetto | Nome contatore |
|:--|:--|
| MySQL Database | Disk Space in Bytes |
| MySQL Database | Tabelle |
| Server MySQL | Aborted Connection Pct |
| Server MySQL | Connection Use Pct |
| Server MySQL | Disk Space Use in Bytes |
| Server MySQL | Full Table Scan Pct |
| Server MySQL | InnoDB Buffer Pool Hit Pct |
| Server MySQL | InnoDB Buffer Pool Use Pct |
| Server MySQL | InnoDB Buffer Pool Use Pct |
| Server MySQL | Key Cache Hit Pct |
| Server MySQL | Key Cache Use Pct |
| Server MySQL | Key Cache Write Pct |
| Server MySQL | Query Cache Hit Pct |
| Server MySQL | Query Cache Prunes Pct |
| Server MySQL | Query Cache Use Pct |
| Server MySQL | Table Cache Hit Pct |
| Server MySQL | Table Cache Use Pct |
| Server MySQL | Table Lock Contention Pct |

## <a name="apache-http-server"></a>Apache HTTP Server 
Se nel computer di hello viene rilevato Apache HTTP Server durante l'installazione del bundle omsagent hello, verranno automaticamente installata un provider di Apache HTTP Server per il monitoraggio delle prestazioni. Questo provider si basa su un modulo Apache che deve essere caricato in dati sulle prestazioni di ordine tooaccess Ciao Apache HTTP Server. modulo Hello può essere caricato con hello comando seguente:
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

toounload hello Apache modulo di monitoraggio, eseguire hello comando seguente:
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```

### <a name="define-performance-counters"></a>Definire i contatori delle prestazioni

Una volta configurato, hello agente OMS per Linux toosend dati tooLog Analitica, è necessario configurare toocollect i contatori delle prestazioni di hello.  Utilizzare la procedura hello in [origini di dati delle prestazioni Windows e Linux in Log Analitica](log-analytics-data-sources-windows-events.md) con contatori hello in hello nella tabella seguente.

| Nome oggetto | Nome contatore |
|:--|:--|
| Apache HTTP Server | Busy Workers |
| Apache HTTP Server | Idle Workers |
| Apache HTTP Server | Pct Busy Workers |
| Apache HTTP Server | Total Pct CPU |
| Apache Virtual Host | Errors per Minute - Client |
| Apache Virtual Host | Errors per Minute - Server |
| Apache Virtual Host | KB per Request |
| Apache Virtual Host | Requests KB per Second |
| Apache Virtual Host | Requests per Second |



## <a name="next-steps"></a>Passaggi successivi
* [Raccogliere i contatori delle prestazioni](log-analytics-data-sources-performance-counters.md) da agenti Linux.
* Informazioni su [log ricerche](log-analytics-log-searches.md) tooanalyze hello dati raccolti da origini dati e le soluzioni. 
