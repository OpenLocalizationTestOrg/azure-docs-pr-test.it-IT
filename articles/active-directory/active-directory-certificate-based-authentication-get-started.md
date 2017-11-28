---
title: aaaAzure l'autenticazione basata sui certificati di Active Directory - introduzione | Documenti Microsoft
description: Informazioni su come l'autenticazione basata su certificati tooconfigure nell'ambiente in uso
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
ms.openlocfilehash: 3c73bdf56018c0716085c923a61e9560dbe4004c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a><span data-ttu-id="a1cf0-103">Introduzione all'autenticazione basata su certificati di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a1cf0-103">Get started with certificate-based authentication in Azure Active Directory</span></span>

<span data-ttu-id="a1cf0-104">Autenticazione basata su certificati consente toobe autenticato da Azure Active Directory con un certificato client in un dispositivo Windows, Android o iOS, quando ci si connette l'account di Exchange online a:</span><span class="sxs-lookup"><span data-stu-id="a1cf0-104">Certificate-based authentication enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

- <span data-ttu-id="a1cf0-105">Applicazioni Office per dispositivi mobili, come Microsoft Outlook e Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="a1cf0-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   

- <span data-ttu-id="a1cf0-106">Client Exchange ActiveSync (EAS)</span><span class="sxs-lookup"><span data-stu-id="a1cf0-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="a1cf0-107">Configurazione di questa funzionalità Elimina hello necessità tooenter un nome utente e la combinazione di password in determinate posta elettronica e le applicazioni di Microsoft Office sul tuo dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="a1cf0-108">In questo argomento:</span><span class="sxs-lookup"><span data-stu-id="a1cf0-108">This topic:</span></span>

- <span data-ttu-id="a1cf0-109">Fornisce hello tooconfigure i passaggi e utilizzare l'autenticazione basata su certificati per gli utenti del tenant Office 365 Enterprise, Business, Education e piani di governo degli Stati Uniti.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-109">Provides you with hello steps tooconfigure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span></span> <span data-ttu-id="a1cf0-110">Questa funzionalità è disponibile in anteprima nei piani Office 365 China, US Government Defense e US Government Federal.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-110">This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans.</span></span> 

- <span data-ttu-id="a1cf0-111">Si presuppone che siano già configurati un'[infrastruttura a chiave pubblica (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) e [AD FS](connect/active-directory-aadconnectfed-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a1cf0-111">Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](connect/active-directory-aadconnectfed-whatis.md) configured.</span></span>    


## <a name="requirements"></a><span data-ttu-id="a1cf0-112">Requisiti</span><span class="sxs-lookup"><span data-stu-id="a1cf0-112">Requirements</span></span>

<span data-ttu-id="a1cf0-113">l'autenticazione basata su certificato tooconfigure, hello devono verificarsi condizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a1cf0-113">tooconfigure certificate-based authentication, hello following must be true:</span></span>  

- <span data-ttu-id="a1cf0-114">L'autenticazione basata sui certificati è supportata solo per ambienti federati per applicazioni browser o client nativi che usano l'autenticazione moderna (ADAL).</span><span class="sxs-lookup"><span data-stu-id="a1cf0-114">Certificate-based authentication (CBA) is only supported for Federated environments for browser applications or native clients using modern authentication (ADAL).</span></span> <span data-ttu-id="a1cf0-115">Hello unica eccezione è Exchange Active Sync (EAS) per EXO che può essere utilizzato per gli account di entrambi, federati e gestiti.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-115">hello one exception is Exchange Active Sync (EAS) for EXO which can be used for both, federated and managed accounts.</span></span> 

- <span data-ttu-id="a1cf0-116">autorità di certificazione radice Hello e qualsiasi autorità di certificazione intermedie devono essere configurati in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-116">hello root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.</span></span>  

- <span data-ttu-id="a1cf0-117">Ogni autorità di certificazione deve avere un elenco di revoche di certificati (Certificate Revocation List o CRL) a cui si possa fare riferimento tramite un URL Internet.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-117">Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.</span></span>  

- <span data-ttu-id="a1cf0-118">È necessario che in Azure Active Directory sia configurata almeno un'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-118">You must have at least one certificate authority configured in Azure Active Directory.</span></span> <span data-ttu-id="a1cf0-119">È possibile trovare passaggi correlati in hello [configurare le autorità di certificazione hello](#step-2-configure-the-certificate-authorities) sezione.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-119">You can find related steps in hello [Configure hello certificate authorities](#step-2-configure-the-certificate-authorities) section.</span></span>  

