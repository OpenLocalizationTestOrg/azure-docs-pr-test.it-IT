---
title: insieme di credenziali chiave di Azure da un'applicazione Web aaaUse | Documenti Microsoft
description: "Utilizzare questa esercitazione toohelp si apprenderà come toouse Azure chiave dell'insieme di credenziali da un'applicazione web."
services: key-vault
documentationcenter: 
author: adhurwit
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 9b7d065e-1979-4397-8298-eeba3aec4792
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: adhurwit
ms.openlocfilehash: d5e2299e60b379c4e234d5cd6be03411c5a5c958
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a><span data-ttu-id="929a6-103">Usare l'insieme di credenziali chiave di Azure da un'applicazione Web</span><span class="sxs-lookup"><span data-stu-id="929a6-103">Use Azure Key Vault from a Web Application</span></span>
## <a name="introduction"></a><span data-ttu-id="929a6-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="929a6-104">Introduction</span></span>
<span data-ttu-id="929a6-105">Utilizzare questa esercitazione toohelp si apprenderà come toouse Azure chiave dell'insieme di credenziali da un'applicazione web in Azure.</span><span class="sxs-lookup"><span data-stu-id="929a6-105">Use this tutorial toohelp you learn how toouse Azure Key Vault from a web application in Azure.</span></span> <span data-ttu-id="929a6-106">Illustra il processo di hello dell'accesso a una chiave privata da un insieme di credenziali chiave di Azure in modo che può essere utilizzato nell'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="929a6-106">It walks you through hello process of accessing a secret from an Azure Key Vault so that it can be used in your web application.</span></span>

<span data-ttu-id="929a6-107">**Toocomplete tempo stimato:** 15 minuti</span><span class="sxs-lookup"><span data-stu-id="929a6-107">**Estimated time toocomplete:** 15 minutes</span></span>

<span data-ttu-id="929a6-108">Per informazioni generali sull'insieme di credenziali di Azure, vedere [Cos'è l'insieme di credenziali chiave di Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="929a6-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="929a6-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="929a6-109">Prerequisites</span></span>
<span data-ttu-id="929a6-110">toocomplete questa esercitazione, è necessario disporre di hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="929a6-110">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="929a6-111">Un segreto tooa URI in un insieme di credenziali chiave di Azure</span><span class="sxs-lookup"><span data-stu-id="929a6-111">A URI tooa secret in an Azure Key Vault</span></span>
* <span data-ttu-id="929a6-112">Un ID Client e un segreto Client per un'applicazione web registrati con Azure Active Directory che ha accesso tooyour insieme di credenziali chiave</span><span class="sxs-lookup"><span data-stu-id="929a6-112">A Client ID and a Client Secret for a web application registered with Azure Active Directory that has access tooyour Key Vault</span></span>
* <span data-ttu-id="929a6-113">Un'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="929a6-113">A web application.</span></span> <span data-ttu-id="929a6-114">Abbiamo mostrato passaggi hello per un'applicazione ASP.NET MVC distribuito in Azure come App Web.</span><span class="sxs-lookup"><span data-stu-id="929a6-114">We will be showing hello steps for an ASP.NET MVC application deployed in Azure as a Web App.</span></span>

> [!NOTE]
> <span data-ttu-id="929a6-115">È essenziale di aver completato i passaggi di hello elencati in [introduzione insieme credenziali chiavi Azure](key-vault-get-started.md) per questa esercitazione in modo da avere hello hello Client ID e segreto tooa URI e il segreto Client per un'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="929a6-115">It is essential that you have completed hello steps listed in [Get Started with Azure Key Vault](key-vault-get-started.md) for this tutorial so that you have hello URI tooa secret and hello Client ID and Client Secret for a web application.</span></span>
> 
> 

<span data-ttu-id="929a6-116">un'applicazione web Hello che accederà a insieme di credenziali chiave hello è hello uno che viene registrato in Azure Active Directory e sia stato assegnato l'accesso tooyour insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="929a6-116">hello web application that will be accessing hello Key Vault is hello one that is registered in Azure Active Directory and has been given access tooyour Key Vault.</span></span> <span data-ttu-id="929a6-117">In caso non hello, tornare indietro tooRegister un'applicazione nell'esercitazione Introduzione hello e ripetere i passaggi di hello elencati.</span><span class="sxs-lookup"><span data-stu-id="929a6-117">If this is not hello case, go back tooRegister an Application in hello Get Started tutorial and repeat hello steps listed.</span></span>

