---
title: una raccolta di Azure RemoteApp di tooyour utente aaaAdd | Documenti Microsoft
description: Informazioni su come tooadd utenti tooyour raccolta di Azure RemoteApp
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
ms.openlocfilehash: 0ae88e04c8bfc2ed55dc963945ed7e9ff687b603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-user-tooyour-azure-remoteapp-collection"></a><span data-ttu-id="8ecf7-103">Come tooadd tooyour un utente raccolta di Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="8ecf7-103">How tooadd a user tooyour Azure RemoteApp collection</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8ecf7-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="8ecf7-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8ecf7-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="8ecf7-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="8ecf7-106">Prima gli utenti possono visualizzare e usare le App in Azure RemoteApp, è necessario toogrant raccolta tooyour loro l'accesso.</span><span class="sxs-lookup"><span data-stu-id="8ecf7-106">Before your users can see and use your apps in Azure RemoteApp, you have toogrant them access tooyour collection.</span></span> <span data-ttu-id="8ecf7-107">Questo aspetto è parte di facile hello: su hello **accesso utente** scheda, immettere le informazioni sull'account hello per utente hello e quindi fare clic su hello segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="8ecf7-107">This is hello easy part: On hello **User Access** tab, enter hello account information for hello user, and then click hello check mark.</span></span>

<span data-ttu-id="8ecf7-108">Quali informazioni sull'account sono necessarie?</span><span class="sxs-lookup"><span data-stu-id="8ecf7-108">What account information do you need?</span></span> <span data-ttu-id="8ecf7-109">Che dipende dal tipo di hello di raccolta creato (cloud o ibrida) e se si utilizza Office 365 ProPlus in tale raccolta.</span><span class="sxs-lookup"><span data-stu-id="8ecf7-109">That depends on hello type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.</span></span>

## <a name="supported-user-identities"></a><span data-ttu-id="8ecf7-110">Identità degli utenti supportate</span><span class="sxs-lookup"><span data-stu-id="8ecf7-110">Supported user identities</span></span>
<span data-ttu-id="8ecf7-111">tipi di raccolta diverso Hello (cloud e ibrido) supportano l'utilizzo di identità utente diverse per tooapplications di accesso.</span><span class="sxs-lookup"><span data-stu-id="8ecf7-111">hello different collection types (cloud vs. hybrid) support using different user identities for access tooapplications.</span></span>  

<span data-ttu-id="8ecf7-112">Per una raccolta ibrida di RemoteApp, è necessario tooset di un'infrastruttura di dominio Active Directory locale e un tenant di Azure Active Directory con l'integrazione di Directory (e facoltativamente accesso single sign-on).</span><span class="sxs-lookup"><span data-stu-id="8ecf7-112">For a hybrid collection of RemoteApp, you need tooset up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on).</span></span> <span data-ttu-id="8ecf7-113">Inoltre, è necessario toocreate alcuni oggetti di Active Directory nella directory locale hello.</span><span class="sxs-lookup"><span data-stu-id="8ecf7-113">Additionally, you need toocreate some Active Directory objects in hello on-premises directory.</span></span>  

<span data-ttu-id="8ecf7-114">Per una raccolta di cloud di RemoteApp, è possibile concedere a qualsiasi utente con Azure Active Directory supporta le identità utente accesso tooRemoteApp tooinclude Accounts di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8ecf7-114">For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access tooRemoteApp tooinclude Microsoft Accounts.</span></span>  <span data-ttu-id="8ecf7-115">Vedere la tabella hello seguente.</span><span class="sxs-lookup"><span data-stu-id="8ecf7-115">See hello table below.</span></span>

<span data-ttu-id="8ecf7-116">Gli utenti di Office 365 sono utenti di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8ecf7-116">Office 365 users are Azure Active Directory users.</span></span> <span data-ttu-id="8ecf7-117">Agli utenti che dispongono di account ibridi con sincronizzazione della directory di Azure Active Directory è possibile concedere l'accesso utente in una distribuzione ibrida di RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8ecf7-117">If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.</span></span>   

<span data-ttu-id="8ecf7-118">È possibile utilizzare questa tabella come riferimento rapido per cui identità è supportato nella raccolta di e quali sono i requisiti di Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="8ecf7-118">You can use this table as a quick reference for which identity is supported in your collection and what hello Active Directory requirements are.</span></span>

