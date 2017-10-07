---
title: 'Esercitazione: Integrazione di Azure Active Directory con Qualtrics | Documentazione Microsoft'
description: Informazioni su come toouse Qualtrics con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 941642e74b90bb13a5ce37ce6665cfa32cd86016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a>Esercitazione: Integrazione di Azure Active Directory con Qualtrics
obiettivo di Hello di questa esercitazione è l'integrazione di hello tooshow di Azure e Qualtrics.  

scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

* Sottoscrizione di Azure valida
* Sottoscrizione di Qualtrics abilitata per l'accesso Single Sign-On (SSO)

Dopo aver completato questa esercitazione, gli utenti di hello Azure AD assegnati tooQualtrics saranno in grado di toosingle sign applicazione hello nel sito della società Qualtrics (accesso avviato dal provider di servizi su) o tramite hello [toohello introduzione Accedere al pannello](active-directory-saas-access-panel-introduction.md).

scenario di Hello descritto in questa esercitazione è costituito da hello seguenti blocchi predefiniti:

1. Abilitazione hello di integrazione dell'applicazione per Qualtrics
2. Configurazione dell'accesso Single Sign-On (SSO)
3. Configurazione del provisioning utente
4. Assegnazione degli utenti

![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")

## <a name="enabling-hello-application-integration-for-qualtrics"></a>Abilitazione hello di integrazione dell'applicazione per Qualtrics
obiettivo di Hello di questa sezione è toooutline come integrazione dell'applicazione per Qualtrics tooenable hello.

**integrazione dell'applicazione hello tooenable per Qualtrics, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico, nel riquadro di spostamento sinistro hello hello fare clic su **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")
2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.
3. visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
   ![Applicazioni](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applicazioni")
4. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.
   
   ![Aggiungere un'applicazione](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Aggiungere un'applicazione")
5. In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.
   
   ![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")
6. In hello **casella di ricerca**, tipo **Qualtrics**.
   
   ![Raccolta di applicazioni](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Raccolta di applicazioni")
7. Nel riquadro risultati hello selezionare **Qualtrics**, quindi fare clic su **completa** tooadd un'applicazione hello.
   
   ![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")
   
## <a name="configure-single-sign-on"></a>Configura accesso Single Sign-On

obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooQualtrics con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.

**tooconfigure accesso single sign-on, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico, in hello hello **Qualtrics** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configurare l'accesso Single Sign-On")
2. In hello **come si sarebbe ad esempio utenti toosign su tooQualtrics** selezionare **Microsoft Azure AD Single Sign-On**e quindi fare clic su **Avanti**.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configurare l'accesso Single Sign-On")
3. In hello **Configura URL App** hello della pagina **URL accesso Qualtrics** casella di testo, digitare l'URL (ad esempio: "*https://ssotest2ut1.qualtrics.com*"), quindi fare clic su **Avanti**.
   
   ![Configurare l'URL dell'app](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configurare l'URL dell'app")
4. In hello **Configura accesso single sign-on in Qualtrics** pagina, fare clic su **Scarica metadati**e quindi salvare il file di metadati hello nel computer in uso.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configurare l'accesso Single Sign-On")
5. Inviare hello metadati file toohello team di supporto di Qualtrics.
   
   >[!NOTE]
   >configurazione di SSO Hello è toobe eseguita dal team di supporto di Qualtrics hello. Si riceverà una notifica non appena la configurazione hello è stata completata.
   > 
   > 
6. Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa** tooclose hello **configurare Single Sign-On** finestra di dialogo.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configurare l'accesso Single Sign-On")
   
## <a name="configure-user-provisioning"></a>Configura provisioning utenti

Non sono presenti elementi di azione per si tooconfigure di provisioning dell'utente tooQualtrics. Quando un utente assegnato tenta toolog a Qualtrics mediante il pannello di accesso di hello, Qualtrics verifica se hello utente esiste.  

Se l’account utente non è disponibile, viene creato automaticamente da Qualtrics.

## <a name="assign-users"></a>Assegna utenti
tootest della configurazione, è necessario toogrant hello Azure AD utenti tooallow utilizzando il tooit di accesso dell'applicazione tramite l'assegnazione.

**tooassign tooQualtrics di utenti, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico hello, creare un account di prova.
2. In hello **Qualtrics** pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.
   
   ![Assegnare utenti](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assegnare utenti")
3. Selezionare l'utente test, fare clic su **assegnare**, quindi fare clic su **Sì** tooconfirm l'assegnazione.
   
   ![Sì](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Sì")

Se si desiderano tootest le impostazioni SSO, aprire Pannello di accesso hello. Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

