---
title: "aggiornamento del Server di autenticazione a più fattori aaaAzure | Documenti Microsoft"
description: "I passaggi e la versione più recente di indicazioni tooupgrade hello del Server Azure multi-Factor Authentication tooa."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 50bb8ac3-5559-4d8b-a96a-799a74978b14
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: aaa8d400e0e5f1c6be3a6d22cde6dd893ef4d546
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-toohello-latest-azure-multi-factor-authentication-server"></a>Toohello l'aggiornamento più recente Server Azure multi-Factor Authentication

Questo articolo illustra hello processo di aggiornamento di versione 6.0 Server Azure multi-Factor Authentication (MFA) o versione successiva. Se occorre una versione precedente dell'agente PhoneFactor hello tooupgrade, fare riferimento troppo[hello aggiornamento agente PhoneFactor tooAzure Server multi-Factor Authentication](multi-factor-authentication-get-started-server-upgrade.md).

Se si esegue l'aggiornamento da v6. x o toov7.x precedenti o successive, tutti i componenti modificare da too.NET 2.0 di .NET 4.5. Inoltre per tutti i componenti è necessario l'aggiornamento di Microsoft Visual C++ 2015 1 o versione successiva. programma di installazione del Server di autenticazione a più fattori Hello installa entrambe le versioni x86 e x64 di hello di questi componenti se non sono già installati. Se hello portale per gli utenti e servizio Web App Mobile eseguite su server separati, è necessario tooinstall i pacchetti prima di aggiornare tali componenti. È possibile cercare aggiornamenti di Microsoft Visual C++ 2015 Redistributable più recenti hello sulla hello [Microsoft Download Center](https://www.microsoft.com/en-us/download/). 

## <a name="install-hello-latest-version-of-azure-mfa-server"></a>Installare una versione più recente di hello del Server di autenticazione a più fattori di Azure

1. Utilizzare le istruzioni hello [Download hello del Server Azure multi-Factor Authentication](multi-factor-authentication-get-started-server.md#download-the-azure-multi-factor-authentication-server) tooget hello più recente di hello Azure MFA Server.
2. Eseguire un backup del file di dati di Server di autenticazione a più fattori hello che si trova in c:\Programmi\Microsoft multi-Factor Authentication Server\Data\PhoneFactor.pfdata (percorso di installazione predefinito hello presupponendo) sul Server master autenticazione a più fattori.
3. Se si eseguono più server per la disponibilità elevata, è possibile modificare i sistemi client hello che eseguono l'autenticazione Server MFA toohello in modo che arrestino l'invio di traffico toohello server che esegue l'aggiornamento. Se si utilizza un bilanciamento del carico, rimuovere un Server di autenticazione a più fattori dal servizio di bilanciamento del carico hello hello aggiornamento e quindi aggiungere il server di hello in farm hello.
4. Eseguire di nuovo programma di installazione hello in ogni Server di autenticazione a più fattori. Aggiornare i server subordinati prima perché essi possono leggere hello vecchio file di dati replicati dal master hello. 

  Non è necessario toouninstall Server MFA corrente prima dell'installazione guidata di hello in esecuzione. programma di installazione di Hello esegue un aggiornamento sul posto. Hello percorso di installazione viene prelevato dal Registro di sistema di hello dall'installazione precedente di hello, per consentire un'installazione in hello stesso percorso (ad esempio, c:\Programmi\Microsoft multi-Factor Authentication Server). 
  
5. Se si tooinstall richiesto Microsoft Visual C++ 2015 update Redistributable package, accettare il messaggio hello. Entrambe le versioni x86 e x64 di hello del pacchetto di hello vengono installate.
5. Se si utilizza hello SDK servizio Web, verrà chiesto tooinstall hello nuovo SDK servizi Web. Quando si installa hello nuovo SDK servizi Web, verificare che il nome della directory virtuale hello corrisponde la directory virtuale hello installato in precedenza (ad esempio, MultiFactorAuthWebServiceSdk).
6. Ripetere i passaggi di hello in tutti i server subordinati. Alzare di livello uno dei hello subalterni toobe hello nuovo master, quindi hello aggiornamento vecchio server master. 

## <a name="upgrade-hello-user-portal"></a>Aggiornamento hello portale per gli utenti

1. Eseguire il backup di hello file Web. config nella directory virtuale di hello di hello il percorso di installazione portale per gli utenti (ad esempio C:\inetpub\wwwroot\MultiFactorAuth). Se il tema predefinito toohello eventuali modifiche, eseguire il backup della cartella nonché di hello App_Themes\Default. È preferibile toocreate una copia della cartella predefinita hello e creare un nuovo tema di tema predefinito di toochange hello.
2. Se viene eseguito il portale per gli utenti hello hello nello stesso server come hello altri componenti Server di autenticazione a più fattori, hello installazione del Server di autenticazione a più fattori richiede tooupdate hello portale per gli utenti. Accettare il prompt hello e installare l'aggiornamento del portale utente hello. Controllare che il nome della directory virtuale hello corrisponde la directory virtuale hello installato in precedenza (ad esempio, MultiFactorAuth).
3. Se hello portale per gli utenti si trova in un server, copia del file MultiFactorAuthenticationUserPortalSetup64.msi hello da hello installare percorso di uno dei server di autenticazione a più fattori hello e inserirla nel server web del portale utenti hello. Eseguire l'installazione guidata di hello. 

  Se si verifica un errore indicante, "Microsoft Visual C++ 2015 Redistributable Update 1 o versione successiva è obbligatorio," scaricare e installare il pacchetto di aggiornamento più recente di hello da hello [Microsoft Download Center](https://www.microsoft.com/download/). Installare entrambe le versioni x86 e x64 di hello.

4. Dopo l'aggiornamento di hello portale per gli utenti è installato software, confrontare il backup di Web. config hello che nel passaggio 1 con nuovo file Web. config di hello. Se è presente alcun attributo di nuovo in Web. config nuovo hello, copiare i file Web. config di backup in hello toooverwrite di directory virtuale hello uno nuovo. Un'altra opzione è toocopy/Incolla hello appSettings valori e hello URL dal file di backup hello in Web. config nuovo hello SDK del servizio Web.

Se si dispone di hello portale per gli utenti in più server, ripetere l'installazione di hello in tutte. 


## <a name="upgrade-hello-mobile-app-web-service"></a>Aggiornamento hello servizio Web App Mobile

1. Eseguire il backup di hello file Web. config nella directory virtuale di hello di hello percorso di installazione di servizio Web App Mobile (ad esempio, C:\inetpub\wwwroot\app o C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService).
2. Copia del file MultiFactorAuthenticationMobileAppWebServiceSetup64.msi hello da hello installare percorso del server di autenticazione a più fattori hello e inserirlo nel server web di registrazione App Mobile hello.
3. Eseguire l'installazione guidata di hello. 

  Se si verifica un errore che informa che è richiesto Microsoft Visual C++ 2015 Redistributable Update 1 o versione successiva, scaricare e installare il pacchetto di aggiornamento più recente di hello da hello [Microsoft Download Center](https://www.microsoft.com/download/). Installare entrambe le versioni x86 e x64 di hello.

4. Dopo aver installato il software di servizio Web App Mobile hello aggiornato, confrontare hello. config che è stato eseguito il backup nel passaggio 1 con il nuovo file di Web. config hello. Se è presente alcun attributo di nuovo in Web. config nuovo hello, è possibile copiare i file Web. config salvato alla directory virtuale hello e sovrascrivere hello uno nuovo. Un'altra opzione è toocopy/Incolla hello appSettings valori e hello URL dal file di backup hello in Web. config nuovo hello SDK del servizio Web.

Se si dispone di hello servizio Web App Mobile su più server, ripetere l'installazione di hello in tutte. 

## <a name="upgrade-hello-ad-fs-adapters"></a>Aggiornamento hello AD FS schede


### <a name="if-mfa-runs-on-different-servers-than-ad-fs"></a>Se MFA viene eseguito su server diversi da AD FS

Queste istruzioni sono valide solo se si esegue il server Multi-Factor Authentication indipendentemente dai server AD FS. Se entrambi i servizi eseguiti hello stessi server, ignorare questa sezione e passare toohello passaggi di installazione. 

1. Salvare una copia del file Multifactorauthenticationadfsadapter config hello che è stata registrata in AD FS o esportare la configurazione di hello utilizzando il comando PowerShell seguente hello: `Export-AdfsAuthenticationProviderConfigurationData -Name [adapter name] -FilePath [path tooconfig file]`. nome dell'adapter Hello è "WindowsAzureMultiFactorAuthentication" o "AzureMfaServerAuthentication" a seconda della versione di hello installata in precedenza.
2. Copiare i seguenti file da server di hello Server MFA installazione percorso toohello AD FS hello:

  - MultiFactorAuthenticationAdfsAdapterSetup64.msi
  - Register-MultiFactorAuthenticationAdfsAdapter.ps1
  - Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
  - MultiFactorAuthenticationAdfsAdapter.config

3. Modifica di script hello Register-multifactorauthenticationadfsadapter.ps1 aggiungendo `-ConfigurationFilePath [path]` toohello fine hello `Register-AdfsAuthenticationProvider` comando. Sostituire *[percorso]* con percorso completo di hello toohello multifactorauthenticationadfsadapter. config file o file di configurazione hello esportati nel passaggio precedente hello. 

  Verificare gli attributi di hello in hello nuovo Multifactorauthenticationadfsadapter toosee se corrispondono ai file di configurazione precedente hello. Se tutti gli attributi sono stati aggiunti o rimossi in una nuova versione di hello, copiare i valori di attributo hello da hello precedente configurazione file toohello uno nuovo o modificare hello precedente toomatch file di configurazione.

### <a name="install-new-ad-fs-adapters"></a>Installare le nuove schede AD FS

> [!IMPORTANT] 
> Gli utenti non saranno tooperform richiesto in due passaggi di verifica durante i passaggi 3-8 di questa sezione. Se si dispone di AD FS configurato in più cluster, è possibile rimuovere, aggiornamento e ripristino della farm in modo indipendente da ogni cluster in hello hello i tempi di inattività tooavoid altri cluster.

1. Rimuovere alcuni server AD FS dalla farm di hello. Aggiornare questi server durante hello che ad altri utenti sono ancora in esecuzione.
2. Installare la nuova scheda ADFS di hello in ogni server rimosso dalla farm di hello AD FS. Se hello MFA Server è installato in ogni server ADFS, è possibile aggiornare tramite il Server di autenticazione a più fattori salve UX. Altrimenti fare l'aggiornamento eseguendo MultiFactorAuthenticationAdfsAdapterSetup64.msi. 

  Se si verifica un errore indicante, "Microsoft Visual C++ 2015 Redistributable Update 1 o versione successiva è obbligatorio," scaricare e installare il pacchetto di aggiornamento più recente di hello da hello [Microsoft Download Center](https://www.microsoft.com/download/). Installare entrambe le versioni x86 e x64 di hello.

3. Andare troppo**ADFS** > **criteri di autenticazione** > **Modifica criteri di autenticazione a più fattori globale**. Deselezionare **WindowsAzureMultiFactorAuthentication** o **AzureMFAServerAuthentication** (a seconda della versione di hello attualmente installata). 

  Dopo avere completato questo passaggio, la verifica in due passaggi tramite il server MFA non sarà disponibile in questo cluster AD FS fino al completamento del passaggio 8.

4. Versione meno recente hello di annullare la registrazione della scheda ADFS hello Active Directory eseguendo uno script di PowerShell di Unregister-MultiFactorAuthenticationAdfsAdapter.ps1 hello. Verificare che hello *-nome* parametro ("WindowsAzureMultiFactorAuthentication" o "AzureMFAServerAuthentication") corrisponde a nome hello che è stato visualizzato nel passaggio 3. Poiché è presente una configurazione centrale, si applica tooall server nel cluster di hello stesso AD FS.
5. Registrare la nuova scheda ADFS di hello eseguendo uno script di PowerShell Register-multifactorauthenticationadfsadapter.ps1 hello. Poiché è presente una configurazione centrale, si applica tooall server nel cluster di hello stesso AD FS.
6. Hello riavvio del servizio AD FS in ogni server rimosso dal hello farm AD FS.
7. Aggiungere server hello aggiornato eseguire il backup di farm di toohello AD FS e Rimuovi hello altri server dalla farm hello.
8. Andare troppo**ADFS** > **criteri di autenticazione** > **Modifica criteri di autenticazione a più fattori globale**. Controllare **AzureMfaServerAuthentication**.
9. Ripetere il passaggio 2 tooupdate: server hello rimosso dalla farm di hello AD FS e riavviare il servizio ADFS hello AD in tali server.
10. Aggiungere i server alla farm hello AD FS.

## <a name="next-steps"></a>Passaggi successivi

- Consultare gli esempi di [Scenari avanzati con Azure Multi-Factor Authentication e VPN di terze parti](multi-factor-authentication-advanced-vpn-configurations.md)

- [Sincronizzazione del server MFA con Windows Server Active Directory](multi-factor-authentication-get-started-server-dirint.md)

- [Configurare l'autenticazione di Windows](multi-factor-authentication-get-started-server-windows.md) per le applicazioni
