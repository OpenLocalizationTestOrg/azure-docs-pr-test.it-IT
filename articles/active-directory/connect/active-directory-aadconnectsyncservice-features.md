---
title: "funzionalità e la configurazione del servizio sincronizzazione Connect aaaAzure AD | Documenti Microsoft"
description: "Descrive le funzionalità sul lato del servizio per il Servizio di sincronizzazione Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 7ad05c45bb6b5fd5deaa3466e2936b19d3d9eabb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-features"></a><span data-ttu-id="3d166-103">Funzionalità del servizio di sincronizzazione Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="3d166-103">Azure AD Connect sync service features</span></span>
<span data-ttu-id="3d166-104">funzionalità di sincronizzazione Hello di Azure AD Connect include due componenti:</span><span class="sxs-lookup"><span data-stu-id="3d166-104">hello synchronization feature of Azure AD Connect has two components:</span></span>

* <span data-ttu-id="3d166-105">componente di Hello locale denominato **sincronizzazione di Azure AD Connect**, denominati anche **motore di sincronizzazione**.</span><span class="sxs-lookup"><span data-stu-id="3d166-105">hello on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span></span>
* <span data-ttu-id="3d166-106">servizio Hello che risiedono in Azure AD, noto anche come **il servizio di sincronizzazione di Azure AD Connect**</span><span class="sxs-lookup"><span data-stu-id="3d166-106">hello service residing in Azure AD also known as **Azure AD Connect sync service**</span></span>

<span data-ttu-id="3d166-107">Questo argomento viene illustrato come hello seguenti funzionalità di hello **servizio di sincronizzazione di Azure AD Connect** lavoro e come è possibile configurare tramite Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3d166-107">This topic explains how hello following features of hello **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span></span>

