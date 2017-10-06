---
title: 'Esercitazione: Integrazione di Azure Active Directory con Soonr Workplace | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Soonr all'area di lavoro.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: f950b45d0beceab2fa17b7690c9de81ec6603089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a>Esercitazione: Integrazione di Azure Active Directory con Soonr Workplace

obiettivo di Hello di questa esercitazione è tooshow è come toointegrate Soonr all'area di lavoro con Azure Active Directory (Azure AD).  
Integrazione Soonr all'area di lavoro con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooSoonr all'area di lavoro
- È possibile abilitare l'utenti tooautomatically get connesso tooSoonr all'area di lavoro (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

tooconfigure integrazione di Azure AD con Soonr all'area di lavoro, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Soonr Workplace abilitata per l'accesso Single Sign-On


> [!NOTE] 
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.


passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione, a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrizione dello scenario
obiettivo di Hello di questa esercitazione è tooenable si tootest AD Azure single sign-on in un ambiente di test.  
scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta all'area di lavoro Soonr dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD


## <a name="adding-soonr-workplace-from-hello-gallery"></a>Aggiunta all'area di lavoro Soonr dalla raccolta hello
integrazione hello tooconfigure di Soonr all'area di lavoro in Azure AD, è necessario tooadd Soonr all'area di lavoro dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Soonr all'area di lavoro Raccolta hello, eseguire hello alla procedura seguente:**

1. In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**. 

    ![Active Directory][1]

2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.

3. visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.

    ![Applicazioni][2]

4. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.

    ![Applicazioni][3]

5. In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.
 
    ![Applicazioni][4]

6. Nella casella di ricerca hello, digitare **Soonr all'area di lavoro**.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. Nel riquadro risultati hello selezionare **Soonr all'area di lavoro**, quindi fare clic su **completa** tooadd un'applicazione hello.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
obiettivo di Hello di questa sezione è tooshow come tooconfigure e prova AD Azure single sign-on con Soonr all'area di lavoro basato su un utente di test denominato "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow è quale utente controparte hello utente tooan Soonr all'area di lavoro in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello nell'area di lavoro Soonr deve toobe stabilita.  

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Soonr all'area di lavoro.

tooconfigure e prova AD Azure single sign-on con Soonr all'area di lavoro, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente di test all'area di lavoro Soonr](#creating-a-soonr-workplace-test-user)**  -toohave un equivalente di Britta Simon Soonr area di lavoro che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on nel portale classico hello e configurare l'accesso single sign-on nell'applicazione Soonr all'area di lavoro.


**Azure AD tooconfigure single sign-on con Soonr all'area di lavoro, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico, in hello hello **Soonr all'area di lavoro** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On**  finestra di dialogo.

    ![Configura accesso Single Sign-On][6] 

2. In hello **come si sarebbe ad esempio utenti toosign su tooSoonr all'area di lavoro** selezionare **Azure Single Sign-On AD**e quindi fare clic su **Avanti**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. In hello **Configura impostazioni App** finestra di dialogo eseguire hello alla procedura seguente:.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    a. In hello **URL di accesso** casella di testo, digitare un URL con modello di hello: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.

    b. Fare clic su **Avanti**.

    > [!NOTE] 
    > Si noti che questo non è il valore reale hello. È necessario tooupdate URL di accesso questo valore con hello effettivo. Contattare tooget team di supporto Soonr all'area di lavoro di questo valore.

4. In hello **Configura accesso single sign-on in luogo di lavoro Soonr** pagina, fare clic su **Scarica metadati** e quindi salvare il file hello nel computer in uso:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. tooget SSO configurato per l'applicazione, contattare il team di supporto Soonr all'area di lavoro e fornire loro seguente hello: 

    • hello scaricato **metadati** file

    • hello **URL autorità di certificazione**

    • hello **URL SSO SAML**

    • hello **URL del servizio Single Sign-Out**

    >[!NOTE]
    >Questa applicazione è stata sostituita da <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask all'area di lavoro</a> e farvi riferimento <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">questo</a> esercitazione per la configurazione di un'applicazione hello con Azure AD.
   
6. Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **Avanti**.

    ![Single Sign-On di Microsoft Azure AD][10]

7. In hello **Single sign-on conferma** pagina, fare clic su **completa**.  
  
    ![Single Sign-On di Microsoft Azure AD][11]



### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure classico chiamato Britta Simon hello toocreate.  

![Creare un utente di Azure AD][20]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.

3. Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente:

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    a. In Tipo di utente selezionare Nuovo utente nell'organizzazione.

    b. In nome utente hello **textbox**, tipo **BrittaSimon**.

    c. Fare clic su **Avanti**.

6.  In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente:

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    a. In hello **nome** casella tipo **Laura**.  

    b. In hello **cognome** casella di testo, tipo, **Simon**.

    c. In hello **nome visualizzato** casella tipo **Britta Simon**.

    d. In hello **ruolo** elenco, selezionare **utente**.

    e. Fare clic su **Avanti**.

7. In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    a. Annotare il valore di hello di hello **nuova Password**.

    b. Fare clic su **Complete**.   



### <a name="creating-a-soonr-workplace-test-user"></a>Creazione di un utente test di Soonr Workplace

obiettivo di Hello di questa sezione è un utente denominato Britta Simon nell'area di lavoro Soonr toocreate. Rivolgersi all'area di lavoro Soonr supporto team toocreate un utente nella piattaforma hello. È possibile generare il ticket di supporto hello con Soonr da <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">qui</a>.


### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

obiettivo di Hello di questa sezione è tooenabling toouse Britta Simon single sign-on Azure concedendo proprio tooSoonr accesso all'area di lavoro.

![Assegna utente][200] 

**tooassign Britta Simon tooSoonr all'area di lavoro, eseguire hello alla procedura seguente:**

1. In hello Azure portale classico, visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Soonr all'area di lavoro**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. Scegliere dal menu hello in primo piano hello **utenti**.

    ![Assegna utente][203] 

1. Nell'elenco di utenti hello, selezionare **Britta Simon**.

2. Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.

    ![Assegna utente][205]



### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.  
Quando si fa clic hello all'area di lavoro Soonr riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione Soonr all'area di lavoro.


## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
