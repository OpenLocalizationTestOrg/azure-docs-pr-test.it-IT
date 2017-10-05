---
title: 'Azure Active Directory B2C: Risoluzione dei problemi per la creazione di tenant | Documentazione Microsoft'
description: Problemi e soluzioni per la creazione di un tenant di Azure Active Directory o di un tenant di Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 7ba4c6b2-161b-45b5-b3bd-ccb662f5d7a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 81af4536fc223319369aff262d42149cfbf1a1e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a><span data-ttu-id="ee88f-103">Risoluzione dei problemi per la creazione di un tenant di Azure Active Directory o di un tenant di Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="ee88f-103">Troubleshoot creating an Azure Active Directory or Azure Active Directory B2C tenant</span></span> 

## <a name="create-an-azure-ad-tenant"></a><span data-ttu-id="ee88f-104">Come creare un tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ee88f-104">Create an Azure AD tenant</span></span>
<span data-ttu-id="ee88f-105">Se non è possibile creare un tenant Azure Active Directory (Azure AD) al primo tentativo, riprovare.</span><span class="sxs-lookup"><span data-stu-id="ee88f-105">If you can't create an Azure Active Directory (Azure AD) tenant on the first attempt, try again.</span></span> <span data-ttu-id="ee88f-106">Se il problema persiste, contattare il supporto di Azure.</span><span class="sxs-lookup"><span data-stu-id="ee88f-106">If the problem persists, contact Azure Support.</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="ee88f-107">Creare un tenant di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="ee88f-107">Create an Azure AD B2C tenant</span></span>
<span data-ttu-id="ee88f-108">Se si verificano problemi quando si [crea un tenant di Azure Active Directory B2C (Azure AD B2C)](active-directory-b2c-get-started.md), provare le seguenti opzioni:</span><span class="sxs-lookup"><span data-stu-id="ee88f-108">If you encounter issues when you [create an Azure Active Directory B2C (Azure AD B2C) tenant](active-directory-b2c-get-started.md), try the following options:</span></span>

* <span data-ttu-id="ee88f-109">Se il tenant di Azure AD B2C non viene visualizzato nell'elenco di tenant, riprovare a creare il tenant.</span><span class="sxs-lookup"><span data-stu-id="ee88f-109">If the Azure AD B2C tenant doesn't show up in your list of tenants, try again to create the tenant.</span></span>
* <span data-ttu-id="ee88f-110">Se il tenant di Azure Active Directory B2C viene visualizzato nell'elenco di tenant e compare il seguente messaggio di errore, eliminare il tenant e crearlo di nuovo:</span><span class="sxs-lookup"><span data-stu-id="ee88f-110">If the Azure AD B2C tenant does show up in your list of tenants and you see the following  error message, delete the tenant and create it again:</span></span>

    <span data-ttu-id="ee88f-111">"Impossibile completare la creazione del tenant B2C 'contosob2c'.</span><span class="sxs-lookup"><span data-stu-id="ee88f-111">"Could not complete the creation of the B2C tenant 'contosob2c'.</span></span> <span data-ttu-id="ee88f-112">Fare clic su questo [collegamento](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) per maggiori informazioni. "</span><span class="sxs-lookup"><span data-stu-id="ee88f-112">Please visit this [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) for more guidance."</span></span>
* <span data-ttu-id="ee88f-113">Si verificano problemi noti quando si elimina un tenant Azure AD B2C esistente e lo si crea nuovamente utilizzando lo stesso nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="ee88f-113">There are known issues when you delete an existing Azure AD B2C tenant and re-create it by using the same domain name.</span></span> <span data-ttu-id="ee88f-114">Quando si crea un nuovo tenant di Azure AD B2C, è necessario utilizzare un nome di dominio diverso.</span><span class="sxs-lookup"><span data-stu-id="ee88f-114">When you create a new Azure AD B2C tenant, you must use a different domain name.</span></span>
* <span data-ttu-id="ee88f-115">Se nessuna di queste soluzioni risolve il problema, contattare il supporto di Azure.</span><span class="sxs-lookup"><span data-stu-id="ee88f-115">If these resolutions don't work, contact Azure Support.</span></span> <span data-ttu-id="ee88f-116">Per maggiori informazioni, vedere [Presentare richieste di supporto per Azure AD B2C](active-directory-b2c-support.md).</span><span class="sxs-lookup"><span data-stu-id="ee88f-116">For more information, see [File support requests for Azure AD B2C](active-directory-b2c-support.md).</span></span>