<span data-ttu-id="3d166-108">Queste impostazioni vengono configurate da hello [modulo di Azure Active Directory per Windows PowerShell](http://aka.ms/aadposh).</span><span class="sxs-lookup"><span data-stu-id="3d166-108">These settings are configured by hello [Azure Active Directory Module for Windows PowerShell](http://aka.ms/aadposh).</span></span> <span data-ttu-id="3d166-109">Scaricarlo e installarlo separatamente da Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="3d166-109">Download and install it separately from Azure AD Connect.</span></span> <span data-ttu-id="3d166-110">i cmdlet di Hello illustrati in questo argomento sono state introdotte in hello [il rilascio di marzo 2016 (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span><span class="sxs-lookup"><span data-stu-id="3d166-110">hello cmdlets documented in this topic were introduced in hello [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span></span> <span data-ttu-id="3d166-111">Se i cmdlet di hello illustrati in questo argomento non si dispone o non producono hello stesso risultato, quindi assicurarsi che si esegue la versione più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="3d166-111">If you do not have hello cmdlets documented in this topic or they do not produce hello same result, then make sure you run hello latest version.</span></span>

<span data-ttu-id="3d166-112">configurazione di hello toosee nella directory di Azure AD, eseguire `Get-MsolDirSyncFeatures`.</span><span class="sxs-lookup"><span data-stu-id="3d166-112">toosee hello configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span></span>  
<span data-ttu-id="3d166-113">![Risultato di Get-MsolDirSyncFeatures](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span><span class="sxs-lookup"><span data-stu-id="3d166-113">![Get-MsolDirSyncFeatures result](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span></span>

<span data-ttu-id="3d166-114">Molte di queste impostazioni possono essere modificate solo da Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="3d166-114">Many of these settings can only be changed by Azure AD Connect.</span></span>

<span data-ttu-id="3d166-115">Hello seguenti possono essere configurate da `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="3d166-115">hello following settings can be configured by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="3d166-116">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="3d166-116">DirSyncFeature</span></span> | <span data-ttu-id="3d166-117">Commento</span><span class="sxs-lookup"><span data-stu-id="3d166-117">Comment</span></span> |
| --- | --- |
| [<span data-ttu-id="3d166-118">EnableSoftMatchOnUpn</span><span class="sxs-lookup"><span data-stu-id="3d166-118">EnableSoftMatchOnUpn</span></span>](#userprincipalname-soft-match) |<span data-ttu-id="3d166-119">Consente oggetti toojoin userPrincipalName indirizzo SMTP tooprimary aggiunta.</span><span class="sxs-lookup"><span data-stu-id="3d166-119">Allows objects toojoin on userPrincipalName in addition tooprimary SMTP address.</span></span> |
| [<span data-ttu-id="3d166-120">SynchronizeUpnForManagedUsers</span><span class="sxs-lookup"><span data-stu-id="3d166-120">SynchronizeUpnForManagedUsers</span></span>](#synchronize-userprincipalname-updates) |<span data-ttu-id="3d166-121">Consente di hello sincronizzazione motore tooupdate hello userPrincipalName attributo utenti gestiti licenza (non federati).</span><span class="sxs-lookup"><span data-stu-id="3d166-121">Allows hello sync engine tooupdate hello userPrincipalName attribute for managed/licensed (non-federated) users.</span></span> |

<span data-ttu-id="3d166-122">Una volta abilitata una funzionalità, non potrà essere disabilitata di nuovo.</span><span class="sxs-lookup"><span data-stu-id="3d166-122">After you have enabled a feature, it cannot be disabled again.</span></span>

> [!NOTE]
> <span data-ttu-id="3d166-123">Da 24 agosto 2016 hello funzionalità *duplicato resilienza attributo* è abilitata per impostazione predefinita per la nuova versione di Azure directory di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3d166-123">From August 24, 2016 hello feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span></span> <span data-ttu-id="3d166-124">Questa funzionalità sarà implementata e abilitata anche nelle directory create prima di tale data.</span><span class="sxs-lookup"><span data-stu-id="3d166-124">This feature will also be rolled out and enabled on directories created before this date.</span></span> <span data-ttu-id="3d166-125">Si riceverà una notifica di posta elettronica quando la directory sulle tooget abilitata questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3d166-125">You will receive an email notification when your directory is about tooget this feature enabled.</span></span>
> 
> 

<span data-ttu-id="3d166-126">Hello seguenti impostazioni sono configurate da Azure AD Connect e non può essere modificate da `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="3d166-126">hello following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="3d166-127">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="3d166-127">DirSyncFeature</span></span> | <span data-ttu-id="3d166-128">Commento</span><span class="sxs-lookup"><span data-stu-id="3d166-128">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="3d166-129">DeviceWriteback</span><span class="sxs-lookup"><span data-stu-id="3d166-129">DeviceWriteback</span></span> |[<span data-ttu-id="3d166-130">Azure AD Connect: abilitazione del writeback dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="3d166-130">Azure AD Connect: Enabling device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |
| <span data-ttu-id="3d166-131">DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="3d166-131">DirectoryExtensions</span></span> |[<span data-ttu-id="3d166-132">Servizio di sincronizzazione Azure AD Connect: estensioni della directory</span><span class="sxs-lookup"><span data-stu-id="3d166-132">Azure AD Connect sync: Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [<span data-ttu-id="3d166-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span><span class="sxs-lookup"><span data-stu-id="3d166-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span></span>](#duplicate-attribute-resiliency) |<span data-ttu-id="3d166-134">Consente a un attributo toobe messi in quarantena quando è un duplicato di un altro oggetto anziché errori l'intero oggetto hello durante l'esportazione.</span><span class="sxs-lookup"><span data-stu-id="3d166-134">Allows an attribute toobe quarantined when it is a duplicate of another object rather than failing hello entire object during export.</span></span> |
| <span data-ttu-id="3d166-135">PasswordSync</span><span class="sxs-lookup"><span data-stu-id="3d166-135">PasswordSync</span></span> |[<span data-ttu-id="3d166-136">Implementazione della sincronizzazione password con il servizio di sincronizzazione Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="3d166-136">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md) |
| <span data-ttu-id="3d166-137">UnifiedGroupWriteback</span><span class="sxs-lookup"><span data-stu-id="3d166-137">UnifiedGroupWriteback</span></span> |[<span data-ttu-id="3d166-138">Anteprima: Writeback dei gruppi</span><span class="sxs-lookup"><span data-stu-id="3d166-138">Preview: Group writeback</span></span>](active-directory-aadconnect-feature-preview.md#group-writeback) |
| <span data-ttu-id="3d166-139">UserWriteback</span><span class="sxs-lookup"><span data-stu-id="3d166-139">UserWriteback</span></span> |<span data-ttu-id="3d166-140">Attualmente non è supportata.</span><span class="sxs-lookup"><span data-stu-id="3d166-140">Not currently supported.</span></span> |

## <a name="duplicate-attribute-resiliency"></a><span data-ttu-id="3d166-141">Duplicate attribute resiliency</span><span class="sxs-lookup"><span data-stu-id="3d166-141">Duplicate attribute resiliency</span></span>
<span data-ttu-id="3d166-142">Anziché avere esito negativo tooprovision gli oggetti con nomi duplicati UPN / proxyAddresses, dell'attributo duplicato hello è "messi in quarantena" e viene assegnato un valore temporaneo.</span><span class="sxs-lookup"><span data-stu-id="3d166-142">Instead of failing tooprovision objects with duplicate UPNs / proxyAddresses, hello duplicated attribute is “quarantined” and a temporary value is assigned.</span></span> <span data-ttu-id="3d166-143">Quando è stato risolto il conflitto di hello, hello temporaneo UPN viene modificata automaticamente toohello di valore appropriato.</span><span class="sxs-lookup"><span data-stu-id="3d166-143">When hello conflict is resolved, hello temporary UPN is changed toohello proper value automatically.</span></span> <span data-ttu-id="3d166-144">Per altre informazioni, vedere [Sincronizzazione delle identità e resilienza degli attributi duplicati](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="3d166-144">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="userprincipalname-soft-match"></a><span data-ttu-id="3d166-145">Corrispondenza flessibile di userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="3d166-145">UserPrincipalName soft match</span></span>
<span data-ttu-id="3d166-146">Quando questa funzionalità è abilitata, soft-match è abilitata per UPN in aggiunta toohello [indirizzo SMTP primario](https://support.microsoft.com/kb/2641663), che è sempre abilitata.</span><span class="sxs-lookup"><span data-stu-id="3d166-146">When this feature is enabled, soft-match is enabled for UPN in addition toohello [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span></span> <span data-ttu-id="3d166-147">Soft-match è toomatch utilizzati gli utenti del cloud esistente in Azure AD con utenti locali.</span><span class="sxs-lookup"><span data-stu-id="3d166-147">Soft-match is used toomatch existing cloud users in Azure AD with on-premises users.</span></span>

<span data-ttu-id="3d166-148">Se è necessario toomatch AD account locali con gli account esistenti creati in un cloud hello e non si usa Exchange Online, quindi questa funzionalità è utile.</span><span class="sxs-lookup"><span data-stu-id="3d166-148">If you need toomatch on-premises AD accounts with existing accounts created in hello cloud and you are not using Exchange Online, then this feature is useful.</span></span> <span data-ttu-id="3d166-149">In questo scenario, in genere non è un attributo di motivo tooset hello SMTP nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="3d166-149">In this scenario, you generally don’t have a reason tooset hello SMTP attribute in hello cloud.</span></span>

<span data-ttu-id="3d166-150">Questa funzionalità è attivata per impostazione predefinita per le nuove directory di Azure AD .</span><span class="sxs-lookup"><span data-stu-id="3d166-150">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="3d166-151">Per vedere se la funzionalità è abilitata per l'utente corrente, eseguire:</span><span class="sxs-lookup"><span data-stu-id="3d166-151">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

<span data-ttu-id="3d166-152">Se questa funzionalità non è abilitata per la directory di Azure AD in uso, è possibile abilitarla eseguendo:</span><span class="sxs-lookup"><span data-stu-id="3d166-152">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a><span data-ttu-id="3d166-153">Sincronizzare gli aggiornamenti di userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="3d166-153">Synchronize userPrincipalName updates</span></span>
<span data-ttu-id="3d166-154">In passato, attributo UserPrincipalName toohello di aggiornamenti tramite il servizio di sincronizzazione hello locale è stato bloccato solo se entrambe queste condizioni sono vere:</span><span class="sxs-lookup"><span data-stu-id="3d166-154">Historically, updates toohello UserPrincipalName attribute using hello sync service from on-premises has been blocked, unless both of these conditions are true:</span></span>

* <span data-ttu-id="3d166-155">utente Hello è gestito (non federati).</span><span class="sxs-lookup"><span data-stu-id="3d166-155">hello user is managed (non-federated).</span></span>
* <span data-ttu-id="3d166-156">utente Hello non è stata assegnata una licenza.</span><span class="sxs-lookup"><span data-stu-id="3d166-156">hello user has not been assigned a license.</span></span>

<span data-ttu-id="3d166-157">Per ulteriori informazioni, vedere [utente non corrispondono a nomi di Office 365, Azure o Intune hello UPN locale o ID di accesso alternativo](https://support.microsoft.com/kb/2523192).</span><span class="sxs-lookup"><span data-stu-id="3d166-157">For more details, see [User names in Office 365, Azure, or Intune don't match hello on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span></span>

<span data-ttu-id="3d166-158">L'abilitazione di questa funzionalità consente hello sincronizzazione motore tooupdate hello userPrincipalName quando è modificato in locale e si utilizza la sincronizzazione delle password. Se si usa la federazione, questa funzionalità non è supportata.</span><span class="sxs-lookup"><span data-stu-id="3d166-158">Enabling this feature allows hello sync engine tooupdate hello userPrincipalName when it is changed on-premises and you use password sync. If you use federation, this feature is not supported.</span></span>

<span data-ttu-id="3d166-159">Questa funzionalità è attivata per impostazione predefinita per le nuove directory di Azure AD .</span><span class="sxs-lookup"><span data-stu-id="3d166-159">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="3d166-160">Per vedere se la funzionalità è abilitata per l'utente corrente, eseguire:</span><span class="sxs-lookup"><span data-stu-id="3d166-160">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

<span data-ttu-id="3d166-161">Se questa funzionalità non è abilitata per la directory di Azure AD in uso, è possibile abilitarla eseguendo:</span><span class="sxs-lookup"><span data-stu-id="3d166-161">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

<span data-ttu-id="3d166-162">Dopo aver abilitato questa funzionalità, i valori di userPrincipalName esistenti rimarranno invariati.</span><span class="sxs-lookup"><span data-stu-id="3d166-162">After enabling this feature, existing userPrincipalName values will remain as-is.</span></span> <span data-ttu-id="3d166-163">Al prossimo cambio di hello userPrincipalName attributo on-premise, sincronizzazione delta normale hello sugli utenti aggiornerà hello UPN.</span><span class="sxs-lookup"><span data-stu-id="3d166-163">On next change of hello userPrincipalName attribute on-premises, hello normal delta sync on users will update hello UPN.</span></span>  

## <a name="see-also"></a><span data-ttu-id="3d166-164">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="3d166-164">See also</span></span>
* [<span data-ttu-id="3d166-165">Servizio di sincronizzazione Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="3d166-165">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="3d166-166">[Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="3d166-166">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

