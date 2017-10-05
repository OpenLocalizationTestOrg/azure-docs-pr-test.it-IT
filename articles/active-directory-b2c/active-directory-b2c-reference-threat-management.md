---
title: 'Azure Active Directory B2C: Gestione delle minacce | Documentazione Microsoft'
description: Vengono illustrate le tecniche di rilevamento e mitigazione di attacchi Denial of Service e attacchi alle password in Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: vigunase
manager: Ajith Alexander
editor: 
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2016
ms.author: 
ms.openlocfilehash: 9472cb01eb713e297053727b1a314293574bb657
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a><span data-ttu-id="37aa4-103">Azure Active Directory B2C: Gestione delle minacce</span><span class="sxs-lookup"><span data-stu-id="37aa4-103">Azure Active Directory B2C: Threat management</span></span>

<span data-ttu-id="37aa4-104">Gestione delle minacce include la pianificazione per la protezione da attacchi contro il sistema e le reti.</span><span class="sxs-lookup"><span data-stu-id="37aa4-104">Threat management includes planning for protection from attacks against your system and networks.</span></span> <span data-ttu-id="37aa4-105">Gli attacchi Denial of Service potrebbero rendere le risorse non disponibili agli utenti previsti.</span><span class="sxs-lookup"><span data-stu-id="37aa4-105">Denial-of-service attacks might make resources unavailable to intended users.</span></span> <span data-ttu-id="37aa4-106">Gli attacchi alle password comportano un rischio di accesso non autorizzato alle risorse.</span><span class="sxs-lookup"><span data-stu-id="37aa4-106">Password attacks lead to unauthorized access to resources.</span></span> <span data-ttu-id="37aa4-107">Azure Active Directory B2C (Azure AD B2C) offre funzionalità incorporate che aiutano a proteggere i dati da queste minacce in diversi modi.</span><span class="sxs-lookup"><span data-stu-id="37aa4-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span></span>

## <a name="denial-of-service-attacks"></a><span data-ttu-id="37aa4-108">Attacchi Denial of Service</span><span class="sxs-lookup"><span data-stu-id="37aa4-108">Denial-of-service attacks</span></span>

<span data-ttu-id="37aa4-109">Azure AD B2C usa tecniche di rilevamento e mitigazione, ad esempio cookie SYN e limiti di velocità e connessione, per proteggere le risorse sottostanti dagli attacchi Denial of Service.</span><span class="sxs-lookup"><span data-stu-id="37aa4-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits to protect underlying resources against denial-of-service attacks.</span></span>

## <a name="password-attacks"></a><span data-ttu-id="37aa4-110">Attacchi alle password</span><span class="sxs-lookup"><span data-stu-id="37aa4-110">Password attacks</span></span>

<span data-ttu-id="37aa4-111">Azure AD B2C dispone inoltre di tecniche di mitigazione per gli attacchi alle password.</span><span class="sxs-lookup"><span data-stu-id="37aa4-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span></span> <span data-ttu-id="37aa4-112">Questa mitigazione include sia attacchi di forza bruta che attacchi con dizionario alle password.</span><span class="sxs-lookup"><span data-stu-id="37aa4-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span></span> <span data-ttu-id="37aa4-113">Le password impostate dagli utenti devono essere ragionevolmente complesse.</span><span class="sxs-lookup"><span data-stu-id="37aa4-113">Passwords that are set by users are required to be reasonably complex.</span></span> <span data-ttu-id="37aa4-114">Tramite segnali diversi, Azure AD B2C analizza l'integrità delle richieste.</span><span class="sxs-lookup"><span data-stu-id="37aa4-114">By using various signals, Azure AD B2C analyzes the integrity of requests.</span></span> <span data-ttu-id="37aa4-115">Azure Active Directory B2C è progettato per distinguere in modo intelligente gli utenti previsti da hacker e botnet.</span><span class="sxs-lookup"><span data-stu-id="37aa4-115">Azure AD B2C is designed to intelligently differentiate intended users from hackers and botnets.</span></span> <span data-ttu-id="37aa4-116">Azure AD B2C fornisce una sofisticata strategia di blocco account in base alle password immesse rispetto alla probabilità di un attacco.</span><span class="sxs-lookup"><span data-stu-id="37aa4-116">Azure AD B2C provides a sophisticated strategy to lock accounts based on the passwords entered, in the likelihood of an attack.</span></span>

<span data-ttu-id="37aa4-117">Per maggiori informazioni, visitare il [Centro protezione Microsoft](https://www.microsoft.com/trustcenter/security/threatmanagement).</span><span class="sxs-lookup"><span data-stu-id="37aa4-117">For more information, visit the [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span></span>
