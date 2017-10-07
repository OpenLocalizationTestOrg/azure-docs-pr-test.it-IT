---
title: aaaHow tooConfigure i parametri del Server nel Database di Azure per MySQL | Documenti Microsoft
description: In questo articolo viene descritto come parametri di server disponibili tooconfigure nel Database di Azure per l'utilizzo di MySQL hello portale di Azure.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/19/2017
ms.openlocfilehash: 8292c8eda605854a06b6a9c82185c857bd353cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-server-parameters-in-azure-database-for-mysql-using-hello-azure-portal"></a>Come parametri di server tooconfigure nel Database di Azure per l'utilizzo di MySQL hello portale di Azure

Database di Azure per MySQL supporta la configurazione di alcuni parametri di server. In questo articolo viene descritto come tooconfigure questi parametri utilizzando hello portale di Azure e gli elenchi di hello supportato parametri, valori predefiniti di hello e hello intervallo di valori validi. Non tutti i parametri di server possono essere modificati. Sono supportati solo hello quelli elencati di seguito.

## <a name="navigate-tooserver-parameters-blade-on-azure-portal"></a>Passare a pannello di parametri tooServer nel portale di Azure

Accedi toohello portale di Azure, quindi fare clic su Database di Azure per il nome di server MySQL. In hello **impostazioni** fare clic su **i parametri del Server** tooopen hello Server parametri pannello hello Database di Azure per MySQL.

![Pannello Parametri del server del portale di Azure](./media/howto-server-parameters/auzre-portal-server-parameters.png)

## <a name="list-of-configurable-server-parameters"></a>Elenco di parametri del server configurabili

Hello nella tabella seguente sono elencati i parametri del server hello attualmente supportato. è possibile configurare i parametri di Hello in base a tooyour requisiti dell'applicazione.

> [!div class="mx-tableFixed"]
|Nome parametro|Valore predefinito|Range|Descrizione|
|---|---|---|---|
|binlog_group_commit_sync_delay|1000|0, 11-1000000|Controlli microsecondi quanti hello attese di registro binario commit prima della sincronizzazione toodisk file di registro binario hello.|
|binlog_group_commit_sync_no_delay_count|0|0-1000000|numero massimo di Hello di toowait di transazioni per il quale viene annullato ritardo corrente di hello come specificato da binlog-gruppo-commit-sync-delay.|
|character_set_server|LATIN1|BIG5, UTF8MB4 e così via.|Utilizzare charset_name come set di caratteri server hello predefinito.|
|div_precision_increment|4|0-30|Numero di cifre da cui la scala hello tooincrease del risultato hello di operazioni di divisione.|
|group_concat_max_len|1024|4-16777216|Lunghezza del risultato vengono massima in byte per hello GROUP_CONCAT().|
|innodb_adaptive_hash_index|ATTIVA|ATTIVA, DISATTIVA|Indica se gli indici hash adattivi di InnoDB sono abilitati o disabilitati.|
|innodb_lock_wait_timeout|50|1-3600|durata Hello in secondi di una transazione InnoDB attende un blocco di riga prima di rinunciare.|
|interactive_timeout|1800|10-1800|Numero di secondi hello server è in attesa dell'attività su una connessione interattiva prima della chiusura.|
|log_bin_trust_function_creators|DISATTIVA|ATTIVA, DISATTIVA|Questa variabile si applica quando è abilitata la registrazione binaria. Controlla se la funzione archiviata gli autori possono essere attendibili non funzioni toocreate archiviati che causano toobe unsafe eventi scritti registro binario toohello.|
|log_queries_not_using_indexes|DISATTIVA|ATTIVA, DISATTIVA|Query log previsto tooretrieve tutti i log di query tooslow righe.|
|log_slow_admin_statements|DISATTIVA|ATTIVA, DISATTIVA|Include istruzioni amministrative lenta nelle istruzioni di hello scritte log query lente toohello.|
|log_throttle_queries_not_using_indexes|0|0-4294967295|Limiti hello numero di tali query al minuto che possono essere scritti i log di query lente toohello.|
|long_query_time|10|1-1E + 100|Se una query richiede più tempo rispetto a questo numero di secondi, il server di hello incrementa variabile di stato Slow_queries hello.|
|max_allowed_packet|536870912|1024-1073741824|dimensione massima di Hello del pacchetto o qualsiasi stringa/intermedio generato o qualsiasi parametro inviato da hello mysql_stmt_send_long_data() funzione API C.|
|min_examined_row_limit|0|0-18446744073709551615|Registra le query che hanno maggiore hello configurato numero di righe nel log query lente hello. |
|server_id|3293747068|1000-4294967295|ID del server Hello, utilizzato nella replica toogive ogni master e slave un'identità univoca.|
|slave_net_timeout|60|30-3600|numero di Hello di toowait secondi per i dati più master hello prima slave hello considera connessione hello interrotto, interrompe hello leggere e tenta di tooreconnect.|
|slow_query_log|DISATTIVA|ATTIVA, DISATTIVA|Abilitare o disabilitare log query lente hello.|
|sql_mode|0 selezionato|ALLOW_INVALID_DATES, IGNORE_SPACE e così via.|modalità SQL server corrente Hello.|
|time_zone|SYSTEM|esempi: -8:00, +05:30|Hello fuso orario del server.|
|wait_timeout|120|60-240|Hello numero di secondi hello server è in attesa dell'attività su una connessione non interattiva prima della chiusura.|

## <a name="next-steps"></a>Passaggi successivi
- [Raccolte connessioni per il Database di Azure per MySQL](concepts-connection-libraries.md)
