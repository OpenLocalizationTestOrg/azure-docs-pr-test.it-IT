---
title: Aggiungere un utente alla raccolta di Azure RemoteApp | Microsoft Docs
description: Informazioni su come aggiungere utenti alla raccolta di Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 281e74c7941c42d8a3e4351953391229e54ce0a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-a-user-to-your-azure-remoteapp-collection"></a><span data-ttu-id="4b7b4-103">Come aggiungere un utente alla raccolta di Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="4b7b4-103">How to add a user to your Azure RemoteApp collection</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4b7b4-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="4b7b4-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="4b7b4-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="4b7b4-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="4b7b4-106">Prima che gli utenti possano visualizzare e usare le app in Azure RemoteApp, è necessario concedere loro l'accesso alla raccolta.</span><span class="sxs-lookup"><span data-stu-id="4b7b4-106">Before your users can see and use your apps in Azure RemoteApp, you have to grant them access to your collection.</span></span> <span data-ttu-id="4b7b4-107">Questo è estremamente semplice: nella scheda **Accesso utente** immettere le informazioni relative all'account dell'utente e quindi fare clic sul segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="4b7b4-107">This is the easy part: On the **User Access** tab, enter the account information for the user, and then click the check mark.</span></span>

<span data-ttu-id="4b7b4-108">Quali informazioni sull'account sono necessarie?</span><span class="sxs-lookup"><span data-stu-id="4b7b4-108">What account information do you need?</span></span> <span data-ttu-id="4b7b4-109">Dipende dal tipo di raccolta creata (cloud o ibrida) e dall'uso o meno di Office 365 ProPlus in tale raccolta.</span><span class="sxs-lookup"><span data-stu-id="4b7b4-109">That depends on the type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.</span></span>

## <a name="supported-user-identities"></a><span data-ttu-id="4b7b4-110">Identità degli utenti supportate</span><span class="sxs-lookup"><span data-stu-id="4b7b4-110">Supported user identities</span></span>
<span data-ttu-id="4b7b4-111">I diversi tipi di raccolta (cloud e ibridi) supportano l'uso di diverse identità utente per l'accesso alle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="4b7b4-111">The different collection types (cloud vs. hybrid) support using different user identities for access to applications.</span></span>  

<span data-ttu-id="4b7b4-112">Per una raccolta ibrida di RemoteApp, è necessario configurare un'infrastruttura di dominio Active Directory locale e un tenant di Azure Active Directory con l'integrazione della directory (e, facoltativamente, Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="4b7b4-112">For a hybrid collection of RemoteApp, you need to set up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on).</span></span> <span data-ttu-id="4b7b4-113">Inoltre, è necessario creare alcuni oggetti Active Directory nella directory locale.</span><span class="sxs-lookup"><span data-stu-id="4b7b4-113">Additionally, you need to create some Active Directory objects in the on-premises directory.</span></span>  

<span data-ttu-id="4b7b4-114">Per una raccolta nel cloud di RemoteApp, a tutti gli utenti che dispongono di identità di supporto per Azure Active Directory è possibile concedere l'accesso utente a RemoteApp in modo che comprenda gli account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4b7b4-114">For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access to RemoteApp to include Microsoft Accounts.</span></span>  <span data-ttu-id="4b7b4-115">Vedere la tabella riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="4b7b4-115">See the table below.</span></span>

<span data-ttu-id="4b7b4-116">Gli utenti di Office 365 sono utenti di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4b7b4-116">Office 365 users are Azure Active Directory users.</span></span> <span data-ttu-id="4b7b4-117">Agli utenti che dispongono di account ibridi con sincronizzazione della directory di Azure Active Directory è possibile concedere l'accesso utente in una distribuzione ibrida di RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="4b7b4-117">If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.</span></span>   

<span data-ttu-id="4b7b4-118">È possibile usare questa tabella come riferimento rapido per le identità supportate nella propria raccolta e per i requisiti di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4b7b4-118">You can use this table as a quick reference for which identity is supported in your collection and what the Active Directory requirements are.</span></span>

