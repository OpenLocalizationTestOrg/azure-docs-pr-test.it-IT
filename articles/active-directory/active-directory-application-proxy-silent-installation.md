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
# <a name="silently-install-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="89443-103">Installare automaticamente hello connettore del Proxy dell'applicazione AD Azure</span><span class="sxs-lookup"><span data-stu-id="89443-103">Silently install hello Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="89443-104">Si desidera toosend di toobe in grado di creare script di un'installazione toomultiple server o Windows Server tooWindows che non dispongono di interfaccia utente attivata.</span><span class="sxs-lookup"><span data-stu-id="89443-104">You want toobe able toosend an installation script toomultiple Windows servers or tooWindows Servers that don't have user interface enabled.</span></span> <span data-ttu-id="89443-105">In questo argomento viene illustrato come creare uno script di Windows PowerShell che consente l'installazione automatica e la registrazione del connettore proxy di applicazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89443-105">This topic helps you create a Windows PowerShell script that enables unattended installation and registration for your Azure AD Application Proxy Connector.</span></span>

<span data-ttu-id="89443-106">Questa funzionalità è utile quando si vuole:</span><span class="sxs-lookup"><span data-stu-id="89443-106">This capability is useful when you want to:</span></span>

* <span data-ttu-id="89443-107">Installare il connettore di hello in computer con nessun livello dell'interfaccia utente o quando non è possibile macchina toohello RDP.</span><span class="sxs-lookup"><span data-stu-id="89443-107">Install hello connector on machines with no UI layer or when you cannot RDP toohello machine.</span></span>
* <span data-ttu-id="89443-108">Installare e registrare più connettori in una sola volta.</span><span class="sxs-lookup"><span data-stu-id="89443-108">Install and register many connectors at once.</span></span>
* <span data-ttu-id="89443-109">Integrare l'installazione del connettore hello e la registrazione come parte di un'altra routine.</span><span class="sxs-lookup"><span data-stu-id="89443-109">Integrate hello connector installation and registration as part of another procedure.</span></span>
* <span data-ttu-id="89443-110">Creare un'immagine server standard che contiene un connettore di hello bit ma non è registrata.</span><span class="sxs-lookup"><span data-stu-id="89443-110">Create a standard server image that contains hello connector bits but is not registered.</span></span>

<span data-ttu-id="89443-111">Proxy dell'applicazione funziona con l'installazione di un servizio di Windows Server sottile denominato hello connettore all'interno della rete.</span><span class="sxs-lookup"><span data-stu-id="89443-111">Application Proxy works by installing a slim Windows Server service called hello Connector inside your network.</span></span> <span data-ttu-id="89443-112">Per toowork connettore Proxy dell'applicazione hello dispone toobe registrato con la directory di Azure AD e password di amministratore globale.</span><span class="sxs-lookup"><span data-stu-id="89443-112">For hello Application Proxy Connector toowork it has toobe registered with your Azure AD directory using a global administrator and password.</span></span> <span data-ttu-id="89443-113">Queste informazioni vengono in genere immesse durante l'installazione del connettore in una finestra di dialogo popup.</span><span class="sxs-lookup"><span data-stu-id="89443-113">Ordinarily this information is entered during Connector installation in a pop-up dialog box.</span></span> <span data-ttu-id="89443-114">Tuttavia, è possibile utilizzare Windows PowerShell toocreate un tooenter oggetto credenziale le informazioni di registrazione.</span><span class="sxs-lookup"><span data-stu-id="89443-114">However, you can use Windows PowerShell toocreate a credential object tooenter your registration information.</span></span> <span data-ttu-id="89443-115">Oppure è possibile creare il proprio token e usarlo tooenter le informazioni di registrazione.</span><span class="sxs-lookup"><span data-stu-id="89443-115">Or you can create your own token and use it tooenter your registration information.</span></span>

## <a name="install-hello-connector"></a><span data-ttu-id="89443-116">Installare il connettore hello</span><span class="sxs-lookup"><span data-stu-id="89443-116">Install hello connector</span></span>
<span data-ttu-id="89443-117">Installare i file MSI connettore hello senza registrare hello connettore, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="89443-117">Install hello Connector MSIs without registering hello Connector as follows:</span></span>

