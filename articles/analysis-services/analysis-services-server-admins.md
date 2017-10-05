---
title: Gestire gli amministratori del server in Azure Analysis Services | Microsoft Docs
description: Informazioni su come gestire gli amministratori del server per un server Analysis Services in Azure.
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
ms.openlocfilehash: a1b58125dafdf73f245b6a8cd0f4917513b22ea9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-server-administrators"></a><span data-ttu-id="d613e-103">Gestire gli amministratori del server</span><span class="sxs-lookup"><span data-stu-id="d613e-103">Manage server administrators</span></span>
<span data-ttu-id="d613e-104">Gli amministratori del server devono essere un utente o un gruppo valido in Azure Active Directory (Azure AD) per il tenant in cui si trova il server.</span><span class="sxs-lookup"><span data-stu-id="d613e-104">Server administrators must be a valid user or group in the Azure Active Directory (Azure AD) for the tenant in which the server resides.</span></span> <span data-ttu-id="d613e-105">È possibile usare **Amministratori di Analysis Services** nel pannello di controllo del server nel portale di Azure o Proprietà server in SSMS per gestire gli amministratori del server.</span><span class="sxs-lookup"><span data-stu-id="d613e-105">You can use **Analysis Services Admins** in the control blade for your server in Azure portal, or Server Properties in SSMS to manage server administrators.</span></span> 

## <a name="to-add-server-administrators-by-using-azure-portal"></a><span data-ttu-id="d613e-106">Per aggiungere amministratori del server usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d613e-106">To add server administrators by using Azure portal</span></span>
1. <span data-ttu-id="d613e-107">Nel pannello di controllo del server fare clic su **Amministratori di Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="d613e-107">In the control blade for your server, click **Analysis Services Admins**.</span></span>
2. <span data-ttu-id="d613e-108">Nel pannello **\<nomeserver> - Amministratori di Analysis Services** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d613e-108">In the **\<servername> - Analysis Services Admins** blade, click **Add**.</span></span>
3. <span data-ttu-id="d613e-109">Nel pannello **Aggiungi amministratori del server** selezionare gli account utente da Azure AD o invitare gli utenti esterni in base all'indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="d613e-109">In the **Add Server Administrators** blade, select user accounts from your Azure AD or invite external users by email address.</span></span>

    ![Amministratori del server nel portale di Azure](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="to-add-server-administrators-by-using-ssms"></a><span data-ttu-id="d613e-111">Per aggiungere amministratori del server usando SSMS</span><span class="sxs-lookup"><span data-stu-id="d613e-111">To add server administrators by using SSMS</span></span>
1. <span data-ttu-id="d613e-112">Fare clic con il pulsante destro del mouse sul server > **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="d613e-112">Right-click the server > **Properties**.</span></span>
2. <span data-ttu-id="d613e-113">In **Proprietà computer Analysis Server** fare clic su **Sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="d613e-113">In **Analysis Server Properties**, click **Security**.</span></span>
3. <span data-ttu-id="d613e-114">Fare clic su **Aggiungi** e quindi immettere l'indirizzo di posta elettronica per un utente o un gruppo in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d613e-114">Click **Add**, and then enter the email address for a user or group in your Azure AD.</span></span>
   
    ![Aggiungere gli amministratori del server in SSMS](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a><span data-ttu-id="d613e-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d613e-116">Next steps</span></span> 
[<span data-ttu-id="d613e-117">Autenticazione e autorizzazioni utente</span><span class="sxs-lookup"><span data-stu-id="d613e-117">Authentication and user permissions</span></span>](analysis-services-manage-users.md)  
[<span data-ttu-id="d613e-118">Gestire ruoli e utenti del database</span><span class="sxs-lookup"><span data-stu-id="d613e-118">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="d613e-119">Controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="d613e-119">Role-Based Access Control</span></span>](../active-directory/role-based-access-control-what-is.md)  

