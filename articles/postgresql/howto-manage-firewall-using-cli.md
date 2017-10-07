---
title: aaaCreate e gestire i Database di Azure per le regole firewall PostgreSQL mediante Azure CLI | Documenti Microsoft
description: Questo articolo viene descritto come toocreate e gestire i Database di Azure per le regole firewall PostgreSQL tramite riga di comando CLI di Azure.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 06e34c9e3996c2ec3df63191d794bc34d0ca0cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a>Creare e gestire regole del firewall di Database di Azure per PostgreSQL tramite l'interfaccia della riga di comando di Azure
Le regole del firewall a livello di server abilitare amministratori toomanage accesso tooan Database di Azure per PostgreSQL Server da un indirizzo IP specifico o l'intervallo di indirizzi IP. Usare i comandi CLI di Azure pratici, è possibile creare, aggiornare, eliminare, elencare e Mostra toomanage regole firewall del server. Per una panoramica dei firewall di Database di Azure per PostgreSQL, vedere [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md) (Regole del firewall di Database di Azure per il server PostgreSQL)

## <a name="prerequisites"></a>Prerequisiti
toostep tramite questa procedura-tooguide, è necessario:
- Un [server e un database di Database di Azure per PostgreSQL](quickstart-create-server-database-azure-cli.md)
- Installare [CLI di Azure 2.0](/cli/azure/install-azure-cli) riga di comando utilità oppure utilizzare hello Azure Cloud Shell nel browser hello.

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a>Configurare le regole del firewall di Database di Azure per PostgreSQL
Hello [az postgres regola firewall del server-](/cli/azure/postgres/server/firewall-rule) comandi sono utilizzati tooconfigure regole del firewall.

## <a name="list-firewall-rules"></a>Elencare le regole del firewall 
toolist hello esistente, le regole firewall del server nel server di hello, eseguire hello [elenco regola firewall di az postgres server](/cli/azure/postgres/server/firewall-rule#list) comando.
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
output di Hello Elenca le regole di hello, se presente, per impostazione predefinita in JSON di formato. È possibile utilizzare l'opzione hello `--output table` per un formato più leggibile di tabella come output di hello.
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a>Creare la regola del firewall
una nuova regola firewall nel server di hello, eseguire hello toocreate [az postgres regola firewall del server-creare](/cli/azure/postgres/server/firewall-rule#create) comando. 

In questo esempio consente un intervallo di tutti i server di hello tooaccess di indirizzi IP **mypgserver 20170401.postgres.database.azure.com**
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
tooallow un tooaccess di indirizzo IP specifico, fornire hello stesso indirizzo come hello IP iniziale e IP finale, come nel seguente esempio.
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
Al completamento dell'operazione, l'output del comando hello Elenca i dettagli di hello hello regola del firewall creata per impostazione predefinita in formato JSON. Se si verifica un errore, hello output invece showserror testo del messaggio.

## <a name="update-firewall-rule"></a>Aggiornare la regola del firewall 
Aggiornare una regola firewall esistente sul server hello utilizzando [aggiornamento regola firewall del server az postgres](/cli/azure/postgres/server/firewall-rule#update) comando. Specificare il nome di hello della regola firewall esistente hello come input e hello inizio IP e fine IP attributi tooupdate.
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
Al completamento dell'operazione, l'output del comando hello Elenca i dettagli di hello hello regola del firewall che sono state aggiornate, per impostazione predefinita in formato JSON. Se si verifica un errore, hello output invece showserror testo del messaggio.
> [!NOTE]
> Se non esiste una regola del firewall hello, viene creato dal comando di aggiornamento hello.

## <a name="show-firewall-rule-details"></a>Visualizzare i dettagli di una regola del firewall
È inoltre possibile visualizzare firewall esistente hello dettagli regola per un server eseguendo [Mostra regola firewall di az postgres server](/cli/azure/postgres/server/firewall-rule#show) comando.
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
Al completamento dell'operazione, l'output del comando hello Elenca i dettagli di hello hello regola del firewall che è stato specificato, per impostazione predefinita in formato JSON. Se si verifica un errore, hello output invece showserror testo del messaggio.

## <a name="delete-firewall-rule"></a>Eliminare la regola del firewall
accesso toorevoke per un intervallo IP dal server di hello, eliminare una regola firewall esistente eseguendo hello [az postgres regola firewall del server-eliminare](/cli/azure/postgres/server/firewall-rule#delete) comando. Specificare il nome di hello della regola firewall esistente hello.
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
Al completamento dell'operazione non verrà visualizzato alcun output. In caso di errore, viene restituito testo del messaggio hello.

## <a name="next-steps"></a>Passaggi successivi
- Analogamente, è possibile utilizzare un web browser troppo[creare e gestire i Database di Azure per le regole firewall PostgreSQL utilizzando hello portale di Azure](howto-manage-firewall-using-portal.md)
- Altre informazioni sulle [regole del firewall di Database di Azure per il server PostgreSQL](concepts-firewall-rules.md)
- Per informazioni sulla connessione tooan Database di Azure per server PostgreSQL, vedere [raccolte di connessioni per il Database di Azure per PostgreSQL](concepts-connection-libraries.md)
