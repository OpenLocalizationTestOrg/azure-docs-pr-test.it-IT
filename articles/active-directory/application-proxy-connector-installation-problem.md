---
title: l'installazione aaaProblem hello connettore agente Proxy dell'applicazione | Documenti Microsoft
description: "Come tootroubleshoot problemi potrà faccia durante l'installazione di hello connettore agente Proxy di applicazione"
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
ms.openlocfilehash: 07ac366a429083af0c9b87aa9df9cf3876132b90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-proxy-agent-connector"></a>Problema durante l'installazione hello connettore agente Proxy di applicazione

Connettore Proxy dell'applicazione Microsoft AAD è un componente di dominio interno che utilizza la connettività di hello tooestablish le connessioni in uscita dal dominio interno toohello hello cloud endpoint disponibile.

## <a name="general-problem-areas-with-connector-installation"></a>Aree problematiche generali con l'installazione del connettore

Quando l'installazione di hello di un connettore non riesce, causa radice di hello è in genere una delle seguenti aree hello:

1.  **Connettività** – toocomplete una corretta installazione hello nuovo connettore esigenze tooregister e stabilire le proprietà di attendibilità future. Questa operazione viene eseguita tramite la connessione toohello servizio cloud Proxy dell'applicazione AAD.

2.  **Creazione del trust** – nuovo connettore hello crea un certificato autofirmato e registra il servizio di cloud toohello.

3.  **L'autenticazione di salve** : durante l'installazione, hello utente deve fornire le credenziali di amministratore l'installazione del connettore toocomplete hello.

## <a name="verify-connectivity-toohello-cloud-application-proxy-service-and-microsoft-login-page"></a>Verifica del servizio Proxy di applicazione Cloud toohello di connettività e di pagine di Login Microsoft

**Obiettivo:** verificare tale macchina connettore hello possa connettersi a endpoint di registrazione AAD Application Proxy toohello come pagina di accesso di Microsoft.

1.  Aprire toohello un browser e andare seguente pagina web: <https://aadap-portcheck.connectorporttest.msappproxy.net> , verificare che tooCentral connettività hello Stati Uniti e funzioni di Data Center Stati Uniti orientali con porte 9090 e 9091.

2.  Se le porte non è riuscita (non dispone di un segno di spunta verde), verificare che hello Firewall o proxy back-end ha \*. msappproxy.net con porte 9090 e 9091 definito correttamente.

3.  Aprire un browser (scheda separata) e passare toohello seguente pagina web: <https://login.microsoftonline.com>, assicurarsi che si può eseguire l'accesso toothat pagina.

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a>Verificare che il computer e i componenti di back-end supportino il certificato di attendibilità proxy dell'applicazione

**Obiettivo:** verificare che macchina connettore hello, back-end proxy e firewall supporti certificato hello creato tramite il connettore di hello per trust future.

>[!NOTE]
>connettore Hello tenta toocreate un certificato SHA512 supportato da TLS 1.2. Se la macchina hello o firewall back-end hello e proxy non supporta TLS 1.2, l'installazione di hello non riuscire.
>
>

**problema di hello tooresolve:**

1.  Verificare che la macchina hello supporta TLS 1.2: le versioni di tutte le finestre dopo 2012 R2 devono supportare TLS 1.2. Se il computer del connettore da una versione del 2012 R2 o precedente, assicurarsi che tale hello Knowledge Base seguente vengono installati nel computer di hello: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2>

2.  Contattare l'amministratore di rete e richiedere tooverify che firewall e proxy di back-end hello non blocchino SHA512 per il traffico in uscita.

## <a name="verify-admin-is-used-tooinstall-hello-connector"></a>Verificare amministrazione viene utilizzato tooinstall hello connettore

**Obiettivo:** verificare che un utente di hello che tenta di connettore hello tooinstall sia un amministratore con le credenziali corrette. Attualmente, utente hello deve essere un amministratore globale per hello installazione toosucceed.

**le credenziali di hello tooverify sono corrette:**

Connettersi troppo<https://login.microsoftonline.com> e utilizzare hello stesse credenziali. Verificare che l'account di accesso hello ha esito positivo. È possibile verificare il ruolo di utente hello passando troppo**Azure Active Directory**  - &gt; **utenti e gruppi**  - &gt; **tutti gli utenti**. 

Selezionare l'account utente, quindi "ruolo della Directory" nel menu di hello risultante. Verificare che il ruolo selezionato hello "Amministratore globale". Se si è grado tooaccess qualsiasi hello pagine lungo questi passaggi, non è un amministratore globale.

## <a name="next-steps"></a>Passaggi successivi
[Comprendere i connettori del proxy applicazione Azure AD](application-proxy-understand-connectors.md)