<span data-ttu-id="929a6-118">Questa esercitazione è progettata per gli sviluppatori web che supportano hello di base per creare applicazioni web in Azure.</span><span class="sxs-lookup"><span data-stu-id="929a6-118">This tutorial is designed for web developers that understand hello basics of creating web applications on Azure.</span></span> <span data-ttu-id="929a6-119">Per altre informazioni sulle app Web di Azure, vedere [Panoramica delle app Web](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="929a6-119">For more information about Azure Web Apps, see [Web Apps overview](../app-service-web/app-service-web-overview.md).</span></span>

## <span data-ttu-id="929a6-120"><a id="packages"></a>Aggiungere i pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="929a6-120"><a id="packages"></a>Add Nuget Packages</span></span>
<span data-ttu-id="929a6-121">Sono disponibili due pacchetti che l'applicazione web deve toohave installato.</span><span class="sxs-lookup"><span data-stu-id="929a6-121">There are two packages that your web application needs toohave installed.</span></span>

* <span data-ttu-id="929a6-122">Active Directory Authentication Library: contiene i metodi per interagire con Azure Active Directory e gestire l'identità utente</span><span class="sxs-lookup"><span data-stu-id="929a6-122">Active Directory Authentication Library - contains methods for interacting with Azure Active Directory and managing user identity</span></span>
* <span data-ttu-id="929a6-123">Azure Key Vault Library: contiene i metodi per interagire con l'insieme di credenziali chiave di Azure</span><span class="sxs-lookup"><span data-stu-id="929a6-123">Azure Key Vault Library - contains methods for interacting with Azure Key Vault</span></span>

<span data-ttu-id="929a6-124">Entrambi questi pacchetti possono essere installati utilizzando la Console di gestione pacchetti utilizzando il comando Install-Package hello hello.</span><span class="sxs-lookup"><span data-stu-id="929a6-124">Both of these packages can be installed using hello Package Manager Console using hello Install-Package command.</span></span>

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <span data-ttu-id="929a6-125"><a id="webconfig"></a>Modificare Web.Config</span><span class="sxs-lookup"><span data-stu-id="929a6-125"><a id="webconfig"></a>Modify Web.Config</span></span>
<span data-ttu-id="929a6-126">Sono disponibili tre impostazioni di applicazioni che richiedono file Web. config di toobe toohello aggiunto come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="929a6-126">There are three application settings that need toobe added toohello web.config file as follows.</span></span>

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


<span data-ttu-id="929a6-127">Se non si ha intenzione toohost dell'applicazione come un'App Web di Azure, è consigliabile aggiungere hello effettivo ClientId, segreto Client e segreto URI valori toohello Web. config. In caso contrario, lasciare i valori fittizi perché i valori effettivi hello verrà aggiunta in hello portale di Azure per un ulteriore livello di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="929a6-127">If you are not going toohost your application as an Azure Web App, then you should add hello actual ClientId, Client Secret, and Secret URI values toohello web.config. Otherwise leave these dummy values because we will be adding hello actual values in hello Azure Portal for an additional level of security.</span></span>

## <span data-ttu-id="929a6-128"><a id="gettoken"></a>Aggiungere un Token di accesso di tooGet (metodo)</span><span class="sxs-lookup"><span data-stu-id="929a6-128"><a id="gettoken"></a>Add Method tooGet an Access Token</span></span>
<span data-ttu-id="929a6-129">In hello toouse ordine API dell'insieme di credenziali chiave, è necessario un token di accesso.</span><span class="sxs-lookup"><span data-stu-id="929a6-129">In order toouse hello Key Vault API you need an access token.</span></span> <span data-ttu-id="929a6-130">Chiave dell'insieme di credenziali Client Hello gestisce le chiamate API dell'insieme di credenziali chiave toohello ma è necessario toosupply con una funzione che ottiene il token di accesso di hello.</span><span class="sxs-lookup"><span data-stu-id="929a6-130">hello Key Vault Client handles calls toohello Key Vault API but you need toosupply it with a function that gets hello access token.</span></span>  

<span data-ttu-id="929a6-131">Di seguito è tooget codice hello un token di accesso da Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="929a6-131">Following is hello code tooget an access token from Azure Active Directory.</span></span> <span data-ttu-id="929a6-132">Questo codice può far accedere ovunque nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="929a6-132">This code can go anywhere in your application.</span></span> <span data-ttu-id="929a6-133">In genere tooadd un'utilità o una classe EncryptionHelper.</span><span class="sxs-lookup"><span data-stu-id="929a6-133">I like tooadd a Utils or EncryptionHelper class.</span></span>  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property toohold hello secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //hello method that will be provided toohello KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed tooobtain hello JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> <span data-ttu-id="929a6-134">Utilizzo di un ID Client e il segreto Client è tooauthenticate modo più semplice di hello un'applicazione Azure AD.</span><span class="sxs-lookup"><span data-stu-id="929a6-134">Using a Client ID and Client Secret is hello easiest way tooauthenticate an Azure AD application.</span></span> <span data-ttu-id="929a6-135">Utilizzarlo nell'applicazione Web consente una separazione dei compiti e maggiore controllo sulla gestione delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="929a6-135">And using it in your web application allows for a separation of duties and more control over your key management.</span></span> <span data-ttu-id="929a6-136">Ma si basa sull'inserimento di hello segreto Client nelle impostazioni di configurazione che, per alcuni, possono essere rischiose come come inserimento segreto hello che si desidera tooprotect nelle impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="929a6-136">But it does rely on putting hello Client Secret in your configuration settings which for some can be as risky as putting hello secret that you want tooprotect in your configuration settings.</span></span> <span data-ttu-id="929a6-137">Per una discussione su come toouse un ID Client e il certificato anziché tooauthenticate ID Client e il segreto Client hello applicazione Azure AD, vedere di seguito.</span><span class="sxs-lookup"><span data-stu-id="929a6-137">See below for a discussion on how toouse a Client ID and Certificate instead of Client ID and Client Secret tooauthenticate hello Azure AD application.</span></span>
> 
> 

## <span data-ttu-id="929a6-138"><a id="appstart"></a>Recuperare il segreto hello su avvio applicazione</span><span class="sxs-lookup"><span data-stu-id="929a6-138"><a id="appstart"></a>Retrieve hello secret on Application Start</span></span>
<span data-ttu-id="929a6-139">È ora base hello toocall API dell'insieme di credenziali chiave di codice e recuperare il segreto hello.</span><span class="sxs-lookup"><span data-stu-id="929a6-139">Now we need code toocall hello Key Vault API and retrieve hello secret.</span></span> <span data-ttu-id="929a6-140">Hello codice riportato di seguito è possibile inserire qualsiasi fino a quando viene chiamato prima che sia necessario toouse è.</span><span class="sxs-lookup"><span data-stu-id="929a6-140">hello following code can be put anywhere as long as it is called before you need toouse it.</span></span> <span data-ttu-id="929a6-141">È stata inserita questo codice nell'evento di avvio dell'applicazione hello in Global. asax hello in modo che viene eseguita una volta all'avvio e rende disponibili per l'applicazione hello segreto di hello.</span><span class="sxs-lookup"><span data-stu-id="929a6-141">I have put this code in hello Application Start event in hello Global.asax so that it runs once on start and makes hello secret available for hello application.</span></span>

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <span data-ttu-id="929a6-142"><a id="portalsettings"></a>Aggiungere le impostazioni dell'App nel portale di Azure (facoltativo) hello</span><span class="sxs-lookup"><span data-stu-id="929a6-142"><a id="portalsettings"></a>Add App Settings in hello Azure Portal (optional)</span></span>
<span data-ttu-id="929a6-143">Se si dispone di un'App Web di Azure è ora possibile aggiungere i valori effettivi per hello AppSettings hello nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="929a6-143">If you have an Azure Web App you can now add hello actual values for hello AppSettings in hello Azure Portal.</span></span> <span data-ttu-id="929a6-144">In questo modo, i valori effettivi hello non saranno inclusi nel file Web. config hello ma protetto tramite hello portale in cui si dispone di funzionalità di controllo di accesso distinti.</span><span class="sxs-lookup"><span data-stu-id="929a6-144">By doing this, hello actual values will not be in hello web.config but protected via hello Portal where you have separate access control capabilities.</span></span> <span data-ttu-id="929a6-145">Questi valori verranno sostituiti dai valori hello immesso nel file Web. config. Verificare che hello stessi nomi hello.</span><span class="sxs-lookup"><span data-stu-id="929a6-145">These values will be substituted for hello values that you entered in your web.config. Make sure that hello names are hello same.</span></span>

![Impostazioni dell'applicazione visualizzate nel portale di Azure][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a><span data-ttu-id="929a6-147">Autenticazione con un certificato anziché un client secret</span><span class="sxs-lookup"><span data-stu-id="929a6-147">Authenticate with a Certificate instead of a Client Secret</span></span>
<span data-ttu-id="929a6-148">Un altro modo tooauthenticate un'applicazione Azure AD è tramite un ID Client e un certificato anziché un ID Client e il segreto Client.</span><span class="sxs-lookup"><span data-stu-id="929a6-148">Another way tooauthenticate an Azure AD application is by using a Client ID and a Certificate instead of a Client ID and Client Secret.</span></span> <span data-ttu-id="929a6-149">Seguenti sono hello passaggi toouse un certificato in un'applicazione Web di Azure:</span><span class="sxs-lookup"><span data-stu-id="929a6-149">Following are hello steps toouse a Certificate in an Azure Web App:</span></span>

1. <span data-ttu-id="929a6-150">Ottenere o creare un certificato</span><span class="sxs-lookup"><span data-stu-id="929a6-150">Get or Create a Certificate</span></span>
2. <span data-ttu-id="929a6-151">Associare hello certificato a un'applicazione Azure AD</span><span class="sxs-lookup"><span data-stu-id="929a6-151">Associate hello Certificate with an Azure AD application</span></span>
3. <span data-ttu-id="929a6-152">Aggiungere hello toouse di App Web tooyour codice certificato</span><span class="sxs-lookup"><span data-stu-id="929a6-152">Add code tooyour Web App toouse hello Certificate</span></span>
4. <span data-ttu-id="929a6-153">Aggiungere un tooyour certificato App Web</span><span class="sxs-lookup"><span data-stu-id="929a6-153">Add a Certificate tooyour Web App</span></span>

<span data-ttu-id="929a6-154">**Ottenere o creare un certificato** Per i nostri scopi rendiamo un certificato di prova.</span><span class="sxs-lookup"><span data-stu-id="929a6-154">**Get or Create a Certificate** For our purposes we will make a test certificate.</span></span> <span data-ttu-id="929a6-155">Ecco un paio di comandi che è possibile utilizzare in un prompt dei comandi per sviluppatori di toocreate un certificato.</span><span class="sxs-lookup"><span data-stu-id="929a6-155">Here are a couple of commands that you can use in a Developer Command Prompt toocreate a certificate.</span></span> <span data-ttu-id="929a6-156">Cambiare directory toowhere che Hello i file di certificato creato.</span><span class="sxs-lookup"><span data-stu-id="929a6-156">Change directory toowhere you want hello cert files created.</span></span>  <span data-ttu-id="929a6-157">Inoltre, per hello all'inizio e data di fine del certificato hello, utilizzare hello data corrente più 1 anno.</span><span class="sxs-lookup"><span data-stu-id="929a6-157">Also, for hello beginning and ending date of hello certificate, use hello current date plus 1 year.</span></span>

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

<span data-ttu-id="929a6-158">Prendere nota della data di fine hello e una password di hello per PFX hello (in questo esempio: 31/07/2016 e test123).</span><span class="sxs-lookup"><span data-stu-id="929a6-158">Make note of hello end date and hello password for hello .pfx (in this example: 07/31/2016 and test123).</span></span> <span data-ttu-id="929a6-159">Saranno necessarie più avanti.</span><span class="sxs-lookup"><span data-stu-id="929a6-159">You will need them below.</span></span>

<span data-ttu-id="929a6-160">Per ulteriori informazioni sulla creazione di un certificato di prova, vedere [Procedura: creare il proprio certificato di prova](https://msdn.microsoft.com/library/ff699202.aspx)</span><span class="sxs-lookup"><span data-stu-id="929a6-160">For more information on creating a test certificate, see [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span></span>

<span data-ttu-id="929a6-161">**Associare hello certificati con un'applicazione Azure AD** dopo aver creato un certificato, è necessario tooassociate con un'applicazione Azure AD.</span><span class="sxs-lookup"><span data-stu-id="929a6-161">**Associate hello Certificate with an Azure AD application** Now that you have a certificate, you need tooassociate it with an Azure AD application.</span></span> <span data-ttu-id="929a6-162">Attualmente, hello portale di Azure non supporta questo flusso di lavoro. Questo può essere completato tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="929a6-162">Presently, hello Azure Portal does not support this workflow; this can be completed through PowerShell.</span></span> <span data-ttu-id="929a6-163">Eseguire hello seguente certificato hello tooassoicate di comandi con un'applicazione hello Azure AD:</span><span class="sxs-lookup"><span data-stu-id="929a6-163">Run hello following commands tooassoicate hello certificate with hello Azure AD application:</span></span>

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get hello thumbprint toouse in your app settings
    $x509.Thumbprint

<span data-ttu-id="929a6-164">Dopo aver eseguito questi comandi, è possibile visualizzare un'applicazione hello in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="929a6-164">After you have run these commands, you can see hello application in Azure AD.</span></span> <span data-ttu-id="929a6-165">Durante la ricerca, assicurarsi di selezionare "Applicazioni di proprietà dell'azienda" anziché "Applicazioni usate dall'azienda" nella finestra di dialogo Ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="929a6-165">When searching, ensure you select "Applications my company owns" instead of "Applications my company uses" in hello search dialog.</span></span>

<span data-ttu-id="929a6-166">toolearn informazioni sugli oggetti di Azure Active Directory dell'applicazione e agli oggetti, vedere [oggetti applicazione e oggetti entità servizio](../active-directory/active-directory-application-objects.md)</span><span class="sxs-lookup"><span data-stu-id="929a6-166">toolearn more about Azure AD Application Objects and ServicePrincipal Objects, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md)</span></span>

<span data-ttu-id="929a6-167">**Aggiungere hello toouse di App Web tooyour codice certificato** ora si aggiungerà codice tooyour App Web tooaccess hello cert e utilizzarlo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="929a6-167">**Add code tooyour Web App toouse hello Certificate** Now we will add code tooyour Web App tooaccess hello cert and use it for authentication.</span></span>

<span data-ttu-id="929a6-168">Prima di tutto è cert hello tooaccess di codice.</span><span class="sxs-lookup"><span data-stu-id="929a6-168">First there is code tooaccess hello cert.</span></span>

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since hello test root isn't installed.
                if (col == null || col.Count == 0)
                    return null;
                return col[0];
            }
            finally
            {
                store.Close();
            }
        }
    }


