---
title: Come eseguire dump e ripristino in Database di Azure per PostgreSQL | Microsoft Docs
description: Descrive come estrarre un database PostgreSQL in un file di dump e come ripristinare il database PostgreSQL da un file di archivio creato da pg_dump in Database di Azure per PostgreSQL.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 190373c4980b67e16b58700e4b7e65658545c615
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a><span data-ttu-id="f4de4-103">Eseguire la migrazione del database PostgreSQL usando dump e ripristino</span><span class="sxs-lookup"><span data-stu-id="f4de4-103">Migrate your PostgreSQL database using dump and restore</span></span>
<span data-ttu-id="f4de4-104">È possibile usare [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) per estrarre un database PostgreSQL in un file di dump e [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) per ripristinare il database PostgreSQL da un file di archivio creato da pg_dump.</span><span class="sxs-lookup"><span data-stu-id="f4de4-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) to extract a PostgreSQL database into a dump file and [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) to restore the PostgreSQL database from an archive file created by pg_dump.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4de4-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f4de4-105">Prerequisites</span></span>
<span data-ttu-id="f4de4-106">Per proseguire con questa guida, si richiedono:</span><span class="sxs-lookup"><span data-stu-id="f4de4-106">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="f4de4-107">Un [server di Database di Azure per PostgreSQL](quickstart-create-server-database-portal.md) con le regole del firewall per consentire l'accesso e il database sottostante.</span><span class="sxs-lookup"><span data-stu-id="f4de4-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules to allow access and database under it.</span></span>
- <span data-ttu-id="f4de4-108">Utilità della riga di comando [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) e [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) installate</span><span class="sxs-lookup"><span data-stu-id="f4de4-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) and [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) command-line utilities installed</span></span>

<span data-ttu-id="f4de4-109">Seguire questi passaggi per eseguire il dump e il ripristino del database PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="f4de4-109">Follow these steps to dump and restore your PostgreSQL database:</span></span>

## <a name="create-a-dump-file-using-pgdump-that-contains-the-data-to-be-loaded"></a><span data-ttu-id="f4de4-110">Creare un file di dump usando pg_dump che contiene i dati da caricare</span><span class="sxs-lookup"><span data-stu-id="f4de4-110">Create a dump file using pg_dump that contains the data to be loaded</span></span>
<span data-ttu-id="f4de4-111">Per eseguire il backup di un database PostgreSQL in locale o in una macchina virtuale, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="f4de4-111">To back up an existing PostgreSQL database on-premises or in a VM, run the following command:</span></span>
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
<span data-ttu-id="f4de4-112">Se ad esempio è presente un server locale che contiene un database denominato **testdb**, eseguire:</span><span class="sxs-lookup"><span data-stu-id="f4de4-112">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-the-data-into-the-target-azure-database-for-postrgesql-using-pgrestore"></a><span data-ttu-id="f4de4-113">Ripristinare i dati nel database di Azure per PostrgeSQL di destinazione usando pg_restore</span><span class="sxs-lookup"><span data-stu-id="f4de4-113">Restore the data into the target Azure Database for PostrgeSQL using pg_restore</span></span>
<span data-ttu-id="f4de4-114">Dopo avere creato il database di destinazione, è possibile usare il comando pg_restore e il parametro -d, --dbname per ripristinare i dati nel database di destinazione dal file di dump.</span><span class="sxs-lookup"><span data-stu-id="f4de4-114">Once you have created the target database, you can use the pg_restore command and the -d, --dbname parameter to restore the data into the target database from the dump file.</span></span>
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
<span data-ttu-id="f4de4-115">In questo esempio i dati vengono ripristinati dal file dump **testdb.dump** nel database **mypgsqldb** disponibile sul server di destinazione **mypgserver-20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="f4de4-115">In this example, restore the data from the dump file **testdb.dump** into the database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a><span data-ttu-id="f4de4-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f4de4-116">Next steps</span></span>
- <span data-ttu-id="f4de4-117">Per eseguire la migrazione di un database PostgreSQL usando esportazione e importazione, vedere [Migrate your PostgreSQL database using export and import](howto-migrate-using-export-and-import.md) (Eseguire la migrazione del database PostgreSQL usando esportazione e importazione)</span><span class="sxs-lookup"><span data-stu-id="f4de4-117">To migrate a PostgreSQL database using export and import, see [Migrate your PostgreSQL database using export and import](howto-migrate-using-export-and-import.md)</span></span>