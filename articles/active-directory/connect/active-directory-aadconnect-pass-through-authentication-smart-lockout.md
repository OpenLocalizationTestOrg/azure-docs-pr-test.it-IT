---
title: 'Azure AD Connect: autenticazione pass-through - Blocco smart | Microsoft Docs'
description: In questo articolo viene descritto come l'autenticazione pass-through di Azure Active Directory (Azure AD) consente di proteggere gli account locali da attacchi di forza bruta password nel cloud hello.
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
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: b02e315c3cc3eae00ca6408d735a416f34c2cdc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a>Autenticazione pass-through di Azure Active Directory: blocco smart

## <a name="overview"></a>Panoramica

Azure AD consente di proteggersi dagli attacchi di forza bruta alle password e impedisce il blocco delle applicazioni Office 365 e SaaS degli utenti originali. Questa funzionalità, denominata **blocco smart**, è supportata quando si usa l'autenticazione pass-through come metodo di accesso. Blocco intelligente è abilitato per impostazione predefinita per tutti i tenant e proteggere tutti i tempi di hello; gli account utente non è alcuna necessità tooturn sul.

Il blocco smart tiene traccia dei tentativi di accesso non riusciti e dopo una determinata **soglia di blocco**, avvia la **durata del blocco**. Eventuali tentativi di accesso da attacchi di hello durante la durata del blocco hello vengono rifiutati. Se l'attacco hello continua, hello successivi tentativi di accesso scadenza hello durata del blocco del risultato in più intervalli di blocco.

>[!NOTE]
>Hello valore predefinito di soglia di blocco è 10 tentativi non riusciti e default hello che durata del blocco è 60 secondi.

Blocco smart anche distingue tra l'accesso degli utenti originali e da utenti malintenzionati e solo i blocchi out gli utenti malintenzionati hello nella maggior parte dei casi. Questa funzionalità impedisce agli utenti malintenzionati di bloccare gli utenti veri. Utilizziamo Accedi il comportamento passato, i dispositivi degli utenti & browser e altre toodistinguish segnali tra originali e utenti malintenzionati. Gli algoritmi vengono migliorati costantemente.

Poiché l'autenticazione pass-through inoltra le richieste di convalida di password in locale Active Directory (AD), è necessario ai pirati informatici tooprevent di blocco degli account di Active Directory degli utenti. Poiché si dispone di propri criteri di blocco degli Account di Active Directory (in particolare, [ **soglia blocco Account** ](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) e [ **Reimposta Account blocco contatore dopo aver criteri** ](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), è necessario soglia di blocco tooconfigure Azure AD e blocca i valori in modo appropriato toofilter attacchi nel cloud hello prima che raggiungano locale Active Directory.

>[!NOTE]
>funzionalità di blocco Smart Hello è gratuita ed _su_ per impostazione predefinita per tutti i clienti. Modifica di soglia di blocco e i valori di durata del blocco usando l'API Graph di Azure AD deve, tuttavia, la licenza di P2 Premium toohave Azure AD almeno un tenant. Non occorre una licenza Azure AD Premium P2 _per ogni utente_ funzionalità di blocco Smart hello tooget con l'autenticazione pass-through.

tooensure che degli utenti AD account locali siano ben protetti, è necessario tooensure che:

1.  La Soglia di blocco di Azure AD sia _inferiore_ alla soglia di blocco dell'account di AD. È consigliabile impostare valori hello tale soglia blocco Account di Active Directory è almeno due o tre volte la soglia di blocco di Azure AD.
2.  La durata del blocco di Azure AD, rappresentata in secondi, è _maggiore_ rispetto al valore di Reimposta blocco account dopo di AD, rappresentato in minuti.

## <a name="verify-your-ad-account-lockout-policies"></a>Verificare i criteri di blocco degli account di AD

Utilizzare hello seguendo le istruzioni tooverify i criteri di blocco degli Account di Active Directory:

1.  Aprire lo strumento di gestione criteri di gruppo hello.
2.  Modificare hello criteri di gruppo applicati tooall utenti, ad esempio, hello criterio dominio predefinito.
3.  Passare tooComputer Configurazione computer\Criteri\Impostazioni di Windows\Impostazioni protezione\Criteri account\Criterio blocco criteri.
4.  Verificare i valori di Soglia di blocchi dell'account e Reimposta blocco account dopo.

