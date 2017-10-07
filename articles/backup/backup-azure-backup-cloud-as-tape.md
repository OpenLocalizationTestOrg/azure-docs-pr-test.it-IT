---
title: aaaUse Azure Backup tooreplace infrastruttura nastro | Documenti Microsoft
description: Informazioni su come Backup di Azure fornisce semantica simile a nastro che consente di toobackup e ripristinare i dati in Azure
services: backup
documentationcenter: 
author: trinadhk
manager: vijayts
editor: 
ms.assetid: 2e1bb67d-986c-4437-8056-3a63169b4214
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 1/10/2017
ms.author: saurse;trinadhk;markgal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4c5b095d95d39267c54b1eed9427bda09658bb94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-your-long-term-storage-from-tape-toohello-azure-cloud"></a><span data-ttu-id="8c308-103">Spostare lo spazio di archiviazione a lungo termine da nastro toohello cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="8c308-103">Move your long-term storage from tape toohello Azure cloud</span></span>
<span data-ttu-id="8c308-104">I clienti di Backup di Azure e System Center Data Protection Manager possono eseguire le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="8c308-104">Azure Backup and System Center Data Protection Manager customers can:</span></span>

* <span data-ttu-id="8c308-105">Eseguire il backup dei dati nelle pianificazioni che più adatto alle proprie esigenze organizzative hello.</span><span class="sxs-lookup"><span data-stu-id="8c308-105">Back up data in schedules which best suit hello organizational needs.</span></span>
* <span data-ttu-id="8c308-106">Dati di backup hello vengono conservati per periodi più lunghi</span><span class="sxs-lookup"><span data-stu-id="8c308-106">Retain hello backup data for longer periods</span></span>
* <span data-ttu-id="8c308-107">Includere Azure nelle strategie di conservazione dei dati a lungo termine, in alternativa al backup su nastro.</span><span class="sxs-lookup"><span data-stu-id="8c308-107">Make Azure a part of their long-term retention needs (instead of tape).</span></span>

<span data-ttu-id="8c308-108">Questo articolo illustra come abilitare i criteri di backup e di conservazione.</span><span class="sxs-lookup"><span data-stu-id="8c308-108">This article explains how customers can enable backup and retention policies.</span></span> <span data-ttu-id="8c308-109">I clienti che utilizzano i nastri tooaddress lungo-termine-conservarli deve ora disponibile un'alternativa potente e affidabile con disponibilità hello di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8c308-109">Customers who use tapes tooaddress their long-term-retention needs now have a powerful and viable alternative with hello availability of this feature.</span></span> <span data-ttu-id="8c308-110">Hello è attivata nella versione più recente di hello di hello Azure Backup (disponibile [qui](http://aka.ms/azurebackup_agent)).</span><span class="sxs-lookup"><span data-stu-id="8c308-110">hello feature is enabled in hello latest release of hello Azure Backup (which is available [here](http://aka.ms/azurebackup_agent)).</span></span> <span data-ttu-id="8c308-111">I clienti di System Center Data Protection Manager è necessario aggiornare, almeno DPM 2012 R2 UR5 prima di utilizzare DPM con hello servizio Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="8c308-111">System Center DPM customers must update to, at least, DPM 2012 R2 UR5 before using DPM with hello Azure Backup service.</span></span>

## <a name="what-is-hello-backup-schedule"></a><span data-ttu-id="8c308-112">Che cos'è hello pianificazione Backup?</span><span class="sxs-lookup"><span data-stu-id="8c308-112">What is hello Backup Schedule?</span></span>
<span data-ttu-id="8c308-113">pianificazione del backup Hello indica la frequenza di hello hello operazione di backup.</span><span class="sxs-lookup"><span data-stu-id="8c308-113">hello backup schedule indicates hello frequency of hello backup operation.</span></span> <span data-ttu-id="8c308-114">Ad esempio, le impostazioni di hello nella seguente schermata hello indicano che i backup vengono eseguiti ogni giorno alle 6 pm e a mezzanotte.</span><span class="sxs-lookup"><span data-stu-id="8c308-114">For example, hello settings in hello following screen indicate that backups are taken daily at 6pm and at midnight.</span></span>

