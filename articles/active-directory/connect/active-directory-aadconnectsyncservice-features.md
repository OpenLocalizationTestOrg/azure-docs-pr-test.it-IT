---
title: "Funzionalità e configurazione del Servizio di sincronizzazione Azure AD Connect | Documentazione Microsoft"
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
ms.openlocfilehash: c2873510c280a2683c235cfdce3d2617c3b665cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-service-features"></a><span data-ttu-id="2ffdd-103">Funzionalità del servizio di sincronizzazione Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="2ffdd-103">Azure AD Connect sync service features</span></span>
<span data-ttu-id="2ffdd-104">La funzionalità di sincronizzazione di Azure AD Connect include due componenti:</span><span class="sxs-lookup"><span data-stu-id="2ffdd-104">The synchronization feature of Azure AD Connect has two components:</span></span>

* <span data-ttu-id="2ffdd-105">Il componente locale, ovvero l'utilità di **sincronizzazione Azure AD Connect** detta anche **motore di sincronizzazione**.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-105">The on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span></span>
* <span data-ttu-id="2ffdd-106">Il servizio residente in Azure AD, noto anche come **Servizio di sincronizzazione Azure AD Connect**</span><span class="sxs-lookup"><span data-stu-id="2ffdd-106">The service residing in Azure AD also known as **Azure AD Connect sync service**</span></span>

<span data-ttu-id="2ffdd-107">Questo argomento illustra l'utilizzo delle funzionalità del **Servizio di sincronizzazione Azure AD Connect** seguenti e come è possibile configurarle e usarle con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-107">This topic explains how the following features of the **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span></span>

