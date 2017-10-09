---
title: aaaMigrate un database utilizzando importare ed esportare nel Database di Azure per PostgreSQL | Documenti Microsoft
description: Viene descritto come estrarre un database PostgreSQL in un file di script e importarli nel database di destinazione hello da tale file hello.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 5ca4650782b02e1067c5a8a3710f2dfbc8c76063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-postgresql-database-using-export-and-import"></a>Migrare il database PostgreSQL usando le funzionalità di esportazione e importazione
È possibile utilizzare [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract un database PostgreSQL in un file di script e [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) dati hello tooimport nel database di destinazione hello da tale file.

## <a name="prerequisites"></a>Prerequisiti
toostep tramite questa procedura-tooguide, è necessario:
- Un [Database di Azure per server PostgreSQL](quickstart-create-server-database-portal.md) con accesso tooallow regole del firewall e il database in essa contenute.
- Utilità della riga di comando [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) installata
- Utilità della riga di comando [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) installata

Seguire questi passaggi tooexport e importare il database PostgreSQL.

## <a name="create-a-script-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a>Creare un file di script tramite pg_dump contenente toobe dati hello caricato
tooexport il PostgreSQL esistente del database locale o in un file script sql tooa macchina virtuale, eseguire hello comando nell'ambiente esistente seguente:
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
Se ad esempio è presente un server locale che contiene un database denominato **testdb**, eseguire:
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-hello-data-on-target-azure-database-for-postrgesql"></a>Importazione dei dati nella destinazione Database di Azure per PostrgeSQL hello
È possibile utilizzare una riga di comando psql hello e hello -d, - dbname dati hello tooimport dei parametri nel Database di Azure per PostrgeSQL è creato e caricare dati da file sql hello.
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
Nell'esempio viene utilizzata l'utilità psql e un file script denominato **testdb.sql** da dati tooimport del passaggio precedente nel database di hello **mypgsqldb** sul server di destinazione  **mypgserver 20170401.postgres.database.azure.com**.
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a>Passaggi successivi
- toomigrate un database PostgreSQL tramite dump e ripristino, vedere [la migrazione del database PostgreSQL utilizzando dump e ripristino](howto-migrate-using-dump-and-restore.md)
