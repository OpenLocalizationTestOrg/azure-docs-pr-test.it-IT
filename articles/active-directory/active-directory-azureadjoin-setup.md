---
title: aaaSetting aggiunta di Azure AD per gli utenti | Documenti Microsoft
description: Viene illustrato come gli amministratori possono configurare Aggiunta da Azure AD per la directory locale e la registrazione del dispositivo.
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 60a5aeb11292cb6057ab1065c3ab77e5981d0cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a><span data-ttu-id="bc11f-103">Configurazione di Aggiunta ad Azure AD nell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="bc11f-103">Setting up Azure AD Join in your organization</span></span>
<span data-ttu-id="bc11f-104">Prima di configurare Azure Active Directory Join (aggiunta di Azure AD), si desidera eseguire la sincronizzazione tooeither configurare la directory locale del cloud toohello utenti oppure creare manualmente gli account gestiti in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bc11f-104">Before you set up Azure Active Directory Join (Azure AD Join), you need tooeither sync up your on-premises directory of users toohello cloud or manually create managed accounts in Azure AD.</span></span>

<span data-ttu-id="bc11f-105">Istruzioni dettagliate per la sincronizzazione del tooAzure gli utenti locali Active Directory è trattata nella [integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="bc11f-105">Detailed instructions for syncing your on-premises users tooAzure AD is covered in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="bc11f-106">toomanually creare e gestire gli utenti in Azure AD, fare riferimento troppo[Gestione utenti in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span><span class="sxs-lookup"><span data-stu-id="bc11f-106">toomanually create and manage users in Azure AD, refer too[User management in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span></span>

## <a name="set-up-device-registration"></a><span data-ttu-id="bc11f-107">Configurare la registrazione dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="bc11f-107">Set up device registration</span></span>
1. <span data-ttu-id="bc11f-108">Accedere toohello portale di Azure come amministratore.</span><span class="sxs-lookup"><span data-stu-id="bc11f-108">Log on toohello Azure portal as an administrator.</span></span>
2. <span data-ttu-id="bc11f-109">Nel riquadro sinistro di hello selezionare **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bc11f-109">On hello left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="bc11f-110">In hello **Directory** scheda, selezionare la directory.</span><span class="sxs-lookup"><span data-stu-id="bc11f-110">On hello **Directory** tab, select your directory.</span></span>
4. <span data-ttu-id="bc11f-111">Seleziona hello **configura** scheda.</span><span class="sxs-lookup"><span data-stu-id="bc11f-111">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="bc11f-112">Passare toohello **dispositivi** sezione.</span><span class="sxs-lookup"><span data-stu-id="bc11f-112">Go toohello **Devices** section.</span></span>
6. <span data-ttu-id="bc11f-113">In hello **dispositivi** scheda, impostare hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="bc11f-113">On hello **devices** tab, set hello following:</span></span>  
   * <span data-ttu-id="bc11f-114">**MASSIMO numero di dispositivi PER utente**: selezionare hello il numero massimo di dispositivi che un utente può disporre di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bc11f-114">**MAXIMUM NUMBER OF DEVICES PER USER**: Select hello maximum number of devices that a user can have in Azure AD.</span></span>  <span data-ttu-id="bc11f-115">Se un utente raggiunge questa quota, non sarà in grado di tooadd altri dispositivi fino alla rimozione di uno o più dispositivi esistenti.</span><span class="sxs-lookup"><span data-stu-id="bc11f-115">If a user reaches this quota, they will not be able tooadd additional devices until one or more of their existing devices are removed.</span></span>
   * <span data-ttu-id="bc11f-116">**TooJOIN multi-FACTOR Authentication RICHIEDENDO dispositivi**: specificare se gli utenti sono necessari tooprovide una seconda autenticazione fattori toojoin loro tooAzure dispositivo Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bc11f-116">**REQUIRE MULTI-FACTOR AUTH tooJOIN DEVICES**: Set whether users are required tooprovide a second authentication factor toojoin their device tooAzure AD.</span></span> <span data-ttu-id="bc11f-117">Per ulteriori informazioni su Azure multi-Factor Authentication, vedere [Introduzione ad Azure multi-Factor Authentication nel cloud hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="bc11f-117">For more information on Azure Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in hello cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>
   * <span data-ttu-id="bc11f-118">**Gli utenti possono AZURE AD aggiungere dispositivi**: selezionare hello utenti e gruppi che sono consentiti toojoin dispositivi tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bc11f-118">**USERS MAY AZURE AD JOIN DEVICES**: Select hello users and groups that are allowed toojoin devices tooAzure AD.</span></span>
   * <span data-ttu-id="bc11f-119">**I dispositivi aggiunti AD altri amministratori ON AZURE**: con Azure AD Premium o hello Enterprise Mobility Suite (EMS), è possibile scegliere gli utenti che dispongono di diritti di amministratore locale toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bc11f-119">**ADDITIONAL ADMINISTRATORS ON AZURE AD JOINED DEVICES**: With Azure AD Premium or hello Enterprise Mobility Suite (EMS), you can choose which users are granted local administrator rights toohello device.</span></span> <span data-ttu-id="bc11f-120">Per impostazione predefinita, agli amministratori globali e ai proprietari dei dispositivi vengono sempre concessi i diritti di amministratore locale.</span><span class="sxs-lookup"><span data-stu-id="bc11f-120">Global administrators and device owners are granted local administrator rights by default.</span></span>

<span data-ttu-id="bc11f-121"><center>![Configurare la registrazione dei dispositivi](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span><span class="sxs-lookup"><span data-stu-id="bc11f-121"><center>![Set up device regisration](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span></span>

<span data-ttu-id="bc11f-122">Dopo aver impostato l'aggiunta di Azure AD per gli utenti, è possibile connettere tooAzure AD tramite aziendale o dispositivi personali.</span><span class="sxs-lookup"><span data-stu-id="bc11f-122">After you set up Azure AD Join for your users, they can connect tooAzure AD through their corporate or personal devices.</span></span>

<span data-ttu-id="bc11f-123">Di seguito sono tre scenari hello è possibile utilizzare il tooset utenti tooenable aggiunta di Azure AD:</span><span class="sxs-lookup"><span data-stu-id="bc11f-123">Following are hello three scenarios you can use tooenable your users tooset up Azure AD Join:</span></span>

* <span data-ttu-id="bc11f-124">Gli utenti di aggiungere un dispositivo di proprietà dell'azienda direttamente tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bc11f-124">Users join a company-owned device directly tooAzure AD.</span></span>
* <span data-ttu-id="bc11f-125">Toohello dispositivo aggiunta al dominio una proprietà dell'azienda di utenti Active Directory locale, quindi estesa hello dispositivo tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bc11f-125">Users domain-join a company-owned device toohello on-premises Active Directory and then extend hello device tooAzure AD.</span></span>
* <span data-ttu-id="bc11f-126">Gli utenti di aggiungere lavoro o scuola account tooWindows su un dispositivo personale</span><span class="sxs-lookup"><span data-stu-id="bc11f-126">Users add work or school accounts tooWindows on a personal device</span></span>

## <a name="additional-information"></a><span data-ttu-id="bc11f-127">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="bc11f-127">Additional information</span></span>
* [<span data-ttu-id="bc11f-128">Windows 10 per enterprise hello: i dispositivi toouse modi per lavoro</span><span class="sxs-lookup"><span data-stu-id="bc11f-128">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="bc11f-129">Estensione cloud dispositivi tooWindows 10 funzionalità tramite Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="bc11f-129">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="bc11f-130">Scenari di utilizzo per Aggiunta ad Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc11f-130">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="bc11f-131">Connettersi tooAzure dispositivi appartenenti a un dominio Active Directory per Windows 10</span><span class="sxs-lookup"><span data-stu-id="bc11f-131">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="bc11f-132">Configurare Aggiunta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc11f-132">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

