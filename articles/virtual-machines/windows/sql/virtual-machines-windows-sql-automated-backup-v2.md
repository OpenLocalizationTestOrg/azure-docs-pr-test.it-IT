---
title: aaaAutomated v2 Backup per SQL Server 2016 macchine virtuali di Azure | Documenti Microsoft
description: "Vengono illustrate funzionalità Backup automatizzato hello per SQL Server 2016 VM in esecuzione in Azure. Questo articolo è specifico tooVMs utilizzando hello Gestione risorse."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: ebd23868-821c-475b-b867-06d4a2e310c7
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/05/2017
ms.author: jroth
ms.openlocfilehash: a322792fb22c76bfa74fafb711b8b1927a6e2b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a><span data-ttu-id="f7894-104">Backup automatico v2 per macchine virtuali SQL Server 2016 in Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="f7894-104">Automated Backup v2 for SQL Server 2016 Azure Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f7894-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="f7894-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="f7894-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="f7894-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="f7894-107">V2 Backup automatizzato configura automaticamente [tooMicrosoft Backup gestito Azure](https://msdn.microsoft.com/library/dn449496.aspx) per tutti i database nuovi ed esistenti in una macchina virtuale di Azure in esecuzione SQL Server 2016 Standard, Enterprise Edition o Developer Edition.</span><span class="sxs-lookup"><span data-stu-id="f7894-107">Automated Backup v2 automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2016 Standard, Enterprise, or Developer editions.</span></span> <span data-ttu-id="f7894-108">In questo modo tooconfigure normali backup di database che utilizzano l'archiviazione blob di Azure durevole.</span><span class="sxs-lookup"><span data-stu-id="f7894-108">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="f7894-109">V2 Backup automatizzati dipende hello [estensione di SQL Server IaaS Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="f7894-109">Automated Backup v2 depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="f7894-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f7894-110">Prerequisites</span></span>
<span data-ttu-id="f7894-111">toouse v2 Backup automatizzato, esaminare hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="f7894-111">toouse Automated Backup v2, review hello following prerequisites:</span></span>

<span data-ttu-id="f7894-112">**Sistema operativo**:</span><span class="sxs-lookup"><span data-stu-id="f7894-112">**Operating System**:</span></span>

- <span data-ttu-id="f7894-113">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="f7894-113">Windows Server 2012 R2</span></span>
- <span data-ttu-id="f7894-114">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="f7894-114">Windows Server 2016</span></span>

<span data-ttu-id="f7894-115">**Versione/edizione di SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="f7894-115">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="f7894-116">SQL Server 2016 Standard</span><span class="sxs-lookup"><span data-stu-id="f7894-116">SQL Server 2016 Standard</span></span>
- <span data-ttu-id="f7894-117">SQL Server 2016 Enterprise</span><span class="sxs-lookup"><span data-stu-id="f7894-117">SQL Server 2016 Enterprise</span></span>
- <span data-ttu-id="f7894-118">SQL Server 2016 Developer</span><span class="sxs-lookup"><span data-stu-id="f7894-118">SQL Server 2016 Developer</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7894-119">Backup automatico v2 funziona con SQL Server 2016.</span><span class="sxs-lookup"><span data-stu-id="f7894-119">Automated Backup v2 works with SQL Server 2016.</span></span> <span data-ttu-id="f7894-120">Se si utilizza SQL Server 2014, è possibile utilizzare Backup automatizzato v1 tooback backup dei database.</span><span class="sxs-lookup"><span data-stu-id="f7894-120">If you are using SQL Server 2014, you can use Automated Backup v1 tooback up your databases.</span></span> <span data-ttu-id="f7894-121">Per altre informazioni, vedere [Backup automatico per SQL Server 2014 in Macchine virtuali di Azure](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="f7894-121">For more information, see [Automated Backup for SQL Server 2014 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

<span data-ttu-id="f7894-122">**Configurazione del database**:</span><span class="sxs-lookup"><span data-stu-id="f7894-122">**Database configuration**:</span></span>

- <span data-ttu-id="f7894-123">Database di destinazione devono utilizzare il modello di recupero con registrazione completa hello.</span><span class="sxs-lookup"><span data-stu-id="f7894-123">Target databases must use hello full recovery model.</span></span> <span data-ttu-id="f7894-124">Per ulteriori informazioni sull'impatto hello del modello di recupero con registrazione completa hello sui backup, vedere [hello Backup nel modello di recupero completo](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="f7894-124">For more information about hello impact of hello full recovery model on backups, see [Backup Under hello Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="f7894-125">Database di sistema non dispone di toouse modello di recupero con registrazione completa.</span><span class="sxs-lookup"><span data-stu-id="f7894-125">System databases do not have toouse full recovery model.</span></span> <span data-ttu-id="f7894-126">Tuttavia, se è necessario toobe backup log per modello o MSDB, è necessario utilizzare il modello di recupero con registrazione completa.</span><span class="sxs-lookup"><span data-stu-id="f7894-126">However, if you require log backups toobe taken for Model or MSDB, you must use full recovery model.</span></span>
- <span data-ttu-id="f7894-127">Database di destinazione devono essere nell'istanza di SQL Server predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="f7894-127">Target databases must be on hello default SQL Server instance.</span></span> <span data-ttu-id="f7894-128">Hello estensione IaaS di SQL Server non supporta le istanze denominate.</span><span class="sxs-lookup"><span data-stu-id="f7894-128">hello SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="f7894-129">**Modello di distribuzione di Azure**:</span><span class="sxs-lookup"><span data-stu-id="f7894-129">**Azure deployment model**:</span></span>

