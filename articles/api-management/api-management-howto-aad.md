---
title: gli account sviluppatore aaaAuthorize tramite Azure Active Directory - gestione API di Azure | Documenti Microsoft
description: Informazioni su come gli utenti tooauthorize tramite Azure Active Directory in Gestione API.
services: api-management
documentationcenter: API Management
author: steved0x
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ebf5447a509a47df35e4262138bfcf423cb1dd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a>La modalità sviluppatore tooauthorize degli account con Azure Active Directory in Gestione API di Azure
## <a name="overview"></a>Panoramica
Questa guida viene spiegato come tooenable accedere portale per sviluppatori toohello per gli utenti da Azure Active Directory. Questa guida illustra anche come toomanage gruppi di utenti di Azure Active Directory tramite l'aggiunta di gruppi esterni che contengono hello agli utenti di Azure Active Directory.

> hello toocomplete i passaggi in questa guida è necessario prima disporre di Azure Active Directory in cui toocreate un'applicazione.
> 
> 

## <a name="how-tooauthorize-developer-accounts-using-azure-active-directory"></a>La modalità sviluppatore tooauthorize degli account con Azure Active Directory
tooget avviato, fare clic su **portale di pubblicazione** nel portale di Azure per il servizio Gestione API hello. Consente di procedere toohello portale di pubblicazione di gestione API.

![Portale di pubblicazione][api-management-management-console]

> Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.
> 
> 

Fare clic su **sicurezza** da hello **gestione API** menu a sinistra di hello e fare clic su **le identità esterne**.

![Identità esterne][api-management-security-external-identities]

Fare clic su **Azure Active Directory**. Prendere nota di hello **l'URL di reindirizzamento** e passare tooyour Azure Active Directory nel portale di Azure classico hello.

![Identità esterne][api-management-security-aad-new]

Fare clic su hello **Aggiungi** toocreate una nuova applicazione Azure Active Directory e scegliere **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.

![Aggiungere una nuova applicazione Azure Active Directory][api-management-new-aad-application-menu]

Immettere un nome per l'applicazione hello, selezionare **Web dell'applicazione e/o API Web**e fare clic sul pulsante Avanti hello.

![Nuova applicazione Azure Active Directory][api-management-new-aad-application-1]

Per **Sign-on URL**, immettere hello sign-on URL del portale per sviluppatori. In questo esempio hello **Sign-on URL** è `https://aad03.portal.current.int-azure-api.net/signin`. 

Per hello **URL ID App**, immettere il dominio predefinito hello o un dominio personalizzato per hello Azure Active Directory e aggiungere tooit una stringa univoca. In questo esempio hello dominio predefinito di **https://contoso5api.onmicrosoft.com** viene utilizzato con il suffisso hello **/api** specificato.

![Proprietà della nuova applicazione Azure Active Directory][api-management-new-aad-application-2]

Fare clic su hello controllo pulsante toosave e creare un'applicazione hello e passa toohello **configura** tooconfigure un'applicazione hello nuova scheda.

![Nuova applicazione Azure Active Directory creata][api-management-new-aad-app-created]

Se più Azure Active Directory prevede toobe utilizzato per questa applicazione, fare clic su **Sì** per **applicazione è multi-tenant**. valore predefinito di Hello è **n**.

