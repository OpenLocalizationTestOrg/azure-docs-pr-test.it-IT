---
title: Aggiungere un dispositivo personale all'organizzazione| Documentazione Microsoft
description: Descrive come gli utenti possono registrare i dispositivi Windows 10 personali nella rete aziendale e fornisce i passaggi di distribuzione per uno scenario BYOD.
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
ms.openlocfilehash: 9418365ea18b065551448742b21c8b17a1749fc8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-personal-device-to-your-organization"></a><span data-ttu-id="53a5e-103">Aggiunta di un dispositivo personale all'organizzazione</span><span class="sxs-lookup"><span data-stu-id="53a5e-103">Join a personal device to your organization</span></span>
## <a name="to-join-a-windows-10-device-to-your-organization"></a><span data-ttu-id="53a5e-104">Per aggiungere un dispositivo Windows 10 personale all'organizzazione</span><span class="sxs-lookup"><span data-stu-id="53a5e-104">To join a Windows 10 device to your organization</span></span>
1. <span data-ttu-id="53a5e-105">Nel menu **Start** selezionare **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="53a5e-105">From the **Start** menu, select **Settings**.</span></span>
2. <span data-ttu-id="53a5e-106">Selezionare **Account**, quindi fare clic su **Account**.</span><span class="sxs-lookup"><span data-stu-id="53a5e-106">Select **Accounts**, and then click **Your account**.</span></span>
3. <span data-ttu-id="53a5e-107">Fare clic su **Aggiungi account aziendale o dell'istituto di istruzione**e quindi digitare l'account dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="53a5e-107">Click **Add Work or School account**, and then type in your organizational account.</span></span>
4. <span data-ttu-id="53a5e-108">Nella pagina di accesso per l'organizzazione, immettere il nome utente e la password e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="53a5e-108">On the sign-in page for your organization, enter your user name and password, and then click **OK**.</span></span>
5. <span data-ttu-id="53a5e-109">Verrà richiesto di effettuare una verifica Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="53a5e-109">You will be prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="53a5e-110">La verifica può essere configurata da un amministratore IT.</span><span class="sxs-lookup"><span data-stu-id="53a5e-110">(This challenge is configurable by an IT administrator.)</span></span>
6. <span data-ttu-id="53a5e-111">Azure Active Directory (Azure AD) controlla se il dispositivo richiede la registrazione per la gestione di dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="53a5e-111">Azure Active Directory (Azure AD) checks whether the device requires mobile device management enrollment.</span></span>
7. <span data-ttu-id="53a5e-112">Windows registra il dispositivo nella directory dell'organizzazione in Azure AD e lo inserisce nella gestione dei dispositivi mobili, se appropriato.</span><span class="sxs-lookup"><span data-stu-id="53a5e-112">Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
8. <span data-ttu-id="53a5e-113">Se si è un utente gestito, Windows visualizza il desktop tramite l'accesso automatico.</span><span class="sxs-lookup"><span data-stu-id="53a5e-113">If you are a managed user, Windows takes you to the desktop through the automatic sign-in.</span></span>
9. <span data-ttu-id="53a5e-114">Se si è un utente federato, viene visualizzata una schermata di accesso di Windows che consente di immettere le proprie credenziali.</span><span class="sxs-lookup"><span data-stu-id="53a5e-114">If you are a federated user, you will be taken to a Windows sign-in screen to enter your credentials.</span></span>

## <a name="additional-information"></a><span data-ttu-id="53a5e-115">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="53a5e-115">Additional information</span></span>
* [<span data-ttu-id="53a5e-116">Windows 10 per le aziende: modalità d'uso dei dispositivi di lavoro</span><span class="sxs-lookup"><span data-stu-id="53a5e-116">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="53a5e-117">Estensione delle funzionalità del cloud ai dispositivi Windows 10 tramite Aggiunta ad Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="53a5e-117">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="53a5e-118">Autenticazione delle identità senza password con Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="53a5e-118">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="53a5e-119">Scenari di utilizzo per Aggiunta ad Azure AD</span><span class="sxs-lookup"><span data-stu-id="53a5e-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="53a5e-120">Connettere dispositivi appartenenti a un dominio ad Azure AD per usufruire di Windows 10</span><span class="sxs-lookup"><span data-stu-id="53a5e-120">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="53a5e-121">Configurare Aggiunta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="53a5e-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