- <span data-ttu-id="a1cf0-120">Per i client di Exchange ActiveSync, certificato client hello necessario hello instradabile elettronica utente indirizzo di Exchange online in entrambi hello nome dell'entità o valore del campo nome alternativo oggetto hello Nome RFC822 hello.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-120">For Exchange ActiveSync clients, hello client certificate must have hello user’s routable email address in Exchange online in either hello Principal Name or hello RFC822 Name value of hello Subject Alternative Name field.</span></span> <span data-ttu-id="a1cf0-121">Azure Active Directory esegue il mapping attributo hello RFC822 value toohello indirizzo Proxy nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-121">Azure Active Directory maps hello RFC822 value toohello Proxy Address attribute in hello directory.</span></span>  

- <span data-ttu-id="a1cf0-122">Il dispositivo client deve avere accesso tooat almeno una autorità di certificazione che emette i certificati client.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-122">Your client device must have access tooat least one certificate authority that issues client certificates.</span></span>  

- <span data-ttu-id="a1cf0-123">Un certificato client per l'autenticazione del client deve essere stato rilasciato tooyour client.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-123">A client certificate for client authentication must have been issued tooyour client.</span></span>  




## <a name="step-1-select-your-device-platform"></a><span data-ttu-id="a1cf0-124">Passaggio 1: Selezionare la piattaforma del dispositivo</span><span class="sxs-lookup"><span data-stu-id="a1cf0-124">Step 1: Select your device platform</span></span>

<span data-ttu-id="a1cf0-125">Come primo passaggio, per la piattaforma del dispositivo hello che è rilevante, è necessario tooreview hello segue:</span><span class="sxs-lookup"><span data-stu-id="a1cf0-125">As a first step, for hello device platform you care about, you need tooreview hello following:</span></span>

- <span data-ttu-id="a1cf0-126">supporto di applicazioni per dispositivi mobili Office Hello</span><span class="sxs-lookup"><span data-stu-id="a1cf0-126">hello Office mobile applications support</span></span> 
- <span data-ttu-id="a1cf0-127">Hello specifici requisiti di implementazione</span><span class="sxs-lookup"><span data-stu-id="a1cf0-127">hello specific implementation requirements</span></span>  

<span data-ttu-id="a1cf0-128">Hello correlate informazioni esistono per hello seguenti piattaforme per dispositivi:</span><span class="sxs-lookup"><span data-stu-id="a1cf0-128">hello related information exists for hello following device platforms:</span></span>

