---
title: Autenticazione basata su certificati di Azure Active Directory - Introduzione | Microsoft Docs
description: Informazioni su come configurare l'autenticazione basata su certificati nel proprio ambiente
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 8ebc6f2dd7502fd75ffdd4d5d68338382cb1a46b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a><span data-ttu-id="1b9da-103">Introduzione all'autenticazione basata su certificati di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b9da-103">Get started with certificate-based authentication in Azure Active Directory</span></span>

<span data-ttu-id="1b9da-104">L'autenticazione basata su certificati consente di essere autenticati da Azure Active Directory con un certificato client su un dispositivo Windows, Android o iOS quando si connette il proprio account Exchange online a:</span><span class="sxs-lookup"><span data-stu-id="1b9da-104">Certificate-based authentication enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

- <span data-ttu-id="1b9da-105">Applicazioni Office per dispositivi mobili, come Microsoft Outlook e Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="1b9da-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   

- <span data-ttu-id="1b9da-106">Client Exchange ActiveSync (EAS)</span><span class="sxs-lookup"><span data-stu-id="1b9da-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="1b9da-107">La configurazione di questa funzionalità elimina la necessità di immettere una combinazione di nome utente e password in determinate applicazioni di posta e applicazioni Microsoft Office sul dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="1b9da-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="1b9da-108">In questo argomento:</span><span class="sxs-lookup"><span data-stu-id="1b9da-108">This topic:</span></span>

- <span data-ttu-id="1b9da-109">Viene descritto come configurare e usare l'autenticazione basata su certificati per gli utenti dei tenant nei piani Office 365 Enterprise, Business, Education e US Government.</span><span class="sxs-lookup"><span data-stu-id="1b9da-109">Provides you with the steps to configure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span></span> <span data-ttu-id="1b9da-110">Questa funzionalità è disponibile in anteprima nei piani Office 365 China, US Government Defense e US Government Federal.</span><span class="sxs-lookup"><span data-stu-id="1b9da-110">This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans.</span></span> 

- <span data-ttu-id="1b9da-111">Si presuppone che siano già configurati un'[infrastruttura a chiave pubblica (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) e [AD FS](connect/active-directory-aadconnectfed-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1b9da-111">Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](connect/active-directory-aadconnectfed-whatis.md) configured.</span></span>    


## <a name="requirements"></a><span data-ttu-id="1b9da-112">Requisiti</span><span class="sxs-lookup"><span data-stu-id="1b9da-112">Requirements</span></span>

<span data-ttu-id="1b9da-113">Per configurare l'autenticazione basata su certificati, devono essere soddisfatti i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="1b9da-113">To configure certificate-based authentication, the following must be true:</span></span>  

- <span data-ttu-id="1b9da-114">L'autenticazione basata sui certificati è supportata solo per ambienti federati per applicazioni browser o client nativi che usano l'autenticazione moderna (ADAL).</span><span class="sxs-lookup"><span data-stu-id="1b9da-114">Certificate-based authentication (CBA) is only supported for Federated environments for browser applications or native clients using modern authentication (ADAL).</span></span> <span data-ttu-id="1b9da-115">L'unica eccezione è Exchange Active Sync per EXO che può essere usato sia per gli account federati che per quelli gestiti.</span><span class="sxs-lookup"><span data-stu-id="1b9da-115">The one exception is Exchange Active Sync (EAS) for EXO which can be used for both, federated and managed accounts.</span></span> 

- <span data-ttu-id="1b9da-116">L'autorità di certificazione radice e tutte le autorità di certificazione intermedie devono essere configurate in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b9da-116">The root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.</span></span>  

- <span data-ttu-id="1b9da-117">Ogni autorità di certificazione deve avere un elenco di revoche di certificati (Certificate Revocation List o CRL) a cui si possa fare riferimento tramite un URL Internet.</span><span class="sxs-lookup"><span data-stu-id="1b9da-117">Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.</span></span>  

- <span data-ttu-id="1b9da-118">È necessario che in Azure Active Directory sia configurata almeno un'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="1b9da-118">You must have at least one certificate authority configured in Azure Active Directory.</span></span> <span data-ttu-id="1b9da-119">I passaggi correlati sono descritti nella sezione [Configure the certificate authorities](#step-2-configure-the-certificate-authorities) (Configurare le autorità di certificazione).</span><span class="sxs-lookup"><span data-stu-id="1b9da-119">You can find related steps in the [Configure the certificate authorities](#step-2-configure-the-certificate-authorities) section.</span></span>  

