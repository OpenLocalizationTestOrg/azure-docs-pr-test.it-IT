---
title: aaaBack backup un tooAzure di Exchange server Backup con System Center 2012 R2 DPM | Documenti Microsoft
description: Informazioni su come eseguire Backup tooback backup un tooAzure di Exchange server con System Center 2012 R2 DPM
services: backup
documentationcenter: 
author: MaanasSaran
manager: NKolli1
editor: 
ms.assetid: 13f32256-888e-416e-a78b-40c2a26a5939
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: masaran;jimpark;delhan;trinadhk;markgal
ms.openlocfilehash: fa99296d095c180333474b6d419ebc5ec727547a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-system-center-2012-r2-dpm"></a><span data-ttu-id="75afd-103">Eseguire il backup di un tooAzure di Exchange server Backup con System Center 2012 R2 DPM</span><span class="sxs-lookup"><span data-stu-id="75afd-103">Back up an Exchange server tooAzure Backup with System Center 2012 R2 DPM</span></span>
<span data-ttu-id="75afd-104">Questo articolo viene descritto come tooconfigure un tooback server System Center 2012 R2 Data Protection Manager (DPM) di un server di Microsoft Exchange troppo Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="75afd-104">This article describes how tooconfigure a System Center 2012 R2 Data Protection Manager (DPM) server tooback up a Microsoft Exchange server too Azure Backup.</span></span>  

## <a name="updates"></a><span data-ttu-id="75afd-105">Aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="75afd-105">Updates</span></span>
<span data-ttu-id="75afd-106">toosuccessfully registro hello DPM server con Backup di Azure, è necessario installare hello ultimo aggiornamento cumulativo per System Center 2012 R2 DPM e hello versione più recente di hello Azure Backup Agent.</span><span class="sxs-lookup"><span data-stu-id="75afd-106">toosuccessfully register hello DPM server with Azure Backup, you must install hello latest update rollup for System Center 2012 R2 DPM and hello latest version of hello Azure Backup Agent.</span></span> <span data-ttu-id="75afd-107">Ottenere l'aggiornamento cumulativo più recente di hello da hello [catalogo Microsoft](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span><span class="sxs-lookup"><span data-stu-id="75afd-107">Get hello latest update rollup from hello [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span></span>

