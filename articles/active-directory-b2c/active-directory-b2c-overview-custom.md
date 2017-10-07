---
title: 'Azure Active Directory B2C: attributi personalizzati | Microsoft Docs'
description: Un argomento sui criteri personalizzati di Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1ff398a4-2079-4615-94f1-57de22c0aad6
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: bada9cf5f1a86f3dd047536f6fd9359c0231a384
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-custom-policies"></a>Azure Active Directory B2C: criteri personalizzati

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

## <a name="what-are-custom-policies"></a>Definizione di criteri personalizzati

Criteri personalizzati sono file di configurazione che definiscono il comportamento di hello del tenant di Azure Active Directory B2C. Mentre **criteri predefiniti** sono predefiniti nel portale di Azure Active Directory B2C hello per hello attività più comuni di identità, i criteri personalizzati può essere modificato completamente da un toocomplete developer identità un numero illimitato vicino di attività. Continuare a leggere toodetermine se i criteri personalizzati sono adatta all'utente e lo scenario di identità.

**La modifica dei criteri personalizzati non è adatta a tutti gli utenti.** curva di apprendimento Hello complesse, tempo di avvio hello è più lungo e criteri toocustom modifiche future richiederà toomaintain esperienza simile. I criteri predefiniti devono essere considerati attentamente per lo scenario prima di usare i criteri personalizzati.

## <a name="comparing-built-in-policies-and-custom-policies"></a>Confronto tra criteri predefiniti e personalizzati

| | Criteri predefiniti | Criteri personalizzati |
|-|-------------------|-----------------|
|Utenti di destinazione | Tutti gli sviluppatori di app con o senza competenze di identità | Professionisti di identità: integratori di sistemi, consulenti e team di identità interni. Hanno familiarità con i flussi OpenIDConnect e comprendono i provider di identità e l'autenticazione basata sulle attestazioni |
|Metodo di configurazione | Portale di Azure con un'interfaccia utente intuitiva | Modificare direttamente i file XML e quindi caricare toohello portale di Azure |
|Personalizzazione dell'interfaccia utente | Personalizzazione completa dell'interfaccia utente, che include il supporto HTML, CSS e jscript, che richiede il dominio personalizzato<br><br>Supporto multilingue con stringhe personalizzate | Uguale |
| Personalizzazione degli attributi | Attributi standard e personalizzati | Uguale |
|Gestione delle sessioni e dei token | Token personalizzato e opzioni di sessione multiple | Uguale |
|Provider di identità| **Oggi**: provider social, predefinito, locale<br><br>**Futuro**: OIDC, SAML, OAuth basati su standard | **Oggi**: OIDC, SAML, OAuth basati su standard<br><br>**Futuro**: WsFed |
|Attività relative all'identità: esempi | Iscrizione o accesso ad account social e locali multipli<br><br>Reimpostazione della password self-service<br><br>Modifica del profilo<br><br>Scenari con autenticazione a più fattori<br><br>Personalizzare token e sessioni<br><br>Flussi di accesso ai token | Completare hello stessa attività come criteri predefiniti utilizzando provider di identità personalizzati o utilizzare gli ambiti personalizzati<br><br>Utente di effettuare il provisioning in un altro sistema in fase di hello della registrazione<br><br>Inviare un messaggio di posta elettronica di benvenuto con il proprio provider di servizi di posta elettronica<br><br>Usare un archivio utente esterno B2C<br><br>Convalidare le informazioni date dall'utente con un sistema attendibile tramite API |

## <a name="policy-files"></a>File dei criteri

Un criterio personalizzato è rappresentato come una o più file di formato XML che fanno riferimento altri in una catena gerarchica tooeach. definiscono gli elementi XML Hello: schema di attestazioni, le attestazioni trasformazioni, le definizioni di contenuto, attestazioni provider o tecnico profili e i passaggi di orchestrazione Userjourney, tra gli altri elementi.

È consigliabile utilizzare hello dei tre tipi di file dei criteri:

