---
title: 'Servizi di dominio di Azure Active Directory: Abilitare il supporto per il servizio profilo utente di SharePoint | Documentazione Microsoft'
description: Configurare la sincronizzazione dei profili toosupport domini gestiti Azure Active Directory Domain Services per SharePoint Server
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9de4f810380309e8f6436fc24412701645978f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-managed-domain-toosupport-profile-synchronization-for-sharepoint-server"></a><span data-ttu-id="ae84a-103">Configurare la sincronizzazione di profilo toosupport un dominio gestito di SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="ae84a-103">Configure a managed domain toosupport profile synchronization for SharePoint Server</span></span>
<span data-ttu-id="ae84a-104">SharePoint Server include un servizio profili utente utilizzato per la sincronizzazione dei profili utente.</span><span class="sxs-lookup"><span data-stu-id="ae84a-104">SharePoint Server includes a User Profile Service that is used for user profile synchronization.</span></span> <span data-ttu-id="ae84a-105">tooset backup hello servizio profili utente, le autorizzazioni appropriate necessario toobe concesse per un dominio Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ae84a-105">tooset up hello User Profile Service, appropriate permissions need toobe granted on an Active Directory domain.</span></span> <span data-ttu-id="ae84a-106">Per ulteriori informazioni, vedere [Concedere a Servizi di dominio di Active Directory le autorizzazioni per la sincronizzazione dei profili in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span><span class="sxs-lookup"><span data-stu-id="ae84a-106">For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span></span>

<span data-ttu-id="ae84a-107">In questo articolo viene illustrato come è possibile configurare i servizio di sincronizzazione dei profili utente di SharePoint Server di servizi di dominio Active Directory di Azure domini gestiti toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="ae84a-107">This article explains how you can configure Azure AD Domain Services managed domains toodeploy hello SharePoint Server User Profile Sync service.</span></span>

## <a name="hello-aad-dc-service-accounts-group"></a><span data-ttu-id="ae84a-108">gruppo 'Account di servizio controller di dominio di AAD' Hello</span><span class="sxs-lookup"><span data-stu-id="ae84a-108">hello 'AAD DC Service Accounts' group</span></span>
<span data-ttu-id="ae84a-109">Un gruppo di sicurezza denominato '**gli account del servizio controller di dominio AAD**' è disponibile all'interno di hello 'Utenti' unità organizzativa nel dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="ae84a-109">A security group called '**AAD DC Service Accounts**' is available within hello 'Users' organizational unit on your managed domain.</span></span> <span data-ttu-id="ae84a-110">È possibile visualizzare questo gruppo di hello **Active Directory Users and Computers** snap-in MMC nel dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="ae84a-110">You can see this group in hello **Active Directory Users and Computers** MMC snap-in on your managed domain.</span></span>

![Il gruppo di sicurezza AAD DC Service Accounts](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

<span data-ttu-id="ae84a-112">I membri di questo gruppo di sicurezza sono delegata hello seguenti privilegi:</span><span class="sxs-lookup"><span data-stu-id="ae84a-112">Members of this security group are delegated hello following privileges:</span></span>
- <span data-ttu-id="ae84a-113">il privilegio 'Replica delle modifiche di Directory' Hello nella directory principale di hello DSE di hello gestiti dominio.</span><span class="sxs-lookup"><span data-stu-id="ae84a-113">hello 'Replicate Directory Changes' privilege on hello root DSE of hello managed domain.</span></span>
- <span data-ttu-id="ae84a-114">il privilegio 'Replica delle modifiche di Directory' nel contesto dei nomi di configurazione hello Hello (cn = contenitore della configurazione) di hello gestito dominio.</span><span class="sxs-lookup"><span data-stu-id="ae84a-114">hello 'Replicate Directory Changes' privilege on hello Configuration naming context (cn=configuration container) of hello managed domain.</span></span>

<span data-ttu-id="ae84a-115">Questo gruppo di sicurezza è anche un membro del gruppo incorporato hello **l'accesso compatibile precedente a Windows 2000**.</span><span class="sxs-lookup"><span data-stu-id="ae84a-115">This security group is also a member of hello built-in group **Pre-Windows 2000 Compatible Access**.</span></span>

![Il gruppo di sicurezza AAD DC Service Accounts](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-toosupport-sharepoint-server-user-profile-sync"></a><span data-ttu-id="ae84a-117">Abilitare la sincronizzazione dei profili utente di SharePoint Server di toosupport dominio gestito</span><span class="sxs-lookup"><span data-stu-id="ae84a-117">Enable your managed domain toosupport SharePoint Server user profile sync</span></span>
<span data-ttu-id="ae84a-118">È possibile aggiungere l'account di servizio hello usato per toohello sincronizzazione profilo utente di SharePoint **gli account del servizio controller di dominio AAD** gruppo.</span><span class="sxs-lookup"><span data-stu-id="ae84a-118">You can add hello service account used for SharePoint user profile synchronization toohello **AAD DC Service Accounts** group.</span></span> <span data-ttu-id="ae84a-119">Di conseguenza, l'account di sincronizzazione hello Ottiene directory toohello modifiche tooreplicate di privilegi adeguati.</span><span class="sxs-lookup"><span data-stu-id="ae84a-119">As a result, hello synchronization account gets adequate privileges tooreplicate changes toohello directory.</span></span> <span data-ttu-id="ae84a-120">Questo passaggio di configurazione consente correttamente toowork sincronizzazione profilo utente di SharePoint Server.</span><span class="sxs-lookup"><span data-stu-id="ae84a-120">This configuration step enables SharePoint Server user profile sync toowork correctly.</span></span>

![AAD DC Service Accounts - aggiunta di membri](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![AAD DC Service Accounts - aggiunta di membri](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a><span data-ttu-id="ae84a-123">Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="ae84a-123">Related Content</span></span>
* [<span data-ttu-id="ae84a-124">Riferimento tecnico - Concedere a Servizi di dominio di Active Directory le autorizzazioni per la sincronizzazione dei profili in SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="ae84a-124">Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013</span></span>](https://technet.microsoft.com/library/hh296982.aspx)
