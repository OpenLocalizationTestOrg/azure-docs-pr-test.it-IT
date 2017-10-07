---
title: aaaCreate e gestire i Database di Azure per il server MySQL tramite il portale di Azure | Documenti Microsoft
description: "Questo articolo descrive come è possibile creare un nuovo Database di Azure per il server MySQL e gestire rapidamente server hello utilizzando hello portale di Azure."
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c532df43b3d2124d7bd34875b32d52357f162af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a>Creare e gestire Database di Azure per il server MySQL con il portale di Azure
Questo articolo descrive come è possibile creare un nuovo Database di Azure per il server MySQL e gestire rapidamente server hello utilizzando hello portale di Azure. Gestione del server include la visualizzazione di database e i dettagli del server, la reimpostazione delle password e l'eliminazione di server hello.

## <a name="log-in-toohello-azure-portal"></a>Accedi toohello portale di Azure
Accedi toohello [portale di Azure](https://portal.azure.com).

## <a name="create-an-azure-database-for-mysql-server"></a>Creare un database di Azure per il server MySQL
Seguire questi toocreate passaggi un Database di Azure per il server MySQL denominato "mysqlserver4demo"

1-click **New** pulsante disponibile nella hello angolo superiore sinistro del portale di Azure hello.

2-selezionare **database** nuova pagina hello e selezionare **Database di Azure per MySQL** dalla pagina di database hello.

> Verrà creata un'istanza di Database di Azure per il server MySQL con un set definito di risorse di [calcolo e di archiviazione](./concepts-compute-unit-and-storage.md). Hello database viene creato all'interno di un gruppo di risorse di Azure e in un Database di Azure per il server MySQL.

![create-new-server](./media/howto-create-manage-server-portal/create-new-server.png)

3 - compilare hello Azure Database MySQL form con hello le seguenti informazioni:

| **Campo modulo** | **Descrizione campo** |
|----------------|-----------------------|
| *Server name* (Nome server) | azure-mysql. Il nome server è univoco a livello globale |
| *Sottoscrizione* | MySQLaaS. Selezionare dall'elenco a discesa |
| *Gruppo di risorse* | myresource. Creare un nuovo gruppo di risorse o usarne uno esistente |
| *Accesso amministratore server* | myadmin (configurare il nome dell'account amministratore) |
| *Password* | Definire la password dell'account amministratore |
| *Conferma password* | Confermare la password dell'account amministratore |
| *Posizione* | Europa settentrionale. La scelta è tra Europa settentrionale e Stati Uniti occidentali. |
| *Versione* | 5.6. Scegliere la versione di Database di Azure per il server MySQL |

Fare clic su 4 **tariffario** toospecify hello servizio livello di prestazioni e per il nuovo server. Il numero delle unità di calcolo può essere configurato tra 50 e 100 nel piano Basic e tra 100 e 200 nel piano Standard. È possibile aggiungere spazio di archiviazione in base alla quantità inclusa. Per questa guida si sceglieranno 50 unità di calcolo e 50 GB. Fare clic su **OK** toosave la selezione.
![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)

Fare clic su 5 **crea** server hello tooprovision. Il provisioning richiede alcuni minuti.

> Controllare hello **toodashboard Pin** rilevamento semplice di opzione tooallow delle distribuzioni.
> [!NOTE]
> Sebbene too1000GB nel livello di base e 10000GB nello Standard sarà supportato livello per l'archiviazione, per l'anteprima pubblica, archiviazione massima hello è comunque limitata too1000GB temporaneamente. 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a>Aggiornare un'istanza di Database di Azure per il server MySQL
Dopo il provisioning di nuovi server, l'utente ha 2 Opzioni tooedit un server esistente: reimpostare la password dell'amministratore o la scala su/giù server hello modificando l'unità di calcolo hello.

### <a name="change-hello-administrator-user-password"></a>Password dell'utente amministratore hello modifica
1 - server hello **Panoramica** pannello, fare clic su **reimpostazione password** toopopulate una finestra di input e Conferma password.

2 - Immettere la nuova password e Conferma password hello nella finestra di hello come indicato di seguito: ![reimpostazione della password](./media/howto-create-manage-server-portal/reset-password.png)

3-fare clic su **OK** nuova password di toosave hello.

### <a name="scale-updown-by-changing-compute-units"></a>Aumentare/ridurre le prestazioni modificando le unità di calcolo

1 - nel pannello server hello in **impostazioni**, fare clic su **tariffario** tooopen hello prezzi livello pannello hello Azure Database per il server MySQL.

2-seguire il passaggio 4 **creare un Database di Azure per il server MySQL** toochange unità di calcolo in hello stesso livello di prezzo.

## <a name="delete-an-azure-database-for-mysql-server"></a>Eliminare un'istanza di Database di Azure per il server MySQL

1 - server hello **Panoramica** pannello, fare clic su **eliminare** del Pannello di conferma eliminazione comando pulsante tooopen hello.

Nome corretto del server di tipo 2 hello nella casella di input del pannello hello conferma double.

3-fare clic su **eliminare** tooconfirm l'eliminazione di azione di nuovo il pulsante e attendere che "L'eliminazione di successo" popup nella barra di notifica hello.

## <a name="list-hello-azure-database-for-mysql-databases"></a>Elenco hello Database di Azure per i database MySQL
Nel server di hello **Panoramica** pannello, scorrere verso il basso fino a visualizzare database hello riquadro nella parte inferiore di hello. Tutti i database hello verranno elencati nella tabella hello. Fare clic su **eliminare** del Pannello di conferma eliminazione comando pulsante tooopen hello.

![show-databases](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a>Visualizzare i dettagli di un'istanza di Database di Azure per il server MySQL
Fare clic su **proprietà** in **impostazioni** sul server hello pannello aprirà hello **proprietà** blade. È quindi possibile visualizzare tutte le informazioni dettagliate sui server hello.

## <a name="next-steps"></a>Passaggi successivi

[Guida introduttiva: Creare Database di Azure per il server MySQL con il portale di Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
