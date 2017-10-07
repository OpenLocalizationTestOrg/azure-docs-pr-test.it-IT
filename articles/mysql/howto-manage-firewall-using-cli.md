---
title: aaaCreate e gestire i Database di Azure per le regole firewall di MySQL mediante Azure CLI | Documenti Microsoft
description: Questo articolo viene descritto come toocreate e gestire i Database di Azure per le regole firewall di MySQL mediante riga di comando CLI di Azure.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: b2f0b4ccf34ce88e3a5e72a64d3f8c78a5bc2a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a>Creare e gestire regole del firewall di Database di Azure per MySQL tramite l'interfaccia della riga di comando di Azure
Regole del firewall a livello di server abilitare amministratori toomanage accesso tooan Database di Azure per il MySQL Server da un indirizzo IP specifico o l'intervallo di indirizzi IP. Usare i comandi CLI di Azure pratici, è possibile creare, aggiornare, eliminare, elencare e Mostra toomanage regole firewall del server. Per una panoramica dei firewall di Database di Azure per MySQL, vedere [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md) (Regole del firewall di Database di Azure per il server MySQL)

## <a name="prerequisites"></a>Prerequisiti
* [Installare l'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)
* Installare Azure Python SDK per PostgreSQL e i servizi MySQL
* Installare il componente di hello CLI di Azure per i servizi MySQL e PostgreSQL
* Creare un database di Azure per il server MySQL

## <a name="firewall-rule-commands"></a>Comandi per le regole del firewall:
Hello **az mysql regola firewall del server-** comando viene utilizzato da toocreate CLI di Azure, eliminare, elenco, visualizzare e aggiornare le regole del firewall.

Comandi:
- **create**: creare una regola del firewall del server MySQL di Azure.
- **delete**: eliminare una regola del firewall del server MySQL di Azure.
- **elenco** : elenco di regole firewall del server MySQL a Azure hello.
- **Mostra** : Mostra i dettagli di hello del server MySQL a Azure regola del firewall.
- **update**: aggiornare una regola del firewall del server MySQL di Azure.

## <a name="login-tooazure-and-list-your-azure-database-for-mysql-servers"></a>TooAzure account di accesso e l'elenco di Database di Azure per il server MySQL
Connettere in modo sicuro l'interfaccia della riga di comando di Azure all'account Azure. Hello utilizzare **accesso az** comando toodo questo.

1. Eseguire hello comando seguente dalla riga di comando hello.
```azurecli
az login
```
Questo comando genera un codice toouse nel passaggio successivo hello.

2. Utilizzare la pagina web browser tooopen hello [https://aka.ms/devicelogin](https://aka.ms/devicelogin) e immettere il codice hello.

3. Al prompt dei comandi hello, accedere con le credenziali di Azure.

4. Una volta che l'account di accesso è autorizzato, un elenco di sottoscrizioni verrà stampato nella console di hello. Id di hello una copia di hello desiderato sottoscrizione tooset hello corrente sottoscrizione toobe usato in futuro.
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. Elenco hello i database di Azure per i server di MySQL per il gruppo di risorse e di sottoscrizione se non si è certi di nomi di hello.

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   Si noti hello attributo del nome in hello elenco, che sarà utilizzato toospecify quali toowork di server MySQL in. Se necessario, verificare i dettagli di hello toousing hello Nome attributo tooconfirm il nome del server sia corretto:

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a>Elencare le regole del firewall per un'istanza di Database di Azure per il server MySQL 
Utilizzando il nome di server hello e nome gruppo di risorse hello, elenco hello esistente regole del firewall nel server di hello. L'attributo nome server hello è specificato in hello **-server** passa e non hello **-nome** passare.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
output di Hello elencherà regole hello, se presente, per impostazione predefinita in JSON di formato. È possibile utilizzare l'opzione hello **-tabella di output** per un formato più leggibile di tabella come output di hello.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a>Creare una regola del firewall nell'istanza di Database di Azure per il server MySQL
Nome del server MySQL a Azure hello e nome del gruppo di risorse hello di creare una nuova regola firewall nel server di hello. Specificare un nome per la regola hello, indirizzo IP iniziale hello e IP finale per hello regola toocover un accesso tooallow di indirizzi IP dell'intervallo.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
Per un indirizzo IP specifico indirizzo toobe consentito l'accesso, fornire hello stesso indirizzo come hello IP iniziale e IP finale, come nel seguente esempio.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
Al completamento dell'operazione, l'output del comando hello elencherà dettagli hello hello regola del firewall creata per impostazione predefinita in formato JSON. Se si verifica un errore, output di hello mostrerà testo messaggio di errore.

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a>Aggiornare una regola del firewall in Database di Azure per il server MySQL 
Usa nome del server MySQL a Azure hello e nome del gruppo di risorse hello, aggiornare una regola firewall esistente nel server di hello. Specificare il nome di hello della regola firewall esistente hello come input e hello inizio IP e fine IP attributi tooupdate.
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
Al completamento dell'operazione, l'output del comando hello elencherà dettagli hello hello regola del firewall che sono state aggiornate, per impostazione predefinita in formato JSON. Se si verifica un errore, output di hello mostrerà testo messaggio di errore.

> [!NOTE]
> Se non esiste una regola del firewall hello, si verrà creato dal comando di aggiornamento hello.

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a>Visualizzare i dettagli di una regola del firewall in Database di Azure per il server MySQL
Usa nome del server MySQL a Azure hello e nome del gruppo di risorse hello, dettagli hello esistente firewall regola dal server hello. Specificare il nome di hello della regola firewall esistente hello come input.
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
Al completamento dell'operazione, l'output del comando hello elencherà dettagli hello hello regola del firewall che è stato specificato, per impostazione predefinita in formato JSON. Se si verifica un errore, output di hello mostrerà testo messaggio di errore.

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a>Eliminare una regola del firewall in Database di Azure per il server MySQL
Nome del server MySQL a Azure hello e nome del gruppo di risorse hello di rimuovere una regola firewall esistente dal server di hello. Specificare il nome di hello della regola firewall esistente hello.
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
Al completamento dell'operazione non verrà visualizzato alcun output. In caso di errore, verrà restituito testo del messaggio hello.

## <a name="next-steps"></a>Passaggi successivi
- Altre informazioni sulle [regole del firewall di Database di Azure per il server MySQL](./concepts-firewall-rules.md)
- [Creare e gestire i Database di Azure per le regole firewall di MySQL mediante hello portale di Azure](./howto-manage-firewall-using-portal.md)
