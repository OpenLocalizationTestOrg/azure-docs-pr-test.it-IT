---
title: Requisiti dei dati di Azure AD SSPR | Documentazione Microsoft
description: Reimpostare i requisiti di dati per la password self-service di Azure AD e come toosatisfy li
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
ms.openlocfilehash: b68a1d7914dcd0bb4509d0e94914dc4309f4463a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="31f16-103">Distribuire la reimpostazione della password senza richiedere la registrazione dell'utente finale</span><span class="sxs-lookup"><span data-stu-id="31f16-103">Deploy password reset without requiring end-user registration</span></span>

<span data-ttu-id="31f16-104">La distribuzione di reimpostazione di Password Self-Service (SSPR) richiede l'autenticazione dati toobe presente.</span><span class="sxs-lookup"><span data-stu-id="31f16-104">Deploying Self-Service Password Reset (SSPR) requires authentication data toobe present.</span></span> <span data-ttu-id="31f16-105">Alcune organizzazioni hanno agli utenti di immettere i dati di autenticazione se stessi, ma molte organizzazioni preferiscono toosynchronize con i dati esistenti in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="31f16-105">Some organizations have their users enter their authentication data themselves, but many organizations prefer toosynchronize with existing data in Active Directory.</span></span> <span data-ttu-id="31f16-106">Se i dati siano formattati correttamente nella directory locale e configurare [Azure AD Connect impostazioni rapide](./connect/active-directory-aadconnect-get-started-express.md), che i dati vengono resi disponibili tooAzure AD e SSPR, senza l'intervento dell'utente necessari.</span><span class="sxs-lookup"><span data-stu-id="31f16-106">If you have properly formatted data in your on-premises directory, and configure [Azure AD Connect using express settings](./connect/active-directory-aadconnect-get-started-express.md), that data is made available tooAzure AD and SSPR with no user interaction required.</span></span>

<span data-ttu-id="31f16-107">Tutti i numeri di telefono devono essere in formato hello + esempio di PhoneNumber CountryCode: + 1 4255551234 toowork correttamente.</span><span class="sxs-lookup"><span data-stu-id="31f16-107">Any phone numbers must be in hello format +CountryCode PhoneNumber Example: +1 4255551234 toowork properly.</span></span>

> [!NOTE]
> <span data-ttu-id="31f16-108">La reimpostazione della password non supporta le estensioni del telefono.</span><span class="sxs-lookup"><span data-stu-id="31f16-108">Password reset does not support phone extensions.</span></span> <span data-ttu-id="31f16-109">Anche in formato 12345 4255551234 + 1 X di hello, le estensioni vengono rimossi prima viene effettuata la chiamata di hello.</span><span class="sxs-lookup"><span data-stu-id="31f16-109">Even in hello +1 4255551234X12345 format, extensions are removed before hello call is placed.</span></span>

## <a name="fields-populated"></a><span data-ttu-id="31f16-110">Campi popolati</span><span class="sxs-lookup"><span data-stu-id="31f16-110">Fields populated</span></span>

<span data-ttu-id="31f16-111">Se si utilizzano le impostazioni predefinite di hello in Azure AD Connect hello seguenti vengono eseguiti mapping.</span><span class="sxs-lookup"><span data-stu-id="31f16-111">If you use hello default settings in Azure AD Connect hello following mappings are made.</span></span>

| <span data-ttu-id="31f16-112">Active Directory locale</span><span class="sxs-lookup"><span data-stu-id="31f16-112">On-premises AD</span></span> | <span data-ttu-id="31f16-113">Azure AD</span><span class="sxs-lookup"><span data-stu-id="31f16-113">Azure AD</span></span> | <span data-ttu-id="31f16-114">Informazioni di contatto per l'autenticazione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="31f16-114">Azure AD Authentication contact info</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31f16-115">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="31f16-115">telephoneNumber</span></span> | <span data-ttu-id="31f16-116">Telefono ufficio</span><span class="sxs-lookup"><span data-stu-id="31f16-116">Office phone</span></span> | <span data-ttu-id="31f16-117">Telefono alternativo</span><span class="sxs-lookup"><span data-stu-id="31f16-117">Alternate phone</span></span> |
| <span data-ttu-id="31f16-118">mobile</span><span class="sxs-lookup"><span data-stu-id="31f16-118">mobile</span></span> | <span data-ttu-id="31f16-119">Cellulare</span><span class="sxs-lookup"><span data-stu-id="31f16-119">Mobile phone</span></span> | <span data-ttu-id="31f16-120">Telefono</span><span class="sxs-lookup"><span data-stu-id="31f16-120">Phone</span></span> |


