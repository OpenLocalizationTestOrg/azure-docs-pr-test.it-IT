---
title: 'Esercitazione: Integrazione di Azure Active Directory con Workplace by Facebook | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e all'area di lavoro da Facebook.
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
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 551ec353a5ec1da936373587688c299a6f4acca7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a>Esercitazione: Configurazione di Workplace by Facebook per il Provisioning utenti

obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform nell'area di lavoro da Facebook e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooWorkplace da Facebook.

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con area di lavoro da Facebook tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Una sottoscrizione di Workplace by Facebook abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="assigning-users-tooworkplace-by-facebook"></a>L'assegnazione di utenti tooWorkplace da Facebook

Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso. Nel contesto di hello di provisioning dell'account utente automatico, solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD è sincronizzato.

Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano utenti hello bisogno di accesso tooyour all'area di lavoro da app Facebook. Una volta deciso, è possibile assegnare questi utenti tooyour all'area di lavoro, da app Facebook seguendo le istruzioni di hello qui:

[Assegnare un'applicazione aziendale tooan utente o gruppo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooworkplace-by-facebook"></a>Suggerimenti importanti per l'assegnazione di utenti tooWorkplace da Facebook

*   È consigliabile che un singolo utente di Azure Active Directory assegnato da Facebook tootest hello configurazione provisioning tooWorkplace. È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.

*   Quando si assegna un utente tooWorkplace da Facebook, è necessario selezionare un ruolo utente valido. ruolo di "accesso predefinita" Hello non funziona per il provisioning.

## <a name="enable-user-provisioning"></a>Abilitare il provisioning utenti

Questa sezione viene illustrato come tramite connessione il tooWorkplace di Azure AD tramite API di provisioning dell'account utente Facebook e hello provisioning toocreate servizio di configurazione, aggiornare e disabilitare gli account utente assegnato nell'area di lavoro da Facebook in base a utenti e gruppi assegnazione di Azure AD.

>[!Tip]
>È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per l'area di lavoro da Facebook, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com). L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.

### <a name="tooconfigure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a>account utente tooconfigure provisioning tooWorkplace da Facebook in Azure AD:

obiettivo di Hello di questa sezione è toooutline tooenable provisioning dell'utente di Active Directory come account di tooWorkplace da Facebook.

Azure supporta AD hello possibilità tooautomatically sincronizzare i dettagli dell'account di hello assegnato tooWorkplace utenti da Facebook. La sincronizzazione automatica consente all'area di lavoro da dati di Facebook hello tooget tooauthorize utenti per l'accesso, è necessario prima di usarle il tentativo di toosign in hello per la prima volta. Esegue anche il deprovisioning degli utenti da Workplace by Facebook una volta che l'accesso viene revocato in Azure AD.

1. In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory** > **le app aziendali** > **tutteleapplicazioni** sezione.

2. Se è già stato configurato all'area di lavoro da Facebook per single sign-on, eseguire la ricerca per l'istanza di una rete aziendale da Facebook tramite il campo di ricerca hello. In caso contrario, selezionare **Aggiungi** e cercare **all'area di lavoro da Facebook** nella raccolta di applicazione hello. Selezionare l'area di lavoro da Facebook dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.

3. Selezionare l'istanza di una rete aziendale da Facebook, quindi selezionare hello **Provisioning** scheda.

4. Set hello **modalità di Provisioning** troppo**automatica**. 

    ![provisioning](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. In hello **credenziali di amministratore** sezione, immettere il Token segreto hello e hello URL Tenant dell'area di lavoro dall'amministratore di Facebook.

6. Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour all'area di lavoro da app Facebook. Se hello connessione non riesce, verificare il che area di lavoro dall'account di Facebook con autorizzazioni di amministratore di Team.

7. Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e casella di controllo hello.

8. Fare clic su **Salva**.

9. Nella sezione mapping hello, selezionare **tooWorkplace sincronizzare Active Directory gli utenti di Azure da Facebook.**

10. In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da Azure AD tooWorkplace da Facebook. gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello account utente nell'area di lavoro da Facebook per operazioni di aggiornamento. Selezionare hello Salva pulsante toocommit tutte le modifiche.

11. tooenable hello servizio provisioning di Azure AD per l'area di lavoro da Facebook, hello modifica **lo stato di Provisioning** troppo**su** in hello **impostazioni** sezione

12. Fare clic su **Salva**.

Per ulteriori informazioni su come il provisioning, vedere tooconfigure automatico [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)

È ora possibile creare un account di test. Attendere che i minuti too20 tooverify che hello account è stato sincronizzato tooWorkplace da Facebook.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Gestione del provisioning degli account utente per app aziendali](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Configurare l'accesso Single Sign-On](active-directory-saas-workplacebyfacebook-tutorial.md)

