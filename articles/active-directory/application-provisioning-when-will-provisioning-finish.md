---
title: "aaaUser provisioning applicazione raccolta tooan Azure AD è tenuto ore o più | Documenti Microsoft"
description: "Come toofind il motivo per cui effettuare il provisioning tooyour applicazione potrebbe essere richiede più tempo del previsto"
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
ms.openlocfilehash: 0658f041724c91ddd1997cc7759393b46680f13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="user-provisioning-tooan-azure-ad-gallery-application-is-taking-hours-or-more"></a><span data-ttu-id="545cb-103">Provisioning dell'applicazione raccolta tooan Azure AD dell'utente è tenuto ore o più</span><span class="sxs-lookup"><span data-stu-id="545cb-103">User provisioning tooan Azure AD Gallery application is taking hours or more</span></span>

<span data-ttu-id="545cb-104">Quando si abilita innanzitutto il provisioning automatico di un'applicazione, la sincronizzazione iniziale hello può richiedere ore tooseveral 20 minuti, a seconda delle dimensioni di hello della directory di Azure AD hello e il numero di hello di utenti nell'ambito per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="545cb-104">When first enabling automatic provisioning for an application, hello initial sync can take anywhere from 20 minutes tooseveral hours, depending on hello size of hello Azure AD directory and hello number of users in scope for provisioning.</span></span> 

<span data-ttu-id="545cb-105">Le sincronizzazioni successive dopo la sincronizzazione iniziale di hello risultare più veloce, come hello provisioning servizio archivia le soglie che rappresentano lo stato di hello di entrambi i sistemi dopo la sincronizzazione iniziale hello, migliorando le prestazioni di sincronizzazioni successive.</span><span class="sxs-lookup"><span data-stu-id="545cb-105">Subsequent syncs after hello initial sync be faster, as hello provisioning service stores watermarks that represent hello state of both systems after hello initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-tooimprove-provisioning-performance"></a><span data-ttu-id="545cb-106">Come tooimprove provisioning delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="545cb-106">How tooimprove provisioning performance</span></span>

<span data-ttu-id="545cb-107">Se la sincronizzazione iniziale hello richiede più di qualche ora, c'è una cosa è possibile eseguire tooimprove prestazioni:</span><span class="sxs-lookup"><span data-stu-id="545cb-107">If hello initial sync is taking more than a few hours, there is one thing you can do tooimprove performance:</span></span>

-   <span data-ttu-id="545cb-108">**Filtri di ambito utente**</span><span class="sxs-lookup"><span data-stu-id="545cb-108">**User scoping filters.**</span></span> <span data-ttu-id="545cb-109">I filtri di ambito consentono toofine ottimizzazione hello i dati hello provisioning servizio estrae da Azure AD filtrando gli utenti in base ai valori di attributo specifico.</span><span class="sxs-lookup"><span data-stu-id="545cb-109">Scoping filters allow you toofine tune hello data that hello provisioning service extracts from Azure AD by filtering out users based on specific attribute values.</span></span> <span data-ttu-id="545cb-110">Per altre informazioni sui filtri di ambito, vedere [Provisioning dell'applicazione basato su attributi con filtri per la definizione dell'ambito](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span><span class="sxs-lookup"><span data-stu-id="545cb-110">For more information on scoping filters, see [Attribute-based application provisioning with scoping filters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="545cb-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="545cb-111">Next steps</span></span>
[<span data-ttu-id="545cb-112">Automatizzare Provisioning e Deprovisioning tooSaaS applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="545cb-112">Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)

