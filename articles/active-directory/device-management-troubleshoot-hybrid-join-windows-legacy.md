---
title: ibrida aaaTroubleshooting Azure Active Directory aggiunti dispositivi di livello inferiore | Documenti Microsoft
description: "Risoluzione dei problemi relativi a dispositivi di livello inferiore aggiunti all'identità ibrida di Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: edd56b89579fac6b427732902284ad9c568b87b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a><span data-ttu-id="a4d62-103">Risoluzione dei problemi relativi a dispositivi di livello inferiore aggiunti all'identità ibrida di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4d62-103">Troubleshooting hybrid Azure Active Directory joined down-level devices</span></span> 

<span data-ttu-id="a4d62-104">In questo argomento è applicabile toohello solo i dispositivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4d62-104">This topic is applicable only toohello following devices:</span></span> 

- <span data-ttu-id="a4d62-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="a4d62-105">Windows 7</span></span> 
- <span data-ttu-id="a4d62-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="a4d62-106">Windows 8.1</span></span> 
- <span data-ttu-id="a4d62-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="a4d62-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="a4d62-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="a4d62-108">Windows Server 2012</span></span> 
- <span data-ttu-id="a4d62-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="a4d62-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="a4d62-110">Per Windows 10 o Windows Server 2016, vedere [Risoluzione dei problemi relativi a dispositivi Windows 10 e Windows Server 2016 aggiunti all'identità ibrida di Azure Active Directory](device-management-troubleshoot-hybrid-join-windows-current.md).</span><span class="sxs-lookup"><span data-stu-id="a4d62-110">For Windows 10 or Windows Server 2016, see [Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices](device-management-troubleshoot-hybrid-join-windows-current.md).</span></span>

<span data-ttu-id="a4d62-111">In questo argomento si presuppone che sia [Configurazione ibrida di Azure Active Directory i dispositivi appartenenti](device-management-hybrid-azuread-joined-devices-setup.md) hello toosupport seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="a4d62-111">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello following scenarios:</span></span>

- <span data-ttu-id="a4d62-112">Accesso condizionale basato su dispositivo</span><span class="sxs-lookup"><span data-stu-id="a4d62-112">Device-based conditional access</span></span>

- [<span data-ttu-id="a4d62-113">Roaming aziendale delle impostazioni</span><span class="sxs-lookup"><span data-stu-id="a4d62-113">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- <span data-ttu-id="a4d62-114">[Windows Hello for Business](active-directory-azureadjoin-passport-deployment.md) (Configurare Windows Hello for Business)</span><span class="sxs-lookup"><span data-stu-id="a4d62-114">[Windows Hello for Business](active-directory-azureadjoin-passport-deployment.md)</span></span> 





<span data-ttu-id="a4d62-115">In questo argomento fornisce informazioni aggiuntive su come tooresolve potenziali problemi di risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="a4d62-115">This topic provides you with troubleshooting guidance on how tooresolve potential issues.</span></span>  

<span data-ttu-id="a4d62-116">**Informazioni utili:**</span><span class="sxs-lookup"><span data-stu-id="a4d62-116">**What you should know:**</span></span> 

- <span data-ttu-id="a4d62-117">numero massimo di Hello di dispositivi per utente è incentrato sui dispositivi.</span><span class="sxs-lookup"><span data-stu-id="a4d62-117">hello maximum number of devices per user is device-centric.</span></span> <span data-ttu-id="a4d62-118">Ad esempio, se *jdoe* e *jharnett* tooa accesso dispositivo, una registrazione separati (DeviceID) viene creata per ognuno di essi in hello **utente** scheda informazioni.</span><span class="sxs-lookup"><span data-stu-id="a4d62-118">For example, if *jdoe* and *jharnett* sign-in tooa device, a separate registration (DeviceID) is created for each of them in hello **USER** info tab.</span></span>  

- <span data-ttu-id="a4d62-119">Hello registrazione iniziale / unione dei dispositivi è tooperform configurato un tentativo di accesso o blocco / sblocco.</span><span class="sxs-lookup"><span data-stu-id="a4d62-119">hello initial registration / join of devices is configured tooperform an attempt at either logon or lock / unlock.</span></span> <span data-ttu-id="a4d62-120">Potrebbero esserci 5 minuti di ritardo causati da un'attività dell'utilità di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="a4d62-120">There could be 5-minute delay triggered by a task scheduler task.</span></span> 

- <span data-ttu-id="a4d62-121">La reinstallazione del sistema operativo hello o un manuale di annullare la registrazione e registrare nuovamente possibile creare una nuova registrazione in Azure AD e hello di risultati in più voci nella scheda informazioni utente di hello nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4d62-121">A reinstall of hello operating system or a manual unregister and re-register may create a new registration on Azure AD and results in multiple entries under hello USER info tab in hello Azure portal.</span></span> 


## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="a4d62-122">Passaggio 1: Recuperare lo stato della registrazione hello</span><span class="sxs-lookup"><span data-stu-id="a4d62-122">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="a4d62-123">**stato della registrazione tooverify hello:**</span><span class="sxs-lookup"><span data-stu-id="a4d62-123">**tooverify hello registration status:**</span></span>  

1. <span data-ttu-id="a4d62-124">Hello Apri prompt dei comandi come amministratore</span><span class="sxs-lookup"><span data-stu-id="a4d62-124">Open hello command prompt as an administrator</span></span> 

2. <span data-ttu-id="a4d62-125">Digitare `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`.</span><span class="sxs-lookup"><span data-stu-id="a4d62-125">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="a4d62-126">Questo comando Visualizza una finestra di dialogo che fornisce le informazioni più dettagliate sullo stato di join di hello.</span><span class="sxs-lookup"><span data-stu-id="a4d62-126">This command displays a dialog box that provides you with more details about hello join status.</span></span>

![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-hybrid-azure-ad-join-status"></a><span data-ttu-id="a4d62-128">Passaggio 2: Valutare lo stato di join hello ibrida Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4d62-128">Step 2: Evaluate hello hybrid Azure AD join status</span></span> 

<span data-ttu-id="a4d62-129">Se l'aggiunta ad Azure AD ibrido hello non ha esito positivo, la finestra di dialogo hello fornisce dettagli sul problema hello che si è verificato.</span><span class="sxs-lookup"><span data-stu-id="a4d62-129">If hello hybrid Azure AD join was not successful, hello dialog box provides you with details about hello issue that has occurred.</span></span>

<span data-ttu-id="a4d62-130">**Hello i problemi più comuni sono:**</span><span class="sxs-lookup"><span data-stu-id="a4d62-130">**hello most common issues are:**</span></span>

- <span data-ttu-id="a4d62-131">Una configurazione errata di AD FS o Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4d62-131">A misconfigured AD FS or Azure AD</span></span>

    ![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="a4d62-133">Non si è connessi come utente di dominio</span><span class="sxs-lookup"><span data-stu-id="a4d62-133">You are not signed on as a domain user</span></span>

    ![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="a4d62-135">È stata raggiunta una quota</span><span class="sxs-lookup"><span data-stu-id="a4d62-135">A quota has been reached</span></span>

    ![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="a4d62-137">servizio Hello non risponde</span><span class="sxs-lookup"><span data-stu-id="a4d62-137">hello service is not responding</span></span> 

    ![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="a4d62-139">È inoltre possibile trovare informazioni sullo stato hello nel registro eventi di hello in **all'area di lavoro di Log\Microsoft servizi e applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a4d62-139">You can also find hello status information in hello event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="a4d62-140">**le cause più comuni di un join di Azure AD ibrido Hello sono:**</span><span class="sxs-lookup"><span data-stu-id="a4d62-140">**hello most common causes for a failed hybrid Azure AD join are:**</span></span> 

- <span data-ttu-id="a4d62-141">Il computer non si trova nella rete interna dell'organizzazione hello o una connessione VPN senza connessione tooan locale controller di dominio Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4d62-141">Your computer is not on hello organization’s internal network or a VPN without connection tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="a4d62-142">Si è connessi in computer tooyour con un account computer locale.</span><span class="sxs-lookup"><span data-stu-id="a4d62-142">You are logged on tooyour computer with a local computer account.</span></span> 

- <span data-ttu-id="a4d62-143">Problemi di configurazione del servizio:</span><span class="sxs-lookup"><span data-stu-id="a4d62-143">Service configuration issues:</span></span> 

  - <span data-ttu-id="a4d62-144">Hello server federativo è stato configurato toosupport **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="a4d62-144">hello federation server has been configured toosupport **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="a4d62-145">È presente alcun oggetto di punto di connessione del servizio che fa riferimento il nome di dominio verificato tooyour in Azure Active Directory nella foresta Active Directory hello cui appartiene il computer di hello.</span><span class="sxs-lookup"><span data-stu-id="a4d62-145">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to.</span></span>

  - <span data-ttu-id="a4d62-146">Un utente ha raggiunto il limite di hello dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="a4d62-146">A user has reached hello limit of devices.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a4d62-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a4d62-147">Next steps</span></span>

<span data-ttu-id="a4d62-148">Per domande, vedere hello [domande frequenti sulla gestione dei dispositivi](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="a4d62-148">For questions, see hello [device management FAQ](device-management-faq.md)</span></span>  
