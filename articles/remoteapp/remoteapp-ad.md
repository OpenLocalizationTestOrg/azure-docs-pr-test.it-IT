---
title: Azure AD + requisiti di Active Directory per Azure RemoteApp | Documentazione Microsoft
description: Informazioni su come configurare Active Directory per lavorare con Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 78008a032faa93795cc02b720d68a0c6f5f16e9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a><span data-ttu-id="cc4ed-103">Azure AD + requisiti di Active Directory per Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="cc4ed-103">Azure AD + Active Directory requirements for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cc4ed-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="cc4ed-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="cc4ed-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="cc4ed-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="cc4ed-106">Per la raccolta ibrida di RemoteApp di Azure o per un insieme di cloud che si desidera attuare utilizzando una connessione di Active Directory, è necessario eseguire le operazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="cc4ed-106">For your Azure RemoteApp hybrid collection or for a cloud collection that you want to federate using AD Connect, you need to do the following.</span></span>

### <a name="connect-azure-ad-and-active-directory"></a><span data-ttu-id="cc4ed-107">Connettersi AD Azure e ad Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc4ed-107">Connect Azure AD and Active Directory</span></span>
<span data-ttu-id="cc4ed-108">Se si desidera connettere il tenant di Azure AD e gli ambienti di Active Directory in locale, utilizzare la connessione di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cc4ed-108">If you want to connect your Azure AD tenant and your on-premises Active Directory environments, use AD Connect.</span></span> <span data-ttu-id="cc4ed-109">Verranno visualizzati solo [4 clic](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) per connettere le due directory.</span><span class="sxs-lookup"><span data-stu-id="cc4ed-109">It will take you only [4 clicks](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) to connect the two directories.</span></span>

<span data-ttu-id="cc4ed-110">Nota - la sincronizzazione delle Directory è necessaria per le raccolte ibride.</span><span class="sxs-lookup"><span data-stu-id="cc4ed-110">Note - Directory synchronization is required for hybrid collections.</span></span>

### <a name="make-sure-your-domaincom-match"></a><span data-ttu-id="cc4ed-111">Controllare la corrispondenza del valore "@domain.com"</span><span class="sxs-lookup"><span data-stu-id="cc4ed-111">Make sure your "@domain.com" match</span></span>
<span data-ttu-id="cc4ed-112">Prima di iniziare, assicurarsi che il nome UPN per la foresta locale corrisponda al suffisso del dominio di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cc4ed-112">Before you get started, make sure that the UPN for your on-premises forest matches the suffix of your Azure AD domain.</span></span> 

<span data-ttu-id="cc4ed-113">Dopo avere impostato il suffisso del dominio UPN in Azure AD, tutti gli utenti che accedono ad Azure RemoteApp accederanno come "user@<the suffix you set up>".</span><span class="sxs-lookup"><span data-stu-id="cc4ed-113">After you set up the UPN domain suffix in Azure AD, all users logging into Azure RemoteApp will log in as "user@<the suffix you set up>."</span></span> <span data-ttu-id="cc4ed-114">Assicurarsi che gli utenti possano inoltre accedere con lo stesso user@suffix nel dominio locale.</span><span class="sxs-lookup"><span data-stu-id="cc4ed-114">Make sure that users can also log in with the same user@suffix into the on-premises domain.</span></span> <span data-ttu-id="cc4ed-115">In alcuni casi è possibile impostare un nome di dominio in Azure AD quando si specifica un suffisso di dominio diverso per l'utente locale.</span><span class="sxs-lookup"><span data-stu-id="cc4ed-115">In certain cases you can set up one domain name in Azure AD while specifying a different domain suffix for the user on-prem.</span></span> <span data-ttu-id="cc4ed-116">In questo caso, gli utenti non potranno connettersi a nessun computer appartenente a un dominio o a risorse tramite Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cc4ed-116">In this case, your users won't be able to connect to any domain-joined computers or resources through Azure RemoteApp.</span></span>

<span data-ttu-id="cc4ed-117">Ad esempio, se si imposta il suffisso di dominio UPN in AAD come contoso.com, ma alcuni utenti in locale o in Active Directory sono configurati per l'accesso con @contoso.uk, tali utenti non potranno accedere correttamente alla raccolta ARA.</span><span class="sxs-lookup"><span data-stu-id="cc4ed-117">For example, if you set up your UPN domain suffix in AAD as contoso.com, but some users on premises/AD are configured to log in with @contoso.uk, then those users will not be able to correctly log into the ARA collection.</span></span> <span data-ttu-id="cc4ed-118">Gli utenti UPN in AAD e in Active Directory devono essere gli stessi affinché l'accesso sia possibile"</span><span class="sxs-lookup"><span data-stu-id="cc4ed-118">Users UPN in AAD and AD must be the same for the login to be possible”</span></span>

### <a name="create-objects-for-azure-remoteapp"></a><span data-ttu-id="cc4ed-119">Creare gli oggetti per RemoteApp di Azure</span><span class="sxs-lookup"><span data-stu-id="cc4ed-119">Create objects for Azure RemoteApp</span></span>
<span data-ttu-id="cc4ed-120">Inoltre, è necessario creare i seguenti oggetti di Active Directory locali:</span><span class="sxs-lookup"><span data-stu-id="cc4ed-120">You also need to create the following on-premises Active Directory objects:</span></span>

* <span data-ttu-id="cc4ed-121">Un account del servizio per fornire l'accesso alle risorse di dominio ai programmi RemoteApp unendo gli endpoint di Host sessione Desktop remoto al dominio locale.</span><span class="sxs-lookup"><span data-stu-id="cc4ed-121">A service account to provide access to domain resources for RemoteApp programs by joining RDSH end points to the on-premises domain.</span></span>
* <span data-ttu-id="cc4ed-122">Un'unità organizzativa per contenere oggetti computer di RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cc4ed-122">An Organizational Unit (OU) to contain RemoteApp machine objects.</span></span> <span data-ttu-id="cc4ed-123">L'uso dell'unità organizzativa è consigliabile (ma non obbligatorio) per isolare gli account e i criteri che si useranno con RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cc4ed-123">Use of the OU is recommended (but not required) to isolate the accounts and policies you will use with RemoteApp.</span></span>

<span data-ttu-id="cc4ed-124">Entrambi questi oggetti sono necessari quando si crea la raccolta di RemoteApp, sarà dunque necessario innanzitutto eseguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="cc4ed-124">You need both of these objects when you create your RemoteApp collection, so be sure to do these steps first.</span></span>

