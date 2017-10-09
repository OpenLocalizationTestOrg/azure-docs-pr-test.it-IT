---
title: Autenticazione pass-through di Azure AD - Avvio rapido | Microsoft Docs
description: "Questo articolo descrive la modalità di avvio tooget con l'autenticazione pass-through di Azure Active Directory (Azure AD)."
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
ms.date: 08/23/2017
ms.author: billmath
ms.openlocfilehash: d6d0f85fe144cf36cc94676f6592d37988b20647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-quick-start"></a>Autenticazione pass-through di Azure Active Directory - Avvio rapido

## <a name="how-toodeploy-azure-ad-pass-through-authentication"></a>Come toodeploy autenticazione pass-through AD Azure

L'autenticazione pass-through di Azure Active Directory (Azure AD) consente il toosign agli utenti di tooboth in locale e applicazioni basate su cloud usando hello stesse password. L'accesso degli utenti avviene tramite la convalida delle password direttamente in Active Directory locale.

>[!IMPORTANT]
>L'autenticazione pass-through di Azure AD è attualmente in fase di anteprima. Se si utilizza questa funzionalità tramite l'anteprima, è necessario assicurarsi che l'aggiornamento di versioni di anteprima di hello autenticazione agenti utilizzando istruzioni hello fornite [qui](./active-directory-aadconnect-pass-through-authentication-upgrade-preview-authentication-agents.md).

È necessario toofollow questi toodeploy istruzioni autenticazione pass-through:

## <a name="step-1-check-prerequisites"></a>Passaggio 1: Verificare i prerequisiti

Verificare che hello seguenti prerequisiti siano soddisfatti:

### <a name="on-hello-azure-active-directory-admin-center"></a>Nel centro di amministrazione di hello Azure Active Directory

1. Creare un account Administrator globale solo cloud nel tenant di Azure AD. In questo modo, è possibile gestire la configurazione hello del tenant dei servizi locali errore o non sono più disponibili. Informazioni su come [aggiungere un account amministratore globale di tipo solo cloud](../active-directory-users-create-azure-portal.md). Eseguendo questo passaggio è tooensure critico che non restare bloccati del tenant.
2. Aggiungere uno o più [nomi di dominio personalizzato](../active-directory-add-domain.md) tenant tooyour Azure AD. Gli utenti accedono usando uno di questi nomi di dominio.

### <a name="in-your-on-premises-environment"></a>Nell'ambiente locale

1. Identificare un server che esegue Windows Server 2012 R2 o versioni successive in cui toorun di Azure AD Connect. Aggiungere l'insieme di strutture di hello server toohello stesso Active Directory come utenti di hello le cui password è necessario toobe convalidato.
2. Installare hello [versione più recente di Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) nel server di hello identificato nel passaggio precedente. Se si dispone già di esecuzione di Azure AD Connect, assicurarsi che la versione hello è 1.1.557.0 o versione successiva.
3. Identificare un server aggiuntivo che esegue Windows Server 2012 R2 o in un secondo momento quali toorun un agente Authentication autonomo. versione dell'agente di autenticazione Hello deve toobe 1.5.193.0 o versione successiva. Il server è necessario tooensure la disponibilità elevata di richieste di accesso. Aggiungere l'insieme di strutture di hello server toohello stesso Active Directory come utenti di hello le cui password è necessario toobe convalidato.
4. Se è presente un firewall tra i server e Azure AD, è necessario hello tooconfigure seguenti elementi:
   - Verificare che gli agenti di autenticazione è possibile rendere **in uscita** le richieste AD tooAzure attraverso hello seguenti porte:
   
   | Numero della porta | Uso |
   | --- | --- |
   | **80** | Download di revoca dei certificati elenchi (CRL) durante la convalida del certificato SSL hello |
   | **443** | Tutte le comunicazioni in uscita con il servizio |
   
   Se il firewall impone le regole in base agli utenti di toooriginating, aprire le porte per il traffico da servizi di Windows in esecuzione come servizio di rete.
   - Se il firewall o proxy consente whitelist DNS, le connessioni whitelist troppo**\*. msappproxy.net** e  **\*. n e t**. In caso contrario, consentire l'accesso troppo[intervalli IP dei Data Center Azure](https://www.microsoft.com/download/details.aspx?id=41653), che vengono aggiornati ogni settimana.
   - Gli agenti di autenticazione necessario accesso troppo**login.windows.net** e **login.microsoftonline.com** per la registrazione iniziale, quindi aprire il firewall per tali URL anche.
   - La convalida del certificato, sbloccare hello URL seguenti: **mscrl.microsoft.com:80**, **crl.microsoft.com:80**, **ocsp.msocsp.com:80** e  **www.microsoft.com:80**. Poiché vengono usati per la convalida del certificato con altri prodotti Microsoft, questi URL potrebbero essere già sbloccati.

