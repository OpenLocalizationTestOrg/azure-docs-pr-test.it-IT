---
title: 'Esercitazione: Integrazione di Azure Active Directory con Help Scout | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Scout Guida in linea.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 58edd140eb1eb5980796ca743b5f7acd891729a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a>Esercitazione: Integrazione di Azure Active Directory con Help Scout

In questa esercitazione illustrato come utilizzare toointegrate Guida con Azure Active Directory (Azure AD).

Si otterrà i seguenti vantaggi dagli Scout consentono l'integrazione con Azure AD hello:

- In Azure AD, è possibile controllare chi ha accesso tooHelp Scout.
- È possibile accedere automaticamente il tooHelp utenti Scout con accesso single sign-on e un account utente in Azure AD.
- È possibile gestire gli account in una posizione centrale, hello portale di Azure.

toolearn ulteriori informazioni su software come un servizio (SaaS) integrazione dell'applicazione con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

tooset l'integrazione di Azure AD con Scout della Guida, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Help Scout, con Single Sign-On attivato 

> [!NOTE]
> Se si passi hello in questa esercitazione, si consiglia di non testare loro in un ambiente di produzione.

Indicazioni per il test passaggi hello in questa esercitazione:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione gratuita di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. 

scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiungere Scout Guida dalla raccolta di hello.
2. Configurare e testare l'accesso Single Sign-On di Azure AD.

## <a name="add-help-scout-from-hello-gallery"></a>Aggiungere Scout Guida dalla raccolta di hello
tooset l'integrazione di hello di Guida Scout con Azure AD, nella raccolta di hello, aggiungere l'elenco tooyour Scout Guida in linea di App SaaS gestite.

tooadd Scout Guida dalla raccolta hello:

