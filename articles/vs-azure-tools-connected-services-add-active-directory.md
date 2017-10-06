---
title: Azure Active Directory utilizzando i servizi connessi in Visual Studio aaaAdding | Documenti Microsoft
description: Aggiungere una Azure Active Directory utilizzando la finestra di dialogo di Visual Studio aggiungere servizi connessi hello
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f599de6b-e369-436f-9cdc-48a0165684cb
ms.service: active-directory
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: kraigb
ms.openlocfilehash: 26c8f68edf9ec5f7bf65cbab34e4f9b4085ed18d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="adding-an-azure-active-directory-by-using-connected-services-in-visual-studio"></a>Aggiunta di Azure Active Directory mediante servizi connessi in Visual Studio
Tramite Azure Active Directory (Azure AD), è possibile supportare Single Sign-On (SSO) per le applicazioni Web ASP.NET MVC o l'autenticazione di Active Directory nei servizi Web API. Con Azure Active Directory l'autenticazione, gli utenti possono usare i propri account dalle applicazioni web di Azure Active Directory tooconnect tooyour. i vantaggi di Hello di Azure Active Directory Authentication con API Web includono protezione avanzata dei dati quando si espone un'API da un'applicazione web. Con Azure AD, non si dispone toomanage un sistema di autenticazione distinto con la gestione di account e utente.

## <a name="prerequisites"></a>Prerequisiti
- Account di Azure: se non si ha un account di Azure, è possibile [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) oppure [attivare i vantaggi della sottoscrizione di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

### <a name="connect-tooazure-active-directory-using-hello-connected-services-dialog"></a>La connessione di Active Directory utilizzando i servizi connessi hello tooAzure finestra di dialogo
1. In Visual Studio creare o aprire un progetto ASP.NET MVC o un progetto API Web ASP.NET.

1. Da hello Esplora soluzioni, fare doppio clic su hello **servizi connessi** nodo, selezionare il menu di scelta rapida hello **aggiungere servizi connessi**.

1. In hello **servizi connessi** selezionare **l'autenticazione con Azure Active Directory**.
   
    ![Pagina di Servizi connessi](./media/vs-azure-tools-connected-services-add-active-directory/connected-services-add-active-directory.png)

1. In hello **Introduzione** pagina di hello **configurare Azure Active Authentication** procedura guidata, selezionare **Avanti**.
   
    ![Pagina Introduzione](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-1.png)

1. In hello **Single Sign-On** pagina di hello **configurare Azure Active Authentication** guidata, selezionare un dominio da hello **dominio** elenco a discesa. elenco di Hello dei domini contiene tutti i domini accessibili dagli account hello elencati nella finestra di dialogo Impostazioni Account hello. In alternativa, è possibile immettere un nome di dominio, se non è possibile trovarla hello si sta cercando, ad esempio `mydomain.onmicrosoft.com`. È possibile scegliere di hello opzione toocreate un'app di Azure Active Directory o utilizzare le impostazioni di hello da un'app di Azure Active Directory esistente. Al termine scegliere **Avanti**.
   
    ![Pagina Single Sign-On](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-2.png)

1. In hello **accesso alla Directory** pagina di hello **configurare Azure Active Authentication** procedura guidata, verificare che hello **lettura dati directory** opzione è selezionata. 
   
    ![Pagina di accesso alla directory](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-3.png)

1. Selezionare **fine** tooadd hello tooenable di configurazione necessarie codice e i riferimenti progetto per l'autenticazione di Azure AD. È possibile visualizzare il dominio di Active Directory hello in hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. In Visual Studio verrà visualizzato un [cosa è successo](#how-your-project-is-modified) tooshow articolo è come è stato modificato il progetto. Se si desidera toocheck che tutto funzioni, aprire uno dei file di configurazione modificato hello e verificare che le impostazioni di hello indicate nell'articolo hello siano presenti. 

## <a name="how-your-project-is-modified"></a>Come viene modificato il progetto
Quando si esegue la procedura guidata hello, Visual Studio aggiunge i riferimenti associati tooyour progetto e Azure Active Directory. File di configurazione e i file di codice nel progetto sono anche supporto tooadd modificato per Azure AD. modifiche specifiche Hello che Visual Studio apporta dipendono dal tipo di progetto hello. Per informazioni dettagliate sul modo in cui vengono modificati i progetti MVC ASP.NET, vedere [Risultati - Progetti MVC](http://go.microsoft.com/fwlink/p/?LinkID=513809). Per i progetti Web API, vedere [Cosa è successo: Progetti Web API](http://go.microsoft.com/fwlink/p/?LinkId=513810).

## <a name="next-steps"></a>Passaggi successivi
* [Forum MSDN su Azure Active Directory](https://social.msdn.microsoft.com/forums/azure/home?forum=WindowsAzureAD)
* [Documentazione di Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)
* [Post di blog: Introduzione tooAzure Active Directory](http://blogs.msdn.com/b/brunoterkaly/archive/2014/03/03/introduction-to-windows-azure-active-directory.aspx)