- <span data-ttu-id="f7894-130">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="f7894-130">Resource Manager</span></span>

> [!NOTE]
> <span data-ttu-id="f7894-131">Backup automatizzato si basa su hello **estensione di SQL Server IaaS Agent**.</span><span class="sxs-lookup"><span data-stu-id="f7894-131">Automated Backup relies on hello **SQL Server IaaS Agent Extension**.</span></span> <span data-ttu-id="f7894-132">Per impostazione predefinita, le attuali immagini della raccolta di macchine virtuali di SQL aggiungono questa estensione.</span><span class="sxs-lookup"><span data-stu-id="f7894-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="f7894-133">Per altre informazioni, vedere [Estensione Agente IaaS di SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="f7894-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="f7894-134">Impostazioni</span><span class="sxs-lookup"><span data-stu-id="f7894-134">Settings</span></span>
<span data-ttu-id="f7894-135">Hello nella tabella seguente vengono descritte hello opzioni che possono essere configurate per Backup automatizzato v2.</span><span class="sxs-lookup"><span data-stu-id="f7894-135">hello following table describes hello options that can be configured for Automated Backup v2.</span></span> <span data-ttu-id="f7894-136">passaggi di configurazione effettivi Hello variano a seconda che si utilizzi hello portale di Azure o i comandi di Windows PowerShell per Azure.</span><span class="sxs-lookup"><span data-stu-id="f7894-136">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

### <a name="basic-settings"></a><span data-ttu-id="f7894-137">Basic Settings</span><span class="sxs-lookup"><span data-stu-id="f7894-137">Basic Settings</span></span>

