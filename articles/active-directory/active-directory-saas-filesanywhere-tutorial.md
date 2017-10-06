---
title: 'Esercitazione: Integrazione di Azure Active Directory con FilesAnywhere | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e FilesAnywhere.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 376364a5c75f8d069ea6390c58586acb378cd8b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a>Esercitazione: Integrazione di Azure Active Directory con FilesAnywhere

In questa esercitazione, è illustrato come toointegrate FilesAnywhere con Azure Active Directory (Azure AD).

Integrazione FilesAnywhere con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooFilesAnywhere
- È possibile abilitare l'utenti tooautomatically get connesso tooFilesAnywhere (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con FilesAnywhere tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di FilesAnywhere abilitata per l'accesso Single Sign-On


> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.


passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione, a meno che non sia necessario.
- Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di FilesAnywhere dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD


## <a name="adding-filesanywhere-from-hello-gallery"></a>Aggiunta di FilesAnywhere dalla raccolta hello
integrazione hello tooconfigure di FilesAnywhere in Azure AD, è necessario tooadd FilesAnywhere dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd FilesAnywhere dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **FilesAnywhere**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. Nel riquadro dei risultati hello, selezionare **FilesAnywhere**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con FilesAnywhere in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in FilesAnywhere è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in FilesAnywhere deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in FilesAnywhere.

tooconfigure e prova AD Azure single sign-on con FilesAnywhere, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test FilesAnywhere](#creating-a-filesanywhere-test-user)**  -toohave un equivalente di Britta Simon in FilesAnywhere toohello collegato AD Azure rappresentazione in seguito.
3. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
4. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nell'applicazione FilesAnywhere.

**Azure AD tooconfigure single sign-on con FilesAnywhere, eseguire hello alla procedura seguente:**

1. Nel portale di gestione di Azure hello in hello **FilesAnywhere** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. In hello **FilesAnywhere dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **modalità avviata da IDP**:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    a. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.filesanywhere.com/saml20.aspx?c=215`
> [!NOTE]
> Si noti il valore di hello **215** è un **clientid** ed è solo un esempio. È necessario tooreplace con valore clientid effettivo hello.

4. In hello **FilesAnywhere dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **modalità iniziata da SP**, eseguire hello alla procedura seguente:
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    a. Fare clic su hello **Mostra URL impostazioni avanzate** opzione

    b. In hello **URL di accesso** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<sub domain>.filesanywhere.com/`

    > [!NOTE] 
    > Si noti che queste non sono valori reali hello. È necessario tooupdate questi valori con hello URL di URL di accesso e di risposta effettivo. Contatto [team di supporto FilesAnywhere](mailto:support@FilesAnywhere.com) tooget questi valori. 

5. Applicazione FilesAnywhere Software prevede asserzioni SAML hello in un formato specifico. Configurare hello seguendo le attestazioni per questa applicazione. È possibile gestire i valori hello di questi attributi da hello "**gli attributi utente**" sezione nella pagina di integrazione dell'applicazione. Hello seguente schermata mostra un esempio per questo oggetto.
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    Hello quando gli utenti effettua l'iscrizione con FilesAnywhere ricevono valore hello **clientid** dall'attributo [FilesAnywhere team](mailto:support@FilesAnywhere.com). È l'attributo "Id Client" hello di tooadd con valore univoco di hello fornito da FilesAnywhere. Tutti gli attributi indicati sopra sono obbligatori.
    > [!NOTE] 
    > Si noti il valore di hello **2331** di **clientid** è solo un esempio. È necessario tooprovide valore effettivo di hello.


6. In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nell'immagine di hello precedente ed eseguire hello alla procedura seguente:
    
    | Nome attributo | Valore attributo |
    | ---------------| --------------- |    
    | clientid | *"uniquevalue"* |

    a. Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    b. In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.
    
    c. Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.
    
    d. Fare clic su **Ok**

7. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. In hello **FilesAnywhere configurazione** fare clic su **configurare FilesAnywhere** tooopen **Configura sign-on** finestra.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. configurazione di SSO tooget completo per l'applicazione alla fine di FilesAnywhere, contattare [team di supporto FilesAnywhere](mailto:support@FilesAnywhere.com) e fornire loro token SAML hello scaricato URL Single Sign On (SSO) e di certificato di firma.

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**. 



### <a name="creating-a-filesanywhere-test-user"></a>Creare un utente test di FilesAnywhere

L'applicazione supporta solo in tempo il provisioning dell'utente e dopo l'autenticazione degli utenti verrà creato automaticamente in un'applicazione hello. 


### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooFilesAnywhere proprio accesso.

![Assegna utente][200] 

**tooassign Britta Simon tooFilesAnywhere, eseguire hello alla procedura seguente:**

1. Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **FilesAnywhere**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    


### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro FilesAnywhere hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour FilesAnywhere applicazione.


## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