- <span data-ttu-id="1b9da-120">Per i client Exchange ActiveSync, il certificato client deve contenere l'indirizzo email instradabile dell'utente in Exchange online, nel nome dell'entità o nel nome RFC822 del campo Nome alternativo soggetto.</span><span class="sxs-lookup"><span data-stu-id="1b9da-120">For Exchange ActiveSync clients, the client certificate must have the user’s routable email address in Exchange online in either the Principal Name or the RFC822 Name value of the Subject Alternative Name field.</span></span> <span data-ttu-id="1b9da-121">Azure Active Directory esegue il mapping del valore RFC822 all'attributo dell'indirizzo Proxy nella directory.</span><span class="sxs-lookup"><span data-stu-id="1b9da-121">Azure Active Directory maps the RFC822 value to the Proxy Address attribute in the directory.</span></span>  

- <span data-ttu-id="1b9da-122">Il dispositivo client deve avere accesso ad almeno un'autorità di certificazione che emetta i certificati client.</span><span class="sxs-lookup"><span data-stu-id="1b9da-122">Your client device must have access to at least one certificate authority that issues client certificates.</span></span>  

- <span data-ttu-id="1b9da-123">È necessario che al client sia stato rilasciato un certificato client per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="1b9da-123">A client certificate for client authentication must have been issued to your client.</span></span>  




## <a name="step-1-select-your-device-platform"></a><span data-ttu-id="1b9da-124">Passaggio 1: Selezionare la piattaforma del dispositivo</span><span class="sxs-lookup"><span data-stu-id="1b9da-124">Step 1: Select your device platform</span></span>

<span data-ttu-id="1b9da-125">Il primo passaggio per quanto riguarda la piattaforma del dispositivo è verificare i punti seguenti:</span><span class="sxs-lookup"><span data-stu-id="1b9da-125">As a first step, for the device platform you care about, you need to review the following:</span></span>

- <span data-ttu-id="1b9da-126">Supporto delle applicazioni Office per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="1b9da-126">The Office mobile applications support</span></span> 
- <span data-ttu-id="1b9da-127">Requisiti specifici di implementazione</span><span class="sxs-lookup"><span data-stu-id="1b9da-127">The specific implementation requirements</span></span>  

<span data-ttu-id="1b9da-128">Le informazioni correlate sono disponibili per le piattaforme dei dispositivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1b9da-128">The related information exists for the following device platforms:</span></span>

