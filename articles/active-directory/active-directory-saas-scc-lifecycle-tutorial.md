---
title: 'Esercitazione: Integrazione di Azure Active Directory con SCC LifeCycle | Microsoft Docs'
description: Informazioni su come toouse ciclo di vita SCC con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a>Esercitazione: Integrazione di Azure Active Directory con SCC LifeCycle
obiettivo di Hello di questa esercitazione è l'integrazione di hello tooshow di Azure e ciclo di vita SCC.  

scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

* Sottoscrizione di Azure valida
* Sottoscrizione di SCC LifeCycle abilitata per l'accesso Single Sign-On (SSO)

Dopo aver completato questa esercitazione, hello Azure AD utenti assegnati tooSCC ciclo di vita sarà toosingle in grado di accesso in un'applicazione hello nel sito della società ciclo di vita SCC (accesso avviato dal provider di servizi su) o tramite hello [introduzione Pannello di accesso toohello](active-directory-saas-access-panel-introduction.md).

scenario di Hello descritto in questa esercitazione è costituito da hello seguenti blocchi predefiniti:

1. Abilitare l'integrazione dell'applicazione hello per ciclo di vita SCC
2. Configurazione dell'accesso Single Sign-On (SSO)
3. Configurazione del provisioning utente
4. Assegnazione degli utenti

![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a>Abilitare l'integrazione dell'applicazione hello per ciclo di vita SCC
obiettivo di Hello di questa sezione è toooutline come integrazione dell'applicazione hello tooenable per ciclo di vita SCC.

**integrazione dell'applicazione hello tooenable per ciclo di vita SCC, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico, nel riquadro di spostamento sinistro hello hello fare clic su **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")
2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.
3. visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
    ![Applicazioni](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applicazioni")
4. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.
   
    ![Aggiungere un'applicazione](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Aggiungere un'applicazione")
5. In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.
   
    ![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")
6. In hello **casella di ricerca**, tipo **ciclo di vita SCC**.
   
    ![Raccolta di applicazioni](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Raccolta di applicazioni")
7. Nel riquadro risultati hello selezionare **ciclo di vita SCC**, quindi fare clic su **completa** tooadd un'applicazione hello.
   
    ![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")
   
## <a name="configure-single-sign-on"></a>Configura accesso Single Sign-On

obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooSCC del ciclo di vita con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.

**tooconfigure accesso single sign-on, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico, in hello hello **ciclo di vita SCC** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** hello tooopen * * configurare Single Sign-On * * finestra di dialogo.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configurare l'accesso Single Sign-On")
2. In hello **come si sarebbe ad esempio utenti toosign nel ciclo di vita tooSCC** selezionare **Microsoft Azure AD Single Sign-On**e quindi fare clic su **Avanti**.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configurare l'accesso Single Sign-On")
3. In hello **Configura URL App** pagina hello **URL di accesso** casella di testo, hello digitare l'URL utilizzato dal toosign gli utenti in tooyour applicazione ciclo di vita SCC tramite hello modello "*https:// bs1.scc.com/lc7/Welcome/Customer/PICTtest.aspx*", quindi fare clic su **Avanti**.
   
    ![Configurare l'URL dell'app](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configurare l'URL dell'app")
4. In hello **configurare single sign-on in ciclo di vita SCC** pagina, fare clic su **Scarica metadati**e quindi salvare il file di metadati in locale nel computer.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configurare l'accesso Single Sign-On")
5. Inoltrare tale tooSCC di file di metadati del team di supporto del ciclo di vita.
   
   >[!NOTE]
   >Accesso Single sign-on è abilitata per il team di supporto di ciclo di vita SCC hello toobe.
   > 
   > 

6. Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa** tooclose hello **configurare Single Sign-On** finestra di dialogo.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configurare l'accesso Single Sign-On")
   
## <a name="configure-user-provisioning"></a>Configura provisioning utenti

In ordine tooenable Azure AD utenti toolog nel ciclo di vita SCC, è necessario eseguirne il provisioning in ciclo di vita SCC. Non sono presenti elementi di azione per si tooconfigure di provisioning dell'utente tooSCC del ciclo di vita.

Quando toolog di tentativi di un utente assegnato nel ciclo di vita SCC, viene creato un account di ciclo di vita SCC automaticamente se necessario.

>[!NOTE]
>È possibile usare qualsiasi altro ciclo di vita SCC utente account strumento di creazione o qualsiasi API fornita da ciclo di vita SCC tooprovision account utente di AAD.
> 
> 

## <a name="assign-users"></a>Assegna utenti
tootest della configurazione, è necessario toogrant hello Azure AD utenti tooallow utilizzando il tooit di accesso dell'applicazione tramite l'assegnazione.

**gli utenti di tooassign tooSCC ciclo di vita, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico hello, creare un account di prova.
2. In hello * * ciclo di vita SCC * * pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.
   
    ![Assegnare utenti](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assegnare utenti")
3. Selezionare l'utente test, fare clic su **assegnare**, quindi fare clic su **Sì** tooconfirm l'assegnazione.
   
    ![Sì](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Sì")

Se si desiderano tootest le impostazioni SSO, aprire Pannello di accesso hello. Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

