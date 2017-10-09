---
title: 'Esercitazione: Integrazione di Azure Active Directory con Wdesk | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Wdesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 2c278a5e4f50cc362663efc0f826ff0c0fcf6e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a>Esercitazione: Integrazione di Azure Active Directory con Wdesk

In questa esercitazione, è illustrato come toointegrate Wdesk con Azure Active Directory (Azure AD).

Integrazione Wdesk con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooWdesk
- È possibile abilitare l'utenti tooautomatically get connesso tooWdesk (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere. [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Wdesk tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Wdesk abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Wdesk dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-wdesk-from-hello-gallery"></a>Aggiunta di Wdesk dalla raccolta hello
integrazione hello tooconfigure di Wdesk in Azure AD, è necessario tooadd Wdesk dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Wdesk dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Wdesk**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. Nel riquadro dei risultati hello, selezionare **Wdesk**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Wdesk con un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Wdesk è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Wdesk deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Wdesk.

tooconfigure e prova AD Azure single sign-on con Wdesk, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Wdesk](#creating-a-wdesk-test-user)**  -toohave un equivalente di Britta Simon in Wdesk che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Wdesk.

**Azure AD tooconfigure single sign-on con Wdesk, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Wdesk** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. In hello **Wdesk dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **IDP** modalità avviato da eseguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    a. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`

    b. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`

4. Selezionare **Mostra impostazioni URL avanzate** Se si desidera un'applicazione hello tooconfigure in **SP** , modalità iniziata da eseguire hello seguente passaggio:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`
     
    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On. Ottenere questi valori dal portale WDesk quando si configura SSO hello. 
  
5. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. In una finestra del web browser, account di accesso tooWdesk come un amministratore della sicurezza.

8. In hello in basso a sinistra, fare clic su **Admin** e scegliere **amministratore dell'Account**:
 
     ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. In Wdesk Admin, passare troppo**sicurezza**, quindi **SAML** > **impostazioni SAML**:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. In **impostazioni generali**, controllare hello **Abilita SAML Single Sign On**:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. In **i dettagli del Provider servizio**, eseguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      a. Hello copia **URL di accesso** e incollarlo in **Sign-on Url** casella di testo nel portale di Azure.
   
      b. Hello copia **Url dei metadati** e incollarlo in **identificatore** casella di testo nel portale di Azure.
       
      c. Hello copia **url Consumer** e incollarlo in **Url di risposta** casella di testo nel portale di Azure.
   
      d. Fare clic su **salvare** alle modifiche apportate hello toosave portale Azure.      

12. Fare clic su **Configura impostazioni IdP** tooopen **Modifica impostazioni IdP** finestra di dialogo. Fare clic su **Scegli File** toolocate hello **Metadata.xml** file salvato dal portale di Azure, quindi caricare il file.
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. Fare clic su **Salva modifiche**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-wdesk-test-user"></a>Creazione di un utente test di Wdesk

toolog agli utenti di Azure AD tooenable in tooWdesk, è necessario eseguirne il provisioning in Wdesk. Nel caso di Wdesk il provisioning è un'attività manuale.

**tooprovision un account utente, eseguire hello alla procedura seguente:**

1. Accedi tooWdesk come un amministratore della sicurezza.
2. Passare troppo**Admin** > **amministratore dell'Account**.

     ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. Fare clic su **Members** (Membri) in **People** (Persone).

4. Fare clic su **Add Member** tooopen **Add Member** la finestra di dialogo. 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. In **utente** testo casella, immettere un nome utente dell'utente come hello  **brittasimon@contoso.com**  e fare clic su **continua** pulsante.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  Immettere i dettagli di hello, come illustrato di seguito:
  
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    a. In **posta elettronica** testo messaggio di posta elettronica hello dell'utente come immettere  **brittasimon@contoso.com** .

    b. In **nome** testo hello nome dell'utente come immettere **Laura**.

    c. In **cognome** testo immettere il cognome di hello dell'utente come **Simon**.

7. Fare clic sul pulsante **Save Member** (Salva membro).  

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooWdesk.

![Assegna utente][200] 

**tooassign Britta Simon tooWdesk, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Wdesk**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Wdesk hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Wdesk applicazione.
Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