1. <span data-ttu-id="89443-118">Aprire un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="89443-118">Open a command prompt.</span></span>
2. <span data-ttu-id="89443-119">Eseguire hello in cui hello /q significa che l'installazione non interattiva di comando seguente: hello installazione non richiede hello tooaccept contratto di licenza.</span><span class="sxs-lookup"><span data-stu-id="89443-119">Run hello following command in which hello /q means quiet installation - hello installation doesn't prompt you tooaccept hello End-User License Agreement.</span></span>
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-hello-connector-with-azure-ad"></a><span data-ttu-id="89443-120">Registrare il connettore di hello con Azure AD</span><span class="sxs-lookup"><span data-stu-id="89443-120">Register hello connector with Azure AD</span></span>
<span data-ttu-id="89443-121">Esistono due metodi è possibile utilizzare il connettore di hello tooregister:</span><span class="sxs-lookup"><span data-stu-id="89443-121">There are two methods you can use tooregister hello connector:</span></span>

* <span data-ttu-id="89443-122">Registrare il connettore di hello utilizzando un oggetto credenziali di Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="89443-122">Register hello connector using a Windows PowerShell credential object</span></span>
* <span data-ttu-id="89443-123">Registrare il connettore di hello usando un token creato non in linea</span><span class="sxs-lookup"><span data-stu-id="89443-123">Register hello connector using a token created offline</span></span>

### <a name="register-hello-connector-using-a-windows-powershell-credential-object"></a><span data-ttu-id="89443-124">Registrare il connettore di hello utilizzando un oggetto credenziali di Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="89443-124">Register hello connector using a Windows PowerShell credential object</span></span>
1. <span data-ttu-id="89443-125">Creare l'oggetto credenziali di Windows PowerShell hello eseguendo questo comando.</span><span class="sxs-lookup"><span data-stu-id="89443-125">Create hello Windows PowerShell Credentials object by running this command.</span></span> <span data-ttu-id="89443-126">Sostituire  *\<username\>*  e  *\<password\>*  con hello username e password per la directory:</span><span class="sxs-lookup"><span data-stu-id="89443-126">Replace *\<username\>* and *\<password\>* with hello username and password for your directory:</span></span>
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. <span data-ttu-id="89443-127">Andare troppo**connettore del Proxy App C:\Program Files\Microsoft AAD** ed eseguire script hello hello PowerShell utilizzando le credenziali dell'oggetto è stato creato.</span><span class="sxs-lookup"><span data-stu-id="89443-127">Go too**C:\Program Files\Microsoft AAD App Proxy Connector** and run hello script using hello PowerShell credentials object you created.</span></span> <span data-ttu-id="89443-128">Sostituire *$cred* con nome hello di hello PowerShell le credenziali dell'oggetto è stato creato:</span><span class="sxs-lookup"><span data-stu-id="89443-128">Replace *$cred* with hello name of hello PowerShell credentials object you created:</span></span>
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-hello-connector-using-a-token-created-offline"></a><span data-ttu-id="89443-129">Registrare il connettore di hello usando un token creato non in linea</span><span class="sxs-lookup"><span data-stu-id="89443-129">Register hello connector using a token created offline</span></span>
1. <span data-ttu-id="89443-130">Creare un token non in linea utilizzando classe AuthenticationContext hello utilizzando i valori hello nel frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="89443-130">Create an offline token using hello AuthenticationContext class using hello values in hello code snippet:</span></span>

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


2. <span data-ttu-id="89443-131">Dopo aver creato il token hello, creare SecureString tramite token hello:</span><span class="sxs-lookup"><span data-stu-id="89443-131">Once you have hello token, create a SecureString using hello token:</span></span>

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. <span data-ttu-id="89443-132">Hello esecuzione comando di Windows PowerShell seguente, sostituendo \<GUID del tenant\> con l'ID di directory:</span><span class="sxs-lookup"><span data-stu-id="89443-132">Run hello following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span></span>

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a><span data-ttu-id="89443-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="89443-133">Next steps</span></span> 
* [<span data-ttu-id="89443-134">Pubblicare applicazioni mediante il proprio nome di dominio</span><span class="sxs-lookup"><span data-stu-id="89443-134">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="89443-135">Abilitare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="89443-135">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="89443-136">Risolvere i problemi che si verificano con il proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="89443-136">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)


