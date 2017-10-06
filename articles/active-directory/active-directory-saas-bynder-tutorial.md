---
title: 'Esercitazione: Integrazione di Azure Active Directory con Bynder | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Bynder.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a>Esercitazione: Integrazione di Azure Active Directory con Bynder
obiettivo di Hello di questa esercitazione è tooshow è come toointegrate Bynder con Azure Active Directory (Azure AD).

Integrazione Bynder con Azure AD fornisce hello seguenti vantaggi:

* È possibile controllare in Azure AD che ha accesso tooBynder
* È possibile abilitare l'utenti tooautomatically get connesso tooBynder single sign-on (SSO) con i propri account Azure AD
* È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti
integrazione di Azure AD con Bynder tooconfigure, è necessario hello seguenti elementi:

* Sottoscrizione di Azure AD.
* Sottoscrizione di Bynder abilitata per l'accesso Single Sign-On (SSO)

>[!NOTE]
>hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione. 
> 

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

* Non usare l'ambiente di produzione, a meno che non sia necessario.
* Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
obiettivo di Hello di questa esercitazione è tooenable si tootest SSO di Microsoft Azure Active Directory in un ambiente di test.

scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Bynder dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Microsoft Azure AD

## <a name="add-bynder-from-hello-gallery"></a>Aggiungere Bynder dalla raccolta di hello
integrazione hello tooconfigure di Bynder in Azure AD, è necessario tooadd Bynder dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Bynder dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**. 
   
    ![Active Directory][1]
2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.
3. visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
    ![Applicazioni][2]
4. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.
   
    ![Applicazioni][3]
5. In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.
   
    ![Applicazioni][4]
6. Nella casella di ricerca hello, digitare **Bynder**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. Nel riquadro dei risultati hello, selezionare **Bynder**, quindi fare clic su **completa** tooadd un'applicazione hello.
   
    ![Selezionare l'applicazione hello nella raccolta hello](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a>Configurare e testare l'accesso Single Sign-On di Microsoft Azure AD
obiettivo di Hello di questa sezione è tooshow come tooconfigure e test di Microsoft Azure AD SSO con Bynder basato su un utente di test denominato "Britta Simon".

Per toowork SSO, Azure AD deve tooknow è quale utente controparte hello Bynder tooan utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Bynder deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Bynder.

tooconfigure e test di Microsoft Azure AD SSO con Bynder, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest Microsoft Azure AD Single Sign-On con Britta Simon.
3. **[Creazione di un utente test Bynder](#creating-a-bynder-test-user)**  -toohave un equivalente di Britta Simon in Bynder toohello collegato AD Azure rappresentazione in seguito.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable toouse Britta Simon Microsoft Azure AD Single Sign-On.
5. **[Test di accesso single sign-on](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-microsoft-azure-ad-sso"></a>Configurazione dell'accesso Single Sign-On (SSO) di Microsoft Azure AD
In questa sezione abilitare SSO di Microsoft Azure Active Directory nel portale classico hello e configurare SSO nell'applicazione Bynder.

**tooconfigure SSO di Microsoft Azure AD con Bynder, eseguire hello alla procedura seguente:**

1. Nel portale classico hello in hello **Bynder** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo.
   
    ![Configura accesso Single Sign-On][6] 
2. In hello **come si sarebbe ad esempio utenti toosign su tooBynder** selezionare **Microsoft Azure AD Single Sign-On**e quindi fare clic su **Avanti**.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. In hello **Configura impostazioni App** nella pagina, se si desidera un'applicazione hello tooconfigure in **modalità avviata da IDP**, eseguire hello alla procedura seguente e fare clic su **Avanti**:
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.getbynder.com/sso/SAML/authenticate/`
  2. Fare clic su **Avanti**.
4. Se si desidera in un'applicazione hello tooconfigure **modalità iniziata da SP** su hello **Configura impostazioni App** nella pagina, quindi fare clic su hello **"(facoltative) Impostazioni avanzate Show"**e quindi immettere hello **URL di accesso** e fare clic su **Avanti**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. In hello **URL di accesso** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.getbynder.com/login/`
  2. Fare clic su **Avanti**.
  
   >[!NOTE]
   >valore Hello hello URL di accesso in questa esercitazione è semplicemente un placeholfer. valore effettivo di hello tooget per l'ambiente, contattare Bynder.
   >

5. In hello **configurare single sign-on a Bynder** pagina, eseguire hello alla procedura seguente e fare clic su **Avanti**:
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. Fare clic su **Scarica metadati**e quindi salvare il file hello nel computer in uso.
  2. Fare clic su **Avanti**.
6. tooget SSO configurato per l'applicazione, contattare il team di supporto Bynder. Collegare il file di metadati scaricato hello e condividerlo con Bynder team tooset di SSO sul relativo lato.
7. Nel portale classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **Avanti**.
   
    ![Single Sign-On di Microsoft Azure AD][10]
8. In hello **Single sign-on conferma** pagina, fare clic su **completa**.  
   
    ![Single Sign-On di Microsoft Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
obiettivo di Hello di questa sezione è toocreate un utente di test nel portale classico di hello chiamato Britta Simon.

![Creare un utente di Azure AD][20]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.
3. Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente:
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. In Tipo di utente selezionare Nuovo utente nell'organizzazione.
  2. In nome utente hello **textbox**, tipo **BrittaSimon**.
  3. Fare clic su **Avanti**.
6. In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente:
   
   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. In hello **nome** casella tipo **Laura**.  
  2. In hello **cognome** casella di testo, tipo, **Simon**. 
  3. In hello **nome visualizzato** casella tipo **Britta Simon**.
  4. In hello **ruolo** elenco, selezionare **utente**.
  5. Fare clic su **Avanti**.
7. In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. Annotare il valore di hello di hello **nuova Password**.
   2. Fare clic su **Complete**.   

### <a name="create-a-bynder-test-user"></a>Creare un utente test per Bynder
obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Bynder toocreate. Bynder supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.

Non è necessario alcun intervento dell'utente in questa sezione. Verrà creato un nuovo utente durante una tooaccess tentativo Bynder se non esiste ancora.

>[!NOTE]
>Se è necessario un utente toocreate manualmente, è necessario team di supporto Bynder toocontact hello. 
> 

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD
obiettivo di Hello di questa sezione è tooenabling Britta Simon toouse SSO Azure concedendo tooBynder proprio accesso.

   ![Assegna utente][200]

**tooassign Britta Simon tooBynder, eseguire hello alla procedura seguente:**

1. Nel portale classico hello, fare clic su visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello **applicazioni** nel menu superiore hello.
   
    ![Assegna utente][201]
2. Nell'elenco di applicazioni hello, selezionare **Bynder**.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. Scegliere dal menu hello in primo piano hello **utenti**.
   
    ![Assegna utente][203]
4. Nell'elenco di utenti hello, selezionare **Britta Simon**.
5. Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.
   
    ![Assegna utente][205]

### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On
obiettivo di Hello di questa sezione è tootest la configurazione di SSO di Microsoft Azure AD mediante hello Pannello di accesso.

Quando si fa clic su riquadro Bynder hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Bynder applicazione.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
