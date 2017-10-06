---
title: aaaCreate e gestire i Database di Azure per le regole firewall di MySQL mediante hello portale di Azure | Documenti Microsoft
description: Creare e gestire i Database di Azure per le regole firewall di MySQL mediante hello portale di Azure
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 30dbdde4299df564fbf6581419e908186fe3b823
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-hello-azure-portal"></a>Creare e gestire i Database di Azure per le regole firewall di MySQL mediante hello portale di Azure
Le regole del firewall a livello di server abilitare tooaccess agli amministratori un Database di Azure per il MySQL Server da un indirizzo IP specifico o l'intervallo di indirizzi IP. 

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Creare una regola del firewall a livello di server nel portale di Azure hello

1. Nel Pannello di server MySQL hello, in impostazioni fare clic su **sicurezza della connessione** tooopen hello sicurezza della connessione pannello hello Database di Azure per MySQL.

   ![Portale di Azure: fare clic su Sicurezza connessione](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Fare clic su **Aggiungi IP My** nella barra degli strumenti di hello toocreate una regola con indirizzo IP di hello del computer, in base alla percezione hello sistema Azure.

   ![Portale di Azure: fare clic su Aggiungi indirizzo IP corrente](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Verificare l'indirizzo IP prima di salvare la configurazione hello. In alcune situazioni, l'indirizzo IP hello osservato dal portale di Azure è diverso dall'indirizzo IP hello utilizzato quando l'accesso a hello internet e i server Azure. Di conseguenza, potrebbe essere necessario toochange IP iniziale e finale IP toomake hello regola funzione hello come previsto.

   Utilizzare un motore di ricerca o altri toocheck strumento online il proprio indirizzo IP (ad esempio, cercare "Qual è l'indirizzo IP").

   ![Ricerca del proprio indirizzo IP in Bing](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. Aggiungere altri intervalli di indirizzi. Nelle regole di hello per hello Azure Database MySQL firewall, è possibile specificare un singolo indirizzo IP o un intervallo di indirizzi. Se si desidera toolimit hello regola tooone singolo indirizzo IP, hello tipo stesso indirizzo nel campo hello per IP iniziale e IP finale. Apertura firewall hello consente tooaccess amministratori e utenti di qualsiasi database hello toowhich di server MySQL disporre di credenziali valide.

   ![Portale di Azure: regole del firewall ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. Fare clic su **salvare** su hello toosave barra degli strumenti la regola del firewall a livello di server. Attendere la conferma hello hello regole del firewall toohello aggiornamento ha avuto esito positivo.

   ![Portale di Azure: fare clic su Salva](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a>Gestire le regole firewall di livello server esistente tramite hello portale di Azure
Ripetere le regole del firewall di hello passaggi toomanage hello.
* tooadd hello correnti del computer, fare clic su **+ Aggiungi IP My**.
* indirizzi IP aggiuntivi tooadd, digitare hello **nome regola**, **IP iniziale**, e **IP finale**.
* toomodify una regola esistente, fare clic su uno dei campi di hello nella regola hello e modificare.
* regola toodelete esistente, fare clic sui puntini di sospensione hello […] e scegliere **eliminare**.
* Fare clic su **salvare** modifiche hello toosave.

## <a name="next-steps"></a>Passaggi successivi
- Per informazioni sulla connessione tooan Database di Azure per il server MySQL, vedere [raccolte di connessioni per il Database di Azure per MySQL](./concepts-connection-libraries.md)
