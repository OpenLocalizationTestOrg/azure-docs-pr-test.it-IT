---
title: Errore imprevisto di aaa quando si esegue l'applicazione di consenso tooan | Documenti Microsoft
description: "Vengono illustrati gli errori che possono verificarsi durante il processo di hello di consenso applicazione tooan e ciò che è possibile eseguire su di essi"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: dfee35f3a10e3cc4313109cedd972499452320f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-error-when-performing-consent-tooan-application"></a>Errore imprevisto durante l'esecuzione dell'applicazione tooan di consenso

Questo articolo illustra gli errori che possono verificarsi durante il processo di hello di consenso tooan applicazione. Per risolvere i problemi relativi a richieste di consenso impreviste che non contengono messaggi di errore, vedere [Scenari di autenticazione per Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).

Molte applicazioni che si integrano con Azure Active Directory richiedono autorizzazioni tooaccess altre risorse in ordine toofunction. Quando queste risorse sono inoltre integrate con Azure Active Directory, autorizzazioni tooaccess li spesso è richiesto mediante hello comune framework di consenso. 

Ciò comporta una richiesta di consenso viene visualizzata, che si verifica in genere hello prima volta che un'applicazione viene utilizzata, ma può anche verificarsi in un utilizzo successivo di un'applicazione hello.

Determinate condizioni devono essere true per un'applicazione richiede le autorizzazioni di toohello tooconsent un utente. In caso contrario, possono verificarsi diversi errori, inclusi i seguenti:

## <a name="requesting-not-authorized-permissions-error"></a>Errore di richiesta di autorizzazioni non consentite
* **AADSTS90093:** &lt;clientAppDisplayName&gt; richiede uno o più autorizzazioni che non sono autorizzate toogrant. Contattare un amministratore, che è possibile fornire il consenso dell'applicazione toothis per conto dell'utente.

Questo errore si verifica quando un utente che non è un amministratore della società tenta toouse un'applicazione che richiede solo un amministratore può concedere le autorizzazioni. Questo errore può essere risolto da un amministratore di concedere l'accesso toohello applicazione per conto dell'organizzazione.

## <a name="policy-prevents-granting-permissions-error"></a>Errore dovuto a criteri che impediscono di concedere le autorizzazioni
* **AADSTS90093:** un amministratore di &lt;tenantDisplayName&gt; ha impostato un criterio che impedisce la concessione &lt;nome dell'app&gt; hello richiede autorizzazioni. Rivolgersi all'amministratore di &lt;tenantDisplayName&gt;, che può concedere autorizzazioni toothis app per conto dell'utente.

Questo errore si verifica quando un amministratore della società si spegne il possibilità hello per gli utenti tooconsent tooapplications, un utente non amministratore tenta toouse un'applicazione che richiede il consenso. Questo errore può essere risolto da un amministratore di concedere l'accesso toohello applicazione per conto dell'organizzazione.

## <a name="intermittent-problem-error"></a>Errore dovuto a un problema intermittente
* **AADSTS90090:** sembra che si è verificato un problema intermittente registrazione autorizzazioni hello si è tentato di troppo toogrant&lt;clientAppDisplayName&gt;. Riprovare in un secondo momento.

Questo errore indica che si è verificato un problema intermittente relativo al servizio. Possa essere risolto tentando nuovamente l'applicazione toohello tooconsent.

## <a name="resource-not-available-error"></a>Errore di risorsa non disponibile
* **AADSTS65005:** app hello &lt;clientAppDisplayName&gt; richiesto autorizzazioni tooaccess una risorsa &lt;resourceAppDisplayName&gt; che non è disponibile. 

Contattare lo sviluppatore dell'applicazione hello.

##  <a name="resource-not-available-in-tenant-error"></a>Errore di risorsa non disponibile nel tenant
* **AADSTS65005:** &lt;clientAppDisplayName&gt; richiede accesso tooa risorse &lt;resourceAppDisplayName&gt; che non è disponibile all'interno dell'organizzazione &lt; tenantDisplayName&gt;. 

Assicurarsi che la risorsa sia disponibile o contattare un amministratore di &lt;NomeVisualizzatoTenant&gt;.

## <a name="permissions-mismatch-error"></a>Errore di mancata corrispondenza delle autorizzazioni
* **AADSTS65005:** app hello richiesto il consenso tooaccess risorse &lt;resourceAppDisplayName&gt;. Questa richiesta non riuscita perché non corrisponde ad come app hello è stato preconfigurato durante la registrazione dell'app. Contattare hello app vendor.* *

Questi tutti gli errori si verificano quando un'applicazione hello un utente tenta di toois tooconsent che richiede autorizzazioni tooaccess un'applicazione della risorsa trovato nella directory dell'organizzazione hello (tenant). Questa situazione può verificarsi per diversi motivi:

-   sviluppatore di applicazioni client Hello ha configurato le applicazioni in modo errato, causandone risorsa non valido di toorequest accesso tooan. In questo caso, sviluppatore dell'applicazione hello necessario aggiornare la configurazione hello di hello client applicazione tooresolve questo problema.

-   Un'entità servizio che rappresenta un'applicazione hello destinazione risorsa non esiste nell'organizzazione di hello, o esisteva in hello precedente, ma è stata rimossa. tooresolve questo problema, un'entità servizio per un'applicazione hello risorsa deve essere effettuato il provisioning nell'organizzazione hello in modo un'applicazione hello client può richiedere le autorizzazioni tooit. Questo può verificarsi un numero di modi, a seconda di tipo hello dell'applicazione, tra cui:

    -   L'acquisizione di una sottoscrizione per l'applicazione della risorsa hello (applicazioni pubblicate da Microsoft)

    -   Applicazione della risorsa toohello consenso

    -   Concessione di autorizzazioni applicazione hello tramite hello portale di Azure

    -   Aggiunta di un'applicazione hello da hello raccolta di applicazioni Azure AD

## <a name="next-steps"></a>Passaggi successivi 

[App, autorizzazioni e consenso in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)<br>

[Gli ambiti, autorizzazioni e consenso hello Azure Active Directory (endpoint v 2.0)](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