<span data-ttu-id="929a6-169">Si noti che hello StoreLocation è CurrentUser anziché LocalMachine.</span><span class="sxs-lookup"><span data-stu-id="929a6-169">Note that hello StoreLocation is CurrentUser instead of LocalMachine.</span></span> <span data-ttu-id="929a6-170">E che ci stiamo fornendo toohello 'false' Find (metodo), poiché si sta usando un certificato di test.</span><span class="sxs-lookup"><span data-stu-id="929a6-170">And that we are supplying 'false' toohello Find method because we are using a test cert.</span></span>

<span data-ttu-id="929a6-171">Di seguito è riportato il codice che usa hello CertificateHelper e crea un ClientAssertionCertificate necessaria per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="929a6-171">Next is code that uses hello CertificateHelper and creates a ClientAssertionCertificate which is needed for authentication.</span></span>

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


<span data-ttu-id="929a6-172">Di seguito è hello nuovo codice tooget hello token di accesso.</span><span class="sxs-lookup"><span data-stu-id="929a6-172">Here is hello new code tooget hello access token.</span></span> <span data-ttu-id="929a6-173">Questo strumento sostituisce hello GetToken (metodo) precedente.</span><span class="sxs-lookup"><span data-stu-id="929a6-173">This replaces hello GetToken method above.</span></span> <span data-ttu-id="929a6-174">È stato indicato un nome diverso per comodità.</span><span class="sxs-lookup"><span data-stu-id="929a6-174">I have given it a different name for convenience.</span></span>

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

