---
title: 'Esercitazione: Integrazione di Azure Active Directory con Halosys | Documentazione Microsoft'
description: Informazioni su come toouse Halosys con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a>Esercitazione: Integrazione di Azure Active Directory con Halosys

In questa esercitazione, è illustrato come toointegrate Halosys con Azure Active Directory (Azure AD).

Integrazione Halosys con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooHalosys
- È possibile abilitare l'utenti tooautomatically get connesso tooHalosys (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Halosys tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Halosys abilitata per l'accesso Single Sign-On


> [!NOTE] 
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.


passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione, a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.

scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Halosys dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD


## <a name="adding-halosys-from-hello-gallery"></a>Aggiunta di Halosys dalla raccolta hello
integrazione hello tooconfigure di Halosys in Azure AD, è necessario tooadd Halosys dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Halosys dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.

    ![Active Directory][1]
2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.

3. visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.

    ![Applicazioni][2]

4. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.

    ![Applicazioni][3]

5. In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.

    ![Applicazioni][4]

6. Nella casella di ricerca hello, digitare **Halosys**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. Nel riquadro risultati hello selezionare **Halosys**, quindi fare clic su **completa** tooadd un'applicazione hello.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Halosys usando un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Halosys è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Halosys deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Halosys.

tooconfigure e prova AD Azure single sign-on con Halosys, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Halosys](#creating-a-halosys-test-user)**  -toohave un equivalente di Britta Simon in Halosys toohello collegato AD Azure rappresentazione in seguito.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on nel portale classico hello e configurare l'accesso single sign-on nell'applicazione Halosys.


**Azure AD tooconfigure single sign-on con Halosys, eseguire hello alla procedura seguente:**

1. Nel portale classico hello in hello **Halosys** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo.
     
    ![Configura accesso Single Sign-On][6] 

2. In hello **come si sarebbe ad esempio utenti toosign su tooHalosys** selezionare **Azure Single Sign-On AD**e quindi fare clic su **Avanti**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. In hello **Configura impostazioni App** finestra di dialogo eseguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    a. In hello **URL di accesso** casella di testo, digitare l'URL hello usato dall'applicazione Halosys tooyour toosign-on agli utenti tramite hello seguente modello: `https://<company-name>.Halosys.com/client-api/api`.

    hello b.In **URL dell'identificatore** casella di testo, digitare l'URL nel modello di hello hello: `https://<company-name>.Halosys.com`. 
         
4. In hello **configurare single sign-on a Halosys** pagina, fare clic su **Scarica metadati**e quindi salvare il file hello nel computer in uso:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. tooget SSO configurato per l'applicazione, contattare il team di supporto Halosys e fornire loro seguente hello:

    • hello scaricato **file di metadati**
    
    • hello **URL SSO SAML**
    

6. Nel portale classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **Avanti**.
    
    ![Single Sign-On di Microsoft Azure AD][10]

7. In hello **Single sign-on conferma** pagina, fare clic su **completa**.  
 
    ![Single Sign-On di Microsoft Azure AD][11]


### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
In questa sezione creare un utente test nel portale classico di hello chiamato Britta Simon.


![Creare un utente di Azure AD][20]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.

3. Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente: ![creazione di un utente prova AD Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png) 

    a. In Tipo di utente selezionare Nuovo utente nell'organizzazione.

    b. In nome utente hello **textbox**, tipo **BrittaSimon**.

    c. Fare clic su **Avanti**.

6.  In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente: ![creazione di un utente prova AD Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png) 

    a. In hello **nome** casella tipo **Laura**.  

    b. In hello **cognome** casella di testo, tipo, **Simon**.

    c. In hello **nome visualizzato** casella tipo **Britta Simon**.

    d. In hello **ruolo** elenco, selezionare **utente**.

    e. Fare clic su **Avanti**.

7. In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    a. Annotare il valore di hello di hello **nuova Password**.

    b. Fare clic su **Completa**.   



### <a name="creating-a-halosys-test-user"></a>Creazione di un utente test per Halosys

In questa sezione viene creato un utente chiamato Britta Simon in Halosys. Rivolgersi Halosys utenti tooadd hello team di supporto nella piattaforma Halosys hello.


### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooHalosys proprio accesso.

![Assegna utente][200] 

**tooassign Britta Simon tooHalosys, eseguire hello alla procedura seguente:**

1. Nel portale classico hello, fare clic su visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello **applicazioni** nel menu superiore hello.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Halosys**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. Scegliere dal menu hello in primo piano hello **utenti**.

    ![Assegna utente][203]

4. Nell'elenco di utenti hello, selezionare **Britta Simon**.

5. Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.

    ![Assegna utente][205]


### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic hello Halosys riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Halosys applicazione.


## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
