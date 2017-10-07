---
title: autenticazione basata su certificati aaaAzure Active Directory in iOS | Documenti Microsoft
description: Informazioni sugli scenari di hello supportata e requisiti di hello per la configurazione dell'autenticazione basata su certificato nelle soluzioni con i dispositivi iOS
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: 26a6fc54-0153-44fb-b970-9b432c99e9f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 4486ff5239c2897b3bc187053f31d74807430301
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a><span data-ttu-id="447ca-103">Autenticazione basata su certificati di Azure Active Directory in iOS</span><span class="sxs-lookup"><span data-stu-id="447ca-103">Azure Active Directory certificate-based authentication on iOS</span></span>

<span data-ttu-id="447ca-104">L'autenticazione basata su certificato (CBA) consente toobe autenticato da Azure Active Directory con un certificato client in un dispositivo Windows, Android o iOS, quando ci si connette l'account di Exchange online a:</span><span class="sxs-lookup"><span data-stu-id="447ca-104">Certificate-based authentication (CBA) enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="447ca-105">Applicazioni Office per dispositivi mobili, come Microsoft Outlook e Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="447ca-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="447ca-106">Client Exchange ActiveSync (EAS)</span><span class="sxs-lookup"><span data-stu-id="447ca-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="447ca-107">Configurazione di questa funzionalità Elimina hello necessità tooenter un nome utente e la combinazione di password in determinate posta elettronica e le applicazioni di Microsoft Office sul tuo dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="447ca-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="447ca-108">In questo argomento vengono fornite hello requisiti e degli scenari di hello è supportato per la configurazione CBA in un dispositivo iOS(Android) per gli utenti del tenant Office 365 Enterprise, Business, formazione, governo, Cina, e piani Germania.</span><span class="sxs-lookup"><span data-stu-id="447ca-108">This topic provides you with hello requirements and hello supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>

<span data-ttu-id="447ca-109">Questa funzionalità è disponibile in anteprima nei piani di Office 365 US Government Defense e Federal.</span><span class="sxs-lookup"><span data-stu-id="447ca-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>




## <a name="office-mobile-applications-support"></a><span data-ttu-id="447ca-110">Supporto delle applicazioni Office per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="447ca-110">Office mobile applications support</span></span>

| <span data-ttu-id="447ca-111">App</span><span class="sxs-lookup"><span data-stu-id="447ca-111">Apps</span></span> | <span data-ttu-id="447ca-112">Supporto</span><span class="sxs-lookup"><span data-stu-id="447ca-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="447ca-113">App Azure Information Protection</span><span class="sxs-lookup"><span data-stu-id="447ca-113">Azure Information Protection app</span></span> |![Controllo][1] |
| <span data-ttu-id="447ca-115">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="447ca-115">Microsoft Teams</span></span> |![Controllo][1] |
| <span data-ttu-id="447ca-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="447ca-117">OneNote</span></span> |![Controllo][1] |
| <span data-ttu-id="447ca-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="447ca-119">OneDrive</span></span> |![Controllo][1] |
| <span data-ttu-id="447ca-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="447ca-121">Outlook</span></span> |![Controllo][1] |
| <span data-ttu-id="447ca-123">App per dispositivi mobili di Power BI</span><span class="sxs-lookup"><span data-stu-id="447ca-123">Power BI mobile apps</span></span> |![Controllo][1] |
| <span data-ttu-id="447ca-125">Skype for Business Online</span><span class="sxs-lookup"><span data-stu-id="447ca-125">Skype for Business</span></span> |![Controllo][1] |
| <span data-ttu-id="447ca-127">Word / Excel / PowerPoint</span><span class="sxs-lookup"><span data-stu-id="447ca-127">Word / Excel / PowerPoint</span></span> |![Controllo][1] |
| <span data-ttu-id="447ca-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="447ca-129">Yammer</span></span> |![Controllo][1] |


## <a name="requirements"></a><span data-ttu-id="447ca-131">Requisiti</span><span class="sxs-lookup"><span data-stu-id="447ca-131">Requirements</span></span> 

<span data-ttu-id="447ca-132">Hello versione sistema operativo del dispositivo deve essere iOS 9 e versioni successive</span><span class="sxs-lookup"><span data-stu-id="447ca-132">hello device OS version must be iOS 9 and above</span></span> 

<span data-ttu-id="447ca-133">È necessario configurare un server federativo.</span><span class="sxs-lookup"><span data-stu-id="447ca-133">A federation server must be configured.</span></span>  

<span data-ttu-id="447ca-134">Per le applicazioni Office in iOS è richiesto Microsoft Authenticator.</span><span class="sxs-lookup"><span data-stu-id="447ca-134">Microsoft Authenticator is required for Office applications on iOS.</span></span>  

