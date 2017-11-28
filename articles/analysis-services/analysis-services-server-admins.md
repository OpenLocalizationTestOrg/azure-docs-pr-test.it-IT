---
title: amministratori di server aaaManage in Azure Analysis Services | Documenti Microsoft
description: Informazioni su come amministratori di server toomanage per un server Analysis Services in Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: e04387e48e9b9483c382ee5cc9fd65f8331fb2a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-server-administrators"></a><span data-ttu-id="55a12-103">Gestire gli amministratori del server</span><span class="sxs-lookup"><span data-stu-id="55a12-103">Manage server administrators</span></span>
<span data-ttu-id="55a12-104">Gli amministratori del server devono essere un utente valido o un gruppo in hello Azure Active Directory (Azure AD) per tenant hello in cui hello risiede server.</span><span class="sxs-lookup"><span data-stu-id="55a12-104">Server administrators must be a valid user or group in hello Azure Active Directory (Azure AD) for hello tenant in which hello server resides.</span></span> <span data-ttu-id="55a12-105">È possibile utilizzare **gli amministratori di Analysis Services** nel Pannello di controllo hello per il server nel portale di Azure, o proprietà del Server negli amministratori del server di SQL Server Management Studio toomanage.</span><span class="sxs-lookup"><span data-stu-id="55a12-105">You can use **Analysis Services Admins** in hello control blade for your server in Azure portal, or Server Properties in SSMS toomanage server administrators.</span></span> 

## <a name="tooadd-server-administrators-by-using-azure-portal"></a><span data-ttu-id="55a12-106">amministratori del server tooadd tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="55a12-106">tooadd server administrators by using Azure portal</span></span>
1. <span data-ttu-id="55a12-107">Nel Pannello di controllo hello del server, fare clic su **gli amministratori di Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="55a12-107">In hello control blade for your server, click **Analysis Services Admins**.</span></span>
2. <span data-ttu-id="55a12-108">In hello  **\<nomeserver >-gli amministratori di Analysis Services** pannello, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="55a12-108">In hello **\<servername> - Analysis Services Admins** blade, click **Add**.</span></span>
3. <span data-ttu-id="55a12-109">In hello **aggiungere gli amministratori del Server** pannello selezionare gli account utente di Azure AD o invitare gli utenti esterni dall'indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="55a12-109">In hello **Add Server Administrators** blade, select user accounts from your Azure AD or invite external users by email address.</span></span>

    ![Amministratori del server nel portale di Azure](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="tooadd-server-administrators-by-using-ssms"></a><span data-ttu-id="55a12-111">amministratori del server tooadd utilizzando SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="55a12-111">tooadd server administrators by using SSMS</span></span>
1. <span data-ttu-id="55a12-112">Server hello rapida > **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="55a12-112">Right-click hello server > **Properties**.</span></span>
2. <span data-ttu-id="55a12-113">In **Proprietà computer Analysis Server** fare clic su **Sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="55a12-113">In **Analysis Server Properties**, click **Security**.</span></span>
3. <span data-ttu-id="55a12-114">Fare clic su **Aggiungi**e quindi immettere l'indirizzo di posta elettronica hello per un utente o gruppo in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55a12-114">Click **Add**, and then enter hello email address for a user or group in your Azure AD.</span></span>
   
    ![Aggiungere gli amministratori del server in SSMS](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a><span data-ttu-id="55a12-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="55a12-116">Next steps</span></span> 
[<span data-ttu-id="55a12-117">Autenticazione e autorizzazioni utente</span><span class="sxs-lookup"><span data-stu-id="55a12-117">Authentication and user permissions</span></span>](analysis-services-manage-users.md)  
[<span data-ttu-id="55a12-118">Gestire ruoli e utenti del database</span><span class="sxs-lookup"><span data-stu-id="55a12-118">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="55a12-119">Controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="55a12-119">Role-Based Access Control</span></span>](../active-directory/role-based-access-control-what-is.md)  

