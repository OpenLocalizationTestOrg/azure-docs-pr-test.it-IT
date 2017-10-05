---
title: "Windows 10 per le aziende: modalità d'uso dei dispositivi di lavoro | Documentazione Microsoft"
description: "Panoramica della distribuzione dei dispositivi Windows 10 per le grandi imprese e dell'integrazione con Azure Active Directory per il cloud di Windows. Confronta i diversi modi in cui è possibile effettuare il provisioning di un dispositivo e usarlo in un'organizzazione tramite il portale di Azure."
keywords: cloud windows, Windows in Azure Active Directory, dispositivi Windows 10 in Azure, dispositivi Windows in Azure
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2cb9ab6a-55b6-4658-b7f2-6e05ae015e1b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 804156048a7596f9937098e6fe762f424526473c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="windows-10-for-the-enterprise-ways-to-use-devices-for-work"></a><span data-ttu-id="7e8e0-105">Windows 10 per le aziende: modalità d'uso dei dispositivi di lavoro</span><span class="sxs-lookup"><span data-stu-id="7e8e0-105">Windows 10 for the enterprise: Ways to use devices for work</span></span>
<span data-ttu-id="7e8e0-106">Windows 10 offre la possibilità di sfruttare Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7e8e0-106">Windows 10 gives you the ability to leverage Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="7e8e0-107">È possibile connettere i dispositivi Windows 10 ad Azure AD in modo che gli utenti possano accedere a Windows usando gli account di Azure AD o aggiungendo i propri ID Azure per accedere alle risorse e alle app aziendali.</span><span class="sxs-lookup"><span data-stu-id="7e8e0-107">You can connect Windows 10 devices to Azure AD so that users can sign in to Windows by using Azure AD accounts or by adding their Azure IDs to gain access to business apps and resources.</span></span>

![Azure Active Directory con cloud Windows](./media/active-directory-azureadjoin/windows10-overview.png)

## <a name="integrating-windows-10-devices-with-azure-active-directory--a-content-map"></a><span data-ttu-id="7e8e0-109">Integrazione di dispositivi Windows 10 con Azure Active Directory - una mappa del contenuto</span><span class="sxs-lookup"><span data-stu-id="7e8e0-109">Integrating Windows 10 devices with Azure Active Directory--a content map</span></span>
<span data-ttu-id="7e8e0-110">I seguenti argomenti forniscono informazioni sulle diverse funzionalità dei dispositivi Windows 10 nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="7e8e0-110">The following topics provide insights into different capabilities of Windows 10 devices in your organization.</span></span>

|  | <span data-ttu-id="7e8e0-111">Argomenti</span><span class="sxs-lookup"><span data-stu-id="7e8e0-111">Topics</span></span> |
| --- | --- |
| <span data-ttu-id="7e8e0-112">Introduzione</span><span class="sxs-lookup"><span data-stu-id="7e8e0-112">Getting started</span></span> |[<span data-ttu-id="7e8e0-113">Uso di dispositivi Windows 10 in azienda</span><span class="sxs-lookup"><span data-stu-id="7e8e0-113">Using Windows 10 devices in your workplace</span></span>](active-directory-azureadjoin-windows10-devices.md) <br> <br> [<span data-ttu-id="7e8e0-114">Estensione delle funzionalità del cloud ai dispositivi Windows 10 tramite Aggiunta ad Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e8e0-114">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-overview.md) <br> <br> [<span data-ttu-id="7e8e0-115">Autenticazione delle identità senza password con Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="7e8e0-115">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md) |
| <span data-ttu-id="7e8e0-116">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="7e8e0-116">Deployment</span></span> |[<span data-ttu-id="7e8e0-117">Scenari di utilizzo e considerazioni sulla distribuzione per Aggiunta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e8e0-117">Usage scenarios and deployment considerations for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md) <br><br> [<span data-ttu-id="7e8e0-118">Connessione di dispositivi appartenenti a un dominio ad Azure AD per usufruire di Windows 10</span><span class="sxs-lookup"><span data-stu-id="7e8e0-118">Connecting domain-joined devices to Azure AD, for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)<br><br>[<span data-ttu-id="7e8e0-119">Abilitazione di Microsoft Passport for Work nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="7e8e0-119">Enabling Microsoft Passport for work in the organization</span></span>](active-directory-azureadjoin-passport-deployment.md)<br><br> [<span data-ttu-id="7e8e0-120">Abilitazione di Enterprise State Roaming per Windows 10</span><span class="sxs-lookup"><span data-stu-id="7e8e0-120">Enabling Enterprise State Roaming for Windows 10</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)<br><br> |
| <span data-ttu-id="7e8e0-121">Attività dell'utente</span><span class="sxs-lookup"><span data-stu-id="7e8e0-121">User tasks</span></span> |[<span data-ttu-id="7e8e0-122">Configurazione di un nuovo dispositivo Windows 10 con Azure AD durante l'installazione</span><span class="sxs-lookup"><span data-stu-id="7e8e0-122">Setting up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md) <br><br> [<span data-ttu-id="7e8e0-123">Configurazione di un dispositivo Windows 10 con Azure AD dal menu Impostazioni</span><span class="sxs-lookup"><span data-stu-id="7e8e0-123">Setting up a Windows 10 device with Azure AD from the settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md) <br><br> [<span data-ttu-id="7e8e0-124">Associazione di un dispositivo Windows 10 personale all'organizzazione</span><span class="sxs-lookup"><span data-stu-id="7e8e0-124">Joining a personal Windows 10 device to your organization</span></span>](active-directory-azureadjoin-personal-device.md) |

