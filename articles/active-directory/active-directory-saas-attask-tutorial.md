---
title: 'Esercitazione: Integrazione di Azure Active Directory con @Task| Documenti Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e @Task.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a>Esercitazione: Integrazione di Azure Active Directory con @Task
obiettivo di Hello di questa esercitazione è tooshow è come toointegrate @Task con Azure Active Directory (Azure AD).  
L'integrazione @Task con Azure AD fornisce hello seguenti vantaggi: 

* È possibile controllare in Azure AD che ha accessotoo@Task
* È possibile consentire agli utenti di ottenere tooautomatically connesso too@Task (Single Sign-On) con i propri account Azure AD
* È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti
integrazione di Azure AD tooconfigure con @Task, è necessario hello seguenti elementi:

* Sottoscrizione di Azure AD.
* Sottoscrizione di @Task abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.
> 
> 

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

* Non usare l'ambiente di produzione, a meno che non sia necessario.
* Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Descrizione dello scenario
obiettivo di Hello di questa esercitazione è tooenable si tootest AD Azure single sign-on in un ambiente di test.  
scenario di Hello descritto in questa esercitazione è composto da tre componenti principali:

1. Aggiunta di @Task dalla raccolta hello 
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-task-from-hello-gallery"></a>Aggiunta di @Task dalla raccolta hello
integrazione di hello tooconfigure di @Task in Azure AD, è necessario tooadd @Task dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd @Task dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**. 
   
    ![Active Directory][1] 
2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.
3. visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
    ![Applicazioni][2] 
4. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.
   
    ![Applicazioni][3] 
5. In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.
   
    ![Applicazioni][4] 
6. Nella casella di ricerca hello, digitare  **@Task** .
   
    ![Applicazioni][5] 
7. Nel riquadro risultati hello selezionare  **@Task** , quindi fare clic su **completa** tooadd un'applicazione hello.
   
    ![Applicazioni][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
obiettivo di questa sezione Hello è tooshow è come tooconfigure e Azure AD di test singolo sign-on con @Task in base a un utente di test denominato "Laura Giussani".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in @Task tooan utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in @Task deve toobe stabilita.   
Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in @Task.

tooconfigure e test di Azure AD accesso single sign-on con @Task, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un @Tasktest utente](#creating-a-halogen-software-test-user)**  -toohave un equivalente di Britta Simon in @Taskthat è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD
obiettivo di Hello di questa sezione è tooenable AD Azure single sign-on nel portale di Azure classico hello e tooconfigure accesso single sign-on nel @Task dell'applicazione.

**tooconfigure AD Azure single sign-on con @Task, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico, in hello hello  **@Task**  pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On**  finestra di dialogo.
   
    ![Configura accesso Single Sign-On][6] 
2. In hello **come farebbe come utenti toosign per too@Task**  selezionare **Azure Single Sign-On AD**e quindi fare clic su **Avanti**.
   
    ![Single Sign-On di Microsoft Azure AD][7] 
3. In hello **Configura impostazioni App** finestra di dialogo eseguire hello alla procedura seguente:
   
    ![Configurare le impostazioni dell'app][8] 
   
     a. In hello **URL di accesso** casella di testo, digitare l'URL hello usato dall'utenti toosign-on tooyour @Task applicazione (ad esempio:*https://<Tenant name>.attask ondemand.com*).
   
     b. Fare clic su **Avanti**.
4. In hello **configurare single sign-on in @Task**  pagina, fare clic su **Scarica metadati**, salvare il file di metadati hello in locale nel computer e quindi fare clic su **Avanti**.
   
    ![Cos'è Azure AD Connect][9] 
5. Sign-on tooyour @Task sito aziendale come amministratore.
6. Andare troppo**Single Sign On Configuration**.
7. In hello **Single Sign-On** finestra di dialogo, eseguire i passaggi hello
   
    ![Configura accesso Single Sign-On][23]
   
    a. Per **Type** selezionare**SAML 2.0**.
   
    b. Selezionare **Service Provider ID**.
   
    c. Nel portale di Azure classico hello, copiare hello **URL accesso remoto**e quindi incollarlo hello **URL del portale account di accesso** casella di testo.
   
    d. Nel portale di Azure classico hello, copiare hello **URL del servizio Single Sign-Out**e quindi incollarlo hello **Sign-Out URL** casella di testo.
   
    e. Nel portale di Azure classico hello, copiare hello **Modifica URL Password**e quindi incollarlo hello **Modifica URL Password** casella di testo.
   
    f. Fare clic su **Salva**.
8. Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **Avanti**. 
   
    ![Cos'è Azure AD Connect][10]
9. In hello **Single sign-on conferma** pagina, fare clic su **completa**.  
   
    ![Cos'è Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure classico chiamato Britta Simon hello toocreate.  

![Creare un utente di Azure AD][20]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.
3. Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**. 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente: 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    a. In Tipo di utente selezionare Nuovo utente nell'organizzazione.
   
    b. In nome utente hello **textbox**, tipo **BrittaSimon**.
   
    c. Fare clic su **Avanti**.
6. In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente: 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    a. In hello **nome** casella tipo **Laura**.  
   
    b. In hello **cognome** casella di testo, tipo, **Simon**.
   
    c. In hello **nome visualizzato** casella tipo **Britta Simon**.
   
    d. In hello **ruolo** elenco, selezionare **utente**.

    e. Fare clic su **Avanti**.

7. In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    a. Annotare il valore di hello di hello **nuova Password**.
   
    b. Fare clic su **Completa**.   

### <a name="creating-an-task-test-user"></a>Creazione di un utente di test di @Task
obiettivo Hello di questa sezione è un utente denominato Britta Simon in toocreate @Task.

**un utente denominato Britta Simon in toocreate @Task, eseguire hello alla procedura seguente:**

1. Accesso tooyour @Task sito aziendale come amministratore.
2. Scegliere dal menu hello in primo piano hello **persone**.
3. Fare clic su **New Person**. 
4. Nella finestra di dialogo nuova persona hello eseguire hello alla procedura seguente:
   
    ![Creare un utente di test di @Task][21] 
   
    a. In hello **nome** casella di testo, digitare "Sandro".
   
    b. In hello **cognome** casella di testo, digitare "Simon".
   
    c. In hello **indirizzo di posta elettronica** casella di testo, digitare l'indirizzo di posta elettronica Britta Simon in Azure Active Directory.
   
    d. Fare clic su **Add Person**.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD
obiettivo di Hello di questa sezione è tooenabling toouse Britta Simon single sign-on Azure tramite la concessione di accesso too@Task.

![Assegna utente][200] 

**tooassign Britta Simon too@Task, eseguire hello alla procedura seguente:**

1. In hello Azure portale classico, visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
    ![Assegna utente][201] 
2. Nell'elenco di applicazioni hello, selezionare  **@Task** .
   
    ![Assegna utente][202] 
3. Scegliere dal menu hello in primo piano hello **utenti**.
   
    ![Assegna utente][203] 
4. Nell'elenco di utenti hello, selezionare **Britta Simon**.
5. Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.
   
    ![Assegna utente][205]

### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On
obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.  
Quando si fa clic su hello @Task hello di riquadro nel Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour @Task dell'applicazione.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






