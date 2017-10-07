---
title: 'Esercitazione: Integrazione di Azure Active Directory con RFPIO | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e RFPIO.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: e0c692276276edd8f859e73d81cf54d75a65957a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a>Esercitazione: Integrazione di Azure Active Directory con RFPIO

In questa esercitazione, è illustrato come toointegrate RFPIO con Azure Active Directory (Azure AD).

Integrazione RFPIO con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare che in Azure AD che ha accesso tooRFPIO.
- È possibile abilitare l'utenti tooautomatically get connesso tooRFPIO (Single Sign-On) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con RFPIO tooconfigure, è necessario hello seguenti elementi:

- Una sottoscrizione di Azure AD.
- Sottoscrizione RFPIO abilitata per l'accesso Single Sign-On.

> [!NOTE]
> Non è consigliabile utilizzare una procedura di produzione ambiente tootest hello in questa esercitazione.

passaggi di hello tootest in questa esercitazione, seguire queste indicazioni:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritta in questa esercitazione è composto da due componenti principali:

1. Aggiunta di RFPIO dalla raccolta hello.
2. Configurazione e test dell'accesso Single Sign-On di Azure AD.

## <a name="add-rfpio-from-hello-gallery"></a>Aggiungere RFPIO dalla raccolta di hello
integrazione hello tooconfigure di RFPIO in Azure AD, è necessario tooadd RFPIO dall'elenco di tooyour hello raccolta di App SaaS gestite.

### <a name="tooadd-rfpio-from-hello-gallery"></a>tooadd RFPIO dalla raccolta hello

1. In hello  **[portale di Azure](https://portal.azure.com)**, nel riquadro di spostamento a sinistra di hello, selezionare hello **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Selezionare **Applicazioni aziendali** e quindi selezionare **Tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd una nuova applicazione, seleziona hello **nuova applicazione** pulsante nella parte superiore di hello nella finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **RFPIO**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. Nel riquadro dei risultati hello, selezionare **RFPIO**, quindi selezionare hello **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con RFPIO in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow relazioni hello sono compreso tra l'utente corrispondente in RFPIO e un utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in RFPIO deve toobe stabilita.

In RFPIO, assegnare il valore di hello del **nome utente** in Azure AD come valore hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con RFPIO, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurare Azure Active Directory Single Sign-On](#configuring-azure-ad-single-sign-on)**- tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#creating-an-azure-ad-test-user)**-tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un utente test RFPIO](#creating-a-rfpio-test-user)**  - toohave un equivalente di Britta Simon in RFPIO che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnare l'utente test hello Azure AD](#assigning-the-azure-ad-test-user)**- tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare Single Sign-On](#testing-single-sign-on)**  - tooverify se configurazione hello funziona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione RFPIO.

**Azure AD tooconfigure single sign-on con RFPIO, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **RFPIO** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. In hello **RFPIO dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    a. In hello **identificatore** casella di testo, digitare l'URL hello:`https://www.rfpio.com`

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    b. Selezionare **Mostra impostazioni URL avanzate**

    c. In hello **stato inoltro** casella di testo immettere un valore stringa. Contatto [team di supporto RFPIO](https://www.rfpio.com/contact/) tooget questo valore. 

4. Selezionare **Mostra impostazioni URL avanzate** Se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:   

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    In hello **URL di accesso** casella di testo, digitare l'URL hello:`https://www.app.rfpio.com`

5. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. In una finestra del web browser, account di accesso toohello **RFPIO** sito Web come amministratore.

8. Fare clic sull'elenco a discesa di hello in basso a sinistra.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. Fare clic su hello **impostazioni organizzazione**. 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. Fare clic su hello **funzionalità & integrazione**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. In hello **SAML SSO Configuration** fare clic su **modifica**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. In questa sezione eseguire le seguenti operazioni:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    a. Copiare il contenuto di hello di hello **XML di metadati scaricato** e incollarlo in hello **la configurazione dell'identità** campo.

    > [!NOTE]
    >scaricato hello toocopy contenuto di **Metadata XML** utilizzare **blocco note + +** o corretto **Editor XML**. 

    b. Fare clic su **Convalida**.

    c. Dopo la selezione **convalida**, capovolgimento **SAML(Enabled)** tooon.

    d. Fare clic su **Submit**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="create-a-rfpio-test-user"></a>Creare un utente di test di RFPIO

toolog agli utenti di Azure AD tooenable in tooRFPIO, è necessario eseguirne il provisioning in RFPIO.  
Nel caso di hello di RFPIO, il provisioning è un'attività manuale.

**tooprovision un account utente, eseguire hello alla procedura seguente:**

1. Accedi tooyour sito della società RFPIO come amministratore.

2. Fare clic sull'elenco a discesa di hello in basso a sinistra.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. Fare clic su hello **impostazioni organizzazione**. 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. Fare clic su **MEMBRI DEL TEAM**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. Fare clic su **AGGIUNGI MEMBRI**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. In hello **aggiungere nuovi membri** sezione. eseguire le seguenti operazioni:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app8.png)

    a. Invio **indirizzo di posta elettronica** in hello **immettere un messaggio di posta elettronica per ogni riga** campo.

    b. Selezionare il **ruolo** in base alle esigenze.

    c. Fare clic su **AGGIUNGI MEMBRI**.
        
    > [!NOTE]
    > titolare dell'account di Azure Active Directory Hello riceve un messaggio di posta elettronica e segue il proprio account tooconfirm un collegamento prima che diventi attivo.

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooRFPIO.

![Assegna utente][200] 

**tooassign Britta Simon tooRFPIO, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **RFPIO**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione Configurazione di Azure AD single sign-on utilizzare test hello Pannello di accesso.

Quando si fa clic hello RFPIO riquadro in hello Pannello di accesso, è necessario ottenere applicazione RFPIO tooyour automaticamente firmato-on.
Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla toointegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