![Pianificazione giornaliera](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

<span data-ttu-id="8c308-116">I clienti possono anche pianificare un backup settimanale.</span><span class="sxs-lookup"><span data-stu-id="8c308-116">Customers can also schedule a weekly backup.</span></span> <span data-ttu-id="8c308-117">Ad esempio, hello impostazioni nella seguente schermata hello indicano che i backup vengono eseguiti ogni alternativo domenica & mercoledì 9.30 e 1:00 AM.</span><span class="sxs-lookup"><span data-stu-id="8c308-117">For example, hello settings in hello following screen indicate that backups are taken every alternate Sunday & Wednesday at 9:30AM and 1:00AM.</span></span>

![Pianificazione settimanale](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-hello-retention-policy"></a><span data-ttu-id="8c308-119">Che cos'è hello criteri di conservazione?</span><span class="sxs-lookup"><span data-stu-id="8c308-119">What is hello Retention Policy?</span></span>
<span data-ttu-id="8c308-120">criteri di conservazione Hello specificano durata hello per cui devono essere archiviati i backup hello.</span><span class="sxs-lookup"><span data-stu-id="8c308-120">hello retention policy specifies hello duration for which hello backup must be stored.</span></span> <span data-ttu-id="8c308-121">Anziché specificare solo un criterio"semplice" per tutti i punti di backup, i clienti possono specificare criteri di conservazione diversi in base a quando viene eseguito il backup di hello.</span><span class="sxs-lookup"><span data-stu-id="8c308-121">Rather than just specifying a “flat policy” for all backup points, customers can specify different retention policies based on when hello backup is taken.</span></span> <span data-ttu-id="8c308-122">Hello punto di backup eseguito ogni giorno, che funge da un punto di ripristino operativo, ad esempio, viene mantenuto per 90 giorni.</span><span class="sxs-lookup"><span data-stu-id="8c308-122">For example, hello backup point taken daily, which serves as an operational recovery point, is preserved for 90 days.</span></span> <span data-ttu-id="8c308-123">punto di backup Hello eseguita alla fine hello ogni trimestre per scopi di controllo viene mantenuto per una durata.</span><span class="sxs-lookup"><span data-stu-id="8c308-123">hello backup point taken at hello end of each quarter for audit purposes is preserved for a longer duration.</span></span>

![Criteri di conservazione](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

<span data-ttu-id="8c308-125">Hello numero totale di "punti di conservazione" specificato in questo criterio è 90 (giornalieri punti) + 40 (uno ogni trimestre per 10 anni) = 130.</span><span class="sxs-lookup"><span data-stu-id="8c308-125">hello total number of “retention points” specified in this policy is 90 (daily points) + 40 (one each quarter for 10 years) = 130.</span></span>

## <a name="example--putting-both-together"></a><span data-ttu-id="8c308-126">Esempio: Uso di entrambi i metodi</span><span class="sxs-lookup"><span data-stu-id="8c308-126">Example – Putting both together</span></span>
![Schermata di esempio](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. <span data-ttu-id="8c308-128">**Criteri di mantenimento giornaliero**: i backup eseguiti quotidianamente vengono archiviati per sette giorni.</span><span class="sxs-lookup"><span data-stu-id="8c308-128">**Daily retention policy**: Backups taken daily are stored for seven days.</span></span>
2. <span data-ttu-id="8c308-129">**Criteri di conservazione settimanale**: i backup eseguiti ogni giorno a mezzanotte e ogni sabato alle 18.00 verranno conservati per quattro settimane</span><span class="sxs-lookup"><span data-stu-id="8c308-129">**Weekly retention policy**: Backups taken every day at midnight and 6PM Saturday are preserved for four weeks</span></span>
3. <span data-ttu-id="8c308-130">**Criteri di conservazione mensile**: vengono conservati i backup eseguiti a mezzanotte e 6 pm hello ultima domenica di ogni mese per 12 mesi</span><span class="sxs-lookup"><span data-stu-id="8c308-130">**Monthly retention policy**: Backups taken at midnight and 6pm on hello last Saturday of each month are preserved for 12 months</span></span>
4. <span data-ttu-id="8c308-131">**Criteri di conservazione annuale**: i backup eseguiti alla mezzanotte hello ultima domenica di ogni marzo vengono conservati per 10 anni</span><span class="sxs-lookup"><span data-stu-id="8c308-131">**Yearly retention policy**: Backups taken at midnight on hello last Saturday of every March are preserved for 10 years</span></span>

<span data-ttu-id="8c308-132">numero totale di "punti di conservazione" Hello (punti da cui un cliente può ripristinare i dati) in hello diagramma precedente viene calcolata come segue:</span><span class="sxs-lookup"><span data-stu-id="8c308-132">hello total number of “retention points” (points from which a customer can restore data) in hello preceding diagram is computed as follows:</span></span>

* <span data-ttu-id="8c308-133">due punti al giorno per sette giorni = 14 punti di ripristino</span><span class="sxs-lookup"><span data-stu-id="8c308-133">two points per day for seven days = 14 recovery points</span></span>
* <span data-ttu-id="8c308-134">due punti a settimana per quattro settimane = 8 punti di ripristino</span><span class="sxs-lookup"><span data-stu-id="8c308-134">two points per week for four weeks = 8 recovery points</span></span>
* <span data-ttu-id="8c308-135">due punti al mese per 12 mesi = 24 punti di ripristino</span><span class="sxs-lookup"><span data-stu-id="8c308-135">two points per month for 12 months = 24 recovery points</span></span>
* <span data-ttu-id="8c308-136">un punto all'anno per 10 anni = 10 punti di ripristino</span><span class="sxs-lookup"><span data-stu-id="8c308-136">one point per year per 10 years = 10 recovery points</span></span>

<span data-ttu-id="8c308-137">numero totale di Hello dei punti di ripristino è 56.</span><span class="sxs-lookup"><span data-stu-id="8c308-137">hello total number of recovery points is 56.</span></span>

> [!NOTE]
> <span data-ttu-id="8c308-138">Il backup di Azure non dispone di una restrizione sul numero di punti di ripristino.</span><span class="sxs-lookup"><span data-stu-id="8c308-138">Azure backup doesn't have a restriction on number of recovery points.</span></span>
>
>

## <a name="advanced-configuration"></a><span data-ttu-id="8c308-139">Configurazione avanzata</span><span class="sxs-lookup"><span data-stu-id="8c308-139">Advanced configuration</span></span>
<span data-ttu-id="8c308-140">Fare clic su **modifica** nella precedente schermata di hello, sono dotate di ulteriore flessibilità nello specificare pianificazioni di conservazione.</span><span class="sxs-lookup"><span data-stu-id="8c308-140">By clicking **Modify** in hello preceding screen, customers have further flexibility in specifying retention schedules.</span></span>

![Modifica](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a><span data-ttu-id="8c308-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8c308-142">Next Steps</span></span>
<span data-ttu-id="8c308-143">Per ulteriori informazioni sul Backup di Azure vedere:</span><span class="sxs-lookup"><span data-stu-id="8c308-143">For more information about Azure Backup, see:</span></span>

* [<span data-ttu-id="8c308-144">Introduzione tooAzure Backup</span><span class="sxs-lookup"><span data-stu-id="8c308-144">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="8c308-145">Valutazione di Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="8c308-145">Try Azure Backup</span></span>](backup-try-azure-backup-in-10-mins.md)