![L'applicazione è multi-tenant][api-management-aad-app-multi-tenant]

Hello copia **l'URL di reindirizzamento** da hello **Azure Active Directory** sezione di hello **le identità esterne** scheda nel portale di pubblicazione hello e incollarla hello **URL di risposta** casella di testo. 

![URL di risposta][api-management-aad-reply-url]

Scorri toohello alla fine di hello configurare della scheda Seleziona hello **autorizzazioni applicazione** elenco a discesa e selezionare **lettura dati directory**.

![Autorizzazioni applicazione][api-management-aad-app-permissions]

Seleziona hello **delegare le autorizzazioni** elenco a discesa e selezionare **attivare l'accesso e leggere i profili degli utenti**.

![Autorizzazioni delegate][api-management-aad-delegated-permissions]

> Per ulteriori informazioni sull'applicazione e le autorizzazioni delegate, vedere [hello accesso API Graph][Accessing hello Graph API].
> 
> 

Hello copia **Id Client** toohello Appunti.

![Client Id][api-management-aad-app-client-id]

Passare il portale di pubblicazione toohello indietro e incollare in hello **Id Client** copiati dalla configurazione dell'applicazione hello Azure Active Directory.

![Client Id][api-management-client-id]

Configurazione di Azure Active Directory toohello nascosto e fare clic su hello **Seleziona durata** menu a discesa hello **chiavi** sezione e specificare un intervallo. In questo esempio viene usato **1 anno** .

![Chiave][api-management-aad-key-before-save]

Fare clic su **salvare** chiave hello configurazione e la visualizzazione toosave hello. Copiare negli Appunti toohello chiave hello.

> Annotare il valore relativo alla chiave. Quando si chiude una finestra di configurazione di hello Azure Active Directory, non è più visualizzata chiave hello.
> 
> 

![Chiave][api-management-aad-key-after-save]

Commutatore toohello back-portale e Incolla hello chiave editore in hello **segreto Client** casella di testo.

![Client Secret][api-management-client-secret]

**Consentito tenant** specifica le directory hanno accesso toohello API dell'istanza del servizio Gestione API hello. Specificare i domini hello di hello toowhich di istanze di Azure Active Directory si desidera accedere toogrant. È possibile separare più domini con virgole, spazi o caratteri di nuova riga.

![Tenant consentiti][api-management-client-allowed-tenants]


Una volta hello lo si desidera che la configurazione viene specificata, fare clic su **salvare**.

![Salva][api-management-client-allowed-tenants-save]

Una volta che vengono salvate le modifiche di hello, gli utenti di hello in hello specificati possono accedere Azure Active Directory nel portale per sviluppatori toohello seguendo i passaggi di hello in [Accedi al portale per sviluppatori toohello utilizzando un account Azure Active Directory] [Log in toohello Developer portal using an Azure Active Directory account].

È possibile specificare più domini in hello **consentito tenant** sezione. Prima di qualsiasi utente può accedere da un dominio diverso da quello hello originale in cui è stata registrata un'applicazione hello, un amministratore globale di dominio diverso hello deve concedere l'autorizzazione per tooaccess applicazione hello dati della directory. autorizzazione toogrant, amministratore globale di hello deve andare troppo`https://<URL of your developer portal>/aadadminconsent` (ad esempio, https://contoso.portal.azure-api.net/aadadminconsent), digitare il nome di dominio hello di hello desiderano toogive accesso tooand tenant di Active Directory fare clic su Invia. In seguito hello esempio, da un amministratore globale `miaoaad.onmicrosoft.com` tenta toogive autorizzazione toothis particolare portale. 

![Autorizzazioni][api-management-aad-consent]

Nella schermata successiva hello, amministratore globale di hello sarà richiesta tooconfirm concesse le autorizzazioni hello. 

![Autorizzazioni][api-management-permissions-form]

> Se un amministratore non globali tenta toolog nella prima le autorizzazioni vengono concesse da un amministratore globale, hello account di accesso non riesce e verrà visualizzato un errore.
> 
> 

## <a name="how-tooadd-an-external-azure-active-directory-group"></a>Modo tooadd esterna Azure Active Directory in cui raggruppare
Dopo l'abilitazione dell'accesso per gli utenti in Azure Active Directory, è possibile aggiungere gruppi di Azure Active Directory in Gestione API toomore gestire facilmente l'associazione di hello di sviluppatori hello gruppo hello con prodotti hello desiderato.

> tooconfigure un gruppo esterno di Azure Active Directory, hello Azure Active Directory deve essere prima configurate nella scheda identità hello seguendo la procedura hello nella sezione precedente hello. 
> 
> 

I gruppi esterni di Azure Active Directory vengono aggiunti da hello **visibilità** scheda del prodotto hello per i quali gruppo di toohello toogrant accesso. Fare clic su **prodotti**, quindi fare clic su nome hello del prodotto desiderate hello.

![Configure product][api-management-configure-product]

Passare toohello **visibilità** scheda e fare clic su **Aggiungi gruppi da Azure Active Directory**.

![Aggiungere i gruppi][api-management-add-groups]

Seleziona hello **Tenant di Azure Active Directory** dall'elenco a discesa hello, quindi nome hello del tipo di gruppo desiderato di hello in hello **gruppi** toobe aggiunto casella di testo.

![Selezionare un gruppo][api-management-select-group]

Nome di questo gruppo è reperibile in hello **gruppi** elenco per Azure Active Directory, come illustrato nell'esempio seguente hello.

![Elenco di gruppi di Azure Active Directory][api-management-aad-groups-list]

Fare clic su **Aggiungi** toovalidate hello nome del gruppo e aggiungere il gruppo di hello. In questo esempio hello **agli sviluppatori di Contoso 5** viene aggiunto un gruppo esterno. 

![Gruppo aggiunto][api-management-aad-group-added]

Fare clic su **salvare** toosave hello nuova selezione gruppo.

Una volta che un gruppo di Azure Active Directory è stato configurato da un prodotto, è disponibile toobe controllate hello **visibilità** scheda hello altri prodotti nell'istanza del servizio Gestione API hello.

tooreview e configurare le proprietà di hello per gruppi esterni dopo che sono stati aggiunti, fare clic sul nome hello del gruppo hello hello **gruppi** scheda.

![Gestire i gruppi][api-management-groups]

Da qui è possibile modificare hello **nome** hello e **descrizione** del gruppo di hello.

![Modificare un gruppo][api-management-edit-group]

Gli utenti da hello configurato Azure Active Directory possono Accedi al portale per sviluppatori toohello e di visualizzazione e sottoscrizione tooany gruppi per cui dispongono di visibilità seguendo le istruzioni di hello nella seguente sezione hello.

## <a name="how-toolog-in-toohello-developer-portal-using-an-azure-active-directory-account"></a>Come toolog nel portale per sviluppatori toohello utilizzando un account Azure Active Directory
toolog portale per sviluppatori hello utilizzando un account di Azure Active Directory configurato nelle sezioni precedenti hello, aprire una nuova finestra del browser utilizzando hello **Sign-on URL** dalla configurazione dell'applicazione hello Active Directory e fare clic su **Azure Active Directory**.

![Portale per sviluppatori][api-management-dev-portal-signin]

Immettere le credenziali di hello di uno degli utenti hello in Azure Active Directory e fare clic su **Accedi**.

![pagina di accesso][api-management-aad-signin]

È possibile che venga richiesto di compilare un modulo di registrazione se sono necessarie altre informazioni. Completare il modulo di registrazione hello e fare clic su **iscriversi**.

![Registrazione][api-management-complete-registration]

L'utente viene ora registrato nel portale per sviluppatori di hello per l'istanza del servizio Gestione API.

![Registrazione completata][api-management-registration-complete]

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-security-external-identities.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-aad-consent]: ./media/api-management-howto-aad/api-management-aad-consent.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

