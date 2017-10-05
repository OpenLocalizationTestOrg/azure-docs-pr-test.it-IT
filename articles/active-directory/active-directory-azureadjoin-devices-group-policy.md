---
title: Connettere dispositivi aggiunti a un dominio ad Azure AD in ambiente Windows 10 | Documentazione Microsoft
description: Illustra agli amministratori come configurare Criteri di gruppo per abilitare i dispositivi per l'aggiunta a un dominio nella rete dell'organizzazione.
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
ms.openlocfilehash: 9c91579d20bb84701f6d0b97d944728c84044adf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="connect-domain-joined-devices-to-azure-ad-for-windows-10-experiences"></a><span data-ttu-id="a5979-103">Connettere dispositivi aggiunti a un dominio ad Azure AD in ambiente Windows 10</span><span class="sxs-lookup"><span data-stu-id="a5979-103">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>
<span data-ttu-id="a5979-104">Negli ultimi 15 anni, per connettere i dispositivi sui cui lavorare le aziende hanno fatto essenzialmente ricorso alla funzione di aggiunta a un dominio.</span><span class="sxs-lookup"><span data-stu-id="a5979-104">Domain join is the traditional way organizations have connected devices for work for the last 15 years and more.</span></span> <span data-ttu-id="a5979-105">Questo ha permesso agli utenti di accedere ai dispositivi con i relativi account aziendali o dell'istituto di istruzione di Windows Server Active Directory (Active Directory) e agli amministratori IT di gestire interamente tali dispositivi.</span><span class="sxs-lookup"><span data-stu-id="a5979-105">It has enabled users to sign in to their devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT to fully manage these devices.</span></span> <span data-ttu-id="a5979-106">In genere, le aziende si basano su metodi di creazione dell'immagine per effettuare il provisioning dei dispositivi agli utenti e, per gestirli, usano System Center Configuration Manager (SCCM) o Criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="a5979-106">Organizations typically rely on imaging methods to provision devices to users and generally use System Center Configuration Manager (SCCM) or Group Policy to manage them.</span></span>


<span data-ttu-id="a5979-107">Dopo aver connesso i dispositivi ad Azure Active Directory (Azure AD), l'aggiunta a un dominio di Windows 10 offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a5979-107">Domain join in Windows 10 provides you with the following benefits after you connect devices to Azure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="a5979-108">Accesso Single Sign-On (SSO) alle risorse di Azure AD da qualsiasi posizione.</span><span class="sxs-lookup"><span data-stu-id="a5979-108">Single sign-on (SSO) to Azure AD resources from anywhere</span></span>
* <span data-ttu-id="a5979-109">Accesso alla sezione aziendale di Windows Store usando account aziendali o dell'istituto di istruzione, non è necessario un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a5979-109">Access to the enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="a5979-110">Roaming delle impostazioni utente tra dispositivi conforme ai criteri dell'organizzazione usando account aziendali o dell'istituto di istruzione, non è necessario un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a5979-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="a5979-111">Autenticazione avanzata e pratico accesso all'account aziendale o dell'istituto di istruzione con Windows Hello for Business e Windows Hello</span><span class="sxs-lookup"><span data-stu-id="a5979-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="a5979-112">Possibilità di limitare l'accesso solo ai dispositivi conformi alle impostazioni di Criteri di gruppo dei dispositivi aziendali.</span><span class="sxs-lookup"><span data-stu-id="a5979-112">Ability to restrict access only to devices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5979-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a5979-113">Prerequisites</span></span>
<span data-ttu-id="a5979-114">Aggiunta a un dominio continua a essere utile.</span><span class="sxs-lookup"><span data-stu-id="a5979-114">Domain join continues to be useful.</span></span> <span data-ttu-id="a5979-115">Tuttavia, per poter sfruttare i vantaggi offerti da Azure AD per l'accesso SSO, il roaming delle impostazioni e l'accesso a Windows Store con account aziendali o dell'istituto di istruzione, è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="a5979-115">However, to get the Azure AD benefits of SSO, roaming of settings with work or school accounts, and access to Windows Store with work or school accounts, you will need the following:</span></span>