<span data-ttu-id="447ca-135">Per un certificato client toorevoke di Azure Active Directory, token ADFS hello deve avere hello seguenti attestazioni:</span><span class="sxs-lookup"><span data-stu-id="447ca-135">For Azure Active Directory toorevoke a client certificate, hello ADFS token must have hello following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="447ca-136">(hello numero di serie del certificato client hello)</span><span class="sxs-lookup"><span data-stu-id="447ca-136">(hello serial number of hello client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="447ca-137">(stringa hello per emittente hello del certificato client hello)</span><span class="sxs-lookup"><span data-stu-id="447ca-137">(hello string for hello issuer of hello client certificate)</span></span> 

<span data-ttu-id="447ca-138">Azure Active Directory aggiunge queste attestazioni toohello il token di aggiornamento se sono disponibili nel token ADFS hello (o qualsiasi altro token SAML).</span><span class="sxs-lookup"><span data-stu-id="447ca-138">Azure Active Directory adds these claims toohello refresh token if they are available in hello ADFS token (or any other SAML token).</span></span> <span data-ttu-id="447ca-139">Quando il token di aggiornamento hello deve toobe convalidato, queste informazioni sono utilizzate toocheck hello revoca.</span><span class="sxs-lookup"><span data-stu-id="447ca-139">When hello refresh token needs toobe validated, this information is used toocheck hello revocation.</span></span> 

<span data-ttu-id="447ca-140">Come procedura consigliata, è necessario aggiornare le pagine di errore hello ADFS con seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="447ca-140">As a best practice, you should update hello ADFS error pages with hello following:</span></span>

* <span data-ttu-id="447ca-141">requisito di Hello per l'installazione di Microsoft Authenticator hello in iOS</span><span class="sxs-lookup"><span data-stu-id="447ca-141">hello requirement for installing hello Microsoft Authenticator on iOS</span></span>
* <span data-ttu-id="447ca-142">Istruzioni su come tooget un certificato utente.</span><span class="sxs-lookup"><span data-stu-id="447ca-142">Instructions on how tooget a user certificate.</span></span> 

<span data-ttu-id="447ca-143">Per ulteriori informazioni, vedere [personalizzazione delle pagine di hello AD FS Sign-in](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="447ca-143">For more details, see [Customizing hello AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>

<span data-ttu-id="447ca-144">Alcune applicazioni di Office (con l'autenticazione moderna abilitata) inviare '*prompt = account di accesso*' tooAzure AD nella richiesta.</span><span class="sxs-lookup"><span data-stu-id="447ca-144">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ tooAzure AD in their request.</span></span> <span data-ttu-id="447ca-145">Per impostazione predefinita, Azure AD Converte l'oggetto in hello richiesta tooADFS troppo '*wauth = usernamepassworduri*' (richiede l'autenticazione ADFS toodo U/P) e '*wfresh = 0*' (richiede lo stato SSO tooignore ad FS ed eseguire una ripetizione dell'autenticazione) .</span><span class="sxs-lookup"><span data-stu-id="447ca-145">By default, Azure AD translates this in hello request tooADFS too‘*wauth=usernamepassworduri*’ (asks ADFS toodo U/P auth) and ‘*wfresh=0*’ (asks ADFS tooignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="447ca-146">Se si desidera tooenable basata sui certificati di autenticazione per queste App, è necessario un comportamento toomodify hello predefinito AD Azure.</span><span class="sxs-lookup"><span data-stu-id="447ca-146">If you want tooenable certificate-based authentication for these apps, you need toomodify hello default Azure AD behavior.</span></span> <span data-ttu-id="447ca-147">Solo il set di hello '*PromptLoginBehavior*' nelle impostazioni del dominio federato troppo '*disabilitato*'.</span><span class="sxs-lookup"><span data-stu-id="447ca-147">Just set hello ‘*PromptLoginBehavior*’ in your federated domain settings too‘*Disabled*‘.</span></span> <span data-ttu-id="447ca-148">È possibile utilizzare hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) tooperform cmdlet questa attività:</span><span class="sxs-lookup"><span data-stu-id="447ca-148">You can use hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet tooperform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="447ca-149">Supporto dei client Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="447ca-149">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="447ca-150">Nelle versioni iOS 9 o versione successiva, client di posta elettronica iOS native hello è supportato.</span><span class="sxs-lookup"><span data-stu-id="447ca-150">On iOS 9 or later, hello native iOS mail client is supported.</span></span> <span data-ttu-id="447ca-151">Per tutte le altre applicazioni di Exchange ActiveSync, toodetermine se questa funzionalità è supportata, contattare lo sviluppatore dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="447ca-151">For all other Exchange ActiveSync applications, toodetermine if this feature is supported, contact your application developer.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="447ca-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="447ca-152">Next steps</span></span>

<span data-ttu-id="447ca-153">Se si desidera l'autenticazione basata su certificato tooconfigure nell'ambiente in uso, vedere [Introduzione all'autenticazione basata sui certificati in Android](active-directory-certificate-based-authentication-get-started.md) per le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="447ca-153">If you want tooconfigure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>


<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
