---
title: "Risoluzione dei problemi relativi ai pacchetti di contenuto dei log attività di Azure Active Directory | Microsoft Docs"
description: "Offre un elenco dei messaggi di errore del pacchetto di contenuto delle attività di Azure Active Directory e i passaggi per risolvere il problema."
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
ms.openlocfilehash: c880e9eb6d48bd1e38075fbd867d3906ec67b547
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a><span data-ttu-id="65bec-103">Risoluzione dei problemi relativi ai pacchetti di contenuto dei log attività di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65bec-103">Troubleshooting Azure Active Directory Activity logs content pack errors</span></span> 


<span data-ttu-id="65bec-104">Quando si usa il pacchetto di contenuto di Power BI per l'anteprima di Azure Active Directory, è possibile che si verifichino gli errori seguenti:</span><span class="sxs-lookup"><span data-stu-id="65bec-104">When working with the Power BI Content Pack for Azure Active Directory Preview, it is possible that you run into the following errors:</span></span> 

- [<span data-ttu-id="65bec-105">Aggiornamento non riuscito</span><span class="sxs-lookup"><span data-stu-id="65bec-105">Refresh failed</span></span>](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [<span data-ttu-id="65bec-106">L'aggiornamento delle credenziali dell'origine dati non è riuscito</span><span class="sxs-lookup"><span data-stu-id="65bec-106">Failed to update data source credentials</span></span>](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [<span data-ttu-id="65bec-107">L'importazione dei dati richiede troppo tempo</span><span class="sxs-lookup"><span data-stu-id="65bec-107">Importing of data is taking too long</span></span>](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
<span data-ttu-id="65bec-108">Questo argomento offre informazioni sulle possibili cause e su come risolvere questi errori.</span><span class="sxs-lookup"><span data-stu-id="65bec-108">This topic provides you with information about the possible causes and how to fix these errors.</span></span>
 
## <a name="refresh-failed"></a><span data-ttu-id="65bec-109">Aggiornamento non riuscito</span><span class="sxs-lookup"><span data-stu-id="65bec-109">Refresh failed</span></span> 
 
<span data-ttu-id="65bec-110">**Modalità di esposizione dell'errore**: messaggio di posta elettronica inviato da Power BI o stato di errore nella cronologia aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="65bec-110">**How this error is surfaced**: Email from Power BI or failed status in the refresh history.</span></span> 


| <span data-ttu-id="65bec-111">Causa</span><span class="sxs-lookup"><span data-stu-id="65bec-111">Cause</span></span> | <span data-ttu-id="65bec-112">Modalità di correzione</span><span class="sxs-lookup"><span data-stu-id="65bec-112">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="65bec-113">Gli errori di aggiornamento non riuscito possono verificarsi quando le credenziali degli utenti che si connettono al pacchetto di contenuto sono state reimpostate ma non sono state aggiornate nelle impostazioni di connessione del pacchetto di contenuto.</span><span class="sxs-lookup"><span data-stu-id="65bec-113">Refresh failure errors can be caused when the credentials of the users connecting to the content pack have been reset but not updated in the connection settings of the of the content pack.</span></span> | <span data-ttu-id="65bec-114">Individuare in Power BI il set di dati corrispondente al dashboard dei log attività di Azure Active Directory (log attività di Azure Active Directory), scegliere Pianifica aggiornamento e quindi immettere le credenziali di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65bec-114">In Power BI, locate the dataset corresponding to the Azure Active Directory Activity logs dashboard (Azure Active Directory Activity logs), choose schedule refresh, and then enter your Azure AD credentials.</span></span> |
| <span data-ttu-id="65bec-115">Un aggiornamento può non riuscire a causa di problemi relativi ai dati nel pacchetto di contenuto sottostante.</span><span class="sxs-lookup"><span data-stu-id="65bec-115">A refresh can fail due to data issues in the underlying content pack.</span></span> | <span data-ttu-id="65bec-116">Inviare un ticket di supporto.</span><span class="sxs-lookup"><span data-stu-id="65bec-116">File a support ticket.</span></span> <span data-ttu-id="65bec-117">Per informazioni dettagliate, vedere [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md) (Come ottenere supporto per Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="65bec-117">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 
 
## <a name="failed-to-update-data-source-credentials"></a><span data-ttu-id="65bec-118">L'aggiornamento delle credenziali dell'origine dati non è riuscito</span><span class="sxs-lookup"><span data-stu-id="65bec-118">Failed to update data source credentials</span></span> 
 
<span data-ttu-id="65bec-119">**Modalità di esposizione dell'errore**: in Power BI durante la connessione al pacchetto di contenuto dei log attività di Azure Active Directory (anteprima).</span><span class="sxs-lookup"><span data-stu-id="65bec-119">**How this error is surfaced**: In Power BI, when you are connecting to the Azure Active Directory Activity logs (preview) content pack.</span></span> 

| <span data-ttu-id="65bec-120">Causa</span><span class="sxs-lookup"><span data-stu-id="65bec-120">Cause</span></span> | <span data-ttu-id="65bec-121">Modalità di correzione</span><span class="sxs-lookup"><span data-stu-id="65bec-121">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="65bec-122">L'utente che sta tentando di connettersi non è un amministratore globale, non dispone di un ruolo con autorizzazioni di lettura per la sicurezza né di amministratore della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="65bec-122">The connecting user is neither a global admin nor a security reader or a security admin.</span></span> | <span data-ttu-id="65bec-123">Per accedere ai pacchetti di contenuto, usare un account di amministratore globale, con autorizzazioni di lettura per la sicurezza o di amministratore della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="65bec-123">Use an account that is either a global admin or a security reader or a security admin to access the content packs.</span></span> |
| <span data-ttu-id="65bec-124">Il tenant non è un tenant Premium o non include almeno un utente con un file di licenza Premium.</span><span class="sxs-lookup"><span data-stu-id="65bec-124">Your tenant is not a Premium tenant or doesn't have at least one user with Premium license File.</span></span> | <span data-ttu-id="65bec-125">Inviare un ticket di supporto.</span><span class="sxs-lookup"><span data-stu-id="65bec-125">File a support ticket.</span></span> <span data-ttu-id="65bec-126">Per informazioni dettagliate, vedere [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md) (Come ottenere supporto per Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="65bec-126">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 

 

## <a name="importing-of-data-is-taking-too-long"></a><span data-ttu-id="65bec-127">L'importazione dei dati richiede troppo tempo</span><span class="sxs-lookup"><span data-stu-id="65bec-127">Importing of data is taking too long</span></span> 
 
<span data-ttu-id="65bec-128">**Modalità di esposizione dell'errore**: in Power BI dopo la connessione del pacchetto di contenuto viene avviato il processo di importazione dei dati per preparare il dashboard per il log attività di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="65bec-128">**How this error is surfaced**: In Power BI, once you have connected your content pack, the data import process starts to prepare your dashboard for Azure Active Directory Activity log.</span></span> <span data-ttu-id="65bec-129">Viene visualizzato il messaggio "*Importazione dei dati in corso...*"</span><span class="sxs-lookup"><span data-stu-id="65bec-129">You see the message: “*Importing data...*”</span></span>  

| <span data-ttu-id="65bec-130">Causa</span><span class="sxs-lookup"><span data-stu-id="65bec-130">Cause</span></span> | <span data-ttu-id="65bec-131">Modalità di correzione</span><span class="sxs-lookup"><span data-stu-id="65bec-131">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="65bec-132">A seconda delle dimensioni del tenant, questo passaggio può richiedere da alcuni minuti a 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="65bec-132">Depending on the size of your tenant, this step could take anywhere from a few mins to 30 minutes.</span></span> | <span data-ttu-id="65bec-133">Attendere.</span><span class="sxs-lookup"><span data-stu-id="65bec-133">Just be patient.</span></span> <span data-ttu-id="65bec-134">Se entro un'ora il messaggio non cambia e non viene visualizzato il dashboard, inviare un ticket di supporto.</span><span class="sxs-lookup"><span data-stu-id="65bec-134">If the message does not change to showing your dashboard within an hour, please file a support ticket.</span></span> <span data-ttu-id="65bec-135">Per informazioni dettagliate, vedere [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md) (Come ottenere supporto per Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="65bec-135">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|

## <a name="next-steps"></a><span data-ttu-id="65bec-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="65bec-136">Next steps</span></span>

<span data-ttu-id="65bec-137">Per installare il pacchetto di contenuto di Power BI per l'anteprima di Azure Active Directory, fare clic su [qui](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span><span class="sxs-lookup"><span data-stu-id="65bec-137">To install the Power BI Content Pack for Azure Active Directory Preview, click [here](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span></span>