## <a name="security-questions-and-answers"></a><span data-ttu-id="31f16-121">Domande di sicurezza e risposte</span><span class="sxs-lookup"><span data-stu-id="31f16-121">Security questions and answers</span></span>

<span data-ttu-id="31f16-122">Domande di sicurezza e le risposte vengono archiviate in modo sicuro nel tenant di Azure AD e sono solo accessibili toousers tramite hello [portale di registrazione SSPR](https://aka.ms/ssprsetup).</span><span class="sxs-lookup"><span data-stu-id="31f16-122">Security questions and answers are stored securely in your Azure AD tenant and are only accessible toousers via hello [SSPR registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="31f16-123">Gli amministratori possono visualizzare o modificare contenuto hello di un altro utenti domande frequenti.</span><span class="sxs-lookup"><span data-stu-id="31f16-123">Administrators can't see or modify hello contents of another users questions and answers.</span></span>

### <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="31f16-124">Cosa accade quando un utente si registra</span><span class="sxs-lookup"><span data-stu-id="31f16-124">What happens when a user registers</span></span>

<span data-ttu-id="31f16-125">Quando un utente registra, pagina di registrazione hello imposta hello seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="31f16-125">When a user registers, hello registration page sets hello following fields:</span></span>

* <span data-ttu-id="31f16-126">Telefono per l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="31f16-126">Authentication Phone</span></span>
* <span data-ttu-id="31f16-127">Indirizzo di posta elettronica per l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="31f16-127">Authentication Email</span></span>
* <span data-ttu-id="31f16-128">Domande di sicurezza e risposte</span><span class="sxs-lookup"><span data-stu-id="31f16-128">Security Questions and Answers</span></span>

<span data-ttu-id="31f16-129">Se è stato specificato un valore per **cellulare** o **posta elettronica alternativo**, gli utenti possono utilizzare immediatamente tooreset tali valori le password, anche se non sono stati registrati per il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="31f16-129">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those values tooreset their passwords, even if they haven't registered for hello service.</span></span> <span data-ttu-id="31f16-130">Inoltre, gli utenti visualizzati tali valori durante la registrazione per hello prima volta e modificarle se necessario.</span><span class="sxs-lookup"><span data-stu-id="31f16-130">In addition, users see those values when registering for hello first time, and modify them if they wish.</span></span> <span data-ttu-id="31f16-131">Dopo la registrazione sono correttamente, tali valori verranno mantenuti nel hello **telefono per l'autenticazione** e **posta elettronica di autenticazione** campi, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="31f16-131">After they successfully register, these values will be persisted in hello **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

## <a name="set-and-read-authentication-data-using-powershell"></a><span data-ttu-id="31f16-132">Impostare e leggere i dati di autenticazione tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="31f16-132">Set and read authentication data using PowerShell</span></span>

<span data-ttu-id="31f16-133">Hello seguente i campi può essere impostata mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="31f16-133">hello following fields can be set using PowerShell</span></span>

* <span data-ttu-id="31f16-134">Indirizzo di posta elettronica alternativo</span><span class="sxs-lookup"><span data-stu-id="31f16-134">Alternate Email</span></span>
* <span data-ttu-id="31f16-135">Cellulare</span><span class="sxs-lookup"><span data-stu-id="31f16-135">Mobile Phone</span></span>
* <span data-ttu-id="31f16-136">Telefono ufficio - può essere impostato solo se non in sincronizzazione con una directory locale</span><span class="sxs-lookup"><span data-stu-id="31f16-136">Office Phone - Can only be set if not synchronizing with an on-premises directory</span></span>

### <a name="using-powershell-v1"></a><span data-ttu-id="31f16-137">Tramite PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="31f16-137">Using PowerShell V1</span></span>

<span data-ttu-id="31f16-138">tooget avviato, è necessario troppo[scaricare e installare il modulo di Azure AD PowerShell hello](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span><span class="sxs-lookup"><span data-stu-id="31f16-138">tooget started, you need too[download and install hello Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span> <span data-ttu-id="31f16-139">Dopo aver installato, è possibile seguire i passaggi di hello che seguono tooconfigure ogni campo.</span><span class="sxs-lookup"><span data-stu-id="31f16-139">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

#### <a name="set-authentication-data-with-powershell-v1"></a><span data-ttu-id="31f16-140">Impostare i Dati di autenticazione con PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="31f16-140">Set Authentication Data with PowerShell V1</span></span>

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a><span data-ttu-id="31f16-141">Leggere i Dati di autenticazione con PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="31f16-141">Read Authentication Data with PowerShellPowerShell V1</span></span>

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-hello-commands-that-follow"></a><span data-ttu-id="31f16-142">Telefono per l'autenticazione e la posta elettronica di autenticazione possono solo essere letti utilizzando Powershell V1 hello utilizzando i comandi che seguono</span><span class="sxs-lookup"><span data-stu-id="31f16-142">Authentication Phone and Authentication Email can only be read using Powershell V1 using hello commands that follow</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a><span data-ttu-id="31f16-143">Tramite PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="31f16-143">Using PowerShell V2</span></span>

<span data-ttu-id="31f16-144">tooget avviato, è necessario troppo[scaricare e installare il modulo di PowerShell hello Azure Active Directory V2](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="31f16-144">tooget started, you need too[download and install hello Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span></span> <span data-ttu-id="31f16-145">Dopo aver installato, è possibile seguire i passaggi di hello che seguono tooconfigure ogni campo.</span><span class="sxs-lookup"><span data-stu-id="31f16-145">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

<span data-ttu-id="31f16-146">tooinstall rapidamente da versioni recenti di PowerShell che supportano Install-Module, eseguire questi comandi (prima riga hello controlla semplicemente toosee se è già installato):</span><span class="sxs-lookup"><span data-stu-id="31f16-146">tooinstall quickly from recent versions of PowerShell that support Install-Module, run these commands (hello first line simply checks toosee if it's installed already):</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a><span data-ttu-id="31f16-147">Impostare i Dati di autenticazione con PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="31f16-147">Set Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a><span data-ttu-id="31f16-148">Leggere i Dati di autenticazione con PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="31f16-148">Read Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a><span data-ttu-id="31f16-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="31f16-149">Next steps</span></span>

<span data-ttu-id="31f16-150">Hello seguenti collegamenti fornisce ulteriori informazioni sull'uso di Azure AD di reimpostazione della password</span><span class="sxs-lookup"><span data-stu-id="31f16-150">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="31f16-151">[**Guida introduttiva**](active-directory-passwords-getting-started.md) - Iniziare a usare la gestione self-service delle password di Azure AD</span><span class="sxs-lookup"><span data-stu-id="31f16-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="31f16-152">[**Licenze**](active-directory-passwords-licensing.md) - configurare le licenze di Azure AD</span><span class="sxs-lookup"><span data-stu-id="31f16-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="31f16-153">[**Implementazione** ](active-directory-passwords-best-practices.md) -pianificare e distribuire agli utenti di tooyour SSPR utilizzando istruzioni hello disponibili qui</span><span class="sxs-lookup"><span data-stu-id="31f16-153">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="31f16-154">[**Personalizzare** ](active-directory-passwords-customize.md) -personalizzare hello aspetto di hello SSPR esperienza per l'azienda.</span><span class="sxs-lookup"><span data-stu-id="31f16-154">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="31f16-155">[**Criteri**](active-directory-passwords-policy.md): comprendere e impostare i criteri password di Azure AD</span><span class="sxs-lookup"><span data-stu-id="31f16-155">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="31f16-156">[**Creazione di report**](active-directory-passwords-reporting.md) - verificare se, quando e dove gli utenti accedono alla reimpostazione password self-service</span><span class="sxs-lookup"><span data-stu-id="31f16-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="31f16-157">[**Approfondimento tecnico** ](active-directory-passwords-how-it-works.md) -Vai dietro hello pannelli toounderstand come funziona</span><span class="sxs-lookup"><span data-stu-id="31f16-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="31f16-158">[**Domande frequenti**](active-directory-passwords-faq.md) - Come</span><span class="sxs-lookup"><span data-stu-id="31f16-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="31f16-159">Perché?</span><span class="sxs-lookup"><span data-stu-id="31f16-159">Why?</span></span> <span data-ttu-id="31f16-160">Cosa?</span><span class="sxs-lookup"><span data-stu-id="31f16-160">What?</span></span> <span data-ttu-id="31f16-161">Dove?</span><span class="sxs-lookup"><span data-stu-id="31f16-161">Where?</span></span> <span data-ttu-id="31f16-162">Chi?</span><span class="sxs-lookup"><span data-stu-id="31f16-162">Who?</span></span> <span data-ttu-id="31f16-163">Quando?</span><span class="sxs-lookup"><span data-stu-id="31f16-163">When?</span></span> <span data-ttu-id="31f16-164">-Risposte tooquestions si desiderava sempre tooask</span><span class="sxs-lookup"><span data-stu-id="31f16-164">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="31f16-165">[**Risoluzione dei problemi** ](active-directory-passwords-troubleshoot.md) -informazioni su come tooresolve comuni problemi che vedremo con SSPR</span><span class="sxs-lookup"><span data-stu-id="31f16-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
