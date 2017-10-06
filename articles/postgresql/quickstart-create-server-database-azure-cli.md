---
title: Creare un Database di Azure per PostgreSQL utilizzando hello CLI di Azure | Documenti Microsoft
description: Rapido avviare Guida toocreate e gestione dei Database di Azure per server PostgreSQL mediante Azure CLI (interfaccia della riga di comando).
services: postgresql
author: sanagama
ms.author: sanagama
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 06/13/2017
ms.openlocfilehash: 946aa3cbf5ff9f5ac4e51248412d3da5d718141e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-using-hello-azure-cli"></a>Creare un Database di Azure per PostgreSQL utilizzando hello CLI di Azure
Il Database di Azure per PostgreSQL è un servizio gestito che consente di toorun, gestire e scalare database PostgreSQL a disponibilità elevata nel cloud hello. Hello CLI di Azure viene utilizzato toocreate e gestire le risorse di Azure dalla riga di comando hello o negli script. Questa Guida introduttiva viene illustrato come toocreate un Azure del Database per server PostgreSQL in un [gruppo di risorse](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) utilizzando hello CLI di Azure.

Se non si ha una sottoscrizione di Azure, creare un account [gratuito](https://azure.microsoft.com/free/) prima di iniziare.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

Se si dispone di più sottoscrizioni, scegliere in cui verranno fatturata risorse hello la sottoscrizione appropriata hello. Selezionare un ID di sottoscrizione specifico sotto l'account tramite il comando [az account set](/cli/azure/account#set).
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) utilizzando hello [gruppo az creare](/cli/azure/group#create) comando. Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite come gruppo. esempio Hello crea un gruppo di risorse denominato `myresourcegroup` in hello `westus` percorso.
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a>Creare un database di Azure per il server PostgreSQL

Creare un [Database di Azure per server PostgreSQL](overview.md) utilizzando hello [az postgres server creare](/cli/azure/postgres/server#create) comando. Un server contiene un gruppo di database gestiti come gruppo. 

esempio Hello crea un server denominato `mypgserver-20170401` nel gruppo di risorse `myresourcegroup` con account di accesso amministratore server `mylogin`. nome Hello di un server esegue il mapping nome tooDNS ed è pertanto necessario toobe globalmente univoco in Azure. Hello Substitute `<server_admin_password>` con il proprio valore.
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> account di accesso amministratore server Hello e una password che è possibile specificare sono necessari toolog toohello server e i relativi database più avanti in questa Guida introduttiva. Prendere nota di queste informazioni per usarle in seguito.

Per impostazione predefinita, il database **postgres** viene creato nel server. Hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database è un database predefinito può essere utilizzata per gli utenti, utilità e applicazioni di terze parti. 


## <a name="configure-a-server-level-firewall-rule"></a>Configurare una regola del firewall a livello di server

Creare una regola firewall di livello server Azure PostgreSQL con hello [az postgres regola firewall del server-creare](/cli/azure/postgres/server/firewall-rule#create) comando. Una regola del firewall a livello di server consente a un'applicazione esterna, ad esempio [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) o [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server firewall hello Azure PostgreSQL servizio. 

È possibile impostare una regola del firewall che copre un intervallo IP toobe tooconnect in grado di dalla rete. Hello seguente utilizza [az postgres regola firewall del server-creare](/cli/azure/postgres/server/firewall-rule#create) toocreate una regola del firewall `AllowAllIps` intervallo di indirizzi IP. tooopen tutti gli indirizzi IP, utilizzare 0.0.0.0 come hello avvio indirizzo IP e 255.255.255.255 come hello indirizzo finale.
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> Il server PostgreSQL Azure comunica sulla porta 5432. Quando si esegue la connessione da una rete aziendale, il traffico in uscita sulla porta 5432 potrebbe non essere consentito dal firewall della rete. È aperto il reparto IT server porte 5432 tooconnect tooyour Database SQL di Azure.

## <a name="get-hello-connection-information"></a>Ottenere informazioni sulla connessione hello

tooconnect tooyour server, sono necessarie credenziali di accesso e le informazioni di host tooprovide.
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

il risultato di Hello è nel formato JSON. Prendere nota di hello **administratorLogin** e **fullyQualifiedDomainName**.
```json
{
  "administratorLogin": "mylogin",
  "fullyQualifiedDomainName": "mypgserver-20170401.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforPostgreSQL/servers/mypgserver-20170401",
  "location": "westus",
  "name": "mypgserver-20170401",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "PGSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 51200,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": "9.6"
}
```

## <a name="connect-toopostgresql-database-using-psql"></a>La connessione a database tooPostgreSQL utilizzando psql

Se il computer client abbia PostgreSQL installato, è possibile utilizzare un'istanza locale di [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL server. Consente di usare ora il server Azure PostgreSQL toohello tooconnect di hello psql utilità della riga di comando.

1. Eseguire hello seguente psql comando tooconnect tooan Database di Azure per server PostgreSQL
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  Ad esempio, hello comando seguente si connette a database predefinito toohello chiamato **postgres** sul server PostgreSQL **mypgserver 20170401.postgres.database.azure.com** utilizzando le credenziali di accesso. Immettere hello `<server_admin_password>` scelto quando viene richiesta la password.
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  Dopo avere connesso toohello server, è possibile creare un database vuoto al prompt dei comandi hello.
```sql
CREATE DATABASE mypgsqldb;
```

3.  Al prompt dei comandi hello, eseguire hello seguente database toohello appena creato di comando tooswitch connessione **mypgsqldb**:
```sql
\c mypgsqldb
```

## <a name="connect-toopostgresql-database-using-pgadmin"></a>La connessione a database tooPostgreSQL utilizzando pgAdmin

tooconnect tooAzure PostgreSQL server utilizzando lo strumento GUI hello _pgAdmin_
1.  Avviare hello _pgAdmin_ applicazione nel computer client. È possibile installare _pgAdmin_ da http://www.pgadmin.org/.
2.  Scegliere **aggiungere nuovi Server** da hello **collegamenti rapidi** menu.
3.  In hello **Create - Server** la finestra di dialogo **generale** , immettere un nome descrittivo univoco per il server di hello. Ad esempio, **Azure PostgreSQL Server**.
 ![Strumento pgAdmin - Finestra di creazione del server](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)
4.  In hello **Create - Server** nella finestra di dialogo **connessione** scheda:
    - Immettere il nome di server completo hello (ad esempio, **mypgserver 20170401.postgres.database.azure.com**) in hello **nome Host / indirizzo** casella. 
    - Immettere la porta 5432 in hello **porta** casella. 
    - Immettere hello **accesso di amministratore di Server (user@mypgserver)** ottenuto in precedenza in questa Guida introduttiva e la password immessa al momento della creazione server hello in hello **Username** e **Password** caselle, rispettivamente.
    - Selezionare **SSL Mode** (Modalità SSL) e impostare **Require** (Richiedi). Per impostazione predefinita, tutti i server PostgreSQL Azure vengono creati con l'opzione di applicazione del protocollo SSL attivata. tooturn OFF applica SSL, vedere i dettagli nella [applicazione SSL](./concepts-ssl-connection-security.md).

    ![pgAdmin - Finestra di creazione del server](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  Fare clic su **Salva**.
6.  Nel riquadro a sinistra del Visualizzatore hello, espandere hello **gruppi di Server**. Scegliere il server **Azure PostgreSQL Server**.
7.  Scegliere hello **Server** connessi e quindi scegliere **database** sotto di esso. 
8.  Fare clic su **database** tooCreate un Database.
9.  Scegliere un nome di database **mypgsqldb** proprietario hello per tale account di accesso amministratore server e **mylogin**.
10. Fare clic su **salvare** toocreate un database vuoto.
11. In hello **Browser**, espandere hello **server** gruppo. Espandere il server di hello è stato creato e vedere database hello **mypgsqldb** in essa contenute.
 ![pgAdmin - Finestra di creazione del database](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)


## <a name="clean-up-resources"></a>Pulire le risorse

Pulizia di tutte le risorse è stato creato in avvio rapido di hello eliminando hello [gruppo di risorse](../azure-resource-manager/resource-group-overview.md).

> [!TIP]
> Altre guide di avvio rapido di questa raccolta si basano sulla presente guida di avvio rapido. Se si intende toocontinue toowork con successive Guide rapide, eseguire la pulizia hello le risorse create in questa Guida rapida. Se non si prevede toocontinue, utilizzare hello seguendo i passaggi toodelete tutte le risorse create da questa Guida rapida di hello CLI di Azure.

```azurecli-interactive
az group delete --name myresourcegroup
```

Se si sarebbe analogo toodelete hello un nuovo server, è possibile eseguire [dell'eliminazione del server postgres az](/cli/azure/postgres/server#delete) comando.
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a>Passaggi successivi
> [!div class="nextstepaction"]
> [Eseguire la migrazione del database usando le funzionalità di esportazione e importazione](./howto-migrate-using-export-and-import.md)