- **Un file di BASE**, che contiene la maggior parte delle definizioni di hello e per cui Azure fornisce un esempio completo.  Si consiglia di che fare un numero minimo di modifiche toothis file toohelp la risoluzione dei problemi e manutenzione a lungo termine dei criteri di
- **un file con estensioni** che contiene le modifiche di configurazione univoco hello per il tenant
- **un file di Relying Party (RP)** ovvero hello singolo incentrato sulle attività e file che viene richiamata direttamente da un'applicazione hello o un servizio (noto anche come Relying Party).  Leggere l'articolo hello alle definizioni dei file di criteri per ulteriori informazioni.  Ogni attività univoco richiede il proprio RP e a seconda di branding requisiti numero hello potrebbe essere "totale delle applicazioni x numero totale di casi di utilizzo".


Criteri predefiniti in Azure Active Directory B2C seguono il modello di 3 file hello illustrato sopra, ma per sviluppatori di hello solo vede hello file Relying Party (RP), mentre il portale di hello apporta modifiche nel file di hello background toohello estensioni.

## <a name="core-concepts-you-should-know-when-using-custom-policies"></a>Concetti di base che è necessario conoscere quando si usano i criteri personalizzati

### <a name="azure-active-directory-b2c"></a>Azure Active Directory B2C

Azure è dotato del servizio di identità del cliente e gestione dell'accesso, CIAM. servizio Hello include:

1. Una directory utente sotto forma di hello di accessibile tramite Microsoft Graph e che contiene i dati utente per gli account locali e account federati una speciale Azure Active Directory 
2. Accesso toohello **identità esperienza Framework** che gestisce la relazione di trust tra utenti e le entità e la passa le attestazioni tra di essi toocomplete un'attività di gestione di identità o l'accesso 
3. Un servizio token di sicurezza (STS) emissione id token, aggiorna i token e accesso token (e asserzioni SAML equivalente) e convalida di tali risorse tooprotect.

Azure Active Directory B2C interagisce con i provider di identità, gli utenti, altri sistemi e all'elenco di utenti locale hello in sequenza tooachieve un'attività di identità (ad esempio account di accesso di un utente, registrare un nuovo utente, reimpostare una password). Hello piattaforma sottostante che stabilisce relazioni di trust più parti ed esegue questa procedura viene chiamata hello Framework esperienza di identità e criteri (detto anche il passaggio di un utente o un criterio di attendibilità framework) definisce in modo esplicito gli attori hello, azioni di hello, hello protocolli e hello sequenza di passaggi toocomplete.

### <a name="identity-experience-framework"></a>Framework dell'esperienza di gestione delle identità

Una piattaforma Azure completamente configurabile, basato sui criteri e su cloud che orchestra le relazioni di trust tra le entità, in modo più ampio i provider di attestazioni, in formati di protocollo standard, ad esempio OpenIDConnect, OAuth, SAML, standard WSFed e alcuni formati non standard, ad esempio, scambi di attestazioni basati su API REST da sistema a sistema. Hello I2E crea intuitiva, whitelabelled esperienze che supportano HTML, CSS e jscript.  Oggi, hello identità esperienza Framework è disponibile solo nel contesto di hello del servizio di Azure Active Directory B2C hello e priorità per le attività correlate tooCIAM.

### <a name="built-in-policies"></a>Criteri predefiniti

File di configurazione che il comportamento di hello diretto dell'identità di Azure Active Directory B2C tooperform hello più diffuse attività (ad esempio la registrazione utente, accesso, la reimpostazione della password) e interagire con le parti attendibili a cui la relazione è predefinita anche in Azure Active Directory B2C (predefinite ad esempio provider di identità Facebook, LinkedIn, Account Microsoft, gli account di Google).  In futuro hello, i criteri predefiniti possono anche fornire per la personalizzazione del provider di identità che sono in genere nell'area di autenticazione enterprise hello, ad esempio Azure Active Directory Premium, Active Directory o ADFS, Salesforce ID Provider via.


### <a name="custom-policies"></a>Criteri personalizzati

