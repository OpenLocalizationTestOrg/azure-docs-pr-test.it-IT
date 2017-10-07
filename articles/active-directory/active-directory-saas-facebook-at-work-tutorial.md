---
title: 'Esercitazione: Integrazione di Azure Active Directory con Workplace by Facebook | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e all'area di lavoro da Facebook.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: fd19b3f178a2aee7dd2f204d6d3cf6df8fe6b444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a>Esercitazione: Integrazione di Azure Active Directory con Workplace by Facebook

In questa esercitazione, è illustrato come toointegrate all'area di lavoro da Facebook con Azure Active Directory (Azure AD).

L'integrazione all'area di lavoro da Facebook con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooWorkplace da Facebook.
- È possibile abilitare gli utenti tooautomatically ottenere l'accesso tooWorkplace da Facebook (single sign-on) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale: hello portale di Azure.

Per altri dettagli sull'integrazione di app SaaS (Software as a Service) con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con area di lavoro da Facebook tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Una sottoscrizione a Workplace by Facebook abilitata per l'accesso Single Sign-On (SSO)

passaggi di hello tootest in questa esercitazione, seguire queste indicazioni:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene testato l'accesso SSO di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiungere all'area di lavoro da Facebook dalla raccolta di hello.
2. Configurare e testare l'accesso Single Sign-On di Azure AD.

## <a name="add-workplace-by-facebook-from-hello-gallery"></a>Aggiungere all'area di lavoro da Facebook dalla raccolta di hello
integrazione di hello tooconfigure di lavoro da Facebook in Azure AD, aggiungere all'area di lavoro da Facebook hello raccolta tooyour elenco di App SaaS gestite.

