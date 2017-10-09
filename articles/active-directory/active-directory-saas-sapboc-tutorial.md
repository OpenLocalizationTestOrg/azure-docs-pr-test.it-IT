---
title: 'Esercitazione: Integrazione di Azure Active Directory con SAP Business Object Cloud | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e SAP Business oggetto Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: a3e9bd93897271531f91bcbc50cd361e8a20551e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a>Esercitazione: Integrazione di Azure Active Directory con SAP Business Object Cloud

In questa esercitazione, è illustrato come toointegrate SAP Business oggetto Cloud con Azure Active Directory (Azure AD).

Si otterrà hello seguenti vantaggi quando si integra SAP Business oggetto Cloud con Azure AD:

- In Azure AD, è possibile controllare chi ha accesso tooSAP Cloud oggetto Business.
- È possibile accedere automaticamente il tooSAP utenti Business oggetto Cloud con accesso single sign-on e un account utente in Azure AD.
- È possibile gestire gli account in una posizione centrale, hello portale di Azure.

toolearn ulteriori informazioni su software come un servizio (SaaS) integrazione dell'applicazione con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

tooset l'integrazione di Azure AD con SAP Business oggetto Cloud, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di SAP Business Object Cloud, con l'accesso Single Sign-On attivato

> [!NOTE]
> Se si passi hello in questa esercitazione, si consiglia di non testare loro in un ambiente di produzione.

Indicazioni per il test passaggi hello in questa esercitazione:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione gratuita di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. 

scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiungere SAP Business oggetto Cloud dalla raccolta di hello.
2. Configurare e testare l'accesso Single Sign-On di Azure AD.

## <a name="add-sap-business-object-cloud-from-hello-gallery"></a>Aggiungere SAP Business oggetto Cloud dalla raccolta di hello
tooset l'integrazione di hello di SAP Business oggetto Cloud con Azure AD, nella raccolta di hello, aggiungere l'elenco tooyour SAP Business oggetto Cloud di App SaaS gestite.

tooadd SAP Business oggetto Cloud dalla raccolta hello:

