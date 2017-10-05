---
title: Installazione automatica del connettore proxy dell'app Azure AD | Microsoft Docs
description: Viene illustrato come eseguire un'installazione automatica del connettore proxy di applicazione di Azure AD per consentire l'accesso remoto alle applicazioni locali.
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
ms.openlocfilehash: 9e28c89d8f64f0ae3d4150017ca544e606075c45
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="silently-install-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="141c5-103">Installazione automatica del connettore proxy di applicazione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="141c5-103">Silently install the Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="141c5-104">Può essere necessario inviare uno script di installazione a più server Windows o ai server Windows che non hanno l'interfaccia utente abilitata.</span><span class="sxs-lookup"><span data-stu-id="141c5-104">You want to be able to send an installation script to multiple Windows servers or to Windows Servers that don't have user interface enabled.</span></span> <span data-ttu-id="141c5-105">In questo argomento viene illustrato come creare uno script di Windows PowerShell che consente l'installazione automatica e la registrazione del connettore proxy di applicazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="141c5-105">This topic helps you create a Windows PowerShell script that enables unattended installation and registration for your Azure AD Application Proxy Connector.</span></span>

<span data-ttu-id="141c5-106">Questa funzionalità è utile quando si vuole:</span><span class="sxs-lookup"><span data-stu-id="141c5-106">This capability is useful when you want to:</span></span>

* <span data-ttu-id="141c5-107">Installare il connettore in computer senza alcun livello di interfaccia utente o quando non è possibile usare il protocollo RDP del computer.</span><span class="sxs-lookup"><span data-stu-id="141c5-107">Install the connector on machines with no UI layer or when you cannot RDP to the machine.</span></span>
* <span data-ttu-id="141c5-108">Installare e registrare più connettori in una sola volta.</span><span class="sxs-lookup"><span data-stu-id="141c5-108">Install and register many connectors at once.</span></span>
* <span data-ttu-id="141c5-109">Integrare l'installazione e la registrazione del connettore come parte di un'altra procedura.</span><span class="sxs-lookup"><span data-stu-id="141c5-109">Integrate the connector installation and registration as part of another procedure.</span></span>
* <span data-ttu-id="141c5-110">Creare un'immagine server standard che contiene i bit del connettore, ma che non è registrata.</span><span class="sxs-lookup"><span data-stu-id="141c5-110">Create a standard server image that contains the connector bits but is not registered.</span></span>

<span data-ttu-id="141c5-111">Il proxy dell’applicazione funziona mediante l'installazione di un servizio di Windows Server slim chiamato connettore all'interno della rete.</span><span class="sxs-lookup"><span data-stu-id="141c5-111">Application Proxy works by installing a slim Windows Server service called the Connector inside your network.</span></span> <span data-ttu-id="141c5-112">Per il corretto funzionamento del connettore del proxy di applicazione, è necessario registrarlo nella directory di Azure AD con un account di amministratore globale e una password.</span><span class="sxs-lookup"><span data-stu-id="141c5-112">For the Application Proxy Connector to work it has to be registered with your Azure AD directory using a global administrator and password.</span></span> <span data-ttu-id="141c5-113">Queste informazioni vengono in genere immesse durante l'installazione del connettore in una finestra di dialogo popup.</span><span class="sxs-lookup"><span data-stu-id="141c5-113">Ordinarily this information is entered during Connector installation in a pop-up dialog box.</span></span> <span data-ttu-id="141c5-114">Tuttavia, è possibile usare Windows PowerShell per creare un oggetto credenziale in modo da immettere le informazioni di registrazione.</span><span class="sxs-lookup"><span data-stu-id="141c5-114">However, you can use Windows PowerShell to create a credential object to enter your registration information.</span></span> <span data-ttu-id="141c5-115">Oppure è possibile creare un token personale e usarlo per immettere le informazioni di registrazione.</span><span class="sxs-lookup"><span data-stu-id="141c5-115">Or you can create your own token and use it to enter your registration information.</span></span>

## <a name="install-the-connector"></a><span data-ttu-id="141c5-116">Installare il connettore</span><span class="sxs-lookup"><span data-stu-id="141c5-116">Install the connector</span></span>
<span data-ttu-id="141c5-117">Per installare i file MSI del connettore senza registrare il connettore, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="141c5-117">Install the Connector MSIs without registering the Connector as follows:</span></span>