File di configurazione che definiscono il comportamento di hello del Framework di esperienza di identità nel tenant di Azure Active Directory B2C. Un criterio personalizzato non è accessibile come uno o più file XML (vedere le definizioni di file di criteri) che vengono eseguiti dall'hello identità esperienza Framework quando viene richiamato per una relying party (ad esempio, un'applicazione). Criteri personalizzati possono essere modificato direttamente da un toocomplete developer identità un numero illimitato vicino di attività. Gli sviluppatori devono definire la configurazione di criteri personalizzati hello relazioni attendibili nell'endpoint dei metadati di dettaglio attenzione tooinclude, esatte attestazioni definizioni di exchange e configurare i certificati, chiavi e segreti in base alle esigenze di ogni provider di identità.

## <a name="policy-file-definitions-for-identity-experience-framework-trustframeworks"></a>Definizione di file di criteri per i framework di attendibilità per il Framework di esperienza di identità

### <a name="policy-files"></a>File dei criteri

Un criterio personalizzato è rappresentato come una o più file di formato XML che fanno riferimento altri in una catena gerarchica tooeach. definiscono gli elementi XML Hello: schema di attestazioni, le attestazioni trasformazioni, le definizioni di contenuto, attestazioni provider o tecnico profili e i passaggi di orchestrazione Userjourney, tra gli altri elementi.  È consigliabile utilizzare hello dei tre tipi di file dei criteri:

- **Un file di BASE**, che contiene la maggior parte delle definizioni di hello e per cui Azure fornisce un esempio completo.  Si consiglia di che fare un numero minimo di modifiche toothis file toohelp la risoluzione dei problemi e manutenzione a lungo termine dei criteri di
- **un file con estensioni** che contiene le modifiche di configurazione univoco hello per il tenant
- **un file di Relying Party (RP)** ovvero hello singolo incentrato sulle attività e file che viene richiamata direttamente da un'applicazione hello o un servizio (noto anche come Relying Party).  Leggere l'articolo hello alle definizioni dei file di criteri per ulteriori informazioni.  Ogni attività univoco richiede il proprio RP e a seconda di branding requisiti numero hello potrebbe essere "totale delle applicazioni x numero totale di casi di utilizzo".

![Tipi di file di criteri](media/active-directory-b2c-overview-custom/active-directory-b2c-overview-custom-policy-files.png)

| Tipo di file di criteri | Nome del file di esempio | Uso consigliato | Eredito da |
|---------------------|--------------------|-----------------|---------------|
| BASE |TrustFrameworkBase.xml<br><br>Mytenant.onmicrosoft.com-B2C-1A_BASE1.xml | Include nello schema di attestazioni di hello principale, le trasformazioni di attestazioni, provider di attestazioni e i percorsi utente configurati da Microsoft<br><br>Verificare il file toothis modifiche minime | Nessuno |
| Estensione (RXT) | TrustFrameworkExtensions.xml<br><br>Mytenant.onmicrosoft.com-B2C-1A_EXT.xml | Consolidare le modifiche toohello BASE file qui<br><br>Provider di attestazioni modificati<br><br>Percorsi utente modificati<br><br>Definizioni dello schema personalizzato | File di BASE |
| Relying Party (RP) | B2C_1A_sign_up_sign_in.xml| Modificare la forma del token e le impostazioni della sessione qui| File Extensions(Ext) |

### <a name="inheritance-model"></a>Modello di ereditarietà

Quando un'applicazione chiama il file dei criteri RP hello, hello Identity Framework esperienza in B2C aggiungere tutti gli elementi di hello di BASE, quindi dalle estensioni e infine da hello RP criteri file tooassemble hello criteri correnti attive.  Gli elementi di hello stesso tipo e nome file RP hello sostituiranno quelle hello estensioni e gli override delle estensioni della BASE.

**Criteri predefiniti** in Azure Active Directory B2C seguono il modello di 3 file hello illustrato sopra, ma per sviluppatori di hello solo vede hello file Relying Party (RP), mentre il portale di hello apporta modifiche nel file di hello background toohello estensioni.  Tutti di Azure Active Directory B2C condivide un file dei criteri BASE che è incluso nel controllo del team di hello Azure B2C hello e viene aggiornato di frequente.
