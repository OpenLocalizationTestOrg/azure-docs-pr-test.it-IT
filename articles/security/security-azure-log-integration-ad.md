---
title: Integrazione dei log di Azure con i log di controllo di Azure Active Directory | Microsoft Docs
description: Informazioni su come installare il servizio di integrazione dei log di Azure e integrare i log dai log di controllo di Azure
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/08/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 8a1295cc86057ed72940e774d0bd423d61142e31
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="0f21a-103">Integrare i log di controllo di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f21a-103">Integrate Azure Active Directory audit logs</span></span>

<span data-ttu-id="0f21a-104">Gli eventi di controllo di Azure Active Directory (Azure AD) aiutano i clienti a identificare le azioni con privilegi che si sono verificate in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0f21a-104">Azure Active Directory (Azure AD) audit events help you identify privileged actions that occurred in Azure Active Directory.</span></span> <span data-ttu-id="0f21a-105">I tipi di eventi di cui è possibile tenere traccia sono visibili esaminando gli [eventi dei report di controllo di Azure Active Directory](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span><span class="sxs-lookup"><span data-stu-id="0f21a-105">You can see the types of events that you can track by reviewing [Azure Active Directory audit report events](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0f21a-106">Prima di eseguire la procedura descritta in questo articolo, è necessario esaminare l'articolo [introduttivo](security-azure-log-integration-get-started.md) e completare la procedura in esso descritta.</span><span class="sxs-lookup"><span data-stu-id="0f21a-106">Before you attempt the steps in this article, you must review the [Get started](security-azure-log-integration-get-started.md) article and complete the steps there.</span></span>

## <a name="steps-to-integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="0f21a-107">Passaggi necessari per integrare i log di controllo di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f21a-107">Steps to integrate Azure Active directory audit logs</span></span>

1. <span data-ttu-id="0f21a-108">Aprire il prompt dei comandi ed eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="0f21a-108">Open the command prompt and run this command:</span></span>

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. <span data-ttu-id="0f21a-109">Eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="0f21a-109">Run this command:</span></span> 
 
   ``azlog createazureid``

   <span data-ttu-id="0f21a-110">Questo comando richiede le credenziali di accesso di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f21a-110">This command prompts you for your Azure login.</span></span> <span data-ttu-id="0f21a-111">Il comando crea quindi un'entità servizio di Azure Active Directory nei tenant di Azure AD che ospitano le sottoscrizioni di Azure in cui l'utente connesso è amministratore, coamministratore o proprietario.</span><span class="sxs-lookup"><span data-stu-id="0f21a-111">The command then creates an Azure Active Directory service principal in the Azure AD tenants that host the Azure subscriptions in which the logged-in user is an administrator, a co-administrator, or an owner.</span></span> <span data-ttu-id="0f21a-112">Se l'utente connesso è solo un utente guest nel tenant di Azure AD, il comando avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="0f21a-112">The command will fail if the logged-in user is only a guest user in the Azure AD tenant.</span></span> <span data-ttu-id="0f21a-113">L'autenticazione in Azure avviene tramite Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f21a-113">Authentication to Azure is done through Azure AD.</span></span> <span data-ttu-id="0f21a-114">La creazione di un'entità servizio per l'integrazione dei log di Azure crea l'identità di Azure AD a cui verrà consentito l'accesso in lettura dalle sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f21a-114">Creating a service principal for Azure Log Integration creates the Azure AD identity that is given access to read from Azure subscriptions.</span></span>

3. <span data-ttu-id="0f21a-115">Eseguire il comando seguente per fornire l'ID del tenant.</span><span class="sxs-lookup"><span data-stu-id="0f21a-115">Run the following command to provide your tenant ID.</span></span> <span data-ttu-id="0f21a-116">Per eseguire il comando è necessario essere membri del ruolo di amministratore tenant.</span><span class="sxs-lookup"><span data-stu-id="0f21a-116">You need to be member of the tenant admin role to run the command.</span></span>

   ``Azlog.exe authorizedirectoryreader tenantId``

   <span data-ttu-id="0f21a-117">Esempio:</span><span class="sxs-lookup"><span data-stu-id="0f21a-117">Example:</span></span>

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. <span data-ttu-id="0f21a-118">Verificare che siano stati creati i file JSON del log di controllo di Azure Active Directory nelle cartelle seguenti:</span><span class="sxs-lookup"><span data-stu-id="0f21a-118">Check the following folders to confirm that the Azure Active Directory audit log JSON files are created in them:</span></span>

   * <span data-ttu-id="0f21a-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span><span class="sxs-lookup"><span data-stu-id="0f21a-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span></span>
   * <span data-ttu-id="0f21a-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span><span class="sxs-lookup"><span data-stu-id="0f21a-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span></span>

