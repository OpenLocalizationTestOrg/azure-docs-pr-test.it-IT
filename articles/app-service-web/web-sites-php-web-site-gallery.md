---
title: un'app web WordPress in Azure App Service aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate una nuova versione di Azure web app per un blog di WordPress usando hello portale di Azure.
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 193ae094-0d7c-4749-a09b-ff4b1240149e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 3a95fcb6732c15a8200921ce474b6dde2298dec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a>Creare un'app WordPress nel servizio app di Azure
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Questa esercitazione viene illustrato come un blog di WordPress toodeploy del sito da hello Azure Marketplace.

Una volta terminato con l'esercitazione hello è necessario il proprio sito blog di WordPress backup e in esecuzione nel cloud hello.

![Sito WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

Si apprenderà come:

* Come un modello di applicazione in Azure Marketplace hello toofind.
* Come toocreate un'app web in Azure App Service che è basato sul modello di hello.
* Come le impostazioni di servizio App di Azure tooconfigure hello nuovo web app e il database.

Hello Azure Marketplace rende disponibile un'ampia gamma di applicazioni web comuni sviluppato da Microsoft, le aziende di terze parti e Apri origine software iniziative. le applicazioni web Hello sono basate su una vasta gamma di popolari Framework, ad esempio [PHP](/develop/nodejs/) in questo esempio WordPress, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), e [Python](/develop/python/), tooname qualche. un'app web da Azure Marketplace hello solo software necessario è browser hello usato per hello hello toocreate [portale Azure](https://portal.azure.com/). 

sito WordPress Hello da distribuire in questa esercitazione Usa MySQL per il database di hello. Se si desidera utilizzare tooinstead Database SQL per database hello, vedere [Nami progetto](http://projectnami.org/). **Progetto Nami** è anche disponibile tramite Marketplace hello.

> [!NOTE]
> toocomplete questa esercitazione, è necessario un account di Microsoft Azure. Se non si dispone di un account, è possibile [attivare i benefici della sottoscrizione Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) oppure [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
> 
> Se si desidera tooget avviato con il servizio App di Azure prima di iscriversi per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/). In questa pagina è possibile creare immediatamente un'app Web iniziale temporanea nel servizio app. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a>Selezionare WordPress ed eseguire la configurazione per il servizio app di Azure
1. Accedi toohello [portale Azure](https://portal.azure.com/).
2. Fare clic su **New**.
   
    ![Creazione di un nuovo sito][5]
3. Cercare **WordPress** e quindi fare clic su **WordPress**. Se si desidera toouse Database SQL anziché MySQL, cercare **Nami progetto**.
   
    ![WordPress nell'elenco][7]
4. Dopo aver letto descrizione hello di hello WordPress app, fare clic su **crea**.
   
    ![Create](./media/web-sites-php-web-site-gallery/create.png)
5. Immettere un nome per l'app web hello in hello **app Web** casella.
   
    Questo nome deve essere univoco nel dominio azurewebsites.net hello perché hello URL dell'app web hello sarà {name}. azurewebsites.net. Se specifica un nome hello non è univoco, viene visualizzato un punto esclamativo rosso nella casella di testo hello.
6. Se si dispone di più di una sottoscrizione, scegliere hello quello che si desidera toouse. 
7. Selezionare un **Gruppo di risorse** o crearne uno nuovo.
   
    Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
8. Selezionare un **Piano di servizio app/Posizione** o crearne uno nuovo.
   
    Per altre informazioni sui piani del servizio app, vedere [Panoramica approfondita dei piani del servizio app di Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)    
9. Fare clic su **Database**e quindi in hello **Nuovo MySQL Database** pannello sono valori hello necessario per la configurazione del database MySQL.
   
    a. Immettere un nuovo nome o lasciare il nome predefinito hello.
   
    b. Lasciare hello **tipo di Database** impostare troppo**Shared**.
   
    c. Scegliere hello nello stesso percorso come hello è selezionato per l'app web hello.
   
    d. Scegliere un piano tariffario. Mercury (gratuito con quantità minima di connessioni consentite e di spazio su disco) è ottimale per questa esercitazione.
10. In hello **Nuovo MySQL Database** pannello, fare clic su **OK**. 
11. In hello **WordPress** pannello, accettare i termini legali specifici hello e quindi fare clic su **crea**. 
    
     ![Configurazione dell'app Web](./media/web-sites-php-web-site-gallery/configure.png)
    
     Servizio App di Azure crea app web hello, in genere in meno di un minuto. È possibile controllare lo stato di avanzamento hello facendo clic sull'icona di campanello hello nella parte superiore di hello della pagina del portale hello.
    
     ![Indicatore di stato](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a>Avviare e gestire l'app Web WordPress
1. Al termine della creazione dell'app web hello, passare in hello Azure Portal toohello gruppo di risorse in cui è stato creato un'applicazione hello e si può vedere hello web app e database hello.
   
    sono Hello risorse aggiuntive con icona lampadina hello [Application Insights](/services/application-insights/), che fornisce servizi di monitoraggio per l'app web.
2. In hello **gruppo di risorse** pannello, fare clic sulla riga di hello web app.
   
    ![Configurazione dell'app Web](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. Nel Pannello di hello Web app, fare clic su **Sfoglia**.
   
    ![URL sito][browse]
4. In hello WordPress **iniziale** immettere le informazioni di configurazione hello richieste da WordPress e quindi fare clic su **installa WordPress**.
   
    ![Configurazione di WordPress](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. Accedere con credenziali hello è stato creato in hello **iniziale** pagina.  
6. Verrà visualizzata la pagina del dashboard del sito.    
   
    ![Sito WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a>Passaggi successivi
Si è visto come toocreate e distribuire un'app web PHP dalla raccolta hello. Per ulteriori informazioni sull'utilizzo di PHP in Azure, vedere hello [Centro sviluppatori PHP](/develop/php/).

Per ulteriori informazioni su come toowork con applicazione servizio Web App, vedere i collegamenti di hello in hello il lato sinistro di pagina hello (per le finestre del browser "wide") o nella parte superiore di hello della pagina di hello (per le finestre del browser "narrow"). 

## <a name="whats-changed"></a>Modifiche apportate
* Per una modifica di toohello della Guida da tooApp di siti Web del servizio, vedere [servizio App di Azure e il relativo impatto sui servizi di Azure esistente](http://go.microsoft.com/fwlink/?LinkId=529714).

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
