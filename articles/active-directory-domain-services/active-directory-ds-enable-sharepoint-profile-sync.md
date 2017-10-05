---
title: 'Servizi di dominio di Azure Active Directory: Abilitare il supporto per il servizio profilo utente di SharePoint | Documentazione Microsoft'
description: Configurare i domini gestiti dei servizi di dominio di Azure Active Directory per supportare la sincronizzazione dei profili per SharePoint Server
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
ms.openlocfilehash: c3c923b5c9cd652f0c5b0ec98c1cda740f180122
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-managed-domain-to-support-profile-synchronization-for-sharepoint-server"></a><span data-ttu-id="06cb1-103">Configurare un dominio gestito per supportare la sincronizzazione dei profili per SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="06cb1-103">Configure a managed domain to support profile synchronization for SharePoint Server</span></span>
<span data-ttu-id="06cb1-104">SharePoint Server include un servizio profili utente utilizzato per la sincronizzazione dei profili utente.</span><span class="sxs-lookup"><span data-stu-id="06cb1-104">SharePoint Server includes a User Profile Service that is used for user profile synchronization.</span></span> <span data-ttu-id="06cb1-105">Per impostare il servizio profili utente, è necessario concedere le autorizzazioni appropriate in un dominio di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="06cb1-105">To set up the User Profile Service, appropriate permissions need to be granted on an Active Directory domain.</span></span> <span data-ttu-id="06cb1-106">Per ulteriori informazioni, vedere [Concedere a Servizi di dominio di Active Directory le autorizzazioni per la sincronizzazione dei profili in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span><span class="sxs-lookup"><span data-stu-id="06cb1-106">For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span></span>

<span data-ttu-id="06cb1-107">In questo articolo viene illustrato come è possibile configurare domini gestiti di servizi di dominio Azure AD per distribuire il servizio di sincronizzazione dei profili utente di SharePoint Server.</span><span class="sxs-lookup"><span data-stu-id="06cb1-107">This article explains how you can configure Azure AD Domain Services managed domains to deploy the SharePoint Server User Profile Sync service.</span></span>

## <a name="the-aad-dc-service-accounts-group"></a><span data-ttu-id="06cb1-108">Il gruppo 'AAD DC Service Accounts'</span><span class="sxs-lookup"><span data-stu-id="06cb1-108">The 'AAD DC Service Accounts' group</span></span>
<span data-ttu-id="06cb1-109">Un gruppo di sicurezza denominato '**AAD DC Service Accounts**' è disponibile all'interno dell'unità organizzativa 'Utenti' nel dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="06cb1-109">A security group called '**AAD DC Service Accounts**' is available within the 'Users' organizational unit on your managed domain.</span></span> <span data-ttu-id="06cb1-110">È possibile visualizzare questo gruppo nello snap-in MMC **Utenti e computer di Active Directory** nel dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="06cb1-110">You can see this group in the **Active Directory Users and Computers** MMC snap-in on your managed domain.</span></span>

![Il gruppo di sicurezza AAD DC Service Accounts](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

<span data-ttu-id="06cb1-112">Ai membri di questo gruppo di sicurezza vengono delegati i privilegi seguenti:</span><span class="sxs-lookup"><span data-stu-id="06cb1-112">Members of this security group are delegated the following privileges:</span></span>
- <span data-ttu-id="06cb1-113">Il privilegio 'Replica modifiche directory' nella directory principale DSE del dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="06cb1-113">The 'Replicate Directory Changes' privilege on the root DSE of the managed domain.</span></span>
- <span data-ttu-id="06cb1-114">Il privilegio 'Replica modifiche Directory' nel contesto di denominazione della configurazione (cn = contenitore di configurazione) del dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="06cb1-114">The 'Replicate Directory Changes' privilege on the Configuration naming context (cn=configuration container) of the managed domain.</span></span>

<span data-ttu-id="06cb1-115">Questo gruppo di sicurezza è anche membro del gruppo predefinito **Accesso compatibile precedente a Windows 2000**.</span><span class="sxs-lookup"><span data-stu-id="06cb1-115">This security group is also a member of the built-in group **Pre-Windows 2000 Compatible Access**.</span></span>

![Il gruppo di sicurezza AAD DC Service Accounts](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-to-support-sharepoint-server-user-profile-sync"></a><span data-ttu-id="06cb1-117">Abilitare il dominio gestito per supportare la sincronizzazione di profili utente di SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="06cb1-117">Enable your managed domain to support SharePoint Server user profile sync</span></span>
<span data-ttu-id="06cb1-118">È possibile aggiungere l'account di servizio utilizzato per la sincronizzazione dei profili utente di SharePoint per il gruppo **AAD DC Service Accounts**.</span><span class="sxs-lookup"><span data-stu-id="06cb1-118">You can add the service account used for SharePoint user profile synchronization to the **AAD DC Service Accounts** group.</span></span> <span data-ttu-id="06cb1-119">Di conseguenza, l'account di sincronizzazione ottiene i privilegi adeguati per replicare le modifiche alla directory.</span><span class="sxs-lookup"><span data-stu-id="06cb1-119">As a result, the synchronization account gets adequate privileges to replicate changes to the directory.</span></span> <span data-ttu-id="06cb1-120">Questo passaggio di configurazione consente il corretto funzionamento della sincronizzazione dei profili utente di SharePoint Server.</span><span class="sxs-lookup"><span data-stu-id="06cb1-120">This configuration step enables SharePoint Server user profile sync to work correctly.</span></span>

![AAD DC Service Accounts - aggiunta di membri](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![AAD DC Service Accounts - aggiunta di membri](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a><span data-ttu-id="06cb1-123">Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="06cb1-123">Related Content</span></span>
* [<span data-ttu-id="06cb1-124">Riferimento tecnico - Concedere a Servizi di dominio di Active Directory le autorizzazioni per la sincronizzazione dei profili in SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="06cb1-124">Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013</span></span>](https://technet.microsoft.com/library/hh296982.aspx)