<span data-ttu-id="0f21a-121">Il video seguente illustra i passaggi descritti in questo articolo:</span><span class="sxs-lookup"><span data-stu-id="0f21a-121">The following video demonstrates the steps covered in this article:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> <span data-ttu-id="0f21a-122">Per istruzioni specifiche su come includere le informazioni dei file JSON nel sistema di gestione delle informazioni e degli eventi di sicurezza (SIEM), contattare il fornitore SIEM.</span><span class="sxs-lookup"><span data-stu-id="0f21a-122">For specific instructions on bringing the information in the JSON files into your security information and event management (SIEM) system, contact your SIEM vendor.</span></span>

<span data-ttu-id="0f21a-123">L'assistenza della community è disponibile tramite il [forum MSDN di Integrazione log di Azure](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span><span class="sxs-lookup"><span data-stu-id="0f21a-123">Community assistance is available through the [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="0f21a-124">Questo forum consente ai membri della community di aiutarsi reciprocamente con domande, risposte, suggerimenti e trucchi.</span><span class="sxs-lookup"><span data-stu-id="0f21a-124">This forum enables people in the Azure Log Integration community to support each other with questions, answers, tips, and tricks.</span></span> <span data-ttu-id="0f21a-125">Inoltre, il team di integrazione dei log di Azure monitora questo forum e offre il suo contributo quando possibile.</span><span class="sxs-lookup"><span data-stu-id="0f21a-125">In addition, the Azure Log Integration team monitors this forum and helps whenever it can.</span></span>

<span data-ttu-id="0f21a-126">Si può anche aprire un [richiesta di supporto](../azure-supportability/how-to-create-azure-support-request.md).</span><span class="sxs-lookup"><span data-stu-id="0f21a-126">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="0f21a-127">Selezionare **Integrazione log** come servizio per cui richiedere il supporto.</span><span class="sxs-lookup"><span data-stu-id="0f21a-127">Select **Log Integration** as the service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f21a-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0f21a-128">Next steps</span></span>
<span data-ttu-id="0f21a-129">Per altre informazioni sull'integrazione dei log di Azure, vedere:</span><span class="sxs-lookup"><span data-stu-id="0f21a-129">To learn more about Azure Log Integration, see:</span></span>

* <span data-ttu-id="0f21a-130">[Microsoft Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) (Integrazione log di Microsoft Azure): pagina di Area download con informazioni dettagliate, requisiti di sistema e istruzioni di installazione per l'integrazione dei log di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f21a-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324): This Download Center page gives details, system requirements, and installation instructions for Azure Log Integration.</span></span>
* <span data-ttu-id="0f21a-131">[Introduzione all'integrazione dei log di Azure](security-azure-log-integration-overview.md): questo articolo presenta l'integrazione dei log di Azure, le funzionalità chiave e il funzionamento.</span><span class="sxs-lookup"><span data-stu-id="0f21a-131">[Introduction to Azure Log Integration](security-azure-log-integration-overview.md): This article introduces you to Azure Log Integration, its key capabilities, and how it works.</span></span>
* <span data-ttu-id="0f21a-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) (Passaggi per la configurazione dei partner): questo post di blog mostra come configurare l'integrazione dei log di Azure per lavorare con le soluzioni partner Splunk, HP ArcSight e IBM QRadar.</span><span class="sxs-lookup"><span data-stu-id="0f21a-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): This blog post shows you how to configure Azure Log Integration to work with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span>
* <span data-ttu-id="0f21a-133">[Domande frequenti sull'integrazione dei log di Azure](security-azure-log-integration-faq.md): questo articolo contiene le risponde alle domande sull'integrazione dei log di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f21a-133">[Azure Log Integration FAQ](security-azure-log-integration-faq.md): This article answers questions about Azure Log Integration.</span></span>
* <span data-ttu-id="0f21a-134">[Integrazione degli avvisi del Centro sicurezza con l'integrazione dei log di Azure](../security-center/security-center-integrating-alerts-with-log-integration.md): questo articolo mostra come sincronizzare gli avvisi del Centro sicurezza di Azure, insieme agli eventi di sicurezza delle macchine virtuali raccolti da Diagnostica di Azure e dai log di controllo di Azure, con la propria soluzione SIEM o di analisi dei log.</span><span class="sxs-lookup"><span data-stu-id="0f21a-134">[Integrating Security Center alerts with Azure Log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md): This article shows you how to sync Security Center alerts, along with virtual machine security events collected by Azure Diagnostics and Azure audit logs, with your log analytics or SIEM solution.</span></span>
* <span data-ttu-id="0f21a-135">[New features for Azure Diagnostics and Azure audit logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) (Nuove funzionalità per Diagnostica di Azure e i log di controllo di Azure): questo post di blog presenta i log di controllo di Azure e altre funzionalità che consentono di ottenere informazioni dettagliate sulle operazioni delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f21a-135">[New features for Azure Diagnostics and Azure audit logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): This blog post introduces you to Azure audit logs and other features that help you gain insights into the operations of your Azure resources.</span></span>
