---
title: Come un Server di Database di Azure per PostgreSQL tooRestore | Documenti Microsoft
description: Questo articolo viene descritto come un server di Database di Azure per l'utilizzo di PostgreSQL toorestore hello portale di Azure.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: bc7351f384607397806d837afd3e1d7a26575e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-postgresql-using-hello-azure-portal"></a>Come tooBackup e il ripristino di un server di Database di Azure per l'utilizzo di PostgreSQL hello portale di Azure

## <a name="backup-happens-automatically"></a>Il backup viene eseguito automaticamente
Quando si utilizza il Database di Azure per PostgreSQL, il servizio di database hello rende automaticamente un backup del servizio hello ogni 5 minuti. 

Quando si utilizza il livello di base e 35 giorni, sono disponibili per 7 giorni backup di Hello quando si usa il livello Standard. Per altre informazioni, vedere [Livelli di servizio del Database di Azure per PostgreSQL](concepts-service-tiers.md)

Utilizzare questa funzionalità di backup automatico è possibile ripristinare server hello e tutti i database in un nuovo server tooan precedente punto nel tempo.

## <a name="restore-in-hello-azure-portal"></a>Ripristinare nel portale di Azure hello
Il Database di Azure per PostgreSQL consente toorestore hello server back-tooa punto nel tempo e in tooa nuova copia del server di hello. È possibile utilizzare questo nuovo toorecover server i dati. 

Ad esempio, se una tabella è stato accidentalmente eliminato a mezzogiorno oggi, si potrebbe ripristinare toohello ora prima di mezzogiorno e recuperare hello mancante nella tabella e i dati dalla nuova copia del server di hello.

Hello seguenti passaggi punto di ripristino hello esempio server tooa nel tempo:
1. Sign in hello [portale di Azure](https://portal.azure.com/)
2. Individuare il Database di Azure per il server PostgreSQL. Nel portale di Azure hello, fare clic su **tutte le risorse** dal menu a sinistra hello e digitare il nome di hello, ad esempio **mypgserver 20170401**, toosearch per il server esistente. Fare clic su un nome server hello elencato nei risultati di ricerca hello. Hello **Panoramica** pagina per il server viene aperto e offre opzioni per un'ulteriore configurazione.

   ![Portale di Azure - il server di ricerca toolocate](media/postgresql-howto-restore-server-portal/1-locate.png)

3. Nella parte superiore di hello del pannello della panoramica hello server, fare clic su **ripristinare** sulla barra degli strumenti hello. verrà visualizzata la finestra di pannello Ripristina Hello.

   ![Database di Azure per PostgreSQL - Panoramica - Pulsante Ripristino](./media/postgresql-howto-restore-server-portal/2_server.png)

4. Compilare il modulo ripristino hello con le informazioni necessarie hello:

   ![Database di Azure per PostgreSQL - Informazioni di ripristino ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - **Punto di ripristino**: selezionare un punto nel tempo che si verifica prima che il server di hello è stato modificato
  - **Server di destinazione**: fornire un nuovo nome del server desiderato toorestore per
  - **Percorso**: non è possibile selezionare l'area di hello, per impostazione predefinita è uguale al server di origine hello
  - **Piano tariffario**: non è possibile modificare questo valore quando si ripristina un server. È uguale al server di origine hello. 

5. Fare clic su **OK** toorestore hello server toorestore tooa punto nel tempo. 

6. Al termine del ripristino di hello, individuare hello nuovo server in cui viene creato hello tooverify ripristino dei dati nel modo previsto.

## <a name="next-steps"></a>Passaggi successivi
- [Raccolte connessioni per il Database di Azure per PostgreSQL](concepts-connection-libraries.md)
