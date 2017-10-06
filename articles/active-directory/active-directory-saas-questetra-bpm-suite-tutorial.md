---
title: 'Esercitazione: Integrazione di Azure Active Directory con Questetra BPM Suite | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Questetra Business Suite.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a>Esercitazione: Integrazione di Azure Active Directory con Questetra BPM Suite
obiettivo di Hello di questa esercitazione è tooshow è come toointegrate Questetra BPM Suite con Azure Active Directory (Azure AD).  
Integrazione Questetra BPM Suite con Azure AD fornisce hello seguenti vantaggi: 

* È possibile controllare in Azure AD che ha accesso tooQuestetra Business Suite 
* È possibile abilitare l'utenti tooautomatically get connesso tooQuestetra Suite BPM (Single Sign-On) con i propri account Azure AD
* È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti
integrazione di Azure AD con Questetra BPM Suite tooconfigure, è necessario hello seguenti elementi:

* Sottoscrizione di Azure AD.
* Sottoscrizione di [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) abilitata per l'accesso Single Sign-On

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

1. Aggiunta gruppo BPM Questetra dalla raccolta hello 
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a>Aggiunta gruppo BPM Questetra dalla raccolta hello
integrazione hello tooconfigure di Questetra Business Suite in Azure AD, è necessario tooadd Questetra BPM gruppo dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Questetra BPM Suite dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**. 
   
    ![Active Directory][1]

2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.

3. visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
    ![Applicazioni][2]

4. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.
   
    ![Applicazioni][3]

5. In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.
   
    ![Applicazioni][4]

6. Nella casella di ricerca hello, digitare **Questetra BPM Suite**.
   
    ![Applicazioni][5]

7. Nel riquadro risultati hello selezionare **Questetra BPM Suite**, quindi fare clic su **completa** tooadd un'applicazione hello.

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
obiettivo di Hello di questa sezione è tooshow come tooconfigure e prova AD Azure single sign-on con Questetra BPM Suite basato su un utente di test denominato "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow è quale utente controparte hello utente tooan Questetra Business Suite in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello Questetra Business Suite deve toobe stabilita.  
Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** Questetra Business Suite.

