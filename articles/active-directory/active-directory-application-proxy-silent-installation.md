---
title: aaaSilent installare connettore del Proxy di App di Azure AD | Documenti Microsoft
description: Descrive come un'installazione automatica di Azure Active Directory Application Proxy Connector tooprovide accesso remoto sicuro tooyour tooperform locale delle app.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3aa1c7f2-fb2a-4693-abd5-95bb53700cbb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ce796ff45a65ba7d5f0f63c02085bdc6af494548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="silently-install-hello-azure-ad-application-proxy-connector"></a>Installare automaticamente hello connettore del Proxy dell'applicazione AD Azure
Si desidera toosend di toobe in grado di creare script di un'installazione toomultiple server o Windows Server tooWindows che non dispongono di interfaccia utente attivata. In questo argomento viene illustrato come creare uno script di Windows PowerShell che consente l'installazione automatica e la registrazione del connettore proxy di applicazione di Azure AD.

Questa funzionalità è utile quando si vuole:

* Installare il connettore di hello in computer con nessun livello dell'interfaccia utente o quando non è possibile macchina toohello RDP.
* Installare e registrare più connettori in una sola volta.
* Integrare l'installazione del connettore hello e la registrazione come parte di un'altra routine.
* Creare un'immagine server standard che contiene un connettore di hello bit ma non è registrata.

Proxy dell'applicazione funziona con l'installazione di un servizio di Windows Server sottile denominato hello connettore all'interno della rete. Per toowork connettore Proxy dell'applicazione hello dispone toobe registrato con la directory di Azure AD e password di amministratore globale. Queste informazioni vengono in genere immesse durante l'installazione del connettore in una finestra di dialogo popup. Tuttavia, è possibile utilizzare Windows PowerShell toocreate un tooenter oggetto credenziale le informazioni di registrazione. Oppure è possibile creare il proprio token e usarlo tooenter le informazioni di registrazione.

## <a name="install-hello-connector"></a>Installare il connettore hello
Installare i file MSI connettore hello senza registrare hello connettore, come indicato di seguito:

1. Aprire un prompt dei comandi.
2. Eseguire hello in cui hello /q significa che l'installazione non interattiva di comando seguente: hello installazione non richiede hello tooaccept contratto di licenza.
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-hello-connector-with-azure-ad"></a>Registrare il connettore di hello con Azure AD
Esistono due metodi è possibile utilizzare il connettore di hello tooregister:

* Registrare il connettore di hello utilizzando un oggetto credenziali di Windows PowerShell
* Registrare il connettore di hello usando un token creato non in linea

### <a name="register-hello-connector-using-a-windows-powershell-credential-object"></a>Registrare il connettore di hello utilizzando un oggetto credenziali di Windows PowerShell
1. Creare l'oggetto credenziali di Windows PowerShell hello eseguendo questo comando. Sostituire  *\<username\>*  e  *\<password\>*  con hello username e password per la directory:
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. Andare troppo**connettore del Proxy App C:\Program Files\Microsoft AAD** ed eseguire script hello hello PowerShell utilizzando le credenziali dell'oggetto è stato creato. Sostituire *$cred* con nome hello di hello PowerShell le credenziali dell'oggetto è stato creato:
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-hello-connector-using-a-token-created-offline"></a>Registrare il connettore di hello usando un token creato non in linea
1. Creare un token non in linea utilizzando classe AuthenticationContext hello utilizzando i valori hello nel frammento di codice hello:

        using System;
        using System.Diagnostics;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

        class Program
        {
        #region constants
        /// <summary>
        /// hello AAD authentication endpoint uri
        /// </summary>
        static readonly Uri AadAuthenticationEndpoint = new Uri("https://login.microsoftonline.com/common/oauth2/token?api-version=1.0");

        /// <summary>
        /// hello application ID of hello connector in AAD
        /// </summary>
        static readonly string ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";

        /// <summary>
        /// hello reply address of hello connector application in AAD
        /// </summary>
        static readonly Uri ConnectorRedirectAddress = new Uri("urn:ietf:wg:oauth:2.0:oob");

        /// <summary>
        /// hello AppIdUri of hello registration service in AAD
        /// </summary>
        static readonly Uri RegistrationServiceAppIdUri = new Uri("https://proxy.cloudwebappproxy.net/registerapp");

        #endregion

        #region private members
        private string token;
        private string tenantID;
        #endregion

        public void GetAuthenticationToken()
        {
            AuthenticationContext authContext = new AuthenticationContext(AadAuthenticationEndpoint.AbsoluteUri);

            AuthenticationResult authResult = authContext.AcquireToken(RegistrationServiceAppIdUri.AbsoluteUri,
                ConnectorAppId,
                ConnectorRedirectAddress,
                PromptBehavior.Always);

            if (authResult == null || string.IsNullOrEmpty(authResult.AccessToken) || string.IsNullOrEmpty(authResult.TenantId))
            {
                Trace.TraceError("Authentication result, token or tenant id returned are null");
                throw new InvalidOperationException("Authentication result, token or tenant id returned are null");
            }

            token = authResult.AccessToken;
            tenantID = authResult.TenantId;
        }


2. Dopo aver creato il token hello, creare SecureString tramite token hello:

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. Hello esecuzione comando di Windows PowerShell seguente, sostituendo \<GUID del tenant\> con l'ID di directory:

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a>Passaggi successivi 
* [Pubblicare applicazioni mediante il proprio nome di dominio](active-directory-application-proxy-custom-domains.md)
* [Abilitare l'accesso Single Sign-On](active-directory-application-proxy-sso-using-kcd.md)
* [Risolvere i problemi che si verificano con il proxy di applicazione](active-directory-application-proxy-troubleshoot.md)


