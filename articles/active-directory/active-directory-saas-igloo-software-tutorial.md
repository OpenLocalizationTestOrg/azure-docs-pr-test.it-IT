---
title: 'Esercitazione: Integrazione di Azure Active Directory con Igloo Software | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Igloo Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 406405d4faa6e56f1005a61e69a29ef2ef2eb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a>Esercitazione: Integrazione di Azure Active Directory con Igloo Software

In questa esercitazione, è illustrato come toointegrate Igloo Software con Azure Active Directory (Azure AD).

Integrazione di Igloo Software con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooIgloo Software
- È possibile abilitare l'utenti tooautomatically get connesso tooIgloo Software (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Igloo Software tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Igloo Software abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Igloo Software dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-igloo-software-from-hello-gallery"></a>Aggiunta di Igloo Software dalla raccolta hello
integrazione hello tooconfigure di Igloo Software in Azure AD, è necessario tooadd Igloo Software dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Igloo Software dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Igloo Software**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. Nel riquadro dei risultati hello, selezionare **Igloo Software**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Igloo Software mediante un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Igloo Software è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Igloo Software richiede toobe stabilita.

In Igloo Software, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e test Azure single sign-on AD con Igloo Software, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Igloo Software](#creating-an-igloo-software-test-user)**  -toohave un equivalente di Britta Simon in Igloo Software che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Igloo Software.

**Azure AD tooconfigure single sign-on con Igloo Software, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Igloo Software** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. In hello **Igloo Software dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.igloocommmunities.com`

    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.igloocommmunities.com/saml.digest`

    c. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.igloocommmunities.com/saml.digest`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On. Contatto [team di supporto Igloo Software Client](https://www.igloosoftware.com/services/support) tooget questi valori. 

4. In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. In hello **Igloo Software configurazione** fare clic su **Configura Igloo Software** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. In una finestra del web browser, accedere come amministratore nel sito della società Igloo Software di tooyour.

8. Passare toohello **Pannello di controllo**.
   
     ![Pannello di controllo](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Pannello di controllo")

9. In hello **appartenenza** scheda, fare clic su **Sign In Settings**.
   
    ![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")

10. Nella sezione di configurazione SAML hello, fare clic su **Configure SAML Authentication**.
   
    ![Configurazione SAML](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "Configurazione SAML")
   
11. In hello **configurazione generale** seguire hello alla procedura seguente:
   
    ![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")

    a. In hello **nome connessione** casella di testo, digitare un nome personalizzato per la configurazione.
   
    b. In hello **IdP Login URL** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.
   
    c. In hello **IdP Logout URL** casella di testo, hello Incolla valore **Sign-Out URL** che è stato copiato dal portale di Azure.
    
    d. Selezionare **Logout Response and Request HTTP Type** (Risposta di disconnessione e tipo di richiesta HTTP) con l'impostazione **POST**.
   
    e. Aprire il **base 64** codificato nel blocco note scaricato dal portale di Azure, hello copia del contenuto di esso negli Appunti, certificato e quindi incollarlo toohello **certificato pubblico** casella di testo.
    
12. In hello **Response and Authentication Configuration**, eseguire hello alla procedura seguente:
    
    ![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")
  
      a. In **Provider di identità** selezionare **Microsoft ADFS**.
      
      b. In **Tipo di identificatore** selezionare **Indirizzo e-mail**. 

      c. In hello **Email Attribute** casella tipo **emailaddress**.

      d. In hello **First Name Attribute** casella tipo **givenname**.

      e. In hello **Last Name Attribute** casella tipo **surname**.

13. Eseguire hello seguente passaggi toocomplete hello configurazione:
    
    ![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in") 

     a. In **User creation on Sign in** (Creazione utente all'accesso) selezionare **Create a new user in your site when they sign in** (Creare un nuovo utente all'accesso).

     b. In **Impostazioni di accesso** selezionare **Usa pulsante SAML nella schermata di accesso**.

     c. Fare clic su **Salva**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-an-igloo-software-test-user"></a>Creazione di un utente test di Igloo Software

Non sono presenti elementi di azione per si tooconfigure di provisioning dell'utente tooIgloo Software.  

Quando un utente assegnato tenta di toolog in tooIgloo Software hello Pannello di accesso, Igloo Software verifica l'esistenza di utente hello.  Se l'account utente non è presente, Igloo Software lo crea automaticamente.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooIgloo Software.

![Assegna utente][200] 

**tooassign Britta Simon tooIgloo Software, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Igloo Software**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Igloo Software hello in hello Pannello di accesso, è necessario ottenere applicazione Igloo Software tooyour automaticamente firmato-on.
Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