1. <span data-ttu-id="141c5-118">Aprire un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="141c5-118">Open a command prompt.</span></span>
2. <span data-ttu-id="141c5-119">Eseguire il comando seguente in cui il parametro /q significa installazione non interattiva. Durante l'installazione non viene richiesto di accettare il contratto di licenza con l'utente finale.</span><span class="sxs-lookup"><span data-stu-id="141c5-119">Run the following command in which the /q means quiet installation - the installation doesn't prompt you to accept the End-User License Agreement.</span></span>
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-the-connector-with-azure-ad"></a><span data-ttu-id="141c5-120">Registrare il connettore in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="141c5-120">Register the connector with Azure AD</span></span>
<span data-ttu-id="141c5-121">Esistono due metodi da usare per registrare il connettore:</span><span class="sxs-lookup"><span data-stu-id="141c5-121">There are two methods you can use to register the connector:</span></span>

* <span data-ttu-id="141c5-122">Registrare il connettore con un oggetto credenziali di Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="141c5-122">Register the connector using a Windows PowerShell credential object</span></span>
* <span data-ttu-id="141c5-123">Registrare il connettore con un token creato offline</span><span class="sxs-lookup"><span data-stu-id="141c5-123">Register the connector using a token created offline</span></span>

### <a name="register-the-connector-using-a-windows-powershell-credential-object"></a><span data-ttu-id="141c5-124">Registrare il connettore con un oggetto credenziali di Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="141c5-124">Register the connector using a Windows PowerShell credential object</span></span>
1. <span data-ttu-id="141c5-125">Creare l'oggetto credenziali di Windows PowerShell eseguendo questo comando.</span><span class="sxs-lookup"><span data-stu-id="141c5-125">Create the Windows PowerShell Credentials object by running this command.</span></span> <span data-ttu-id="141c5-126">Sostituire *\<username\>* e *\<password\>* con il nome utente e la password per la directory:</span><span class="sxs-lookup"><span data-stu-id="141c5-126">Replace *\<username\>* and *\<password\>* with the username and password for your directory:</span></span>
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. <span data-ttu-id="141c5-127">Passare a **C:\Programmi\Microsoft AAD App Proxy Connector** ed eseguire lo script usando l'oggetto credenziali di PowerShell creato.</span><span class="sxs-lookup"><span data-stu-id="141c5-127">Go to **C:\Program Files\Microsoft AAD App Proxy Connector** and run the script using the PowerShell credentials object you created.</span></span> <span data-ttu-id="141c5-128">Sostituire *$cred* con il nome dell'oggetto credenziali di PowerShell creato:</span><span class="sxs-lookup"><span data-stu-id="141c5-128">Replace *$cred* with the name of the PowerShell credentials object you created:</span></span>
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-the-connector-using-a-token-created-offline"></a><span data-ttu-id="141c5-129">Registrare il connettore con un token creato offline</span><span class="sxs-lookup"><span data-stu-id="141c5-129">Register the connector using a token created offline</span></span>
1. <span data-ttu-id="141c5-130">Creare un token offline con la classe AuthenticationContext, utilizzando i valori nel frammento di codice:</span><span class="sxs-lookup"><span data-stu-id="141c5-130">Create an offline token using the AuthenticationContext class using the values in the code snippet:</span></span>

        using System;
        using System.Diagnostics;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

        class Program
        {
        #region constants
        /// <summary>
        /// The AAD authentication endpoint uri
        /// </summary>
        static readonly Uri AadAuthenticationEndpoint = new Uri("https://login.microsoftonline.com/common/oauth2/token?api-version=1.0");

        /// <summary>
        /// The application ID of the connector in AAD
        /// </summary>
        static readonly string ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";

        /// <summary>
        /// The reply address of the connector application in AAD
        /// </summary>
        static readonly Uri ConnectorRedirectAddress = new Uri("urn:ietf:wg:oauth:2.0:oob");

        /// <summary>
        /// The AppIdUri of the registration service in AAD
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


2. <span data-ttu-id="141c5-131">Dopo aver ottenuto il token, creare una SecureString con il token:</span><span class="sxs-lookup"><span data-stu-id="141c5-131">Once you have the token, create a SecureString using the token:</span></span>

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. <span data-ttu-id="141c5-132">Eseguire il comando Windows PowerShell seguente, sostituendo \<tenant GUID\> con l'ID della directory:</span><span class="sxs-lookup"><span data-stu-id="141c5-132">Run the following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span></span>

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a><span data-ttu-id="141c5-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="141c5-133">Next steps</span></span> 
* [<span data-ttu-id="141c5-134">Pubblicare applicazioni mediante il proprio nome di dominio</span><span class="sxs-lookup"><span data-stu-id="141c5-134">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="141c5-135">Abilitare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="141c5-135">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="141c5-136">Risolvere i problemi che si verificano con il proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="141c5-136">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)


