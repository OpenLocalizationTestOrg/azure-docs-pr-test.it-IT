---
title: aaaTranslate collegamenti e gli URL Azure AD App Proxy | Documenti Microsoft
description: Nozioni fondamentali di hello include informazioni sui connettori Proxy di applicazione di Azure AD.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7ec2b9fb01617067cf5d676037877bf72c19217b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="redirect-hardcoded-links-for-apps-published-with-azure-ad-application-proxy"></a>Reindirizzare i collegamenti hardcoded per le app pubblicate con il proxy di app di Azure AD

Proxy dell'applicazione AD Azure rende il toousers di disponibili App locale o remoto con i propri dispositivi. Alcune applicazioni, tuttavia, sono state sviluppate con collegamenti locali incorporati in hello HTML. Questi collegamenti non funzionano correttamente quando l'applicazione hello viene usato in remoto. Quando si dispone di più sedi applicazioni punto tooeach altri, gli utenti si aspettano hello collegamenti tookeep funziona se non si trovano nell'ufficio hello. 

Hello migliore modo toomake verificare che il collegamento funzioni hello stesso sia all'interno e all'esterno della rete aziendale sia tooconfigure hello URL esterni di toobe l'App stessa hello come i relativi URL interno. Utilizzare [domini personalizzati](active-directory-application-proxy-custom-domains.md) tooconfigure il toohave URL esterno anziché dominio proxy di applicazione predefinito hello assegnare un nome del dominio aziendale.

Se non è possibile utilizzare i domini personalizzati nel tenant, funzionalità di traduzione di collegamento hello del Proxy dell'applicazione mantiene i collegamenti di lavorare indipendentemente in cui gli utenti. Quando si dispongono di applicazioni che fanno riferimento direttamente toointernal endpoint o porte, è possibile associare questi toohello URL interno pubblicato URL Proxy dell'applicazione esterna. Quando è abilitata la traslazione del collegamento e il Proxy dell'applicazione ricerca tramite HTML, CSS e seleziona i tag di JavaScript per i collegamenti interni pubblicati. Quindi hello servizio Proxy applicazione li converte in modo che gli utenti di ottenere un'esperienza senza interruzioni.

>[!NOTE]
>Hello funzionalità di traduzione di collegamento è per i tenant che, per qualsiasi motivo, non è possibile usare i domini personalizzati toohave hello stesso URL interni ed esterni per le app. Prima di abilitare questa funzionalità, verificare se i [domini personalizzati nel proxy di applicazione di Azure AD](active-directory-application-proxy-custom-domains.md) possono fare al caso.
>
>In alternativa, se un'applicazione hello è necessario tooconfigure con conversione dei collegamenti di SharePoint, vedere [configurare i mapping di accesso alternativo per SharePoint 2013](https://technet.microsoft.com/library/cc263208.aspx) per i collegamenti di un altro approccio toomapping.

## <a name="how-link-translation-works"></a>Come funziona la conversione dei collegamenti

Dopo l'autenticazione, quando il server proxy hello passa utente toohello dati dell'applicazione hello, Proxy applicazione esegue l'analisi di un'applicazione hello per i collegamenti hardcoded e li sostituisce con i rispettivi URL esterni pubblicato.

Il Proxy dell'applicazione presuppone che le applicazioni vengano codificate in UTF-8. Se non è questo caso di hello, specificare il tipo di codifica hello in un'intestazione di risposta http, ad esempio `Content-Type:text/html;charset=utf-8`.

### <a name="which-links-are-affected"></a>Quali collegamenti sono interessati?

funzionalità di traduzione di collegamento Hello è solo per i collegamenti contenuti nel tag di codice nel corpo di hello di un'app. Il proxy di applicazione ha una funzione separata per la conversione dei cookie o URL in intestazioni. 

Esistono due tipi comuni di collegamenti interni nelle applicazioni locali:

