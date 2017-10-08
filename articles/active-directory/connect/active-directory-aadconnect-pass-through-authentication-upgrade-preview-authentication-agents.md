---
title: 'Azure AD Connect: Autenticazione pass-through -Aggiornare gli agenti di autenticazione di anteprima | Microsoft Docs'
description: Questo articolo viene descritto come tooupgrade la configurazione di autenticazione pass-through di Azure Active Directory (Azure AD).
services: active-directory
keywords: Autenticazione pass-through di Azure AD Connect, installare Active Directory, componenti necessari per Azure AD, SSO, Single Sign-On
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 1695326b182278944e9f1584da72b18862b6ef27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-upgrade-preview-authentication-agents"></a>Autenticazione pass-through di Azure Active Directory - Aggiornare gli agenti di autenticazione di anteprima

## <a name="overview"></a>Panoramica

Questo articolo è destinato ai clienti che usano l'autenticazione pass-through di Azure AD tramite l'anteprima. Abbiamo recentemente aggiornato (e ridenominata) hello software dell'agente di autenticazione. È necessario too_manually_ aggiornamento anteprima autenticazione agenti installati nei server locali. L'aggiornamento manuale è un'azione da eseguire una sola volta. Tutti i futuri aggiornamenti tooAuthentication gli agenti sono automatici. Hello motivi tooupgrade sono i seguenti:

- versioni di anteprima Hello degli agenti di autenticazione non riceverà qualsiasi ulteriore sicurezza o correzioni di bug.
-   versioni di anteprima Hello degli agenti di autenticazione non possono essere installate su server aggiuntivi per la disponibilità elevata.

## <a name="check-versions-of-your-authentication-agents"></a>Controllare le versioni degli agenti autenticazione

### <a name="step-1-check-where-your-authentication-agents-are-installed"></a>Passaggio 1: Controllare se gli agenti di autenticazione sono installati

Seguire questi passaggi toocheck in cui sono installati gli agenti di autenticazione:

1. Accedi toohello [centro di amministrazione di Azure Active Directory](https://aad.portal.azure.com) con credenziali di amministratore globale di hello per il tenant.
2. Selezionare **Azure Active Directory** nella navigazione a sinistra di hello.
3. Selezionare **Azure AD Connect**. 
4. Selezionare **Autenticazione pass-through**. Questo pannello sono elencati i server di hello in cui sono installati gli agenti di autenticazione.

![Interfaccia di amministrazione di Azure Active Directory - Pannello Autenticazione pass-through](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

### <a name="step-2-check-hello-versions-of-your-authentication-agents"></a>Passaggio 2: Controllo delle versioni di hello di agenti di autenticazione

versioni di hello toocheck degli agenti, l'autenticazione in ogni server identificato nel precedente passaggio hello seguono queste istruzioni:

1. Andare troppo**Pannello di controllo -> programmi -> programmi e funzionalità** nel server locale hello.
2. Se è presente una voce per "**agente autenticazione di Microsoft Azure AD Connect**", è necessario tootake qualsiasi azione su questo server.
3. Se è presente una voce per "**connettore Proxy dell'applicazione di Microsoft Azure AD**", le versioni 1.5.132.0 o versioni precedenti, è necessario toomanually aggiornamento nel server.

![Versione di anteprima dell'agente di autenticazione](./media/active-directory-aadconnect-pass-through-authentication/pta6.png)

## <a name="best-practices-toofollow-before-starting-hello-upgrade"></a>Procedure consigliate toofollow prima di avviare l'aggiornamento di hello

Prima dell'aggiornamento, assicurarsi di aver hello elementi sul posto:

1. **Creare account di amministratore globale solo cloud**: non effettua l'aggiornamento senza un toouse account amministratore globale solo cloud in situazioni di emergenza in cui gli agenti di autenticazione pass-through non funzionino correttamente. Informazioni su come [aggiungere un account amministratore globale di tipo solo cloud](../active-directory-users-create-azure-portal.md). L'esecuzione di questo passaggio è fondamentale ed evita di rimanere bloccati fuori dal tenant.
2.  **Verificare la disponibilità elevata**: se non è stata completata in precedenza, installare una seconda autonoma agente Authentication tooprovide la disponibilità elevata per le richieste di accesso, utilizzo di queste [istruzioni](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability).

## <a name="upgrading-hello-authentication-agent-on-your-azure-ad-connect-server"></a>L'aggiornamento di hello agente di autenticazione nel server di Azure AD Connect

È necessario aggiornare Azure AD Connect prima di aggiornare hello agente di autenticazione in hello nello stesso server. Eseguire la procedura seguente nei server primario e di gestione temporanea di Azure AD Connect:

1. **L'aggiornamento di Azure AD Connect**: seguire questo [articolo](./active-directory-aadconnect-upgrade-previous-version.md) e toohello più recente Azure AD Connect versione di aggiornamento.
2. **Disinstallare la versione di anteprima hello di hello agente Authentication**: scaricare [questo script di PowerShell](https://aka.ms/rmpreviewagent) ed eseguirlo come amministratore nel server di hello.
3. **Scaricare hello la versione più recente dell'agente di autenticazione hello (versioni 1.5.193.0 o versione successiva)**: Accedi toohello [centro di amministrazione di Azure Active Directory](https://aad.portal.azure.com) con credenziali di amministratore globale del tenant. Selezionare **Azure Active Directory -> Azure AD Connect -> Autenticazione pass-through -> Scarica agente**. Accettare le condizioni di hello del servizio e scaricare hello la versione più recente dell'agente di autenticazione hello.
4. **Installare hello la versione più recente dell'agente di autenticazione hello**: hello esecuzione eseguibile scaricato nel passaggio 3. Fornire le credenziali di amministratore globale del tenant quando viene richiesto.
5. **Verificare che sia stata installata la versione più recente hello**: come illustrato in precedenza, andare troppo**Pannello di controllo -> programmi -> programmi e funzionalità** e verificare che sia presente una voce per "**Microsoft Azure AD Connect Agente di autenticazione**".

>[!NOTE]
>Se si seleziona il pannello autenticazione pass-through hello in hello [centro di amministrazione di Azure Active Directory](https://aad.portal.azure.com) dopo aver completato i passaggi precedenti, hello, si noterà due voci di agente di autenticazione per ogni server - una voce di visualizzazione hello Agente di autenticazione come **Active** e hello altro **inattivo**. Questo è il comportamento _previsto_. Hello **inattivo** voce viene eliminata automaticamente dopo alcuni giorni.

## <a name="upgrading-hello-authentication-agent-on-other-servers"></a>L'aggiornamento di hello agente di autenticazione su altri server

Seguire questi tooupgrade passaggi autenticazione agenti su altri server (in cui Azure AD Connect non è installato):

1. **Disinstallare la versione di anteprima hello di hello agente Authentication**: scaricare [questo script di PowerShell](https://aka.ms/rmpreviewagent) ed eseguirlo come amministratore nel server di hello.
2. **Scaricare hello la versione più recente dell'agente di autenticazione hello (versioni 1.5.193.0 o versione successiva)**: Accedi toohello [centro di amministrazione di Azure Active Directory](https://aad.portal.azure.com) con credenziali di amministratore globale del tenant. Selezionare **Azure Active Directory -> Azure AD Connect -> Autenticazione pass-through -> Scarica agente**. Accettare le condizioni di hello del servizio e scaricare la versione più recente di hello.
3. **Installare hello la versione più recente dell'agente di autenticazione hello**: hello esecuzione eseguibile scaricato nel passaggio 2. Fornire le credenziali di amministratore globale del tenant quando viene richiesto.
4. **Verificare che sia stata installata la versione più recente hello**: come illustrato in precedenza, andare troppo**Pannello di controllo -> programmi -> programmi e funzionalità** e verificare che sia presente una voce denominata **Microsoft Azure AD Connect Agente di autenticazione**.

>[!NOTE]
>Se si seleziona il pannello autenticazione pass-through hello in hello [centro di amministrazione di Azure Active Directory](https://aad.portal.azure.com) dopo aver completato i passaggi precedenti, hello, si noterà due voci di agente di autenticazione per ogni server - una voce di visualizzazione hello Agente di autenticazione come **Active** e hello altro **inattivo**. Questo è il comportamento _previsto_. Hello **inattivo** voce viene eliminata automaticamente dopo alcuni giorni.

## <a name="next-steps"></a>Passaggi successivi
- [**Risoluzione dei problemi** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -informazioni su come le problematiche comuni tooresolve con funzionalità hello.
