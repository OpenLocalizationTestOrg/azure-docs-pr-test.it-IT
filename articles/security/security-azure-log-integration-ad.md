---
title: Integrazione di Log con i log di controllo di Azure Active Directory aaaAzure | Documenti Microsoft
description: Informazioni su come tooinstall hello servizio di integrazione di Log di Azure e integrare i registri dai log di controllo di Azure
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
ms.openlocfilehash: 3ee8fa3b8b5e9bd33202e57ed5327cd8d3127f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="f0886-103">Integrare i log di controllo di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0886-103">Integrate Azure Active Directory audit logs</span></span>

<span data-ttu-id="f0886-104">Gli eventi di controllo di Azure Active Directory (Azure AD) aiutano i clienti a identificare le azioni con privilegi che si sono verificate in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f0886-104">Azure Active Directory (Azure AD) audit events help you identify privileged actions that occurred in Azure Active Directory.</span></span> <span data-ttu-id="f0886-105">È possibile visualizzare hello tipi di eventi che è possibile tenere traccia, è consigliabile consultare [eventi di report di controllo di Azure Active Directory](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span><span class="sxs-lookup"><span data-stu-id="f0886-105">You can see hello types of events that you can track by reviewing [Azure Active Directory audit report events](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f0886-106">Prima di eseguire i passaggi di hello in questo articolo, è necessario esaminare hello [iniziare](security-azure-log-integration-get-started.md) articolo e completare i passaggi hello.</span><span class="sxs-lookup"><span data-stu-id="f0886-106">Before you attempt hello steps in this article, you must review hello [Get started](security-azure-log-integration-get-started.md) article and complete hello steps there.</span></span>

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a><span data-ttu-id="f0886-107">Procedura toointegrate Azure Active directory log di controllo</span><span class="sxs-lookup"><span data-stu-id="f0886-107">Steps toointegrate Azure Active directory audit logs</span></span>

1. <span data-ttu-id="f0886-108">Aprire il prompt dei comandi di hello ed eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="f0886-108">Open hello command prompt and run this command:</span></span>

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. <span data-ttu-id="f0886-109">Eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="f0886-109">Run this command:</span></span> 
 
   ``azlog createazureid``

   <span data-ttu-id="f0886-110">Questo comando richiede le credenziali di accesso di Azure.</span><span class="sxs-lookup"><span data-stu-id="f0886-110">This command prompts you for your Azure login.</span></span> <span data-ttu-id="f0886-111">Hello comando crea quindi una Azure Active Directory principale del servizio nel tenant di Azure AD hello che ospitano hello le sottoscrizioni di Azure in cui hello utente connesso è un amministratore, coamministratore o un proprietario.</span><span class="sxs-lookup"><span data-stu-id="f0886-111">hello command then creates an Azure Active Directory service principal in hello Azure AD tenants that host hello Azure subscriptions in which hello logged-in user is an administrator, a co-administrator, or an owner.</span></span> <span data-ttu-id="f0886-112">comando Hello avrà esito negativo se l'utente connesso di hello è solo un utente guest nel tenant di Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="f0886-112">hello command will fail if hello logged-in user is only a guest user in hello Azure AD tenant.</span></span> <span data-ttu-id="f0886-113">TooAzure l'autenticazione viene eseguita mediante Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0886-113">Authentication tooAzure is done through Azure AD.</span></span> <span data-ttu-id="f0886-114">Creazione di un'entità servizio per l'integrazione di Log di Azure crea hello identità di Azure AD che ha accesso tooread dalle sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="f0886-114">Creating a service principal for Azure Log Integration creates hello Azure AD identity that is given access tooread from Azure subscriptions.</span></span>

3. <span data-ttu-id="f0886-115">Comando che segue hello esecuzione tooprovide l'ID del tenant.</span><span class="sxs-lookup"><span data-stu-id="f0886-115">Run hello following command tooprovide your tenant ID.</span></span> <span data-ttu-id="f0886-116">È necessario membro toobe del comando di hello tenant admin ruolo toorun hello.</span><span class="sxs-lookup"><span data-stu-id="f0886-116">You need toobe member of hello tenant admin role toorun hello command.</span></span>

   ``Azlog.exe authorizedirectoryreader tenantId``

   <span data-ttu-id="f0886-117">Esempio:</span><span class="sxs-lookup"><span data-stu-id="f0886-117">Example:</span></span>

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. <span data-ttu-id="f0886-118">Controllare hello seguente tooconfirm cartelle che hello Azure Active Directory i JSON file di registro viene creato in essi contenuti:</span><span class="sxs-lookup"><span data-stu-id="f0886-118">Check hello following folders tooconfirm that hello Azure Active Directory audit log JSON files are created in them:</span></span>

   * <span data-ttu-id="f0886-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span><span class="sxs-lookup"><span data-stu-id="f0886-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span></span>
   * <span data-ttu-id="f0886-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span><span class="sxs-lookup"><span data-stu-id="f0886-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span></span>

