---
title: "Servizio Web App Mobile Server di autenticazione a più fattori aaaAzure | Documenti Microsoft"
description: app Microsoft Authenticator Hello offre un'opzione di autenticazione fuori banda aggiuntiva.  Consente di hello toousers le notifiche push MFA server toouse.
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 6c8d6fcc-70f4-4da4-9610-c76d66635b8b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 4175b68fcbf85ec3fd53d8edf4e07306c75a4c71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-mobile-app-authentication-with-azure-multi-factor-authentication-server"></a>Abilitare l'autenticazione con il server Azure Multi-Factor Authentication

app Microsoft Authenticator Hello offre un'opzione di verifica fuori banda aggiuntiva. Invece di effettuare una chiamata automatizzata o utente toohello SMS durante l'accesso, Azure multi-Factor Authentication inserisce un'app di Microsoft Authenticator notifica toohello dell'utente hello smartphone o sul tablet. Hello utente tocca semplicemente **verificare** (o immette il PIN e tocca "Esegui autenticazione") in hello app toocomplete loro Accedi.

Quando la ricezione del telefono non è affidabile, è preferibile usare un'app per dispositivi mobili per la verifica in due passaggi. Se si utilizza l'applicazione hello come un generatore di token OATH, non richiede una connessione di rete o internet.

A seconda dell'ambiente, è consigliabile toodeploy servizio web app per dispositivi mobili di hello in hello nello stesso server come Server Azure multi-Factor Authentication o in un altro server con connessione internet.

## <a name="requirements"></a>Requisiti

app Microsoft Authenticator hello toouse seguente hello sono necessarie affinché hello app in grado di comunicare con il servizio Web App Mobile:

