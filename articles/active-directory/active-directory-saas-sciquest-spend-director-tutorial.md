---
title: 'Esercitazione: Integrazione di Azure Active Directory con SciQuest Spend Director | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e SciQuest direttore di spesa.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 47c46f1297054fd96b86c1d8c66e1a55ec151497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a>Esercitazione: Integrazione di Azure Active Directory con SciQuest Spend Director
obiettivo di Hello di questa esercitazione è tooshow è come toointegrate SciQuest spesa Director con Azure Active Directory (Azure AD).  
Integrazione SciQuest spesa Director con Azure AD fornisce hello seguenti vantaggi: 

* È possibile controllare in Azure AD che ha accesso tooSciQuest spesa Director 
* È possibile abilitare l'utenti tooautomatically get connesso tooSciQuest Director spesa (Single Sign-On) con i propri account Azure AD
* È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti
integrazione di Azure AD con Director spesa SciQuest tooconfigure, è necessario hello seguenti elementi:

* Sottoscrizione di Azure AD.
* Sottoscrizione di SciQuest Spend Director abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.
> 
> 

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

* Non usare l'ambiente di produzione, a meno che non sia necessario.
* Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Descrizione dello scenario
obiettivo di Hello di questa esercitazione è tooenable si tootest AD Azure single sign-on in un ambiente di test.  
scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Director spesa SciQuest dalla raccolta hello 
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-sciquest-spend-director-from-hello-gallery"></a>Aggiunta di Director spesa SciQuest dalla raccolta hello
integrazione hello tooconfigure di SciQuest spesa Director in Azure AD, è necessario tooadd SciQuest spesa Director dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd SciQuest spesa Director dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**. 
   
    ![Active Directory][1]

2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.

3. visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
    ![Applicazioni][2]

4. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.
   
    ![Applicazioni][3]

5. In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.
   
    ![Applicazioni][4]

6. Nella casella di ricerca hello, digitare **sciQuest spesa director**.
   
    ![Applicazioni][5]

