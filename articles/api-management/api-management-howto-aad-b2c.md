---
title: gli account sviluppatore aaaAuthorize tramite Azure Active Directory B2C - gestione API di Azure | Documenti Microsoft
description: Informazioni su come gli utenti di tooauthorize usando Azure Active Directory B2C in Gestione API.
services: api-management
documentationcenter: API Management
author: miaojiang
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
ms.openlocfilehash: 28f7cae53138938dbbc848b4afcbf08b72690e37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a>La modalità sviluppatore tooauthorize degli account con Azure Active Directory B2C in Gestione API di Azure
## <a name="overview"></a>Panoramica
Azure Active Directory B2C è una soluzione di gestione delle identità cloud per applicazioni per dispositivi mobili e Web rivolte agli utenti. È possibile utilizzare il portale per sviluppatori di toomanage accesso tooyour. Questa guida viene illustrata hello configurazione necessarie nel toointegrate servizio Gestione API con Azure Active Directory B2C. Per informazioni sull'abilitazione di portale per sviluppatori di accesso toohello utilizzando Active Directory di Azure classico, vedere [modalità sviluppatore tooauthorize degli account con Azure Active Directory].

> [!NOTE]
> passaggi di hello toocomplete in questa Guida, è innanzitutto necessario un toocreate tenant Azure Active Directory B2C un'applicazione. Inoltre, è necessario criteri di iscrizione e signin toohave pronto. Per altre informazioni, vedere la [panoramica di Azure Active Directory B2C].

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a>Autorizzare gli account per sviluppatore usando Azure Active Directory B2C

1. tooget avviato, fare clic su **portale di pubblicazione** nel portale di Azure per il servizio Gestione API hello. Consente di procedere toohello portale di pubblicazione di gestione API.

   ![Portale di pubblicazione][api-management-management-console]

   > [!NOTE]
   > Se è ancora stata creata un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [iniziare con gestione API di Azure esercitazione][Get started with Azure API Management].

2. In hello **gestione API** menu, fare clic su **sicurezza**. In hello **identità** scegliere **Azure Active Directory B2C**.

  ![Identità esterne 1][api-management-howto-aad-b2c-security-tab]