* Server Azure Multi-Factor Authentication v6.0 o versioni successive
* Installare il servizio Web app per dispositivi mobili in un server Web con connessione Internet che esegue Microsoft® [Internet Information Services (IIS) 7.x o versione successiva](http://www.iis.net/)
* ASP.NET v 4.0.30319 è installato, registrato e impostato tooAllowed
* I servizi ruolo obbligatori includono ASP.NET e Compatibilità metabase IIS 6
* Il servizio Web app per dispositivi mobili deve essere accessibile tramite un URL pubblico
* Il servizio Web app per dispositivi mobili deve essere protetto con un certificato SSL.
* Installare hello Azure multi-Factor Authentication Web Service SDK in IIS 7. x o versione successiva hello **nello stesso server hello del Server Azure multi-Factor Authentication**
* Hello Azure multi-Factor Authentication Web Service SDK è protetto con un certificato SSL.
* Servizio Web App mobile può connettersi toohello Azure multi-Factor Authentication Web Service SDK tramite SSL
* Servizio Web App mobile può autenticare toohello SDK servizi Web di Azure MFA con hello credenziali di un account di servizio che è un membro del gruppo di sicurezza "PhoneFactor Admins" hello. Questo account del servizio e il gruppo esistono in Active Directory se hello del Server Azure multi-Factor Authentication è in un server di dominio. Questo account del servizio e il gruppo esistono in locale sul Server Azure multi-Factor Authentication hello in caso contrario tooa aggiunti a un dominio.

## <a name="install-hello-mobile-app-web-service"></a>Installare il servizio web app per dispositivi mobili hello

Prima di installare servizio web app per dispositivi mobili di hello, tenere hello seguenti dettagli:

* È necessario un account del servizio che fa parte del gruppo "PhoneFactor Admins". Questo account può essere identico a quello hello uno utilizzato per l'installazione di portale per gli utenti hello hello.
* È utile tooopen un web browser nel server web con connessione Internet di hello e passare toohello URL di Web Service SDK immesso nel file Web. config hello hello. Se il browser hello può accedere correttamente a servizio web toohello, venga chiesto di credenziali. Immettere nome utente hello e la password precedentemente immessi nel file Web. config hello esattamente come appaiono nel file hello. Assicurarsi che non vengano visualizzati errori o avvisi relativi al certificato.
* Se un proxy inverso o un firewall si trova davanti al server web di servizio Web App Mobile hello che esegue SSL offloading, è possibile modificare i file Web. config di servizio Web App Mobile hello in modo che hello servizio Web App Mobile di usare http anziché https. SSL è sempre necessario dall'hello proxy firewall/inversa toohello di App per dispositivi mobili. Aggiungere hello seguente toohello chiave \<appSettings\> sezione:

        <add key="SSL_REQUIRED" value="false"/>

### <a name="install-hello-web-service-sdk"></a>Installare il SDK servizi web di hello

In entrambi gli scenari, se hello Azure multi-Factor Authentication Web Service SDK è **non** già installati nel Server Azure multi-Factor Authentication (MFA) hello, hello completato i passaggi che seguono.

1. Aprire la console di Server multi-Factor Authentication hello.
2. Passare toohello **Web Service SDK** e selezionare **installare Web Service SDK**.
3. Installazione completa di hello utilizzando le impostazioni predefinite di hello a meno che non è necessario toochange per qualche motivo.
4. Associare un sito di toohello certificato SSL in IIS.

Se hai domande sulla configurazione di un certificato SSL in un server IIS, vedere l'articolo hello [come configurare SSL in IIS tooSet](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

Hello Web Service SDK deve essere protetto con un certificato SSL. Un certificato autofirmato è accettabile per questo scopo. Importare il certificato di hello nell'archivio "Autorità di certificazione" hello dell'account Computer locale hello server web del portale per gli utenti hello in modo da considerare attendibile tale certificato quando si avvia una connessione SSL hello.

![Configurazione del server MFA, SDK servizio Web](./media/multi-factor-authentication-get-started-server-webservice/sdk.png)

### <a name="install-hello-service"></a>Installare il servizio hello

1. **Nel Server di autenticazione a più fattori hello**, individuare il percorso di installazione toohello.
2. Passare toohello cartella in cui hello Azure MFA Server predefinito installato hello è **c:\Programmi\Microsoft c:\programmi\azure multi-Factor Authentication**.
3. Individuare il file di installazione di hello **MultiFactorAuthenticationMobileAppWebServiceSetup64**. Se il server di hello **non** con connessione Internet, il server di accesso a Internet toohello copia hello installazione file.
4. Se hello Server MFA è **non** switch con connessione internet toohello **server con connessione internet**.
5. Eseguire hello **MultiFactorAuthenticationMobileAppWebServiceSetup64** installare file come amministratore, se si desidera modificare hello del sito e modificare nome breve tooa directory virtuale hello se si desidera.
6. Dopo il completamento dell'installazione, hello Sfoglia troppo**C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService** (o alla directory appropriata in base al nome di directory virtuale hello) e modificare file Web. config hello.

   * Trovare la chiave di hello **"WEB_SERVICE_SDK_AUTHENTICATION_USERNAME"** e modificare **valore = ""** troppo**valore = "Dominio\nomeutente"** dove dominio\utente è un Account del servizio che fa parte di Gruppo "Amministratori di PhoneFactor".
   * Trovare la chiave di hello **"WEB_SERVICE_SDK_AUTHENTICATION_PASSWORD"** e modificare **valore = ""** troppo**valore = "Password"** in cui Password è hello per hello servizio Account specificato nella riga precedente hello.
   * Trovare hello **impostazione pfMobile App Web Service_pfwssdk_PfWsSdk** impostare e modificare il valore di hello da **http://hostlocale:4898/pfwssdk.asmx** toohello URL SDK servizio Web (esempio: https://mfa.contoso.com/ MultiFactorAuthWebServiceSdk/PfWsSdk.asmx).
   * Salvare i file Web. config hello e chiudere il blocco note.

   > [!NOTE]
   > Poiché SSL viene utilizzato per questa connessione, è necessario fare riferimento hello Web Service SDK con **il nome di dominio completo (FQDN)** e **non l'indirizzo IP**. Hello certificato SSL sarebbe rilasciato per hello FQDN e hello URL utilizzato deve corrispondere hello nome sul certificato hello.

7. Se il sito Web di hello installati nel servizio Web App Mobile non è già associato con un certificato firmato pubblicamente, installare hello certificato nel server di hello, aprire Gestione IIS e associare sito Web di toohello certificato hello.
8. Aprire un web browser da qualsiasi computer, quindi spostarsi toohello URL in cui è stato installato il servizio Web App Mobile (esempio: https://mfa.contoso.com/MultiFactorAuthMobileAppWebService). Assicurarsi che non vengano visualizzati errori o avvisi relativi al certificato.

## <a name="configure-hello-mobile-app-settings-in-hello-azure-multi-factor-authentication-server"></a>Configurare le impostazioni di app per dispositivi mobili hello in hello del Server Azure multi-Factor Authentication

Ora che servizio web app per dispositivi mobili di hello è installato, è necessario tooconfigure hello del Server Azure multi-Factor Authentication toowork con il portale di hello.

1. Nella console di Server multi-Factor Authentication hello, fare clic sull'icona portale per gli utenti di hello. Se gli utenti sono autorizzati toocontrol controllare i propri metodi di autenticazione, **App Mobile** nella scheda Impostazioni hello in **consentire agli utenti il metodo tooselect**. Senza questa funzionalità è abilitata, gli utenti finali sono necessari toocontact l'attivazione di toocomplete dell'Help Desk per hello App per dispositivi mobili.
2. Controllare hello **consentire agli utenti tooactivate App Mobile** casella.
3. Controllare hello **Consenti registrazione utente** casella.
4. Fare clic su hello **App Mobile** icona.
5. Immettere l'URL di hello viene utilizzato con la directory virtuale hello creato durante l'installazione di MultiFactorAuthenticationMobileAppWebServiceSetup64 (esempio: https://mfa.contoso.com/MultiFactorAuthMobileAppWebService/) nel campo hello  **URL del servizio Web App mobile:**.
6. Popolare hello **nome Account** campo toodisplay di nome di società o organizzazione hello in un'applicazione hello per dispositivi mobili per questo account.
   ![Impostazioni dell'app per dispositivi mobili per la configurazione del server MFA](./media/multi-factor-authentication-get-started-server-webservice/mobile.png)

## <a name="next-steps"></a>Passaggi successivi

- [Scenari avanzati con Azure Multi-Factor Authentication e soluzioni VPN di terze parti](multi-factor-authentication-advanced-vpn-configurations.md).