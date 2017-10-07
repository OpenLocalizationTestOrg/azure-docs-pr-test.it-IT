---
title: aaaDesign di Azure prima di Database per database MySQL - CLI di Azure | Documenti Microsoft
description: In questa esercitazione viene illustrato come toocreate e gestire Database di Azure per il server MySQL e di database mediante Azure CLI 2.0 dalla riga di comando hello.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 6339913c2af58e0e4c4eabb69097a5c9c245781c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a>Progettare il primo database di Azure per il database MySQL

Il Database di Azure per MySQL è un servizio di database relazionale in hello Microsoft cloud basato sul motore di database MySQL Community Edition. In questa esercitazione, si utilizza Azure CLI (interfaccia della riga di comando) e toolearn altre utilità come a:

> [!div class="checklist"]
> * Creare un database di Azure per MySQL
> * Configurare firewall hello del server
> * Utilizzare [strumento da riga di comando mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate un database
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
Creare un [gruppo di risorse di Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) con il comando [az group create](https://docs.microsoft.com/cli/azure/group#create). Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite come gruppo.

esempio Hello crea un gruppo di risorse denominato `mycliresource` in hello `westus` percorso.

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>Creare un database di Azure per il server MySQL
Creare un Database di Azure per comando di creazione di server MySQL hello az mysql server. Un server può gestire più database. In genere, viene usato un database separato per ogni progetto o per ogni utente.

esempio Hello crea un Database di Azure per il server MySQL situato in `westus` nel gruppo di risorse hello `mycliresource` con nome `mycliserver`. Hello server dispone di un accesso di amministratore in denominato `myadmin` e la password `Password01!`. Hello server viene creato con **base** livello di prestazioni e **50** unità condivisa tra tutti i database hello server hello di calcolo. È possibile applicare la scalabilità di calcolo e archiviazione verso l'alto o verso il basso a seconda delle esigenze dell'applicazione hello.

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>Configurare una regola del firewall
Creare un Database di Azure per regola del firewall di livello di server MySQL con hello az mysql regola firewall del server-creare un comando. Una regola del firewall a livello di server consente a un'applicazione esterna, ad esempio **mysql** strumento da riga di comando o un server di tooyour tooconnect MySQL Workbench tramite firewall del servizio Azure MySQL hello. 

Hello esempio seguente viene creata una regola del firewall per un intervallo di indirizzi predefiniti. In questo esempio viene hello intera possibili intervallo di indirizzi IP.

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-hello-connection-information"></a>Ottenere informazioni sulla connessione hello

tooconnect tooyour server, sono necessarie credenziali di accesso e le informazioni di host tooprovide.
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

il risultato di Hello è nel formato JSON. Prendere nota di hello **fullyQualifiedDomainName** e **administratorLogin**.
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mycliserver.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mycliresource/providers/Microsoft.DBforMySQL/servers/mycliserver",
  "location": "westus",
  "name": "mycliserver",
  "resourceGroup": "mycliresource",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-toohello-server-using-mysql"></a>Connessione server toohello con mysql
Utilizzare [strumento da riga di comando mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish tooyour una connessione Database di Azure per il server MySQL. In questo esempio, il comando hello è:
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a>Creazione di un database vuoto
Dopo aver connesso toohello server, creare un database vuoto.
```sql
mysql> CREATE DATABASE mysampledb;
```

Al prompt dei comandi hello, eseguire hello seguenti database di comando tooswitch hello connessione toothis appena creato:
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a>Creare tabelle nel database di hello
Ora che è stato appreso come tooconnect toohello Database di Azure per il database MySQL, possiamo andare come toocomplete alcune attività di base.

In primo luogo, è possibile creare una tabella e caricarla con alcuni dati. Creare una tabella che contenga le informazioni riguardanti l'inventario.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a>Caricamento dei dati nelle tabelle di hello
Ora che abbiamo una tabella, possiamo inserire alcuni dati al suo interno. Nella finestra del prompt dei comandi aperta hello eseguire hello seguente query tooinsert alcune righe di dati.
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

Ora si dispone di due righe di dati di esempio nella tabella hello creato in precedenza.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Eseguire una query e aggiornare i dati nelle tabelle di hello hello
Eseguire le seguenti query tooretrieve informazioni dalla tabella di database hello hello.
```sql
SELECT * FROM inventory;
```

È inoltre possibile aggiornare i dati di hello nelle tabelle di hello.
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

la riga Hello Ottiene aggiornata di conseguenza quando si recuperano dati.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Ripristinare un punto precedente tooa di database nel tempo
Si supponga di aver eliminato accidentalmente questa tabella. Si tratta di un elemento che non è facile da ripristinare. Il Database di Azure per MySQL consente toogo tooany indietro punto nel tempo di hello ultimo backup too35 giorni e questo punto nel tempo tooa nuovo server di ripristino. È possibile utilizzare questo nuovo toorecover server i dati eliminati. Hello seguente punto di ripristino hello campione server tooa passaggi prima tabella hello è stato aggiunto.

Per hello ripristino è necessario hello le seguenti informazioni:

- Punto di ripristino: selezionare un punto nel tempo che si verifica prima che il server di hello è stato modificato. Deve essere maggiore o uguale valore backup meno recenti del database di origine toohello.
- Server di destinazione: fornire un nuovo nome del server desiderato toorestore per
- Server di origine: specificare il nome di hello hello del server di si desidera toorestore da
- Percorso: Non è possibile selezionare l'area di hello, per impostazione predefinita è uguale al server di origine hello

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

server hello toorestore e [tooa momento di ripristinare](./howto-restore-server-portal.md) prima tabella hello è stata eliminata. Ripristino di un punto diverso di server tooa nel tempo crea un duplicato nuovo server come server originale hello come hello punto nel tempo specificato, purché tale valore entro il periodo di memorizzazione hello per le [livello di servizio](./concepts-service-tiers.md).

## <a name="next-steps"></a>Passaggi successivi
Questa esercitazione illustra come:
> [!div class="checklist"]
> * Creare un database di Azure per MySQL
> * Configurare firewall hello del server
> * Utilizzare [strumento da riga di comando mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate un database
> * Caricare dati di esempio
> * Eseguire query sui dati
> * Aggiornare i dati
> * Ripristinare i dati

> [!div class="nextstepaction"]
> [Database di Azure per MySQL - Esempi di interfaccia della riga di comando di Azure](./sample-scripts-azure-cli.md)
