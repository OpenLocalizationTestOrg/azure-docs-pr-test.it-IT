---
title: aaaAdding servizi mobili utilizzando i servizi connessi in Visual Studio | Documenti Microsoft
description: Aggiungere servizi mobili mediante la finestra di dialogo di Visual Studio aggiungere servizi connessi hello
services: visual-studio-online
documentationcenter: na
author: mlhoop
manager: douge
editor: 
ms.assetid: 75c3cb93-88e1-476d-a416-f34caa3608e3
ms.service: visual-studio-online
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: mobile
ms.date: 12/16/2015
ms.author: mlearned
ms.openlocfilehash: c47b6fb63dc99fbc012e1c627c6c7e95249de7a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="adding-mobile-services-by-using-visual-studio-connected-services"></a>Aggiunta di servizi mobili tramite Servizi connessi di Visual Studio
Con Visual Studio 2015, è possibile connettersi a servizi mobili tooAzure utilizzando hello **Aggiungi servizio connesso** finestra di dialogo. È possibile connettersi da qualsiasi app client C#, qualsiasi app JavaScript o app Cordova multipiattaforma. Una volta connessi, è possibile creare e accedere ai dati, creare API personalizzate e i processi pianificati o aggiungere il supporto per le notifiche push.  Hello servizi connessi operazione aggiunge tutti i riferimenti appropriati e il codice di connessione. È possibile anche sfruttare il supporto integrato per l'autenticazione con un'ampia gamma di sistemi di identità comuni, quali Azure AD, Facebook, Twitter e Account di Microsoft.

## <a name="supported-project-types"></a>Tipi di progetto supportati
> [!NOTE]
> In Visual Studio 2015, l'aggiunta di progetti universali di Windows (Windows 10) di servizi mobili di Azure tooa utilizzando la finestra di dialogo Aggiungi servizi connessi hello non è supportata. È possibile aggiungere servizi mobili di Azure mediante l'installazione di pacchetti di hello appropriati utilizzando hello Gestione pacchetti NuGet per il progetto.
> 
> 

È possibile utilizzare i servizi connessi finestra di dialogo hello tooconnect tooAzure servizi mobili in hello seguenti tipi di progetto.

* Progetti .NET Windows 8.1 Store, Phone e Universal App
* Progetti JavaScript Windows 8.1 Store, Phone e Universal App
* Progetti creati usando Strumenti di Visual Studio per Apache Cordova

## <a name="connect-tooazure-mobile-services-using-hello-add-connected-services-dialog"></a>Connettersi a servizi mobili tooAzure mediante finestra di dialogo Aggiungi servizi connessi hello
1. È necessario disporre di un account Azure. Se non si ha un account Azure, è possibile iscriversi per ottenere una [versione di valutazione gratuita](http://go.microsoft.com/fwlink/?LinkId=518146).
2. Aprire hello **aggiungere servizi connessi** la finestra di dialogo.
   
   * Per le applicazioni .NET, aprire il progetto in Visual Studio, aprire hello menu di scelta rapida hello **riferimenti** nodo in Esplora soluzioni, quindi scegliere **Aggiungi servizio connesso**
     
        ![Connessione del servizio Mobile tooAzure](./media/vs-azure-tools-connected-services-add-mobile-services/IC797635.png)
   * Per i progetti di app Apache Cordova, aprire il progetto in Visual Studio, menu di scelta rapida aprire hello hello nodo di progetto in Esplora soluzioni e quindi scegliere **Aggiungi servizio connesso**.
3. In hello **Aggiungi servizio connesso** finestra di dialogo scegliere **servizi mobili di Azure**, quindi scegliere hello **configura** pulsante. Se non è già fatto, potrebbe essere richiesta toolog in Azure.
   
    ![Aggiunta di un servizio Mobile di Azure](./media/vs-azure-tools-connected-services-add-mobile-services/IC797636.png)
4. In hello **servizi mobili di Azure** finestra di dialogo, scegliere un servizio mobile esistente se si dispone di uno. Se è necessario un nuovo servizio mobile di Azure toocreate, procedura hello sotto toodo così. In caso contrario, andare toohello successivo.
   
    toocreate un nuovo account di servizio mobile:
   
   1. Scegliere hello * * Crea servizio * * collegamento nella parte inferiore di hello della finestra di dialogo hello.
       ![Aggiungere un nuovo servizio connesso mobile](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)
   2. In hello **Crea servizio Mobile** nella finestra di dialogo è possibile scegliere un servizio mobile back-end di JavaScript, o un servizio mobile back-end di .NET da hello **Runtime** elenco a discesa. 
      
       ![Creazione di un servizio mobile](./media/vs-azure-tools-connected-services-add-mobile-services/IC797638.png)
      
       Un servizio back-end di JavaScript è semplice ed efficiente. Se si crea un servizio mobile back-end di JavaScript, il codice JavaScript sul lato server hello viene archiviato nel cloud hello, ma è possibile modificare gli script server tramite Esplora Server o il portale di gestione di Azure hello. 
      
       Un servizio mobile back-end di .NET offre hello completo e flessibilità di API Web ed Entity Framework. Se si crea un servizio mobile di back-end .NET, un progetto viene creato e aggiunto tooyour soluzione. 
   3. Scegliere hello **area** in cui si desidera servizio mobile hello e quindi immettere un nome utente e una password per il server di hello.
   4. Dopo aver immesso tutte le informazioni necessarie hello, scegliere hello **crea** pulsante toocreate servizio mobile di hello.
   5. nuovo servizio mobile Hello deve essere visualizzato nell'elenco servizio hello in hello **servizi mobili di Azure** la finestra di dialogo. Scegliere nuovo servizio mobile hello nell'elenco di hello e quindi scegliere hello **Aggiungi** progetto tooyour del pulsante tooadd hello servizio.
5. Revisione hello la pagina Guida introduttiva visualizzata e scoprire come è stato modificato il progetto. Ogni volta che si aggiunge un servizio connesso, nel browser verrà visualizzata una pagina introduttiva. È possibile esaminare hello passaggi successivi suggeriti e gli esempi di codice oppure passare toohello cosa è successo pagina toosee sui riferimenti che sono stati aggiunti tooyour progetto e la modalità in cui sono stati modificati i file di codice e la configurazione.
6. Utilizzando gli esempi di codice hello come guida, iniziare a scrivere codice tooaccess il servizio mobile.

## <a name="how-your-project-is-modified"></a>Come viene modificato il progetto
Come Visual Studio modifica il progetto dipende dal tipo di progetto hello. Per le app client C#, vedere [Informazioni sull’evento – Progetti C#](http://go.microsoft.com/fwlink/p/?LinkId=513119). Per le applicazioni client JavaScript, vedere [Risultati - Progetti JavaScript](http://go.microsoft.com/fwlink/p/?LinkId=513120). Per le applicazioni Cordova, vedere [Risultati - Progetti Cordova](http://go.microsoft.com/fwlink/p/?LinkId=513116).

## <a name="next-steps"></a>Passaggi successivi
Domande e assistenza: 

* [Forum MSDN: Servizi mobili di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azuremobile)
* [Servizi mobili di Azure in hello Blog del Team di Microsoft Azure](https://azure.microsoft.com/blog/topics/mobile/)
* [Servizi mobili di Azure in azure.microsoft.com](https://azure.microsoft.com/services/mobile-services/)
* [Documentazione dei servizi mobili di Azure sul sito azure.microsoft.com](https://azure.microsoft.com/documentation/services/mobile-services/)