- [<span data-ttu-id="a1cf0-129">Android</span><span class="sxs-lookup"><span data-stu-id="a1cf0-129">Android</span></span>](active-directory-certificate-based-authentication-android.md)
- [<span data-ttu-id="a1cf0-130">iOS</span><span class="sxs-lookup"><span data-stu-id="a1cf0-130">iOS</span></span>](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-hello-certificate-authorities"></a><span data-ttu-id="a1cf0-131">Passaggio 2: Configurare le autorità di certificazione hello</span><span class="sxs-lookup"><span data-stu-id="a1cf0-131">Step 2: Configure hello certificate authorities</span></span> 

<span data-ttu-id="a1cf0-132">tooconfigure l'autorità di certificazione in Azure Active Directory, per ogni autorità di certificazione, caricare hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="a1cf0-132">tooconfigure your certificate authorities in Azure Active Directory, for each certificate authority, upload hello following:</span></span> 

* <span data-ttu-id="a1cf0-133">Hello parte pubblica del certificato hello, in *con estensione cer* formato</span><span class="sxs-lookup"><span data-stu-id="a1cf0-133">hello public portion of hello certificate, in *.cer* format</span></span> 
* <span data-ttu-id="a1cf0-134">Hello per Internet URL in cui hello degli elenchi di revoche di certificati (CRL) si trovano</span><span class="sxs-lookup"><span data-stu-id="a1cf0-134">hello Internet facing URLs where hello Certificate Revocation Lists (CRLs) reside</span></span>

<span data-ttu-id="a1cf0-135">schema di Hello per un'autorità di certificazione è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a1cf0-135">hello schema for a certificate authority looks as follows:</span></span> 

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

<span data-ttu-id="a1cf0-136">Per la configurazione di hello, è possibile utilizzare hello [Azure Active Directory PowerShell versione 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="a1cf0-136">For hello configuration, you can use hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span></span>  

1. <span data-ttu-id="a1cf0-137">Avviare Windows PowerShell con privilegi amministrativi.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-137">Start Windows PowerShell with administrator privileges.</span></span> 
2. <span data-ttu-id="a1cf0-138">Installare il modulo hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-138">Install hello Azure AD module.</span></span> <span data-ttu-id="a1cf0-139">È necessario tooinstall versione [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-139">You need tooinstall Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.</span></span>  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

<span data-ttu-id="a1cf0-140">Come primo passaggio di configurazione, è necessario tooestablish una connessione con il tenant.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-140">As a first configuration step, you need tooestablish a connection with your tenant.</span></span> <span data-ttu-id="a1cf0-141">Non appena un tenant tooyour connessione esiste, è possibile esaminare, aggiungere, eliminare e modificare le autorità di certificazione attendibile hello definiti nella directory.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-141">As soon as a connection tooyour tenant exists, you can review, add, delete and modify hello trusted certificate authorities that are defined in your directory.</span></span> 

### <a name="connect"></a><span data-ttu-id="a1cf0-142">Connettere</span><span class="sxs-lookup"><span data-stu-id="a1cf0-142">Connect</span></span>

<span data-ttu-id="a1cf0-143">una connessione con il tenant, usare hello tooestablish [Connetti AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a1cf0-143">tooestablish a connection with your tenant, use hello [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span></span>

    Connect-AzureAD 


### <a name="retrieve"></a><span data-ttu-id="a1cf0-144">Recupero</span><span class="sxs-lookup"><span data-stu-id="a1cf0-144">Retrieve</span></span> 

<span data-ttu-id="a1cf0-145">le autorità di certificazione attendibile hello tooretrieve definiti nella directory, utilizzare hello [Get AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-145">tooretrieve hello trusted certificate authorities that are defined in your directory, use hello [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span></span> 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a><span data-ttu-id="a1cf0-146">Add</span><span class="sxs-lookup"><span data-stu-id="a1cf0-146">Add</span></span>

<span data-ttu-id="a1cf0-147">toocreate un'autorità di certificazione, usare hello [New AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet e set hello **crlDistributionPoint** tooa corretto valore dell'attributo:</span><span class="sxs-lookup"><span data-stu-id="a1cf0-147">toocreate a trusted certificate authority, use hello [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet and set hello **crlDistributionPoint** attribute tooa correct value:</span></span> 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF hello CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a><span data-ttu-id="a1cf0-148">Rimuovere</span><span class="sxs-lookup"><span data-stu-id="a1cf0-148">Remove</span></span>

<span data-ttu-id="a1cf0-149">tooremove un'autorità di certificazione, usare hello [Remove AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a1cf0-149">tooremove a trusted certificate authority, use hello [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a><span data-ttu-id="a1cf0-150">Modificare</span><span class="sxs-lookup"><span data-stu-id="a1cf0-150">Modfiy</span></span>

<span data-ttu-id="a1cf0-151">toomodify un'autorità di certificazione, usare hello [Set AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a1cf0-151">toomodify a trusted certificate authority, use hello [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a><span data-ttu-id="a1cf0-152">Passaggio 3: Configurare la revoca</span><span class="sxs-lookup"><span data-stu-id="a1cf0-152">Step 3: Configure revocation</span></span>

<span data-ttu-id="a1cf0-153">un certificato client, Azure Active Directory toorevoke Recupera certificato hello elenco di revoche di certificati (CRL) dagli URL hello caricato come parte di informazioni autorità di certificazione e lo memorizza nella cache.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-153">toorevoke a client certificate, Azure Active Directory fetches hello certificate revocation list (CRL) from hello URLs uploaded as part of certificate authority information and caches it.</span></span> <span data-ttu-id="a1cf0-154">Hello all'ultima pubblicazione timestamp (**data di validità** proprietà) in hello CRL viene utilizzato tooensure hello CRL è ancora valido.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-154">hello last publish timestamp (**Effective Date** property) in hello CRL is used tooensure hello CRL is still valid.</span></span> <span data-ttu-id="a1cf0-155">Hello CRL è toocertificates accesso toorevoke periodicamente con cui viene fatto riferimento che fanno parte dell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-155">hello CRL is periodically referenced toorevoke access toocertificates that are a part of hello list.</span></span>

<span data-ttu-id="a1cf0-156">Se una revoca più immediata è necessaria (ad esempio, se un utente perde un dispositivo), il token di autorizzazione hello dell'utente hello può essere invalidato.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-156">If a more instant revocation is required (for example, if a user loses a device), hello authorization token of hello user can be invalidated.</span></span> <span data-ttu-id="a1cf0-157">tooinvalidate hello autorizzazione token, impostare hello **StsRefreshTokenValidFrom** campo per l'utente con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-157">tooinvalidate hello authorization token, set hello **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell.</span></span> <span data-ttu-id="a1cf0-158">È necessario aggiornare hello **StsRefreshTokenValidFrom** campo per ogni utente che si desidera accedere toorevoke per.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-158">You must update hello **StsRefreshTokenValidFrom** field for each user you want toorevoke access for.</span></span>

<span data-ttu-id="a1cf0-159">tooensure che revoca hello persiste, è necessario impostare hello **data di validità** di hello CRL tooa data hello valore impostato da **StsRefreshTokenValidFrom** e verificare che certificato hello in questione sia Hello CRL.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-159">tooensure that hello revocation persists, you must set hello **Effective Date** of hello CRL tooa date after hello value set by **StsRefreshTokenValidFrom** and ensure hello certificate in question is in hello CRL.</span></span>

<span data-ttu-id="a1cf0-160">Hello seguendo i passaggi struttura hello processo per aggiornare e invalidare il token di autorizzazione hello dall'impostazione hello **StsRefreshTokenValidFrom** campo.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-160">hello following steps outline hello process for updating and invalidating hello authorization token by setting hello **StsRefreshTokenValidFrom** field.</span></span> 

<span data-ttu-id="a1cf0-161">**revoca tooconfigure:**</span><span class="sxs-lookup"><span data-stu-id="a1cf0-161">**tooconfigure revocation:**</span></span> 

1. <span data-ttu-id="a1cf0-162">Connettersi con il servizio di MSOL toohello credenziali di amministratore:</span><span class="sxs-lookup"><span data-stu-id="a1cf0-162">Connect with admin credentials toohello MSOL service:</span></span> 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. <span data-ttu-id="a1cf0-163">Recuperare hello corrente StsRefreshTokensValidFrom valore per un utente:</span><span class="sxs-lookup"><span data-stu-id="a1cf0-163">Retrieve hello current StsRefreshTokensValidFrom value for a user:</span></span> 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. <span data-ttu-id="a1cf0-164">Configurare un nuovo valore StsRefreshTokensValidFrom per timestamp corrente di hello utente toohello uguale:</span><span class="sxs-lookup"><span data-stu-id="a1cf0-164">Configure a new StsRefreshTokensValidFrom value for hello user equal toohello current timestamp:</span></span> 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

<span data-ttu-id="a1cf0-165">deve essere futura hello data Hello che è impostata.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-165">hello date you set must be in hello future.</span></span> <span data-ttu-id="a1cf0-166">Se data hello non hello future, hello **StsRefreshTokensValidFrom** non è impostata.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-166">If hello date is not in hello future, hello **StsRefreshTokensValidFrom** property is not set.</span></span> <span data-ttu-id="a1cf0-167">Se la data hello è nel futuro, hello **StsRefreshTokensValidFrom** è impostata l'ora corrente (non hello date indicata dal comando Set-MsolUser) toohello.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-167">If hello date is in hello future, **StsRefreshTokensValidFrom** is set toohello current time (not hello date indicated by Set-MsolUser command).</span></span> 


## <a name="step-4-test-your-configuration"></a><span data-ttu-id="a1cf0-168">Passaggio 4: Testare la configurazione</span><span class="sxs-lookup"><span data-stu-id="a1cf0-168">Step 4: Test your configuration</span></span>

### <a name="testing-your-certificate"></a><span data-ttu-id="a1cf0-169">Test del certificato</span><span class="sxs-lookup"><span data-stu-id="a1cf0-169">Testing your certificate</span></span>

<span data-ttu-id="a1cf0-170">Come un primo test della configurazione, è consigliabile toosign in troppo[Outlook Web Access](https://outlook.office365.com) o [SharePoint Online](https://microsoft.sharepoint.com) utilizzando il **browser sul dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-170">As a first configuration test, you should try toosign in too[Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.</span></span>

<span data-ttu-id="a1cf0-171">Se l'accesso ha esito positivo significa che:</span><span class="sxs-lookup"><span data-stu-id="a1cf0-171">If your sign-in is successful, then you know that:</span></span>

- <span data-ttu-id="a1cf0-172">certificato utente Hello è stato sottoposto a provisioning tooyour test dispositivo</span><span class="sxs-lookup"><span data-stu-id="a1cf0-172">hello user certificate has been provisioned tooyour test device</span></span>
- <span data-ttu-id="a1cf0-173">AD FS è configurato correttamente</span><span class="sxs-lookup"><span data-stu-id="a1cf0-173">AD FS is configured correctly</span></span>  


### <a name="testing-office-mobile-applications"></a><span data-ttu-id="a1cf0-174">Test delle applicazioni Office per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="a1cf0-174">Testing Office mobile applications</span></span>

<span data-ttu-id="a1cf0-175">**autenticazione basata su certificati tootest sull'applicazione di Office per dispositivi mobili:**</span><span class="sxs-lookup"><span data-stu-id="a1cf0-175">**tootest certificate-based authentication on your mobile Office application:**</span></span> 

1. <span data-ttu-id="a1cf0-176">Nel dispositivo di test installare un'applicazione Office per dispositivi mobili (ad esempio OneDrive).</span><span class="sxs-lookup"><span data-stu-id="a1cf0-176">On your test device, install an Office mobile application (e.g., OneDrive).</span></span>
3. <span data-ttu-id="a1cf0-177">Avvia un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-177">Launch hello application.</span></span> 
4. <span data-ttu-id="a1cf0-178">Immettere il nome utente e quindi selezionare il certificato di utente hello desiderato toouse.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-178">Enter your user name, and then select hello user certificate you want toouse.</span></span> 

<span data-ttu-id="a1cf0-179">È necessario aver eseguito l'accesso.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-179">You should be successfully signed in.</span></span> 

### <a name="testing-exchange-activesync-client-applications"></a><span data-ttu-id="a1cf0-180">Test delle applicazioni client Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="a1cf0-180">Testing Exchange ActiveSync client applications</span></span>

<span data-ttu-id="a1cf0-181">tooaccess Exchange ActiveSync (EAS) tramite l'autenticazione basata su certificato, un profilo EAS contenente hello client certificato deve essere disponibile toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-181">tooaccess Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing hello client certificate must be available toohello application.</span></span> 

<span data-ttu-id="a1cf0-182">Hello profilo EAS deve contenere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="a1cf0-182">hello EAS profile must contain hello following information:</span></span>

- <span data-ttu-id="a1cf0-183">Hello toobe certificato utente utilizzato per l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="a1cf0-183">hello user certificate toobe used for authentication</span></span> 

- <span data-ttu-id="a1cf0-184">endpoint EAS Hello (ad esempio, outlook.office365.com)</span><span class="sxs-lookup"><span data-stu-id="a1cf0-184">hello EAS endpoint (for example, outlook.office365.com)</span></span>

<span data-ttu-id="a1cf0-185">Un profilo EAS può essere configurato e sul dispositivo hello tramite l'utilizzo di gestione dei dispositivi mobili (MDM), ad esempio Intune o inserendo manualmente il certificato di hello in hello profilo EAS sul dispositivo hello hello.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-185">An EAS profile can be configured and placed on hello device through hello utilization of Mobile device management (MDM) such as Intune or by manually placing hello certificate in hello EAS profile on hello device.</span></span>  

### <a name="testing-eas-client-applications-on-android"></a><span data-ttu-id="a1cf0-186">Test delle applicazioni client EAS in Android</span><span class="sxs-lookup"><span data-stu-id="a1cf0-186">Testing EAS client applications on Android</span></span>

<span data-ttu-id="a1cf0-187">**autenticazione del certificato tootest:**</span><span class="sxs-lookup"><span data-stu-id="a1cf0-187">**tootest certificate authentication:**</span></span>  

1. <span data-ttu-id="a1cf0-188">Configurare un profilo EAS in un'applicazione hello che soddisfi i requisiti di hello precedenti.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-188">Configure an EAS profile in hello application that satisfies hello requirements above.</span></span>  
2. <span data-ttu-id="a1cf0-189">Aprire un'applicazione hello e verificare che la sincronizzazione della posta.</span><span class="sxs-lookup"><span data-stu-id="a1cf0-189">Open hello application, and verify that mail is synchronizing.</span></span> 

