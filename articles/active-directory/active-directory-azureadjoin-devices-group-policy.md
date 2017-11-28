---
title: si verifica nel aaaConnect tooAzure di dispositivi appartenenti a un dominio Active Directory per Windows 10 | Documenti Microsoft
description: Viene illustrato come gli amministratori possono configurare rete di criteri di gruppo tooenable dispositivi toobe toohello dominio aziendale.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2ff29f3e-5325-4f43-9baa-6ae8d6bad3e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 9766aa702352dea2ecad3a9a0bdf8d3286ee6d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a><span data-ttu-id="4c218-103">Connettersi tooAzure dispositivi appartenenti a un dominio Active Directory per Windows 10</span><span class="sxs-lookup"><span data-stu-id="4c218-103">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>
<span data-ttu-id="4c218-104">Aggiunta a un dominio è organizzazioni modalità tradizionale hello avere stabilito la connessione di dispositivi per lavoro hello ultimi 15 anni e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="4c218-104">Domain join is hello traditional way organizations have connected devices for work for hello last 15 years and more.</span></span> <span data-ttu-id="4c218-105">È abilitato toosign utenti nei dispositivi tootheir utilizzando il proprio lavoro di Windows Server Active Directory (Active Directory) o scuola e consentiti toofully IT di gestire questi dispositivi.</span><span class="sxs-lookup"><span data-stu-id="4c218-105">It has enabled users toosign in tootheir devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT toofully manage these devices.</span></span> <span data-ttu-id="4c218-106">Le organizzazioni si basano su metodi tooprovision dispositivi toousers imaging e in genere utilizzare criteri di gruppo o System Center Configuration Manager (SCCM) toomanage li.</span><span class="sxs-lookup"><span data-stu-id="4c218-106">Organizations typically rely on imaging methods tooprovision devices toousers and generally use System Center Configuration Manager (SCCM) or Group Policy toomanage them.</span></span>


<span data-ttu-id="4c218-107">Aggiunta a un dominio Windows 10 vengono fornite hello seguenti vantaggi dopo aver connesso i dispositivi tooAzure Active Directory (Azure AD):</span><span class="sxs-lookup"><span data-stu-id="4c218-107">Domain join in Windows 10 provides you with hello following benefits after you connect devices tooAzure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="4c218-108">Single sign-on (SSO) tooAzure AD risorse da qualsiasi posizione</span><span class="sxs-lookup"><span data-stu-id="4c218-108">Single sign-on (SSO) tooAzure AD resources from anywhere</span></span>
* <span data-ttu-id="4c218-109">Accedere a toohello enterprise, Windows Store utilizzando lavoro o scuola account (necessari account di Microsoft)</span><span class="sxs-lookup"><span data-stu-id="4c218-109">Access toohello enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="4c218-110">Roaming delle impostazioni utente tra dispositivi conforme ai criteri dell'organizzazione usando account aziendali o dell'istituto di istruzione, non è necessario un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4c218-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="4c218-111">Autenticazione avanzata e pratico accesso all'account aziendale o dell'istituto di istruzione con Windows Hello for Business e Windows Hello</span><span class="sxs-lookup"><span data-stu-id="4c218-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="4c218-112">Toorestrict possibilità di accedere solo toodevices conformi con le impostazioni di criteri di gruppo di dispositivi aziendali</span><span class="sxs-lookup"><span data-stu-id="4c218-112">Ability toorestrict access only toodevices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c218-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4c218-113">Prerequisites</span></span>
<span data-ttu-id="4c218-114">Aggiunta a un dominio continua toobe utile.</span><span class="sxs-lookup"><span data-stu-id="4c218-114">Domain join continues toobe useful.</span></span> <span data-ttu-id="4c218-115">Tuttavia, tooget i vantaggi di hello Azure AD di SSO, il roaming delle impostazioni con o lavoro o scuola account e accedere tooWindows archivio con lavoro o scuola account, sarà necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c218-115">However, tooget hello Azure AD benefits of SSO, roaming of settings with work or school accounts, and access tooWindows Store with work or school accounts, you will need hello following:</span></span>

