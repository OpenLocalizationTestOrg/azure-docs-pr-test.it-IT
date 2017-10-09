---
title: 'Esercitazione: Eseguire l''integrazione di Azure Active Directory con vxMaintain | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e vxMaintain.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 937ea276d898986fc5a953c96fddabdc8940309f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a>Esercitazione: Eseguire l'integrazione di Azure Active Directory con vxMaintain

In questa esercitazione, è illustrato come vxMaintain toointegrate con Azure Active Directory (Azure AD).

Questa integrazione offre diversi vantaggi importanti. È possibile:

- Controllo di Azure AD che dispone dell'accesso toovxMaintain.
- Abilitare l'accesso agli utenti tooautomatically toovxMaintain con single sign-on (SSO) utilizzando gli account di Azure AD.
- Gestire gli account in un'unica posizione centrale: hello portale di Azure.

toolearn più sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con vxMaintain tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di vxMaintain abilitata per l'accesso SSO

> [!NOTE]
> Quando si testano passaggi hello in questa esercitazione, è consigliabile non utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, seguire queste indicazioni:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. 

scenario di Hello cui sono illustrati in questa esercitazione è composto da due componenti principali:

* Aggiunta di vxMaintain dalla raccolta hello
* Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="add-vxmaintain-from-hello-gallery"></a>Aggiungere vxMaintain dalla raccolta di hello
integrazione di hello tooconfigure di vxMaintain con Azure AD, è necessario vxMaintain tooadd dall'elenco di tooyour hello raccolta di App SaaS gestite.

vxMaintain tooadd dalla raccolta di hello, hello seguenti:

