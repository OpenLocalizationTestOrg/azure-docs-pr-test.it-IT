---
title: aaaCreate una piattaforma UWP (Universal Windows) che utilizza in App per dispositivi mobili | Documenti Microsoft
description: Seguire questa esercitazione tooget introduttive sull'utilizzo di back-end delle app mobili di Azure per lo sviluppo di app Universal Windows Platform (UWP) in c#, Visual Basic o JavaScript.
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 47124296-2908-4d92-85e0-05c4aa6db916
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: d0f57bca5a8195b8b0461b8f7a0d8516371d56a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-app"></a>Creare un'app Windows
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Panoramica
Questa esercitazione viene illustrato come del servizio app di Windows della piattaforma UWP (Universal) tooa tooadd un back-end basato su cloud. Per altre informazioni, vedere [Informazioni sulle app per dispositivi mobili](app-service-mobile-value-prop.md). di seguito Hello sono acquisizioni dello schermo da app hello completata:

![App desktop completata](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
Esecuzione in un computer desktop.

![App per telefono completata](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
Esecuzione in un telefono.

Il completamento di questa esercitazione costituisce un prerequisito per tutte le altre esercitazioni delle app per dispositivi mobili relative ad app UWP.

## <a name="prerequisites"></a>Prerequisiti
toocomplete questa esercitazione, è necessario hello seguenti:

* Un account Azure attivo. Se non si dispone di un account, è possibile iscriversi a una versione di valutazione di Azure e iniziare a too10 libero App per dispositivi mobili che è possibile continuare a usare anche il termine di valutazione. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* [Visual Studio Community 2015] o versione successiva.

## <a name="create-a-new-azure-mobile-app-backend"></a>Creare un nuovo back-end dell'app per dispositivi mobili di Azure
Seguire questi toocreate passaggi un nuova App per dispositivi mobili di back-end.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

È stato eseguito il provisioning di un back-end dell'app per dispositivi mobili di Azure che può essere usato dalle applicazioni client per dispositivi mobili. Successivamente, scaricare un progetto server di un semplice "elenco di attività" back-end e pubblicarlo tooAzure.

## <a name="configure-hello-server-project"></a>Configurare il progetto server di hello
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-client-project"></a>Scaricare ed eseguire il progetto di client hello
Dopo aver configurato il back-end dell'App per dispositivi mobili, è possibile creare una nuova app client o modificare un tooAzure di tooconnect app esistente. In questa sezione si scarica un progetto di modello di app UWP di back-end App Mobile di tooyour tooconnect personalizzato.

1. In hello **introduttiva** pannello per il back-end App Mobile, fare clic su **crea una nuova app** > **scaricare**, quindi estrarre i file di progetto hello compresso tooyour computer locale.

    ![Download del progetto di guida introduttiva di Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. (Facoltativo) Aggiungere toohello di progetto app UWP hello stessa soluzione come progetto server hello. Questo rende più semplice toodebug e i test sia hello back-end app e hello in hello stessa soluzione di Visual Studio, se si sceglie toodo questa operazione. tooadd una soluzione di toohello progetto di app UWP, è necessario utilizzare Visual Studio 2015 o versione successiva.
3. Con app UWP hello come progetto di avvio hello, premere hello F5 chiave toodeploy e app hello esecuzione.
4. Nell'app hello, digitare un testo significativo, ad esempio *esercitazione hello completo*, in hello **Insert a TodoItem** casella di testo e quindi fare clic su **salvare**.

    ![Desktop completo di guida introduttiva di Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    Consente di inviare un POST richiesta toohello nuova app per dispositivi mobili back-end che è ospitato in Azure.
5. (Facoltativo) Arrestare l'applicazione hello e riavviarla in un altro dispositivo o un emulatore per dispositivi mobili.

    ![Telefono completo di guida introduttiva di Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    Si noti che i dati salvati dal passaggio precedente hello venga caricati dalla Azure dopo l'avvio di hello app UWP.

## <a name="next-steps"></a>Passaggi successivi
* [Aggiungere app tooyour authentication](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  Informazioni su come gli utenti tooauthenticate dell'app con un provider di identità.
* [Aggiungere app tooyour di notifiche push](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  Informazioni su come le notifiche push tooadd supportano tooyour app e configurare le notifiche di push toosend App Mobile back-end toouse gli hub di notifica di Azure.
* [Abilitare la sincronizzazione offline per l'app per dispositivi mobili Xamarin.Forms](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Informazioni su come offline tooadd supportano un'applicazione con un back-end dell'App Mobile. Sincronizzazione non in linea consente agli utenti finali toointeract con un'app mobile&mdash;visualizzazione, aggiunta o modifica dei dati&mdash;anche quando è presente alcuna connessione di rete.

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203
