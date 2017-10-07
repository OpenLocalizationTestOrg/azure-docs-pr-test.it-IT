---
title: Transparent Data Encryption nel Centro protezione Azure aaaEnable | Documenti Microsoft
description: Questo documento viene illustrato come tooimplement hello raccomandazione Centro sicurezza di Azure * * abilitare Transparent Data Encryption * *.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 94c6e9a1feddaa48faac6c835d416c4d131cd5c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a><span data-ttu-id="06bbd-103">Abilitare Transparent Data Encryption nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="06bbd-103">Enable Transparent Data Encryption in Azure Security Center</span></span>
<span data-ttu-id="06bbd-104">Il Centro sicurezza di Azure consiglia di abilitare Transparent Data Encryption (TDE) nel database SQL, se non è già abilitato.</span><span class="sxs-lookup"><span data-stu-id="06bbd-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span></span> <span data-ttu-id="06bbd-105">Transparent Data Encryption consente di proteggere i dati e consente di soddisfare i requisiti di conformità grazie alla crittografia del database, i backup associati e i file di log delle transazioni inattivi, senza richiedere modifiche tooyour applicazione.</span><span class="sxs-lookup"><span data-stu-id="06bbd-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes tooyour application.</span></span> <span data-ttu-id="06bbd-106">vedere più toolearn [Transparent Data Encryption con il Database di SQL Azure](https://msdn.microsoft.com/library/dn948096).</span><span class="sxs-lookup"><span data-stu-id="06bbd-106">toolearn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span></span>

<span data-ttu-id="06bbd-107">Questa indicazione si applica toohello solo servizio di SQL Azure non include SQL in esecuzione nelle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="06bbd-107">This recommendation applies toohello Azure SQL service only; doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="06bbd-108">Questo documento introduce servizio hello utilizzando un esempio di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="06bbd-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="06bbd-109">Questa non è una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="06bbd-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="06bbd-110">Implementare la raccomandazione hello</span><span class="sxs-lookup"><span data-stu-id="06bbd-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="06bbd-111">In hello **indicazioni** pannello seleziona **abilitare Transparent Data Encryption**.</span><span class="sxs-lookup"><span data-stu-id="06bbd-111">In hello **Recommendations** blade, select **Enable Transparent Data Encryption**.</span></span>
   <span data-ttu-id="06bbd-112">![Abilita Transparent Data Encryption][1]</span><span class="sxs-lookup"><span data-stu-id="06bbd-112">![Enable Transparent Data Encryption][1]</span></span>
2. <span data-ttu-id="06bbd-113">Verrà visualizzata hello **abilitare Transparent Data Encryption nel database SQL** blade.</span><span class="sxs-lookup"><span data-stu-id="06bbd-113">This opens hello **Enable Transparent Data Encryption on SQL databases** blade.</span></span> <span data-ttu-id="06bbd-114">Selezionare un tooenable di database SQL Transparent Data Encryption.</span><span class="sxs-lookup"><span data-stu-id="06bbd-114">Select a SQL database tooenable TDE on.</span></span>
   <span data-ttu-id="06bbd-115">![Selezionare database SQL tooenable TDE nel][2]</span><span class="sxs-lookup"><span data-stu-id="06bbd-115">![Select SQL DB tooenable TDE on][2]</span></span>
3. <span data-ttu-id="06bbd-116">In hello **crittografia dati trasparente** pannello seleziona **ON** sotto la crittografia dei dati e selezionare **salvare** nella barra multifunzione superiore hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="06bbd-116">On hello **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in hello top ribbon of hello blade.</span></span>
   <span data-ttu-id="06bbd-117">![Attivare la crittografia TDE][3]</span><span class="sxs-lookup"><span data-stu-id="06bbd-117">![Turn on TDE][3]</span></span>

   <span data-ttu-id="06bbd-118">Una volta TDE è abilitata nel hello selezionati database SQL, hello **lo stato di crittografia** cambierà troppo**Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="06bbd-118">Once TDE is enabled on hello selected SQL database, hello **Encryption status** will change too**Encrypted**.</span></span>    

   ![Stato della crittografia][4]

## <a name="see-also"></a><span data-ttu-id="06bbd-120">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="06bbd-120">See also</span></span>
<span data-ttu-id="06bbd-121">In questo articolo ha illustrato come tooimplement hello raccomandazione Centro sicurezza PC "Abilitazione di Transparent Data Encryption".</span><span class="sxs-lookup"><span data-stu-id="06bbd-121">This article showed you how tooimplement hello Security Center recommendation "Enable Transparent Data Encryption."</span></span> <span data-ttu-id="06bbd-122">toolearn ulteriori informazioni su TDE SQL, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="06bbd-122">toolearn more about SQL TDE, see hello following:</span></span>

* [<span data-ttu-id="06bbd-123">Transparent Data Encryption con il database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="06bbd-123">Transparent Data Encryption with Azure SQL Database</span></span>](https://msdn.microsoft.com/library/dn948096)
* [<span data-ttu-id="06bbd-124">Introduzione a Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="06bbd-124">Get started with Transparent Data Encryption (TDE)</span></span>](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

<span data-ttu-id="06bbd-125">toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="06bbd-125">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="06bbd-126">[L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="06bbd-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="06bbd-127">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="06bbd-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="06bbd-128">[Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) -informazioni su come toomonitor hello integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="06bbd-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="06bbd-129">[La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.</span><span class="sxs-lookup"><span data-stu-id="06bbd-129">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="06bbd-130">[Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) -informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.</span><span class="sxs-lookup"><span data-stu-id="06bbd-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="06bbd-131">[Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="06bbd-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="06bbd-132">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) -ottenere informazioni e notizie sicurezza di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="06bbd-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