1. In hello [portale di Azure](https://portal.azure.com)in hello menu a sinistra, selezionare **Azure Active Directory**. 

    ![pulsante di Hello Azure Active Directory][1]

2. Selezionare **Applicazioni aziendali** e quindi selezionare **Tutte le applicazioni**.

    ![pagina applicazioni di Enterprise Hello][2]
    
3. Selezionare una nuova applicazione, tooadd **nuova applicazione**.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, immettere **Guida Scout**. Nei risultati della ricerca hello, selezionare **Guida Scout**, quindi selezionare **Aggiungi**.

    ![Guida in linea Scout nell'elenco risultati hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Help Scout in base a un utente di test di nome *Britta Simon*.

Per toowork di accesso singolo, Azure AD deve tooknow hello Azure controparte utente di Active Directory nella Guida in linea Scout. È necessario stabilire una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Guida in linea Scout.

hello tooestablish relazione, in Guida in linea Scout, dei collegamenti per **Username**, assegnare il valore di hello di hello **nome utente** in Azure AD.

tooconfigure e prova AD Azure single sign-on con Scout Guida in linea, hello completo seguenti attività:

1. [Configurare l'accesso Single Sign-On di Azure AD](#set-up-azure-ad-single-sign-on). Imposta un toouse utente questa funzionalità.
2. [Creare un utente test di Azure AD](#create-an-azure-ad-test-user). Test AD Azure single sign-on con utente hello Britta Simon.
3. [Creare un utente di test di Help Scout](#create-a-help-scout-test-user). Crea un equivalente di Britta Simon Scout della Guida che è collegato toohello rappresentazione in forma di Azure AD dell'utente hello.
4. [Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user). Imposta Britta Simon toouse AD Azure single sign-on.
5. [Testare l'accesso Single Sign-On](#test-single-sign-on). Verifica che la configurazione di hello funziona.

### <a name="set-up-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, impostare di Azure AD single sign-on in hello portale di Azure. quindi si configura Single Sign-On nell'applicazione Help Scout.

tooset di Azure AD single sign-on con Scout Guida:

1. Nel portale di Azure su hello hello **Guida Scout** pagina di integrazione dell'applicazione, seleziona **Single sign-on**.
 
    ![Collegamento di configurazione di Single Sign-On][4]

2. In hello **Single sign-on** pagina per **modalità**selezionare **basato su SAML Sign-on**.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. In **Guida Scout dominio e gli URL**, se si desidera tooset di un'applicazione hello in modalità avviata da IDP hello completo alla procedura seguente:

    1. In hello **identificatore** , immettere un URL con hello seguente motivo:`urn:auth0:helpscout:<instancename>`

    2. In hello **URL di risposta** , immettere un URL con hello seguente motivo:`https://helpscout.auth0.com/login/callback?connection=<instancename>`

    ![Informazioni su URL e dominio per Single Sign-On di Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. Se si desidera tooset di un'applicazione hello in modalità SP initiated, selezionare hello **Mostra URL impostazioni avanzate** casella di controllo e quindi hello seguenti:

    * In hello **URL di accesso** , immettere un URL con hello seguente formato:`https://secure.helpscout.net/members/login/`

    ![Informazioni su URL e dominio per Single Sign-On di Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > i valori Hello in questi URL sono solo a scopo dimostrativo. Aggiornare i valori hello con URL effettivo identificatore hello e l'URL di risposta. Questi valori, contattare il tooget [team di supporto della Guida Scout](mailto:help@helpscout.com). 

5. In **certificato di firma SAML**selezionare **Metadata XML**e quindi salvare il file di metadati hello nel computer in uso.

    ![collegamento al download del certificato Hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. Selezionare **Salva**.

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. tooset di single sign-on sul lato di Guida Scout hello, trasmissione hello scaricato metadati XML file toohello [team di supporto della Guida Scout](mailto:help@helpscout.com). il team di supporto della Guida Scout Hello si applica questa impostazione in modo che sia impostata correttamente hello SAML single sign-on connessione su entrambi i lati.

> [!TIP]
> È possibile leggere una versione di queste istruzioni in hello concisa [portale di Azure](https://portal.azure.com), mentre si configura l'app. Dopo aver aggiunto l'applicazione hello selezionando **Active Directory** > **applicazioni aziendali**selezionare hello **Single Sign-On** scheda. È possibile accedere alla documentazione di hello incorporato in hello **configurazione** alla sezione, hello parte inferiore della pagina hello. Per altre informazioni, vedere la [documentazione incorporata su Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

In questa sezione, nel portale di Azure hello si crea un utente di test denominato Britta Simon.

![Creare un utente test di Azure AD][100]

toocreate un utente di prova in Azure AD:

1. Nel portale di Azure, nel menu a sinistra di hello, hello selezionare **Azure Active Directory**.

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. elenco di hello toodisplay di utenti, selezionare **utenti e gruppi**, quindi selezionare **tutti gli utenti**.

    ![Selezionare Utenti e gruppi e quindi selezionare Tutti gli utenti.](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. hello tooopen **utente** la finestra di dialogo, nella parte superiore di hello di hello **tutti gli utenti** selezionare **Aggiungi**.

    ![pulsante Aggiungi Hello](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. In hello **utente** della finestra di dialogo hello completo alla procedura seguente:

    1. In hello **nome** immettere **BrittaSimon**.

    2. In hello **nome utente** , immettere l'indirizzo di posta elettronica hello di Britta Simon utente.

    3. Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.

    4. Selezionare **Crea**.

        ![finestra di dialogo utente Hello](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a>Creare un utente test di Help Scout

oggetto Hello di questa sezione è un utente denominato Britta Simon nella Guida in linea Scout toocreate. Help Scout supporta il provisioning JIT, che è attivato per impostazione predefinita.

In questa sezione non è toocomplete alcuna azione o un'attività. Se un utente non esiste già nella Guida in linea Scout, viene creato uno nuovo quando si tenta di tooaccess Scout Guida in linea.

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione utente hello Britta Simon toouse AD Azure single sign-on tramite la concessione di hello utente account accesso tooHelp Scout.

![Assegnazione del ruolo utente hello][200] 

tooassign Britta Simon tooHelp Scout:

1. Nel portale di Azure hello, aprire visualizzazione applicazioni hello e fare clic sulla visualizzazione directory toohello. Selezionare **Applicazioni aziendali** e quindi selezionare **Tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Guida Scout**.

    ![collegamento della Guida Scout Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. Nel menu a sinistra di hello, selezionare **utenti e gruppi**.

    ![Hello gli utenti e gruppi][202]

4. Selezionare **Aggiungi**. Quindi, nella hello **Aggiungi** selezionare **utenti e gruppi**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In hello **utenti e gruppi** hello elenco di utenti, selezionare pagina **Britta Simon**.

6. In hello **utenti e gruppi** selezionare **selezionare**.

7. In hello **Aggiungi** selezionare **assegnare**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando il pannello di accesso di hello.

Quando si seleziona riquadro Guida Scout hello nel Pannello di accesso hello, è necessario essere connessi automaticamente tooyour applicazione Scout Guida in linea.

Per ulteriori informazioni sul pannello di accesso, vedere [Pannello di accesso di introduzione toohello](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sull'App SaaS toointegrate con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png

