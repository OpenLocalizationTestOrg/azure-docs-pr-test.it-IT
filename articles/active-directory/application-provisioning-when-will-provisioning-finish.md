---
title: Il provisioning utenti per un'applicazione della raccolta di AD Azure richiede alcune ore o tempi maggiori | Microsoft Docs
description: "Come individuare il motivo per cui il provisioning per l'applicazione in uso può richiedere più tempo del previsto"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 183d60cbbbc8d02f7cd3cacc160453c45717ef0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="user-provisioning-to-an-azure-ad-gallery-application-is-taking-hours-or-more"></a><span data-ttu-id="5237d-103">Il provisioning utenti per un'applicazione della raccolta di AD Azure richiede alcune ore o tempi maggiori</span><span class="sxs-lookup"><span data-stu-id="5237d-103">User provisioning to an Azure AD Gallery application is taking hours or more</span></span>

<span data-ttu-id="5237d-104">Quando si abilita il provisioning automatico per un'applicazione, la sincronizzazione iniziale può richiedere da 20 minuti a diverse ore, a seconda delle dimensioni della directory di Azure AD e del numero di utenti inclusi nell'ambito del provisioning.</span><span class="sxs-lookup"><span data-stu-id="5237d-104">When first enabling automatic provisioning for an application, the initial sync can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span></span> 

<span data-ttu-id="5237d-105">Le sincronizzazioni successive a quella iniziale risultano più veloci, poiché il servizio di provisioning archivia i limiti che rappresentano lo stato di entrambi i sistemi dopo la sincronizzazione iniziale, migliorando le prestazioni delle sincronizzazioni successive.</span><span class="sxs-lookup"><span data-stu-id="5237d-105">Subsequent syncs after the initial sync be faster, as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-to-improve-provisioning-performance"></a><span data-ttu-id="5237d-106">Come migliorare le prestazioni del provisioning</span><span class="sxs-lookup"><span data-stu-id="5237d-106">How to improve provisioning performance</span></span>

<span data-ttu-id="5237d-107">Se la sincronizzazione iniziale richiede più di qualche ora, è possibile eseguire un'operazione per migliorare le prestazioni:</span><span class="sxs-lookup"><span data-stu-id="5237d-107">If the initial sync is taking more than a few hours, there is one thing you can do to improve performance:</span></span>

-   <span data-ttu-id="5237d-108">**Filtri di ambito utente**</span><span class="sxs-lookup"><span data-stu-id="5237d-108">**User scoping filters.**</span></span> <span data-ttu-id="5237d-109">I filtri di ambito consentono di ottimizzare i dati che il servizio di provisioning estrae da Azure AD, filtrando gli utenti in base a valori di attributo specifici.</span><span class="sxs-lookup"><span data-stu-id="5237d-109">Scoping filters allow you to fine tune the data that the provisioning service extracts from Azure AD by filtering out users based on specific attribute values.</span></span> <span data-ttu-id="5237d-110">Per altre informazioni sui filtri di ambito, vedere [Provisioning dell'applicazione basato su attributi con filtri per la definizione dell'ambito](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span><span class="sxs-lookup"><span data-stu-id="5237d-110">For more information on scoping filters, see [Attribute-based application provisioning with scoping filters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5237d-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5237d-111">Next steps</span></span>
[<span data-ttu-id="5237d-112">Automatizzare il provisioning e il deprovisioning utenti in applicazioni SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5237d-112">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)

