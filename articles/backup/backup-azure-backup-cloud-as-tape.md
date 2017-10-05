---
title: Usare Backup di Azure per sostituire l'infrastruttura basata su nastro | Documentazione Microsoft
description: Informazioni sulla semantica di Backup di Azure, simile all'archiviazione su nastro, che consente di eseguire il backup e il ripristino dei dati in Azure
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
ms.openlocfilehash: f0f3152daf5f91f7c9e540797bf09b21969d2d33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="move-your-long-term-storage-from-tape-to-the-azure-cloud"></a><span data-ttu-id="c341a-103">Spostare lo spazio di archiviazione a lungo termine su nastro nel cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="c341a-103">Move your long-term storage from tape to the Azure cloud</span></span>
<span data-ttu-id="c341a-104">I clienti di Backup di Azure e System Center Data Protection Manager possono eseguire le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="c341a-104">Azure Backup and System Center Data Protection Manager customers can:</span></span>

* <span data-ttu-id="c341a-105">Eseguire il backup dei dati secondo le pianificazioni più adatte alle esigenze dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="c341a-105">Back up data in schedules which best suit the organizational needs.</span></span>
* <span data-ttu-id="c341a-106">Mantenere i dati di backup per periodi più lunghi</span><span class="sxs-lookup"><span data-stu-id="c341a-106">Retain the backup data for longer periods</span></span>
* <span data-ttu-id="c341a-107">Includere Azure nelle strategie di conservazione dei dati a lungo termine, in alternativa al backup su nastro.</span><span class="sxs-lookup"><span data-stu-id="c341a-107">Make Azure a part of their long-term retention needs (instead of tape).</span></span>

<span data-ttu-id="c341a-108">Questo articolo illustra come abilitare i criteri di backup e di conservazione.</span><span class="sxs-lookup"><span data-stu-id="c341a-108">This article explains how customers can enable backup and retention policies.</span></span> <span data-ttu-id="c341a-109">I clienti che usano i nastri per soddisfare le esigenze di conservazione a lungo termine dispongono ora di un'alternativa efficace e affidabile.</span><span class="sxs-lookup"><span data-stu-id="c341a-109">Customers who use tapes to address their long-term-retention needs now have a powerful and viable alternative with the availability of this feature.</span></span> <span data-ttu-id="c341a-110">Questa funzionalità è abilitata nella versione più recente di Backup di Azure, disponibile [in questa pagina](http://aka.ms/azurebackup_agent).</span><span class="sxs-lookup"><span data-stu-id="c341a-110">The feature is enabled in the latest release of the Azure Backup (which is available [here](http://aka.ms/azurebackup_agent)).</span></span> <span data-ttu-id="c341a-111">I clienti di System Center DPM devono effettuare l'aggiornamento a DPM 2012 R2 UR5 almeno, prima di poter usare DPM con il servizio Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="c341a-111">System Center DPM customers must update to, at least, DPM 2012 R2 UR5 before using DPM with the Azure Backup service.</span></span>

## <a name="what-is-the-backup-schedule"></a><span data-ttu-id="c341a-112">Che cos'è la pianificazione di backup?</span><span class="sxs-lookup"><span data-stu-id="c341a-112">What is the Backup Schedule?</span></span>
<span data-ttu-id="c341a-113">La pianificazione del backup indica la frequenza dell'operazione di backup.</span><span class="sxs-lookup"><span data-stu-id="c341a-113">The backup schedule indicates the frequency of the backup operation.</span></span> <span data-ttu-id="c341a-114">Ad esempio, le impostazioni nella schermata di seguito indicano che i backup vengono eseguiti ogni giorno alle ore 18.00 e a mezzanotte.</span><span class="sxs-lookup"><span data-stu-id="c341a-114">For example, the settings in the following screen indicate that backups are taken daily at 6pm and at midnight.</span></span>

