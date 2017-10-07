---
title: 'Esercitazione: Integrazione di Azure Active Directory con LinkedIn Learning| Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e l'apprendimento di LinkedIn.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 14610a25132ed0ccf5892cad6ccc4e1ef03ff280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a>Esercitazione: Integrazione di Azure Active Directory con LinkedIn Learning

In questa esercitazione, è illustrato come toointegrate Learning LinkedIn con Azure Active Directory (Azure AD).

Integrazione di apprendimento di LinkedIn con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooLinkedIn di apprendimento
- È possibile abilitare il get tooautomatically utenti connesso tooLinkedIn Learning (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Learning LinkedIn tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di LinkedIn Learning abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di apprendimento LinkedIn dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-linkedin-learning-from-hello-gallery"></a>Aggiunta di apprendimento LinkedIn dalla raccolta hello
integrazione hello tooconfigure di LinkedIn apprendimento in Azure AD, è necessario tooadd LinkedIn Learning dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Learning LinkedIn dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **LinkedIn Learning**. Dal riquadro dei risultati, fare clic su **LinkedIn Learning** tooadd un'applicazione hello.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con LinkedIn Learning in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Learning LinkedIn è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in LinkedIn Learning richiede toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Learning LinkedIn.

tooconfigure e prova AD Azure single sign-on con LinkedIn Learning, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test LinkedIn Learning](#creating-a-linkedin-learning-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Learning LinkedIn.

**Azure AD tooconfigure single sign-on con Learning LinkedIn, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **LinkedIn Learning** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. In una finestra del web browser, tenant LinkedIn Learning tooyour accesso come amministratore.

4. In **Account Center** (Centro account) fare clic su **Global Settings** (Impostazioni globali) in **Settings** (Impostazioni). Selezionare inoltre **Learning - predefinito** dall'elenco a discesa hello.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. Fare clic su **o fare clic qui tooload e copia dei singoli campi modulo hello** e copia **Id entità** e **Url asserzione Consumer accesso (ACS)**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. Nel portale di Azure in **LinkedIn Learning dominio e gli URL**, eseguire i passaggi se si desidera tooconfigure SSO hello in **avviata da IdP** modalità

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    a. In hello **identificatore** casella di testo immettere hello **ID entità** copiata dal portale di LinkedIn 

    b. In hello **URL di risposta** casella di testo immettere hello **Url asserzione Consumer accesso (ACS)** copiata dal portale di LinkedIn

7. Se si desidera tooconfigure SSO in **SP Initiated**, quindi fare clic su Mostra avanzate URL opzione di impostazione nella sezione di configurazione hello e configurare URL hello-sign-on con hello seguente motivo:

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. L'applicazione di apprendimento LinkedIn prevede asserzioni SAML hello in un formato specifico, che richiede di tooadd attributo personalizzato configurazione dei mapping tooyour SAML degli attributi del token. Hello seguente schermata mostra un esempio per questo oggetto. il valore predefinito di Hello **identificatore utente** è **User** ma LinkedIn Learning prevede che questo toobe mappato con indirizzo di posta elettronica dell'utente hello. A tale scopo è possibile utilizzare **user.mail** attributo dall'elenco hello o utilizzare il valore di attributo appropriato hello in base alla configurazione dell'organizzazione. 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. In **gli attributi utente** fare clic su **visualizzare e modificare tutti gli altri attributi utente** e impostare gli attributi di hello. Hello utente necessita di attestazioni di quattro tooadd denominate **posta elettronica**, **reparto**, **firstname**, e **lastname** e il valore di hello è mappata a toobe **user.mail**, **Department**, **user.givenname**, e **user.surname** rispettivamente

    | Nome attributo | Valore attributo |
    | --- | --- |
    | email| user.mail |    
    | department| user.department |
    | firstname| user.givenname |
    | lastname| user.surname |
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    a. Fare clic su **Aggiungi attributo** tooopen finestra di dialogo attributo hello.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    b. In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.
    
    c. Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.
    
    d. Fare clic su **Ok**

10. Eseguire hello seguendo i passaggi hello **nome** - attributo

    a. Fare clic su hello tooopen di attributo hello **Modifica attributo** finestra.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    b. Eliminare il valore di URL hello dalla hello **dello spazio dei nomi**.
    
    c. Fare clic su **Ok** impostazione hello toosave.

11. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. Fare clic su **Salva**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. Andare troppo**le impostazioni di amministrazione di LinkedIn** sezione. Caricare file XML di hello che è stato scaricato dal portale di Azure hello facendo hello caricare XML file opzione.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. Fare clic su **su** tooenable SSO. Modifica stato SSO da **non connesso** troppo**connesso**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**. 

### <a name="creating-a-linkedin-learning-test-user"></a>Creare un utente test di LinkedIn Learning

L'applicazione LinkedIn Learning supporta Provisioning utente tempo Just-in e dopo l'autenticazione degli utenti vengono creati automaticamente in un'applicazione hello. Nella pagina Impostazioni di amministrazione hello interruttore portale hello capovolto LinkedIn Learning hello **automaticamente assegnare licenze** tooactive tooenable JIT in fase di provisioning e questo verrà assegnato un utente toohello di licenza.
   
   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione, si abilita Britta Simon toouse single sign-on Azure tramite la concessione di accesso tooLinkedIn di apprendimento.

![Assegna utente][200] 

**tooassign tooLinkedIn Britta Simon apprendimento, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **LinkedIn Learning**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro LinkedIn Learning hello in hello Pannello di accesso, è necessario ottenere una pagina di accesso Azure hello e su dopo l'esito positivo sign-on, viene visualizzato nell'applicazione Learning LinkedIn.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png