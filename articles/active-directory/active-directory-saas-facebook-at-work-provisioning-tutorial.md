---
title: 'Esercitazione: Configurare Workplace by Facebook per il provisioning degli utenti | Microsoft Docs'
description: Informazioni su come degli account utente di effettuare il provisioning e la prestazione tooautomatically da Azure AD tooWorkplace da Facebook.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33d294dbc8f441b29138408b3c9ca41f2141f8af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a>Esercitazione: Configurare Workplace by Facebook per il provisioning degli utenti

Questa esercitazione si hello tooautomatically necessari passaggi è illustrato il provisioning e deprovisioning degli account utente da Azure Active Directory (Azure AD) tooWorkplace da Facebook.

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con area di lavoro da Facebook tooconfigure, è necessario seguente hello:

- Sottoscrizione di Azure AD.
- Una sottoscrizione a Workplace by Facebook abilitata per l'accesso Single Sign-On (SSO)

passaggi di hello tootest in questa esercitazione, seguire queste indicazioni:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di valutazione di Azure AD, è possibile ricevere un'[offerta di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="assign-users-tooworkplace-by-facebook"></a>Assegnare gli utenti tooWorkplace da Facebook

Azure AD Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso. Nel contesto di hello di provisioning dell'account utente automatico, vengono sincronizzati solo gli utenti di hello e i gruppi che sono stati assegnati tooan applicazione in Azure AD.

Prima configurazione o abilitazione del provisioning del servizio, hello decidere quali utenti e gruppi in Azure Active Directory rappresentano utenti hello bisogno di accesso tooyour all'area di lavoro da app Facebook. È quindi possibile assegnare questi utenti tooyour all'area di lavoro, da app Facebook seguendo hello istruzioni [assegnare un'applicazione aziendale tooan utente o gruppo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).

>[!IMPORTANT]
>*   Hello test configurazione di provisioning mediante l'assegnazione di un singolo tooWorkplace utente Azure AD da Facebook. Assegnare utenti e gruppi aggiuntivi in un secondo momento.
>*   Quando si assegna un utente tooWorkplace da Facebook, è necessario selezionare un ruolo utente valido. ruolo di accesso predefinito Hello non funziona per il provisioning.

## <a name="enable-automated-user-provisioning"></a>Abilitare il provisioning utenti automatico

In questa sezione descrive la connessione AD Azure toohello account utente provisioning API dell'area di lavoro da Facebook. Verrà inoltre descritto come tooconfigure hello provisioning servizio toocreate, aggiornare e disabilitare gli account utente assegnato nell'area di lavoro da Facebook. Questo è basato sull'assegnazione di utenti e gruppi in Azure AD.

>[!Tip]
>È anche possibile scegliere tooenabled basato su SAML SSO per l'area di lavoro da Facebook, da seguendo le istruzioni di hello cui hello [portale di Azure](https://portal.azure.com). L'accesso SSO può essere configurato indipendentemente dal provisioning automatico, anche se queste due funzionalità sono complementari.

### <a name="configure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a>Configurare l'account utente di provisioning tooWorkplace da Facebook in Azure AD

Azure supporta AD hello possibilità tooautomatically sincronizzare i dettagli dell'account di hello assegnato tooWorkplace utenti da Facebook. La sincronizzazione automatica consente all'area di lavoro da dati di Facebook hello tooget tooauthorize utenti per l'accesso, è necessario prima di usarle il tentativo di toosign in hello per la prima volta. Esegue anche il deprovisioning degli utenti da Workplace by Facebook una volta che l'accesso viene revocato in Azure AD.

1. In hello [portale di Azure](https://portal.azure.com)selezionare **Azure Active Directory** > **le app aziendali** > **tutte le applicazioni**.

2. Se è già stato configurato all'area di lavoro da Facebook per SSO, cercare l'istanza di una rete aziendale da Facebook tramite il campo di ricerca hello. In caso contrario, selezionare **Aggiungi** e cercare **all'area di lavoro da Facebook** nella raccolta di applicazione hello. Selezionare **all'area di lavoro da Facebook** da hello risultati di ricerca e aggiungerlo tooyour elenco delle applicazioni.

3. Selezionare l'istanza di una rete aziendale da Facebook, quindi hello **Provisioning** scheda.

4. Impostare **modalità di Provisioning** troppo**automatica**. 

    ![Screenshot delle opzioni di provisioning di Workplace by Facebook](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. In hello **credenziali di amministratore** immettere hello **segreto Token** hello e **URL Tenant** dell'area di lavoro dall'amministratore di Facebook.

6. Nel portale di Azure hello, selezionare **Test connessione** tooensure Azure AD può connettersi tooyour all'area di lavoro da app Facebook. Se la connessione hello non riesce, verificare che l'area di lavoro dall'account Facebook disponga delle autorizzazioni di amministratore di Team.

7. Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e selezionare la casella di controllo hello.

8. Selezionare **Salva**.

9. Nella sezione mapping hello, selezionare **tooWorkplace sincronizzare Active Directory gli utenti di Azure da Facebook**.

10. In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da Azure AD tooWorkplace da Facebook. gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello account utente nell'area di lavoro da Facebook per operazioni di aggiornamento. Selezionare tutte le modifiche, toocommit **salvare**.

11. tooenable hello servizio provisioning di Azure AD per l'area di lavoro da Facebook, in hello **impostazioni** modificare hello **lo stato di Provisioning** troppo**su**.

12. Selezionare **Salva**.

Per ulteriori informazioni su come il provisioning, vedere tooconfigure automatico [hello Facebook documentazione](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).

È ora possibile creare un account di test. Attendere che i minuti too20 tooverify che hello account è stato sincronizzato tooWorkplace da Facebook.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Gestione del provisioning degli account utente per le app aziendali](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Configurare l'accesso Single Sign-On](active-directory-saas-facebook-at-work-tutorial.md)

