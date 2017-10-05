---
title: Requisiti dei dati di Azure AD SSPR | Documentazione Microsoft
description: Requisiti dei dati per la Reimpostazione self-service delle password e informazioni su come soddisfarli
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 2d1afd2d1265b371e0d311ed70fffbc55874b0a7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="a6b25-103">Distribuire la reimpostazione della password senza richiedere la registrazione dell'utente finale</span><span class="sxs-lookup"><span data-stu-id="a6b25-103">Deploy password reset without requiring end-user registration</span></span>

<span data-ttu-id="a6b25-104">La distribuzione della Reimpostazione self-service delle password (SSPR) richiede che siano presenti i dati di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="a6b25-104">Deploying Self-Service Password Reset (SSPR) requires authentication data to be present.</span></span> <span data-ttu-id="a6b25-105">Alcune organizzazioni fanno immettere autonomamente agli utenti i dati di autenticazione, ma molte organizzazioni preferiscono sincronizzarsi con i dati esistenti in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a6b25-105">Some organizations have their users enter their authentication data themselves, but many organizations prefer to synchronize with existing data in Active Directory.</span></span> <span data-ttu-id="a6b25-106">Se i dati sono stati formattati correttamente nella directory locale e si configura [Azure AD Connect tramite le impostazioni rapide](./connect/active-directory-aadconnect-get-started-express.md), quei dati vengono resi disponibili in Azure AD e SSPR senza che si richieda l'intervento dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a6b25-106">If you have properly formatted data in your on-premises directory, and configure [Azure AD Connect using express settings](./connect/active-directory-aadconnect-get-started-express.md), that data is made available to Azure AD and SSPR with no user interaction required.</span></span>

<span data-ttu-id="a6b25-107">Tutti i numeri di telefono devono essere nel formato +CountryCode PhoneNumber Esempio: + 1 4255551234 per funzionare correttamente.</span><span class="sxs-lookup"><span data-stu-id="a6b25-107">Any phone numbers must be in the format +CountryCode PhoneNumber Example: +1 4255551234 to work properly.</span></span>

> [!NOTE]
> <span data-ttu-id="a6b25-108">La reimpostazione della password non supporta le estensioni del telefono.</span><span class="sxs-lookup"><span data-stu-id="a6b25-108">Password reset does not support phone extensions.</span></span> <span data-ttu-id="a6b25-109">Anche nel formato +1 4255551234X12345, le estensioni vengono rimosse prima della chiamata.</span><span class="sxs-lookup"><span data-stu-id="a6b25-109">Even in the +1 4255551234X12345 format, extensions are removed before the call is placed.</span></span>

## <a name="fields-populated"></a><span data-ttu-id="a6b25-110">Campi popolati</span><span class="sxs-lookup"><span data-stu-id="a6b25-110">Fields populated</span></span>

<span data-ttu-id="a6b25-111">Se si usano le impostazioni predefinite in Azure AD Connect, vengono eseguiti i mapping seguenti.</span><span class="sxs-lookup"><span data-stu-id="a6b25-111">If you use the default settings in Azure AD Connect the following mappings are made.</span></span>

| <span data-ttu-id="a6b25-112">Active Directory locale</span><span class="sxs-lookup"><span data-stu-id="a6b25-112">On-premises AD</span></span> | <span data-ttu-id="a6b25-113">Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6b25-113">Azure AD</span></span> | <span data-ttu-id="a6b25-114">Informazioni di contatto per l'autenticazione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6b25-114">Azure AD Authentication contact info</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a6b25-115">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="a6b25-115">telephoneNumber</span></span> | <span data-ttu-id="a6b25-116">Telefono ufficio</span><span class="sxs-lookup"><span data-stu-id="a6b25-116">Office phone</span></span> | <span data-ttu-id="a6b25-117">Telefono alternativo</span><span class="sxs-lookup"><span data-stu-id="a6b25-117">Alternate phone</span></span> |
| <span data-ttu-id="a6b25-118">mobile</span><span class="sxs-lookup"><span data-stu-id="a6b25-118">mobile</span></span> | <span data-ttu-id="a6b25-119">Cellulare</span><span class="sxs-lookup"><span data-stu-id="a6b25-119">Mobile phone</span></span> | <span data-ttu-id="a6b25-120">Telefono</span><span class="sxs-lookup"><span data-stu-id="a6b25-120">Phone</span></span> |


## <a name="security-questions-and-answers"></a><span data-ttu-id="a6b25-121">Domande di sicurezza e risposte</span><span class="sxs-lookup"><span data-stu-id="a6b25-121">Security questions and answers</span></span>

