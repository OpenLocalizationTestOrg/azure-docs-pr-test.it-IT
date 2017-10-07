---
title: 'Esercitazione: Integrazione di Azure Active Directory con SuccessFactors | Microsoft Docs'
description: Informazioni su come toouse SuccessFactors con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a>Esercitazione: Integrazione di Azure Active Directory con SuccessFactors
obiettivo di Hello di questa esercitazione è tooshow è come toointegrate SuccessFactors con Azure Active Directory (Azure AD).

Integrazione di SuccessFactors con Azure AD fornisce hello seguenti vantaggi:

* È possibile controllare in Azure AD che ha accesso tooSuccessFactors
* È possibile abilitare l'utenti tooautomatically get connesso tooSuccessFactors (Single Sign-On) con i propri account Azure AD
* È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti
integrazione di Azure AD con SuccessFactors tooconfigure, è necessario hello seguenti elementi:

* Sottoscrizione di Azure valida
* Un tenant in SuccessFactors

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.
> 
> 

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

* Non usare l'ambiente di produzione, a meno che non sia necessario.
* Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
obiettivo di Hello di questa esercitazione è tooenable si tootest AD Azure single sign-on in un ambiente di test.

scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di SuccessFactors dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-successfactors-from-hello-gallery"></a>Aggiunta di SuccessFactors dalla raccolta hello
integrazione hello tooconfigure di SuccessFactors in Azure AD, è necessario tooadd SuccessFactors dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd SuccessFactors dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico, nel riquadro di navigazione sinistro hello hello fare clic su **Active Directory**.
   
    ![Configurazione dell'accesso Single Sign-On][1]
2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.
3. visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
    ![Configurazione dell'accesso Single Sign-On][2]
4. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.
   
    ![Applicazioni][3]
5. In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.
   
    ![Configurazione dell'accesso Single Sign-On][4]
6. In hello **casella di ricerca**, tipo **SuccessFactors**.
   
    ![Configurazione dell'accesso Single Sign-On][5]
7. Nel riquadro dei risultati hello, selezionare **SuccessFactors**, quindi fare clic su **completa** tooadd un'applicazione hello.
   
    ![Configurazione dell'accesso Single Sign-On][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
obiettivo di Hello di questa sezione è tooshow come tooconfigure e prova AD Azure single sign-on con SuccessFactors basato su un utente di test denominato "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow è quale utente controparte hello in SuccessFactors tooan utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in SuccessFactors deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in SuccessFactors.

tooconfigure e prova AD Azure single sign-on con SuccessFactors, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test SuccessFactors](#creating-a-successfactors-test-user)**  -toohave un equivalente di Britta Simon in SuccessFactors toohello collegato AD Azure rappresentazione in seguito.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD
In questa sezione, si abilita Azure AD single sign-on nel portale classico hello e configurare l'accesso single sign-on nell'applicazione SuccessFactors.

**Azure AD tooconfigure single sign-on con SuccessFactors, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico, in hello hello **SuccessFactors** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo.
   
    ![Configurazione dell'accesso Single Sign-On][7]
2. In hello **come si sarebbe ad esempio utenti toosign su tooSuccessFactors** selezionare **Microsoft Azure AD Single Sign-On**e quindi fare clic su **Avanti**.
   
    ![Configurazione dell'accesso Single Sign-On][8]
3. In hello **Configura URL App** pagina, eseguire hello alla procedura seguente e quindi fare clic su **Avanti**.
   
    ![Configurazione dell'accesso Single Sign-On][9]
   
    a. In hello **URL di accesso** casella di testo, digitare un URL utilizzando uno dei hello seguenti motivi: 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    b. In hello **URL di risposta** casella di testo, digitare un URL utilizzando uno dei hello seguenti motivi: 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    c. Fare clic su **Avanti**. 

    > [!NOTE]
    > Si noti che queste non sono valori reali hello. È necessario tooupdate questi valori con hello URL di URL di accesso e di risposta effettivo. Questi valori, contattare il tooget [team di supporto di SuccessFactors](https://www.successfactors.com/en_us/support.html).

1. In hello **Configura accesso single sign-on in SuccessFactors** pagina, fare clic su **Scarica certificato**e quindi salvare il file di certificato hello in locale nel computer.
   
    ![Configurazione dell'accesso Single Sign-On][10]

2. In un'altra finestra del Web browser accedere al **portale di amministrazione di SuccessFactors** come amministratore.

3. Visitare **sicurezza delle applicazioni** e native troppo**funzione accesso singolo**. 

4. Inserire un valore in hello **Reimposta Token** e fare clic su **salvare Token** tooenable SAML SSO.
   
    ![Configurazione dell'accesso Single Sign-On sul lato app][11]

    > [!NOTE] 
    > Questo valore viene utilizzato solo come hello opzione on/off. Se qualsiasi valore viene salvato, hello SAML SSO è impostata su ON. Se un valore vuoto viene salvato hello SAML SSO è impostata su OFF.

1. Schermata di toobelow native ed eseguire hello seguenti azioni.
   
    ![Configurazione dell'accesso Single Sign-On sul lato app][12]
   
    a. Seleziona hello **SAML SSO v2** pulsante di opzione
   
    b. Impostare hello SAML asserzione entità Name(e.g. SAml issuer + company name).
   
    c. In hello **autorità di certificazione SAML** casella di testo inserire il valore di hello di **URL autorità di certificazione** dalla configurazione guidata di Azure AD applicazione.
   
    d. Selezionare **Response(Customer Generated/IdP/AP)** (Risposta - Generata da cliente/IdP/AP) per **Require Mandatory Signature** (Richiedi firma obbligatoria).
   
    e. Selezionare **Abilitato** per **Enable SAML Flag** (Abilita flag SAML).
   
    f. Selezionare **No** per **Login Request Signature(SF Generated/SP/RP)** (Firma richiesta di accesso - Generata da SF/SP/RP).
   
    g. Selezionare **Browser/Post Profile** (Profilo browser/post) per **SAML Profile** (Profilo SAML).
   
    h. Selezionare **No** per **Enforce Certificate Valid Period** (Applicare periodo di validità certificato).
   
    i. Copiare il contenuto di hello hello scaricato del file di certificato e quindi incollarlo hello **certificato di verifica SAML** casella di testo.

    > [!NOTE] 
    > contenuto del certificato Hello devono avere certificato e fine certificato i tag di inizio.

1. Passare tooSAML V2 e quindi eseguire hello alla procedura seguente:
   
    ![Configurazione dell'accesso Single Sign-On sul lato app][13]
   
    a. Selezionare **Sì** per **Support SP-initiated Global Logout** (Supporto disconnessione globale avviata da SP).
   
    b. In hello **globale Logout URL del servizio (destinazione LogoutRequest)** casella di testo inserire il valore di hello di **URL disconnessione remota** dalla configurazione guidata di Azure AD applicazione.
   
    c. Selezionare **No** per **Require sp must encrypt all NameID element** (Richiesta a sp di crittografare tutti gli elementi NameID).
   
    d. Selezionare **non specificato** per **NameID Format** (Formato NameID).
   
    e. Selezionare **Sì** per **Enable sp initiated login (AuthnRequest)** (Abilita accesso avviato da sp - AuthnRequest).
   
    f. In hello **richiesta di invio da autorità di certificazione aziendale** casella di testo inserire il valore di hello di **URL accesso remoto** dalla configurazione guidata di Azure AD applicazione.
2. Eseguire questi passaggi se si desidera che i nomi utente di accesso hello toomake maiuscole e minuscole.
   
    a. Visitare **impostazioni società**(vicino alla parte inferiore di hello).
   
    b. Selezionare la casella di controllo accanto alla **Enable Non-Case-Sensitive Username**(Abilita nome utente senza distinzione maiuscole/minuscole).
   
    c.Fare clic su **Save**(Salva).
   
    ![Configura accesso Single Sign-On][29]

    > [!NOTE] 
    > Se si esegue questa tooenable, sistema di hello controlla se verrà creato automaticamente un nome di account di accesso SAML duplicato. Se, ad esempio hello cliente dispone di nomi utente User1 e user1. L'annullamento della distinzione maiuscole/minuscole crea questi duplicati. sistema di Hello verrà visualizzato un messaggio di errore e non viene abilitata la funzionalità di hello. Hello il cliente dovrà toochange uno dei nomi utente hello in modo sia stato digitato in realtà diversi. 

1. Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa** tooclose hello **configurare Single Sign-On** finestra di dialogo.
   
    ![Applicazioni][14]
2. In hello **Single sign-on conferma** pagina, fare clic su **completa**.
   
    ![Applicazioni][15]

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è toocreate un utente di test nel portale classico di hello chiamato Britta Simon.

![Creare un utente di Azure AD][16]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.
   
    ![Creazione di un utente test di Azure AD][17]
2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.
3. Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.
   
    ![Creazione di un utente test di Azure AD][18]
4. hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**.
   
    ![Creazione di un utente test di Azure AD][19]
5. In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente:
   
    ![Creazione di un utente test di Azure AD][20]
   
    a. In Tipo di utente selezionare Nuovo utente nell'organizzazione.
   
    b. In nome utente hello **textbox**, tipo **BrittaSimon**.
   
    c. Fare clic su **Avanti**.
6. In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente:
   
    ![Creazione di un utente test di Azure AD][21]
   
    a. In hello **nome** casella tipo **Laura**.  
   
    b. In hello **cognome** casella di testo, tipo, **Simon**.
   
    c. In hello **nome visualizzato** casella tipo **Britta Simon**.
   
    d. In hello **ruolo** elenco, selezionare **utente**.
   
    e. Fare clic su **Avanti**.
7. In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.
   
    ![Creazione di un utente test di Azure AD][22]
8. In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:
   
    ![Creazione di un utente test di Azure AD][23]
   
    a. Annotare il valore di hello di hello **nuova Password**.
   
    b. Fare clic su **Completa**.  

### <a name="creating-a-successfactors-test-user"></a>Creazione di un utente test SuccessFactors
In ordine tooenable Azure AD utenti toolog in SuccessFactors, è necessario eseguirne il provisioning in SuccessFactors.  
Nel caso di hello di SuccessFactors, il provisioning è un'attività manuale.

tooget degli utenti creati in SuccessFactors, è necessario hello toocontact [team di supporto di SuccessFactors](https://www.successfactors.com/en_us/support.html).

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD
obiettivo di Hello di questa sezione è tooenabling toouse Britta Simon single sign-on Azure concedendo tooSuccessFactors proprio accesso.

![Assegna utente][24]

**tooassign Britta Simon tooSuccessFactors, eseguire hello alla procedura seguente:**

1. Nel portale classico hello, fare clic su visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello **applicazioni** nel menu superiore hello.
   
    ![Assegna utente][25]
2. Nell'elenco di applicazioni hello, selezionare **SuccessFactors**.
   
    ![Configura accesso Single Sign-On][26]
3. Scegliere dal menu hello in primo piano hello **utenti**.
   
    ![Assegna utente][27]
4. Nell'elenco di utenti hello, selezionare **Britta Simon**.
5. Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.
   
    ![Assegna utente][28]

### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On
obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.

Quando si fa clic hello SuccessFactors riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione SuccessFactors.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
