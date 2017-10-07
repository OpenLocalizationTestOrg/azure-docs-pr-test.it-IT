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
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a><span data-ttu-id="c3de1-103">Eseguire la migrazione del database PostgreSQL usando dump e ripristino</span><span class="sxs-lookup"><span data-stu-id="c3de1-103">Migrate your PostgreSQL database using dump and restore</span></span>
<span data-ttu-id="c3de1-104">È possibile utilizzare [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract un database PostgreSQL in un file di dump e [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) database PostgreSQL di hello toorestore da un file di archiviazione creato da pg_dump.</span><span class="sxs-lookup"><span data-stu-id="c3de1-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract a PostgreSQL database into a dump file and [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) toorestore hello PostgreSQL database from an archive file created by pg_dump.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3de1-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c3de1-105">Prerequisites</span></span>
<span data-ttu-id="c3de1-106">toostep tramite questa procedura-tooguide, è necessario:</span><span class="sxs-lookup"><span data-stu-id="c3de1-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="c3de1-107">Un [Database di Azure per server PostgreSQL](quickstart-create-server-database-portal.md) con accesso tooallow regole del firewall e il database in essa contenute.</span><span class="sxs-lookup"><span data-stu-id="c3de1-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules tooallow access and database under it.</span></span>
- <span data-ttu-id="c3de1-108">Utilità della riga di comando [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) e [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) installate</span><span class="sxs-lookup"><span data-stu-id="c3de1-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) and [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) command-line utilities installed</span></span>

<span data-ttu-id="c3de1-109">Seguire questi passaggi toodump e ripristinare il database PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="c3de1-109">Follow these steps toodump and restore your PostgreSQL database:</span></span>

## <a name="create-a-dump-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a><span data-ttu-id="c3de1-110">Creare un file di dump tramite pg_dump contenente toobe dati hello caricato</span><span class="sxs-lookup"><span data-stu-id="c3de1-110">Create a dump file using pg_dump that contains hello data toobe loaded</span></span>
<span data-ttu-id="c3de1-111">tooback backup un PostgreSQL esistente del database locale o in una macchina virtuale, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c3de1-111">tooback up an existing PostgreSQL database on-premises or in a VM, run hello following command:</span></span>
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
<span data-ttu-id="c3de1-112">Se ad esempio è presente un server locale che contiene un database denominato **testdb**, eseguire:</span><span class="sxs-lookup"><span data-stu-id="c3de1-112">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-hello-data-into-hello-target-azure-database-for-postrgesql-using-pgrestore"></a><span data-ttu-id="c3de1-113">Ripristinare i dati di hello in Database di Azure di destinazione hello di PostrgeSQL utilizzando pg_restore</span><span class="sxs-lookup"><span data-stu-id="c3de1-113">Restore hello data into hello target Azure Database for PostrgeSQL using pg_restore</span></span>
<span data-ttu-id="c3de1-114">Dopo aver creato il database di destinazione hello, è possibile utilizzare il comando di pg_restore hello e hello -d, - dbname dati hello toorestore dei parametri nel database di destinazione hello dal file di dump hello.</span><span class="sxs-lookup"><span data-stu-id="c3de1-114">Once you have created hello target database, you can use hello pg_restore command and hello -d, --dbname parameter toorestore hello data into hello target database from hello dump file.</span></span>
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
<span data-ttu-id="c3de1-115">In questo esempio, ripristinare i dati di hello da file di dump hello **testdb.dump** nel database di hello **mypgsqldb** sul server di destinazione **mypgserver-20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="c3de1-115">In this example, restore hello data from hello dump file **testdb.dump** into hello database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a><span data-ttu-id="c3de1-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c3de1-116">Next steps</span></span>
- <span data-ttu-id="c3de1-117">vedere un database PostgreSQL utilizzando Importazione ed esportazione, toomigrate [la migrazione del database PostgreSQL tramite esportazione e importazione](howto-migrate-using-export-and-import.md)</span><span class="sxs-lookup"><span data-stu-id="c3de1-117">toomigrate a PostgreSQL database using export and import, see [Migrate your PostgreSQL database using export and import](howto-migrate-using-export-and-import.md)</span></span>