1. In hello [portale di Azure](https://portal.azure.com), nel riquadro sinistro di hello, selezionare **Azure Active Directory**. 

    ![pulsante di Hello Azure Active Directory][1]

2. Sfoglia troppo**applicazioni aziendali** > **tutte le applicazioni**.

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. tooadd hello nuova applicazione, seleziona **nuova applicazione** nella parte superiore di hello della finestra di dialogo hello.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, digitare **all'area di lavoro da Facebook**e selezionare **all'area di lavoro da Facebook** dai risultati. Selezionare quindi **Aggiungi**, un'applicazione hello tooadd.

    ![Nell'elenco dei risultati all'area di lavoro da Facebook in hello](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso SSO di Azure AD con Workplace by Facebook usando un utente di test di nome "Britta Simon".

Per toowork SSO, Azure AD deve tooknow quale utente controparte hello nell'area di lavoro da Facebook è tooa utente in Azure AD. In altre parole, stabilire una relazione tra un utente di Azure Active Directory e l'utente correlato di hello nell'area di lavoro da Facebook collegata.

Stabilire questa relazione assegnando il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** nell'area di lavoro da Facebook.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure Active Directory SSO in hello portale di Azure e si configura SSO nell'area di lavoro dall'applicazione Facebook.

1. Nel portale di Azure su hello hello **all'area di lavoro da Facebook** pagina di integrazione dell'applicazione, seleziona **Single sign-on**.

    ![Configurare il collegamento Single Sign-On][4]

2. In hello **Single sign-on** nella finestra di dialogo **modalità** come **basato su SAML Sign-on** tooenable SSO.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. In hello **all'area di lavoro al dominio di Facebook e URL** sezione, hello seguenti:

    a. In hello **Sign-on URL** nella casella di testo digitare l'URL che utilizza hello seguente motivo:`https://<company subdomain>.facebook.com`

    b. In hello **identificatore** nella casella di testo digitare l'URL che utilizza hello seguente motivo:`https://www.facebook.com/company/<scim company id>`

    > [!NOTE]
    > Questi valori sono solo un esempio. Aggiornare questi valori con URL hello effettivo sign-on e l'identificatore. Contatto hello [all'area di lavoro dal team di supporto Client di Facebook](https://workplace.fb.com/faq/) tooget questi valori. 

4. In hello **certificato di firma SAML** selezionare **certificato (Base64)**e quindi salvare il file di certificato hello nel computer in uso.

    ![collegamento al download del certificato Hello](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. Selezionare **Salva**.

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. In hello **all'area di lavoro dalla configurazione di Facebook** selezionare **configurare all'area di lavoro da Facebook** tooopen hello **Configura sign-on** finestra. Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **riferimento rapido** sezione.

    ![Configurazione di Workplace by Facebook](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. In una finestra del web browser, accedere all'area di lavoro dal sito della società Facebook tooyour come amministratore.
  
   > [!NOTE] 
   > Come parte del processo di autenticazione SAML hello, all'area di lavoro è possibile utilizzare le stringhe di query di backup too2.5 kilobyte in dimensioni in ordine toopass parametri tooAzure Active Directory.

8. In hello **Dashboard aziendali**, visitare toohello **autenticazione** scheda.

9. In **SAML Authentication**selezionare **SSO solo** dall'elenco a discesa hello.

10. Immettere i valori hello copiati hello **all'area di lavoro dalla configurazione di Facebook** sezione del portale di Azure nei campi corrispondenti hello hello:

    *   Nel **SAML URL** Incolla hello valore della casella di testo **URL servizio Single Sign-On**, che è stato copiato da hello portale di Azure.
    *   Nel **SAML Issuer URL** Incolla hello valore della casella di testo **ID entità SAML**, che è stato copiato da hello portale di Azure.
    *   In **SAML Logout Redirect (facoltativo)**, incollare il valore di hello di **Sign-Out URL**, che è stato copiato da hello portale di Azure.
    *   Aprire il **certificato con codifica base 64** nel blocco note, scaricato dal portale di Azure hello. Copia contenuto hello negli Appunti e quindi incollarlo toothe **SAML Certificate** casella di testo.

11. Potrebbe essere necessario destinatari hello tooenter URL, l'URL del destinatario e ACS (servizio Consumer di asserzione) URL, elencati in hello **configurazione SAML** sezione.

12. Scorrere nella parte inferiore toohello della sezione hello e selezionare **SSO Test**. Viene visualizzata una finestra popup con hello Azure AD nella pagina di accesso. tooauthenticate, immettere le credenziali come di consueto. Verificare l'indirizzo di posta elettronica hello restituito da Azure AD è hello stesso hello account aziendale con cui si è connessi.

13. Se è stato completato il test di hello, scorrere toohello parte inferiore della pagina hello e selezionare **salvare**.

14. Chiunque usi Workplace visualizza ora la pagina di accesso ad Azure AD per l'autenticazione.

È possibile scegliere tooconfigure un URL, che può essere utilizzato toopoint alla pagina di disconnessione hello Azure AD di disconnessione SAML. Quando questa impostazione è abilitata e configurata, hello utente non è più diretto toohello pagina di disconnessione all'area di lavoro. In alternativa, hello è reindirizzato toohello URL che è stato aggiunto in base alle impostazioni di reindirizzamento disconnessione SAML hello.


> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello. Dopo l'aggiunta di questa app da hello **Active Directory** > **applicazioni aziendali** , selezionare semplicemente hello **Single Sign-On** scheda e hello accesso documentazione tramite hello incorporato **configurazione** sezione nella parte inferiore di hello. Altre informazioni sulla funzionalità di documentazione embedded hello in hello [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="configure-reauthentication-frequency"></a>Configurare la frequenza di riautenticazione

È possibile configurare tooprompt all'area di lavoro per un controllo SAML ogni giorno, tre giorni, una settimana, mese, due settimane o mai.

> [!NOTE] 
>Hello valore minimo per il controllo SAML hello in applicazioni per dispositivi mobili è impostata tooone settimana.

È inoltre possibile forzare una reimpostazione SAML per tutti gli utenti. toodo hello, utilizzare **SAML richiedono l'autenticazione per tutti gli utenti ora** pulsante.


### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

1. In hello **portale di Azure**, nel riquadro sinistro di hello, selezionare **Azure Active Directory**.

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**e selezionare **tutti gli utenti**.
    
    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** nella finestra di dialogo **Aggiungi**.
 
    ![pulsante Aggiungi Hello](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo casella, hello seguenti:
 
    ![finestra di dialogo utente Hello](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    a. In hello **nome** nella casella di testo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Mostra password**e annotare la password.

    d. Selezionare **Crea**.
 
### <a name="create-a-workplace-by-facebook-test-user"></a>Creare un utente test di Workplace by Facebook

In questa sezione si crea un utente di nome Britta Simon in Workplace by Facebook. Workplace by Facebook supporta il provisioning JIT, abilitato per impostazione predefinita.

Non è necessaria alcuna azione dell'utente in questa sezione. Se un utente non esiste nell'area di lavoro da Facebook, una nuova istanza viene creata quando si tenta di tooaccess all'area di lavoro da Facebook.

>[!Note]
>Se è necessario un utente toocreate manualmente, contattare hello [all'area di lavoro dal team di supporto Client di Facebook](https://workplace.fb.com/faq/).

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse SSO Azure concessione dell'accesso tooWorkplace da Facebook.

![Assegnare utenti][200] 

1. Consente di visualizzare applicazioni di portale, aprire hello in hello Azure. Vai a visualizzazione directory toohello, andare troppo**applicazioni aziendali**, quindi selezionare **tutte le applicazioni**.

    ![Assegnare utenti][201] 

2. Nell'elenco di applicazioni hello, selezionare **all'area di lavoro da Facebook**.

    ![Hello all'area di lavoro da Facebook collegamento nell'elenco delle applicazioni hello](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. Dal menu hello hello sinistra, selezionare **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202] 

4. Selezionare **Aggiungi**. Quindi, nel hello **Aggiungi** riquadro, selezionare **utenti e gruppi**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In hello **utenti e gruppi** nella finestra di dialogo **Britta Simon** nell'elenco di utenti hello.

6. In hello **utenti e gruppi** nella finestra di dialogo **selezionare**.

7. In hello **Aggiungi** nella finestra di dialogo **assegnare**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

Se si desiderano tootest le impostazioni SSO, aprire Pannello di accesso hello.
Per ulteriori informazioni, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).


## <a name="next-steps"></a>Passaggi successivi

* Vedere hello [elenco di esercitazioni sulla toointegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md).
* Leggere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).
* Per ulteriori informazioni su troppo[Configura provisioning utente](active-directory-saas-facebook-at-work-provisioning-tutorial.md).



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