<span data-ttu-id="2ffdd-108">Queste impostazioni sono configurate tramite il [Modulo di Microsoft Azure Active Directory per Windows PowerShell](http://aka.ms/aadposh).</span><span class="sxs-lookup"><span data-stu-id="2ffdd-108">These settings are configured by the [Azure Active Directory Module for Windows PowerShell](http://aka.ms/aadposh).</span></span> <span data-ttu-id="2ffdd-109">Scaricarlo e installarlo separatamente da Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-109">Download and install it separately from Azure AD Connect.</span></span> <span data-ttu-id="2ffdd-110">I cmdlet documentati in questo argomento sono stati introdotti nella [versione di marzo 2016 (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span><span class="sxs-lookup"><span data-stu-id="2ffdd-110">The cmdlets documented in this topic were introduced in the [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span></span> <span data-ttu-id="2ffdd-111">Se i cmdlet documentati in questo argomento non sono disponibili o non producono lo stesso risultato, assicurarsi di eseguire la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-111">If you do not have the cmdlets documented in this topic or they do not produce the same result, then make sure you run the latest version.</span></span>

<span data-ttu-id="2ffdd-112">Per visualizzare la configurazione nella directory di Azure AD, eseguire `Get-MsolDirSyncFeatures`.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-112">To see the configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span></span>  
<span data-ttu-id="2ffdd-113">![Risultato di Get-MsolDirSyncFeatures](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span><span class="sxs-lookup"><span data-stu-id="2ffdd-113">![Get-MsolDirSyncFeatures result](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span></span>

<span data-ttu-id="2ffdd-114">Molte di queste impostazioni possono essere modificate solo da Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-114">Many of these settings can only be changed by Azure AD Connect.</span></span>

<span data-ttu-id="2ffdd-115">Di seguito sono riportate le impostazioni che possono essere configurate da `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="2ffdd-115">The following settings can be configured by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="2ffdd-116">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="2ffdd-116">DirSyncFeature</span></span> | <span data-ttu-id="2ffdd-117">Commento</span><span class="sxs-lookup"><span data-stu-id="2ffdd-117">Comment</span></span> |
| --- | --- |
| [<span data-ttu-id="2ffdd-118">EnableSoftMatchOnUpn</span><span class="sxs-lookup"><span data-stu-id="2ffdd-118">EnableSoftMatchOnUpn</span></span>](#userprincipalname-soft-match) |<span data-ttu-id="2ffdd-119">Consente l'aggiunta di oggetti a userPrincipalName oltre all'indirizzo SMTP primario.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-119">Allows objects to join on userPrincipalName in addition to primary SMTP address.</span></span> |
| [<span data-ttu-id="2ffdd-120">SynchronizeUpnForManagedUsers</span><span class="sxs-lookup"><span data-stu-id="2ffdd-120">SynchronizeUpnForManagedUsers</span></span>](#synchronize-userprincipalname-updates) |<span data-ttu-id="2ffdd-121">Consente al motore di sincronizzazione di aggiornare l'attributo userPrincipalName per gli utenti gestiti/con licenza (non federati).</span><span class="sxs-lookup"><span data-stu-id="2ffdd-121">Allows the sync engine to update the userPrincipalName attribute for managed/licensed (non-federated) users.</span></span> |

<span data-ttu-id="2ffdd-122">Una volta abilitata una funzionalità, non potrà essere disabilitata di nuovo.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-122">After you have enabled a feature, it cannot be disabled again.</span></span>

> [!NOTE]
> <span data-ttu-id="2ffdd-123">Dal 24 agosto 2016, la funzionalità *Duplicate attribute resiliency* (Resilienza degli attributi duplicati) è abilitata per impostazione predefinita per le nuove directory di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-123">From August 24, 2016 the feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span></span> <span data-ttu-id="2ffdd-124">Questa funzionalità sarà implementata e abilitata anche nelle directory create prima di tale data.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-124">This feature will also be rolled out and enabled on directories created before this date.</span></span> <span data-ttu-id="2ffdd-125">Si riceverà una notifica tramite posta elettronica quando sta per essere abilitata questa funzionalità nella directory dell'utente.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-125">You will receive an email notification when your directory is about to get this feature enabled.</span></span>
> 
> 

<span data-ttu-id="2ffdd-126">Le impostazioni seguenti vengono configurate da Azure AD Connect e non possono essere modificate da `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="2ffdd-126">The following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="2ffdd-127">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="2ffdd-127">DirSyncFeature</span></span> | <span data-ttu-id="2ffdd-128">Commento</span><span class="sxs-lookup"><span data-stu-id="2ffdd-128">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="2ffdd-129">DeviceWriteback</span><span class="sxs-lookup"><span data-stu-id="2ffdd-129">DeviceWriteback</span></span> |[<span data-ttu-id="2ffdd-130">Azure AD Connect: abilitazione del writeback dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="2ffdd-130">Azure AD Connect: Enabling device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |
| <span data-ttu-id="2ffdd-131">DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="2ffdd-131">DirectoryExtensions</span></span> |[<span data-ttu-id="2ffdd-132">Servizio di sincronizzazione Azure AD Connect: estensioni della directory</span><span class="sxs-lookup"><span data-stu-id="2ffdd-132">Azure AD Connect sync: Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [<span data-ttu-id="2ffdd-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span><span class="sxs-lookup"><span data-stu-id="2ffdd-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span></span>](#duplicate-attribute-resiliency) |<span data-ttu-id="2ffdd-134">Consente di mettere in quarantena un attributo quando è un duplicato di un altro oggetto, invece di causare l'errore dell'intero oggetto durante l'esportazione.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-134">Allows an attribute to be quarantined when it is a duplicate of another object rather than failing the entire object during export.</span></span> |
| <span data-ttu-id="2ffdd-135">PasswordSync</span><span class="sxs-lookup"><span data-stu-id="2ffdd-135">PasswordSync</span></span> |[<span data-ttu-id="2ffdd-136">Implementazione della sincronizzazione password con il servizio di sincronizzazione Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="2ffdd-136">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md) |
| <span data-ttu-id="2ffdd-137">UnifiedGroupWriteback</span><span class="sxs-lookup"><span data-stu-id="2ffdd-137">UnifiedGroupWriteback</span></span> |[<span data-ttu-id="2ffdd-138">Anteprima: Writeback dei gruppi</span><span class="sxs-lookup"><span data-stu-id="2ffdd-138">Preview: Group writeback</span></span>](active-directory-aadconnect-feature-preview.md#group-writeback) |
| <span data-ttu-id="2ffdd-139">UserWriteback</span><span class="sxs-lookup"><span data-stu-id="2ffdd-139">UserWriteback</span></span> |<span data-ttu-id="2ffdd-140">Attualmente non è supportata.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-140">Not currently supported.</span></span> |

## <a name="duplicate-attribute-resiliency"></a><span data-ttu-id="2ffdd-141">Duplicate attribute resiliency</span><span class="sxs-lookup"><span data-stu-id="2ffdd-141">Duplicate attribute resiliency</span></span>
<span data-ttu-id="2ffdd-142">Invece di causare un errore di provisioning degli oggetti con UPN o proxyAddress duplicati, l'attributo duplicato viene "messo in quarantena" e viene assegnato un valore temporaneo.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-142">Instead of failing to provision objects with duplicate UPNs / proxyAddresses, the duplicated attribute is “quarantined” and a temporary value is assigned.</span></span> <span data-ttu-id="2ffdd-143">Una volta risolto il conflitto, l'UPN temporaneo viene modificato automaticamente con il valore appropriato.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-143">When the conflict is resolved, the temporary UPN is changed to the proper value automatically.</span></span> <span data-ttu-id="2ffdd-144">Per altre informazioni, vedere [Sincronizzazione delle identità e resilienza degli attributi duplicati](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="2ffdd-144">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="userprincipalname-soft-match"></a><span data-ttu-id="2ffdd-145">Corrispondenza flessibile di userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="2ffdd-145">UserPrincipalName soft match</span></span>
<span data-ttu-id="2ffdd-146">Quando questa funzionalità è abilitata, la corrispondenza flessibile viene abilitata per l'UPN, oltre all' [indirizzo SMTP primario](https://support.microsoft.com/kb/2641663)che è sempre abilitato.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-146">When this feature is enabled, soft-match is enabled for UPN in addition to the [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span></span> <span data-ttu-id="2ffdd-147">La corrispondenza flessibile viene usata per associare gli utenti del cloud esistente in Azure AD con gli utenti locali.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-147">Soft-match is used to match existing cloud users in Azure AD with on-premises users.</span></span>

<span data-ttu-id="2ffdd-148">Questa funzionalità è utile se gli account AD account locali devono corrispondere agli account esistenti creati nel cloud e non si usa Exchange Online.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-148">If you need to match on-premises AD accounts with existing accounts created in the cloud and you are not using Exchange Online, then this feature is useful.</span></span> <span data-ttu-id="2ffdd-149">In questo scenario non esiste in genere un motivo per impostare l'attributo SMTP nel cloud.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-149">In this scenario, you generally don’t have a reason to set the SMTP attribute in the cloud.</span></span>

<span data-ttu-id="2ffdd-150">Questa funzionalità è attivata per impostazione predefinita per le nuove directory di Azure AD .</span><span class="sxs-lookup"><span data-stu-id="2ffdd-150">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="2ffdd-151">Per vedere se la funzionalità è abilitata per l'utente corrente, eseguire:</span><span class="sxs-lookup"><span data-stu-id="2ffdd-151">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

<span data-ttu-id="2ffdd-152">Se questa funzionalità non è abilitata per la directory di Azure AD in uso, è possibile abilitarla eseguendo:</span><span class="sxs-lookup"><span data-stu-id="2ffdd-152">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a><span data-ttu-id="2ffdd-153">Sincronizzare gli aggiornamenti di userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="2ffdd-153">Synchronize userPrincipalName updates</span></span>
<span data-ttu-id="2ffdd-154">In genere, gli aggiornamenti dell'attributo UserPrincipalName usando il servizio di sincronizzazione locale vengono bloccati, a meno che siano rispettate entrambe le condizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2ffdd-154">Historically, updates to the UserPrincipalName attribute using the sync service from on-premises has been blocked, unless both of these conditions are true:</span></span>

* <span data-ttu-id="2ffdd-155">L'utente è gestito (non federato).</span><span class="sxs-lookup"><span data-stu-id="2ffdd-155">The user is managed (non-federated).</span></span>
* <span data-ttu-id="2ffdd-156">All'utente non è stata assegnata una licenza.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-156">The user has not been assigned a license.</span></span>

<span data-ttu-id="2ffdd-157">Per alte informazioni, vedere [I nomi utente in Office 365, Azure o Intune non corrispondono agli ID di accesso o alternativi dell'UPN locale](https://support.microsoft.com/kb/2523192).</span><span class="sxs-lookup"><span data-stu-id="2ffdd-157">For more details, see [User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span></span>

<span data-ttu-id="2ffdd-158">L'abilitazione di questa funzionalità consente al motore di sincronizzazione di aggiornare l'attributo userPrincipalName quando viene modificato a livello locale e si usa la sincronizzazione password.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-158">Enabling this feature allows the sync engine to update the userPrincipalName when it is changed on-premises and you use password sync.</span></span> <span data-ttu-id="2ffdd-159">Se si usa la federazione, questa funzionalità non è supportata.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-159">If you use federation, this feature is not supported.</span></span>

<span data-ttu-id="2ffdd-160">Questa funzionalità è attivata per impostazione predefinita per le nuove directory di Azure AD .</span><span class="sxs-lookup"><span data-stu-id="2ffdd-160">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="2ffdd-161">Per vedere se la funzionalità è abilitata per l'utente corrente, eseguire:</span><span class="sxs-lookup"><span data-stu-id="2ffdd-161">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

<span data-ttu-id="2ffdd-162">Se questa funzionalità non è abilitata per la directory di Azure AD in uso, è possibile abilitarla eseguendo:</span><span class="sxs-lookup"><span data-stu-id="2ffdd-162">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

<span data-ttu-id="2ffdd-163">Dopo aver abilitato questa funzionalità, i valori di userPrincipalName esistenti rimarranno invariati.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-163">After enabling this feature, existing userPrincipalName values will remain as-is.</span></span> <span data-ttu-id="2ffdd-164">Alla successiva modifica dell'attributo userPrincipalName locale, la normale sincronizzazione differenziale degli utenti aggiornerà l'UPN.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-164">On next change of the userPrincipalName attribute on-premises, the normal delta sync on users will update the UPN.</span></span>  

## <a name="see-also"></a><span data-ttu-id="2ffdd-165">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2ffdd-165">See also</span></span>
* [<span data-ttu-id="2ffdd-166">Servizio di sincronizzazione Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="2ffdd-166">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="2ffdd-167">[Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="2ffdd-167">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