<span data-ttu-id="929a6-175">È stato inserito tutto il codice nella classe Utils del progetto Web App per semplificarne l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="929a6-175">I have put all of this code into my Web App project's Utils class for ease of use.</span></span>

<span data-ttu-id="929a6-176">ultima modifica del codice Hello è hello metodo Application_Start.</span><span class="sxs-lookup"><span data-stu-id="929a6-176">hello last code change is in hello Application_Start method.</span></span> <span data-ttu-id="929a6-177">È prima necessario toocall hello hello tooload di metodo GetCert() ClientAssertionCertificate.</span><span class="sxs-lookup"><span data-stu-id="929a6-177">First we need toocall hello GetCert() method tooload hello ClientAssertionCertificate.</span></span> <span data-ttu-id="929a6-178">E quindi si modifica metodo di callback hello che viene fornito quando si crea un nuovo KeyVaultClient.</span><span class="sxs-lookup"><span data-stu-id="929a6-178">And then we change hello callback method that we supply when creating a new KeyVaultClient.</span></span> <span data-ttu-id="929a6-179">Si noti che questa impostazione sostituisce il codice hello che si è verificato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="929a6-179">Note that this replaces hello code that we had above.</span></span>

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


<span data-ttu-id="929a6-180">**Aggiungere un certificato tooyour App Web, tramite il portale di Azure hello** aggiunta tooyour un certificato App Web è un processo semplice in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="929a6-180">**Add a Certificate tooyour Web App through hello Azure Portal** Adding a Certificate tooyour Web App is a simple two-step process.</span></span> <span data-ttu-id="929a6-181">In primo luogo, andare toohello portale di Azure e passare tooyour App Web.</span><span class="sxs-lookup"><span data-stu-id="929a6-181">First, go toohello Azure Portal and navigate tooyour Web App.</span></span> <span data-ttu-id="929a6-182">Nel pannello delle impostazioni hello per le App Web, fare clic sulla voce di hello per "i domini personalizzati e SSL".</span><span class="sxs-lookup"><span data-stu-id="929a6-182">On hello Settings blade for your Web App, click on hello entry for "Custom domains and SSL".</span></span> <span data-ttu-id="929a6-183">In hello pannello visualizzato è saranno hello tooupload in grado di certificato creato in precedenza, KVWebApp.pfx, che è importante ricordare la password di hello per pfx hello.</span><span class="sxs-lookup"><span data-stu-id="929a6-183">On hello blade that opens you will be able tooupload hello Certificate that you created above, KVWebApp.pfx, make sure that you remember hello password for hello pfx.</span></span>