| <span data-ttu-id="4b7b4-119">Account utente</span><span class="sxs-lookup"><span data-stu-id="4b7b4-119">User accounts</span></span> | <span data-ttu-id="4b7b4-120">Cloud</span><span class="sxs-lookup"><span data-stu-id="4b7b4-120">Cloud</span></span> | <span data-ttu-id="4b7b4-121">Ibrido</span><span class="sxs-lookup"><span data-stu-id="4b7b4-121">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4b7b4-122">Account Microsoft</span><span class="sxs-lookup"><span data-stu-id="4b7b4-122">Microsoft Account</span></span> |<span data-ttu-id="4b7b4-123">Sì</span><span class="sxs-lookup"><span data-stu-id="4b7b4-123">Yes</span></span> |<span data-ttu-id="4b7b4-124">No</span><span class="sxs-lookup"><span data-stu-id="4b7b4-124">No</span></span> |
| <span data-ttu-id="4b7b4-125">Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="4b7b4-125">Azure Active Directory (Azure AD)</span></span> | | |
| <span data-ttu-id="4b7b4-126">Solo cloud Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b7b4-126">Azure AD cloud only</span></span> |<span data-ttu-id="4b7b4-127">Sì</span><span class="sxs-lookup"><span data-stu-id="4b7b4-127">Yes</span></span> |<span data-ttu-id="4b7b4-128">No</span><span class="sxs-lookup"><span data-stu-id="4b7b4-128">No</span></span> |
| <span data-ttu-id="4b7b4-129">Sincronizzazione Active Directory con sincronizzazione password</span><span class="sxs-lookup"><span data-stu-id="4b7b4-129">ADsync with password sync</span></span> |<span data-ttu-id="4b7b4-130">Sì</span><span class="sxs-lookup"><span data-stu-id="4b7b4-130">Yes</span></span> |<span data-ttu-id="4b7b4-131">Sì</span><span class="sxs-lookup"><span data-stu-id="4b7b4-131">Yes</span></span> |
| <span data-ttu-id="4b7b4-132">Sincronizzazione Active Directory senza sincronizzazione password</span><span class="sxs-lookup"><span data-stu-id="4b7b4-132">ADsync without password sync</span></span> |<span data-ttu-id="4b7b4-133">Sì</span><span class="sxs-lookup"><span data-stu-id="4b7b4-133">Yes</span></span> |<span data-ttu-id="4b7b4-134">No</span><span class="sxs-lookup"><span data-stu-id="4b7b4-134">No</span></span> |
| <span data-ttu-id="4b7b4-135">Sincronizzazione Active Directory con ADFS</span><span class="sxs-lookup"><span data-stu-id="4b7b4-135">ADsync with AD FS</span></span> |<span data-ttu-id="4b7b4-136">Sì</span><span class="sxs-lookup"><span data-stu-id="4b7b4-136">Yes</span></span> |<span data-ttu-id="4b7b4-137">sì</span><span class="sxs-lookup"><span data-stu-id="4b7b4-137">Yes</span></span> |
| <span data-ttu-id="4b7b4-138">[Provider di identità di terze parti supportati da Azure](https://msdn.microsoft.com/library/azure/jj679342.aspx), ad esempio Ping</span><span class="sxs-lookup"><span data-stu-id="4b7b4-138">[3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping)</span></span> |<span data-ttu-id="4b7b4-139">sì</span><span class="sxs-lookup"><span data-stu-id="4b7b4-139">Yes</span></span> |<span data-ttu-id="4b7b4-140">Sì</span><span class="sxs-lookup"><span data-stu-id="4b7b4-140">Yes</span></span> |
| <span data-ttu-id="4b7b4-141">Autenticazione a più fattori</span><span class="sxs-lookup"><span data-stu-id="4b7b4-141">Multi-Factor Authentication</span></span> |<span data-ttu-id="4b7b4-142">Sì</span><span class="sxs-lookup"><span data-stu-id="4b7b4-142">Yes</span></span> |<span data-ttu-id="4b7b4-143">Sì</span><span class="sxs-lookup"><span data-stu-id="4b7b4-143">Yes</span></span> |

<span data-ttu-id="4b7b4-144">Per [altre informazioni](remoteapp-ad.md) , vedere Configurare Azure Active Directory per RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="4b7b4-144">Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.</span></span>

> [!NOTE]
> <span data-ttu-id="4b7b4-145">Gli utenti di Azure Active Directory devono provenire dal tenant associato alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="4b7b4-145">The Azure Active Directory users must be from the tenant that's associated with your subscription.</span></span> <span data-ttu-id="4b7b4-146">(è possibile visualizzare e modificare la sottoscrizione nella scheda **Impostazioni** nel portale.</span><span class="sxs-lookup"><span data-stu-id="4b7b4-146">(You can view and modify your subscription on the **Settings** tab in the portal.</span></span> <span data-ttu-id="4b7b4-147">Per altre informazioni, vedere l'articolo relativo alla [modifica del tenant di Azure Active Directory usato da RemoteApp](remoteapp-changetenant.md) ).</span><span class="sxs-lookup"><span data-stu-id="4b7b4-147">See [Change the Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)</span></span>
> 
> 

## <a name="office-365-proplus-user-account-information"></a><span data-ttu-id="4b7b4-148">Informazioni sugli account utente di Office 365 ProPlus</span><span class="sxs-lookup"><span data-stu-id="4b7b4-148">Office 365 ProPlus user account information</span></span>
<span data-ttu-id="4b7b4-149">Se si usa l'immagine modello di Office 365 ProPlus nella raccolta *o* se è stata creata un'immagine personalizzata che usa Office 365, è possibile solo aggiungere gli utenti di Azure Active Directory che dispongono di sottoscrizioni a Office 365 per il dominio predefinito della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="4b7b4-149">If you are using the Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed to add Azure Active Directory users that have Office 365 subscriptions for the default domain of your subscription.</span></span> <span data-ttu-id="4b7b4-150">Per altre informazioni, vedere l'articolo relativo all' [uso di Office 365 con Azure RemoteApp](remoteapp-o365.md) .</span><span class="sxs-lookup"><span data-stu-id="4b7b4-150">See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.</span></span>