3. Prendere nota di hello **l'URL di reindirizzamento** e passare tooAzure Active Directory B2C in hello portale di Azure.

  ![Identità esterne 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. Fare clic su hello **applicazioni** pulsante.

  ![Registrare una nuova applicazione 1][api-management-howto-aad-b2c-portal-menu]

5. Fare clic su hello **Aggiungi** pulsante applicazione toocreate un nuovo B2C Directory Azure attivo.

  ![Registrare una nuova applicazione 2][api-management-howto-aad-b2c-add-button]

6. In hello **nuova applicazione** pannello, immettere un nome per un'applicazione hello. Scegliere **Sì** in **App Web/API Web** e quindi **Sì** in **Consenti flusso implicito**. Quindi hello copia **l'URL di reindirizzamento** da hello **Azure Active Directory B2C** sezione di hello **identità** scheda nel portale di pubblicazione hello e incollarla hello **URL di risposta** casella di testo.

  ![Registrare una nuova applicazione 3][api-management-howto-aad-b2c-app-details]

7. Fare clic su hello **crea** pulsante. Quando viene creata un'applicazione hello, viene visualizzata in hello **applicazioni** blade. Fare clic su hello applicazione nome toosee i dettagli.

  ![Registrare una nuova applicazione 4][api-management-howto-aad-b2c-app-created]

8. Da hello **proprietà** blade, hello copia **ID applicazione** toohello Appunti.

  ![ID applicazione 1][api-management-howto-aad-b2c-app-id]

9. Passa indietro toohello portale di pubblicazione e incollare hello ID hello **Id Client** casella di testo.

  ![ID applicazione 2][api-management-howto-aad-b2c-client-id]

10. Passa indietro toohello portale di Azure, fare clic su hello **chiavi** pulsante e quindi fare clic su **Genera chiave**. Fare clic su **salvare** hello di configurazione e la visualizzazione di hello toosave **chiave App**. Copiare negli Appunti toohello chiave hello.

  ![Chiave dell'app 1][api-management-howto-aad-b2c-app-key]

11. Commutatore toohello back-portale e Incolla hello chiave editore in hello **segreto Client** casella di testo.

  ![Chiave dell'app 2][api-management-howto-aad-b2c-client-secret]

12. Specificare il nome di dominio hello del tenant di Azure Active Directory B2C hello in **consentito Tenant**.

  ![Tenant consentito][api-management-howto-aad-b2c-allowed-tenant]

13. Specificare hello **criteri iscrizione** e **criteri Signin**. Facoltativamente, è anche possibile fornire hello **profilo criteri di modifica** e **criteri di reimpostazione Password**.

  ![Criteri][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > Per altre informazioni sui criteri, vedere [Azure Active Directory B2C: framework di criteri estendibile].

14. Dopo aver specificato la configurazione desiderata di hello, fare clic su **salvare**.

  Dopo aver salvate le modifiche di hello, gli sviluppatori verranno toocreate in grado di nuovi account e accedere nel portale per sviluppatori toohello usando Azure Active Directory B2C.

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a>Eseguire l'iscrizione per un account per sviluppatore usando Azure Active Directory B2C

1. toosign a un account sviluppatore utilizzando Active B2C Directory di Azure, aprire una nuova finestra del browser e passare il portale per sviluppatori di toohello. Fare clic su hello **iscriversi** pulsante.

   ![Portale per sviluppatori 1][api-management-howto-aad-b2c-dev-portal]

2. Scegliere toosign con **Azure Active Directory B2C**.

   ![Portale per sviluppatori 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. Si è reindirizzato toohello iscrizione criteri configurato nella sezione precedente hello. Scegliere toosign utilizzando l'indirizzo di posta elettronica o uno degli account di social networking esistente.

   > [!NOTE]
   > Se Azure Active Directory B2C hello unica opzione che è stato attivato hello **identità** scheda nel portale di pubblicazione hello, sarà reindirizzato toohello iscrizione criteri direttamente.

   ![Portale per sviluppatori][api-management-howto-aad-b2c-dev-portal-b2c-options]

   Una volta completato hello iscrizione, si è portale per sviluppatori toohello indietro reindirizzato. È ora effettuata nel portale per sviluppatori toohello per l'istanza del servizio Gestione API.

    ![Registrazione completata][api-management-registration-complete]

## <a name="next-steps"></a>Passaggi successivi

*  [panoramica di Azure Active Directory B2C]
*  [Azure Active Directory B2C: framework di criteri estendibile]
*  [Usare un account Microsoft come provider di identità in Azure Active Directory B2C]
*  [Usare un account Google come provider di identità in Azure Active Directory B2C]
*  [Usare un account LinkedIn come provider di identità in Azure Active Directory B2C]
*  [Usare un account Facebook come provider di identità in Azure Active Directory B2C]




[api-management-howto-aad-b2c-security-tab]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab.PNG
[api-management-howto-aad-b2c-security-tab-reply-url]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab-reply-url.PNG
[api-management-howto-aad-b2c-portal-menu]: ./media/api-management-howto-aad-b2c/api-management-b2c-portal-menu.PNG
[api-management-howto-aad-b2c-add-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-add-button.PNG
[api-management-howto-aad-b2c-app-details]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-details.PNG
[api-management-howto-aad-b2c-app-created]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-created.PNG
[api-management-howto-aad-b2c-app-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-id.PNG
[api-management-howto-aad-b2c-client-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-id.PNG
[api-management-howto-aad-b2c-app-key]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key.PNG
[api-management-howto-aad-b2c-app-key-saved]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key-saved.PNG
[api-management-howto-aad-b2c-client-secret]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-secret.PNG
[api-management-howto-aad-b2c-allowed-tenant]: ./media/api-management-howto-aad-b2c/api-management-b2c-allowed-tenant.PNG
[api-management-howto-aad-b2c-policies]: ./media/api-management-howto-aad-b2c/api-management-b2c-policies.PNG
[api-management-howto-aad-b2c-dev-portal]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-button.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-options]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-options.PNG
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.PNG
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-b2c-security-tab.png
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
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
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
[panoramica di Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview
[modalità sviluppatore tooauthorize degli account con Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad
[Azure Active Directory B2C: framework di criteri estendibile]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies
[Usare un account Microsoft come provider di identità in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app
[Usare un account Google come provider di identità in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app
[Usare un account Facebook come provider di identità in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app
[Usare un account LinkedIn come provider di identità in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