![Pianificazione giornaliera](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

<span data-ttu-id="c341a-116">I clienti possono anche pianificare un backup settimanale.</span><span class="sxs-lookup"><span data-stu-id="c341a-116">Customers can also schedule a weekly backup.</span></span> <span data-ttu-id="c341a-117">Ad esempio, le impostazioni nella schermata di seguito indicano che verranno eseguiti backup a domeniche e mercoledì alterni alle 9:30 e all'1: 00.</span><span class="sxs-lookup"><span data-stu-id="c341a-117">For example, the settings in the following screen indicate that backups are taken every alternate Sunday & Wednesday at 9:30AM and 1:00AM.</span></span>

![Pianificazione settimanale](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-the-retention-policy"></a><span data-ttu-id="c341a-119">Che cos'è il criterio di conservazione?</span><span class="sxs-lookup"><span data-stu-id="c341a-119">What is the Retention Policy?</span></span>
<span data-ttu-id="c341a-120">I criteri di conservazione specificano il periodo di tempo per cui il backup deve essere archiviato.</span><span class="sxs-lookup"><span data-stu-id="c341a-120">The retention policy specifies the duration for which the backup must be stored.</span></span> <span data-ttu-id="c341a-121">Anziché specificare solo un "criterio semplice" per tutti i punti di backup, i clienti possono specificare criteri di conservazione diversi in base al momento in cui viene eseguito il backup.</span><span class="sxs-lookup"><span data-stu-id="c341a-121">Rather than just specifying a “flat policy” for all backup points, customers can specify different retention policies based on when the backup is taken.</span></span> <span data-ttu-id="c341a-122">Ad esempio, un punto di backup eseguito quotidianamente, che funge da punto di ripristino operativo, viene conservato per 90 giorni.</span><span class="sxs-lookup"><span data-stu-id="c341a-122">For example, the backup point taken daily, which serves as an operational recovery point, is preserved for 90 days.</span></span> <span data-ttu-id="c341a-123">Il punto di backup eseguito alla fine di ogni trimestre per scopi di controllo viene mantenuto per un periodo più lungo.</span><span class="sxs-lookup"><span data-stu-id="c341a-123">The backup point taken at the end of each quarter for audit purposes is preserved for a longer duration.</span></span>

![Criteri di conservazione](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

<span data-ttu-id="c341a-125">Il numero totale di "punti di conservazione" specificati in questi criteri è pari a 90 (punti giornalieri) + 40 (uno per ogni trimestre per 10 anni) = 130.</span><span class="sxs-lookup"><span data-stu-id="c341a-125">The total number of “retention points” specified in this policy is 90 (daily points) + 40 (one each quarter for 10 years) = 130.</span></span>

## <a name="example--putting-both-together"></a><span data-ttu-id="c341a-126">Esempio: Uso di entrambi i metodi</span><span class="sxs-lookup"><span data-stu-id="c341a-126">Example – Putting both together</span></span>
![Schermata di esempio](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. <span data-ttu-id="c341a-128">**Criteri di mantenimento giornaliero**: i backup eseguiti quotidianamente vengono archiviati per sette giorni.</span><span class="sxs-lookup"><span data-stu-id="c341a-128">**Daily retention policy**: Backups taken daily are stored for seven days.</span></span>
2. <span data-ttu-id="c341a-129">**Criteri di conservazione settimanale**: i backup eseguiti ogni giorno a mezzanotte e ogni sabato alle 18.00 verranno conservati per quattro settimane</span><span class="sxs-lookup"><span data-stu-id="c341a-129">**Weekly retention policy**: Backups taken every day at midnight and 6PM Saturday are preserved for four weeks</span></span>
3. <span data-ttu-id="c341a-130">**Criteri di mantenimento mensile**: i backup eseguiti a mezzanotte e alle 18.00 dell'ultimo sabato del mese verranno conservati per 12 mesi</span><span class="sxs-lookup"><span data-stu-id="c341a-130">**Monthly retention policy**: Backups taken at midnight and 6pm on the last Saturday of each month are preserved for 12 months</span></span>
4. <span data-ttu-id="c341a-131">**Criteri di mantenimento annuale**: i backup eseguiti a mezzanotte dell'ultimo sabato del mese di marzo verranno conservati per 10 anni</span><span class="sxs-lookup"><span data-stu-id="c341a-131">**Yearly retention policy**: Backups taken at midnight on the last Saturday of every March are preserved for 10 years</span></span>

<span data-ttu-id="c341a-132">Il numero totale dei "punti di conservazione" (punti da cui un cliente può ripristinare i dati) riportati nel diagramma precedente viene calcolato nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="c341a-132">The total number of “retention points” (points from which a customer can restore data) in the preceding diagram is computed as follows:</span></span>

* <span data-ttu-id="c341a-133">due punti al giorno per sette giorni = 14 punti di ripristino</span><span class="sxs-lookup"><span data-stu-id="c341a-133">two points per day for seven days = 14 recovery points</span></span>
* <span data-ttu-id="c341a-134">due punti a settimana per quattro settimane = 8 punti di ripristino</span><span class="sxs-lookup"><span data-stu-id="c341a-134">two points per week for four weeks = 8 recovery points</span></span>
* <span data-ttu-id="c341a-135">due punti al mese per 12 mesi = 24 punti di ripristino</span><span class="sxs-lookup"><span data-stu-id="c341a-135">two points per month for 12 months = 24 recovery points</span></span>
* <span data-ttu-id="c341a-136">un punto all'anno per 10 anni = 10 punti di ripristino</span><span class="sxs-lookup"><span data-stu-id="c341a-136">one point per year per 10 years = 10 recovery points</span></span>

<span data-ttu-id="c341a-137">Il numero totale dei punti di ripristino è 56.</span><span class="sxs-lookup"><span data-stu-id="c341a-137">The total number of recovery points is 56.</span></span>

> [!NOTE]
> <span data-ttu-id="c341a-138">Il backup di Azure non dispone di una restrizione sul numero di punti di ripristino.</span><span class="sxs-lookup"><span data-stu-id="c341a-138">Azure backup doesn't have a restriction on number of recovery points.</span></span>
>
>

## <a name="advanced-configuration"></a><span data-ttu-id="c341a-139">Configurazione avanzata</span><span class="sxs-lookup"><span data-stu-id="c341a-139">Advanced configuration</span></span>
<span data-ttu-id="c341a-140">Facendo clic su **Modifica** nella schermata precedente, i clienti dispongono di un'ulteriore flessibilità nella definizione delle pianificazioni di conservazione.</span><span class="sxs-lookup"><span data-stu-id="c341a-140">By clicking **Modify** in the preceding screen, customers have further flexibility in specifying retention schedules.</span></span>

![Modifica](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a><span data-ttu-id="c341a-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c341a-142">Next Steps</span></span>
<span data-ttu-id="c341a-143">Per ulteriori informazioni sul Backup di Azure vedere:</span><span class="sxs-lookup"><span data-stu-id="c341a-143">For more information about Azure Backup, see:</span></span>

* [<span data-ttu-id="c341a-144">Introduzione a Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="c341a-144">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="c341a-145">Valutazione di Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="c341a-145">Try Azure Backup</span></span>](backup-try-azure-backup-in-10-mins.md)
