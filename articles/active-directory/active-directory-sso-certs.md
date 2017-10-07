---
title: i certificati di federazione aaaManage in Azure AD | Documenti Microsoft
description: "Informazioni su come toocustomize hello data di scadenza dei certificati di federazione e utilizzo dei certificati che toorenew scadrà a breve."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f516f7f0-b25a-4901-8247-f5964666ce23
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/09/2017
ms.author: jeedes
ms.openlocfilehash: e17622d25c9babfa295cc0bb68c24e21b8c574d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-certificates-for-federated-single-sign-on-in-azure-active-directory"></a>Gestione di certificati per accesso Single Sign-On federato in Azure Active Directory
Questo articolo descrive domande più comuni e le informazioni relative a certificati toohello che Azure Active Directory (Azure AD) Crea tooestablish federata applicazioni single sign-on (SSO) tooyour SaaS. Aggiungere le applicazioni dalla raccolta di app di Azure AD hello o utilizzando un modello di applicazione non di raccolta. Configurare un'applicazione hello utilizzando l'opzione di SSO federato hello.

In questo articolo è tooapps solo pertinenti che sono configurati toouse SSO AD Azure tramite la federazione SAML, come illustrato nell'esempio seguente hello:

![Single Sign-On di Microsoft Azure AD](./media/active-directory-sso-certs/saml_sso.PNG)

## <a name="auto-generated-certificate-for-gallery-and-non-gallery-applications"></a>Certificato generato automaticamente per le applicazioni incluse e non incluse nella raccolta
Quando si aggiunge una nuova applicazione dalla raccolta hello e configurare un sign-on basato su SAML, Azure AD genera un certificato per l'applicazione hello che sono valida per tre anni. È possibile scaricare il certificato da hello **certificato di firma SAML** sezione. Per le applicazioni di raccolta, un certificato di opzione toodownload hello o i metadati, in base al requisito di hello di un'applicazione hello potrebbe essere in questa sezione.

![Accesso Single Sign-On di Azure AD](./media/active-directory-sso-certs/saml_certificate_download.png)

## <a name="customize-hello-expiration-date-for-your-federation-certificate-and-roll-it-over-tooa-new-certificate"></a>Personalizzare la data di scadenza hello per il certificato di federazione e viene continuata tooa nuovo certificato
Per impostazione predefinita, i certificati sono tooexpire dopo tre anni. È possibile scegliere una data di scadenza diversa per il certificato completando hello alla procedura seguente.
Hello catture di schermata usano Salesforce per i migliori risultati di esempio hello, ma questi passaggi è possono applicare app SaaS tooany federata.

1. In hello [portale di Azure](https://aad.portal.azure.com), fare clic su **applicazione aziendale** in hello riquadro sinistro e quindi fare clic su **nuova applicazione** su hello **Panoramica** pagina:

   ![Configurazione guidata di hello aprire SSO](./media/active-directory-sso-certs/enterprise_application_new_application.png)

2. Eseguire la ricerca di un'applicazione hello raccolta e quindi selezionare un'applicazione hello che si desidera tooadd. Se non è possibile trovare un'applicazione hello necessario, aggiungere un'applicazione hello utilizzando hello **applicazione Non raccolta** opzione. Questa funzionalità è disponibile solo in SKU di Azure AD Premium (P1 e P2) hello.

    ![Accesso Single Sign-On di Azure AD](./media/active-directory-sso-certs/add_gallery_application.png)

3. Fare clic su hello **Single sign-on** collegamento hello lasciato riquadro e impostare **modalità Single Sign-on** troppo**basato su SAML Sign-on**. Questo passaggio genera un certificato valido tre anni per l'applicazione.

4. toocreate un nuovo certificato, fare clic su hello **Crea nuovo certificato** collegamento hello **certificato di firma SAML** sezione.

    ![Genera un nuovo certificato](./media/active-directory-sso-certs/create_new_certficate.png)

5. Hello **creare un nuovo certificato** collegamento apre il controllo di calendario hello. È possibile impostare qualsiasi data e ora backup toothree anni da hello data corrente. Hello selezionato data e ora è nuova data di scadenza hello e l'ora del nuovo certificato. Fare clic su **Salva**.

    ![È possibile scaricare, quindi caricare il certificato di hello](./media/active-directory-sso-certs/certifcate_date_selection.PNG)

6. Nuovo certificato hello è ora disponibile toodownload. Fare clic su hello **certificato** toodownload di collegamento è. Per il momento il certificato non è attivo. Quando si desidera tooroll sulla toothis certificato, selezionare hello **attivare di nuovo certificato** casella di controllo e fare clic su **salvare**. Da questo punto, Azure AD avvia usando di hello nuovo certificato per la firma risposta hello.

7.  toolearn come certificato di hello tooupload particolare applicazione SaaS di tooyour, fare clic su hello **tutorial di configurazione dell'applicazione di visualizzazione** collegamento.

## <a name="renew-a-certificate-that-will-soon-expire"></a>Rinnovare un certificato con scadenza imminente
procedura di rinnovo Hello dovrebbe restituire alcun tempo di inattività significativi per gli utenti. schermate di Hello in questa sezione caratteristica Salesforce un esempio, ma questi passaggi è possono applicare app SaaS tooany federata.

1. In hello **Azure Active Directory** applicazione **Single sign-on** pagina, generare hello nuovo certificato per l'applicazione. È possibile farlo facendo hello **Crea nuovo certificato** collegamento hello **certificato di firma SAML** sezione.

    ![Genera un nuovo certificato](./media/active-directory-sso-certs/create_new_certficate.png)

2. Lo si desidera seleziona hello data di scadenza e l'ora per il nuovo certificato e fare clic su **salvare**.

3. Scaricare il certificato di hello in hello **certificato di firma SAML** opzione. Schermata di configurazione di single sign-on caricamento hello certificato toohello SaaS della nuova applicazione. toolearn come toodo per l'applicazione SaaS specifica, fare clic su hello **tutorial di configurazione dell'applicazione di visualizzazione** collegamento.
   
4. nuovo certificato hello tooactivate in Azure AD, seleziona hello **attivare di nuovo certificato** casella di controllo e fare clic su hello **salvare** pulsante nella parte superiore di hello della pagina hello. Si esegue il rollup sul nuovo certificato hello in Azure Active Directory lato hello. Modifica stato Hello del certificato hello da **New** troppo**Active**. Da questo punto, Azure AD avvia usando di hello nuovo certificato per la firma risposta hello. 
   
    ![Genera un nuovo certificato](./media/active-directory-sso-certs/new_certificate_download.png)

## <a name="related-articles"></a>Articoli correlati
* [Elenco di esercitazioni sull'App SaaS toointegrate con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Risoluzione dei problemi dell'accesso Single Sign-On basato su SAML](active-directory-saml-debugging.md)
