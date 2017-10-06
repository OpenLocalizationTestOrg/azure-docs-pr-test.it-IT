---
title: 'Esercitazione: Integrazione di Azure Active Directory con Workpath | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Workpath.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 320b0daf-14be-4813-b59b-25a6a5070690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 69f443f314edb7c8c489a6c193e09b6f8fe6795a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workpath"></a>Esercitazione: Integrazione di Azure Active Directory con Workpath

In questa esercitazione, è illustrato come toointegrate Workpath con Azure Active Directory (Azure AD).

Integrazione Workpath con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooWorkpath
- È possibile abilitare l'utenti tooautomatically get connesso tooWorkpath (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Workpath tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Workpath abilitata per l'accesso Single Sign-On.

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Workpath dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-workpath-from-hello-gallery"></a>Aggiunta di Workpath dalla raccolta hello
integrazione hello tooconfigure di Workpath in Azure AD, è necessario tooadd Workpath dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Workpath dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Workpath**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_search.png)

5. Nel riquadro dei risultati hello, selezionare **Workpath**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Workpath con un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Workpath è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Workpath deve toobe stabilita.

In Workpath, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con Workpath, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Workpath](#creating-a-workpath-test-user)**  -toohave un equivalente di Britta Simon in Workpath che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Workpath.

**Azure AD tooconfigure single sign-on con Workpath, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Workpath** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_samlbase.png)

3. In hello **Workpath dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **IDP** modalità avviato da eseguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url.png)

    a. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://api.workpath.com/v1/saml/metadata/<instancename>`

    b. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://api.workpath.com/v1/saml/assert/<instancename>`

4. Selezionare **Mostra impostazioni URL avanzate** Se si desidera in un'applicazione hello tooconfigure **SP** , modalità iniziata da eseguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url1.png)

    In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.workpath.com/ `

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con URL hello effettivo Sign-on, l'identificatore e l'URL di risposta. Contatto [team di supporto Workpath](https://help.workpath.com) tooget questi valori.

5. Applicazione di Workpath prevede asserzioni SAML hello in un formato specifico. Configurare hello seguendo le attestazioni per questa applicazione. È possibile gestire i valori hello di questi attributi da hello "**gli attributi utente**" sezione nella pagina di integrazione dell'applicazione. Hello seguente schermata illustra un esempio di questa configurazione. 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_attributes.png)
    
6. In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nella figura hello ed eseguire hello alla procedura seguente:
    
    | Nome attributo | Valore attributo |
    | ------------------- | -------------------- |    
    | first_name | user.givenname |
    | last_name | user.surname |
    
    a. Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_04.png)

    b. In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_05.png)

    c. Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.

    d. Lasciare hello **Namespace** casella di testo vuoto.
    
    e. Fare clic su **OK**.
    

7. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_certificate.png) 

8. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workpath-tutorial/tutorial_general_400.png)

9. In hello **Workpath configurazione** fare clic su **configurare Workpath** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_configure.png) 

10. tooconfigure single sign-on sul **Workpath** lato, è necessario hello toosend scaricato **Metadata XML**, **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** troppo[team di supporto Workpath](https://help.workpath.com). 

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-workpath-test-user"></a>Creazione di un utente di test di Workpath

Workpath supporta il provisioning utenti JIT. Dopo l'autenticazione degli utenti vengono creati automaticamente in un'applicazione hello. 


### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooWorkpath.

![Assegna utente][200] 

**tooassign Britta Simon tooWorkpath, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Workpath**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Workpath hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Workpath applicazione.
Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_203.png

