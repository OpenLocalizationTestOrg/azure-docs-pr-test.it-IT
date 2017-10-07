---
title: 'Esercitazione: Integrazione di Azure Active Directory con LinkedIn Elevate| Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory ed elevare il livello di LinkedIn.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 189bd72c230be7dc0c0b934f94ea01e84af9ad23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a>Esercitazione: Integrazione di Azure Active Directory con LinkedIn Elevate

In questa esercitazione, è illustrato come toointegrate LinkedIn elevare con Azure Active Directory (Azure AD).

Integrazione di elevare il livello di LinkedIn con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooLinkedIn Esegui con privilegi elevati
- È possibile abilitare l'utenti tooautomatically get connesso tooLinkedIn Esegui con privilegi elevati (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con LinkedIn elevare tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di LinkedIn Elevate abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione, a meno che non sia necessario.
- Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di LinkedIn elevare dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-linkedin-elevate-from-hello-gallery"></a>Aggiunta di LinkedIn elevare dalla raccolta hello
integrazione hello tooconfigure di LinkedIn elevare in Azure AD, è necessario tooadd LinkedIn elevare dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd LinkedIn elevare dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **LinkedIn elevare**. Dal riquadro dei risultati, fare clic su **LinkedIn elevare** tooadd un'applicazione hello.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con LinkedIn Elevate in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in LinkedIn elevare è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato hello LinkedIn elevare deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in elevare il livello di LinkedIn.

tooconfigure e prova AD Azure single sign-on con LinkedIn elevare, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test LinkedIn elevare](#creating-a-linkedin-elevate-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nell'applicazione elevare LinkedIn.

**Azure AD tooconfigure single sign-on con LinkedIn elevare, eseguire hello alla procedura seguente:**

1. Nel portale di gestione di Azure hello in hello **LinkedIn elevare** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. In una finestra del web browser, accesso tooyour LinkedIn elevare tenant come amministratore.

4. In **Account Center** (Centro account) fare clic su **Global Settings** (Impostazioni globali) in **Settings** (Impostazioni). Selezionare inoltre **Elevate - elevare Test AAD** dall'elenco a discesa hello.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. Fare clic su **o fare clic qui tooload e copia dei singoli campi modulo hello** e copia **Id entità** e **Url asserzione Consumer accesso (ACS)**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. Nel portale di Azure, in **LinkedIn elevare il livello di dominio e gli URL**, eseguire i passaggi se si desidera tooconfigure SSO hello in **avviata da IdP** modalità

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    a. In hello **identificatore** casella di testo immettere hello **ID entità** copiata dal portale di LinkedIn 

    b. In hello **URL di risposta** casella di testo immettere hello **Url asserzione Consumer accesso (ACS)** copiata dal portale di LinkedIn

7. Se si desidera tooconfigure SSO in **SP Initiated**, quindi fare clic su Mostra avanzate URL opzione di impostazione nella sezione di configurazione hello e configurare hello accesso URL con modello di hello:

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. L'applicazione di LinkedIn elevare prevede asserzioni SAML hello in un formato specifico, che richiede di tooadd attributo personalizzato configurazione dei mapping tooyour SAML degli attributi del token. Hello seguente schermata mostra un esempio per questo oggetto. il valore predefinito di Hello **identificatore utente** è **User** ma LinkedIn elevare prevede che questo toobe mappato con indirizzo di posta elettronica dell'utente hello. A tale scopo è possibile utilizzare **user.mail** attributo dall'elenco hello o utilizzare il valore di attributo appropriato hello in base alla configurazione dell'organizzazione. 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. In **gli attributi utente** fare clic su **visualizzare e modificare tutti gli altri attributi utente** e impostare gli attributi di hello. È necessario tooadd un'altra attestazione denominata **reparto** e il valore di hello deve toobe mappato troppo**Department**.

    | Nome attributo | Valore attributo |
    | --- | --- |    
    | department| user.department |

      ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      a. Fare clic su nella pagina dettagli di Aggiungi attributo tooopen hello attributo Aggiungi attributo department hello, come illustrato di seguito

      ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      b. Fare clic su **Ok** attributo hello toosave.

      c. Modifica nome hello dell'attributo hello **emailaddress** troppo**posta elettronica**.


10. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. Fare clic su **Salva**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. Andare troppo**le impostazioni di amministrazione di LinkedIn** sezione. Caricare file XML di hello che appena scaricato dal portale di Azure hello facendo clic su hello opzione file caricare XML.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. Fare clic su **su** tooenable SSO. Stato SSO viene modificato da **non connesso** troppo**connesso**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**. 

### <a name="creating-a-linkedin-elevate-test-user"></a>Creare un utente test di LinkedIn Elevate

Applicazione di elevare collegato supporta immediatamente in tempo il provisioning dell'utente e dopo l'autenticazione degli utenti verrà creato automaticamente in un'applicazione hello. Nella pagina di impostazioni di amministrazione di hello interruttore hello LinkedIn elevare portale hello capovolto **automaticamente assegnare licenze** tooactive tooenable JIT in fase di provisioning e questo verrà assegnato un utente toohello di licenza.

   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo proprio tooLinkedIn accesso Esegui con privilegi elevati.

![Assegna utente][200] 

**tooassign Britta Simon tooLinkedIn Esegui con privilegi elevati, eseguire hello alla procedura seguente:**

1. Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **LinkedIn elevare**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro LinkedIn elevare hello in hello Pannello di accesso, è necessario ottenere hello Azure pagina accesso e in a dopo l'esito positivo sign-on, è necessario ottenere LinkedIn elevare nell'applicazione in uso.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Esercitazione: Configurazione di LinkedIn Elevate per il provisioning utenti automatico con Azure Active Directory](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
