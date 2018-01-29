---
title: Aggiunta di servizi mobili tramite Servizi connessi di Visual Studio | Documentazione Microsoft
description: 'Aggiungere servizi mobili tramite la finestra di dialogo Aggiungi servizi connessi di Visual Studio '
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
ms.openlocfilehash: d185fdafebad56f8970e390b2a0672c3fb84df8f
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="adding-mobile-services-by-using-visual-studio-connected-services"></a>Aggiunta di servizi mobili tramite Servizi connessi di Visual Studio
Con Visual Studio 2015, è possibile connettersi a Servizi mobili di Azure usando la finestra di dialogo **Aggiungi servizio connesso** . È possibile connettersi da qualsiasi app client C#, qualsiasi app JavaScript o app Cordova multipiattaforma. Una volta connessi, è possibile creare e accedere ai dati, creare API personalizzate e i processi pianificati o aggiungere il supporto per le notifiche push.  L'operazione di servizi connessi aggiunge tutti i riferimenti appropriati e il codice di connessione. È possibile anche sfruttare il supporto integrato per l'autenticazione con un'ampia gamma di sistemi di identità comuni, quali Azure AD, Facebook, Twitter e Account di Microsoft.

## <a name="supported-project-types"></a>Tipi di progetto supportati
> [!NOTE]
> In Visual Studio 2015, l'aggiunta di Servizi mobili di Azure a progetti di Windows Universal (Windows 10) mediante la finestra di dialogo Aggiungi servizi connessi non è supportata. È possibile aggiungere servizi mobili di Azure installando i pacchetti appropriati usando Gestione pacchetti NuGet per il progetto.
> 
> 

È possibile usare la finestra di dialogo Servizi connessi per connettersi a Servizi mobili di Azure nei tipi di progetto seguenti.

* Progetti .NET Windows 8.1 Store, Phone e Universal App
* Progetti JavaScript Windows 8.1 Store, Phone e Universal App
* Progetti creati usando Strumenti di Visual Studio per Apache Cordova

## <a name="connect-to-azure-mobile-services-using-the-add-connected-services-dialog"></a>Connettersi a Servizi mobili di Azure usando la finestra di dialogo Aggiungi servizi connessi
1. È necessario disporre di un account Azure. Se non si ha un account Azure, è possibile iscriversi per ottenere una [versione di valutazione gratuita](http://go.microsoft.com/fwlink/?LinkId=518146).
2. Aprire la finestra di dialogo **Aggiungi servizi connessi** .
   
   * Per le applicazioni .NET, aprire il progetto in Visual Studio, aprire il menu di scelta rapida del nodo **Riferimenti** in Esplora soluzioni, quindi scegliere **Aggiungi servizio connesso**
     
        ![Connessione al Servizio mobile di Azure](./media/vs-azure-tools-connected-services-add-mobile-services/IC797635.png)
   * Per i progetti di app Apache Cordova, aprire il progetto in Visual Studio, aprire il menu di scelta rapida del nodo del progetto in Esplora soluzioni e quindi scegliere **Aggiungi servizio connesso**.
3. Nella finestra di dialogo **Aggiungi servizio connesso** scegliere **Servizi mobili di Azure**, quindi fare clic su **Configura**. Se non è già stato effettuato, potrebbe essere richiesto l'accesso ad Azure.
   
    ![Aggiunta di un servizio Mobile di Azure](./media/vs-azure-tools-connected-services-add-mobile-services/IC797636.png)
4. Nella finestra di dialogo **Servizi mobili di Azure** scegliere un servizio mobile esistente, se disponibile. Se è necessario creare un nuovo servizio mobile di Azure, eseguire la procedura seguente. In caso contrario, continuare con il passaggio successivo.
   
    Per creare un nuovo account di servizio mobile:
   
   1. fare clic sul collegamento **Crea servizio** nella parte inferiore della finestra di dialogo.
       ![Aggiungere un nuovo servizio connesso mobile](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)
   2. Nella finestra di dialogo **Crea servizio mobile** è possibile scegliere un servizio mobile back-end JavaScript o un servizio mobile back-end .NET nell'elenco a discesa **Runtime**. 
      
       ![Creazione di un servizio mobile](./media/vs-azure-tools-connected-services-add-mobile-services/IC797638.png)
      
       Un servizio back-end di JavaScript è semplice ed efficiente. Se si crea un servizio mobile back-end di JavaScript, il codice JavaScript lato server viene archiviato nel cloud, ma è possibile modificare gli script del server tramite Esplora server o il portale di gestione di Azure. 
      
       Un servizio mobile back-end di .NET offre la potenza e flessibilità dell'API Web e di Entity Framework. Se si crea un servizio mobile back-end di .NET, un progetto viene creato e aggiunto alla soluzione. 
   3. Scegliere l' **Area** in cui si vuole il servizio mobile e quindi immettere un nome utente e una password per il server.
   4. Dopo aver immesso tutte le informazioni necessarie, fare clic su **Crea** per creare il servizio mobile.
   5. Il nuovo servizio mobile dovrebbe essere visualizzato nell'elenco dei servizi nella finestra di dialogo **Servizi mobili di Azure** . Scegliere il nuovo servizio mobile dall'elenco, quindi fare clic su **Aggiungi** per aggiungere il servizio al progetto.
5. Esaminare la pagina introduttiva visualizzata e controllare come è stato modificato il progetto. Ogni volta che si aggiunge un servizio connesso, nel browser verrà visualizzata una pagina introduttiva. È possibile esaminare i passaggi successivi e gli esempi di codice suggeriti o passare alla pagina Informazioni sull'evento per vedere quali riferimenti sono stati aggiunti al progetto e in che modo i file di configurazione e il codice sono stati modificati.
6. Usando gli esempi di codice come guida, iniziare a scrivere il codice per accedere al servizio mobile.

## <a name="how-your-project-is-modified"></a>Come viene modificato il progetto
La modalità di modifica del progetto di Visual Studio dipende dal tipo di progetto. Per le app client C#, vedere [Informazioni sull’evento – Progetti C#](http://go.microsoft.com/fwlink/p/?LinkId=513119). Per le applicazioni client JavaScript, vedere [Risultati - Progetti JavaScript](http://go.microsoft.com/fwlink/p/?LinkId=513120). Per le applicazioni Cordova, vedere [Risultati - Progetti Cordova](http://go.microsoft.com/fwlink/p/?LinkId=513116).

## <a name="next-steps"></a>Passaggi successivi
Domande e assistenza: 

* [Forum MSDN: Servizi mobili di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azuremobile)
* [Servizi mobili di Azure nel blog del Team di Microsoft Azure](https://azure.microsoft.com/blog/topics/mobile/)
* [Servizi mobili di Azure in azure.microsoft.com](https://azure.microsoft.com/services/mobile-services/)
* [Documentazione dei servizi mobili di Azure sul sito azure.microsoft.com](https://azure.microsoft.com/documentation/services/mobile-services/)

