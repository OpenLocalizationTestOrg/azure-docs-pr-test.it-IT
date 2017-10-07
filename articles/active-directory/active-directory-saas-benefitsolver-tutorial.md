---
title: 'Esercitazione: Integrazione di Azure Active Directory con Benefitsolver | Microsoft Docs'
description: Informazioni su come toouse Benefitsolver con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 5bb8511ef9be1e386956188a93e899d6ebe56ed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a>Esercitazione: Integrazione di Azure Active Directory con Benefitsolver
obiettivo di Hello di questa esercitazione è l'integrazione di hello tooshow di Azure e Benefitsolver.  

scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

* Sottoscrizione di Azure valida
* Sottoscrizione di Benefitsolver abilitata per l'accesso Single Sign-On (SSO)

Dopo aver completato questa esercitazione, gli utenti di hello Azure AD assegnati tooBenefitsolver saranno in grado di toosingle sign in un'applicazione hello utilizzando hello [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

scenario di Hello descritto in questa esercitazione è costituito da hello seguenti blocchi predefiniti:

1. Abilitare l'integrazione dell'applicazione hello per Benefitsolver
2. Configurazione dell'accesso Single Sign-On (SSO)
3. Configurazione del provisioning utente
4. Assegnazione degli utenti

![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")

## <a name="enabling-hello-application-integration-for-benefitsolver"></a>Abilitare l'integrazione dell'applicazione hello per Benefitsolver
obiettivo di Hello di questa sezione è toooutline come integrazione dell'applicazione hello tooenable per Benefitsolver.

### <a name="tooenable-hello-application-integration-for-benefitsolver-perform-hello-following-steps"></a>integrazione dell'applicazione hello tooenable per Benefitsolver, eseguire hello alla procedura seguente:
1. Nel portale di Azure classico, nel riquadro di spostamento sinistro hello hello fare clic su **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")
2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.
3. visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
   ![Applicazioni](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applicazioni")
4. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.
   
   ![Aggiungere un'applicazione](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Aggiungere un'applicazione")
5. In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.
   
   ![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")
6. In hello **casella di ricerca**, tipo **Benefitsolver**.
   
   ![Raccolta di applicazioni](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Raccolta di applicazioni")
7. Nel riquadro risultati hello selezionare **Benefitsolver**, quindi fare clic su **completa** tooadd un'applicazione hello.
   
   ![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")
   
## <a name="configure-single-sign-on"></a>Configura accesso Single Sign-On

obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooBenefitsolver con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.  

L'applicazione Benefitsolver prevede asserzioni SAML hello in un formato specifico, che richiede il tooyour mapping di attributi personalizzati tooadd **attributi token saml** configurazione. 

Hello seguente schermata mostra un esempio per questo oggetto.

![Attributi](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributi")

**tooconfigure accesso single sign-on, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico, in hello hello **Benefitsolver** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configurare l'accesso Single Sign-On")
2. In hello **come si sarebbe ad esempio utenti toosign su tooBenefitsolver** selezionare **Microsoft Azure AD Single Sign-On**e quindi fare clic su **Avanti**.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configurare l'accesso Single Sign-On")
3. In hello **Configura impostazioni App** eseguire hello alla procedura seguente:
   
   ![Configurare le impostazioni dell'app](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configurare le impostazioni dell'app")
   
   1. In hello **URL di accesso** casella tipo **http://azure.benefitsolver.com**.
   2. In hello **URL di risposta** casella tipo **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.  
   3. Fare clic su **Avanti**.
4. In hello **configurare single sign-on a Benefitsolver** pagina, toodownload i metadati, fare clic su **Scarica metadati**e quindi salvare il file di metadati hello in locale nel computer.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configurare l'accesso Single Sign-On")
5. Il team di supporto Benefitsolver hello scaricato metadati file tooyour di trasmissione.
   
   >[!NOTE]
   >Il team di supporto Benefitsolver dispone di configurazione di SSO toodo hello effettivo. Una volta completata l'abilitazione dell'accesso Single Sign-On per la sottoscrizione, si riceverà una notifica.
   >

6. Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa** tooclose hello **configurare Single Sign-On** finestra di dialogo.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configurare l'accesso Single Sign-On")
7. Scegliere dal menu hello in primo piano hello **attributi** tooopen hello **attributi Token SAML** finestra di dialogo.
   
   ![Attributi](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributi")
8. mapping di attributi tooadd hello necessario, eseguire hello alla procedura seguente:
   
   ![Attributi](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributi")
   
   | Nome attributo | Valore attributo |
   | --- | --- |
   | ClientID |È necessario tooget questo valore dal team di supporto Benefitsolver. |
   | ClientKey |È necessario tooget questo valore dal team di supporto Benefitsolver. |
   | LogoutURL |È necessario tooget questo valore dal team di supporto Benefitsolver. |
   | EmployeeID |È necessario tooget questo valore dal team di supporto Benefitsolver. |
   
   1. Per ogni riga di dati della tabella hello precedente, fare clic su **Aggiungi attributo utente**.
   2. In hello **nome dell'attributo** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.
   3. In hello **valore dell'attributo** casella di testo, il valore di attributo hello selezionare mostrato per la riga.
   4. Fare clic su **Complete**.
9. Fare clic su **Applica modifiche**.

## <a name="configure-user-provisioning"></a>Configura provisioning utenti
In ordine tooenable Azure AD utenti toolog in Benefitsolver, è necessario eseguirne il provisioning in Benefitsolver.  

Nel caso di hello di Benefitsolver, i dati dei dipendenti sono nell'applicazione compilata tramite un file di censimento dal sistema HRIS (in genere durante la notte).  

>[!NOTE]
>È possibile usare qualsiasi altro Benefitsolver utente account strumento di creazione o le API fornite da Benefitsolver tooprovision account utente di AAD. 
> 

## <a name="assigning-users"></a>Assegnazione degli utenti
tootest della configurazione, è necessario toogrant hello Azure AD utenti tooallow utilizzando il tooit di accesso dell'applicazione tramite l'assegnazione.

### <a name="tooassign-users-toobenefitsolver-perform-hello-following-steps"></a>tooassign tooBenefitsolver di utenti, eseguire hello alla procedura seguente:
1. Nel portale di Azure classico hello, creare un account di prova.
2. In hello * * Benefitsolver * * pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.
   
   ![Assegnare utenti](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assegnare utenti")
3. Selezionare l'utente test, fare clic su **assegnare**, quindi fare clic su **Sì** tooconfirm l'assegnazione.
   
   ![Sì](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Sì")

Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello. Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

