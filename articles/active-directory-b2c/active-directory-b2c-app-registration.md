---
title: 'Azure Active Directory B2C: registrazione dell''applicazione | Documentazione Microsoft'
description: Come tooregister l'applicazione con Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: PatAltimore
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f69
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: parakhj
ms.openlocfilehash: bd58e123751db387d6c8f16bd010291ba698b1a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a>Azure Active Directory B2C: registrare l'applicazione

Questa esercitazione introduttiva consente di registrare un'applicazione in un tenant di Microsoft Azure Active Directory (Azure AD) B2C in pochi minuti. Al termine, l'applicazione è registrata per l'uso nel tenant di Azure B2C hello.

## <a name="prerequisites"></a>Prerequisiti

toobuild un'applicazione che accetta consumer per l'abbonamento e l'accesso, è necessario innanzitutto un'applicazione hello tooregister con un tenant di Azure Active Directory B2C. Ottenere il proprio tenant utilizzando i passaggi descritti nella procedura hello [creare un tenant di Azure Active Directory B2C](active-directory-b2c-get-started.md).

Le applicazioni create dal Pannello di Azure Active Directory B2C hello in hello portale di Azure devono essere gestite da hello nello stesso percorso. Se si modificano applicazioni B2C hello tramite PowerShell o un altro portale, essi diventano non supportati e non funzionano con Azure Active Directory B2C. Visualizzare i dettagli di hello [errore app](#faulted-apps) sezione. 

## <a name="navigate-toob2c-settings"></a>Passare a impostazioni tooB2C

Accedi toohello [portale di Azure](https://portal.azure.com/) come amministratore globale del tenant hello B2C hello. 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

Scegliere i passaggi successivi in base al tipo di applicazione hello che registrazione:

* [Registrare un'applicazione Web](#register-a-web-app)
* [Registrare un'API Web](#register-a-web-api).
* [Registrare un'applicazione per dispositivi mobili o nativa](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a>Registrare un'app Web

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

Se l'applicazione Web chiama un'API Web protetta da Azure AD B2C, seguire questa procedura:
   1. Creare un segreto dell'applicazione da passare toohello **chiavi** blade e facendo clic su hello **Genera chiave** pulsante. Prendere nota di hello **chiave App** valore. Valore di hello è utilizzato come segreto dell'applicazione hello nel codice dell'applicazione.
   2. Fare clic su **Accesso all'API**, quindi su **Aggiungi** e selezionare l'API Web e gli ambiti (autorizzazioni).

> [!NOTE]
> Un **segreto dell'applicazione** è una credenziale di sicurezza importante e deve essere protetto in modo appropriato.
> 

[Passare troppo**passaggi successivi**](#next-steps)

## <a name="register-a-web-api"></a>Registrare un'API Web

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

Fare clic su **pubblicati ambiti** tooadd più ambiti in base alle esigenze. Per impostazione predefinita, l'ambito "user_impersonation" hello è definito. ambito user_impersonation Hello offre altri tooaccess possibilità di hello applicazioni questa api per conto di utente connesso di hello. Se si desidera, è possibile rimuovere ambito user_impersonation hello.

[Passare troppo**passaggi successivi**](#next-steps)

## <a name="register-a-mobile-or-native-app"></a>Registrare un'app per dispositivi mobili o nativa

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[Passare troppo**passaggi successivi**](#next-steps)

## <a name="limitations"></a>Limitazioni

### <a name="choosing-a-web-app-or-api-reply-url"></a>Scelta di un URL di risposta per un'API o un'app Web

Le applicazioni che sono registrate con Azure Active Directory B2C non sono attualmente limitate tooa limitato set di valori di URL di risposta. Hello reply URL per le applicazioni web e servizi deve iniziare con lo schema di hello `https`, e Rispondi a tutti i valori di URL devono condividere un singolo dominio DNS. Non è possibile ad esempio registrare un'app Web con uno degli URL di risposta seguenti:

`https://login-east.contoso.com`

`https://login-west.contoso.com`

sistema di registrazione Hello Confronta hello intero DNS nome di hello esistente reply URL toohello DNS hello dell'URL di risposta che si sta aggiungendo. hello tooadd di Hello richiesta nome DNS non riesce se viene soddisfatta una delle seguenti condizioni hello:

* intero nome DNS Hello hello nuovo dell'URL di risposta non corrisponde il nome DNS hello hello esistente dell'URL di risposta.
* intero nome DNS Hello hello nuovo dell'URL di risposta non è un sottodominio hello esistente dell'URL di risposta.

Ad esempio, se hello app è l'URL di risposta seguente:

`https://login.contoso.com`

È possibile aggiungere tooit, simile al seguente:

`https://login.contoso.com/new`

In questo caso, il nome DNS hello corrisponde esattamente. In alternativa, è possibile eseguire un'aggiunta analoga alla seguente:

`https://new.login.contoso.com`

In questo caso, si fa riferimento il sottodominio DNS tooa di login.contoso.com. Se si desidera toohave un'applicazione che dispone di account di accesso east.contoso.com e west.contoso.com account di accesso come URL di risposta, è necessario aggiungere tali URL di risposta in questo ordine:

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

È possibile aggiungere queste ultime hello perché sono sottodomini hello prima dell'URL di risposta, contoso.com.

### <a name="choosing-a-native-app-redirect-uri"></a>Scelta di un URI di reindirizzamento per un'app nativa

Quando si sceglie un URI di reindirizzamento per applicazioni per dispositivi mobili/native, occorre tenere presenti due considerazioni importanti:

* **Univoco**: schema hello dell'URI di reindirizzamento hello deve essere univoco per ogni applicazione. Nel nostro esempio (com.onmicrosoft.contoso.appname://redirect/path), utilizziamo com.onmicrosoft.contoso.appname lo schema di hello. È consigliabile seguire questo modello. Se due applicazioni condividono hello stesso schema, hello utente visualizza una finestra di dialogo "Scegli app". Se l'utente hello effettua una scelta errata, l'account di accesso hello ha esito negativo.
* **Completezza**: l'URI di reindirizzamento deve avere uno schema e un percorso. percorso di Hello deve contenere almeno una barra rovesciata dopo dominio hello (ad esempio, //contoso/ works e ha esito negativo //contoso).

Verificare che non sono presenti caratteri speciali come carattere di sottolineatura hello uri di reindirizzamento.

### <a name="faulted-apps"></a>App con errori

Le applicazioni B2C NON devono essere modificate:

* In altri portali di gestione delle applicazioni, tra cui il [portale di Azure classico](https://manage.windowsazure.com/) o il [portale di registrazione delle applicazioni](https://apps.dev.microsoft.com/).
* Usando l'API Graph o PowerShell

Se si modifica un'applicazione hello B2C come descritto in precedenza e provare tooedit nuovamente nel Pannello di Azure Active Directory B2C hello funzionalità nel portale di Azure di hello, diventa un'app di errore e l'applicazione non è più utilizzabile con Azure Active Directory B2C. Si dispone di un'applicazione hello toodelete e crearne uno nuovo.

app hello toodelete, andare toohello [portale di registrazione applicazione](https://apps.dev.microsoft.com/) ed eliminare l'applicazione hello non esiste. Affinché toobe applicazione hello visibile, è necessario proprietario hello toobe dell'applicazione hello (e non solo un amministratore del tenant hello).

## <a name="next-steps"></a>Passaggi successivi

Dopo aver creato un'applicazione registrata con Azure Active Directory B2C, è possibile completare una delle [le esercitazioni introduttive](active-directory-b2c-overview.md#get-started) tooget attivo e in esecuzione.

> [!div class="nextstepaction"]
> [Creare un'app Web ASP.NET con iscrizione, accesso e reimpostazione della password](active-directory-b2c-devquickstarts-web-dotnet-susi.md)