* <span data-ttu-id="a5979-116">Sottoscrizione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5979-116">Azure AD subscription</span></span>
* <span data-ttu-id="a5979-117">Azure AD Connect per estendere la directory locale ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5979-117">Azure AD Connect to extend the on-premises directory to Azure AD</span></span>
* <span data-ttu-id="a5979-118">Criteri impostati per connettere dispositivi aggiunti a un dominio ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5979-118">Policy that's set to connect domain-joined devices to Azure AD</span></span>
* <span data-ttu-id="a5979-119">Build di Windows 10 (build 10551 o successiva) per i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="a5979-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="a5979-120">Per abilitare Windows Hello for Business e Windows Hello è anche necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="a5979-120">To enable Windows Hello for Business and Windows Hello, you will also need the following:</span></span>

- <span data-ttu-id="a5979-121">**Infrastruttura a chiave pubblica (PKI)** per il rilascio di certificati utente.</span><span class="sxs-lookup"><span data-stu-id="a5979-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="a5979-122">**System Center Configuration Manager Current Branch**: è necessario installare la versione 1606 o successiva.</span><span class="sxs-lookup"><span data-stu-id="a5979-122">**System Center Configuration Manager Current Branch** - You need to install version 1606 or better.</span></span>  
<span data-ttu-id="a5979-123">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="a5979-123">For more information, see:</span></span> 
    - [<span data-ttu-id="a5979-124">Documentazione per System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="a5979-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="a5979-125">Blog del team di System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="a5979-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="a5979-126">Impostazioni di Windows Hello for Business in System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="a5979-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="a5979-127">In alternativa alla distribuzione di un'infrastruttura PKI, è possibile soddisfare il requisito seguente:</span><span class="sxs-lookup"><span data-stu-id="a5979-127">As an alternative to the PKI deployment requirement, you can do the following:</span></span>

* <span data-ttu-id="a5979-128">Disporre di alcuni controller di dominio con Servizi di dominio Active Directory di Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="a5979-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="a5979-129">Per abilitare l'accesso condizionale, è possibile creare impostazioni di Criteri di gruppo che consentano l'accesso a dispositivi aggiunti al dominio senza distribuzioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="a5979-129">To enable conditional access, you can create Group Policy settings that allow access to domain-joined devices with no additional deployments.</span></span> <span data-ttu-id="a5979-130">Per gestire il controllo di accesso in base alla conformità dei dispositivi, è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="a5979-130">To manage access control based on compliance of the device, you will need the following:</span></span>

* <span data-ttu-id="a5979-131">System Center Configuration Manager Current Branch (1606 o versione successiva) per scenari Windows Hello for Business</span><span class="sxs-lookup"><span data-stu-id="a5979-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="a5979-132">Istruzioni per la distribuzione</span><span class="sxs-lookup"><span data-stu-id="a5979-132">Deployment instructions</span></span>

<span data-ttu-id="a5979-133">Per eseguire la distribuzione, seguire la procedura indicata in [Come configurare la registrazione automatica dei dispositivi di dominio Windows con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="a5979-133">To deploy, follow the steps listed in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="a5979-134">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="a5979-134">Next step</span></span>
* [<span data-ttu-id="a5979-135">Windows 10 per le aziende: modalità d'uso dei dispositivi di lavoro</span><span class="sxs-lookup"><span data-stu-id="a5979-135">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="a5979-136">Estensione delle funzionalità del cloud ai dispositivi Windows 10 tramite Aggiunta ad Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5979-136">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="a5979-137">Scenari di utilizzo per Aggiunta ad Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5979-137">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="a5979-138">Connettere dispositivi appartenenti a un dominio ad Azure AD per usufruire di Windows 10</span><span class="sxs-lookup"><span data-stu-id="a5979-138">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="a5979-139">Configurare Aggiunta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5979-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

