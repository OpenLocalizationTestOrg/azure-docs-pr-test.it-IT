---
title: 'Esercitazione: Integrazione di Azure Active Directory con Wizergos Productivity Software | Microsoft Docs'
description: "Informazioni su come tooconfigure single sign-on tra Azure Active Directory e produttività Wizergos."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: cdd186c38c426dde404ed8bb84700faf9c8c1a46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a>Esercitazione: Integrazione di Azure Active Directory con Wizergos Productivity Software
obiettivo di Hello di questa esercitazione è tooshow è come toointegrate Wizergos produttività con Azure Active Directory (Azure AD).

Integrazione di Software per la produttività Wizergos con Azure AD fornisce hello seguenti vantaggi:

* È possibile controllare in Azure AD che ha accesso tooWizergos Software per la produttività
* È possibile abilitare l'utenti tooautomatically get connesso tooWizergos produttività single sign-on (SSO) con i propri account Azure AD
* È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti
integrazione di Azure AD con Software per la produttività Wizergos tooconfigure, è necessario hello seguenti elementi:

* Sottoscrizione di Azure AD.
* Sottoscrizione di Wizergos Productivity Software abilitata per l'accesso SSO

>[!NOTE]
>hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione. 
> 

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

* Non usare l'ambiente di produzione, a meno che non sia necessario.
* Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
obiettivo di Hello di questa esercitazione è tooenable si tootest SSO AD Azure in un ambiente di test.

scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Software per la produttività Wizergos dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On (SSO) di Microsoft Azure AD

## <a name="adding-wizergos-productivity-software-from-hello-gallery"></a>Aggiunta di Software per la produttività Wizergos dalla raccolta hello
integrazione hello tooconfigure di produttività Wizergos in Azure AD, è necessario tooadd Wizergos produttività Software dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Wizergos produttività Software dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**. 
   
    ![Active Directory][1]
2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.
3. visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
    ![Applicazioni][2]
4. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.
   
    ![Applicazioni][3]
5. In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.
   
    ![Applicazioni][4]
6. Nella casella di ricerca hello, digitare **Wizergos produttività**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. Nel riquadro dei risultati hello, selezionare **produttività Wizergos**, quindi fare clic su **completa** tooadd un'applicazione hello.
   
    ![Selezionare l'applicazione hello nella raccolta hello](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a>Configurare e testare l'accesso Single Sign-On (SSO) di Azure AD
obiettivo di Hello di questa sezione è tooshow come tooconfigure e test di accesso SSO AD Azure con Wizergos produttività Software basato su un utente di test denominato "Britta Simon".

Per toowork SSO, Azure AD deve tooknow è quale utente controparte hello utente tooan Wizergos produttività in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e utente correlato di hello nel Software di produttività Wizergos deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** Wizergos produttività software.

tooconfigure e prova AD Azure single sign-on con BynWizergos produttività Softwareder, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure single sign-on AD](#configuring-azure-ad-single-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente di test del Software per la produttività Wizergos](#creating-a-wizergos-productivity-software-test-user)**  -toohave un equivalente di Britta Simon Wizergos produttività software che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di accesso single sign-on](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-sso"></a>Configurazione dell'accesso Single Sign-On (SSO) di Microsoft Azure AD
In questa sezione, si abilita Azure AD single sign-on nel portale classico hello e configurare single sign-on Wizergos produttività dell'applicazione in uso.

**tooconfigure Azure single sign-on AD Wizergos produttività software, eseguire hello alla procedura seguente:**

1. Nel portale classico hello in hello **produttività Wizergos** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On**finestra di dialogo.
   
    ![Configura accesso Single Sign-On][6] 
2. In hello **come si sarebbe ad esempio utenti toosign su tooWizergos Software per la produttività** selezionare **Azure Single Sign-On AD**e quindi fare clic su **Avanti**:
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. In hello **Configura impostazioni App** nella pagina, fare clic su **Avanti**:
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. In hello **Configura accesso single sign-on in Software di produttività Wizergos** pagina, fare clic su **Scarica certificato**e quindi salvare il file hello nel computer in uso:
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. In una finestra del web browser, tenant produttività Wizergos tooyour accesso come amministratore.
6. Scegliere dal menu a tre linee hello **Admin**.
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. Nella pagina visualizzata selezionare **AUTHENTICATION** (AUTENTICAZIONE) nel menu a sinistra e fare clic su **Azure AD**.
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. Eseguire hello seguendo i passaggi **autenticazione** sezione.
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. Fare clic su **caricare** hello tooupload pulsante scaricato certificato da Azure AD. 
  2. In hello **URL autorità di certificazione** casella di testo inserire il valore di hello di **URL autorità di certificazione** dalla configurazione guidata di Azure AD applicazione.
  3. In hello **URL servizio Single Sign-On** casella di testo inserire il valore di hello di **URL servizio Single Sign-on** dalla configurazione guidata di Azure AD applicazione.
  4. In hello **Single Sign-Out URL** casella di testo inserire il valore di hello di **URL del servizio Single Sign-Out** dalla configurazione guidata di Azure AD applicazione.
  5. Fare clic sul pulsante **Salva** .
9. Nel portale classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **Avanti**.
   
    ![Single Sign-On di Microsoft Azure AD][10]
10. In hello **Single sign-on conferma** pagina, fare clic su **completa**.  
    
    ![Single Sign-On di Microsoft Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
obiettivo di Hello di questa sezione è toocreate un utente di test nel portale classico di hello chiamato Britta Simon.

![Creare un utente di Azure AD][20]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.
3. Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente:
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. In Tipo di utente selezionare Nuovo utente nell'organizzazione.
  2. In nome utente hello **textbox**, tipo **BrittaSimon**.
  3. Fare clic su **Avanti**.
6. In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente:
   
   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. In hello **nome** casella tipo **Laura**.  
  2. In hello **cognome** casella di testo, tipo, **Simon**.
  3. In hello **nome visualizzato** casella tipo **Britta Simon**.
  4. In hello **ruolo** elenco, selezionare **utente**.
  5. Fare clic su **Avanti**.
7. In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. Annotare il valore di hello di hello **nuova Password**.
  2. Fare clic su **Complete**.   

### <a name="create-a-wizergos-productivity-software-test-user"></a>Creare un utente di test Wizergos Productivity Software
In questa sezione viene creato un utente chiamato Britta Simon in Wizergos Productivity Software. Rivolgersi al team di supporto di Software per la produttività Wizergos tramite [ support@wizergos.com ](emailTo:support@wizergos.com) utenti hello tooadd nella piattaforma di produttività Wizergos hello.

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD
obiettivo Hello di questa sezione è tooenabling Britta Simon toouse SSO Azure concedendo proprio tooWizergos accesso Software per la produttività.

  ![Assegna utente][200]

**tooassign Britta Simon tooWizergos Software per la produttività, eseguire hello alla procedura seguente:**

1. Nel portale classico hello, fare clic su visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello **applicazioni** nel menu superiore hello.
   
    ![Assegna utente][201]
2. Nell'elenco di applicazioni hello, selezionare **Wizergos produttività**.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. Scegliere dal menu hello in primo piano hello **utenti**.
   
    ![Assegna utente][203]
4. Nell'elenco di utenti hello, selezionare **Britta Simon**.
5. Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.
   
    ![Assegna utente][205]

### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On
obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Wizergos produttività hello in hello Pannello di accesso, è necessario ottenere l'applicazione Software per la produttività Wizergos tooyour firmato in automaticamente.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
