---
title: aaaUpgrade PhoneFactor tooAzure Server MFA | Documenti Microsoft
description: Introduzione a Azure MFA Server quando esegue l'aggiornamento dall'agente phonefactor precedente hello.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 42838ff7-bdf2-4d06-bacc-b3839a00cd76
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.openlocfilehash: 15b7b8517929c30f66e6a39cd44c69d12d25c6d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hello-phonefactor-agent-tooazure-multi-factor-authentication-server"></a>Aggiornamento hello agente PhoneFactor tooAzure Server multi-Factor Authentication
tooupgrade hello agente PhoneFactor versione 5. x o precedenti tooAzure Server multi-Factor Authentication, disinstallare l'agente PhoneFactor hello e associato prima di componenti. Quindi hello Server multi-Factor Authentication e possono essere installati i componenti associati.

## <a name="uninstall-hello-phonefactor-agent"></a>Disinstallare l'agente PhoneFactor hello

1. Per eseguire il backup del file di dati di hello PhoneFactor. il percorso di installazione di Hello predefinito è c:\Programmi\Microsoft Files\PhoneFactor\Data\Phonefactor.pfdata.

2. Se è installato hello portale per gli utenti:
  1. Passare la cartella di installazione toohello ed eseguire il backup dei file Web. config hello. il percorso di installazione di Hello predefinito è c:\inetpub\wwwroot\phonefactor.

  2. Se sono stati aggiunti portale toohello temi personalizzati, eseguire il backup della cartella personalizzata directory c:\inetpub\wwwroot\phonefactor\app_themes. hello.

  3. Disinstallare hello portale per gli utenti tramite hello agente PhoneFactor (disponibile solo se è installato in hello nello stesso server hello agente PhoneFactor) o tramite programmi di Windows e funzionalità.

3. Se è installato il servizio Web App Mobile hello:

  1. Passare la cartella di installazione toohello ed eseguire il backup dei file Web. config hello. il percorso di installazione di Hello predefinito è c:\inetpub\wwwroot\phonefactorphoneappwebservice.

  2. Disinstallare hello servizio Web App per dispositivi mobili tramite programmi di Windows e funzionalità.

4. Se hello Web Service SDK è installato, disinstallarlo tramite hello agente PhoneFactor o programmi di Windows e funzionalità.

5. Disinstallare hello agente PhoneFactor tramite programmi di Windows e funzionalità.

## <a name="install-hello-multi-factor-authentication-server"></a>Installare hello Server multi-Factor Authentication

Hello percorso di installazione viene prelevato dal Registro di sistema di hello dall'installazione dell'agente PhoneFactor precedente hello, pertanto è necessario installare hello stesso percorso (ad esempio, c:\Programmi\Microsoft Files\PhoneFactor). Le nuove installazioni hanno un percorso di installazione predefinito diverso, ad esempio C:\Programmi\Multi-Factor Authentication Server. Hello file di dati lasciati dall'agente PhoneFactor devono essere aggiornati durante l'installazione, in modo le impostazioni e gli utenti dovrebbero essere ancora che presente dopo l'installazione di hello nuova Server multi-Factor Authentication hello precedente.

1. Se richiesto, attivare hello Server multi-Factor Authentication e assicurarsi che venga assegnato il gruppo di replica corretto toohello.

2. Se Web Service SDK è stato installato in precedenza, hello installa hello nuovi SDK di servizi Web tramite l'interfaccia utente del Server multi-Factor Authentication hello.

  impostazione predefinita il nome di directory virtuale è adesso Hello **MultiFactorAuthWebServiceSdk** anziché **PhoneFactorWebServiceSdk**. Se si desidera toouse hello precedente nome, è necessario modificare il nome di hello della directory virtuale hello durante l'installazione. In caso contrario, se si consente a hello installazione toouse hello nuovo nome predefinito, è necessario toochange hello URL in tutte le applicazioni che hello riferimento SDK servizi Web (ad esempio hello portale per gli utenti e servizio Web App Mobile) toopoint nella posizione corretta hello.