tooconfigure e prova AD Azure single sign-on con Questetra Business Suite, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Questetra BPM Suite](#creating-a-questetra-bpm-suite-test-user)**  -toohave un equivalente di Britta Simon Questetra BPM Suite rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD
obiettivo di Hello di questa sezione è tooenable AD Azure single sign-on nel portale di Azure classico hello e tooconfigure single sign-on nell'applicazione Questetra Business Suite.

**tooconfigure AD Azure single sign-on con Questetra Business Suite, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico, in hello hello **Questetra BPM Suite** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On**  finestra di dialogo.
   
    ![Configura accesso Single Sign-On][8]

2. In hello **come si sarebbe ad esempio utenti toosign su tooQuestetra BPM Suite** selezionare **Azure Single Sign-On AD**e quindi fare clic su **Avanti**.
   
    ![Single Sign-On di Microsoft Azure AD][9]

3. In un'altra finestra del Web browser accedere al sito aziendale di **Questetra BPM Suite** come amministratore.

4. Scegliere dal menu hello in primo piano hello **le impostazioni di sistema**. 
   
    ![Single Sign-On di Microsoft Azure AD][10]

5. hello tooopen **SingleSignOnSAML** pagina, fare clic su **SSO (SAML)**. 
   
    ![Single Sign-On di Microsoft Azure AD][11]

6. Nel portale di Azure classico, in hello hello **Configura impostazioni App** finestra di dialogo eseguire hello alla procedura seguente: 
   
    ![Configurare le impostazioni dell'app][13]
   
    a. In è **Questetra BPM Suite** hello sezione SP informazioni del sito della società, hello copia **URL ACS**e quindi incollarlo hello **URL di accesso** casella di testo.
   
    b. In è **Questetra BPM Suite** hello sezione SP informazioni del sito della società, hello copia **ID entità**e quindi incollarlo hello **URL autorità di certificazione** casella di testo.
   
    c. In è **Questetra BPM Suite** hello sezione SP informazioni del sito della società, hello copia **URL ACS**e quindi incollarlo hello **URL di risposta** casella di testo.
   
    d. Fare clic su **Avanti**.

7. In hello **Configura accesso single sign-on Questetra BPM Suite** pagina, fare clic su **Scarica certificato**e quindi salvare il file di certificato hello in locale nel computer.
   
    ![Configura accesso Single Sign-On][14]

8. In è **Questetra BPM Suite** sito della società, eseguire hello alla procedura seguente: 
   
    ![Configura accesso Single Sign-On][15]
   
    a. Selezionare **Enable Single Sign-On**.
   
    b. Nel portale di Azure classico hello, copiare hello **URL autorità di certificazione** valore e quindi incollarlo hello **ID entità** casella di testo.
   
    c. Nel portale di Azure classico hello, copiare hello **URL servizio Single Sign-On** valore e quindi incollarlo hello **accesso URL della pagina** casella di testo.
   
    d. Nel portale di Azure classico hello, copiare hello **URL del servizio Single Sign-Out** valore e quindi incollarlo hello **URL pagina di disconnessione** casella di testo.
   
    e. In hello **NameID format** casella tipo **urn: oasis: nomi: tc: SAML: 1.1 NameID-formato: emailAddress**.

    f. Creare un file con codifica Base 64 dal certificato scaricato. 

    >[!TIP] 
    >Per ulteriori informazioni, vedere [come tooconvert certificato di un file binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o).

    g. Aprire il certificato con codifica base 64 nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo hello **certificato di convalida** casella di testo. 

    h. Fare clic su **Salva**.

1. Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **Avanti**. 
   
    ![Cos'è Azure AD Connect][17]

2. In hello **Single sign-on conferma** pagina, fare clic su **completa**.  
   
    ![Cos'è Azure AD Connect][18]


### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure classico chiamato Britta Simon hello toocreate.

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.
   
    ![Creare un utente test di Azure AD][100] 

2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.

3. Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.
   
    ![Creare un utente test di Azure AD][101] 

4. hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**. 
   
    ![Creare un utente test di Azure AD][102] 

5. In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente:
   
    ![Creare un utente test di Azure AD][103]
   
    a. In **Tipo di utente** selezionare **Nuovo utente nell'organizzazione**.
   
    b. In nome utente hello **textbox**, tipo **BrittaSimon**.
   
    c. Fare clic su Avanti.

6. In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente: 
   
    ![Creare un utente test di Azure AD][104] 
   
    a. In hello **nome** casella tipo **Laura**. 
   
    b. In hello **cognome** casella di testo, tipo, **Simon**.
   
    c. In hello **nome visualizzato** casella tipo **Britta Simon**.
   
    d. In hello **ruolo** elenco, selezionare **utente**.
   
    e. Fare clic su **Avanti**.

7. In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.
   
    ![Creare un utente test di Azure AD][105]  

8. In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:
   
    ![Creare un utente test di Azure AD][106]   
   
    a. Annotare il valore di hello di hello **nuova Password**.
   
    b. Fare clic su **Complete**.   

### <a name="creating-a-questetra-bpm-suite-test-user"></a>Creazione di un utente test di Questetra BPM Suite
obiettivo di Hello di questa sezione è toocreate un utente denominato Britta Simon Questetra Business Suite.

**un utente denominato Britta Simon Questetra Business Suite, toocreate eseguire hello alla procedura seguente:**

1. Sito dell'azienda Questetra BPM Suite tooyour accesso come amministratore.
2. Andare troppo**le impostazioni di sistema > elenco utenti > Nuovo utente**. 
3. Nella finestra di dialogo Nuovo utente hello eseguire hello alla procedura seguente: 
   
    ![Creare un utente test][300] 
   
    a. In hello **nome** casella di testo, digitare nome utente di Laura in Azure AD.
   
    b. In hello **posta elettronica** casella di testo, digitare nome utente di Laura in Azure AD.
   
    c. In hello **Password** casella di testo, digitare una password.

4. Fare clic su **Add new user**.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD
obiettivo di Hello di questa sezione è tooenabling toouse Britta Simon single sign-on Azure concedendo proprio tooQuestetra accesso Business Suite.

![Cos'è Azure AD Connect][200]

**tooassign Britta Simon tooQuestetra Business Suite, eseguire hello alla procedura seguente:**

1. In hello Azure portale classico, visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
    ![Cos'è Azure AD Connect][201]
2. Nell'elenco di applicazioni hello, selezionare **Questetra BPM Suite**.
   
    ![Cos'è Azure AD Connect][205]
3. Scegliere dal menu hello in primo piano hello **utenti**.
   
    ![Cos'è Azure AD Connect][202]
4. Nell'elenco di utenti hello, selezionare **Britta Simon**.
   
    ![Cos'è Azure AD Connect][203]
5. Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.
   
    ![Cos'è Azure AD Connect][204]

### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On
obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.  
Quando si fa clic su riquadro Questetra BPM Suite hello in hello Pannello di accesso, è necessario ottenere un'applicazione Questetra BPM Suite tooyour automaticamente firmato in.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