* <span data-ttu-id="4c218-116">Sottoscrizione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c218-116">Azure AD subscription</span></span>
* <span data-ttu-id="4c218-117">Azure AD Connect tooextend hello locale tooAzure di directory Active Directory</span><span class="sxs-lookup"><span data-stu-id="4c218-117">Azure AD Connect tooextend hello on-premises directory tooAzure AD</span></span>
* <span data-ttu-id="4c218-118">Criteri impostati tooconnect tooAzure di dispositivi appartenenti a un dominio Active Directory</span><span class="sxs-lookup"><span data-stu-id="4c218-118">Policy that's set tooconnect domain-joined devices tooAzure AD</span></span>
* <span data-ttu-id="4c218-119">Build di Windows 10 (build 10551 o successiva) per i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="4c218-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="4c218-120">tooenable Windows Hello for Business e di Windows Hello, è necessario anche seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="4c218-120">tooenable Windows Hello for Business and Windows Hello, you will also need hello following:</span></span>

- <span data-ttu-id="4c218-121">**Infrastruttura a chiave pubblica (PKI)** per il rilascio di certificati utente.</span><span class="sxs-lookup"><span data-stu-id="4c218-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="4c218-122">**System Center Configuration Manager Current Branch** -è necessario tooinstall versione 1606 o migliori.</span><span class="sxs-lookup"><span data-stu-id="4c218-122">**System Center Configuration Manager Current Branch** - You need tooinstall version 1606 or better.</span></span>  
<span data-ttu-id="4c218-123">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="4c218-123">For more information, see:</span></span> 
    - [<span data-ttu-id="4c218-124">Documentazione per System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="4c218-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="4c218-125">Blog del team di System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="4c218-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="4c218-126">Impostazioni di Windows Hello for Business in System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="4c218-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="4c218-127">Come requisito distribuzione PKI toohello alternativo, è possibile eseguire il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="4c218-127">As an alternative toohello PKI deployment requirement, you can do hello following:</span></span>

* <span data-ttu-id="4c218-128">Disporre di alcuni controller di dominio con Servizi di dominio Active Directory di Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="4c218-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="4c218-129">tooenable l'accesso condizionale, è possibile creare le impostazioni di criteri di gruppo che consentono di accedere ai dispositivi aggiunti a un toodomain con nessun altre distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="4c218-129">tooenable conditional access, you can create Group Policy settings that allow access toodomain-joined devices with no additional deployments.</span></span> <span data-ttu-id="4c218-130">controllo di accesso toomanage basata sulla conformità del dispositivo hello, sarà necessario seguente hello:</span><span class="sxs-lookup"><span data-stu-id="4c218-130">toomanage access control based on compliance of hello device, you will need hello following:</span></span>

* <span data-ttu-id="4c218-131">System Center Configuration Manager Current Branch (1606 o versione successiva) per scenari Windows Hello for Business</span><span class="sxs-lookup"><span data-stu-id="4c218-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="4c218-132">Istruzioni per la distribuzione</span><span class="sxs-lookup"><span data-stu-id="4c218-132">Deployment instructions</span></span>

<span data-ttu-id="4c218-133">toodeploy, seguire la procedura seguente hello elencata in [come tooconfigure la registrazione automatica di Windows appartenenti a un dominio dispositivi con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="4c218-133">toodeploy, follow hello steps listed in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="4c218-134">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="4c218-134">Next step</span></span>
* [<span data-ttu-id="4c218-135">Windows 10 per enterprise hello: i dispositivi toouse modi per lavoro</span><span class="sxs-lookup"><span data-stu-id="4c218-135">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="4c218-136">Estensione cloud dispositivi tooWindows 10 funzionalità tramite Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="4c218-136">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="4c218-137">Scenari di utilizzo per Aggiunta ad Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c218-137">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="4c218-138">Connettersi tooAzure dispositivi appartenenti a un dominio Active Directory per Windows 10</span><span class="sxs-lookup"><span data-stu-id="4c218-138">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="4c218-139">Configurare Aggiunta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c218-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

