---
title: Esercitazione Integrazione di Azure Active Directory con Litmos | Documentazione Microsoft
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Litmos.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 026fd10058760f2d63d185ef4aa9d7de3b82525e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a>Esercitazione Integrazione di Azure Active Directory con Litmos

In questa esercitazione, è illustrato come toointegrate Litmos con Azure Active Directory (Azure AD).

Integrazione Litmos con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooLitmos.
- È possibile abilitare l'utenti tooautomatically get connesso tooLitmos (Single Sign-On) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Litmos tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Litmos abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Litmos dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-litmos-from-hello-gallery"></a>Aggiunta di Litmos dalla raccolta hello
integrazione hello tooconfigure di Litmos in Azure AD, è necessario tooadd Litmos dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Litmos dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![pulsante di Hello Azure Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, digitare **Litmos**selezionare **Litmos** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Nell'elenco risultati hello Litmos](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Litmos usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Litmos è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Litmos deve toobe stabilita.

In Litmos, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con Litmos, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un utente test Litmos](#create-a-litmos-test-user)**  -toohave un equivalente di Britta Simon in Litmos che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Litmos.

**Azure AD tooconfigure single sign-on con Litmos, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Litmos** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. In hello **Litmos dominio e gli URL** seguire hello alla procedura seguente:

    ![Informazioni sul Single Sign-On di URL e dominio di Litmos](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    a. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.litmos.com/account/Login`

    b. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.litmos.com/integration/samllogin`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello identificatore e Reply URL effettivo, che vengono descritte più avanti nell'esercitazione o contatto [team di supporto Litmos](https://www.litmos.com/contact-us/) tooget questi valori.

4. In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![collegamento al download del certificato Hello](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. Come parte della configurazione di hello, è necessario hello toocustomize **attributi Token SAML** per l'applicazione Litmos.

    ![Sezione relativa all'attributo](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | Nome attributo   | Valore attributo |   
    | ---------------  | ----------------|
    | FirstName |user.givenname |
    | LastName  |user.surname |
    | Email |user.mail |

    a. Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.

    ![Aggiungi attributo](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![Finestra di dialogo Aggiungi attributo](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    b. In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.

    c. Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.
    
    d. Fare clic su **OK**.     

6. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. In un'altra finestra del browser del sito di accesso tooyour Litmos aziendale come amministratore.

8. Nella barra di navigazione hello sul lato sinistro di hello, fare clic su **account**.
   
    ![Sezione relativa agli account sul lato dell'app][22] 

9. Fare clic su hello **integrazioni** scheda.
   
    ![Scheda Integrazione][23] 

10. In hello **integrazioni** scheda, scorrere verso il basso troppo**3rd Party integrazioni**, quindi fare clic su **SAML 2.0** scheda.
   
    ![Sezione SAML 2.0][24] 

11. Copiare il valore di hello in **hello endpoint SAML per litmos:** e incollarlo in hello **URL di risposta** casella di testo in hello **Litmos dominio e gli URL** sezione nel portale di Azure. 
   
    ![Endpoint SAML][26] 

12. Nel **Litmos** applicazione, eseguire hello alla procedura seguente:
    
     ![Applicazione Litmos][25] 
     
     a. Fare clic su **Enable SAML**.
    
     b. Aprire il certificato con codifica base 64 nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato x. 509 SAML** casella di testo.
     
     c. Fare clic su **Salva modifiche**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

   ![Creare un utente test di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.

    ![pulsante Aggiungi Hello](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:

    ![finestra di dialogo utente Hello](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    a. In hello **nome** digitare **BrittaSimon**.

    b. In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.

    c. Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.

    d. Fare clic su **Crea**.
  
### <a name="create-a-litmos-test-user"></a>Creare un utente di test di Litmos

obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Litmos toocreate.  
Hello Litmos applicazione supporta Just-in-Time di provisioning. In questo campo, un account utente viene creato automaticamente se necessario durante un'applicazione di hello tooaccess tentativo utilizzando hello Pannello di accesso.

**un utente denominato Britta Simon in Litmos, toocreate eseguire hello alla procedura seguente:**

1. In un'altra finestra del browser del sito di accesso tooyour Litmos aziendale come amministratore.

2. Nella barra di navigazione hello sul lato sinistro di hello, fare clic su **account**.
   
    ![Sezione relativa agli account sul lato dell'app][22] 

3. Fare clic su hello **integrazioni** scheda.
   
    ![Scheda Integrazioni][23] 

4. In hello **integrazioni** scheda, scorrere verso il basso troppo**3rd Party integrazioni**, quindi fare clic su **SAML 2.0** scheda.
   
    ![SAML 2.0][24] 
    
5. Selezionare **Autogenerate Users**(Genera utenti in automatico)
   
    ![Autogenerate Users (Genera utenti in automatico)][27] 

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooLitmos.

![Assegnazione del ruolo utente hello][200] 

**tooassign Britta Simon tooLitmos, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Litmos**.

    ![collegamento Litmos Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.  

Quando si fa clic hello Litmos riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Litmos applicazione. 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