> [!NOTE]
> <span data-ttu-id="75afd-108">Per esempi di hello in questo articolo, è installata la versione 2.0.8719.0 di hello Azure Backup Agent e aggiornamento cumulativo 6 è installato System Center 2012 R2 DPM.</span><span class="sxs-lookup"><span data-stu-id="75afd-108">For hello examples in this article, version 2.0.8719.0 of hello Azure Backup Agent is installed, and Update Rollup 6 is installed on System Center 2012 R2 DPM.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="75afd-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="75afd-109">Prerequisites</span></span>
<span data-ttu-id="75afd-110">Prima di continuare, assicurarsi che tutti hello [prerequisiti](backup-azure-dpm-introduction.md#prerequisites) per l'utilizzo di Microsoft Azure Backup tooprotect i carichi di lavoro sono stati soddisfatti.</span><span class="sxs-lookup"><span data-stu-id="75afd-110">Before you continue, make sure that all hello [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup tooprotect workloads have been met.</span></span> <span data-ttu-id="75afd-111">Questi prerequisiti includono l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="75afd-111">These prerequisites include hello following:</span></span>

* <span data-ttu-id="75afd-112">È stato creato un insieme di credenziali di backup nel sito di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="75afd-112">A backup vault on hello Azure site has been created.</span></span>
* <span data-ttu-id="75afd-113">Le credenziali dell'agente e l'insieme di credenziali sono state server DPM toohello scaricato.</span><span class="sxs-lookup"><span data-stu-id="75afd-113">Agent and vault credentials have been downloaded toohello DPM server.</span></span>
* <span data-ttu-id="75afd-114">Hello agente è installato nel server DPM hello.</span><span class="sxs-lookup"><span data-stu-id="75afd-114">hello agent is installed on hello DPM server.</span></span>
* <span data-ttu-id="75afd-115">insieme di credenziali Hello erano server DPM di hello tooregister utilizzato.</span><span class="sxs-lookup"><span data-stu-id="75afd-115">hello vault credentials were used tooregister hello DPM server.</span></span>
* <span data-ttu-id="75afd-116">Se si desidera proteggere Exchange 2016, eseguire l'aggiornamento tooDPM 2012 R2 UR9 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="75afd-116">If you are protecting Exchange 2016, please upgrade tooDPM 2012 R2 UR9 or later</span></span>

## <a name="dpm-protection-agent"></a><span data-ttu-id="75afd-117">Agente protezione DPM</span><span class="sxs-lookup"><span data-stu-id="75afd-117">DPM protection agent</span></span>
<span data-ttu-id="75afd-118">agente di protezione di DPM tooinstall hello hello Exchange Server, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="75afd-118">tooinstall hello DPM protection agent on hello Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="75afd-119">Assicurarsi che i firewall hello siano configurati correttamente.</span><span class="sxs-lookup"><span data-stu-id="75afd-119">Make sure that hello firewalls are correctly configured.</span></span> <span data-ttu-id="75afd-120">Vedere [configurare le eccezioni del firewall per l'agente di hello](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="75afd-120">See [Configure firewall exceptions for hello agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="75afd-121">Installare l'agente di hello sul server Exchange hello facendo **gestione > agenti > installare** nella Console amministrazione DPM.</span><span class="sxs-lookup"><span data-stu-id="75afd-121">Install hello agent on hello Exchange server by clicking **Management > Agents > Install** in DPM Administrator Console.</span></span> <span data-ttu-id="75afd-122">Vedere [agente protezione DPM di installare hello](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) per i passaggi dettagliati.</span><span class="sxs-lookup"><span data-stu-id="75afd-122">See [Install hello DPM protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-hello-exchange-server"></a><span data-ttu-id="75afd-123">Creare un gruppo protezione dati per il server di Exchange hello</span><span class="sxs-lookup"><span data-stu-id="75afd-123">Create a protection group for hello Exchange server</span></span>
1. <span data-ttu-id="75afd-124">Nella Console amministrazione DPM hello, fare clic su **protezione**e quindi fare clic su **New** su hello tooopen della barra multifunzione dello strumento di hello **Crea nuovo gruppo protezione dati** procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="75afd-124">In hello DPM Administrator Console, click **Protection**, and then click **New** on hello tool ribbon tooopen hello **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="75afd-125">In hello **iniziale** schermata di hello guidata fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="75afd-125">On hello **Welcome** screen of hello wizard click **Next**.</span></span>
3. <span data-ttu-id="75afd-126">In hello **Seleziona tipo di gruppo protezione dati** selezionare **server** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="75afd-126">On hello **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="75afd-127">Database del server Exchange hello selezionare tooprotect desiderati e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="75afd-127">Select hello Exchange server database that you want tooprotect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="75afd-128">Se si desidera proteggere Exchange 2013, controllare hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="75afd-128">If you are protecting Exchange 2013, check hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="75afd-129">Nell'esempio seguente di hello, è selezionato il database di Exchange 2010 hello.</span><span class="sxs-lookup"><span data-stu-id="75afd-129">In hello following example, hello Exchange 2010 database is selected.</span></span>

    ![Seleziona membri del gruppo](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="75afd-131">Selezionare il metodo di protezione dati hello.</span><span class="sxs-lookup"><span data-stu-id="75afd-131">Select hello data protection method.</span></span>

    <span data-ttu-id="75afd-132">Nome gruppo di protezione dati hello e quindi selezionare entrambi hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="75afd-132">Name hello protection group, and then select both of hello following options:</span></span>

   * <span data-ttu-id="75afd-133">Protezione dati breve termine tramite: Disco.</span><span class="sxs-lookup"><span data-stu-id="75afd-133">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="75afd-134">Protezione dati online.</span><span class="sxs-lookup"><span data-stu-id="75afd-134">I want online protection.</span></span>
6. <span data-ttu-id="75afd-135">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="75afd-135">Click **Next**.</span></span>
7. <span data-ttu-id="75afd-136">Seleziona hello **l'integrità dei dati di esecuzione di Eseutil toocheck** opzione se si desidera integrità hello toocheck dei database di Exchange Server hello.</span><span class="sxs-lookup"><span data-stu-id="75afd-136">Select hello **Run Eseutil toocheck data integrity** option if you want toocheck hello integrity of hello Exchange Server databases.</span></span>

    <span data-ttu-id="75afd-137">Dopo aver selezionato questa opzione, la verifica della coerenza del backup deve essere eseguita su hello DPM server tooavoid hello i/o il traffico generato eseguendo hello **eseutil** comando sul server Exchange hello.</span><span class="sxs-lookup"><span data-stu-id="75afd-137">After you select this option, backup consistency checking will be run on hello DPM server tooavoid hello I/O traffic that’s generated by running hello **eseutil** command on hello Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="75afd-138">toouse questa opzione, è necessario copiare hello Ese.dll ed Eseutil.exe directory C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin toohello dei file nel server DPM hello.</span><span class="sxs-lookup"><span data-stu-id="75afd-138">toouse this option, you must copy hello Ese.dll and Eseutil.exe files toohello C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin directory on hello DPM server.</span></span> <span data-ttu-id="75afd-139">In caso contrario, viene attivato hello errore seguente:</span><span class="sxs-lookup"><span data-stu-id="75afd-139">Otherwise, hello following error is triggered:</span></span>  
   > <span data-ttu-id="75afd-140">![Errore di Eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="75afd-140">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="75afd-141">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="75afd-141">Click **Next**.</span></span>
9. <span data-ttu-id="75afd-142">Database selezionare hello per **Backup di copia**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="75afd-142">Select hello database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="75afd-143">Se non si seleziona "Backup completo" per almeno una copia del gruppo di disponibilità dei database di un database, i registri non verranno troncati.</span><span class="sxs-lookup"><span data-stu-id="75afd-143">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="75afd-144">Configurare gli obiettivi di hello per **backup a breve termine**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="75afd-144">Configure hello goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="75afd-145">Esaminare lo spazio disponibile su disco hello e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="75afd-145">Review hello available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="75afd-146">Selezionare hello ora in cui DPM hello server Creazione replica iniziale hello e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="75afd-146">Select hello time at which hello DPM server will create hello initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="75afd-147">Selezionare opzioni di verifica coerenza hello e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="75afd-147">Select hello consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="75afd-148">Scegliere hello database che desidera tooback backup tooAzure e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="75afd-148">Choose hello database that you want tooback up tooAzure, and then click **Next**.</span></span> <span data-ttu-id="75afd-149">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="75afd-149">For example:</span></span>

    ![Specifica i dati da proteggere online](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="75afd-151">Definire la pianificazione hello per **Azure Backup**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="75afd-151">Define hello schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="75afd-152">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="75afd-152">For example:</span></span>

    ![Specificare la pianificazione dei backup online](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="75afd-154">Tenere presente che i punti di ripristino online sono basati sui punti di ripristino di backup completo rapido.</span><span class="sxs-lookup"><span data-stu-id="75afd-154">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="75afd-155">Pertanto, è necessario pianificare il punto di ripristino online hello dopo hello periodo di tempo specificato per hello express punto di recupero con registrazione completa.</span><span class="sxs-lookup"><span data-stu-id="75afd-155">Therefore, you must schedule hello online recovery point after hello time that’s specified for hello express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="75afd-156">Configurare i criteri di conservazione hello **Azure Backup**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="75afd-156">Configure hello retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="75afd-157">Scegliere un'opzione di replica online e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="75afd-157">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="75afd-158">Se si dispone di un database di grandi dimensioni, potrebbero richiedere molto tempo per hello iniziale toobe backup creati tramite rete hello.</span><span class="sxs-lookup"><span data-stu-id="75afd-158">If you have a large database, it could take a long time for hello initial backup toobe created over hello network.</span></span> <span data-ttu-id="75afd-159">tooavoid questo problema, è possibile creare un backup offline.</span><span class="sxs-lookup"><span data-stu-id="75afd-159">tooavoid this issue, you can create an offline backup.</span></span>  

    ![Specificare i criteri di mantenimento online](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="75afd-161">Confermare le impostazioni di hello e quindi fare clic su **Crea gruppo**.</span><span class="sxs-lookup"><span data-stu-id="75afd-161">Confirm hello settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="75afd-162">Fare clic su **Close**.</span><span class="sxs-lookup"><span data-stu-id="75afd-162">Click **Close**.</span></span>

## <a name="recover-hello-exchange-database"></a><span data-ttu-id="75afd-163">Ripristinare il database di Exchange hello</span><span class="sxs-lookup"><span data-stu-id="75afd-163">Recover hello Exchange database</span></span>
1. <span data-ttu-id="75afd-164">Fare clic su un database di Exchange, toorecover **ripristino** nella Console amministrazione DPM hello.</span><span class="sxs-lookup"><span data-stu-id="75afd-164">toorecover an Exchange database, click **Recovery** in hello DPM Administrator Console.</span></span>
2. <span data-ttu-id="75afd-165">Individuare il database di Exchange hello che si desidera toorecover.</span><span class="sxs-lookup"><span data-stu-id="75afd-165">Locate hello Exchange database that you want toorecover.</span></span>
3. <span data-ttu-id="75afd-166">Selezionare un punto di ripristino in linea da hello *tempo di recupero* elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="75afd-166">Select an online recovery point from hello *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="75afd-167">Fare clic su **ripristinare** toostart hello **ripristino guidato**.</span><span class="sxs-lookup"><span data-stu-id="75afd-167">Click **Recover** toostart hello **Recovery Wizard**.</span></span>

<span data-ttu-id="75afd-168">Per i punti di ripristino online sono disponibili cinque tipi:</span><span class="sxs-lookup"><span data-stu-id="75afd-168">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="75afd-169">**Ripristinare il percorso di Exchange Server toooriginal:** dati hello sarà ripristinato toohello originale Exchange server.</span><span class="sxs-lookup"><span data-stu-id="75afd-169">**Recover toooriginal Exchange Server location:** hello data will be recovered toohello original Exchange server.</span></span>
* <span data-ttu-id="75afd-170">**Ripristinare il database tooanother su un Server Exchange:** dati hello sarà ripristinato tooanother database in un altro server di Exchange.</span><span class="sxs-lookup"><span data-stu-id="75afd-170">**Recover tooanother database on an Exchange Server:** hello data will be recovered tooanother database on another Exchange server.</span></span>
* <span data-ttu-id="75afd-171">**Ripristinare i Database di ripristino tooa:** dati hello sarà ripristinato tooan Exchange ripristino Database (RDB).</span><span class="sxs-lookup"><span data-stu-id="75afd-171">**Recover tooa Recovery Database:** hello data will be recovered tooan Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="75afd-172">**Cartella di rete copia tooa:** dati hello sarà ripristinato tooa cartella di rete.</span><span class="sxs-lookup"><span data-stu-id="75afd-172">**Copy tooa network folder:** hello data will be recovered tooa network folder.</span></span>
* <span data-ttu-id="75afd-173">**Copiare tootape:** se si dispone di una libreria di nastri o un'unità nastro autonoma hello collegato e configurato nel server DPM, il punto di ripristino hello saranno copiati tooa nastro.</span><span class="sxs-lookup"><span data-stu-id="75afd-173">**Copy tootape:** If you have a tape library or a stand-alone tape drive attached and configured on hello DPM server, hello recovery point will be copied tooa free tape.</span></span>

    ![Scegliere la replica online](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="75afd-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="75afd-175">Next steps</span></span>
* [<span data-ttu-id="75afd-176">Backup di Azure - Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="75afd-176">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
