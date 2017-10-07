---
title: aaaConfigure accesso server nei registri e PostgreSQL mediante Azure CLI | Documenti Microsoft
description: In questo articolo viene descritto come tooconfigure e accesso hello i log del server nel Database di Azure per PostgreSQL tramite riga di comando CLI di Azure.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 924d4e7634cc48405bcb0f813cf61d8b72ad8aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a>Configurare e accedere ai log del server usando l'interfaccia della riga di comando di Azure
È possibile scaricare i log degli errori server PostgreSQL hello utilizzando hello interfaccia della riga di comando (CLI di Azure). Tuttavia, i registri tootransaction di accesso non è supportata. 

## <a name="prerequisites"></a>Prerequisiti
toostep tramite questa procedura-tooguide, è necessario:
- [Database di Azure per il server PostgreSQL](quickstart-create-server-database-azure-cli.md)
- Installare [CLI di Azure 2.0](/cli/azure/install-azure-cli) della riga di comando utilità oppure utilizzare hello Azure Cloud Shell nel browser hello.

## <a name="configure-logging-for-azure-database-for-postgresql"></a>Configurare la registrazione per Database di Azure per PostgreSQL
È possibile configurare i log di query di hello server tooaccess e i log degli errori. I log degli errori possono contenere informazioni su checkpoint, connessioni e vuoto automatico.
1. Abilitare la registrazione
2. Registro aggiornamento\_istruzione e log\_min\_durata\_registrazione delle query tooenable istruzione
3. Abilitare il periodo di conservazione

Per altre informazioni, vedere [Personalizzazione dei parametri di configurazione](howto-configure-server-parameters-using-cli.md).

## <a name="list-logs-for-azure-database-for-postgresql-server"></a>Elencare i log per il database di Azure per il server PostgreSQL
file di log disponibili toolist hello del server, eseguire hello [elenco di registri server az postgres](/cli/azure/postgres/server-logs#list) comando.

È possibile elencare i file di log hello per server **mypgserver 20170401.postgres.database.azure.com** nel gruppo di risorse **myresourcegroup**e indirizzarlo testo tooa file denominato **log\_file\_txt.**
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a>Scaricare i log in locale dal server hello
Hello [az postgres server-log scaricare](/cli/azure/postgres/server-logs#download) comando consente toodownload singoli file di log per il server. 

In questo esempio hello di download di file di log specifici per il server di hello **mypgserver 20170401.postgres.database.azure.com** nel gruppo di risorse **myresourcegroup** tooyour di ambiente locale.
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a>Passaggi successivi
- toolearn più sui log del server, vedere [log del Server nel Database di Azure per PostgreSQL](concepts-server-logs.md)
- Per altre informazioni sui parametri del server, vedere [Personalizzare i parametri di configurazione server usando l'interfaccia della riga di comando di Azure](howto-configure-server-parameters-using-cli.md)
