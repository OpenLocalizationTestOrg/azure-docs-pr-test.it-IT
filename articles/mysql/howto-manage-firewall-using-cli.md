---
title: Creare e gestire le regole del firewall di Database di Azure per MySQL tramite l'interfaccia della riga di comando di Azure | Microsoft Docs
description: Questo articolo descrive come creare e gestire regole del firewall di Database di Azure per MySQL tramite l'interfaccia della riga di comando di Azure.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 9a03722e9f71be307bdbf0b846a4cbf7b34cd7ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a>Creare e gestire regole del firewall di Database di Azure per MySQL tramite l'interfaccia della riga di comando di Azure
Le regole del firewall a livello di server consentono agli amministratori di gestire l'accesso a un'istanza di Database di Azure per il server MySQL da uno specifico indirizzo IP o intervallo di indirizzi IP. Usando pratici comandi dell'interfaccia della riga di comando di Azure è possibile creare, aggiornare, eliminare, elencare e visualizzare le regole del firewall per gestire il server. Per una panoramica dei firewall di Database di Azure per MySQL, vedere [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md) (Regole del firewall di Database di Azure per il server MySQL)

## <a name="prerequisites"></a>Prerequisiti
* [Installare l'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)
* Installare Azure Python SDK per PostgreSQL e i servizi MySQL
* Installare il componente dell'interfaccia della riga di comando di Azure per PostgreSQL e i servizi MySQL
* Creare un'istanza di Database di Azure per il server MySQL

## <a name="firewall-rule-commands"></a>Comandi per le regole del firewall:
Il comando **az mysql server firewall-rule** viene usato dall'interfaccia della riga di comando di Azure per creare, eliminare, elencare, visualizzare e aggiornare le regole del firewall.

Comandi:
- **create**: creare una regola del firewall del server MySQL di Azure.
- **delete**: eliminare una regola del firewall del server MySQL di Azure.
- **list**: elencare le regole del firewall del server MySQL di Azure.
- **show**: visualizzare i dettagli di una regola del firewall del server MySQL di Azure.
- **update**: aggiornare una regola del firewall del server MySQL di Azure.

## <a name="login-to-azure-and-list-your-azure-database-for-mysql-servers"></a>Accedere ad Azure ed elencare le istanze di Database di Azure per i server MySQL
Connettere in modo sicuro l'interfaccia della riga di comando di Azure all'account Azure. A tale scopo, usare il comando **az login**.

1. Eseguire il comando seguente dalla riga di comando.
```azurecli
az login
```
Questo comando restituirà un codice da usare nel passaggio successivo.

2. Usare un Web browser per aprire la pagina [https://aka.ms/devicelogin](https://aka.ms/devicelogin) e immettere il codice.

3. Al prompt dei comandi, accedere usando le credenziali di Azure.

4. Dopo che l'accesso è stato autorizzato, nella console verrà visualizzato un elenco di sottoscrizioni. Copiare l'ID della sottoscrizione desiderata per impostare la sottoscrizione corrente da usare per procedere.
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. Elencare le istanze di Database di Azure per i server MySQL per la sottoscrizione e il gruppo di risorse, se non si è certi dei nomi.

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   Prendere nota dell'attributo del nome nell'elenco, che verrà usato per specificare il server MySQL. Se necessario, verificare i dettagli del server usando l'attributo del nome per verificare che il nome sia corretto:

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a>Elencare le regole del firewall per un'istanza di Database di Azure per il server MySQL 
Usando il nome del server e il nome del gruppo di risorse, elencare le regole del firewall esistenti nel server. Si noti che l'attributo del nome server è specificato nell'opzione **--server** e non nell'opzione **--name**.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
L'output elencherà le eventuali regole presenti, per impostazione predefinita in formato JSON. È possibile usare l'opzione **--output table** per ottenere un formato di tabella più leggibile come output.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a>Creare una regola del firewall nell'istanza di Database di Azure per il server MySQL
Usando il nome del server MySQL di Azure e il nome del gruppo di risorse, creare una nuova regola del firewall nel server. Specificare un nome per la regola, oltre all'indirizzo IP iniziale e all'indirizzo IP finale per coprire un intervallo di indirizzi IP cui consentire l'accesso.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
Per consentire l'accesso a un solo indirizzo IP, specificare lo stesso valore come indirizzo IP iniziale e finale, come nell'esempio seguente.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
Al termine dell'operazione, l'output del comando elencherà i dettagli della regola del firewall creata, per impostazione predefinita in formato JSON. Se si verifica un errore, l'output visualizzerà invece il testo di un messaggio di errore.

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a>Aggiornare una regola del firewall in Database di Azure per il server MySQL 
Usando il nome del server MySQL di Azure e il nome del gruppo di risorse, aggiornare una regola del firewall esistente nel server. Specificare il nome della regola del firewall esistente come input e gli attributi dell'indirizzo IP iniziale e finale per l'aggiornamento.
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
Al termine dell'operazione, l'output del comando elencherà i dettagli della regola del firewall aggiornata, per impostazione predefinita in formato JSON. Se si verifica un errore, l'output visualizzerà invece il testo di un messaggio di errore.

> [!NOTE]
> Se la regola del firewall non esiste, verrà creata dal comando di aggiornamento.

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a>Visualizzare i dettagli di una regola del firewall in Database di Azure per il server MySQL
Usando il nome del server MySQL di Azure e il nome del gruppo di risorse, visualizzare i dettagli di una regola del firewall esistente nel server. Specificare il nome della regola del firewall esistente come input.
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
Al termine dell'operazione, l'output del comando elencherà i dettagli della regola del firewall specificata, per impostazione predefinita in formato JSON. Se si verifica un errore, l'output visualizzerà invece il testo di un messaggio di errore.

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a>Eliminare una regola del firewall in Database di Azure per il server MySQL
Usando il nome del server MySQL di Azure e il nome del gruppo di risorse, rimuovere una regola del firewall esistente dal server. Specificare il nome della regola del firewall esistente.
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
Al completamento dell'operazione non verrà visualizzato alcun output. In caso di errore, verrà restituito il testo di un messaggio di errore.

## <a name="next-steps"></a>Passaggi successivi
- Altre informazioni sulle [regole del firewall di Database di Azure per il server MySQL](./concepts-firewall-rules.md)
- [Creare e gestire regole del firewall di Database di Azure per MySQL con il portale di Azure](./howto-manage-firewall-using-portal.md)