![Criteri di blocco degli account di AD](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-hello-graph-api-toomanage-your-tenants-smart-lockout-values"></a>Utilizzare hello API Graph toomanage valori blocco Smart del tenant

>[!IMPORTANT]
>La modifica dei valori relativi alla soglia di blocco e alla durata del blocco di Azure AD tramite l'API Graph di Azure AD sono funzionalità di Azure AD Premium P2. Richiede inoltre toobe un amministratore globale per il tenant.

È possibile utilizzare [Esplora grafico](https://developer.microsoft.com/graph/graph-explorer) tooread, impostare e aggiornare i valori di blocco Smart di Azure AD. Ma è anche possibile eseguire queste operazioni a livello di programmazione.

### <a name="read-smart-lockout-values"></a>Leggere i valori di blocco smart

Seguire questi tooread passaggi valori blocco Smart del tenant:

1. Accedere a Graph explorer come amministratore globale del tenant. Se richiesto, concedere l'accesso per hello richiesta delle autorizzazioni.
2. Selezionare l'autorizzazione "Directory.ReadWrite.All" hello "Autorizzazioni di modifica".
3. Configurare richiesta all'API Graph hello come segue: Set versione troppo "BETA", tipo di richiesta troppo "GET" e l'URL troppo`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.
4. Fare clic su "Esegui Query" toosee valori blocco Smart del tenant. Se i valori del tenant non sono stati mai impostati, viene visualizzato un insieme vuoto.

### <a name="set-smart-lockout-values"></a>Impostare i valori di blocco smart

Seguire questi tooset passaggi valori blocco Smart del tenant (per hello solo la prima volta):

1. Accedere a Graph explorer come amministratore globale del tenant. Se richiesto, concedere l'accesso per hello richiesta delle autorizzazioni.
2. Selezionare l'autorizzazione "Directory.ReadWrite.All" hello "Autorizzazioni di modifica".
3. Configurare richiesta all'API Graph hello come segue: Set versione troppo "BETA", tipo di richiesta troppo "POST" e l'URL troppo`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.
4. Copiare e incollare hello seguente richiesta JSON nel campo "Corpo della richiesta" hello. Modificare valori blocco Smart hello in modo appropriato e usare un GUID casuale per `templateId`.
5. Fare clic su "Esegui Query" tooset valori blocco Smart del tenant.

```
{
  "templateId": "5cf42378-d67d-4f36-ba46-e8b86229381d",
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "300"
    },
    {
      "name": "LockoutThreshold",
      "value": "5"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

>[!NOTE]
>Se non vengono utilizzati, è possibile lasciare hello **BannedPasswordList** e **EnableBannedPasswordCheck** i valori come vuoto ("") e "false" rispettivamente.

Verificare di aver impostato i valori di blocco smart del tenant correttamente tramite [questa procedura](#read-smart-lockout-values).

### <a name="update-smart-lockout-values"></a>Aggiornare i valori di blocco smart

Seguire questi tooupdate passaggi valori blocco Smart del tenant (se è già stato impostato in precedenza):

1. Accedere a Graph explorer come amministratore globale del tenant. Se richiesto, concedere l'accesso per hello richiesta delle autorizzazioni.
2. Selezionare l'autorizzazione "Directory.ReadWrite.All" hello "Autorizzazioni di modifica".
3. [Seguire questi tooread passaggi valori blocco Smart del tenant](#read-smart-lockout-values). Hello copia `id` valore (GUID) dell'elemento hello con "displayName" come "PasswordRuleSettings".
4. Configurare richiesta all'API Graph hello come segue: Set versione troppo "BETA", tipo di richiesta troppo "PATCH" e l'URL troppo`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` -utilizzare hello GUID dal passaggio 3 per `<id>`.
5. Copiare e incollare hello seguente richiesta JSON nel campo "Corpo della richiesta" hello. Modificare i valori di blocco Smart hello come appropriato.
6. Fare clic su "Esegui Query" tooupdate valori blocco Smart del tenant.

```
{
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "30"
    },
    {
      "name": "LockoutThreshold",
      "value": "4"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

Verificare di aver aggiornato i valori di blocco smart del tenant correttamente tramite [questa procedura](#read-smart-lockout-values).

## <a name="next-steps"></a>Passaggi successivi
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): per l'invio di richieste di nuove funzionalità.