3. Se installa portale per gli utenti precedentemente installato nel Server agente PhoneFactor, hello hello hello portale utenti di multi-Factor Authentication nuovo tramite l'interfaccia utente del Server multi-Factor Authentication hello.

  impostazione predefinita il nome di directory virtuale è adesso Hello **MultiFactorAuth** anziché **PhoneFactor**. Se si desidera toouse hello precedente nome, è necessario modificare il nome di hello della directory virtuale hello durante l'installazione. In caso contrario, se si consente hello installazione toouse hello nuovo nome predefinito, è necessario fare clic sull'icona portale per gli utenti hello hello Server multi-Factor Authentication e aggiornare hello URL portale utenti nella scheda Impostazioni hello.

4. Se in precedenza hello portale per gli utenti e/o al servizio Web App Mobile è stato installato in un server diverso da hello agente PhoneFactor:

  1. Passare il percorso di installazione toohello (ad esempio, c:\Programmi\Microsoft Files\PhoneFactor) e copiare toohello programmi di installazione di uno o più altri server. Sono disponibili i programmi di installazione a 32 e 64 bit per hello portale per gli utenti e servizio Web App Mobile. Si chiamano MultiFactorAuthenticationUserPortalSetupXX.msi e MultiFactorAuthenticationMobileAppWebServiceSetupXX.msi.

  2. tooinstall hello portale per gli utenti nel server web hello, aprire un prompt dei comandi come amministratore ed eseguire MultiFactorAuthenticationUserPortalSetupXX.msi.

    impostazione predefinita il nome di directory virtuale è adesso Hello **MultiFactorAuth** anziché **PhoneFactor**. Se si desidera toouse hello precedente nome, è necessario modificare il nome di hello della directory virtuale hello durante l'installazione. In caso contrario, se si consente hello installazione toouse hello nuovo nome predefinito, è necessario fare clic sull'icona portale per gli utenti hello hello Server multi-Factor Authentication e aggiornare hello URL portale utenti nella scheda Impostazioni hello. Gli utenti esistenti devono toobe informato di hello nuovo URL.

  3. Andare toohello percorso di installazione portale per gli utenti (ad esempio C:\inetpub\wwwroot\MultiFactorAuth) e modificare file Web. config hello. Copiare i valori hello hello sezioni appSettings e applicationSettings del file Web. config originale che è stato eseguito il backup prima dell'aggiornamento hello in nuovo file Web. config di hello. Se il nuovo nome di directory virtuale predefinito di hello è stato mantenuto durante l'installazione di hello Web Service SDK, modificare l'URL di hello nella posizione corretta di hello applicationSettings sezione toopoint toohello. Se altre impostazioni predefinite sono state modificate nel file Web. config precedente hello, si applicano le stesse modifiche toohello file Web. config.

  4. tooinstall hello, servizio Web App Mobile nel server web hello, aprire un prompt dei comandi come amministratore ed eseguire MultiFactorAuthenticationMobileAppWebServiceSetupXX.msi hello.

    impostazione predefinita il nome di directory virtuale è adesso Hello **MultiFactorAuthMobileAppWebService** anziché **PhoneFactorPhoneAppWebService**. Se si desidera toouse hello precedente nome, è necessario modificare il nome di hello della directory virtuale hello durante l'installazione. È possibile toochoose un toomake nome più breve è più facile per gli utenti finali tootype nei dispositivi mobili. In caso contrario, se si consente hello installazione toouse hello nuovo nome predefinito, è necessario fare clic sull'icona App Mobile hello hello Server multi-Factor Authentication e aggiornare hello URL del servizio Web App Mobile.

  5. Passare a percorso di installazione di servizio Web App Mobile toohello (ad esempio C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService) e modificare file Web. config hello. Copiare i valori hello hello sezioni appSettings e applicationSettings del file Web. config originale che è stato eseguito il backup prima dell'aggiornamento hello in nuovo file Web. config di hello. Se il nuovo nome di directory virtuale predefinito di hello è stato mantenuto durante l'installazione di hello Web Service SDK, modificare l'URL di hello nella posizione corretta di hello applicationSettings sezione toopoint toohello. Se altre impostazioni predefinite sono state modificate nel file Web. config precedente hello, si applicano le stesse modifiche toohello file Web. config.

## <a name="next-steps"></a>Passaggi successivi

- [Installare portale per gli utenti hello](multi-factor-authentication-get-started-portal.md) per hello del Server Azure multi-Factor Authentication.

- [Configurare l'autenticazione di Windows](multi-factor-authentication-get-started-server-windows.md) per le applicazioni. 
