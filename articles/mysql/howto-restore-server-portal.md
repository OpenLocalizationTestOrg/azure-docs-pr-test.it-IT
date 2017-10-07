---
title: aaaHow tooRestore un Server di Database di Azure per MySQL | Documenti Microsoft
description: Questo articolo viene descritto come un server di Database di Azure per l'utilizzo di MySQL toorestore hello portale di Azure.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b990d5b37c5d4924de9571192b923e3c81094ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-mysql-using-hello-azure-portal"></a>Come tooBackup e il ripristino di un server di Database di Azure per l'utilizzo di MySQL hello portale di Azure

## <a name="backup-happens-automatically"></a>Il backup viene eseguito automaticamente
Quando si utilizza il Database di Azure per MySQL, il servizio di database hello rende automaticamente un backup del servizio hello ogni 5 minuti. 

Quando si utilizza il livello di base e 35 giorni, sono disponibili per 7 giorni backup di Hello quando si usa il livello Standard. Per altre informazioni, vedere [Livelli di servizio del Database di Azure per MySQL](concepts-service-tiers.md)

Utilizzare questa funzionalità di backup automatico è possibile ripristinare server hello e tutti i database in un nuovo server tooan precedente punto nel tempo.

## <a name="restore-in-hello-azure-portal"></a>Ripristinare nel portale di Azure hello
Il Database di Azure per MySQL consente toorestore hello server back-tooa punto nel tempo e in tooa nuova copia del server di hello. È possibile utilizzare questo nuovo toorecover server i dati. 

Ad esempio, se una tabella è stato accidentalmente eliminato a mezzogiorno oggi, si potrebbe ripristinare toohello ora prima di mezzogiorno e recuperare hello mancante nella tabella e i dati dalla nuova copia del server di hello.

Hello seguenti passaggi punto di ripristino hello esempio server tooa nel tempo:

1. Sign in hello [portale di Azure](https://portal.azure.com/)

2. Individuare il Database di Azure per il server MySQL. Nel riquadro sinistro hello selezionare **tutte le risorse**, quindi selezionare il server dall'elenco di hello.

3.  Nella parte superiore di hello del pannello della panoramica hello server, fare clic su **ripristinare** sulla barra degli strumenti hello. verrà visualizzata la finestra di pannello Ripristina Hello.
![fare clic sul pulsante Ripristina](./media/howto-restore-server-portal/click-restore-button.png)

4. Compilare il modulo ripristino hello con le informazioni necessarie hello:

- **(UTC) punto di ripristino**: utilizzando selezione data hello e selezione ora, selezionare toorestore un punto nel tempo per. tempo Hello specificato è in formato UTC, pertanto è possibile sia necessario tooconvert hello locale ora in formato UTC.
- **Ripristinare il server toonew**: fornire un nuovo server di server esistente nome toorestore hello in.
- **Percorso**: hello area scelta automaticamente compilata con l'area del server di origine hello e non può essere modificato.
- **Livello di prezzo**: hello prezzi scelta livello automaticamente popola con hello prezzi stesso livello del server di origine hello e non possono essere modificate qui. 
![Ripristino temporizzato](./media/howto-restore-server-portal/pitr-restore.png)

5. Fare clic su **OK** toorestore hello server toorestore tooa punto nel tempo. 

6. Al termine del ripristino di hello, individuare hello nuovo server in cui è stato creato hello tooverify sono stati ripristinati i database, come previsto.

## <a name="next-steps"></a>Passaggi successivi
- [Raccolte connessioni per il Database di Azure per MySQL](concepts-connection-libraries.md)