---
title: 'Avvio rapido: Creare un database di Azure per il server MySQL - Interfaccia della riga di comando di Azure | Microsoft Docs'
description: Questa Guida rapida viene descritto come toouse hello toocreate CLI di Azure un Database di Azure per il server MySQL in un gruppo di risorse di Azure.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: hero-article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 708d0cce12e812cb464adcf7e83e6f85c196bafe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a>Creare un database di Azure per il server MySQL tramite l'interfaccia della riga di comando di Azure
Questa Guida rapida viene descritto come toouse hello toocreate CLI di Azure un Database di Azure per il server MySQL in un gruppo di risorse di Azure in circa cinque minuti. Hello CLI di Azure viene utilizzato toocreate e gestire le risorse di Azure dalla riga di comando hello o negli script.

Se non si ha una sottoscrizione di Azure, creare un account [gratuito](https://azure.microsoft.com/free/) prima di iniziare.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

Se si dispone di più sottoscrizioni, scegliere la sottoscrizione appropriata di hello in cui esistano risorse hello o viene fatturata per. Selezionare un ID di sottoscrizione specifico sotto l'account tramite il comando [az account set](/cli/azure/account#set).
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse
Creare un [gruppo di risorse](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) utilizzando hello [gruppo az creare](https://docs.microsoft.com/cli/azure/group#create) comando. Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite come gruppo.

esempio Hello crea un gruppo di risorse denominato `myresourcegroup` in hello `westus` percorso.

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>Creare un database di Azure per il server MySQL
Creare un Database di Azure per il server MySQL con hello **creare server mysql az** comando. Un server può gestire più database. In genere, viene usato un database separato per ogni progetto o per ogni utente.

esempio Hello crea un Database di Azure per il server MySQL situato in `westus` nel gruppo di risorse hello `myresourcegroup` con nome `myserver4demo`. Hello server dispone di un accesso di amministratore in denominato `myadmin` e la password `Password01!`. Hello server viene creato con **base** livello di prestazioni e **50** unità condivisa tra tutti i database hello server hello di calcolo. È possibile applicare la scalabilità di calcolo e archiviazione verso l'alto o verso il basso a seconda delle esigenze dell'applicazione hello.

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>Configurare una regola del firewall
Creare un Database di Azure per la regola del firewall a livello di server MySQL mediante hello **az mysql regola firewall del server-creare** comando. Una regola del firewall a livello di server consente a un'applicazione esterna, ad esempio hello **mysql.exe** strumento da riga di comando o un server di tooyour tooconnect MySQL Workbench tramite firewall del servizio Azure MySQL hello. 

Hello esempio seguente viene creata una regola del firewall per un intervallo di indirizzi predefiniti, ovvero in questo esempio hello intera possibili intervallo di indirizzi IP.

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a>Configurare le impostazioni SSL
Per impostazione predefinita, tra il server e le applicazioni client vengono applicate connessioni SSL.  In questo modo di sicurezza di "in movimento" hello di dati mediante la crittografia di flusso di dati hello su internet.  toomake questa rapida più semplice, abbiamo disabilitato le connessioni SSL per il server.  Questo comportamento non è consigliato per i server di produzione.  Per ulteriori informazioni, vedere [connettività configurare SSL in toosecurely l'applicazione connessione tooAzure Database MySQL](./howto-configure-ssl.md).

Hello esempio seguente viene disabilitato l'applicazione SSL sul server MySQL.
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-hello-connection-information"></a>Ottenere informazioni sulla connessione hello

tooconnect tooyour server, sono necessarie credenziali di accesso e le informazioni di host tooprovide.

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

il risultato di Hello è nel formato JSON. Prendere nota di hello **fullyQualifiedDomainName** e **administratorLogin**.
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "myserver4demo.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforMySQL/servers/myserver4demo",
  "location": "westus",
  "name": "myserver4demo",
  "resourceGroup": "myresourcegroup",
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

## <a name="connect-toohello-server-using-hello-mysqlexe-command-line-tool"></a>Connessione server toohello utilizzando lo strumento da riga di comando di hello mysql.exe
Connessione server tooyour utilizzando hello **mysql.exe** strumento da riga di comando. È possibile scaricare MySQL da [qui](https://dev.mysql.com/downloads/) e installarlo nel computer in uso. È invece possibile scegliere hello **Provalo** pulsante esempi di codice o hello `>_` pulsante hello superiore destro della barra degli strumenti in hello portale di Azure e avviare hello **Azure Cloud Shell**.

Digitare i comandi successivi hello: 

1. Connessione tramite server toohello **mysql** strumento da riga di comando:
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. Visualizzare lo stato del server:
```sql
 mysql> status
```
Se tutto va bene, lo strumento da riga di comando hello deve restituire come output hello seguente testo:

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome toohello MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.

mysql> status
--------------
mysql  Ver 14.14 Distrib 5.6.35, for Win64 (x86_64)

Connection id:          65512
Current database:
Current user:           myadmin@116.230.243.143
SSL:                    Not in use
Using delimiter:        ;
Server version:         5.6.26.0 MySQL Community Server (GPL)
Protocol version:       10
Connection:             myserver4demo.mysql.database.azure.com via TCP/IP
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    gbk
Conn.  characterset:    gbk
TCP port:               3306
Uptime:                 2 days 9 hours 47 min 20 sec

Threads: 4  Questions: 34833  Slow queries: 2  Opens: 84  Flush tables: 4  Open tables: 1  Queries per second avg: 0.167
--------------

mysql>
```

> [!TIP]
> Per altri comandi, vedere il capitolo 4.5.1 di [MySQL 5.7 Reference Manual](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) (Manuale di riferimento di MySQL 5.7).

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a>Connessione server toohello strumento GUI Workbench MySQL hello
1.  Avviare hello applicazione Workbench di MySQL nel computer client. È possibile scaricare e installare MySQL Workbench da [qui](https://dev.mysql.com/downloads/workbench/).

2.  In hello **il programma di installazione nuova connessione** finestra di dialogo immettere le seguenti informazioni hello **parametri** scheda:

   ![Setup New Connection (Configura nuova connessione)](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| **Impostazione** | **Valore consigliato** | **Descrizione** |
|---|---|---|
|   Connection Name (Nome connessione) | Connessione in uso | Specificare un'etichetta per la connessione (può essere qualsiasi nome) |
| Connection Method (Metodo di connessione) | Scegliere Standard (TCP/IP) | Utilizzare TCP/IP protocollo tooconnect tooAzure Database per MySQL > |
| Nome host | myserver4demo.mysql.database.azure.com | Nome del server annotato in precedenza. |
| Porta | 3306 | viene utilizzata la porta predefinita Hello per MySQL. |
| Username | myadmin@myserver4demo | Hello amministratore account di accesso server annotato in precedenza. |
| Password | **** | Utilizzare password dell'account admin hello configurati in precedenza. |

Fare clic su **Test connessione** tootest se tutti i parametri siano configurati correttamente.
A questo punto, è possibile fare clic su connessione hello toosuccessfully connettersi toohello server.

## <a name="clean-up-resources"></a>Pulire le risorse
Se queste risorse non è necessario per un altro conosca, è possibile eliminare effettuando hello comando seguente: 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Progettare un database MySQL con l'interfaccia della riga di comando di Azure](./tutorial-design-database-using-cli.md)