![Aggiunta di un tooa certificato App Web nel portale di Azure hello][2]

<span data-ttu-id="929a6-185">ultimo elemento che è necessario toodo Hello è tooadd un tooyour di impostazione dell'applicazione Web App con sito Web di nome hello\_carico\_certificati e il valore *.</span><span class="sxs-lookup"><span data-stu-id="929a6-185">hello last thing that you need toodo is tooadd an Application Setting tooyour Web App that has hello name WEBSITE\_LOAD\_CERTIFICATES and a value of *.</span></span> <span data-ttu-id="929a6-186">Ciò garantisce che siano caricati tutti i certificati.</span><span class="sxs-lookup"><span data-stu-id="929a6-186">This will ensure that all Certificates are loaded.</span></span> <span data-ttu-id="929a6-187">Se si desidera hello solo tooload i certificati che è stato caricato, quindi è possibile immettere un elenco delimitato da virgole di relative identificazioni personali.</span><span class="sxs-lookup"><span data-stu-id="929a6-187">If you wanted tooload only hello Certificates that you have uploaded, then you can enter a comma-separated list of their thumbprints.</span></span>

<span data-ttu-id="929a6-188">toolearn più sull'aggiunta di un tooa certificato App Web, vedere [tramite certificati nelle applicazioni di siti Web di Azure](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span><span class="sxs-lookup"><span data-stu-id="929a6-188">toolearn more about adding a Certificate tooa Web App, see [Using Certificates in Azure Websites Applications](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span></span>

<span data-ttu-id="929a6-189">**Aggiungere un insieme di credenziali di tooKey certificato come un segreto** invece di caricare direttamente il toohello certificato del servizio Web App, è possibile archiviarla nell'insieme di credenziali chiave come chiave privata e distribuirlo da questa posizione.</span><span class="sxs-lookup"><span data-stu-id="929a6-189">**Add a Certificate tooKey Vault as a secret** Instead of uploading your certificate toohello Web App service directly, you can store it in Key Vault as a secret and deploy it from there.</span></span> <span data-ttu-id="929a6-190">Si tratta di un processo in due passaggi descritto nella seguente post di blog, hello [distribuzione certificato dell'App Web Azure tramite l'insieme di credenziali chiave](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span><span class="sxs-lookup"><span data-stu-id="929a6-190">This is a two-step process that is outlined in hello following blog post, [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span></span>

## <span data-ttu-id="929a6-191"><a id="next"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="929a6-191"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="929a6-192">Per i riferimenti alla programmazione, vedere [Informazioni di riferimento sull'API client C# dell'insieme di credenziali chiave di Azure](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span><span class="sxs-lookup"><span data-stu-id="929a6-192">For programming references, see [Azure Key Vault C# Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span></span>

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
