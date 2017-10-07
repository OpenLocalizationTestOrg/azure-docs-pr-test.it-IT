---
title: 'Esercitazione: Integrazione di Azure Active Directory con AirWatch | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e AirWatch.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e5230d5a36824778a4d9804dadf9f13a0d11a68d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a>Esercitazione: Integrazione di Azure Active Directory con AirWatch

In questa esercitazione, è illustrato come toointegrate AirWatch con Azure Active Directory (Azure AD).

Integrazione di AirWatch con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooAirWatch
- È possibile abilitare l'utenti tooautomatically get connesso tooAirWatch (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con AirWatch tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di AirWatch abilitata per l'accesso Single Sign-On.

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di AirWatch dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-airwatch-from-hello-gallery"></a>Aggiunta di AirWatch dalla raccolta hello
integrazione hello tooconfigure di AirWatch in Azure AD, è necessario tooadd AirWatch dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd AirWatch dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **AirWatch**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. Nel riquadro dei risultati hello, selezionare **AirWatch**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con AirWatch con un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in AirWatch è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in AirWatch deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in AirWatch.

tooconfigure e prova AD Azure single sign-on con AirWatch, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test AirWatch](#creating-a-airwatch-test-user)**  -toohave un equivalente di Britta Simon in AirWatch che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione AirWatch.

**Azure AD tooconfigure single sign-on con AirWatch, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **AirWatch** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. In hello **AirWatch dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`

    b. In hello **identificatore** casella di testo, tipo di valore hello di`AirWatch`

    > [!NOTE] 
    > Questo valore non è hello reale. Aggiornare questo valore con URL hello effettivo Sign-on. Contatto [team di supporto Client di AirWatch](http://www.air-watch.com/company/contact-us/) tooget questo valore. 
 
4. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. In hello **AirWatch configurazione** fare clic su **configurare AirWatch** tooopen **Configura sign-on** finestra. Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. Fare clic sul pulsante **Salva** .

    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS>
7. In una finestra del web browser, accedere come amministratore nel sito della società AirWatch di tooyour.

8. Nel riquadro di spostamento a sinistra di hello, fare clic su **account**, quindi fare clic su **amministratori**.
   
   ![Amministratori](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Amministratori")

9. Espandere hello **impostazioni** menu e quindi fare clic su **servizi Directory**.
   
   ![Impostazioni](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Impostazioni")

10. Fare clic su hello **utente** scheda hello **DN di Base** casella di testo, digitare il nome di dominio e quindi fare clic su **salvare**.
   
   ![Utente](./media/active-directory-saas-airwatch-tutorial/ic791922.png "Utente")

11. Fare clic su hello **Server** scheda.
   
   ![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")

12. Eseguire hello alla procedura seguente:
    
    ![Caricamento](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Caricamento")   
    
    a. Per **Directory Type** selezionare **None**.

    b. Selezionare **Use SAML For Authentication**.

    c. tooupload hello certificato scaricato, fare clic su **caricare**.

13. In hello **richiesta** seguire hello alla procedura seguente:
    
    ![Richiesta](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Richiesta")  

    a. Per **Request Binding Type** selezionare **POST**.

    b. Nel portale di Azure su hello hello **Configura accesso single sign-on in Airwatch** nella pagina, hello copia **SAML Single Sign-On Service URL** valore e quindi incollarlo hello **Provider di identità Single Sign On URL** casella di testo.

    c. Per **NameID format** selezionare **Email address**.

    d. Fare clic su **Salva**.

14. Fare clic su hello **utente** scheda nuovamente.
    
    ![Utente](./media/active-directory-saas-airwatch-tutorial/ic791926.png "Utente")

15. In hello **attributo** seguire hello alla procedura seguente:
    
    ![Attributo](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attributo")

    a. In hello **identificatore di oggetto** casella tipo **http://schemas.microsoft.com/identity/claims/objectidentifier**.

    b. In hello **Username** casella tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    c. In hello **nome visualizzato** casella tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.

    d. In hello **nome** casella tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.

    e. In hello **cognome** casella tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.

    f. In hello **posta elettronica** casella tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    g. Fare clic su **Salva**.

<CE>

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di Britta Simon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-airwatch-test-user"></a>Creazione di un utente di test di AirWatch

toolog agli utenti di Azure AD tooenable in tooAirWatch, è necessario eseguirne il provisioning in tooAirWatch.

* Nel caso di AirWatch, il provisioning è un'attività manuale.

**tooprovision un account utente, eseguire hello alla procedura seguente:**

1. Accedi tooyour **AirWatch** sito aziendale come amministratore.
2. Nel riquadro di spostamento hello sul lato sinistro di hello, fare clic su **account**, quindi fare clic su **utenti**.
   
   ![Utenti](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Utenti")
3. In hello **utenti** menu, fare clic su **visualizzazione elenco**, quindi fare clic su **Aggiungi \> Aggiungi utente**.
   
   ![Aggiungere un utente](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Aggiungere un utente")
4. In hello **Add / Edit User** finestra di dialogo, eseguire hello alla procedura seguente:

   ![Aggiungere un utente](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Aggiungere un utente")   
   1. Hello tipo **Username**, **Password**, **Conferma Password**, **nome**, **cognome**,  **Indirizzo di posta elettronica** relative caselle di testo di un valido di Azure all'account di Active Directory desiderata tooprovision in hello.
   2. Fare clic su **Salva**.

>[!NOTE]
>È possibile usare qualsiasi altro AirWatch utente account strumento di creazione o le API fornite da AirWatch tooprovision account utente di AAD.
>  

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooAirWatch.

![Assegna utente][200] 

**tooassign Britta Simon tooAirWatch, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **AirWatch**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello. Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

