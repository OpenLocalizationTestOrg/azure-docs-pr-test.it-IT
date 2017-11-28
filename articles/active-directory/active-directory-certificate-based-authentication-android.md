---
title: autenticazione basata su certificati aaaAzure Active Directory in Android | Documenti Microsoft
description: Informazioni sugli scenari di hello supportata e requisiti di hello per la configurazione dell'autenticazione basata su certificato nelle soluzioni con i dispositivi Android
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/28/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 148275fa3da610530c278fcd57e02e907f735d9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-android"></a><span data-ttu-id="114c5-103">Autenticazione basata su certificati di Azure Active Directory in Android</span><span class="sxs-lookup"><span data-stu-id="114c5-103">Azure Active Directory certificate-based authentication on Android</span></span>


<span data-ttu-id="114c5-104">L'autenticazione basata su certificato (CBA) consente toobe autenticato da Azure Active Directory con un certificato client in un dispositivo Windows, Android o iOS, quando ci si connette l'account di Exchange online a:</span><span class="sxs-lookup"><span data-stu-id="114c5-104">Certificate-based authentication (CBA) enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="114c5-105">Applicazioni Office per dispositivi mobili, come Microsoft Outlook e Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="114c5-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="114c5-106">Client Exchange ActiveSync (EAS)</span><span class="sxs-lookup"><span data-stu-id="114c5-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="114c5-107">Configurazione di questa funzionalità Elimina hello necessità tooenter un nome utente e la combinazione di password in determinate posta elettronica e le applicazioni di Microsoft Office sul tuo dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="114c5-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="114c5-108">In questo argomento vengono fornite hello requisiti e degli scenari di hello è supportato per la configurazione CBA in un dispositivo iOS(Android) per gli utenti del tenant Office 365 Enterprise, Business, formazione, governo, Cina, e piani Germania.</span><span class="sxs-lookup"><span data-stu-id="114c5-108">This topic provides you with hello requirements and hello supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>



<span data-ttu-id="114c5-109">Questa funzionalità è disponibile in anteprima nei piani di Office 365 US Government Defense e Federal.</span><span class="sxs-lookup"><span data-stu-id="114c5-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>


## <a name="office-mobile-applications-support"></a><span data-ttu-id="114c5-110">Supporto delle applicazioni Office per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="114c5-110">Office mobile applications support</span></span>
| <span data-ttu-id="114c5-111">App</span><span class="sxs-lookup"><span data-stu-id="114c5-111">Apps</span></span> | <span data-ttu-id="114c5-112">Supporto</span><span class="sxs-lookup"><span data-stu-id="114c5-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="114c5-113">App Azure Information Protection</span><span class="sxs-lookup"><span data-stu-id="114c5-113">Azure Information Protection app</span></span> |![Controllo][1] |
| <span data-ttu-id="114c5-115">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="114c5-115">Microsoft Teams</span></span> |![Controllo][1] |
| <span data-ttu-id="114c5-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="114c5-117">OneNote</span></span> |![Controllo][1] |
| <span data-ttu-id="114c5-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="114c5-119">OneDrive</span></span> |![Controllo][1] |
| <span data-ttu-id="114c5-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="114c5-121">Outlook</span></span> |![Controllo][1] |
| <span data-ttu-id="114c5-123">App per dispositivi mobili di Power BI</span><span class="sxs-lookup"><span data-stu-id="114c5-123">Power BI mobile apps</span></span> |![Controllo][1] |
| <span data-ttu-id="114c5-125">Skype for Business Online</span><span class="sxs-lookup"><span data-stu-id="114c5-125">Skype for Business</span></span> |![Controllo][1] |
| <span data-ttu-id="114c5-127">Word / Excel / PowerPoint</span><span class="sxs-lookup"><span data-stu-id="114c5-127">Word / Excel / PowerPoint</span></span> |![Controllo][1] |
| <span data-ttu-id="114c5-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="114c5-129">Yammer</span></span> |![Controllo][1] |


### <a name="implementation-requirements"></a><span data-ttu-id="114c5-131">Requisiti di implementazione</span><span class="sxs-lookup"><span data-stu-id="114c5-131">Implementation requirements</span></span>

<span data-ttu-id="114c5-132">Hello versione sistema operativo del dispositivo deve essere Android 5.0 (simbolo) e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="114c5-132">hello device OS version must be Android 5.0 (Lollipop) and above.</span></span> 

<span data-ttu-id="114c5-133">È necessario configurare un server federativo.</span><span class="sxs-lookup"><span data-stu-id="114c5-133">A federation server must be configured.</span></span>  

