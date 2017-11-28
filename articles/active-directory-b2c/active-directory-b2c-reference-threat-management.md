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
ms.openlocfilehash: 60bc0cc392b332cc4e9741ddb97dfa58e68ed420
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a><span data-ttu-id="5d480-103">Azure Active Directory B2C: Gestione delle minacce</span><span class="sxs-lookup"><span data-stu-id="5d480-103">Azure Active Directory B2C: Threat management</span></span>

<span data-ttu-id="5d480-104">Gestione delle minacce include la pianificazione per la protezione da attacchi contro il sistema e le reti.</span><span class="sxs-lookup"><span data-stu-id="5d480-104">Threat management includes planning for protection from attacks against your system and networks.</span></span> <span data-ttu-id="5d480-105">Attacchi Denial of service potrebbero rendere le risorse agli utenti di toointended non disponibile.</span><span class="sxs-lookup"><span data-stu-id="5d480-105">Denial-of-service attacks might make resources unavailable toointended users.</span></span> <span data-ttu-id="5d480-106">Password attacchi lead toounauthorized accesso tooresources.</span><span class="sxs-lookup"><span data-stu-id="5d480-106">Password attacks lead toounauthorized access tooresources.</span></span> <span data-ttu-id="5d480-107">Azure Active Directory B2C (Azure AD B2C) offre funzionalità incorporate che aiutano a proteggere i dati da queste minacce in diversi modi.</span><span class="sxs-lookup"><span data-stu-id="5d480-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span></span>

## <a name="denial-of-service-attacks"></a><span data-ttu-id="5d480-108">Attacchi Denial of Service</span><span class="sxs-lookup"><span data-stu-id="5d480-108">Denial-of-service attacks</span></span>

<span data-ttu-id="5d480-109">Azure Active Directory B2C utilizza tecniche di rilevamento e prevenzione come cookie SYN e tooprotect di limiti di velocità e connessione sottostante risorse contro gli attacchi di tipo denial of service.</span><span class="sxs-lookup"><span data-stu-id="5d480-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits tooprotect underlying resources against denial-of-service attacks.</span></span>

## <a name="password-attacks"></a><span data-ttu-id="5d480-110">Attacchi alle password</span><span class="sxs-lookup"><span data-stu-id="5d480-110">Password attacks</span></span>

<span data-ttu-id="5d480-111">Azure AD B2C dispone inoltre di tecniche di mitigazione per gli attacchi alle password.</span><span class="sxs-lookup"><span data-stu-id="5d480-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span></span> <span data-ttu-id="5d480-112">Questa mitigazione include sia attacchi di forza bruta che attacchi con dizionario alle password.</span><span class="sxs-lookup"><span data-stu-id="5d480-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span></span> <span data-ttu-id="5d480-113">Le password impostati per gli utenti sono necessari toobe piuttosto complessi.</span><span class="sxs-lookup"><span data-stu-id="5d480-113">Passwords that are set by users are required toobe reasonably complex.</span></span> <span data-ttu-id="5d480-114">Tramite segnali diversi, Azure AD B2C analizza integrità hello delle richieste.</span><span class="sxs-lookup"><span data-stu-id="5d480-114">By using various signals, Azure AD B2C analyzes hello integrity of requests.</span></span> <span data-ttu-id="5d480-115">Azure Active Directory B2C è progettato toointelligently differenziare utenti previsti da pirati informatici e botnet bloccate.</span><span class="sxs-lookup"><span data-stu-id="5d480-115">Azure AD B2C is designed toointelligently differentiate intended users from hackers and botnets.</span></span> <span data-ttu-id="5d480-116">Azure Active Directory B2C fornisce un toolock strategia sofisticate gli account basati su password hello immesse, probabilità hello di un attacco.</span><span class="sxs-lookup"><span data-stu-id="5d480-116">Azure AD B2C provides a sophisticated strategy toolock accounts based on hello passwords entered, in hello likelihood of an attack.</span></span>

<span data-ttu-id="5d480-117">Per ulteriori informazioni, visitare hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span><span class="sxs-lookup"><span data-stu-id="5d480-117">For more information, visit hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span></span>
