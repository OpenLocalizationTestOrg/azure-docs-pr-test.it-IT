---
title: 'Esercitazione: integrazione di Azure Active Directory con LinkedIn Lookup| Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e la ricerca di LinkedIn.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: d79c34baa676391699e4b49806f16422fcfe73e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a>Esercitazione: Integrazione di Azure Active Directory con LinkedIn Lookup

In questa esercitazione, è illustrato come toointegrate ricerca LinkedIn con Azure Active Directory (Azure AD).

Integrazione di ricerca di LinkedIn con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooLinkedIn ricerca
- È possibile abilitare l'utenti tooautomatically get connesso tooLinkedIn ricerca (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con ricerca LinkedIn tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di LinkedIn Lookup abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di ricerca di LinkedIn dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-linkedin-lookup-from-hello-gallery"></a>Aggiunta di ricerca di LinkedIn dalla raccolta hello
integrazione hello tooconfigure di ricerca di LinkedIn in Azure AD, è necessario tooadd LinkedIn ricerca dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd ricerca LinkedIn dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic su **nuova applicazione** pulsante nella parte superiore di hello di hello finestra di dialogo tooadd nuova applicazione.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **LinkedIn ricerca**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. Nel riquadro dei risultati hello, selezionare **ricerca LinkedIn**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con LinkedIn Lookup in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in ricerca di LinkedIn è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in ricerca di LinkedIn deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** nella ricerca di LinkedIn.

tooconfigure e prova AD Azure single sign-on con LinkedIn ricerca, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test ricerca LinkedIn](#creating-an-linkedin-lookup-test-user)**  -toohave un equivalente di Britta Simon nella ricerca di LinkedIn che è la rappresentazione toohello collegato AD Azure.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione di ricerca di LinkedIn.

**Azure AD tooconfigure single sign-on con ricerca LinkedIn, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **ricerca LinkedIn** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo, nella **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. In una finestra del web browser, accesso tooyour **ricerca LinkedIn** sito Web come amministratore.

4. In **Account Center** (Centro account) fare clic su **Global Settings** (Impostazioni globali) in **Settings** (Impostazioni). Selezionare inoltre **ricerca** dall'elenco a discesa hello.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. Fare clic su **o fare clic qui tooload e copia dei singoli campi modulo hello** e copia **Id entità** e **Url asserzione Consumer accesso (ACS)**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. Nel portale di Azure in **URL e il dominio di ricerca di LinkedIn** seguire hello procedura seguente se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    a. In hello **identificatore** casella di testo immettere hello **ID entità** copiata dal portale di LinkedIn 

    b. In hello **URL di risposta** casella di testo immettere hello **Url asserzione Consumer accesso (ACS)** copiata dal portale di LinkedIn

7. Controllare **Mostra URL impostazioni avanzate**, se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`
     
    > [!NOTE] 
    > Questo non è il valore reale. utente Hello presenta tooupdate questi valori con hello URL effettivo Sign-On. Contatto [team di supporto Client di LinkedIn ricerca](https://business.LinkedIn.com/lookup) tooget questo valore.

8. Il **ricerca LinkedIn** asserzioni SAML hello prevista dall'applicazione in un formato specifico. Hello utente dispone di configurazione di attributi del token SAML tooadd attributo personalizzato mapping toohello. Hello seguente schermata mostra un esempio. il valore predefinito di Hello **identificatore utente** è **User** ma LinkedIn ricerca prevede che questo toobe mappato con indirizzo di posta elettronica dell'utente hello. È possibile utilizzare **user.mail** attributo dall'elenco hello o utilizzare il valore di attributo appropriato hello in base alla configurazione dell'organizzazione. 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. In **gli attributi utente** fare clic su **visualizzare e modificare tutti gli altri attributi utente** e impostare gli attributi di hello. Hello utente necessita di attestazioni di quattro tooadd denominate **posta elettronica**, **reparto**, **firstname**, e **lastname** e il valore di hello è mappata a toobe **user.mail**, **Department**, **user.givenname**, e **user.surname** rispettivamente

    | Nome attributo | Valore attributo |
    | --- | --- |
    | email| user.mail |    
    | department| user.department |
    | firstname| user.givenname |
    | lastname| user.surname |

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    a. Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    b. In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.
    
    c. Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.
    
    d. Fare clic su **Ok**

10. Eseguire hello seguendo i passaggi hello **nome** - attributo

    a. Fare clic su hello tooopen di attributo hello **Modifica attributo** finestra.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    b. Eliminare il valore di URL hello dalla hello **dello spazio dei nomi**.
    
    c. Fare clic su **Ok** impostazione hello toosave.

10. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. Andare troppo**le impostazioni di amministrazione di LinkedIn** sezione. File XML di hello caricamento è stato scaricato dal portale di Azure hello facendo hello **file caricare XML** opzione.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. Fare clic su **su** tooenable SSO. Modifica stato SSO da **non connesso** troppo**connesso**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. Fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **Britta Simon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di Britta Simon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-an-linkedin-lookup-test-user"></a>Creazione di un utente test di LinkedIn Lookup

Applicazione di ricerca collegato supporta immediatamente in il provisioning dell'utente di tempo (JIT) e dopo l'autenticazione degli utenti viene creato automaticamente in un'applicazione hello. Attivare **automaticamente assegnare licenze** tooassign un utente toohello di licenza.
   
   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooLinkedIn ricerca.

![Assegna utente][200] 

**tooassign Britta Simon tooLinkedIn ricerca, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **LinkedIn ricerca**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.

    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic hello LinkedIn ricerca riquadro in hello Pannello di accesso, dovrebbe essere reindirizzato tooOrganizational pagina in cui occorre tooprovide i dettagli dell'account personali LinkedIn. In questo modo l'account personale viene collegato all'account aziendale di LinkedIn. 

Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