1. In hello [portale di Azure](https://portal.azure.com)in hello menu a sinistra, selezionare **Azure Active Directory**. 

    ![pulsante di Hello Azure Active Directory][1]

2. Selezionare **Applicazioni aziendali** e quindi selezionare **Tutte le applicazioni**.

    ![pagina applicazioni di Enterprise Hello][2]
    
3. Selezionare una nuova applicazione, tooadd **nuova applicazione**.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, immettere **SAP Business oggetto Cloud**.

    ![casella di ricerca Hello](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. Nel riquadro dei risultati hello, selezionare **SAP Business oggetto Cloud**, quindi selezionare **Aggiungi**.

    ![SAP Business oggetto Cloud nell'elenco risultati hello](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SAP Business Object Cloud con un utente di test di nome *Britta Simon*.

Per toowork di accesso singolo, Azure AD deve tooknow hello Azure controparte utente di Active Directory nel Cloud di oggetto SAP Business. È necessario stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello nel Cloud di oggetto SAP Business.

hello tooestablish collegamento relazione, nel Cloud di oggetto Business di SAP, per **Username**, assegnare il valore di hello di hello **nome utente** in Azure AD.

tooconfigure e prova AD Azure single sign-on con SAP Business oggetto Cloud, hello completo seguenti attività:

1. [Configurare l'accesso Single Sign-On di Azure AD](#set-up-azure-ad-single-sign-on). Imposta un toouse utente questa funzionalità.
2. [Creare un utente test di Azure AD](#create-an-azure-ad-test-user). Test AD Azure single sign-on con utente hello Britta Simon.
3. [Creare un utente di test di SAP Business Object Cloud](#create-an-sap-business-object-cloud-test-user). Crea un equivalente di Britta Simon in SAP Business oggetto Cloud toohello collegato rappresentazione in forma di Azure AD dell'utente hello.
4. [Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user). Imposta Britta Simon toouse AD Azure single sign-on.
5. [Testare l'accesso Single Sign-On](#test-single-sign-on). Verifica che la configurazione di hello funziona.

### <a name="set-up-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione accendere singola AD Azure sign-on in hello portale di Azure. quindi si configura Single Sign-On nell'applicazione SAP Business Object Cloud.

tooset di Azure AD single sign-on con SAP Business oggetto Cloud:

1. Nel portale di Azure su hello hello **SAP Business oggetto Cloud** pagina di integrazione dell'applicazione, seleziona **Single sign-on**.

    ![Selezionare Single Sign-On][4]

2. In hello **Single sign-on** pagina per **modalità**selezionare **basato su SAML Sign-on**.
 
    ![Selezionare Accesso basato su SAML](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. In **SAP Business oggetto Cloud dominio e gli URL**completa hello i passaggi seguenti:

    1. In hello **Sign-on URL** , immettere un URL con hello seguente motivo: 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. In hello **identificatore** , immettere un URL con hello seguente motivo:
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![URL della pagina SAP Business Object Cloud Domain and URLs (URL e dominio SAP Business Object Cloud)](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > i valori Hello in questi URL sono solo a scopo dimostrativo. Aggiornare i valori hello con hello effettivo sign-on URL URL e l'identificatore. tooget hello URL sign-on, hello contatto [team di supporto SAP Business oggetto Cloud Client](https://www.sap.com/product/analytics/cloud-analytics.support.html). È possibile ottenere l'URL dell'identificatore hello scaricando i metadati di SAP Business oggetto Cloud hello dalla console di amministrazione di hello. Ciò è illustrato più avanti nell'esercitazione di hello. 

4. In **Certificato di firma SAML** selezionare **XML metadati**, Quindi, salvare il file di metadati hello nel computer in uso.

    ![Selezionare XML metadati](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. Selezionare **Salva**.

    ![Selezionare Salva](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. In una finestra del web browser, accedere come amministratore nel sito della società di SAP Business oggetto Cloud tooyour.

7. Selezionare **Menu** > **Sistema** > **Amministrazione**.
    
    ![Selezionare Menu, quindi Sistema e infine Amministrazione](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. In hello **sicurezza** scheda, seleziona hello **modifica** icona (penna).
    
    ![Nella scheda sicurezza hello, selezionare l'icona di modifica di hello](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. Per **Metodo di autenticazione** selezionare **SAML Single Sign-On (SSO)**.

    ![Selezionare SAML Single Sign-On per il metodo di autenticazione hello](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. toodownload hello provider i metadati del servizio (passaggio 1), selezionare **scaricare**. Nel file di metadati hello, trovare e copiare hello **entityID** valore. In hello Azure portale, in **SAP Business oggetto Cloud dominio e gli URL**, incollare il valore di hello in hello **identificatore** casella.

    ![Copiare e incollare il valore di entityID hello](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. tooupload hello metadati del servizio provider (passaggio 2) nel file hello scaricato da hello portale di Azure in **i metadati del Provider di identità caricare**selezionare **caricare**.  

    ![In Upload Identity Provider metadata (Caricare i metadati del provider di identità) selezionare Carica](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. In hello **attributo utente** elencare, attributo utente di selezionare hello (passaggio 3) che si desidera toouse per l'implementazione. Questo attributo utente esegue il mapping toohello provider di identità. un attributo personalizzato nella pagina dell'utente hello, utilizzare hello tooenter **Mapping SAML personalizzate** opzione. In alternativa, è possibile selezionare **posta elettronica** o **ID utente** come attributo utente hello. In questo esempio, è selezionato **posta elettronica** perché è stato eseguito il mapping di attestazione dell'identificatore utente hello con hello **userprincipalname** attributo hello **gli attributi utente** sezione hello Portale di Azure. Ciò fornisce un messaggio di posta elettronica utente univoco, che viene inviata toohello applicazione SAP Business oggetto Cloud a ogni risposta SAML corretta.

    ![Selezionare Attributo utente](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. account di hello tooverify con il provider di identità hello (passaggio 4), in hello **credenziali di account di accesso (posta elettronica)** , immettere l'indirizzo di posta elettronica dell'utente hello. Selezionare quindi **Verifica account**. sistema Hello aggiunge l'account utente toohello di credenziali di accesso.

    ![Immettere l'indirizzo di posta elettronica e selezionare Verifica account](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. Seleziona hello **salvare** icona.

    ![Icona Salva](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> È possibile leggere una versione di queste istruzioni in hello concisa [portale di Azure](https://portal.azure.com), mentre si configura l'app. Dopo aver aggiunto l'applicazione hello selezionando **Active Directory** > **applicazioni aziendali**selezionare hello **Single Sign-On** scheda. È possibile accedere alla documentazione di hello incorporato in hello **configurazione** alla sezione, hello parte inferiore della pagina hello. Per altre informazioni, vedere la [documentazione incorporata su Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
In questa sezione si crea un utente di test denominato Britta Simon in hello portale di Azure.

toocreate un utente di prova in Azure AD:

1. Nel portale di Azure, nel menu a sinistra di hello, hello selezionare **Azure Active Directory**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, selezionare **utenti e gruppi**, quindi selezionare **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** nella finestra di dialogo **Aggiungi**.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. In hello **utente** della finestra di dialogo hello completo alla procedura seguente:
 
    1. In hello **nome** immettere **BrittaSimon**.

    2. In hello **nome utente** , immettere l'indirizzo di posta elettronica hello dell'utente hello Britta Simon.

    3. Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.

    4. Selezionare **Crea**.

        ![finestra di dialogo utente Hello](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Creare un utente di Azure AD][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a>Creare un utente di test di SAP Business Object Cloud

Agli utenti di Azure AD devono essere eseguiti nel Cloud di oggetto SAP Business prima che possano accedere in tooSAP Cloud oggetto Business. In SAP Business Object Cloud il provisioning è un'attività manuale.

tooprovision un account utente:

1. Accedi tooyour sito della società SAP Business oggetto Cloud come amministratore.

2. Selezionare **Menu** > **Security** (Sicurezza)  > **Users** (Utenti).

    ![Aggiungere un dipendente](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. In hello **utenti** tooadd nuovi dettagli dell'utente, selezionare  **+** . 

    ![Pagina Aggiungi utenti (Aggiungi utenti)](./media/active-directory-saas-sapboc-tutorial/user4.png)

    Completare quindi hello alla procedura seguente:

    1. In hello **ID utente** immettere hello l'ID dell'utente di hello, ad esempio **Laura**.

    2. In hello **nome** immettere come nome dell'utente di hello, hello **Laura**.

    3. In hello **cognome** immettere hello cognome di hello utente, ad esempio **Simon**.

    4. In hello **nome visualizzato** casella, immettere hello nome completo dell'utente di hello, ad esempio **Britta Simon**.

    5. In hello **posta elettronica** immettere indirizzo di posta elettronica hello dell'utente di hello, ad esempio  **brittasimon@contoso.com** .

    6. In hello **Selezione ruoli** pagina, selezionare hello ruolo appropriato per l'utente hello e quindi selezionare **OK**.

      ![Selezionare il ruolo](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. Seleziona hello **salvare** icona.  


### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione utente hello Britta Simon toouse AD Azure single sign-on tramite la concessione di hello utente account accesso tooSAP Cloud oggetto Business.

tooassign Britta Simon tooSAP Cloud oggetto Business:

1. Nel portale di Azure hello, aprire visualizzazione applicazioni hello e fare clic sulla visualizzazione directory toohello. Selezionare **Applicazioni aziendali** e quindi selezionare **Tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **SAP Business oggetto Cloud**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. Nel menu a sinistra di hello, selezionare **utenti e gruppi**.

    ![Selezionare Utenti e gruppi][202] 

4. Selezionare **Aggiungi**. Quindi, nella hello **Aggiungi** selezionare **utenti e gruppi**.

    ![pagina Aggiungi Hello][203]

5. In hello **utenti e gruppi** hello elenco di utenti, selezionare pagina **Britta Simon**.

6. In hello **utenti e gruppi** selezionare **selezionare**.

7. In hello **Aggiungi** selezionare **assegnare**.

![Assegnazione del ruolo utente hello][200] 
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando il pannello di accesso di hello.

Quando si seleziona il riquadro di SAP Business oggetto Cloud hello nel Pannello di accesso hello, è necessario essere connessi automaticamente tooyour applicazione SAP Business oggetto Cloud.

Per ulteriori informazioni sul pannello di accesso hello, vedere [Pannello di accesso di introduzione toohello](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sull'App SaaS toointegrate con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

