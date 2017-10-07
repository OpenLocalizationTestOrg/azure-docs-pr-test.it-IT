---
title: aaaJoin un'organizzazione tooyour dispositivo personale | Documenti Microsoft
description: Viene illustrato come gli utenti possono registrare personali Windows 10 dispositivi tootheir rete aziendale e fornisce i passaggi di distribuzione per uno scenario BYOD.
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 9f3d38f5-1cfd-43d4-97da-4fed1255a1ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 979e2461dd9ad0438aa402a0a3223cc84c4c625c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-personal-device-tooyour-organization"></a><span data-ttu-id="0f007-103">Aggiungere un'organizzazione tooyour dispositivo personale</span><span class="sxs-lookup"><span data-stu-id="0f007-103">Join a personal device tooyour organization</span></span>
## <a name="toojoin-a-windows-10-device-tooyour-organization"></a><span data-ttu-id="0f007-104">organizzazione di tooyour dispositivo toojoin Windows 10</span><span class="sxs-lookup"><span data-stu-id="0f007-104">toojoin a Windows 10 device tooyour organization</span></span>
1. <span data-ttu-id="0f007-105">Da hello **avviare** dal menu **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="0f007-105">From hello **Start** menu, select **Settings**.</span></span>
2. <span data-ttu-id="0f007-106">Selezionare **Account**, quindi fare clic su **Account**.</span><span class="sxs-lookup"><span data-stu-id="0f007-106">Select **Accounts**, and then click **Your account**.</span></span>
3. <span data-ttu-id="0f007-107">Fare clic su **Aggiungi account aziendale o dell'istituto di istruzione**e quindi digitare l'account dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="0f007-107">Click **Add Work or School account**, and then type in your organizational account.</span></span>
4. <span data-ttu-id="0f007-108">In hello-pagina di accesso per l'organizzazione, immettere il nome utente e la password e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0f007-108">On hello sign-in page for your organization, enter your user name and password, and then click **OK**.</span></span>
5. <span data-ttu-id="0f007-109">Verrà richiesto di effettuare una verifica Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="0f007-109">You will be prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="0f007-110">La verifica può essere configurata da un amministratore IT.</span><span class="sxs-lookup"><span data-stu-id="0f007-110">(This challenge is configurable by an IT administrator.)</span></span>
6. <span data-ttu-id="0f007-111">Azure Active Directory (Azure AD) verifica se il dispositivo hello necessita di registrazione gestione dei dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="0f007-111">Azure Active Directory (Azure AD) checks whether hello device requires mobile device management enrollment.</span></span>
7. <span data-ttu-id="0f007-112">Windows registra il dispositivo hello nella directory dell'organizzazione hello in Azure AD e registra nella gestione dei dispositivi mobili, se appropriato.</span><span class="sxs-lookup"><span data-stu-id="0f007-112">Windows registers hello device in hello organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
8. <span data-ttu-id="0f007-113">Nel caso di un utente gestito, Windows esegue toohello desktop tramite hello automatico Accedi.</span><span class="sxs-lookup"><span data-stu-id="0f007-113">If you are a managed user, Windows takes you toohello desktop through hello automatic sign-in.</span></span>
9. <span data-ttu-id="0f007-114">Se si è un utente federato, sarà possibile prendere tooenter schermata tooa sign-in Windows le credenziali.</span><span class="sxs-lookup"><span data-stu-id="0f007-114">If you are a federated user, you will be taken tooa Windows sign-in screen tooenter your credentials.</span></span>

## <a name="additional-information"></a><span data-ttu-id="0f007-115">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0f007-115">Additional information</span></span>
* [<span data-ttu-id="0f007-116">Windows 10 per enterprise hello: i dispositivi toouse modi per lavoro</span><span class="sxs-lookup"><span data-stu-id="0f007-116">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="0f007-117">Estensione cloud dispositivi tooWindows 10 funzionalità tramite Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="0f007-117">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="0f007-118">Autenticazione delle identità senza password con Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="0f007-118">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="0f007-119">Scenari di utilizzo per Aggiunta ad Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f007-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="0f007-120">Connettersi tooAzure dispositivi appartenenti a un dominio Active Directory per Windows 10</span><span class="sxs-lookup"><span data-stu-id="0f007-120">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="0f007-121">Configurare Aggiunta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f007-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

