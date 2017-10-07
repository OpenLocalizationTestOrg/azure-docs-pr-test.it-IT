---
title: 'Esercitazione: Integrazione di Azure Active Directory con 123ContactForm | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e 123ContactForm.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5211910a-ab96-4709-959a-524c4d57c43e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 931255887845edd1aa7f53b9051a82a2f898e055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-123contactform"></a>Esercitazione: Integrazione di Azure Active Directory con 123ContactForm

In questa esercitazione, è illustrato come 123ContactForm toointegrate con Azure Active Directory (Azure AD).

Integrazione 123ContactForm con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso too123ContactForm
- È possibile abilitare il get tooautomatically utenti connesso too123ContactForm (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con 123ContactForm tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di 123ContactForm abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di 123ContactForm dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-123contactform-from-hello-gallery"></a>Aggiunta di 123ContactForm dalla raccolta hello
integrazione hello tooconfigure di 123ContactForm in Azure AD, è necessario 123ContactForm tooadd dall'elenco di tooyour hello raccolta di App SaaS gestite.

**123ContactForm tooadd dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **123ContactForm**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_search.png)

5. Nel riquadro dei risultati hello, selezionare **123ContactForm**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con 123ContactForm mediante un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in 123ContactForm è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in 123ContactForm deve toobe stabilita.

In 123ContactForm, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con 123ContactForm, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test 123ContactForm](#creating-a-123contactform-test-user)**  -toohave un equivalente di Britta Simon in 123ContactForm che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione 123ContactForm.

**Azure AD tooconfigure single sign-on con 123ContactForm, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **123ContactForm** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_samlbase.png)

3. In hello **123ContactForm dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **modalità avviata da IDP**, eseguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/url1.png)

    a. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`

    b. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`

4. Se si desidera in un'applicazione hello tooconfigure **modalità iniziata da SP**, eseguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/url2.png)

    a. Fare clic su hello **Mostra URL impostazioni avanzate** opzione

    b. In hello **URL di accesso** casella di testo, digitare un URL come:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, È necessario tooupdate questi valore effettivo URL e l'identificatore di cui è illustrato più avanti nell'esercitazione di hello.
    
5. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_certificate.png) 

6. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/tutorial_general_400.png)

7. tooconfigure single sign-on sul **123ContactForm** sul lato, andare troppo[https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) ed eseguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/submit.png) 

    a. In hello **posta elettronica** casella di testo, posta elettronica hello tipo di nome utente hello **BrittaSimon@Contoso.com**.

    b. Fare clic su **caricare** ed esplorare hello file Metadata XML, che è stato scaricato dal portale di Azure.

    c. Fare clic su **SUBMIT FORM** (Invia modulo).

8. In hello **AD-Single sign on a Microsoft Azure Configura impostazioni App** eseguire hello alla procedura seguente:
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/url3.png)

    a. Se si desidera in un'applicazione hello tooconfigure **modalità avviata da IDP**, hello copia **identificatore** valore per l'istanza e incollarlo in **identificatore** casella di testo in **123ContactForm dominio e gli URL** sezione nel portale di Azure.
    
    b. Se si desidera in un'applicazione hello tooconfigure **modalità avviata da IDP**, hello copia **URL di risposta** valore per l'istanza e incollarlo in **URL di risposta** casella di testo in **123ContactForm dominio e gli URL** sezione nel portale di Azure.

    c. Se si desidera in un'applicazione hello tooconfigure **modalità iniziata da SP**, hello copia **SIGN ON URL** valore per l'istanza e incollarlo in **URL di accesso** casella di testo in **123ContactForm dominio e gli URL** sezione nel portale di Azure.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-123contactform-test-user"></a>Creazione di un utente test di 123ContactForm

L'applicazione supporta solo in tempo il provisioning dell'utente e dopo l'autenticazione degli utenti verrà creato automaticamente in un'applicazione hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso too123ContactForm.

![Assegna utente][200] 

**tooassign Britta Simon too123ContactForm, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **123ContactForm**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro 123ContactForm hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour 123ContactForm applicazione.
Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_203.png

