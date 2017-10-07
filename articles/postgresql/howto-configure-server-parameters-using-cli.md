---
title: parametri del servizio hello aaaConfigure nel Database di Azure per PostgreSQL | Documenti Microsoft
description: In questo articolo viene descritto come parametri del servizio hello tooconfigure nel Database di Azure per l'utilizzo di PostgreSQL hello della riga di comando CLI di Azure.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 84a11de24ba87fc0eb6744aaa4b53f65a183903d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a>Personalizzare i parametri di configurazione server usando l'interfaccia della riga di comando di Azure
È possibile elencare, visualizzare e aggiornare i parametri di configurazione per un server di Azure PostgreSQL utilizzando hello interfaccia della riga di comando (CLI di Azure). ma solo un subset delle configurazioni del motore viene esposto a livello di server e può essere modificato. 

## <a name="prerequisites"></a>Prerequisiti
toostep tramite questa procedura-tooguide, è necessario:
- Un server e un database [Creare un database di Azure per PostgreSQL](quickstart-create-server-database-azure-cli.md)
- Installare [CLI di Azure 2.0](/cli/azure/install-azure-cli) riga di comando utilità oppure utilizzare hello Azure Cloud Shell nel browser hello.

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a>Elencare i parametri di configurazione del server per Database di Azure per il server PostgreSQL
eseguire tutti i parametri modificabili in un server e i relativi valori, toolist hello [elenco configurazione dei server az postgres](/cli/azure/postgres/server/configuration#list) comando.

È possibile elencare i parametri di configurazione server hello per server hello **mypgserver 20170401.postgres.database.azure.com** nel gruppo di risorse **myresourcegroup**.
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a>Visualizzare i dettagli dei parametri di configurazione server
Dettagli tooshow su un parametro di configurazione specifico per un server, eseguire hello [la dimostrazione di configurazione del server di az postgres](/cli/azure/postgres/server/configuration#show) comando.

In questo esempio mostra i dettagli di hello **log\_min\_messaggi** parametro di configurazione server per server **mypgserver 20170401.postgres.database.azure.com** in gruppo di risorse **myresourcegroup.**
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a>Modificare il valore di un parametro di configurazione server
È inoltre possibile modificare il valore di hello di un determinato parametro di configurazione di server e Aggiorna valore di configurazione per il motore di hello PostgreSQL server sottostante hello. hello utilizzare configurazione di tooupdate hello [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) comando. 

hello tooupdate **log\_min\_messaggi** parametro di configurazione del server server **mypgserver 20170401.postgres.database.azure.com** nel gruppo di risorse **myresourcegroup.**
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
Se si desidera tooreset hello valore di un parametro di configurazione, sufficiente scegliere tooleave out hello facoltativo `--value` parametro e il servizio hello applicherà il valore di predefinito hello. Nell'esempio precedente sarà simile a quanto segue:
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
Questa operazione reimposta hello **log\_min\_messaggi** configurazione valore predefinito di toohello **avviso**. Per altre informazioni sulla configurazione server e sui valori consentiti, vedere la documentazione di PostgreSQL in [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html) (Configurazione server).

## <a name="next-steps"></a>Passaggi successivi
- tooconfigure e accesso ai log di server, vedere [log del Server nel Database di Azure per PostgreSQL](concepts-server-logs.md)
