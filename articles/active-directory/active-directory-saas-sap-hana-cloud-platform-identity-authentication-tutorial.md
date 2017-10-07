---
title: 'Esercitazione: Integrazione di Azure Active Directory con SAP HANA Cloud Platform Identity Authentication |Microsoft Docs'
description: "Informazioni su come tooconfigure single sign-on tra Azure Active Directory e SAP HANA Cloud Platform identità autenticazione."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 2142770779ddb745555b47fc85b5457b573f9506
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a>Esercitazione: Integrazione di Azure Active Directory con SAP HANA Cloud Platform Identity Authentication

In questa esercitazione, è illustrato come toointegrate SAP HANA Cloud Platform identità autenticazione con Azure Active Directory (Azure AD). Autenticazione dell'identità di SAP HANA Cloud Platform viene utilizzato un proxy IdP tooaccess SAP come applicazioni che utilizzano Azure AD come hello IdP principale.

Integrazione di autenticazione dell'identità di SAP HANA Cloud Platform con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooSAP applicazione
- È possibile abilitare l'utenti tooautomatically get connesso tooSAP applicazioni single sign-on (SSO) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).


## <a name="prerequisites"></a>Prerequisiti

tooconfigure integrazione di Azure AD con l'autenticazione dell'identità di SAP HANA Cloud Platform, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di **SAP HANA Cloud Platform Identity Authentication** abilitata per l'accesso SSO


>[!NOTE] 
>hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.
>

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione, a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.

scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di autenticazione dell'identità di SAP HANA Cloud Platform dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On (SSO) di Microsoft Azure AD

Prima di leggere i dettagli tecnici di hello, è essenziale toounderstand concetti di hello in che eseguirai toolook. Autenticazione dell'identità di SAP HANA Cloud Platform e Azure Active Directory federation Hello consente tooimplement SSO tra applicazioni o servizi protetti da Azure ad (come un provider di identità) con le applicazioni SAP e servizi protetti dall'identità di SAP HANA Cloud Platform Autenticazione.

Attualmente, l'autenticazione identità di SAP HANA Cloud Platform funge da un Provider di identità Proxy tooSAP-applicazioni. Azure Active Directory è a sua volta agisce come hello iniziali di Provider di identità in questa configurazione. 

Hello seguente diagramma viene illustrata questa situazione:    

![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

Con questa configurazione, il tenant di SAP HANA Cloud Platform Identity Authentication viene configurato come applicazione attendibile in Azure Active Directory. 

Tutte le applicazioni SAP e servizi da tooprotect tramite in questo modo vengono configurati successivamente nella console di gestione di autenticazione dell'identità di SAP HANA Cloud Platform hello!

Questo significa che tale autorizzazione per la concessione dell'accesso tooSAP applicazioni e servizi sul posto tootake esigenze in SAP HANA Cloud Platform identità di autenticazione per una configurazione di questo tipo (come tooconfiguring anziché l'autorizzazione in Azure Active Directory).

Tramite la configurazione di autenticazione dell'identità di SAP HANA Cloud Platform come un'applicazione tramite Azure Active Directory Marketplace hello, non è necessario tootake cure attestazioni singole richieste di configurazione / asserzioni SAML e le trasformazioni necessarie tooproduce un token di autenticazione valido per le applicazioni SAP.

>[!NOTE] 
>Attualmente solo Web SSO è stato testato da entrambe le parti. I flussi necessari per la comunicazione da App a API o da API a API dovrebbero funzionare ma non sono ancora stati testati. I test verranno eseguiti come parte delle attività successive.
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-hello-gallery"></a>Aggiungere l'autenticazione dell'identità di SAP HANA Cloud Platform dalla raccolta hello
integrazione hello tooconfigure di SAP HANA Cloud Platform identità autenticazione in Azure AD, è necessario tooadd autenticazione dell'identità di SAP HANA Cloud Platform dall'elenco di tooyour hello raccolta di App SaaS gestite.

**Autenticazione identità dalla raccolta di hello, SAP HANA Cloud Platform tooadd eseguire hello alla procedura seguente:**

