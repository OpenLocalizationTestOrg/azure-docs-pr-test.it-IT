---
title: Progettare il primo Database di Azure per PostgreSQL tramite l'interfaccia della riga di comando di Azure | Documentazione Microsoft
description: In questa esercitazione viene illustrato come tooDesign di Azure prima di Database per PostgreSQL utilizzando CLI di Azure.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: tutorial
ms.date: 06/13/2017
ms.openlocfilehash: 7914925c090e0b6f3e7c8a999eedb0b2baf83d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a>Progettare il primo Database di Azure per PostgreSQL tramite l'interfaccia della riga di comando di Azure 
In questa esercitazione, si utilizza Azure CLI (interfaccia della riga di comando) e toolearn altre utilità come a:
> [!div class="checklist"]
> * Creare un database di Azure per PostgreSQL
> * Configurare firewall hello del server
> * Utilizzare [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate utilità un database
> * Caricare dati di esempio
> * Eseguire query sui dati
> * Aggiornare i dati
> * Ripristinare i dati

È possibile utilizzare hello Azure Cloud Shell nel browser hello o [installare Azure CLI 2.0]( /cli/azure/install-azure-cli) su blocchi di codice hello toorun propri computer in questa esercitazione.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

Se si dispone di più sottoscrizioni, scegliere la sottoscrizione appropriata di hello in cui esistano risorse hello o viene fatturata per. Selezionare un ID di sottoscrizione specifico sotto l'account tramite il comando [az account set](/cli/azure/account#set).
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

esempio Hello crea un server denominato `mypgserver-20170401` nel gruppo di risorse `myresourcegroup` con account di accesso amministratore server `mylogin`. Nome di un server esegue il mapping nome tooDNS ed è pertanto necessario toobe globalmente univoco in Azure. Hello Substitute `<server_admin_password>` con il proprio valore.
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
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
>

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

## <a name="connect-tooazure-database-for-postgresql-database-using-psql"></a>Connettersi tooAzure Database per database PostgreSQL utilizzando psql
Se il computer client abbia PostgreSQL installato, è possibile utilizzare un'istanza locale di [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), o hello Azure Cloud Console tooconnect tooan Azure PostgreSQL server. Verrà ora utilizzare hello psql utilità della riga di comando tooconnect toohello Azure Database PostgreSQL server.

1. Eseguire hello seguente psql comando tooconnect tooan Database di Azure per server PostgreSQL
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  Ad esempio, hello comando seguente si connette a database predefinito toohello chiamato **postgres** sul server PostgreSQL **mypgserver 20170401.postgres.database.azure.com** utilizzando le credenziali di accesso. Immettere hello `<server_admin_password>` scelto quando viene richiesta la password.
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  Dopo avere connesso toohello server, è possibile creare un database vuoto al prompt dei comandi hello.
```sql
CREATE DATABASE mypgsqldb;
```

3.  Al prompt dei comandi hello, eseguire hello seguente database toohello appena creato di comando tooswitch connessione **mypgsqldb**:
```sql
\c mypgsqldb
```

## <a name="create-tables-in-hello-database"></a>Creare tabelle nel database di hello
Ora che è stato appreso come tooconnect toohello Database di Azure per PostgreSQL, possiamo andare come toocomplete alcune attività di base.

In primo luogo, è possibile creare una tabella e caricarla con alcuni dati. Creare una tabella che tiene traccia delle informazioni riguardanti l'inventario.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

È possibile visualizzare hello creata tabella nell'elenco delle tabelle di hello ora digitando:
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a>Caricamento dei dati nelle tabelle di hello
Ora che abbiamo una tabella, possiamo inserire alcuni dati al suo interno. Nella finestra del prompt dei comandi aperta hello eseguire hello seguente query tooinsert alcune righe di dati
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

È ora due righe di dati di esempio nella tabella hello creato in precedenza.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Eseguire una query e aggiornare i dati nelle tabelle di hello hello
Eseguire le seguenti query tooretrieve informazioni dalla tabella di database hello hello. 
```sql
SELECT * FROM inventory;
```

È inoltre possibile aggiornare i dati di hello nelle tabelle di hello
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

la riga Hello Ottiene aggiornata di conseguenza quando si recuperano dati.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Ripristinare un punto precedente tooa di database nel tempo
Si supponga di aver eliminato accidentalmente una tabella. Si tratta di un elemento che non è facile da ripristinare. Il Database di Azure per PostgreSQL consente toogo tooany indietro punto nel tempo (in hello ultimo backup too7 giorni (Basic) e 35 giorni (Standard)) e il ripristino di questo nuovo server tooa punto nel tempo. È possibile utilizzare questo nuovo toorecover server i dati eliminati. Hello seguente punto di ripristino hello campione server tooa passaggi prima tabella hello è stato aggiunto.

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

Hello `az postgres server restore` comando deve hello seguenti parametri:
| Impostazione | Valore consigliato | Descrizione  |
| --- | --- | --- |
| --resource-group |  myResourceGroup |  Il gruppo di risorse in cui hello server di origine esiste.  |
| --name | mypgserver-restored | nome di Hello del server di nuovo hello viene creato dal comando di ripristino hello. |
| restore-point-in-time | 2017-04-13T13:59:00Z | Selezionare un toorestore punto nel tempo per. Questa data e ora deve essere entro il periodo di conservazione dei backup del server di origine hello. Usare il formato ISO8601 per la data e l'ora. È possibile usare il fuso orario locale, ad esempio `2017-04-13T05:59:00-08:00`, o il formato UTC Zulu `2017-04-13T13:59:00Z`. |
| --source-server | mypgserver-20170401 | Hello nome o ID di hello origine server toorestore da. |

Ripristino di un server tooa punto nel tempo, viene creato un nuovo server, la copia come server originale di hello a partire da hello punto nel tempo specificato. percorso Hello e prezzi indicati i livelli per server hello ripristinato sono hello stesso come server di origine hello.

comando Hello è sincrono e verrà restituito dopo il ripristino del server di hello. Al termine del ripristino di hello, individuare hello nuovo server in cui è stato creato. Verificare hello ripristino dei dati nel modo previsto.


## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, si è appreso toouse CLI di Azure (interfaccia della riga di comando) e di altre utilità per:
> [!div class="checklist"]
> * Creare un database di Azure per PostgreSQL
> * Configurare firewall hello del server
> * Utilizzare [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate utilità un database
> * Caricare dati di esempio
> * Eseguire query sui dati
> * Aggiornare i dati
> * Ripristinare i dati

Successivamente, informazioni su come toouse hello attività simili toodo portale Azure, rivedere l'esercitazione: [di progettazione di un Database di Azure per PostgreSQL utilizzando hello portale di Azure](tutorial-design-database-using-azure-portal.md)
