---
title: Come tooback di backup e ripristino di un server di Database di Azure per PostgreSQL | Documenti Microsoft
description: Informazioni su come tooback backup e ripristino da un server di Database di Azure per PostgreSQL utilizzando hello CLI di Azure.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 0b9ed25e3e3a88dd5c7ffe2ae7c27f8eef9be710
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-hello-azure-cli"></a>Come tooback backup e ripristino da un server di Database di Azure per PostgreSQL utilizzando hello CLI di Azure

Utilizzare il Database di Azure per PostgreSQL toorestore un tooan di database del server Data precedente che si estende da 7 giorni too35.

## <a name="prerequisites"></a>Prerequisiti
toocomplete questo come-tooguide, è necessario:
- Un [server e un database di Database di Azure per PostgreSQL](quickstart-create-server-database-azure-cli.md)

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> Se si installa e utilizza hello CLI di Azure localmente, questa procedura-tooguide richiede l'utilizzo di Azure CLI versione 2.0 o versione successiva. versione di hello tooconfirm, al prompt dei comandi di hello CLI di Azure, immettere `az --version`. tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="back-up-happens-automatically"></a>Il backup viene eseguito automaticamente
Quando si utilizza il Database di Azure per PostgreSQL, servizio database hello esegue automaticamente il backup del servizio di hello ogni 5 minuti. 

Per il livello di base, sono disponibili backup hello per 7 giorni. Per il livello Standard, i backup hello sono disponibili per 35 giorni. Per altre informazioni, vedere [Piano tariffario di Database di Azure per PostgreSQL](concepts-service-tiers.md).

Con questa funzionalità di backup automatico, è possibile ripristinare il server di hello e tooan il database Data precedente o punto nel tempo.

## <a name="restore-a-database-tooa-previous-point-in-time-by-using-hello-azure-cli"></a>Ripristinare un punto precedente tooa di database nel tempo tramite hello CLI di Azure
Utilizzare il Database di Azure per PostgreSQL toorestore hello server tooa precedente punto nel tempo. i dati ripristinato Hello sono copiato tooa nuovo server e server esistente hello viene lasciato invariato. Se, ad esempio, una tabella viene accidentalmente eliminata a mezzogiorno oggi, è possibile ripristinare toohello tempo prima di mezzogiorno. Quindi, è possibile recuperare hello mancante nella tabella e i dati dalla copia ripristinata hello del server di hello. 

server hello toorestore, utilizzare hello Azure CLI [ripristino del server postgres az](/cli/azure/postgres/server#restore) comando.

### <a name="run-hello-restore-command"></a>Eseguire il comando di ripristino hello

server hello toorestore, al prompt dei comandi di hello CLI di Azure, immettere hello comando seguente:

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

Hello `az postgres server restore` comando richiede hello seguenti parametri:
| Impostazione | Valore consigliato | Descrizione  |
| --- | --- | --- |
| resource-group |  myResourceGroup |  Il gruppo di risorse in cui è presente il server di origine hello.  |
| name | mypgserver-restored | nome di Hello del server di nuovo hello viene creato dal comando di ripristino hello. |
| restore-point-in-time | 2017-04-13T13:59:00Z | Selezionare un punto nel tempo toorestore per. Questa data e ora deve essere compresa hello del server di origine eseguire il backup periodo di memorizzazione. Utilizzare il formato di data e ora hello ISO8601. È possibile usare il proprio fuso orario locale, ad esempio `2017-04-13T05:59:00-08:00`. È inoltre possibile utilizzare hello UTC Zulu formato, ad esempio, `2017-04-13T13:59:00Z`. |
| source-server | mypgserver-20170401 | Hello nome o ID di hello origine server toorestore da. |

Quando si ripristina un server tooan punto nel tempo precedente, viene creato un nuovo server. server originale Hello e i relativi database da hello specificato punto nel tempo vengono copiati toohello nuovo server.

valori di livello di posizione e prezzi Hello per server hello ripristinato rimangono hello stesso come server originale hello. 

Hello `az postgres server restore` comando è sincrono. Dopo il ripristino del server hello, è possibile utilizzare il nuovo toorepeat hello processo per un altro punto nel tempo. 

Dopo hello ripristino configurazione di processo è completato, individuare il nuovo server di hello e verificare che i dati hello vengano ripristinati come previsto.

## <a name="next-steps"></a>Passaggi successivi
[Raccolte connessioni per il Database di Azure per PostgreSQL](concepts-connection-libraries.md)