<span data-ttu-id="f0886-121">Hello video seguente illustra i passaggi di hello illustrati in questo articolo:</span><span class="sxs-lookup"><span data-stu-id="f0886-121">hello following video demonstrates hello steps covered in this article:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> <span data-ttu-id="f0886-122">Per istruzioni dettagliate su come rendere le informazioni di hello nei file JSON hello le informazioni di sicurezza e un sistema (SIEM) di gestione degli eventi, contattare il fornitore SIEM.</span><span class="sxs-lookup"><span data-stu-id="f0886-122">For specific instructions on bringing hello information in hello JSON files into your security information and event management (SIEM) system, contact your SIEM vendor.</span></span>

<span data-ttu-id="f0886-123">Assistenza della community è disponibile tramite hello [Forum MSDN di Azure Log integrazione](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span><span class="sxs-lookup"><span data-stu-id="f0886-123">Community assistance is available through hello [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="f0886-124">Questo forum consente agli utenti in hello Azure Log integrazione community toosupport reciprocamente con domande, le risposte, suggerimenti e consigli.</span><span class="sxs-lookup"><span data-stu-id="f0886-124">This forum enables people in hello Azure Log Integration community toosupport each other with questions, answers, tips, and tricks.</span></span> <span data-ttu-id="f0886-125">Inoltre, il team di integrazione di Azure Log hello questo forum consente di monitorare e aiuta ogni volta che è possibile.</span><span class="sxs-lookup"><span data-stu-id="f0886-125">In addition, hello Azure Log Integration team monitors this forum and helps whenever it can.</span></span>

<span data-ttu-id="f0886-126">Si può anche aprire un [richiesta di supporto](../azure-supportability/how-to-create-azure-support-request.md).</span><span class="sxs-lookup"><span data-stu-id="f0886-126">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="f0886-127">Selezionare **Log integrazione** come servizio hello per il quale si richiede supporto.</span><span class="sxs-lookup"><span data-stu-id="f0886-127">Select **Log Integration** as hello service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0886-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f0886-128">Next steps</span></span>
<span data-ttu-id="f0886-129">toolearn più informazioni sull'integrazione di Log di Azure, vedere:</span><span class="sxs-lookup"><span data-stu-id="f0886-129">toolearn more about Azure Log Integration, see:</span></span>

* <span data-ttu-id="f0886-130">[Microsoft Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) (Integrazione log di Microsoft Azure): pagina di Area download con informazioni dettagliate, requisiti di sistema e istruzioni di installazione per l'integrazione dei log di Azure.</span><span class="sxs-lookup"><span data-stu-id="f0886-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324): This Download Center page gives details, system requirements, and installation instructions for Azure Log Integration.</span></span>
* <span data-ttu-id="f0886-131">[Introduzione tooAzure Log integrazione](security-azure-log-integration-overview.md): questo articolo illustra tooAzure integrazione di Log, le funzionalità chiave e il funzionamento.</span><span class="sxs-lookup"><span data-stu-id="f0886-131">[Introduction tooAzure Log Integration](security-azure-log-integration-overview.md): This article introduces you tooAzure Log Integration, its key capabilities, and how it works.</span></span>
* <span data-ttu-id="f0886-132">[Passaggi di configurazione di partner](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): questo post di blog viene illustrato come tooconfigure toowork di integrazione di Log di Azure con soluzioni Splunk, HP ArcSight e IBM QRadar di partner.</span><span class="sxs-lookup"><span data-stu-id="f0886-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): This blog post shows you how tooconfigure Azure Log Integration toowork with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span>
* <span data-ttu-id="f0886-133">[Domande frequenti sull'integrazione dei log di Azure](security-azure-log-integration-faq.md): questo articolo contiene le risponde alle domande sull'integrazione dei log di Azure.</span><span class="sxs-lookup"><span data-stu-id="f0886-133">[Azure Log Integration FAQ](security-azure-log-integration-faq.md): This article answers questions about Azure Log Integration.</span></span>
* <span data-ttu-id="f0886-134">[Gli avvisi del Centro sicurezza di integrazione con l'integrazione di Azure Log](../security-center/security-center-integrating-alerts-with-log-integration.md): questo articolo illustra come centro di sicurezza toosync avvisi, insieme agli eventi di sicurezza di macchina virtuale raccolti da diagnostica di Azure e i log di controllo di Azure, con analitica il log o Soluzione SIEM.</span><span class="sxs-lookup"><span data-stu-id="f0886-134">[Integrating Security Center alerts with Azure Log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md): This article shows you how toosync Security Center alerts, along with virtual machine security events collected by Azure Diagnostics and Azure audit logs, with your log analytics or SIEM solution.</span></span>
* <span data-ttu-id="f0886-135">[Registri di verifica delle nuove funzionalità per la diagnostica di Azure e Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): questo post di blog introduce i log di controllo tooAzure e altre funzionalità che consentono di ottenere informazioni approfondite operazioni hello delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f0886-135">[New features for Azure Diagnostics and Azure audit logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): This blog post introduces you tooAzure audit logs and other features that help you gain insights into hello operations of your Azure resources.</span></span>
