---
title: Come eseguire il backup e ripristinare un server nel Database di Azure per MySQL | Microsoft Docs
description: Informazioni su come eseguire la procedura di backup e ripristino di un server in Database di Azure per MySQL tramite l'interfaccia della riga di comando di Azure.
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 11/28/2017
ms.openlocfilehash: 44b3c68b8df4006d3fe087e5ad4118d7616d3d9a
ms.sourcegitcommit: 29bac59f1d62f38740b60274cb4912816ee775ea
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/29/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-mysql-by-using-the-azure-cli"></a>Come eseguire la procedura di backup e ripristino di un server in Database di Azure per MySQL tramite l'interfaccia della riga di comando di Azure

Usare Database di Azure per MySQL per ripristinare il database di un server a una data precedente che va dai 7 ai 35 giorni.

## <a name="prerequisites"></a>Prerequisiti
Per completare questa guida, è necessario:
- Un [database di Azure per il database e il server MySQL](quickstart-create-mysql-server-database-using-azure-portal.md)

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

> [!IMPORTANT]
> Se si installa e si usa l'interfaccia della riga di comando in locale, per questa guida è necessario usare la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure. Per verificare la versione, al prompt dei comandi dell'interfaccia della riga di comando di Azure immettere `az --version`. Per eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).

## <a name="backup-happens-automatically"></a>Il backup viene eseguito automaticamente
Quando si usa Database di Azure per MySQL, il servizio di database esegue automaticamente il backup del servizio ogni 5 minuti. 

Per il livello di base, il servizio di backup è disponibile per 7 giorni. Per il livello standard, il servizio di backup è disponibile per 35 giorni. Per altre informazioni, vedere [Piano tariffario di Database di Azure per MySQL](concepts-service-tiers.md).

Con questa funzionalità di backup automatico è possibile ripristinare il server e i suoi database a una data precedente o a un precedente punto nel tempo.

## <a name="restore-a-database-to-a-previous-point-in-time-by-using-the-azure-cli"></a>Ripristinare un database a un momento precedente con l'interfaccia della riga di comando di Azure
Usare Database di Azure per MySQL per ripristinare il server a un momento precedente. I dati ripristinati vengono copiati in un nuovo server e il server esistente viene lasciato invariato. Se, ad esempio, una tabella è stata involontariamente eliminata a mezzogiorno di oggi, è possibile eseguire il ripristino a un qualsiasi momento prima di mezzogiorno. È possibile quindi recuperare la tabella e i dati mancanti dalla copia ripristinata del server. 

Per ripristinare il server, usare il comando [az mysql server restore](/cli/azure/mysql/server#az_mysql_server_restore) dell'interfaccia della riga di comando di Azure.

### <a name="run-the-restore-command"></a>Eseguire il comando di ripristino

Per ripristinare il server, al prompt dei comandi dell'interfaccia della riga di comando di Azure immettere il comando seguente:

```azurecli-interactive
az mysql server restore --resource-group myResourceGroup --name myserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server myserver4demo
```

Il comando `az mysql server restore` richiede i parametri seguenti:
| Impostazione | Valore consigliato | Descrizione  |
| --- | --- | --- |
| resource-group | myResourceGroup |  Il gruppo di risorse in cui si trova il server di origine.  |
| name | myserver-restored | Il nome del nuovo server creato con il comando di ripristino. |
| restore-point-in-time | 2017-04-13T13:59:00Z | Selezionare un punto nel tempo per il ripristino. La data e l'ora devono trovarsi all'interno del periodo di memorizzazione dei backup del server di origine. Usare il formato ISO8601 per la data e l'ora. È possibile usare il proprio fuso orario locale, ad esempio `2017-04-13T05:59:00-08:00`. È anche possibile usare il formato UTC Zulu, ad esempio `2017-04-13T13:59:00Z`. |
| source-server | myserver4demo | Il nome o l'ID del server di origine da cui eseguire il ripristino. |

Quando si ripristina un server a un punto precedente nel tempo, viene creato un nuovo server. Il server originale e i database dal punto nel punto specificato vengono copiati nel nuovo server.

I valori relativi al percorso e al piano tariffario per il server ripristinato sono gli stessi del server di origine. 

Il comando `az mysql server restore` è sincrono. Dopo il ripristino, il server può essere usato di nuovo per ripetere il processo per un altro punto nel tempo. 

Al termine del ripristino, individuare il nuovo server creato per verificare che il ripristino dei dati sia avvenuto come previsto.

## <a name="next-steps"></a>Passaggi successivi
[Raccolte connessioni per il Database di Azure per MySQL](concepts-connection-libraries.md)