- [<span data-ttu-id="1b9da-129">Android</span><span class="sxs-lookup"><span data-stu-id="1b9da-129">Android</span></span>](active-directory-certificate-based-authentication-android.md)
- [<span data-ttu-id="1b9da-130">iOS</span><span class="sxs-lookup"><span data-stu-id="1b9da-130">iOS</span></span>](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-the-certificate-authorities"></a><span data-ttu-id="1b9da-131">Passaggio 2: Configurare le autorità di certificazione</span><span class="sxs-lookup"><span data-stu-id="1b9da-131">Step 2: Configure the certificate authorities</span></span> 

<span data-ttu-id="1b9da-132">Per configurare le proprie autorità di certificazione in Azure Active Directory, caricare gli elementi seguenti per ogni autorità:</span><span class="sxs-lookup"><span data-stu-id="1b9da-132">To configure your certificate authorities in Azure Active Directory, for each certificate authority, upload the following:</span></span> 

* <span data-ttu-id="1b9da-133">La parte pubblica del certificato, nel formato *.cer*</span><span class="sxs-lookup"><span data-stu-id="1b9da-133">The public portion of the certificate, in *.cer* format</span></span> 
* <span data-ttu-id="1b9da-134">Gli URL Internet in cui si trovano gli elenchi di revoche di certificati (Certificate Revocation List o CRL)</span><span class="sxs-lookup"><span data-stu-id="1b9da-134">The Internet facing URLs where the Certificate Revocation Lists (CRLs) reside</span></span>

<span data-ttu-id="1b9da-135">Lo schema per un'autorità di certificazione ha un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="1b9da-135">The schema for a certificate authority looks as follows:</span></span> 

    class TrustedCAsForPasswordlessAuth 
    { 
       CertificateAuthorityInformation[] certificateAuthorities;    
    } 

    class CertificateAuthorityInformation 

    { 
        CertAuthorityType authorityType; 
        X509Certificate trustedCertificate; 
        string crlDistributionPoint; 
        string deltaCrlDistributionPoint; 
        string trustedIssuer; 
        string trustedIssuerSKI; 
    }                

    enum CertAuthorityType 
    { 
        RootAuthority = 0, 
        IntermediateAuthority = 1 
    } 

<span data-ttu-id="1b9da-136">Per la configurazione, è possibile usare [Azure Active Directory PowerShell versione 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="1b9da-136">For the configuration, you can use the [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span></span>  

1. <span data-ttu-id="1b9da-137">Avviare Windows PowerShell con privilegi amministrativi.</span><span class="sxs-lookup"><span data-stu-id="1b9da-137">Start Windows PowerShell with administrator privileges.</span></span> 
2. <span data-ttu-id="1b9da-138">Installare il modulo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b9da-138">Install the Azure AD module.</span></span> <span data-ttu-id="1b9da-139">È necessario installare la versione [2.0.0.33](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) o una versione successiva.</span><span class="sxs-lookup"><span data-stu-id="1b9da-139">You need to install Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.</span></span>  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

<span data-ttu-id="1b9da-140">Il primo passaggio di configurazione consiste nello stabilire una connessione con il tenant.</span><span class="sxs-lookup"><span data-stu-id="1b9da-140">As a first configuration step, you need to establish a connection with your tenant.</span></span> <span data-ttu-id="1b9da-141">Una volta stabilita la connessione al tenant è possibile rivedere, aggiungere, eliminare e modificare le autorità di certificazione attendibili definite nella directory.</span><span class="sxs-lookup"><span data-stu-id="1b9da-141">As soon as a connection to your tenant exists, you can review, add, delete and modify the trusted certificate authorities that are defined in your directory.</span></span> 

### <a name="connect"></a><span data-ttu-id="1b9da-142">Connettere</span><span class="sxs-lookup"><span data-stu-id="1b9da-142">Connect</span></span>

<span data-ttu-id="1b9da-143">Per stabilire una connessione con il tenant, usare il cmdlet [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="1b9da-143">To establish a connection with your tenant, use the [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span></span>

    Connect-AzureAD 


### <a name="retrieve"></a><span data-ttu-id="1b9da-144">Recupero</span><span class="sxs-lookup"><span data-stu-id="1b9da-144">Retrieve</span></span> 

<span data-ttu-id="1b9da-145">Per recuperare le autorità di certificazione attendibili definite nella directory, usare il cmdlet [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="1b9da-145">To retrieve the trusted certificate authorities that are defined in your directory, use the [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span></span> 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a><span data-ttu-id="1b9da-146">Add</span><span class="sxs-lookup"><span data-stu-id="1b9da-146">Add</span></span>

<span data-ttu-id="1b9da-147">Per creare un'autorità di certificazione attendibile, usare il cmdlet [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) e l'attributo **crlDistributionPoint** per un valore corretto:</span><span class="sxs-lookup"><span data-stu-id="1b9da-147">To create a trusted certificate authority, use the [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet and set the **crlDistributionPoint** attribute to a correct value:</span></span> 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF THE CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a><span data-ttu-id="1b9da-148">Rimuovere</span><span class="sxs-lookup"><span data-stu-id="1b9da-148">Remove</span></span>

<span data-ttu-id="1b9da-149">Per rimuovere un'autorità di certificazione attendibile, usare il cmdlet [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="1b9da-149">To remove a trusted certificate authority, use the [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a><span data-ttu-id="1b9da-150">Modificare</span><span class="sxs-lookup"><span data-stu-id="1b9da-150">Modfiy</span></span>

<span data-ttu-id="1b9da-151">Per modificare un'autorità di certificazione attendibile, usare il cmdlet [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="1b9da-151">To modify a trusted certificate authority, use the [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a><span data-ttu-id="1b9da-152">Passaggio 3: Configurare la revoca</span><span class="sxs-lookup"><span data-stu-id="1b9da-152">Step 3: Configure revocation</span></span>

<span data-ttu-id="1b9da-153">Per revocare un certificato client, Azure Active Directory recupera l'elenco di revoche di certificati (Certificate Revocation List o CRL) dagli URL caricati come parte delle informazioni sull'autorità di certificazione e li memorizza nella cache.</span><span class="sxs-lookup"><span data-stu-id="1b9da-153">To revoke a client certificate, Azure Active Directory fetches the certificate revocation list (CRL) from the URLs uploaded as part of certificate authority information and caches it.</span></span> <span data-ttu-id="1b9da-154">L'ultimo timestamp di pubblicazione, ovvero la proprietà**Effective Date** (Data di validità), in CRL viene usato per assicurare la validità di CRL.</span><span class="sxs-lookup"><span data-stu-id="1b9da-154">The last publish timestamp (**Effective Date** property) in the CRL is used to ensure the CRL is still valid.</span></span> <span data-ttu-id="1b9da-155">Il CRL viene referenziato periodicamente per revocare l'accesso ai certificati che fanno parte dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="1b9da-155">The CRL is periodically referenced to revoke access to certificates that are a part of the list.</span></span>

<span data-ttu-id="1b9da-156">Se è necessaria una revoca più immediata (ad esempio in caso di smarrimento del dispositivo da parte di un utente), il token di autorizzazione dell'utente può essere annullato.</span><span class="sxs-lookup"><span data-stu-id="1b9da-156">If a more instant revocation is required (for example, if a user loses a device), the authorization token of the user can be invalidated.</span></span> <span data-ttu-id="1b9da-157">Per annullare il token di autorizzazione, impostare il campo **StsRefreshTokenValidFrom** per questo particolare utente usando Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1b9da-157">To invalidate the authorization token, set the **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell.</span></span> <span data-ttu-id="1b9da-158">È necessario aggiornare il campo **StsRefreshTokenValidFrom** per ogni utente a cui revocare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="1b9da-158">You must update the **StsRefreshTokenValidFrom** field for each user you want to revoke access for.</span></span>

<span data-ttu-id="1b9da-159">Per fare in modo che la revoca persista, è necessario impostare la proprietà **Effective Date** (Data di validità) di CRL su una data successiva al valore impostato da **StsRefreshTokenValidFrom** e assicurarsi che il certificato in questione sia in CRL.</span><span class="sxs-lookup"><span data-stu-id="1b9da-159">To ensure that the revocation persists, you must set the **Effective Date** of the CRL to a date after the value set by **StsRefreshTokenValidFrom** and ensure the certificate in question is in the CRL.</span></span>

<span data-ttu-id="1b9da-160">I passaggi seguenti illustrano il processo per aggiornare e annullare il token di autorizzazione impostando il campo **StsRefreshTokenValidFrom** .</span><span class="sxs-lookup"><span data-stu-id="1b9da-160">The following steps outline the process for updating and invalidating the authorization token by setting the **StsRefreshTokenValidFrom** field.</span></span> 

<span data-ttu-id="1b9da-161">**Per configurare la revoca:**</span><span class="sxs-lookup"><span data-stu-id="1b9da-161">**To configure revocation:**</span></span> 

1. <span data-ttu-id="1b9da-162">Connettersi con credenziali amministrative al servizio MSOL:</span><span class="sxs-lookup"><span data-stu-id="1b9da-162">Connect with admin credentials to the MSOL service:</span></span> 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. <span data-ttu-id="1b9da-163">Recuperare il valore StsRefreshTokensValidFrom corrente per un utente:</span><span class="sxs-lookup"><span data-stu-id="1b9da-163">Retrieve the current StsRefreshTokensValidFrom value for a user:</span></span> 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. <span data-ttu-id="1b9da-164">Configurare un nuovo valore StsRefreshTokensValidFrom per l'utente uguale al timestamp corrente:</span><span class="sxs-lookup"><span data-stu-id="1b9da-164">Configure a new StsRefreshTokensValidFrom value for the user equal to the current timestamp:</span></span> 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

<span data-ttu-id="1b9da-165">La data impostata deve essere futura.</span><span class="sxs-lookup"><span data-stu-id="1b9da-165">The date you set must be in the future.</span></span> <span data-ttu-id="1b9da-166">Se la data non è futura, la proprietà **StsRefreshTokensValidFrom** non viene impostata.</span><span class="sxs-lookup"><span data-stu-id="1b9da-166">If the date is not in the future, the **StsRefreshTokensValidFrom** property is not set.</span></span> <span data-ttu-id="1b9da-167">Se la data è futura, la proprietà **StsRefreshTokensValidFrom** viene impostata sull'ora corrente, non sulla data indicata dal comando Set-MsolUser.</span><span class="sxs-lookup"><span data-stu-id="1b9da-167">If the date is in the future, **StsRefreshTokensValidFrom** is set to the current time (not the date indicated by Set-MsolUser command).</span></span> 


## <a name="step-4-test-your-configuration"></a><span data-ttu-id="1b9da-168">Passaggio 4: Testare la configurazione</span><span class="sxs-lookup"><span data-stu-id="1b9da-168">Step 4: Test your configuration</span></span>

### <a name="testing-your-certificate"></a><span data-ttu-id="1b9da-169">Test del certificato</span><span class="sxs-lookup"><span data-stu-id="1b9da-169">Testing your certificate</span></span>

<span data-ttu-id="1b9da-170">Come primo test di configurazione è consigliabile accedere a [Outlook Web Access](https://outlook.office365.com) o a [SharePoint Online](https://microsoft.sharepoint.com) usando il **browser sul dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="1b9da-170">As a first configuration test, you should try to sign in to [Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.</span></span>

<span data-ttu-id="1b9da-171">Se l'accesso ha esito positivo significa che:</span><span class="sxs-lookup"><span data-stu-id="1b9da-171">If your sign-in is successful, then you know that:</span></span>

- <span data-ttu-id="1b9da-172">È stato eseguito il provisioning del certificato utente al dispositivo di test</span><span class="sxs-lookup"><span data-stu-id="1b9da-172">The user certificate has been provisioned to your test device</span></span>
- <span data-ttu-id="1b9da-173">AD FS è configurato correttamente</span><span class="sxs-lookup"><span data-stu-id="1b9da-173">AD FS is configured correctly</span></span>  


### <a name="testing-office-mobile-applications"></a><span data-ttu-id="1b9da-174">Test delle applicazioni Office per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="1b9da-174">Testing Office mobile applications</span></span>

<span data-ttu-id="1b9da-175">**Per testare l'autenticazione basata su certificati sulla propria applicazione Office per dispositivi mobili:**</span><span class="sxs-lookup"><span data-stu-id="1b9da-175">**To test certificate-based authentication on your mobile Office application:**</span></span> 

1. <span data-ttu-id="1b9da-176">Nel dispositivo di test installare un'applicazione Office per dispositivi mobili (ad esempio OneDrive).</span><span class="sxs-lookup"><span data-stu-id="1b9da-176">On your test device, install an Office mobile application (e.g., OneDrive).</span></span>
3. <span data-ttu-id="1b9da-177">Avviare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1b9da-177">Launch the application.</span></span> 
4. <span data-ttu-id="1b9da-178">Immettere il nome utente, quindi selezionare il certificato utente da usare.</span><span class="sxs-lookup"><span data-stu-id="1b9da-178">Enter your user name, and then select the user certificate you want to use.</span></span> 

<span data-ttu-id="1b9da-179">È necessario aver eseguito l'accesso.</span><span class="sxs-lookup"><span data-stu-id="1b9da-179">You should be successfully signed in.</span></span> 

### <a name="testing-exchange-activesync-client-applications"></a><span data-ttu-id="1b9da-180">Test delle applicazioni client Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="1b9da-180">Testing Exchange ActiveSync client applications</span></span>

<span data-ttu-id="1b9da-181">Per accedere a Exchange ActiveSync (EAS) tramite l'autenticazione basata su certificati, l'applicazione deve avere a disposizione un profilo EAS contenente il certificato client.</span><span class="sxs-lookup"><span data-stu-id="1b9da-181">To access Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing the client certificate must be available to the application.</span></span> 

<span data-ttu-id="1b9da-182">Il profilo EAS deve contenere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="1b9da-182">The EAS profile must contain the following information:</span></span>

- <span data-ttu-id="1b9da-183">Il certificato utente da usare per l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="1b9da-183">The user certificate to be used for authentication</span></span> 

- <span data-ttu-id="1b9da-184">L'endpoint EAS (ad esempio outlook.office365.com)</span><span class="sxs-lookup"><span data-stu-id="1b9da-184">The EAS endpoint (for example, outlook.office365.com)</span></span>

<span data-ttu-id="1b9da-185">Un profilo EAS può essere configurato e aggiunto al dispositivo tramite l'uso di software MDM, come Intune, o inserendo manualmente il certificato nel profilo EAS sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1b9da-185">An EAS profile can be configured and placed on the device through the utilization of Mobile device management (MDM) such as Intune or by manually placing the certificate in the EAS profile on the device.</span></span>  

### <a name="testing-eas-client-applications-on-android"></a><span data-ttu-id="1b9da-186">Test delle applicazioni client EAS in Android</span><span class="sxs-lookup"><span data-stu-id="1b9da-186">Testing EAS client applications on Android</span></span>

<span data-ttu-id="1b9da-187">**Per testare l'autenticazione basata su certificati:**</span><span class="sxs-lookup"><span data-stu-id="1b9da-187">**To test certificate authentication:**</span></span>  

1. <span data-ttu-id="1b9da-188">Configurare un profilo EAS nell'applicazione che soddisfi i requisiti riportati sopra.</span><span class="sxs-lookup"><span data-stu-id="1b9da-188">Configure an EAS profile in the application that satisfies the requirements above.</span></span>  
2. <span data-ttu-id="1b9da-189">Aprire l'applicazione e verificare che venga eseguita la sincronizzazione dell'email.</span><span class="sxs-lookup"><span data-stu-id="1b9da-189">Open the application, and verify that mail is synchronizing.</span></span> 

