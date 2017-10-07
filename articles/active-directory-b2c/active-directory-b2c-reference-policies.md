---
title: 'Azure Active Directory B2C: criteri predefiniti | Microsoft Docs'
description: Un argomento nel framework di criteri estendibile hello di Azure Active Directory B2C e su come toocreate vari tipi di criteri
services: active-directory-b2c
documentationcenter: 
author: sama
manager: mbaldwin
editor: PatAltimore
ms.assetid: 0d453e72-7f70-4aa2-953d-938d2814d5a9
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: sama
ms.openlocfilehash: 24bb85eba30f888c6ea7d0401e05235e8eb6ea79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a>Azure Active Directory B2C: criteri predefiniti


framework di criteri estendibile Hello di B2C Azure Active Directory (Azure AD) è il livello di attendibilità di hello componenti di base del servizio hello. I criteri descrivono le esperienze di identità, ad esempio iscrizione, accesso o modifica del profilo. Ad esempio, un criterio per l'abbonamento consente comportamenti toocontrol configurando hello seguenti impostazioni:

* Account di tipi (account di social networking, ad esempio Facebook) o locale, ad esempio indirizzi di posta elettronica che i consumer possono utilizzare toosign per un'applicazione hello
* Attributi (ad esempio nome, il CAP e scarpe) toobe raccolti dai consumer hello durante l'iscrizione
* Uso di Azure Multi-Factor Authentication
* Hello aspetto di tutte le pagine di iscrizione
* Informazioni (che si manifesta come attestazioni in un token) che l'applicazione hello riceve al termine dell'esecuzione dei criteri di hello

È possibile creare più criteri di tipi diversi nel proprio tenant e usarli nelle applicazioni in base alle esigenze. I criteri possono essere usati per più applicazioni. Questa flessibilità consente agli sviluppatori toodefine e modificare esperienze di identità consumer con una quantità minima o nessun codice tootheir le modifiche.

Per usare i criteri, è disponibile una semplice interfaccia per sviluppatori. L'applicazione può attivare un criterio tramite una richiesta di autenticazione HTTP standard (passando un parametro di criteri nella richiesta di hello) e riceve un token personalizzato come risposta. Ad esempio, hello l'unica differenza tra le richieste che richiamano un criterio di iscrizione e richiamare un criterio di accesso è nome criterio hello utilizzato nel parametro di stringa di query hello "p":

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siup                                       // Your sign-up policy

```

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siin                                       // Your sign-in policy

```

Per ulteriori informazioni su hello criteri framework, vedere [questo post di blog sul Blog di sicurezza e Azure Active Directory B2C su Enterprise Mobility hello](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).

## <a name="create-a-sign-up-or-sign-in-policy"></a>Creare un criterio di iscrizione o accesso

Questo criterio consente di gestire le esperienze di iscrizione e accesso dei consumatori tramite una singola configurazione. I consumer sono dirette verso il basso hello percorso verso destra (iscrizione o accesso) a seconda del contesto di hello. Vengono inoltre descritte contenuto hello di token che un'applicazione hello riceverà iscrizioni ha esito positivo o accessi.  È un esempio di codice per il criterio di iscrizione o accesso hello [disponibile qui](active-directory-b2c-devquickstarts-web-dotnet-susi.md).  È consigliabile usare questo criterio invece di criteri di iscrizione e di accesso.  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a>Creare un criterio di iscrizione

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a>Creare un criterio di accesso

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a>Creare i criteri di modifica del profilo

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a>Creare i criteri di reimpostazione delle password

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a>Domande frequenti

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a>Come si collegano i criteri di iscrizione o accesso ai criteri di reimpostazione delle password?
Quando si crea un criterio di iscrizione o accesso (con gli account locali), viene visualizzato un **password dimenticata?** collegamento hello prima pagina dell'esperienza di hello. Se si fa clic su questo collegamento non si attivano automaticamente i criteri di reimpostazione delle password. 

Hello, invece, il codice di errore  **`AADB2C90118`**  viene restituito tooyour app. L'app deve toohandle questo codice di errore tramite la chiamata di un criterio di reimpostazione password specifica. Per ulteriori informazioni, vedere una [esempio che illustra l'approccio di hello del collegamento dei criteri di](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a>È consigliabile usare criteri di iscrizione o accesso o criteri di iscrizione e criteri di accesso?
È consigliabile usare criteri di iscrizione o accesso al posto di criteri di iscrizione e criteri di accesso.  

criteri di iscrizione o accesso Hello offre maggiori funzionalità rispetto a criterio di accesso hello. Inoltre, consente la personalizzazione dell'interfaccia utente di pagina toouse e ha un supporto migliore per la localizzazione. 

criteri di accesso Hello sono consigliato se non è necessario toolocalize i criteri, solo necessario funzionalità di personalizzazione secondaria per la personalizzazione e la password reset incorporato.

## <a name="next-steps"></a>Passaggi successivi
* [Configurazione di token, sessione e accesso Single Sign-On](active-directory-b2c-token-session-sso.md)
* [Disabilitare la verifica della posta elettronica durante l'iscrizione dell'utente](active-directory-b2c-reference-disable-ev.md)