1. In hello [portale di Azure](https://portal.azure.com), nel riquadro sinistro di hello, selezionare hello **Azure Active Directory** pulsante. 

    ![pulsante di Hello Azure Active Directory][1]

2. Selezionare **Applicazioni aziendali** > **Tutte le applicazioni**.

    ![riquadro "Applicazioni aziendali" Hello][2]
    
3. un'applicazione, in hello tooadd **tutte le applicazioni** nella finestra di dialogo **nuova applicazione**.

    !["Nuova applicazione" Hello pulsante][3]

4. Nella casella di ricerca hello, digitare **vxMaintain**.

    ![elenco a discesa "Modalità Single Sign-on" Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. Selezionare dall'elenco risultati hello **vxMaintain**, quindi selezionare **Aggiungi**.

    ![collegamento vxMaintain Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso SSO di Azure AD con vxMaintain usando un utente di test di nome "Britta Simon".

Per toowork SSO, Azure AD deve utente di Azure AD toohello vxMaintain controparte tooknow hello. Ovvero, è necessario stabilire una relazione di collegamento tra utenti di Azure AD hello e utente vxMaintain corrispondente hello.

relazione di collegamento hello tooestablish, assegnare hello vxMaintain **nome utente** valore come hello Azure AD **Username** valore.

tooconfigure e SSO AD Azure tramite vxMaintain, hello completo seguenti blocchi predefiniti di test.

### <a name="configure-azure-ad-sso"></a>Configurare l'accesso SSO di Azure AD

In questa sezione, è possibile abilitare SSO AD Azure nel portale di Azure hello e configurare SSO nell'applicazione vxMaintain eseguendo hello seguenti:

1. Nel portale di Azure su hello hello **vxMaintain** pagina di integrazione dell'applicazione, seleziona **Single sign-on**.

    ![comando "Single sign-on" Hello][4]

2. tooenable SSO, in hello **modalità Single Sign-on** elenco a discesa, seleziona **basato su SAML Sign-on**.
 
    ![comando "SAML-Sign-on basato su" Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. In **vxMaintain dominio e gli URL**, hello seguenti:

    ![Hello vxMaintain sezione URL e di dominio](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    a. In hello **identificatore** casella, digitare un URL che ha hello la seguente sintassi:`https://<company name>.verisae.com`

    b. In hello **URL di risposta** casella, digitare un URL che ha hello la seguente sintassi:`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`

    > [!NOTE] 
    > Hello valori precedenti non sono reali. Aggiornarli con identificatore effettivo hello e URL di risposta. i valori hello tooobtain, hello contatto [team di supporto vxMaintain](http://www.verisae.com/contact-us).
 
4. In **certificato di firma SAML**selezionare **Metadata XML**e quindi salvare computer tooyour file dei metadati di hello.

    ![la sezione "Certificato di firma SAML" Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. Selezionare **Salva**.

    ![pulsante Salva Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. tooconfigure **vxMaintain** SSO, hello trasmissione scaricato **Metadata XML** file toohello [team di supporto vxMaintain](http://www.verisae.com/contact-us).

> [!TIP]
> Per la configurazione di app hello, è possibile leggere una versione di hello precedenti istruzioni in hello concisa [portale di Azure](https://portal.azure.com). Dopo aver aggiunto l'applicazione hello da hello **Active Directory** > **applicazioni aziendali** sezione, seleziona hello **Single Sign-On** e quindi hello accesso documentazione fornita dal hello incorporato **configurazione** sezione. 
>
>toolearn più feature hello documentazione incorporati, vedere [gestione di single sign-on per le app aziendali](https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
In questa sezione è creare utente test Britta Simon nel portale di Azure hello eseguendo hello seguenti:

![utente test hello Azure AD][100]

1. In hello **portale di Azure**, nel riquadro sinistro di hello, selezionare hello **Azure Active Directory** pulsante.

    ![pulsante "Azure Active Directory" Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. toodisplay un elenco di utenti, andare troppo**utenti e gruppi** > **tutti gli utenti**.
    
    ![collegano Hello "Tutti gli utenti"](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)  
    Hello **tutti gli utenti** verrà visualizzata la finestra di dialogo. 

3. hello tooopen **utente** nella finestra di dialogo **Aggiungi**.
 
    ![pulsante Aggiungi Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo casella, hello seguenti:
 
    ![finestra di dialogo utente Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    a. In hello **nome** digitare **BrittaSimon**.

    b. In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente di prova Britta Simon.

    c. Seleziona hello **Show Password** casella di controllo, quindi valore hello si noti che è stato generato in hello **Password** casella.

    d. Selezionare **Crea**.
 
### <a name="create-a-vxmaintain-test-user"></a>Creare un utente di test di vxMaintain

In questa sezione viene creato un utente di test di nome Britta Simon in vxMaintain. gli utenti tooadd nella piattaforma vxMaintain hello, utilizzare il [team di supporto vxMaintain](http://www.verisae.com/contact-us). Prima di utilizzare SSO, creare e attivare gli utenti di hello.

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare l'utente test Britta Simon toouse SSO di Azure concessione dell'accesso toovxMaintain. toodo in tal caso, hello seguenti:

![Utente test nell'elenco nome visualizzato hello][200] 

1. Nel portale di Azure hello **applicazioni** visualizzare, andare troppo**Directory** Vista > **applicazioni aziendali** > **tutteleapplicazioni**.

    ![collegano Hello "Tutte le applicazioni"][201] 

2. In hello **applicazioni** elenco, selezionare **vxMaintain**.

    ![collegamento vxMaintain Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. Nel riquadro sinistro hello selezionare **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202] 

4. Selezionare **Aggiungi** e quindi nel hello **Aggiungi** riquadro, selezionare **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][203]

5. In hello **utenti e gruppi** della finestra di dialogo hello **utenti** elenco, selezionare **Britta Simon**, quindi selezionare hello **selezionare** pulsante.

7. In hello **Aggiungi** nella finestra di dialogo **assegnare**.
    
### <a name="test-your-azure-ad-single-sign-on"></a>Testare l'accesso Single Sign-On di Azure AD

In questa sezione verificare la configurazione di SSO AD Azure tramite hello Pannello di accesso.

Se si seleziona hello **vxMaintain** riquadro nel Pannello di accesso hello deve eseguire l'accesso tooyour vxMaintain applicazione automaticamente.

Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="next-steps"></a>Passaggi successivi

* [Elenco di esercitazioni sull'integrazione delle app SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

