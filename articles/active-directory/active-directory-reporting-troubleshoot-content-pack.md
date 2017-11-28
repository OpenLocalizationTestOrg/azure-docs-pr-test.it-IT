---
title: "Risoluzione dei problemi relativi ai pacchetti di contenuto dei log attività di Azure Active Directory | Microsoft Docs"
description: "Fornisce un elenco di messaggi di errore di hello attività di Azure Active Directory contenuto pack e i passaggi toofix li."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 325de65ff1572a2f8f8319c0a52350bda03af3de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a><span data-ttu-id="3b577-103">Risoluzione dei problemi relativi ai pacchetti di contenuto dei log attività di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3b577-103">Troubleshooting Azure Active Directory Activity logs content pack errors</span></span> 


<span data-ttu-id="3b577-104">Quando si lavora con hello pacchetto di contenuto di Power BI per l'anteprima di Azure Active Directory, è possibile che si verifichino hello gli errori seguenti:</span><span class="sxs-lookup"><span data-stu-id="3b577-104">When working with hello Power BI Content Pack for Azure Active Directory Preview, it is possible that you run into hello following errors:</span></span> 

- [<span data-ttu-id="3b577-105">Aggiornamento non riuscito</span><span class="sxs-lookup"><span data-stu-id="3b577-105">Refresh failed</span></span>](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [<span data-ttu-id="3b577-106">Credenziali dell'origine dati tooupdate non riuscita</span><span class="sxs-lookup"><span data-stu-id="3b577-106">Failed tooupdate data source credentials</span></span>](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [<span data-ttu-id="3b577-107">L'importazione dei dati richiede troppo tempo</span><span class="sxs-lookup"><span data-stu-id="3b577-107">Importing of data is taking too long</span></span>](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
<span data-ttu-id="3b577-108">In questo argomento vengono fornite informazioni sulle possibili cause di hello e come toofix questi errori.</span><span class="sxs-lookup"><span data-stu-id="3b577-108">This topic provides you with information about hello possible causes and how toofix these errors.</span></span>
 
## <a name="refresh-failed"></a><span data-ttu-id="3b577-109">Aggiornamento non riuscito</span><span class="sxs-lookup"><span data-stu-id="3b577-109">Refresh failed</span></span> 
 
<span data-ttu-id="3b577-110">**La modalità in cui viene esposto l'errore**: messaggio di posta elettronica da Power BI o stato di errore nella cronologia dell'aggiornamento hello.</span><span class="sxs-lookup"><span data-stu-id="3b577-110">**How this error is surfaced**: Email from Power BI or failed status in hello refresh history.</span></span> 


| <span data-ttu-id="3b577-111">Causa</span><span class="sxs-lookup"><span data-stu-id="3b577-111">Cause</span></span> | <span data-ttu-id="3b577-112">Come toofix</span><span class="sxs-lookup"><span data-stu-id="3b577-112">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="3b577-113">Aggiornare l'errore possono verificarsi errori quando le credenziali di hello di utenti hello connessione toohello pacchetto di contenuto sono state reimpostare ma non aggiornate nelle impostazioni di connessione hello di hello del pacchetto di contenuto hello.</span><span class="sxs-lookup"><span data-stu-id="3b577-113">Refresh failure errors can be caused when hello credentials of hello users connecting toohello content pack have been reset but not updated in hello connection settings of hello of hello content pack.</span></span> | <span data-ttu-id="3b577-114">In Power BI, è possibile individuare hello set di dati corrispondente toohello dashboard log attività di Azure Active Directory (registri dell'attività di Azure Active Directory), scegliere la pianificazione dell'aggiornamento e quindi immettere le credenziali di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b577-114">In Power BI, locate hello dataset corresponding toohello Azure Active Directory Activity logs dashboard (Azure Active Directory Activity logs), choose schedule refresh, and then enter your Azure AD credentials.</span></span> |
| <span data-ttu-id="3b577-115">Un aggiornamento può non riuscire a causa di problemi di toodata hello sottostante pacchetto di contenuto.</span><span class="sxs-lookup"><span data-stu-id="3b577-115">A refresh can fail due toodata issues in hello underlying content pack.</span></span> | <span data-ttu-id="3b577-116">Inviare un ticket di supporto.</span><span class="sxs-lookup"><span data-stu-id="3b577-116">File a support ticket.</span></span> <span data-ttu-id="3b577-117">Per ulteriori informazioni, vedere [come tooget il supporto per Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="3b577-117">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 
 
## <a name="failed-tooupdate-data-source-credentials"></a><span data-ttu-id="3b577-118">Credenziali dell'origine dati tooupdate non riuscita</span><span class="sxs-lookup"><span data-stu-id="3b577-118">Failed tooupdate data source credentials</span></span> 
 
<span data-ttu-id="3b577-119">**La modalità in cui viene esposto l'errore**: In Power BI, quando ci si connette toohello pacchetto di contenuto (anteprima) log attività di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3b577-119">**How this error is surfaced**: In Power BI, when you are connecting toohello Azure Active Directory Activity logs (preview) content pack.</span></span> 

| <span data-ttu-id="3b577-120">Causa</span><span class="sxs-lookup"><span data-stu-id="3b577-120">Cause</span></span> | <span data-ttu-id="3b577-121">Come toofix</span><span class="sxs-lookup"><span data-stu-id="3b577-121">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="3b577-122">utente che si connette Hello è né un amministratore globale né un lettore di sicurezza o un amministratore di protezione.</span><span class="sxs-lookup"><span data-stu-id="3b577-122">hello connecting user is neither a global admin nor a security reader or a security admin.</span></span> | <span data-ttu-id="3b577-123">Utilizzare un account che è un amministratore globale o un lettore di protezione o una protezione admin tooaccess hello pacchetti di contenuto.</span><span class="sxs-lookup"><span data-stu-id="3b577-123">Use an account that is either a global admin or a security reader or a security admin tooaccess hello content packs.</span></span> |
| <span data-ttu-id="3b577-124">Il tenant non è un tenant Premium o non include almeno un utente con un file di licenza Premium.</span><span class="sxs-lookup"><span data-stu-id="3b577-124">Your tenant is not a Premium tenant or doesn't have at least one user with Premium license File.</span></span> | <span data-ttu-id="3b577-125">Inviare un ticket di supporto.</span><span class="sxs-lookup"><span data-stu-id="3b577-125">File a support ticket.</span></span> <span data-ttu-id="3b577-126">Per ulteriori informazioni, vedere [come tooget il supporto per Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="3b577-126">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 

 

## <a name="importing-of-data-is-taking-too-long"></a><span data-ttu-id="3b577-127">L'importazione dei dati richiede troppo tempo</span><span class="sxs-lookup"><span data-stu-id="3b577-127">Importing of data is taking too long</span></span> 
 
<span data-ttu-id="3b577-128">**La modalità in cui viene esposto l'errore**: In Power BI, dopo avere connesso il pacchetto di contenuto, processo di importazione dati hello inizia tooprepare dashboard per il log attività di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3b577-128">**How this error is surfaced**: In Power BI, once you have connected your content pack, hello data import process starts tooprepare your dashboard for Azure Active Directory Activity log.</span></span> <span data-ttu-id="3b577-129">Viene visualizzato il messaggio hello: "*l'importazione di dati...* "</span><span class="sxs-lookup"><span data-stu-id="3b577-129">You see hello message: “*Importing data...*”</span></span>  

| <span data-ttu-id="3b577-130">Causa</span><span class="sxs-lookup"><span data-stu-id="3b577-130">Cause</span></span> | <span data-ttu-id="3b577-131">Come toofix</span><span class="sxs-lookup"><span data-stu-id="3b577-131">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="3b577-132">A seconda delle dimensioni di hello del tenant, questo passaggio potrebbe richiedere da alcuni minuti too30 minuti.</span><span class="sxs-lookup"><span data-stu-id="3b577-132">Depending on hello size of your tenant, this step could take anywhere from a few mins too30 minutes.</span></span> | <span data-ttu-id="3b577-133">Attendere.</span><span class="sxs-lookup"><span data-stu-id="3b577-133">Just be patient.</span></span> <span data-ttu-id="3b577-134">Se il messaggio hello non cambia tooshowing dashboard entro un'ora, inviare un ticket di supporto.</span><span class="sxs-lookup"><span data-stu-id="3b577-134">If hello message does not change tooshowing your dashboard within an hour, please file a support ticket.</span></span> <span data-ttu-id="3b577-135">Per ulteriori informazioni, vedere [come tooget il supporto per Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="3b577-135">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|

## <a name="next-steps"></a><span data-ttu-id="3b577-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3b577-136">Next steps</span></span>

<span data-ttu-id="3b577-137">Fare clic su hello tooinstall pacchetto di contenuto Power BI per Azure Active Directory anteprima [qui](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span><span class="sxs-lookup"><span data-stu-id="3b577-137">tooinstall hello Power BI Content Pack for Azure Active Directory Preview, click [here](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span></span>