7. Nel riquadro dei risultati di hello, selezionare **SciQuest spesa Director**, quindi fare clic su **completa** tooadd un'applicazione hello.
   
    ![Applicazioni][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
obiettivo di Hello di questa sezione è tooshow come tooconfigure e prova AD Azure single sign-on con SciQuest spesa Director basato su un utente di test denominato "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow è quale utente controparte hello Director spesa SciQuest tooan utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in SciQuest spesa Director deve toobe stabilita.  
Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in SciQuest direttore di spesa.

tooconfigure e prova AD Azure single sign-on con SciQuest spesa Director, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure Active Directory singola Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Director spesa SciQuest](#creating-a-halogen-software-test-user)**  -toohave un equivalente di Britta Simon in SciQuest spesa Director toohello collegato AD Azure rappresentazione in seguito.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD
obiettivo di Hello di questa sezione è tooenable Azure AD single sign-on nel portale di Azure classico hello e tooconfigure single sign-on nell'applicazione SciQuest spesa Director.

**tooconfigure AD Azure single sign-on con SciQuest spesa Director, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico, in hello hello **SciQuest spesa Director** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On**finestra di dialogo.
   
    ![Configura accesso Single Sign-On][8]

2. In hello **come si sarebbe ad esempio utenti toosign su tooSciQuest spesa Director** selezionare **Azure Single Sign-On AD**e quindi fare clic su **Avanti**.
   
    ![Single Sign-On di Microsoft Azure AD][9]

3. In hello **Configura impostazioni App** finestra di dialogo eseguire hello alla procedura seguente: 
   
    ![Configurare le impostazioni dell'app][10]
   
     a. In hello **URL di accesso** , digitare l'URL usato dal toosign gli utenti nell'applicazione SciQuest spesa Director tooyour utilizzando hello seguente modello: *https://.* SciQuest.com/.**
   
     b. In hello **URL di risposta** casella di testo, hello tipo stesso valore è stato digitato in hello **URL di accesso** casella di testo. 
   
     c. Fare clic su **Avanti**.

4. In hello **configurare single sign-on in Director spesa SciQuest** pagina, fare clic su **Scarica metadati**e quindi salvare il file di metadati hello in locale nel computer.
   
    ![Cos'è Azure AD Connect][11]

5. Contattare SciQuest supporto tooenable questo metodo di autenticazione utilizzando i metadati scaricato hello precedente.

6. Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa** tooclose hello **configurare Single Sign-On** finestra di dialogo. 
   
    ![Cos'è Azure AD Connect][15]

7. In hello **Single sign-on conferma** pagina, fare clic su **completa**.  

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure classico chiamato Britta Simon hello toocreate.

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.
   
    ![Cos'è Azure AD Connect][100] 

2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.

3. Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.
   
    ![Cos'è Azure AD Connect][101] 

4. hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**. 
   
    ![Cos'è Azure AD Connect][102] 

5. In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente:
   
    ![Cos'è Azure AD Connect][103] 
   
    a. In **Tipo di utente** selezionare **Nuovo utente nell'organizzazione**.
   
    b. In nome utente hello **textbox**, tipo **BrittaSimon**.
   
    c. Fare clic su **Avanti**.

6. In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente: 
   
    ![Cos'è Azure AD Connect][104] 
   
    a. In hello **nome** casella tipo **Laura**.  
   
    b. In hello **cognome** txtbox, tipo, **Simon**.
   
    c. In hello **nome visualizzato** casella tipo **Britta Simon**.
   
    d. In hello **ruolo** elenco, selezionare **utente**.
   
    e. Fare clic su **Avanti**.

7. In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.
   
    ![Cos'è Azure AD Connect][105]  

8. In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:
   
    ![Cos'è Azure AD Connect][106]   
   
    a. Annotare il valore di hello di hello **nuova Password**.
   
    b. Fare clic su **Complete**.   

### <a name="creating-a-sciquest-spend-director-test-user"></a>Creazione di un utente test di SciQuest Spend Director
obiettivo Hello di questa sezione è un utente denominato Britta Simon in Director spesa SciQuest toocreate.

È necessario toocontact il team di supporto SciQuest direttore di spesa e di fornire dettagli hello su tooget di account del test che è creato.

In alternativa, è anche possibile sfruttare il provisioning JIT, una funzionalità Single Sign-On supportata da SciQuest Spend Director.  
Se il provisioning JIT è abilitato, gli utenti vengono creati automaticamente da SciQuest Spend Director durante un tentativo di accesso Single Sign-ON, se non esistono già. Questa funzionalità Elimina la necessità di hello toomanually creare single sign-on controparte utenti.

provisioning just-in-time tooget abilitato, è necessario toocontact sei il team di supporto SciQuest direttore di spesa.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD
obiettivo di Hello di questa sezione è tooenabling toouse Britta Simon single sign-on Azure concedendo proprio tooSciQuest accesso direttore di spesa.

![Cos'è Azure AD Connect][200]

**tooassign Britta Simon tooSciQuest direttore di spesa, eseguire hello alla procedura seguente:**

1. In hello Azure portale classico, visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
    ![Cos'è Azure AD Connect][201]

2. Nell'elenco di applicazioni hello, selezionare **SciQuest spesa Director**.
   
    ![Cos'è Azure AD Connect][202]

3. Scegliere dal menu hello in primo piano hello **utenti**.
   
    ![Cos'è Azure AD Connect][203]

4. Nell'elenco di utenti hello, selezionare **Britta Simon**.
   
    ![Cos'è Azure AD Connect][204]

5. Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.
   
    ![Cos'è Azure AD Connect][205]

### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On
obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.  
Quando si fa clic su riquadro SciQuest spesa Director hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour SciQuest spesa Director applicazione.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

