---
title: aaaCreate e gestire i Database di Azure per le regole firewall PostgreSQL utilizzando hello portale di Azure | Documenti Microsoft
description: Creare e gestire i Database di Azure per le regole firewall PostgreSQL utilizzando hello portale di Azure
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6a41a077168657769e442401e9df9931aa809240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-hello-azure-portal"></a>Creare e gestire i Database di Azure per le regole firewall PostgreSQL utilizzando hello portale di Azure
Le regole del firewall a livello di server abilitare tooaccess agli amministratori un Database di Azure per PostgreSQL Server da un indirizzo IP specifico o l'intervallo di indirizzi IP. 

## <a name="prerequisites"></a>Prerequisiti
toostep tramite questa procedura-tooguide, è necessario:
- Un server [Creare un database di Azure per PostgreSQL](quickstart-create-server-database-portal.md)

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Creare una regola del firewall a livello di server nel portale di Azure hello
1. Nel Pannello di server PostgreSQL hello, in impostazioni fare clic su **sicurezza della connessione** tooopen hello sicurezza della connessione pannello hello Azure Database PostgreSQL.

  ![Portale di Azure: fare clic su Sicurezza connessione](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Fare clic su **Aggiungi IP My** sulla barra degli strumenti hello. Questa viene creata automaticamente una regola con indirizzo IP di hello del computer, come percepito da hello sistema Azure.

  ![Portale di Azure: fare clic su Aggiungi indirizzo IP corrente](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Verificare l'indirizzo IP prima di salvare la configurazione hello. In alcune situazioni, l'indirizzo IP hello osservato dal portale di Azure è diverso dall'indirizzo IP hello utilizzato quando l'accesso a hello internet e i server Azure. Di conseguenza, potrebbe essere necessario toochange IP iniziale e finale IP toomake hello regola funzione hello come previsto.
Utilizzare un motore di ricerca o altri toocheck strumento online il proprio indirizzo IP (ad esempio, ricerca Bing "che cos'è l'IP").

  ![Ricerca Bing di What is my IP](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. Aggiungere altri intervalli di indirizzi. Nelle regole di hello per hello Azure Database PostgreSQL firewall, è possibile specificare un singolo indirizzo IP o un intervallo di indirizzi. Se si desidera toolimit hello regola tooone singolo indirizzo IP, hello tipo stesso indirizzo nel campo hello per IP iniziale e IP finale. Apertura firewall hello consente di utenti e amministratori di database di tooany toologin su hello PostgreSQL server toowhich disporre di credenziali valide.

  ![Portale di Azure: regole del firewall ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. Fare clic su **salvare** su hello toosave barra degli strumenti la regola del firewall a livello di server. Attendere la conferma hello hello regole del firewall toohello aggiornamento ha avuto esito positivo.

  ![Portale di Azure: fare clic su Salva](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a>Gestire le regole firewall di livello server esistente tramite hello portale di Azure
Ripetere le regole del firewall di hello passaggi toomanage hello.
* tooadd hello correnti del computer, fare clic su pulsante hello troppo + **Aggiungi IP My**. Fare clic su **salvare** modifiche hello toosave.
* indirizzi IP aggiuntivi tooadd, digitare hello regola nome, indirizzo IP iniziale e l'indirizzo IP finale. Fare clic su **salvare** modifiche hello toosave.
* toomodify una regola esistente, fare clic su uno dei campi di hello nella regola hello e modificare. Fare clic su **salvare** modifiche hello toosave.
* toodelete una regola esistente, fare clic sui puntini di sospensione hello […] e fare clic su Rimuovi Elimina regola di hello. Fare clic su **salvare** modifiche hello toosave.

## <a name="next-steps"></a>Passaggi successivi
- Analogamente, è possibile generare script troppo[creare e gestire i Database di Azure per le regole firewall PostgreSQL mediante Azure CLI](howto-manage-firewall-using-cli.md)
- Per informazioni sulla connessione tooan Database di Azure per server PostgreSQL, vedere [raccolte di connessioni per il Database di Azure per PostgreSQL](concepts-connection-libraries.md)
