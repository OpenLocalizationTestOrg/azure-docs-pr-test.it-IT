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
ms.openlocfilehash: 4bb7ec6ec67d3368a0e36c098f290f582510714a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a><span data-ttu-id="e8f91-103">Risoluzione dei problemi per la creazione di un tenant di Azure Active Directory o di un tenant di Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="e8f91-103">Troubleshoot creating an Azure Active Directory or Azure Active Directory B2C tenant</span></span> 

## <a name="create-an-azure-ad-tenant"></a><span data-ttu-id="e8f91-104">Come creare un tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e8f91-104">Create an Azure AD tenant</span></span>
<span data-ttu-id="e8f91-105">Se è possibile creare un tenant Azure Active Directory (Azure AD) nel primo tentativo di hello, riprovare.</span><span class="sxs-lookup"><span data-stu-id="e8f91-105">If you can't create an Azure Active Directory (Azure AD) tenant on hello first attempt, try again.</span></span> <span data-ttu-id="e8f91-106">Se hello problema persiste, contattare il supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="e8f91-106">If hello problem persists, contact Azure Support.</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="e8f91-107">Creare un tenant di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="e8f91-107">Create an Azure AD B2C tenant</span></span>
<span data-ttu-id="e8f91-108">Se si verificano problemi quando si [creare un Active Directory B2C di Azure (Azure AD B2C) tenant](active-directory-b2c-get-started.md), provare hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e8f91-108">If you encounter issues when you [create an Azure Active Directory B2C (Azure AD B2C) tenant](active-directory-b2c-get-started.md), try hello following options:</span></span>

* <span data-ttu-id="e8f91-109">Se il tenant di Azure Active Directory B2C hello non viene visualizzato nell'elenco di tenant, provare di nuovo tenant hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="e8f91-109">If hello Azure AD B2C tenant doesn't show up in your list of tenants, try again toocreate hello tenant.</span></span>
* <span data-ttu-id="e8f91-110">Se il tenant di Azure Active Directory B2C hello visualizzati nell'elenco di tenant e viene visualizzato hello seguente messaggio di errore, eliminare tenant hello e crearlo di nuovo:</span><span class="sxs-lookup"><span data-stu-id="e8f91-110">If hello Azure AD B2C tenant does show up in your list of tenants and you see hello following  error message, delete hello tenant and create it again:</span></span>

    <span data-ttu-id="e8f91-111">"Impossibile completare la creazione di hello del tenant B2C hello 'contosob2c'.</span><span class="sxs-lookup"><span data-stu-id="e8f91-111">"Could not complete hello creation of hello B2C tenant 'contosob2c'.</span></span> <span data-ttu-id="e8f91-112">Fare clic su questo [collegamento](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) per maggiori informazioni. "</span><span class="sxs-lookup"><span data-stu-id="e8f91-112">Please visit this [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) for more guidance."</span></span>
* <span data-ttu-id="e8f91-113">Vi sono problemi noti quando si elimina un esistente AD B2C Azure tenant e ricrearlo con hello stesso nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="e8f91-113">There are known issues when you delete an existing Azure AD B2C tenant and re-create it by using hello same domain name.</span></span> <span data-ttu-id="e8f91-114">Quando si crea un nuovo tenant di Azure AD B2C, è necessario utilizzare un nome di dominio diverso.</span><span class="sxs-lookup"><span data-stu-id="e8f91-114">When you create a new Azure AD B2C tenant, you must use a different domain name.</span></span>
* <span data-ttu-id="e8f91-115">Se nessuna di queste soluzioni risolve il problema, contattare il supporto di Azure.</span><span class="sxs-lookup"><span data-stu-id="e8f91-115">If these resolutions don't work, contact Azure Support.</span></span> <span data-ttu-id="e8f91-116">Per maggiori informazioni, vedere [Presentare richieste di supporto per Azure AD B2C](active-directory-b2c-support.md).</span><span class="sxs-lookup"><span data-stu-id="e8f91-116">For more information, see [File support requests for Azure AD B2C](active-directory-b2c-support.md).</span></span>

