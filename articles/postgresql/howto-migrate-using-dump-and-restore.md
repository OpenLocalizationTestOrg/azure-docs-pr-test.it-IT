---
title: aaaHow tooDump e il ripristino nel Database di Azure per PostgreSQL | Documenti Microsoft
description: Viene descritto come tooextract un PostgreSQL database in un file di dump e ripristinare il database PostgreSQL hello da un file di archivio creato da pg_dump nel Database di Azure per PostgreSQL.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 9ad28e9dec3927b0f80b5e6bab6423cc944f5156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a>Eseguire la migrazione del database PostgreSQL usando dump e ripristino
È possibile utilizzare [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract un database PostgreSQL in un file di dump e [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) database PostgreSQL di hello toorestore da un file di archiviazione creato da pg_dump.

## <a name="prerequisites"></a>Prerequisiti
toostep tramite questa procedura-tooguide, è necessario:
- Un [Database di Azure per server PostgreSQL](quickstart-create-server-database-portal.md) con accesso tooallow regole del firewall e il database in essa contenute.
- Utilità della riga di comando [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) e [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) installate

Seguire questi passaggi toodump e ripristinare il database PostgreSQL:

## <a name="create-a-dump-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a>Creare un file di dump tramite pg_dump contenente toobe dati hello caricato
tooback backup un PostgreSQL esistente del database locale o in una macchina virtuale, eseguire hello comando seguente:
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
Se ad esempio è presente un server locale che contiene un database denominato **testdb**, eseguire:
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-hello-data-into-hello-target-azure-database-for-postrgesql-using-pgrestore"></a>Ripristinare i dati di hello in Database di Azure di destinazione hello di PostrgeSQL utilizzando pg_restore
Dopo aver creato il database di destinazione hello, è possibile utilizzare il comando di pg_restore hello e hello -d, - dbname dati hello toorestore dei parametri nel database di destinazione hello dal file di dump hello.
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
In questo esempio, ripristinare i dati di hello da file di dump hello **testdb.dump** nel database di hello **mypgsqldb** sul server di destinazione **mypgserver-20170401.postgres.database.azure.com**.
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a>Passaggi successivi
- vedere un database PostgreSQL utilizzando Importazione ed esportazione, toomigrate [la migrazione del database PostgreSQL tramite esportazione e importazione](howto-migrate-using-export-and-import.md)