<span data-ttu-id="114c5-134">Per un certificato client toorevoke di Azure Active Directory, token ADFS hello deve avere hello seguenti attestazioni:</span><span class="sxs-lookup"><span data-stu-id="114c5-134">For Azure Active Directory toorevoke a client certificate, hello ADFS token must have hello following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="114c5-135">(hello numero di serie del certificato client hello)</span><span class="sxs-lookup"><span data-stu-id="114c5-135">(hello serial number of hello client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="114c5-136">(stringa hello per emittente hello del certificato client hello)</span><span class="sxs-lookup"><span data-stu-id="114c5-136">(hello string for hello issuer of hello client certificate)</span></span> 

<span data-ttu-id="114c5-137">Azure Active Directory aggiunge queste attestazioni toohello il token di aggiornamento se sono disponibili nel token ADFS hello (o qualsiasi altro token SAML).</span><span class="sxs-lookup"><span data-stu-id="114c5-137">Azure Active Directory adds these claims toohello refresh token if they are available in hello ADFS token (or any other SAML token).</span></span> <span data-ttu-id="114c5-138">Quando il token di aggiornamento hello deve toobe convalidato, queste informazioni sono utilizzate toocheck hello revoca.</span><span class="sxs-lookup"><span data-stu-id="114c5-138">When hello refresh token needs toobe validated, this information is used toocheck hello revocation.</span></span> 

<span data-ttu-id="114c5-139">Come procedura consigliata, è necessario aggiornare le pagine di errore hello ADFS con istruzioni su come tooget un certificato utente.</span><span class="sxs-lookup"><span data-stu-id="114c5-139">As a best practice, you should update hello ADFS error pages with instructions on how tooget a user certificate.</span></span>  
<span data-ttu-id="114c5-140">Per ulteriori informazioni, vedere [personalizzazione delle pagine di hello AD FS Sign-in](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="114c5-140">For more details, see [Customizing hello AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>  

<span data-ttu-id="114c5-141">Alcune applicazioni di Office (con l'autenticazione moderna abilitata) inviare '*prompt = account di accesso*' tooAzure AD nella richiesta.</span><span class="sxs-lookup"><span data-stu-id="114c5-141">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ tooAzure AD in their request.</span></span> <span data-ttu-id="114c5-142">Per impostazione predefinita, Azure AD Converte l'oggetto in hello richiesta tooADFS troppo '*wauth = usernamepassworduri*' (richiede l'autenticazione ADFS toodo U/P) e '*wfresh = 0*' (richiede lo stato SSO tooignore ad FS ed eseguire una ripetizione dell'autenticazione) .</span><span class="sxs-lookup"><span data-stu-id="114c5-142">By default, Azure AD translates this in hello request tooADFS too‘*wauth=usernamepassworduri*’ (asks ADFS toodo U/P auth) and ‘*wfresh=0*’ (asks ADFS tooignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="114c5-143">Se si desidera tooenable basata sui certificati di autenticazione per queste App, è necessario un comportamento toomodify hello predefinito AD Azure.</span><span class="sxs-lookup"><span data-stu-id="114c5-143">If you want tooenable certificate-based authentication for these apps, you need toomodify hello default Azure AD behavior.</span></span> <span data-ttu-id="114c5-144">Solo il set di hello '*PromptLoginBehavior*' nelle impostazioni del dominio federato troppo '*disabilitato*'.</span><span class="sxs-lookup"><span data-stu-id="114c5-144">Just set hello ‘*PromptLoginBehavior*’ in your federated domain settings too‘*Disabled*‘.</span></span> <span data-ttu-id="114c5-145">È possibile utilizzare hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) tooperform cmdlet questa attività:</span><span class="sxs-lookup"><span data-stu-id="114c5-145">You can use hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet tooperform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`



## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="114c5-146">Supporto dei client Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="114c5-146">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="114c5-147">Alcune applicazioni Exchange ActiveSync sono supportate in Android 5.0 (Lollipop) o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="114c5-147">Certain Exchange ActiveSync applications on Android 5.0 (Lollipop) or later are supported.</span></span> <span data-ttu-id="114c5-148">toodetermine se l'applicazione di posta elettronica che supportano questa funzionalità, contattare lo sviluppatore dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="114c5-148">toodetermine if your email application does support this feature, please contact your application developer.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="114c5-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="114c5-149">Next steps</span></span>

<span data-ttu-id="114c5-150">Se si desidera l'autenticazione basata su certificato tooconfigure nell'ambiente in uso, vedere [Introduzione all'autenticazione basata sui certificati in Android](active-directory-certificate-based-authentication-get-started.md) per le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="114c5-150">If you want tooconfigure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>

<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-android/ic195031.png
