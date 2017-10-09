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
# <a name="migrate-your-postgresql-database-using-export-and-import"></a><span data-ttu-id="03d40-103">Migrare il database PostgreSQL usando le funzionalità di esportazione e importazione</span><span class="sxs-lookup"><span data-stu-id="03d40-103">Migrate your PostgreSQL database using export and import</span></span>
<span data-ttu-id="03d40-104">È possibile utilizzare [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract un database PostgreSQL in un file di script e [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) dati hello tooimport nel database di destinazione hello da tale file.</span><span class="sxs-lookup"><span data-stu-id="03d40-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract a PostgreSQL database into a script file and [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport hello data into hello target database from that file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03d40-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="03d40-105">Prerequisites</span></span>
<span data-ttu-id="03d40-106">toostep tramite questa procedura-tooguide, è necessario:</span><span class="sxs-lookup"><span data-stu-id="03d40-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="03d40-107">Un [Database di Azure per server PostgreSQL](quickstart-create-server-database-portal.md) con accesso tooallow regole del firewall e il database in essa contenute.</span><span class="sxs-lookup"><span data-stu-id="03d40-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules tooallow access and database under it.</span></span>
- <span data-ttu-id="03d40-108">Utilità della riga di comando [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) installata</span><span class="sxs-lookup"><span data-stu-id="03d40-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) command-line utility installed</span></span>
- <span data-ttu-id="03d40-109">Utilità della riga di comando [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) installata</span><span class="sxs-lookup"><span data-stu-id="03d40-109">[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) command-line utility installed</span></span>

<span data-ttu-id="03d40-110">Seguire questi passaggi tooexport e importare il database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="03d40-110">Follow these steps tooexport and import your PostgreSQL database.</span></span>

## <a name="create-a-script-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a><span data-ttu-id="03d40-111">Creare un file di script tramite pg_dump contenente toobe dati hello caricato</span><span class="sxs-lookup"><span data-stu-id="03d40-111">Create a script file using pg_dump that contains hello data toobe loaded</span></span>
<span data-ttu-id="03d40-112">tooexport il PostgreSQL esistente del database locale o in un file script sql tooa macchina virtuale, eseguire hello comando nell'ambiente esistente seguente:</span><span class="sxs-lookup"><span data-stu-id="03d40-112">tooexport your existing PostgreSQL database on-premises or in a VM tooa sql script file, run hello following command in your existing environment:</span></span>
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
<span data-ttu-id="03d40-113">Se ad esempio è presente un server locale che contiene un database denominato **testdb**, eseguire:</span><span class="sxs-lookup"><span data-stu-id="03d40-113">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-hello-data-on-target-azure-database-for-postrgesql"></a><span data-ttu-id="03d40-114">Importazione dei dati nella destinazione Database di Azure per PostrgeSQL hello</span><span class="sxs-lookup"><span data-stu-id="03d40-114">Import hello data on target Azure Database for PostrgeSQL</span></span>
<span data-ttu-id="03d40-115">È possibile utilizzare una riga di comando psql hello e hello -d, - dbname dati hello tooimport dei parametri nel Database di Azure per PostrgeSQL è creato e caricare dati da file sql hello.</span><span class="sxs-lookup"><span data-stu-id="03d40-115">You can use hello psql command line and hello -d, --dbname parameter tooimport hello data into Azure Database for PostrgeSQL we created and load data from hello sql file.</span></span>
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
<span data-ttu-id="03d40-116">Nell'esempio viene utilizzata l'utilità psql e un file script denominato **testdb.sql** da dati tooimport del passaggio precedente nel database di hello **mypgsqldb** sul server di destinazione  **mypgserver 20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="03d40-116">This example uses psql utility and a script file named **testdb.sql** from previous step tooimport data into hello database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a><span data-ttu-id="03d40-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="03d40-117">Next steps</span></span>
- <span data-ttu-id="03d40-118">toomigrate un database PostgreSQL tramite dump e ripristino, vedere [la migrazione del database PostgreSQL utilizzando dump e ripristino](howto-migrate-using-dump-and-restore.md)</span><span class="sxs-lookup"><span data-stu-id="03d40-118">toomigrate a PostgreSQL database using dump and restore, see [Migrate your PostgreSQL database using dump and restore](howto-migrate-using-dump-and-restore.md)</span></span>
