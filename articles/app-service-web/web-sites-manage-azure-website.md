---
title: aaaManage un'app web nel servizio App di Azure
description: Tooresources collegamenti per la gestione di un'app web nel servizio App di Azure.
services: app-service\web
documentationcenter: 
author: erikre
manager: erikre
editor: 
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: daf69245e66068b0e97e3ae1c3fb5fce45605b91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a>Scalare un'app Web in Servizio app di Azure
In questo argomento contiene collegamenti tooresources per la gestione di un'app web nel [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). La gestione include tutte le attività hello che consentono di mantenere l'app web in esecuzione senza problemi. 

Nel corso della durata hello di un'app web, verranno eseguite diverse operazioni di gestione, si sposta da operazione toonormal distribuzione iniziale degli aggiornamenti e manutenzione.

Molte attività di gestione di app web possono essere eseguite in hello portale di Azure.

## <a name="before-you-deploy-your-web-app-tooproduction"></a>Prima di distribuire il tooproduction app web
### <a name="choose-a-tier"></a>Scegliere un livello
Servizio di applicazione Azure è disponibile in cinque livelli: libero, Shared, Basic, Standard e Premium. Per informazioni sulle funzionalità di hello e sui prezzi per ogni livello, vedere [prezzi](https://azure.microsoft.com/pricing/details/app-service/). 

* [Piani di servizio app](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) consentono di raggruppare più App web in hello stesso livello.
* È sempre possibile [cambiare livello](web-sites-scale.md) dopo aver creato il sito Web.

### <a name="configuration"></a>Configurazione
Hello utilizzare [portale Azure](https://portal.azure.com/) tooset varie opzioni di configurazione. Per informazioni dettagliate, vedere [Configurazione delle app Web in Servizio app di Azure](web-sites-configure.md). Di seguito è riportato un rapido elenco di controllo:

* Selezionare le **versioni runtime** per .NET, PHP, Java o Python, se necessario.
* Abilitare **WebSocket** se l'app web Usa protocollo WebSocket hello. Sono incluse le app che usano [ASP.NET SignalR](http://www.asp.net/signalr) o [socket.io](web-sites-nodejs-chat-app-socketio.md).
* Sul sito vengono eseguiti lavori Web continui? In caso affermativo, abilitare l'opzione **Sempre attivo**.
* Set hello **documento predefinito**, ad esempio index.html.

Nelle impostazioni di configurazione di base toothese aggiunta, è necessario seguente hello tooconfigure:

* **Secure Socket Layer (SSL)** . toouse SSL con un nome di dominio personalizzato, è necessario ottenere un SSL dei certificati e configurare il toouse app web è. Vedere [Abilitazione di HTTPS per un'app Web nel servizio app di Azure](app-service-web-tutorial-custom-ssl.md).
* **Nome di dominio personalizzato.** L'applicazione web dispone automaticamente un sottodominio in azurewebsites.net. È possibile associare un nome di dominio personalizzato, ad esempio contoso.com. Vedere [Configurazione di un nome di dominio personalizzato nel servizio app di Azure](app-service-web-tutorial-custom-domain.md).

Configurazione specifica per ciascun linguaggio:

* **PHP**: [Configurazione di PHP nelle app Web di Servizio app di Azure](web-sites-php-configure.md).
* **Python**: [configurazione Python con Azure applicazione servizio Web App](web-sites-python-configure.md)

## <a name="while-your-web-app-is-running"></a>Durante l'esecuzione di un'applicazione web
Mentre l'app web è in esecuzione, si desidera che sia disponibile e che si adatta il traffico utente toomeet toomake. È necessario anche tootroubleshoot errori.

### <a name="monitoring"></a>Monitoraggio
* Tramite il portale di Azure hello, è possibile [aggiungere metriche delle prestazioni](web-sites-monitor.md) , ad esempio l'utilizzo della CPU e numero di richieste client.
* [Ridimensionare l'app web](web-sites-scale.md) in tootraffic di risposta. A seconda del livello, è possibile scalare il numero di hello di macchine virtuali e/o di dimensioni hello di istanze VM hello. In hello Standard e i livelli Premium, è possibile anche impostare il ridimensionamento automatico in modo da app web si adatta automaticamente, in base a una pianificazione fissa o in tooload di risposta.  

### <a name="backups"></a>Backup
* Impostare i [backups automatici](web-sites-backup.md) del sito Web. Ulteriori informazioni sui backup sono disponibili in [questo video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).
* Informazioni sulle opzioni di hello per [il ripristino del database](../sql-database/sql-database-business-continuity.md) nel Database di SQL Azure.

### <a name="troubleshooting"></a>Risoluzione dei problemi
* Se si verificano problemi, è possibile [risoluzione dei problemi in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), utilizzando i log di diagnostica e il debug nel cloud hello attivo. 
* All'esterno di Visual Studio, esistono diversi modi toocollect i log di diagnostica. Vedere [Abilitazione della registrazione diagnostica per app Web nel servizio app di Azure](web-sites-enable-diagnostic-log.md).
* Per le applicazioni Node.js, vedere [come toodebug un Node.js web app in Azure App Service](web-sites-nodejs-debug.md).

### <a name="restoring-data"></a>Ripristino dei dati
* [Ripristino](web-sites-restore.md) di un sito Web di cui si era eseguito un backup in precedenza.

## <a name="when-you-update-your-web-app"></a>Durante l'aggiornamento del sito Web
Se non sono stati abilitati i backup automatici, è possibile creare un [backup manuale](web-sites-backup.md).

Valutare l'opportunità di applicare una [distribuzione a fasi](web-sites-staged-publishing.md). Questa opzione consente di pubblicare aggiornamenti tooa distribuzione che viene eseguito side-by-side di gestione temporanea con la distribuzione di produzione. 


<!-- Anchors. -->

[Before you deploy your site tooproduction]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


