---
title: Autenticazione basata su certificati di Azure Active Directory in iOS | Documentazione Microsoft
description: Informazioni sugli scenari supportati e i requisiti per configurare l'autenticazione basata su certificati nelle soluzioni con i dispositivi iOS
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
ms.openlocfilehash: c781f3f054fad5c5092fed5058c932fd4e97cf35
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a><span data-ttu-id="d2790-103">Autenticazione basata su certificati di Azure Active Directory in iOS</span><span class="sxs-lookup"><span data-stu-id="d2790-103">Azure Active Directory certificate-based authentication on iOS</span></span>

<span data-ttu-id="d2790-104">L'autenticazione basata su certificati (CBA) consente di essere autenticati da Azure Active Directory con un certificato client su un dispositivo Windows, Android o iOS quando si connette il proprio account Exchange online a:</span><span class="sxs-lookup"><span data-stu-id="d2790-104">Certificate-based authentication (CBA) enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="d2790-105">Applicazioni Office per dispositivi mobili, come Microsoft Outlook e Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="d2790-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="d2790-106">Client Exchange ActiveSync (EAS)</span><span class="sxs-lookup"><span data-stu-id="d2790-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="d2790-107">La configurazione di questa funzionalità elimina la necessità di immettere una combinazione di nome utente e password in determinate applicazioni di posta e applicazioni Microsoft Office sul dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="d2790-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="d2790-108">Questo argomento indica i requisiti e gli scenari supportati per la configurazione dell'autenticazione basata su certificati su un dispositivo iOS (Android) per gli utenti dei tenant nei piani di Office 365 Enterprise, Business, Education, US Government, China e Germany.</span><span class="sxs-lookup"><span data-stu-id="d2790-108">This topic provides you with the requirements and the supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>

<span data-ttu-id="d2790-109">Questa funzionalità è disponibile in anteprima nei piani di Office 365 US Government Defense e Federal.</span><span class="sxs-lookup"><span data-stu-id="d2790-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>




## <a name="office-mobile-applications-support"></a><span data-ttu-id="d2790-110">Supporto delle applicazioni Office per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="d2790-110">Office mobile applications support</span></span>

| <span data-ttu-id="d2790-111">App</span><span class="sxs-lookup"><span data-stu-id="d2790-111">Apps</span></span> | <span data-ttu-id="d2790-112">Supporto</span><span class="sxs-lookup"><span data-stu-id="d2790-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="d2790-113">App Azure Information Protection</span><span class="sxs-lookup"><span data-stu-id="d2790-113">Azure Information Protection app</span></span> |![Controllo][1] |
| <span data-ttu-id="d2790-115">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d2790-115">Microsoft Teams</span></span> |![Controllo][1] |
| <span data-ttu-id="d2790-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="d2790-117">OneNote</span></span> |![Controllo][1] |
| <span data-ttu-id="d2790-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="d2790-119">OneDrive</span></span> |![Controllo][1] |
| <span data-ttu-id="d2790-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="d2790-121">Outlook</span></span> |![Controllo][1] |
| <span data-ttu-id="d2790-123">App per dispositivi mobili di Power BI</span><span class="sxs-lookup"><span data-stu-id="d2790-123">Power BI mobile apps</span></span> |![Controllo][1] |
| <span data-ttu-id="d2790-125">Skype for Business Online</span><span class="sxs-lookup"><span data-stu-id="d2790-125">Skype for Business</span></span> |![Controllo][1] |
| <span data-ttu-id="d2790-127">Word / Excel / PowerPoint</span><span class="sxs-lookup"><span data-stu-id="d2790-127">Word / Excel / PowerPoint</span></span> |![Controllo][1] |
| <span data-ttu-id="d2790-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="d2790-129">Yammer</span></span> |![Controllo][1] |


## <a name="requirements"></a><span data-ttu-id="d2790-131">Requisiti</span><span class="sxs-lookup"><span data-stu-id="d2790-131">Requirements</span></span> 

<span data-ttu-id="d2790-132">La versione del sistema operativo del dispositivo deve essere iOS 9 o successiva</span><span class="sxs-lookup"><span data-stu-id="d2790-132">The device OS version must be iOS 9 and above</span></span> 

<span data-ttu-id="d2790-133">È necessario configurare un server federativo.</span><span class="sxs-lookup"><span data-stu-id="d2790-133">A federation server must be configured.</span></span>  

<span data-ttu-id="d2790-134">Per le applicazioni Office in iOS è richiesto Microsoft Authenticator.</span><span class="sxs-lookup"><span data-stu-id="d2790-134">Microsoft Authenticator is required for Office applications on iOS.</span></span>  