1. In hello [ **portale di gestione di Azure**](https://portal.azure.com)via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **autenticazione dell'identità di SAP HANA Cloud Platform**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. Nel riquadro dei risultati hello, selezionare **autenticazione dell'identità di SAP HANA Cloud Platform**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso SSO di Azure AD con SAP HANA Cloud Platform Identity Authentication con un utente test di nome "Britta Simon".

Per toowork SSO, Azure AD deve tooknow quale utente controparte hello in SAP HANA Cloud Platform identità autenticazione è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in SAP HANA Cloud Platform identità autenticazione richiede toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** nell'autenticazione dell'identità di SAP HANA Cloud Platform.

tooconfigure e test SSO AD Azure con l'autenticazione dell'identità di SAP HANA Cloud Platform, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure single sign-on AD](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente di test di autenticazione dell'identità di SAP HANA Cloud Platform](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)**  -toohave un equivalente di Britta Simon in SAP HANA Cloud Platform autenticazione identità che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di accesso single sign-on](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-sso"></a>Configurazione dell'accesso Single Sign-On (SSO) di Microsoft Azure AD

In questa sezione abilitare SSO AD Azure nel portale di gestione di Azure hello e configurare single sign-on nell'applicazione SAP HANA Cloud Platform identità autenticazione.

Applicazione di autenticazione dell'identità di SAP HANA Cloud Platform prevede asserzioni SAML hello in un formato specifico. È possibile gestire i valori hello di questi attributi da hello "**gli attributi utente**" sezione nella pagina di integrazione dell'applicazione. Hello seguente schermata mostra un esempio per questo oggetto.

![Configura accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

**tooconfigure SSO AD Azure con l'autenticazione identità di SAP HANA Cloud Platform, eseguire hello alla procedura seguente:**

1. Nel portale di gestione di Azure hello in hello **autenticazione dell'identità di SAP HANA Cloud Platform** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On][5]

3. In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, se l'applicazione SAP prevede un attributo, ad esempio "firstName". Nella finestra di dialogo di hello SAML degli attributi del token, aggiungere l'attributo "firstName" hello.
 1. Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.
 
    ![Configura accesso Single Sign-On][6]

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. In hello **nome dell'attributo** casella di testo, nome dell'attributo di tipo hello "firstName".
 3. Da hello **valore dell'attributo** elenco, il valore dell'attributo hello selezionare "user.givenname".
 4. Fare clic su **OK**.

4. In hello **URL e il dominio di autenticazione identità SAP HANA Cloud Platform** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. In hello **URL di accesso** casella di testo, digitare hello sign in URL per un'applicazione hello SAP.
 2. In hello **identificatore** casella valore hello del tipo di modello:`<entity-id>.accounts.ondemand.com` 
    * Se non si conosce questo valore, seguire la documentazione di autenticazione dell'identità di SAP HANA Cloud Platform hello [Tenant SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).

5. In hello **configurazione dell'autenticazione identità SAP HANA Cloud Platform** fare clic su **configurare SAP HANA Cloud Platform identità autenticazione** tooopen **configurasign-on** finestra di dialogo. Quindi, fare clic su **metadati XML SAML** e salvare il file hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. tooget SSO configurato per l'applicazione, andare tooSAP Console di amministrazione di identità autenticazione HANA Cloud Platform. URL di Hello è hello seguente motivo:`https://<tenant-id>.accounts.ondemand.com/admin`
 * Quindi, seguire troppo documentazione hello in SAP HANA Cloud Platform identità autenticazione[configura Microsoft Azure AD come Provider di identità aziendale all'autenticazione dell'identità di SAP HANA Cloud Platform](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html). 

7. Nel portale di gestione di Azure hello, fare clic su **salvare** pulsante.
8. Continuare seguendo i passaggi solo se si desidera tooadd e abilitare SSO per un'altra applicazione SAP hello. Ripetere i passaggi in hello sezione "Aggiunta SAP HANA Cloud Platform autenticazione identità dalla raccolta hello" tooadd un'altra istanza di autenticazione dell'identità di SAP HANA Cloud Platform.
9. Nel portale di gestione di Azure hello in hello **autenticazione dell'identità di SAP HANA Cloud Platform** pagina di integrazione dell'applicazione, fare clic su **collegato Sign-on**.

    ![Configurare l'accesso collegato](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. Quindi, salvare la configurazione hello.

>[!NOTE] 
>nuova applicazione Hello sfruttano la configurazione di SSO hello per un'applicazione hello precedente SAP. Assicurarsi di utilizzare hello stesso provider di identità aziendale nella Console di amministrazione di SAP HANA Cloud Platform identità autenticazione hello.
>

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
obiettivo di Hello di questa sezione è toocreate un utente di test nel nuovo portale hello chiamato Britta Simon.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. In hello **nome** casella tipo **BrittaSimon**.
  2. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.
  3. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.
  4. Fare clic su **Crea**. 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a>Creare un utente test di SAP HANA Cloud Platform Identity Authentication

Non è necessario un utente nell'autenticazione dell'identità di SAP HANA Cloud Platform toocreate. Gli utenti che sono nell'archivio utente hello Azure AD possono usare funzionalità SSO hello.

Autenticazione dell'identità di SAP HANA Cloud Platform supporta l'opzione di federazione delle identità di hello. Questa opzione consente toocheck applicazione hello in presenza di utenti hello autenticati dal provider di identità aziendale hello in hello archivio di SAP HANA Cloud Platform identità autenticazione utente. 

In impostazione hello, hello opzione federazione delle identità è disabilitato. Se è abilitata la federazione delle identità, solo gli utenti di hello che vengono importati nell'autenticazione dell'identità di SAP HANA Cloud Platform sono in grado di tooaccess un'applicazione hello. 

Per ulteriori informazioni su come tooenable o federazione delle identità con l'autenticazione identità di SAP HANA Cloud Platform, disabilitare la funzione vedere abilitare la federazione delle identità con l'autenticazione dell'identità in SAP HANA Cloud Platform [Configura federazione identità con hello archivio di SAP HANA Cloud Platform identità autenticazione utente. ](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo proprio tooSAP accesso autenticazione dell'identità di HANA Cloud Platform.

![Assegna utente][200] 

**tooassign Britta Simon tooSAP autenticazione dell'identità di HANA Cloud Platform, eseguire hello alla procedura seguente:**

1. Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **autenticazione dell'identità di SAP HANA Cloud Platform**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    

### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione è verificare la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro di autenticazione dell'identità di SAP HANA Cloud Platform hello in hello Pannello di accesso, è necessario ottenere l'applicazione SAP HANA Cloud Platform identità autenticazione tooyour automaticamente firmato-on.


## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png