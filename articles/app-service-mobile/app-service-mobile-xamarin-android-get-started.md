---
title: aaaGet avviato con App mobili di Azure per le app xamarin
description: Seguire questa esercitazione tooget avviato tramite app mobili di Azure per lo sviluppo di Xamarin Android
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 81649dd3-544f-40ff-b9b7-60c66d683e60
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 38710660d9328fe3c068efca972f76aa8b6e049b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinandroid-app"></a>Creare un'app per Xamarin.Android
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Panoramica
Questa esercitazione viene illustrato come tooadd un back-end basato su cloud service tooa xamarin app. Per altre informazioni, vedere [Informazioni sulle app per dispositivi mobili](app-service-mobile-value-prop.md).

Di seguito viene riportata una schermata da app hello completata:

![][0]

Il completamento di questa esercitazione è un prerequisito per tutte le altre esercitazioni relative alle app per dispositivi mobili per Xamarin.Android.

## <a name="prerequisites"></a>Prerequisiti
toocomplete questa esercitazione, è necessario hello seguenti prerequisiti:

* Un account Azure attivo. Se non si dispone di un account, iscriversi a una versione di valutazione di Azure e ottenere le App per dispositivi mobili too10 disponibile. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* Visual Studio con Xamarin. Per le istruzioni vedere [Configurazione e installazione di Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) .

## <a name="create-an-azure-mobile-app-backend"></a>Creare un back-end dell'app per dispositivi mobili di Azure
Seguire questi toocreate passaggi un back-end dell'App Mobile.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

È stato eseguito il provisioning di un back-end dell'app per dispositivi mobili di Azure che può essere usato dalle applicazioni client per dispositivi mobili. Successivamente, scaricare un progetto server di un semplice "elenco di attività" back-end e pubblicarlo tooAzure.

## <a name="configure-hello-server-project"></a>Configurare il progetto server di hello
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinandroid-app"></a>Scaricare ed eseguire app xamarin hello
1. In **scaricare ed eseguire il progetto xamarin**, fare clic su hello **scaricare** pulsante.

      Salvare computer locale tooyour file progetto compresso hello e prendere nota del dove salvarla.
2. Hello premere **F5** progetto hello toobuild della chiave e riavviare l'applicazione hello.
3. Nell'app hello, digitare un testo significativo, ad esempio *esercitazione hello completo* e quindi fare clic su hello **Aggiungi** pulsante.

    ![][10]

    Dati richiesta hello viene inseriti nella tabella TodoItem hello. Vengono restituiti gli elementi archiviati nella tabella hello dal back-end di hello app per dispositivi mobili e i dati vengono visualizzati nell'elenco di hello.

   > [!NOTE]
   > È possibile esaminare il codice hello che accede a tooquery di back-end le app per dispositivi mobili e inserire i dati, disponibile in c# ToDoActivity.cs file hello.
   >
   >

## <a name="next-steps"></a>Passaggi successivi
* [Aggiungere app tooyour sincronizzazione Offline](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [Aggiungere app tooyour authentication](app-service-mobile-xamarin-android-get-started-users.md)
* [Aggiungere app xamarin tooyour di notifiche push](app-service-mobile-xamarin-android-get-started-push.md)
* [Modalità di gestione client per App mobili di Azure hello toouse](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