<span data-ttu-id="d2790-135">Perché Azure Active Directory possa revocare un certificato client, il token ADFS deve avere le attestazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d2790-135">For Azure Active Directory to revoke a client certificate, the ADFS token must have the following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="d2790-136">(Il numero di serie del certificato client)</span><span class="sxs-lookup"><span data-stu-id="d2790-136">(The serial number of the client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="d2790-137">(La stringa per l'autorità emittente del certificato client)</span><span class="sxs-lookup"><span data-stu-id="d2790-137">(The string for the issuer of the client certificate)</span></span> 

<span data-ttu-id="d2790-138">Azure Active Directory aggiunge queste attestazioni per il token di aggiornamento se sono disponibili nel token ADFS (o in qualsiasi altro token SAML).</span><span class="sxs-lookup"><span data-stu-id="d2790-138">Azure Active Directory adds these claims to the refresh token if they are available in the ADFS token (or any other SAML token).</span></span> <span data-ttu-id="d2790-139">Quando il token di aggiornamento deve essere convalidato, queste informazioni vengono usate per controllare la revoca.</span><span class="sxs-lookup"><span data-stu-id="d2790-139">When the refresh token needs to be validated, this information is used to check the revocation.</span></span> 

<span data-ttu-id="d2790-140">Come procedura consigliata, è necessario aggiornare le pagine di errore di ADFS con le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d2790-140">As a best practice, you should update the ADFS error pages with the following:</span></span>

* <span data-ttu-id="d2790-141">Il requisito dell'installazione di Microsoft Authenticator in iOS</span><span class="sxs-lookup"><span data-stu-id="d2790-141">The requirement for installing the Microsoft Authenticator on iOS</span></span>
* <span data-ttu-id="d2790-142">Istruzioni su come ottenere un certificato utente.</span><span class="sxs-lookup"><span data-stu-id="d2790-142">Instructions on how to get a user certificate.</span></span> 

<span data-ttu-id="d2790-143">Per altre informazioni, vedere [Personalizzazione delle pagine di accesso ad AD FS](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="d2790-143">For more details, see [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>

<span data-ttu-id="d2790-144">Alcune app di Office, in cui non è abilitata l'autenticazione moderna, inviano "*prompt=login*" ad Azure AD nella richiesta.</span><span class="sxs-lookup"><span data-stu-id="d2790-144">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ to Azure AD in their request.</span></span> <span data-ttu-id="d2790-145">Per impostazione predefinita, Azure AD lo traduce in una richiesta ad AD FS di eseguire l'autorizzazione di nome utente e password, ovvero "*wauth=usernamepassworduri*", e di ignorare lo stato SSO ed eseguire una nuova autenticazione, ovvero "*wfresh=0*".</span><span class="sxs-lookup"><span data-stu-id="d2790-145">By default, Azure AD translates this in the request to ADFS to ‘*wauth=usernamepassworduri*’ (asks ADFS to do U/P auth) and ‘*wfresh=0*’ (asks ADFS to ignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="d2790-146">Per abilitare l'autenticazione basata su certificati per queste applicazioni, è necessario modificare il comportamento predefinito di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2790-146">If you want to enable certificate-based authentication for these apps, you need to modify the default Azure AD behavior.</span></span> <span data-ttu-id="d2790-147">È sufficiente impostare "*PromptLoginBehavior*" tra le impostazioni del dominio federato su "*Disabled*" (Disabilitato).</span><span class="sxs-lookup"><span data-stu-id="d2790-147">Just set the ‘*PromptLoginBehavior*’ in your federated domain settings to ‘*Disabled*‘.</span></span> <span data-ttu-id="d2790-148">Per eseguire questa operazione è possibile usare il cmdlet [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0):</span><span class="sxs-lookup"><span data-stu-id="d2790-148">You can use the [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet to perform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="d2790-149">Supporto dei client Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="d2790-149">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="d2790-150">In iOS 9 o versioni successive è supportato il client di posta iOS nativo.</span><span class="sxs-lookup"><span data-stu-id="d2790-150">On iOS 9 or later, the native iOS mail client is supported.</span></span> <span data-ttu-id="d2790-151">Per tutte le altre applicazioni Exchange ActiveSync, contattare lo sviluppatore dell'applicazione per determinare se questa funzionalità è supportata.</span><span class="sxs-lookup"><span data-stu-id="d2790-151">For all other Exchange ActiveSync applications, to determine if this feature is supported, contact your application developer.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="d2790-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d2790-152">Next steps</span></span>

<span data-ttu-id="d2790-153">Se si desidera configurare l'autenticazione basata su certificati nel proprio ambiente, vedere [Introduzione all'autenticazione basata su certificati in Android](active-directory-certificate-based-authentication-get-started.md) per le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="d2790-153">If you want to configure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>


<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