| <span data-ttu-id="f7894-138">Impostazione</span><span class="sxs-lookup"><span data-stu-id="f7894-138">Setting</span></span> | <span data-ttu-id="f7894-139">Intervallo (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="f7894-139">Range (Default)</span></span> | <span data-ttu-id="f7894-140">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7894-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f7894-141">**Backup automatico**</span><span class="sxs-lookup"><span data-stu-id="f7894-141">**Automated Backup**</span></span> | <span data-ttu-id="f7894-142">Enable/Disable (disabilitato)</span><span class="sxs-lookup"><span data-stu-id="f7894-142">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="f7894-143">Abilita o disabilita il backup automatico per una macchina virtuale di Azure in cui viene eseguito SQL Server 2016 Standard o Enterprise.</span><span class="sxs-lookup"><span data-stu-id="f7894-143">Enables or disables Automated Backup for an Azure VM running SQL Server 2016 Standard or Enterprise.</span></span> |
| <span data-ttu-id="f7894-144">**Periodo di conservazione**</span><span class="sxs-lookup"><span data-stu-id="f7894-144">**Retention Period**</span></span> | <span data-ttu-id="f7894-145">1-30 giorni (30 giorni)</span><span class="sxs-lookup"><span data-stu-id="f7894-145">1-30 days (30 days)</span></span> | <span data-ttu-id="f7894-146">numero di Hello di backup di tooretain giorni.</span><span class="sxs-lookup"><span data-stu-id="f7894-146">hello number of days tooretain backups.</span></span> |
| <span data-ttu-id="f7894-147">**Storage Account**</span><span class="sxs-lookup"><span data-stu-id="f7894-147">**Storage Account**</span></span> | <span data-ttu-id="f7894-148">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="f7894-148">Azure storage account</span></span> | <span data-ttu-id="f7894-149">Toouse un account di archiviazione di Azure per archiviare i file di Backup automatizzato nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="f7894-149">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="f7894-150">Un contenitore viene creato in questo percorso toostore tutti i file di backup.</span><span class="sxs-lookup"><span data-stu-id="f7894-150">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="f7894-151">file di backup Hello convenzione di denominazione include hello data, ora e il GUID del database.</span><span class="sxs-lookup"><span data-stu-id="f7894-151">hello backup file naming convention includes hello date, time, and database GUID.</span></span> |
| <span data-ttu-id="f7894-152">**Crittografia**</span><span class="sxs-lookup"><span data-stu-id="f7894-152">**Encryption**</span></span> |<span data-ttu-id="f7894-153">Enable/Disable (disabilitato)</span><span class="sxs-lookup"><span data-stu-id="f7894-153">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="f7894-154">Abilita o disabilita la crittografia.</span><span class="sxs-lookup"><span data-stu-id="f7894-154">Enables or disables encryption.</span></span> <span data-ttu-id="f7894-155">Quando la crittografia è abilitata, hello i certificati utilizzati toorestore hello backup si trovano in hello specificato dell'account di archiviazione in hello stesso **automaticbackup** contenitore usando hello stessa convenzione di denominazione.</span><span class="sxs-lookup"><span data-stu-id="f7894-155">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same **automaticbackup** container using hello same naming convention.</span></span> <span data-ttu-id="f7894-156">Se la modifica di password hello, viene generato un nuovo certificato con la password, ma vecchio certificato hello rimane toorestore eventuale backup precedente.</span><span class="sxs-lookup"><span data-stu-id="f7894-156">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="f7894-157">**Password**</span><span class="sxs-lookup"><span data-stu-id="f7894-157">**Password**</span></span> |<span data-ttu-id="f7894-158">Testo della password</span><span class="sxs-lookup"><span data-stu-id="f7894-158">Password text</span></span> | <span data-ttu-id="f7894-159">Password per le chiavi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="f7894-159">A password for encryption keys.</span></span> <span data-ttu-id="f7894-160">Questa impostazione è necessaria solo se la crittografia è abilitata.</span><span class="sxs-lookup"><span data-stu-id="f7894-160">This is only required if encryption is enabled.</span></span> <span data-ttu-id="f7894-161">In ordine toorestore un backup crittografato, è necessario disporre la password corretta hello e del certificato correlato che è stato utilizzato in fase di hello hello del backup.</span><span class="sxs-lookup"><span data-stu-id="f7894-161">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> |

### <a name="advanced-settings"></a><span data-ttu-id="f7894-162">Impostazioni avanzate</span><span class="sxs-lookup"><span data-stu-id="f7894-162">Advanced Settings</span></span>

| <span data-ttu-id="f7894-163">Impostazione</span><span class="sxs-lookup"><span data-stu-id="f7894-163">Setting</span></span> | <span data-ttu-id="f7894-164">Intervallo (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="f7894-164">Range (Default)</span></span> | <span data-ttu-id="f7894-165">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7894-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f7894-166">**Backup dei database di sistema**</span><span class="sxs-lookup"><span data-stu-id="f7894-166">**System Database Backups**</span></span> | <span data-ttu-id="f7894-167">Enable/Disable (disabilitato)</span><span class="sxs-lookup"><span data-stu-id="f7894-167">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="f7894-168">Quando abilitata, questa funzionalità verrà anche eseguito il backup il database di sistema hello: Master, MSDB e modello.</span><span class="sxs-lookup"><span data-stu-id="f7894-168">When enabled, this feature will also back up hello system databases: Master, MSDB, and Model.</span></span> <span data-ttu-id="f7894-169">Per hello MSDB e modello di database, verificare che siano in modalità di recupero con registrazione completa se si desidera toobe i backup del log eseguito.</span><span class="sxs-lookup"><span data-stu-id="f7894-169">For hello MSDB and Model databases, verify that they are in full recovery mode if you want log backups toobe taken.</span></span> <span data-ttu-id="f7894-170">Non vengono mai eseguiti backup di log per Master,</span><span class="sxs-lookup"><span data-stu-id="f7894-170">Log backups are never taken for Master.</span></span> <span data-ttu-id="f7894-171">né backup di alcun tipo per TempDB.</span><span class="sxs-lookup"><span data-stu-id="f7894-171">And no backups are taken for TempDB.</span></span> |
| <span data-ttu-id="f7894-172">**Pianificazione backup**</span><span class="sxs-lookup"><span data-stu-id="f7894-172">**Backup Schedule**</span></span> | <span data-ttu-id="f7894-173">Manual/Automated (Automated) (Manuale/Automatizzato - Automatizzato)</span><span class="sxs-lookup"><span data-stu-id="f7894-173">Manual/Automated (Automated)</span></span> | <span data-ttu-id="f7894-174">Per impostazione predefinita, pianificazione del backup hello verrà automaticamente determinato in base a una crescita log hello.</span><span class="sxs-lookup"><span data-stu-id="f7894-174">By default, hello backup schedule will be automatically determined based on hello log growth.</span></span> <span data-ttu-id="f7894-175">Pianificazione del backup manuale consente l'intervallo di tempo hello toospecify hello utente per i backup.</span><span class="sxs-lookup"><span data-stu-id="f7894-175">Manual backup schedule allows hello user toospecify hello time window for backups.</span></span> <span data-ttu-id="f7894-176">In questo caso, i backup avranno sempre luogo hello frequenza durante hello specificate e intervallo di tempo di un determinato giorno.</span><span class="sxs-lookup"><span data-stu-id="f7894-176">In this case, backups will only ever take place at hello specified frequency and during hello specified time window of a given day.</span></span> |
| <span data-ttu-id="f7894-177">**Frequenza backup completo**</span><span class="sxs-lookup"><span data-stu-id="f7894-177">**Full backup frequency**</span></span> | <span data-ttu-id="f7894-178">Giornaliera/settimanale</span><span class="sxs-lookup"><span data-stu-id="f7894-178">Daily/Weekly</span></span> | <span data-ttu-id="f7894-179">Frequenza dei backup completi.</span><span class="sxs-lookup"><span data-stu-id="f7894-179">Frequency of full backups.</span></span> <span data-ttu-id="f7894-180">In entrambi i casi, i backup completi verranno avviato il successivo intervallo di tempo pianificato hello.</span><span class="sxs-lookup"><span data-stu-id="f7894-180">In both cases, full backups will begin during hello next scheduled time window.</span></span> <span data-ttu-id="f7894-181">Quando si seleziona la frequenza settimanale, i backup potrebbero durare più giorni fino ad aver incluso tutti i database.</span><span class="sxs-lookup"><span data-stu-id="f7894-181">When weekly is selected, backups could span multiple days until all databases have successfully backed up.</span></span> |
| <span data-ttu-id="f7894-182">**Ora di inizio backup completo**</span><span class="sxs-lookup"><span data-stu-id="f7894-182">**Full backup start time**</span></span> | <span data-ttu-id="f7894-183">00:00 – 23:00 (01:00)</span><span class="sxs-lookup"><span data-stu-id="f7894-183">00:00 – 23:00 (01:00)</span></span> | <span data-ttu-id="f7894-184">Ora di inizio di un determinato giorno in cui possono avere luogo i backup completi.</span><span class="sxs-lookup"><span data-stu-id="f7894-184">Start time of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="f7894-185">**Intervallo di tempo per il backup completo**</span><span class="sxs-lookup"><span data-stu-id="f7894-185">**Full backup time window**</span></span> | <span data-ttu-id="f7894-186">1-23 ore (1 ora)</span><span class="sxs-lookup"><span data-stu-id="f7894-186">1 – 23 hours (1 hour)</span></span> | <span data-ttu-id="f7894-187">Durata dell'intervallo di tempo hello di un determinato giorno durante il quale può avvenire backup completi.</span><span class="sxs-lookup"><span data-stu-id="f7894-187">Duration of hello time window of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="f7894-188">**Frequenza di backup del log**</span><span class="sxs-lookup"><span data-stu-id="f7894-188">**Log backup frequency**</span></span> | <span data-ttu-id="f7894-189">5-60 minuti (60 minuti)</span><span class="sxs-lookup"><span data-stu-id="f7894-189">5 – 60 minutes (60 minutes)</span></span> | <span data-ttu-id="f7894-190">Frequenza dei backup dei log.</span><span class="sxs-lookup"><span data-stu-id="f7894-190">Frequency of log backups.</span></span> |

## <a name="understanding-full-backup-frequency"></a><span data-ttu-id="f7894-191">Informazioni sulla frequenza dei backup completi</span><span class="sxs-lookup"><span data-stu-id="f7894-191">Understanding full backup frequency</span></span>
<span data-ttu-id="f7894-192">È importante toounderstand differenza di hello tra i backup completi giornalieri e settimanali.</span><span class="sxs-lookup"><span data-stu-id="f7894-192">It is important toounderstand hello difference between daily and weekly full backups.</span></span> <span data-ttu-id="f7894-193">Per farlo, verranno illustrati due scenari di esempio.</span><span class="sxs-lookup"><span data-stu-id="f7894-193">In this effort, we will walk through two example scenarios.</span></span>

### <a name="scenario-1-weekly-backups"></a><span data-ttu-id="f7894-194">Scenario 1: Backup settimanali</span><span class="sxs-lookup"><span data-stu-id="f7894-194">Scenario 1: Weekly backups</span></span>
<span data-ttu-id="f7894-195">Si dispone di una macchina virtuale di SQL Server che contiene una serie di database di dimensioni molto grandi.</span><span class="sxs-lookup"><span data-stu-id="f7894-195">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="f7894-196">Lunedì, si attiva v2 Backup automatizzato con hello seguenti impostazioni:</span><span class="sxs-lookup"><span data-stu-id="f7894-196">On Monday, you enable Automated Backup v2 with hello following settings:</span></span>

- <span data-ttu-id="f7894-197">Pianificazione backup: **Manuale**</span><span class="sxs-lookup"><span data-stu-id="f7894-197">Backup schedule: **Manual**</span></span>
- <span data-ttu-id="f7894-198">Frequenza backup completo: **Settimanale**</span><span class="sxs-lookup"><span data-stu-id="f7894-198">Full backup frequency: **Weekly**</span></span>
- <span data-ttu-id="f7894-199">Ora di inizio backup completo: **01:00**</span><span class="sxs-lookup"><span data-stu-id="f7894-199">Full backup start time: **01:00**</span></span>
- <span data-ttu-id="f7894-200">Intervallo di tempo dei backup completi: **1 ora**</span><span class="sxs-lookup"><span data-stu-id="f7894-200">Full backup time window: **1 hour**</span></span>

<span data-ttu-id="f7894-201">Ciò significa che hello disponibili backup successivo è martedì alle 13.00 per 1 ora.</span><span class="sxs-lookup"><span data-stu-id="f7894-201">This means that hello next available backup window is Tuesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="f7894-202">In quel momento, Backup automatico inizierà a eseguire il backup dei database, uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="f7894-202">At that time, Automated Backup will begin backing up your databases one at a time.</span></span> <span data-ttu-id="f7894-203">In questo scenario, i database sono sufficientemente grandi il completamento per i database coppia primo hello backup completi.</span><span class="sxs-lookup"><span data-stu-id="f7894-203">In this scenario, your databases are large enough that full backups will complete for hello first couple databases.</span></span> <span data-ttu-id="f7894-204">Tuttavia, dopo un'ora non tutti i database hello è stato eseguito il.</span><span class="sxs-lookup"><span data-stu-id="f7894-204">However, after one hour not all of hello databases have been backed up.</span></span>

<span data-ttu-id="f7894-205">In questo caso, verrà avviato Backup automatizzato backup hello rimanenti hello database giorno successivo, mercoledì alle 13.00 per 1 ora.</span><span class="sxs-lookup"><span data-stu-id="f7894-205">When this happens, Automated Backup will begin backing up hello remaining databases hello next day, Wednesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="f7894-206">Se non tutti i database sottoposti a backup in quel momento, si tenterà nuovamente hello giorno successivo a hello stesso tempo.</span><span class="sxs-lookup"><span data-stu-id="f7894-206">If not all databases have been backed up in that time, it will try again hello next day at hello same time.</span></span> <span data-ttu-id="f7894-207">fe così via fino a quando non sarà stato eseguito il backup di tutti i database.</span><span class="sxs-lookup"><span data-stu-id="f7894-207">This will continue until all databases have been successfully backed up.</span></span>

<span data-ttu-id="f7894-208">Il martedì successivo, Backup automatico comincerà nuovamente il backup di tutti i database.</span><span class="sxs-lookup"><span data-stu-id="f7894-208">Once it reaches Tuesday again, Automated Backup will begin backing up all databases once again.</span></span>

<span data-ttu-id="f7894-209">Questo scenario viene illustrato che funzionerà solo Backup automatizzato nell'intervallo di tempo specificato hello e ogni database da sottoporre a backup una volta alla settimana.</span><span class="sxs-lookup"><span data-stu-id="f7894-209">This scenario shows that Automated Backup will only operate within hello specified time window, and each database will be backed up once per week.</span></span> <span data-ttu-id="f7894-210">Mostra anche che è possibile per backup toospan più giorni in hello caso in cui non è possibile toocomplete tutti i backup in un solo giorno.</span><span class="sxs-lookup"><span data-stu-id="f7894-210">This also shows that it is possible for backups toospan multiple days in hello case where it is not possible toocomplete all backups in a single day.</span></span>

### <a name="scenario-2-daily-backups"></a><span data-ttu-id="f7894-211">Scenario 2: Backup giornalieri</span><span class="sxs-lookup"><span data-stu-id="f7894-211">Scenario 2: Daily backups</span></span>
<span data-ttu-id="f7894-212">Si dispone di una macchina virtuale di SQL Server che contiene una serie di database di dimensioni molto grandi.</span><span class="sxs-lookup"><span data-stu-id="f7894-212">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="f7894-213">Lunedì, si attiva v2 Backup automatizzato con hello seguenti impostazioni:</span><span class="sxs-lookup"><span data-stu-id="f7894-213">On Monday, you enable Automated Backup v2 with hello following settings:</span></span>

- <span data-ttu-id="f7894-214">Pianificazione backup: Manuale</span><span class="sxs-lookup"><span data-stu-id="f7894-214">Backup schedule: Manual</span></span>
- <span data-ttu-id="f7894-215">Frequenza backup completo: Ogni giorno</span><span class="sxs-lookup"><span data-stu-id="f7894-215">Full backup frequency: Daily</span></span>
- <span data-ttu-id="f7894-216">Ora di inizio backup completo: 22:00</span><span class="sxs-lookup"><span data-stu-id="f7894-216">Full backup start time: 22:00</span></span>
- <span data-ttu-id="f7894-217">Intervallo di tempo dei backup completi: 6 ore</span><span class="sxs-lookup"><span data-stu-id="f7894-217">Full backup time window: 6 hours</span></span>

<span data-ttu-id="f7894-218">Ciò significa che hello disponibili backup successivo è lunedì 10 PM per 6 ore.</span><span class="sxs-lookup"><span data-stu-id="f7894-218">This means that hello next available backup window is Monday at 10 PM for 6 hours.</span></span> <span data-ttu-id="f7894-219">In quel momento, Backup automatico inizierà a eseguire il backup dei database, uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="f7894-219">At that time, Automated Backup will begin backing up your databases one at a time.</span></span>

<span data-ttu-id="f7894-220">Il backup sarà quindi eseguito nuovamente martedì alle 22:00 per 6 ore.</span><span class="sxs-lookup"><span data-stu-id="f7894-220">Then, on Tuesday at 10 for 6 hours, full backups of all databases will start again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7894-221">Durante la pianificazione dei backup giornalieri, è consigliabile pianificare un tooensure finestra wide ora che tutti i database è possibile eseguire backup entro questo intervallo.</span><span class="sxs-lookup"><span data-stu-id="f7894-221">When scheduling daily backups, it is recommended that you schedule a wide time window tooensure all databases can be backed up within this time.</span></span> <span data-ttu-id="f7894-222">Ciò è particolarmente importante in caso di hello in cui si dispone di una grande quantità di dati tooback backup.</span><span class="sxs-lookup"><span data-stu-id="f7894-222">This is especially important in hello case where you have a large amount of data tooback up.</span></span>

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="f7894-223">Configurazione di hello portale</span><span class="sxs-lookup"><span data-stu-id="f7894-223">Configuration in hello Portal</span></span>

<span data-ttu-id="f7894-224">È possibile utilizzare hello tooconfigure portale Azure Backup automatizzato v2 durante il provisioning o per le macchine virtuali di esistente SQL Server 2016.</span><span class="sxs-lookup"><span data-stu-id="f7894-224">You can use hello Azure portal tooconfigure Automated Backup v2 during provisioning or for existing SQL Server 2016 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="f7894-225">Nuove VM</span><span class="sxs-lookup"><span data-stu-id="f7894-225">New VMs</span></span>

<span data-ttu-id="f7894-226">Quando si crea una nuova macchina virtuale di SQL Server 2016 nel modello di distribuzione di gestione risorse di hello, utilizzare hello tooconfigure portale Azure Backup automatizzato v2.</span><span class="sxs-lookup"><span data-stu-id="f7894-226">Use hello Azure portal tooconfigure Automated Backup v2 when you create a new SQL Server 2016 Virtual Machine in hello Resource Manager deployment model.</span></span> 

<span data-ttu-id="f7894-227">In hello **impostazioni di SQL Server** pannello seleziona **backup automatizzato**.</span><span class="sxs-lookup"><span data-stu-id="f7894-227">In hello **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="f7894-228">schermata del portale di Azure seguente Hello Mostra hello **Backup automatizzato SQL** blade.</span><span class="sxs-lookup"><span data-stu-id="f7894-228">hello following Azure portal screenshot shows hello **SQL Automated Backup** blade.</span></span>

![Configurazione del backup automatico di SQL nel Portale di Azure](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> <span data-ttu-id="f7894-230">L'opzione Backup automatico v2 è disabilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="f7894-230">Automated Backup v2 is disabled by default.</span></span>

<span data-ttu-id="f7894-231">Per contesto, vedere l'argomento completo hello in [provisioning di una macchina virtuale di SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="f7894-231">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="f7894-232">VM esistenti</span><span class="sxs-lookup"><span data-stu-id="f7894-232">Existing VMs</span></span>

<span data-ttu-id="f7894-233">Per le macchine virtuali SQL Server esistenti, selezionare la macchina virtuale SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f7894-233">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="f7894-234">Selezionare quindi hello **configurazione di SQL Server** sezione di hello **impostazioni** blade.</span><span class="sxs-lookup"><span data-stu-id="f7894-234">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Backup automatico di SQL per le VM esistenti](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

<span data-ttu-id="f7894-236">In hello **configurazione di SQL Server** pannello, fare clic su hello **modifica** pulsante hello automatizzata sezione backup.</span><span class="sxs-lookup"><span data-stu-id="f7894-236">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated backup section.</span></span>

![Configurare il backup automatico di SQL per le VM esistenti](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

<span data-ttu-id="f7894-238">Al termine, fare clic su hello **OK** pulsante nella parte inferiore di hello di hello **configurazione di SQL Server** pannello toosave le modifiche.</span><span class="sxs-lookup"><span data-stu-id="f7894-238">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="f7894-239">Se si sta abilitando Backup automatizzato per hello prima volta, Azure Configura hello agente IaaS di SQL Server in background hello.</span><span class="sxs-lookup"><span data-stu-id="f7894-239">If you are enabling Automated Backup for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="f7894-240">Durante questo periodo, hello portale di Azure potrebbe non visualizzare che Backup automatizzato è configurato.</span><span class="sxs-lookup"><span data-stu-id="f7894-240">During this time, hello Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="f7894-241">Attendere alcuni minuti per hello agente toobe installato, configurato.</span><span class="sxs-lookup"><span data-stu-id="f7894-241">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="f7894-242">Dopo tale hello Azure portale rispecchierà le nuove impostazioni hello.</span><span class="sxs-lookup"><span data-stu-id="f7894-242">After that hello Azure portal will reflect hello new settings.</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="f7894-243">Configurazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7894-243">Configuration with PowerShell</span></span>

<span data-ttu-id="f7894-244">È possibile utilizzare PowerShell tooconfigure v2 Backup automatizzato.</span><span class="sxs-lookup"><span data-stu-id="f7894-244">You can use PowerShell tooconfigure Automated Backup v2.</span></span> <span data-ttu-id="f7894-245">Prima di iniziare, è necessario eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="f7894-245">Before you begin, you must:</span></span>

- <span data-ttu-id="f7894-246">[Scaricare e installare hello più recente di Azure PowerShell](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="f7894-246">[Download and install hello latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="f7894-247">Aprire Windows PowerShell e associarlo al proprio account.</span><span class="sxs-lookup"><span data-stu-id="f7894-247">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="f7894-248">È possibile farlo attenendosi alla seguente procedura hello in hello [configura la sottoscrizione](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) sezione di hello provisioning argomento.</span><span class="sxs-lookup"><span data-stu-id="f7894-248">You can do this by following hello steps in hello [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of hello provisioning topic.</span></span>

### <a name="install-hello-sql-iaas-extension"></a><span data-ttu-id="f7894-249">Installare hello estensione SQL IaaS</span><span class="sxs-lookup"><span data-stu-id="f7894-249">Install hello SQL IaaS Extension</span></span>
<span data-ttu-id="f7894-250">Se eseguito il provisioning di una macchina virtuale di SQL Server dal portale di Azure hello, hello estensione IaaS di SQL Server deve essere già installato.</span><span class="sxs-lookup"><span data-stu-id="f7894-250">If you provisioned a SQL Server virtual machine from hello Azure portal, hello SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="f7894-251">È possibile determinare se è installato per la macchina virtuale tramite la chiamata **Get AzureRmVM** comando ed esaminando hello **estensioni** proprietà.</span><span class="sxs-lookup"><span data-stu-id="f7894-251">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining hello **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions 
```

<span data-ttu-id="f7894-252">Se è installato l'estensione di SQL Server IaaS Agent hello, si dovrebbe che è elencato come "SqlIaaSAgent" o "SQLIaaSExtension".</span><span class="sxs-lookup"><span data-stu-id="f7894-252">If hello SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="f7894-253">**ProvisioningState** per estensione hello deve inoltre visualizzare "Succeeded".</span><span class="sxs-lookup"><span data-stu-id="f7894-253">**ProvisioningState** for hello extension should also show “Succeeded”.</span></span> 

<span data-ttu-id="f7894-254">Se non è installato o non è stato possibile toobe il provisioning, è possibile installarlo con hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="f7894-254">If it is not installed or failed toobe provisioned, you can install it with hello following command.</span></span> <span data-ttu-id="f7894-255">In aggiunta toohello VM nome e la risorsa gruppo, è necessario specificare anche area hello (**$region**) che la macchina virtuale si trova in.</span><span class="sxs-lookup"><span data-stu-id="f7894-255">In addition toohello VM name and resource group, you must also specify hello region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region 
```

### <span data-ttu-id="f7894-256"><a id="verifysettings"></a> Verificare le impostazioni correnti</span><span class="sxs-lookup"><span data-stu-id="f7894-256"><a id="verifysettings"></a> Verify current settings</span></span>
<span data-ttu-id="f7894-257">Se è abilitato il backup automatizzato durante il provisioning, è possibile utilizzare PowerShell toocheck la configurazione corrente.</span><span class="sxs-lookup"><span data-stu-id="f7894-257">If you enabled automated backup during provisioning, you can use PowerShell toocheck your current configuration.</span></span> <span data-ttu-id="f7894-258">Eseguire hello **Get AzureRmVMSqlServerExtension** comando ed esaminare hello **AutoBackupSettings** proprietà:</span><span class="sxs-lookup"><span data-stu-id="f7894-258">Run hello **Get-AzureRmVMSqlServerExtension** command and examine hello **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="f7894-259">È necessario ottenere seguente toohello simili di output:</span><span class="sxs-lookup"><span data-stu-id="f7894-259">You should get output similar toohello following:</span></span>

```
Enable                      : True
EnableEncryption            : False
RetentionPeriod             : 30
StorageUrl                  : https://test.blob.core.windows.net/
StorageAccessKey            :  
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : Manual
FullBackupFrequency         : WEEKLY
FullBackupStartTime         : 2
FullBackupWindowHours       : 2
LogBackupFrequency          : 60
```

<span data-ttu-id="f7894-260">Se l'output mostra che **abilitare** è troppo**False**, è necessario tooenable backup automatico.</span><span class="sxs-lookup"><span data-stu-id="f7894-260">If your output shows that **Enable** is set too**False**, then you have tooenable automated backup.</span></span> <span data-ttu-id="f7894-261">Hello buone notizie sono attivare e configurare il Backup automatizzato in hello allo stesso modo.</span><span class="sxs-lookup"><span data-stu-id="f7894-261">hello good news is that you enable and configure Automated Backup in hello same way.</span></span> <span data-ttu-id="f7894-262">Vedere hello sezione successiva per ottenere questa informazione.</span><span class="sxs-lookup"><span data-stu-id="f7894-262">See hello next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="f7894-263">Se si seleziona impostazioni hello immediatamente dopo aver apportato una modifica, è possibile che si otterranno nuovamente i valori di configurazione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="f7894-263">If you check hello settings immediately after making a change, it is possible that you will get back hello old configuration values.</span></span> <span data-ttu-id="f7894-264">Attendere alcuni minuti e verificare le impostazioni di hello nuovamente toomake assicurarsi che siano state applicate le modifiche.</span><span class="sxs-lookup"><span data-stu-id="f7894-264">Wait a few minutes and check hello settings again toomake sure that your changes were applied.</span></span>

### <a name="configure-automated-backup-v2"></a><span data-ttu-id="f7894-265">Configurare Backup automatico v2</span><span class="sxs-lookup"><span data-stu-id="f7894-265">Configure Automated Backup v2</span></span>
<span data-ttu-id="f7894-266">È possibile utilizzare PowerShell tooenable Backup automatizzato, nonché toomodify la configurazione e il comportamento in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="f7894-266">You can use PowerShell tooenable Automated Backup as well as toomodify its configuration and behavior at any time.</span></span> 

<span data-ttu-id="f7894-267">In primo luogo, selezionare o creare un account di archiviazione per hello i file di backup.</span><span class="sxs-lookup"><span data-stu-id="f7894-267">First, select or create a storage account for hello backup files.</span></span> <span data-ttu-id="f7894-268">Hello lo script seguente consente di selezionare un account di archiviazione o la crea se non esiste.</span><span class="sxs-lookup"><span data-stu-id="f7894-268">hello following script selects a storage account or creates it if it does not exist.</span></span>

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region } 
```

> [!NOTE]
> <span data-ttu-id="f7894-269">Backup automatico non supporta l'archiviazione di backup nell'archiviazione Premium, ma può ottenere i backup da dischi di macchine virtuali che usano l'archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="f7894-269">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="f7894-270">Utilizzare quindi hello **New AzureRmVMSqlServerAutoBackupConfig** comando tooenable e configurare i backup di toostore impostazioni hello v2 Backup automatizzato nell'account di archiviazione Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f7894-270">Then use hello **New-AzureRmVMSqlServerAutoBackupConfig** command tooenable and configure hello Automated Backup v2 settings toostore backups in hello Azure storage account.</span></span> <span data-ttu-id="f7894-271">In questo esempio, i backup di hello sono impostati toobe conservati per 10 giorni.</span><span class="sxs-lookup"><span data-stu-id="f7894-271">In this example, hello backups are set toobe retained for 10 days.</span></span> <span data-ttu-id="f7894-272">I backup del database di sistema sono abilitati.</span><span class="sxs-lookup"><span data-stu-id="f7894-272">System database backups are enabled.</span></span> <span data-ttu-id="f7894-273">I backup completi sono pianificati come settimanali, con un intervallo di tempo di due ore a partire dalle 20:00.</span><span class="sxs-lookup"><span data-stu-id="f7894-273">Full backups are scheduled for weekly with a time window starting at 20:00 for two hours.</span></span> <span data-ttu-id="f7894-274">I backup del log vengono eseguiti ogni 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="f7894-274">Log backups are scheduled for every 30 minutes.</span></span> <span data-ttu-id="f7894-275">Hello secondo comando, **Set AzureRmVMSqlServerExtension**, hello aggiornamenti specificato macchina virtuale di Azure con queste impostazioni.</span><span class="sxs-lookup"><span data-stu-id="f7894-275">hello second command, **Set-AzureRmVMSqlServerExtension**, updates hello specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname 
```

<span data-ttu-id="f7894-276">Potrebbe richiedere diversi minuti tooinstall e configurare hello agente IaaS di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f7894-276">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span> 

<span data-ttu-id="f7894-277">crittografia tooenable, modificare hello di hello precedente script toopass **EnableEncryption** parametro e una password (stringa sicura) per hello **CertificatePassword** parametro.</span><span class="sxs-lookup"><span data-stu-id="f7894-277">tooenable encryption, modify hello previous script toopass hello **EnableEncryption** parameter along with a password (secure string) for hello **CertificatePassword** parameter.</span></span> <span data-ttu-id="f7894-278">Hello seguente script abilita le impostazioni di Backup automatizzato hello nell'esempio precedente hello e aggiunge la crittografia.</span><span class="sxs-lookup"><span data-stu-id="f7894-278">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="f7894-279">le impostazioni vengono applicate, tooconfirm [verificare la configurazione di Backup automatizzato hello](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="f7894-279">tooconfirm your settings are applied, [verify hello Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="f7894-280">Disabilitare Backup automatico</span><span class="sxs-lookup"><span data-stu-id="f7894-280">Disable Automated Backup</span></span>
<span data-ttu-id="f7894-281">Backup automatizzato, esecuzione hello stesso script senza hello toodisable **-abilitare** parametro toohello **New AzureRmVMSqlServerAutoBackupConfig** comando.</span><span class="sxs-lookup"><span data-stu-id="f7894-281">toodisable Automated Backup, run hello same script without hello **-Enable** parameter toohello **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="f7894-282">assenza di hello Hello **-abilitare** funzionalità di parametro segnali hello comando toodisable hello.</span><span class="sxs-lookup"><span data-stu-id="f7894-282">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span> <span data-ttu-id="f7894-283">Come per l'installazione, può richiedere diversi minuti toodisable Backup automatizzato.</span><span class="sxs-lookup"><span data-stu-id="f7894-283">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="f7894-284">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="f7894-284">Example script</span></span>
<span data-ttu-id="f7894-285">Hello script riportato di seguito fornisce un set di variabili che è possibile personalizzare tooenable e configurare il Backup automatizzato per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f7894-285">hello following script provides a set of variables that you can customize tooenable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="f7894-286">Il caso, potrebbe essere necessario script hello toocustomize in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="f7894-286">In your case, you might need toocustomize hello script based on your requirements.</span></span> <span data-ttu-id="f7894-287">Ad esempio, si sarebbe sono state apportate modifiche toomake, se si desidera utilizzare backup hello toodisable dei database di sistema o abilitare la crittografia.</span><span class="sxs-lookup"><span data-stu-id="f7894-287">For example, you would have toomake changes if you wanted toodisable hello backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10
$backupscheduletype = "Manual"
$fullbackupfrequency = "Weekly"
$fullbackupstarthour = "20"
$fullbackupwindow = "2"
$logbackupfrequency = "30"

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension 

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="f7894-288">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f7894-288">Next steps</span></span>
<span data-ttu-id="f7894-289">Backup automatico v2 configura backup gestito in Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f7894-289">Automated Backup v2 configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="f7894-290">È importante troppo[, vedere la documentazione di hello per il Backup gestito](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello comportamento e le implicazioni.</span><span class="sxs-lookup"><span data-stu-id="f7894-290">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="f7894-291">È possibile trovare ulteriori backup e ripristino istruzioni for SQL Server in macchine virtuali di Azure nel seguente argomento hello: [di Backup e ripristino per SQL Server in macchine virtuali di Azure](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="f7894-291">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="f7894-292">Per informazioni sulle altre attività di automazione disponibili, vedere [Estensione Agente IaaS di SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="f7894-292">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="f7894-293">Per altre informazioni sull'esecuzione di SQL Server nelle VM di Azure, vedere [Panoramica di SQL Server nelle macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f7894-293">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

