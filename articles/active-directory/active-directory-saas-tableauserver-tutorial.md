---
title: 'Esercitazione: Integrazione di Azure Active Directory con Tableau Server | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Tableau Server.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: feb2087bd6ae6ddcb920901e6719688fc95ae287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a>Esercitazione: Integrazione di Azure Active Directory con Tableau Server

In questa esercitazione, è illustrato come toointegrate Tableau Server con Azure Active Directory (Azure AD).

Integrazione di Server Tableau con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooTableau Server
- È possibile abilitare l'utenti tooautomatically get connesso tooTableau Server (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Server Tableau tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Tableau Server abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Server Tableau dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-tableau-server-from-hello-gallery"></a>Aggiunta di Server Tableau dalla raccolta hello
integrazione hello tooconfigure di Tableau Server in Azure AD, è necessario tooadd Tableau Server dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Tableau Server dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Tableau Server**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. Nel riquadro dei risultati hello, selezionare **Tableau Server**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Tableau Server usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Server Tableau è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in Server Tableau deve toobe stabilita.

Nel Server Tableau, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con Server Tableau, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Tableau Server](#creating-a-tableau-server-test-user)**  -toohave un equivalente di Britta Simon Tableau server che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Server Tableau.

**Azure AD tooconfigure single sign-on con Server Tableau, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Tableau Server** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. In hello **Tableau dominio del Server e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://azure.<domain name>.link`
    
    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://azure.<domain name>.link`

    c. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://azure.<domain name>.link/wg/saml/SSO/index.html`
     
    > [!NOTE] 
    > Hello valori precedenti non sono valori reali. In un secondo momento, aggiornare i valori hello con URL effettivo hello e l'identificatore dalla pagina di configurazione Server Tableau hello. 

4. Applicazione Server tableau prevede asserzioni SAML hello in un formato specifico. Configurare hello seguendo le attestazioni per questa applicazione. È possibile gestire i valori hello di questi attributi da hello **"Attributi utente"** sezione nella pagina di integrazione dell'applicazione. Hello schermata riportata di seguito viene illustrato un esempio di hello stesso.
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nell'immagine di hello precedente ed eseguire hello alla procedura seguente:
    
    | Nome attributo | Valore attributo |
    | ---------------| --------------- |    
    | username | *user.displayname* |

    a. Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    b. In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.
    
    c. Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.
    
    d. Fare clic su **Ok**


6. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. Fare clic sul pulsante **Salva** .

    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS>
8. tooget SSO configurato per l'applicazione, è necessario tooyour toosign-nel tenant di Tableau Server come amministratore.
   
   a. In configurazione Server Tableau hello, fare clic su hello **SAML** scheda.
  
    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   b. Selezionare una casella di controllo hello **Use SAML single sign-on**.
   
   c. URL restituito tableau Server: URL del Server Tableau gli utenti accedono, ad esempio http://tableau_server hello. Non è consigliabile utilizzare http://localhost. Gli URL con barra finale (ad esempio http://tableau_server/) non sono supportati. Copia **URL restituito Server Tableau** e incollarlo tooAzure AD **URL di accesso** nella casella di testo **Tableau dominio del Server e gli URL** sezione.
   
   d. ID entità SAML: hello entity ID che identifica in modo univoco il toohello di installazione Server Tableau IdP. È possibile immettere l'URL del Server Tableau nuovamente in questo caso, se si desidera, ma non è toobe l'URL del Server Tableau. Copia **ID entità SAML** e incollarlo tooAzure AD **identificatore** nella casella di testo **Tableau dominio del Server e gli URL** sezione.
     
   e. Fare clic su hello **Esporta File di metadati** e aprirlo in un'applicazione hello testo dell'editor. Individuare l'URL di servizio Consumer di asserzione con Http Post e indice 0 e copia hello URL. Ora incollarlo tooAzure AD **URL di risposta** nella casella di testo **Tableau dominio del Server e gli URL** sezione.
   
   f. Individuare il file di metadati di federazione scaricato dal portale di Azure e quindi caricarlo in hello **file di metadati del provider di identità SAML**.
   
   g. Fare clic su hello **OK** nella pagina Configurazione Server Tableau hello.
   
    >[!NOTE] 
    >Cliente tooupload qualsiasi certificato nella configurazione di hello Tableau Server SAML SSO e si verrà ottenere ignorato in hello flusso SSO.
    >Se si devono consentire la configurazione SAML nel Server Tableau, vedere l'articolo toothis [configurare SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).
    >
<CE>

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-tableau-server-test-user"></a>Creazione di un utente test di Tableau Server

obiettivo di Hello di questa sezione è un utente denominato Britta Simon Tableau server toocreate. È necessario tooprovision tutti gli utenti di hello server Tableau hello. 

Nome utente dell'utente hello deve corrispondere il valore hello che è stato configurato nell'attributo personalizzato di hello Azure AD di **username**. Con hello corretto mapping integrazione hello dovrebbe funzionare [configurazione Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).

>[!NOTE]
>Se è necessario un utente toocreate manualmente, è necessario toocontact messaggio Tableau Server per l'amministratore dell'organizzazione.
> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooTableau Server.

![Assegna utente][200] 

**tooassign Britta Simon tooTableau Server, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Tableau Server**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Server Tableau hello in hello Pannello di accesso, è necessario ottenere l'applicazione Server Tableau tooyour automaticamente firmato-on.
Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