<span data-ttu-id="a6b25-122">Domande di sicurezza e risposte sono archiviate in modo sicuro nel tenant di Azure AD e sono accessibili agli utenti esclusivamente tramite il [portale di registrazione SSPR](https://aka.ms/ssprsetup).</span><span class="sxs-lookup"><span data-stu-id="a6b25-122">Security questions and answers are stored securely in your Azure AD tenant and are only accessible to users via the [SSPR registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="a6b25-123">Gli amministratori non possono vedere o modificare il contenuto di domande e risposte di altri utenti.</span><span class="sxs-lookup"><span data-stu-id="a6b25-123">Administrators can't see or modify the contents of another users questions and answers.</span></span>

### <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="a6b25-124">Cosa accade quando un utente si registra</span><span class="sxs-lookup"><span data-stu-id="a6b25-124">What happens when a user registers</span></span>

<span data-ttu-id="a6b25-125">Quando un utente si registra, i campi seguenti vengono impostati nella pagina di registrazione:</span><span class="sxs-lookup"><span data-stu-id="a6b25-125">When a user registers, the registration page sets the following fields:</span></span>

* <span data-ttu-id="a6b25-126">Telefono per l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="a6b25-126">Authentication Phone</span></span>
* <span data-ttu-id="a6b25-127">Indirizzo di posta elettronica per l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="a6b25-127">Authentication Email</span></span>
* <span data-ttu-id="a6b25-128">Domande di sicurezza e risposte</span><span class="sxs-lookup"><span data-stu-id="a6b25-128">Security Questions and Answers</span></span>

<span data-ttu-id="a6b25-129">Se è stato specificato un valore per **Cellulare** o **Indirizzo di posta elettronica alternativo**, gli utenti possono usare immediatamente questi valori per reimpostare le password, anche se non hanno eseguito la registrazione per il servizio.</span><span class="sxs-lookup"><span data-stu-id="a6b25-129">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those values to reset their passwords, even if they haven't registered for the service.</span></span> <span data-ttu-id="a6b25-130">Gli utenti visualizzano e possono anche modificare tali valori quando si registrano per la prima volta.</span><span class="sxs-lookup"><span data-stu-id="a6b25-130">In addition, users see those values when registering for the first time, and modify them if they wish.</span></span> <span data-ttu-id="a6b25-131">Dopo aver completato la registrazione, questi valori vengono salvati in modo permanente rispettivamente nei campi **Telefono per l'autenticazione** e **Indirizzo di posta elettronica per l'autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="a6b25-131">After they successfully register, these values will be persisted in the **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

## <a name="set-and-read-authentication-data-using-powershell"></a><span data-ttu-id="a6b25-132">Impostare e leggere i dati di autenticazione tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6b25-132">Set and read authentication data using PowerShell</span></span>

<span data-ttu-id="a6b25-133">I campi seguenti possono essere impostati tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6b25-133">The following fields can be set using PowerShell</span></span>

* <span data-ttu-id="a6b25-134">Indirizzo di posta elettronica alternativo</span><span class="sxs-lookup"><span data-stu-id="a6b25-134">Alternate Email</span></span>
* <span data-ttu-id="a6b25-135">Cellulare</span><span class="sxs-lookup"><span data-stu-id="a6b25-135">Mobile Phone</span></span>
* <span data-ttu-id="a6b25-136">Telefono ufficio - può essere impostato solo se non in sincronizzazione con una directory locale</span><span class="sxs-lookup"><span data-stu-id="a6b25-136">Office Phone - Can only be set if not synchronizing with an on-premises directory</span></span>

### <a name="using-powershell-v1"></a><span data-ttu-id="a6b25-137">Tramite PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="a6b25-137">Using PowerShell V1</span></span>

<span data-ttu-id="a6b25-138">Per iniziare, è necessario [scaricare e installare il modulo di Azure AD PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span><span class="sxs-lookup"><span data-stu-id="a6b25-138">To get started, you need to [download and install the Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span> <span data-ttu-id="a6b25-139">Al termine dell'installazione, è possibile seguire la procedura seguente per configurare tutti i campi.</span><span class="sxs-lookup"><span data-stu-id="a6b25-139">Once you have it installed, you can follow the steps that follow to configure each field.</span></span>

#### <a name="set-authentication-data-with-powershell-v1"></a><span data-ttu-id="a6b25-140">Impostare i Dati di autenticazione con PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="a6b25-140">Set Authentication Data with PowerShell V1</span></span>

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a><span data-ttu-id="a6b25-141">Leggere i Dati di autenticazione con PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="a6b25-141">Read Authentication Data with PowerShellPowerShell V1</span></span>

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-the-commands-that-follow"></a><span data-ttu-id="a6b25-142">L'Autenticazione tramite telefono e l'Autenticazione tramite posta elettronica possono essere lette solo tramite Powershell V1 usando i comandi che seguono</span><span class="sxs-lookup"><span data-stu-id="a6b25-142">Authentication Phone and Authentication Email can only be read using Powershell V1 using the commands that follow</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a><span data-ttu-id="a6b25-143">Tramite PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="a6b25-143">Using PowerShell V2</span></span>

<span data-ttu-id="a6b25-144">Per iniziare, è necessario [scaricare e installare il modulo di Azure AD PowerShell V2](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="a6b25-144">To get started, you need to [download and install the Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span></span> <span data-ttu-id="a6b25-145">Al termine dell'installazione, è possibile seguire la procedura seguente per configurare tutti i campi.</span><span class="sxs-lookup"><span data-stu-id="a6b25-145">Once you have it installed, you can follow the steps that follow to configure each field.</span></span>

<span data-ttu-id="a6b25-146">Per eseguire rapidamente l'installazione da versioni recenti di PowerShell che supportano Install-Module, eseguire questi comandi (la prima riga verifica semplicemente se l'installazione è già stata eseguita):</span><span class="sxs-lookup"><span data-stu-id="a6b25-146">To install quickly from recent versions of PowerShell that support Install-Module, run these commands (the first line simply checks to see if it's installed already):</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a><span data-ttu-id="a6b25-147">Impostare i Dati di autenticazione con PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="a6b25-147">Set Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a><span data-ttu-id="a6b25-148">Leggere i Dati di autenticazione con PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="a6b25-148">Read Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a><span data-ttu-id="a6b25-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a6b25-149">Next steps</span></span>

<span data-ttu-id="a6b25-150">I collegamenti seguenti forniscono altre informazioni sull'uso della reimpostazione della password con Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6b25-150">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="a6b25-151">[**Guida introduttiva**](active-directory-passwords-getting-started.md) - Iniziare a usare la gestione self-service delle password di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6b25-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="a6b25-152">[**Licenze**](active-directory-passwords-licensing.md) - configurare le licenze di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6b25-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="a6b25-153">[**Implementazione**](active-directory-passwords-best-practices.md) - pianificare e distribuire agli utenti la reimpostazione password self-service usando le istruzioni disponibili in questo articolo</span><span class="sxs-lookup"><span data-stu-id="a6b25-153">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="a6b25-154">[**Personalizzazione**](active-directory-passwords-customize.md) - personalizzare l'aspetto dell'esperienza della reimpostazione password self-service per l'azienda.</span><span class="sxs-lookup"><span data-stu-id="a6b25-154">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="a6b25-155">[**Criteri**](active-directory-passwords-policy.md) - comprendere e impostare i criteri password di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6b25-155">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="a6b25-156">[**Creazione di report**](active-directory-passwords-reporting.md) - verificare se, quando e dove gli utenti accedono alla reimpostazione password self-service</span><span class="sxs-lookup"><span data-stu-id="a6b25-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="a6b25-157">[**Approfondimento tecnico**](active-directory-passwords-how-it-works.md): approfondimento sul funzionamento</span><span class="sxs-lookup"><span data-stu-id="a6b25-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="a6b25-158">[**Domande frequenti**](active-directory-passwords-faq.md) - Come</span><span class="sxs-lookup"><span data-stu-id="a6b25-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="a6b25-159">Perché?</span><span class="sxs-lookup"><span data-stu-id="a6b25-159">Why?</span></span> <span data-ttu-id="a6b25-160">Cosa?</span><span class="sxs-lookup"><span data-stu-id="a6b25-160">What?</span></span> <span data-ttu-id="a6b25-161">Dove?</span><span class="sxs-lookup"><span data-stu-id="a6b25-161">Where?</span></span> <span data-ttu-id="a6b25-162">Chi?</span><span class="sxs-lookup"><span data-stu-id="a6b25-162">Who?</span></span> <span data-ttu-id="a6b25-163">Quando?</span><span class="sxs-lookup"><span data-stu-id="a6b25-163">When?</span></span> <span data-ttu-id="a6b25-164">- Risposte alle domande di maggiore interesse</span><span class="sxs-lookup"><span data-stu-id="a6b25-164">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="a6b25-165">[**Risoluzione dei problemi**](active-directory-passwords-troubleshoot.md): informazioni su come risolvere i problemi comuni con la reimpostazione password self-service</span><span class="sxs-lookup"><span data-stu-id="a6b25-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>
