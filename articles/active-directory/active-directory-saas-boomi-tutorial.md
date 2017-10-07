---
title: 'Esercitazione: Integrazione di Azure Active Directory con Boomi | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Boomi.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ce64a4561697d311a8c7b1b244315bb552c5cfb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a>Esercitazione: Integrazione di Azure Active Directory con Boomi

In questa esercitazione, è illustrato come toointegrate Boomi con Azure Active Directory (Azure AD).

Integrazione di Boomi con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooBoomi
- È possibile abilitare l'utenti tooautomatically get connesso tooBoomi (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Boomi tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Boomi abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Boomi dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-boomi-from-hello-gallery"></a>Aggiunta di Boomi dalla raccolta hello
integrazione hello tooconfigure di Boomi in Azure AD, è necessario tooadd Boomi dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Boomi dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Boomi**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. Nel riquadro dei risultati hello, selezionare **Boomi**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Boomi in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Boomi è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Boomi deve toobe stabilita.

In Boomi, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con Boomi, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Boomi](#creating-a-boomi-test-user)**  -toohave un equivalente di Britta Simon in Boomi che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Boomi.

**Azure AD tooconfigure single sign-on con Boomi, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Boomi** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. In hello **Boomi dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    a. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://platform.boomi.com/sso/<accountname>/saml`

    b. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://platform.boomi.com/sso/<accountname>/saml`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con URL di risposta e identificatore effettivo hello. Contatto [team di supporto di Boomi](https://boomi.com/company/contact/) tooget questi valori.

4. In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. Applicazione di Boomi prevede asserzioni SAML hello in un formato specifico. Configurare hello seguendo le attestazioni per questa applicazione. È possibile gestire i valori hello di questi attributi da hello "**gli attributi utente**" sezione nella pagina di integrazione dell'applicazione. Hello seguente schermata mostra un esempio per questo oggetto.
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, per ogni riga nella tabella hello, eseguire hello alla procedura seguente:

    | Nome attributo | Valore attributo |
    | -------------- | --------------- |
    | FEDERATION_ID | user.mail |
    
    a. Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    b. In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.
    
    c. Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.
    
    d. Fare clic su **OK**.

6. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. In hello **Boomi configurazione** fare clic su **configurare Boomi** tooopen **Configura sign-on** finestra. Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. In un'altra finestra del Web browser accedere al sito aziendale di Boomi come amministratore. 

9. Passare troppo**nome società** e andare troppo**impostare**.

10. Fare clic su hello **opzioni SSO** scheda ed eseguire i passaggi successivi.

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    a. Selezionare la casella di controllo **Abilita Single Sign-On SAML**.

    b. Fare clic su **importazione** hello tooupload scaricato certificato da Azure AD troppo**Identity Provider Certificate**.
    
    c. In hello **Identity Provider Login URL** casella di testo, inserire il valore di hello di **SAML Single Sign-On Service URL** dalla finestra di configurazione dell'applicazione Azure AD.

    d. Come **Federation Id Location** selezionare il pulsante di opzione **Federation Id is in FEDERATION_ID Attribute element**. 

    e. Fare clic sul pulsante **Salva** .

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-boomi-test-user"></a>Creazione di un utente test di Boomi

In ordine tooenable Azure AD utenti toolog in tooBoomi, è necessario eseguirne il provisioning in Boomi. Nel caso di hello di Boomi, il provisioning è un'attività manuale.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision un account utente, eseguire hello alla procedura seguente:

1. Accedi tooyour sito della società Boomi come amministratore.

2. Dopo aver effettuato l'accesso, cercare troppo**Gestione utenti** e andare troppo**utenti**.

    ![Utenti](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Utenti")

3. Fare clic su  **+**  icona e hello **ruoli utente di aggiungere/Gestisci** verrà visualizzata la finestra di dialogo.

    ![Utenti](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Utenti")

    ![Utenti](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Utenti")

    a. In hello **indirizzo di posta elettronica utente** casella Tipo hello email dell'utente come BrittaSimon@contoso.com.
    
    b. In hello **nome** casella Tipo hello nome dell'utente come Laura.

    c. In hello **cognome** casella di testo, digitare hello cognome dell'utente come Simon.
    
    d. Immettere dell'utente hello **ID federazione**. Ogni utente deve avere un ID di federazione che identifica in modo univoco l'utente hello nell'account hello.
    
    e. Assegnare hello **utente Standard** utente toohello ruolo. Non assegnare il ruolo di amministratore hello perché in tal quest'ultimo accesso atmosfera normale, nonché l'accesso single sign-on.
    
    f. Fare clic su **OK**.
    
    > [!NOTE]
    > utente Hello non riceverà un messaggio di notifica iniziale contenente la password che può essere utilizzati toolog in toohello AtomSphere account perché la password viene gestita mediante il provider di identità hello. È possibile utilizzare qualsiasi altro Boomi utente account strumento di creazione o le API fornite da Boomi tooprovision account utente di AAD. 

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooBoomi.

![Assegna utente][200] 

**tooassign Britta Simon tooBoomi, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Boomi**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Boomi hello in hello Pannello di accesso, è necessario ottenere applicazione Boomi tooyour automaticamente firmato-on.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