## <a name="step-2-enable-exchange-activesync-support-optional"></a>Passaggio 2: Abilitare il supporto di Exchange ActiveSync (facoltativo)

Seguire questi tooenable istruzioni il supporto di Exchange ActiveSync:

1. Utilizzare [Exchange PowerShell](https://technet.microsoft.com/library/mt587043(v=exchg.150).aspx) hello toorun comando seguente:
```
Get-OrganizationConfig | fl per*
```

2. Controllare il valore di hello di hello `PerTenantSwitchToESTSEnabled` impostazione. Se il valore di hello è **true**, il tenant sia configurato correttamente - ciò avviene in genere hello per la maggior parte dei clienti. Se il valore di hello è **false**eseguire hello il seguente comando:
```
Set-OrganizationConfig -PerTenantSwitchToESTSEnabled:$true
```

3. Verificare che il valore di hello hello `PerTenantSwitchToESTSEnabled` è ora impostato troppo**true**. Attendere un'ora prima del passaggio successivo di toohello mobile.

In caso di problemi durante questo passaggio, vedere la [guida alla risoluzione dei problemi](active-directory-aadconnect-troubleshoot-pass-through-authentication.md#exchange-activesync-configuration-issues) per altre informazioni.

## <a name="step-3-enable-hello-feature"></a>Passaggio 3: Abilitare la funzionalità hello

L'autenticazione pass-through di Azure AD può essere abilitata tramite [Azure AD Connect](active-directory-aadconnect.md).

>[!IMPORTANT]
>L'autenticazione pass-through può essere abilitata nel server primario o di gestione temporanea di Connect hello Azure AD. Si consiglia di abilitarlo dal server primario hello.

Se si installa Microsoft Azure AD Connect per hello prima volta, scegliere hello [percorso di installazione personalizzato](active-directory-aadconnect-get-started-custom.md). In hello **account utente** pagina, scegliere **autenticazione pass-through** come hello Sign sul metodo. Al termine, viene installato un agente di autenticazione pass-through in hello nello stesso server di Azure AD Connect. Inoltre, funzionalità di autenticazione pass-through hello è abilitata per il tenant.

![Azure AD Connect - Accesso utente](./media/active-directory-aadconnect-sso/sso3.png)

Se è già stato installato Azure AD Connect (utilizzando hello [express installazione](active-directory-aadconnect-get-started-express.md) o hello [installazione personalizzata](active-directory-aadconnect-get-started-custom.md) percorso), selezionare **modifica utente nella pagina di accesso** su Azure AD La connessione e fare clic su **Avanti**. Selezionare quindi **autenticazione pass-through** come hello Sign sul metodo. Al termine, viene installato un agente di autenticazione pass-through in hello nello stesso server di funzionalità di Azure AD Connect e hello è abilitato per il tenant.

![Azure AD Connect - Cambiare l'accesso utente](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

>[!IMPORTANT]
>L'autenticazione pass-through è una funzionalità a livello di tenant. Riattivarlo influisce su sign-in per gli utenti tra _tutti_ hello gestito domini nel tenant. Se si passa da tooPass-tramite l'autenticazione AD FS, è consigliabile che l'attesa di almeno 12 ore prima di arrestare l'infrastruttura di ADFS, il tempo di attesa è tooensure che gli utenti possono mantenere accesso tooExchange ActiveSync durante la transizione.

## <a name="step-4-test-hello-feature"></a>Passaggio 4: Testare la funzionalità di hello

Seguire questi tooverify istruzioni che è stata attivata l'autenticazione pass-through correttamente:

1. Accedi toohello [centro di amministrazione di Azure Active Directory](https://aad.portal.azure.com) con credenziali di amministratore globale di hello per il tenant.
2. Selezionare **Azure Active Directory** nella navigazione a sinistra di hello.
3. Selezionare **Azure AD Connect**.
4. Verificare che hello **autenticazione pass-through** funzionalità Mostra come **abilitato**.
5. Selezionare **Autenticazione pass-through**. Questo pannello sono elencati i server di hello in cui sono installati gli agenti di autenticazione.

![Interfaccia di amministrazione di Azure Active Directory - Pannello Azure AD Connect](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Interfaccia di amministrazione di Azure Active Directory - Pannello Autenticazione pass-through](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

Dopo questo passaggio, gli utenti di tutti i domini gestiti nel tenant possono accedere usando l'autenticazione pass-through. Tuttavia, gli utenti da domini federati continuare toosign utilizzando Active Directory Federation Services (ADFS) o un altro provider di federazione che sono stati configurati. Se si converte un dominio da toomanaged federati, tutti gli utenti da quel dominio viene avviato automaticamente la firma usando l'autenticazione pass-through. Gli utenti solo cloud non sono interessati dalla funzionalità di autenticazione pass-through hello.

## <a name="step-5-ensure-high-availability"></a>Passaggio 5: Garantire la disponibilità elevata

Se si prevede di toodeploy autenticazione pass-through in un ambiente di produzione, è necessario installare un agente di autenticazione autonomo. Installare il secondo agente di autenticazione in un server _altri_ hello una connessione AD Azure in esecuzione e hello agente prima di autenticazione. Questa configurazione fornisce la disponibilità elevata delle richieste di accesso. Seguire questi toodeploy istruzioni un agente di autenticazione autonomo:

1. **Scaricare hello la versione più recente dell'agente di autenticazione hello (versioni 1.5.193.0 o versione successiva)**: Accedi toohello [centro di amministrazione di Azure Active Directory](https://aad.portal.azure.com) con credenziali di amministratore globale del tenant.
2. Selezionare **Azure Active Directory** nella navigazione a sinistra di hello.
3. Selezionare **Azure AD Connect****, quindi** Autenticazione pass-through. Selezionare quindi **Scarica agente**.
4. Fare clic su hello **accettarle & scaricare** pulsante.
5. **Installare hello la versione più recente dell'agente di autenticazione hello**: hello esecuzione eseguibile scaricato nel passaggio precedente hello. Fornire le credenziali di amministratore globale del tenant quando viene richiesto.

![Interfaccia di amministrazione di Azure Active Directory - Pulsante Scarica per l'agente di autenticazione](./media/active-directory-aadconnect-pass-through-authentication/pta9.png)

![Interfaccia di amministrazione di Azure Active Directory - Pannello Scarica agente](./media/active-directory-aadconnect-pass-through-authentication/pta10.png)

>[!NOTE]
>È inoltre possibile scaricare hello agente di autenticazione da [qui](https://aka.ms/getauthagent). Assicurarsi di esaminare e accettare hello autenticazione agente [Terms of Service](https://aka.ms/authagenteula) _prima_ l'installazione.

## <a name="next-steps"></a>Passaggi successivi
- [**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) (Limitazioni correnti): questa funzionalità è attualmente in anteprima. Informazioni su quali scenari sono supportati e quali non lo sono.
- [**Approfondimento tecnico**](active-directory-aadconnect-pass-through-authentication-how-it-works.md): informazioni sul funzionamento di questa funzionalità.
- [**Domande frequenti su** ](active-directory-aadconnect-pass-through-authentication-faq.md) -risposte toofrequently domande frequenti.
- [**Risoluzione dei problemi** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -informazioni su come le problematiche comuni tooresolve con funzionalità hello.
- [**Seamless Single Sign-On di Azure AD**](active-directory-aadconnect-sso.md): altre informazioni su questa funzionalità complementare.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): per l'invio di richieste di nuove funzionalità.