- **I collegamenti interni relativi** tooa tale punto condiviso in una struttura di file locale come risorsa `/claims/claims.html`. Questi collegamenti vengono attivati automaticamente nelle App che vengono pubblicate tramite Proxy di applicazione e continuare toowork con o senza conversione dei collegamenti. 
- **I collegamenti interni hardcoded** tooother locale App come `http://expenses` o i file come pubblicati `http://expenses/logo.jpg`. funzionalità di traduzione di collegamento Hello funziona per i collegamenti interni hardcoded e li modifica toopoint toohello URL esterni che gli utenti remoti devono toogo tramite.

### <a name="how-do-apps-link-tooeach-other"></a>Come App collegano tooeach altri?

Conversione dei collegamenti è abilitato per ogni applicazione, in modo da disporre di un controllo esperienza utente hello a livello di hello per app. Attivare la conversione dei collegamenti per un'app quando si desidera che i collegamenti di hello *da* tradotte toobe tale app, non collegamenti *a* tale app. 

Ad esempio, si supponga che le tre applicazioni pubblicate mediante il Proxy di applicazione che tutti i collegamenti tooeach altri: vantaggi e spese di viaggio. C'è una quarta app, Feedback, che non viene pubblicata tramite il proxy di applicazione.

Quando si abilita la conversione dei collegamenti per app vantaggi hello, viaggi e hello collegamenti tooExpenses sono toohello reindirizzato URL esterni per le app, ma tooFeedback collegamento hello non viene reindirizzata perché non esiste alcun URL esterno. Collegamenti dai viaggi e spese non funzionano tooBenefits indietro, in quanto la traduzione di collegamento non è stata abilitata per queste due app.

![Collegamenti da vantaggi tooother App quando è abilitata la conversione di collegamento](./media/application-proxy-link-translation/one_app.png)

### <a name="which-links-arent-translated"></a>Quali collegamenti non vengono convertiti?

sicurezza e prestazioni tooimprove, alcuni collegamenti non vengono tradotti:

- Collegamenti non interni ai tag di codice. 
- Collegamenti non in HTML, CSS o JavaScript. 
- Collegamenti interni aperti da altri programmi. I collegamenti inviati tramite posta elettronica o messaggistica istantanea o inclusi in altri documenti non vengono convertiti. gli utenti di Hello devono URL esterno di tooknow toogo toohello.

Se è necessario toosupport uno di questi due scenari, utilizzare hello stesso URL interni ed esterni invece di conversione dei collegamenti.  

## <a name="enable-link-translation"></a>Abilitare la conversione dei collegamenti

Per iniziare con la conversione dei collegamenti, è sufficiente fare clic su un pulsante:

1. Accedi toohello [portale di Azure](https://portal.azure.com) come amministratore.
2. Andare troppo**Azure Active Directory** > **applicazioni aziendali** > **tutte le applicazioni** > app hello selezionare da toomanage > **Proxy dell'applicazione**.
3. Attivare **tradurre gli URL nel corpo di applicazione** troppo**Sì**.

   ![Selezionare Sì tootranslate URL nel corpo di applicazione](./media/application-proxy-link-translation/select_yes.png).
4. Selezionare **salvare** tooapply le modifiche.

Quando gli utenti accedono a questa applicazione, proxy hello analizzi automaticamente per gli URL interni che sono stati pubblicati tramite il Proxy di applicazione per il tenant.

## <a name="send-feedback"></a>Invia commenti

Vogliamo toomake la Guida in linea questo lavoro funzionalità per tutte le app. È cercare oltre 30 tag in HTML e CSS e intende quali toosupport casi JavaScript. Se si dispone di un esempio di collegamenti generati che non sono tradotta, inviare un frammento di codice troppo[commenti e suggerimenti Proxy di applicazione](mailto:aadapfeedback@microsoft.com). 

## <a name="next-steps"></a>Passaggi successivi
[Usare i domini personalizzati con Proxy dell'applicazione AD Azure](active-directory-application-proxy-custom-domains.md) toohave hello stesso URL interni ed esterni

[Configurare i mapping di accesso alternativo per for SharePoint 2013](https://technet.microsoft.com/library/cc263208.aspx)