| <span data-ttu-id="8ecf7-119">Account utente</span><span class="sxs-lookup"><span data-stu-id="8ecf7-119">User accounts</span></span> | <span data-ttu-id="8ecf7-120">Cloud</span><span class="sxs-lookup"><span data-stu-id="8ecf7-120">Cloud</span></span> | <span data-ttu-id="8ecf7-121">Ibrido</span><span class="sxs-lookup"><span data-stu-id="8ecf7-121">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8ecf7-122">Account Microsoft</span><span class="sxs-lookup"><span data-stu-id="8ecf7-122">Microsoft Account</span></span> |<span data-ttu-id="8ecf7-123">Sì</span><span class="sxs-lookup"><span data-stu-id="8ecf7-123">Yes</span></span> |<span data-ttu-id="8ecf7-124">No</span><span class="sxs-lookup"><span data-stu-id="8ecf7-124">No</span></span> |
| <span data-ttu-id="8ecf7-125">Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="8ecf7-125">Azure Active Directory (Azure AD)</span></span> | | |
| <span data-ttu-id="8ecf7-126">Solo cloud Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ecf7-126">Azure AD cloud only</span></span> |<span data-ttu-id="8ecf7-127">Sì</span><span class="sxs-lookup"><span data-stu-id="8ecf7-127">Yes</span></span> |<span data-ttu-id="8ecf7-128">No</span><span class="sxs-lookup"><span data-stu-id="8ecf7-128">No</span></span> |
| <span data-ttu-id="8ecf7-129">Sincronizzazione Active Directory con sincronizzazione password</span><span class="sxs-lookup"><span data-stu-id="8ecf7-129">ADsync with password sync</span></span> |<span data-ttu-id="8ecf7-130">Sì</span><span class="sxs-lookup"><span data-stu-id="8ecf7-130">Yes</span></span> |<span data-ttu-id="8ecf7-131">Sì</span><span class="sxs-lookup"><span data-stu-id="8ecf7-131">Yes</span></span> |
| <span data-ttu-id="8ecf7-132">Sincronizzazione Active Directory senza sincronizzazione password</span><span class="sxs-lookup"><span data-stu-id="8ecf7-132">ADsync without password sync</span></span> |<span data-ttu-id="8ecf7-133">Sì</span><span class="sxs-lookup"><span data-stu-id="8ecf7-133">Yes</span></span> |<span data-ttu-id="8ecf7-134">No</span><span class="sxs-lookup"><span data-stu-id="8ecf7-134">No</span></span> |
| <span data-ttu-id="8ecf7-135">Sincronizzazione Active Directory con ADFS</span><span class="sxs-lookup"><span data-stu-id="8ecf7-135">ADsync with AD FS</span></span> |<span data-ttu-id="8ecf7-136">Sì</span><span class="sxs-lookup"><span data-stu-id="8ecf7-136">Yes</span></span> |<span data-ttu-id="8ecf7-137">sì</span><span class="sxs-lookup"><span data-stu-id="8ecf7-137">Yes</span></span> |
| <span data-ttu-id="8ecf7-138">[Provider di identità di terze parti supportati da Azure](https://msdn.microsoft.com/library/azure/jj679342.aspx), ad esempio Ping</span><span class="sxs-lookup"><span data-stu-id="8ecf7-138">[3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping)</span></span> |<span data-ttu-id="8ecf7-139">sì</span><span class="sxs-lookup"><span data-stu-id="8ecf7-139">Yes</span></span> |<span data-ttu-id="8ecf7-140">Sì</span><span class="sxs-lookup"><span data-stu-id="8ecf7-140">Yes</span></span> |
| <span data-ttu-id="8ecf7-141">Autenticazione a più fattori</span><span class="sxs-lookup"><span data-stu-id="8ecf7-141">Multi-Factor Authentication</span></span> |<span data-ttu-id="8ecf7-142">Sì</span><span class="sxs-lookup"><span data-stu-id="8ecf7-142">Yes</span></span> |<span data-ttu-id="8ecf7-143">Sì</span><span class="sxs-lookup"><span data-stu-id="8ecf7-143">Yes</span></span> |

<span data-ttu-id="8ecf7-144">Per [altre informazioni](remoteapp-ad.md) , vedere Configurare Azure Active Directory per RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8ecf7-144">Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.</span></span>

> [!NOTE]
> <span data-ttu-id="8ecf7-145">gli utenti di Azure Active Directory Hello devono essere di tenant hello è associato alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8ecf7-145">hello Azure Active Directory users must be from hello tenant that's associated with your subscription.</span></span> <span data-ttu-id="8ecf7-146">(È possibile visualizzare e modificare la sottoscrizione hello **impostazioni** scheda nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="8ecf7-146">(You can view and modify your subscription on hello **Settings** tab in hello portal.</span></span> <span data-ttu-id="8ecf7-147">Vedere [tenant di Azure Active Directory hello modifica usata da RemoteApp](remoteapp-changetenant.md) per ulteriori informazioni.)</span><span class="sxs-lookup"><span data-stu-id="8ecf7-147">See [Change hello Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)</span></span>
> 
> 

## <a name="office-365-proplus-user-account-information"></a><span data-ttu-id="8ecf7-148">Informazioni sugli account utente di Office 365 ProPlus</span><span class="sxs-lookup"><span data-stu-id="8ecf7-148">Office 365 ProPlus user account information</span></span>
<span data-ttu-id="8ecf7-149">Se si utilizza Office 365 ProPlus immagine di modello hello nella raccolta di *o* se si crea un'immagine personalizzata che usa Office 365, è consentito solo agli utenti di Azure Active Directory tooadd che dispone di sottoscrizioni di Office 365 per hello dominio predefinito della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8ecf7-149">If you are using hello Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed tooadd Azure Active Directory users that have Office 365 subscriptions for hello default domain of your subscription.</span></span> <span data-ttu-id="8ecf7-150">Per altre informazioni, vedere l'articolo relativo all' [uso di Office 365 con Azure RemoteApp](remoteapp-o365.md) .</span><span class="sxs-lookup"><span data-stu-id="8ecf7-150">See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.</span></span>

