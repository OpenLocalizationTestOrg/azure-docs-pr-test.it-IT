---
title: aaaBack backup un tooAzure di Exchange server Backup con il Server di Backup di Azure | Documenti Microsoft
description: Informazioni su come eseguire Backup tooback backup un tooAzure di Exchange server tramite il Server di Backup di Azure
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: e46557e8-2eaf-4ee0-99ea-00fbb8687dca
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: db874161151fc57c5b79c41531e18d577f567f66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-azure-backup-server"></a><span data-ttu-id="9d2f6-103">Eseguire il backup di un tooAzure di Exchange server con Server di Backup di Azure Backup</span><span class="sxs-lookup"><span data-stu-id="9d2f6-103">Back up an Exchange server tooAzure Backup with Azure Backup Server</span></span>
<span data-ttu-id="9d2f6-104">Questo articolo viene descritto come tooconfigure tooback di Microsoft Azure Backup Server (MABS) di un tooAzure di Microsoft Exchange server.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-104">This article describes how tooconfigure Microsoft Azure Backup Server (MABS) tooback up a Microsoft Exchange server tooAzure.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="9d2f6-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9d2f6-105">Prerequisites</span></span>
<span data-ttu-id="9d2f6-106">Prima di continuare, assicurarsi che il Server di Backup di Azure sia [installato e pronto](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="9d2f6-106">Before you continue, make sure that Azure Backup Server is [installed and prepared](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="mabs-protection-agent"></a><span data-ttu-id="9d2f6-107">Agente protezione MABS</span><span class="sxs-lookup"><span data-stu-id="9d2f6-107">MABS protection agent</span></span>
<span data-ttu-id="9d2f6-108">agente di protezione MABS hello tooinstall hello Exchange Server, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="9d2f6-108">tooinstall hello MABS protection agent on hello Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="9d2f6-109">Assicurarsi che i firewall hello siano configurati correttamente.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-109">Make sure that hello firewalls are correctly configured.</span></span> <span data-ttu-id="9d2f6-110">Vedere [configurare le eccezioni del firewall per l'agente di hello](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d2f6-110">See [Configure firewall exceptions for hello agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="9d2f6-111">Installare l'agente di hello sul server Exchange hello facendo **gestione > agenti > installare** nella Console di amministrazione di MABS.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-111">Install hello agent on hello Exchange server by clicking **Management > Agents > Install** in MABS Administrator Console.</span></span> <span data-ttu-id="9d2f6-112">Vedere [agente protezione di installazione hello MABS](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) per i passaggi dettagliati.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-112">See [Install hello MABS protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-hello-exchange-server"></a><span data-ttu-id="9d2f6-113">Creare un gruppo protezione dati per il server di Exchange hello</span><span class="sxs-lookup"><span data-stu-id="9d2f6-113">Create a protection group for hello Exchange server</span></span>
1. <span data-ttu-id="9d2f6-114">Nella Console di amministrazione MABS hello, fare clic su **protezione**, quindi fare clic su **New** su hello tooopen della barra multifunzione dello strumento di hello **Crea nuovo gruppo protezione dati** procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-114">In hello MABS Administrator Console, click **Protection**, and then click **New** on hello tool ribbon tooopen hello **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="9d2f6-115">In hello **iniziale** schermata di hello guidata fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-115">On hello **Welcome** screen of hello wizard click **Next**.</span></span>
3. <span data-ttu-id="9d2f6-116">In hello **Seleziona tipo di gruppo protezione dati** selezionare **server** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-116">On hello **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="9d2f6-117">Database del server Exchange hello selezionare tooprotect desiderati e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-117">Select hello Exchange server database that you want tooprotect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9d2f6-118">Se si desidera proteggere Exchange 2013, controllare hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d2f6-118">If you are protecting Exchange 2013, check hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="9d2f6-119">Nell'esempio seguente di hello, è selezionato il database di Exchange 2010 hello.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-119">In hello following example, hello Exchange 2010 database is selected.</span></span>

    ![Seleziona membri del gruppo](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="9d2f6-121">Selezionare il metodo di protezione dati hello.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-121">Select hello data protection method.</span></span>

    <span data-ttu-id="9d2f6-122">Nome gruppo di protezione dati hello e quindi selezionare entrambi hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9d2f6-122">Name hello protection group, and then select both of hello following options:</span></span>

   * <span data-ttu-id="9d2f6-123">Protezione dati breve termine tramite: Disco.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-123">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="9d2f6-124">Protezione dati online.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-124">I want online protection.</span></span>
6. <span data-ttu-id="9d2f6-125">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-125">Click **Next**.</span></span>
7. <span data-ttu-id="9d2f6-126">Seleziona hello **l'integrità dei dati di esecuzione di Eseutil toocheck** opzione se si desidera integrità hello toocheck dei database di Exchange Server hello.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-126">Select hello **Run Eseutil toocheck data integrity** option if you want toocheck hello integrity of hello Exchange Server databases.</span></span>

    <span data-ttu-id="9d2f6-127">Dopo aver selezionato questa opzione, la verifica della coerenza del backup verrà eseguita in MABS tooavoid hello i/o il traffico che viene generato eseguendo hello **eseutil** comando sul server Exchange hello.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-127">After you select this option, backup consistency checking will be run on MABS tooavoid hello I/O traffic that’s generated by running hello **eseutil** command on hello Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9d2f6-128">toouse questa opzione, è necessario copiare hello Ese.dll ed Eseutil.exe directory C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin toohello dei file nel server MAB hello.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-128">toouse this option, you must copy hello Ese.dll and Eseutil.exe files toohello C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin directory on hello MAB server.</span></span> <span data-ttu-id="9d2f6-129">In caso contrario, viene attivato hello errore seguente:</span><span class="sxs-lookup"><span data-stu-id="9d2f6-129">Otherwise, hello following error is triggered:</span></span>  
   > <span data-ttu-id="9d2f6-130">![Errore di Eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="9d2f6-130">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="9d2f6-131">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-131">Click **Next**.</span></span>
9. <span data-ttu-id="9d2f6-132">Database selezionare hello per **Backup di copia**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-132">Select hello database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9d2f6-133">Se non si seleziona "Backup completo" per almeno una copia del gruppo di disponibilità dei database di un database, i registri non verranno troncati.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-133">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="9d2f6-134">Configurare gli obiettivi di hello per **backup a breve termine**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-134">Configure hello goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="9d2f6-135">Esaminare lo spazio disponibile su disco hello e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-135">Review hello available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="9d2f6-136">Selezionare hello ora in cui hello MAB Server Creazione replica iniziale hello e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-136">Select hello time at which hello MAB Server will create hello initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="9d2f6-137">Selezionare opzioni di verifica coerenza hello e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-137">Select hello consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="9d2f6-138">Scegliere hello database che desidera tooback backup tooAzure e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-138">Choose hello database that you want tooback up tooAzure, and then click **Next**.</span></span> <span data-ttu-id="9d2f6-139">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="9d2f6-139">For example:</span></span>

    ![Specifica i dati da proteggere online](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="9d2f6-141">Definire la pianificazione hello per **Azure Backup**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-141">Define hello schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="9d2f6-142">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="9d2f6-142">For example:</span></span>

    ![Specificare la pianificazione dei backup online](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="9d2f6-144">Tenere presente che i punti di ripristino online sono basati sui punti di ripristino di backup completo rapido.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-144">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="9d2f6-145">Pertanto, è necessario pianificare il punto di ripristino online hello dopo hello periodo di tempo specificato per hello express punto di recupero con registrazione completa.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-145">Therefore, you must schedule hello online recovery point after hello time that’s specified for hello express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="9d2f6-146">Configurare i criteri di conservazione hello **Azure Backup**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-146">Configure hello retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="9d2f6-147">Scegliere un'opzione di replica online e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-147">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="9d2f6-148">Se si dispone di un database di grandi dimensioni, potrebbero richiedere molto tempo per hello iniziale toobe backup creati tramite rete hello.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-148">If you have a large database, it could take a long time for hello initial backup toobe created over hello network.</span></span> <span data-ttu-id="9d2f6-149">tooavoid questo problema, è possibile creare un backup offline.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-149">tooavoid this issue, you can create an offline backup.</span></span>  

    ![Specificare i criteri di mantenimento online](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="9d2f6-151">Confermare le impostazioni di hello e quindi fare clic su **Crea gruppo**.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-151">Confirm hello settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="9d2f6-152">Fare clic su **Close**.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-152">Click **Close**.</span></span>

## <a name="recover-hello-exchange-database"></a><span data-ttu-id="9d2f6-153">Ripristinare il database di Exchange hello</span><span class="sxs-lookup"><span data-stu-id="9d2f6-153">Recover hello Exchange database</span></span>
1. <span data-ttu-id="9d2f6-154">Fare clic su un database di Exchange, toorecover **ripristino** nella Console di amministrazione MABS hello.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-154">toorecover an Exchange database, click **Recovery** in hello MABS Administrator Console.</span></span>
2. <span data-ttu-id="9d2f6-155">Individuare il database di Exchange hello che si desidera toorecover.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-155">Locate hello Exchange database that you want toorecover.</span></span>
3. <span data-ttu-id="9d2f6-156">Selezionare un punto di ripristino in linea da hello *tempo di recupero* elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-156">Select an online recovery point from hello *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="9d2f6-157">Fare clic su **ripristinare** toostart hello **ripristino guidato**.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-157">Click **Recover** toostart hello **Recovery Wizard**.</span></span>

<span data-ttu-id="9d2f6-158">Per i punti di ripristino online sono disponibili cinque tipi:</span><span class="sxs-lookup"><span data-stu-id="9d2f6-158">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="9d2f6-159">**Ripristinare il percorso di Exchange Server toooriginal:** dati hello sarà ripristinato toohello originale Exchange server.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-159">**Recover toooriginal Exchange Server location:** hello data will be recovered toohello original Exchange server.</span></span>
* <span data-ttu-id="9d2f6-160">**Ripristinare il database tooanother su un Server Exchange:** dati hello sarà ripristinato tooanother database in un altro server di Exchange.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-160">**Recover tooanother database on an Exchange Server:** hello data will be recovered tooanother database on another Exchange server.</span></span>
* <span data-ttu-id="9d2f6-161">**Ripristinare i Database di ripristino tooa:** dati hello sarà ripristinato tooan Exchange ripristino Database (RDB).</span><span class="sxs-lookup"><span data-stu-id="9d2f6-161">**Recover tooa Recovery Database:** hello data will be recovered tooan Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="9d2f6-162">**Cartella di rete copia tooa:** dati hello sarà ripristinato tooa cartella di rete.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-162">**Copy tooa network folder:** hello data will be recovered tooa network folder.</span></span>
* <span data-ttu-id="9d2f6-163">**Copiare tootape:** se si dispone di una libreria di nastri o un'unità nastro autonoma associata e configurato in MABS, il punto di ripristino hello saranno copiati tooa nastro.</span><span class="sxs-lookup"><span data-stu-id="9d2f6-163">**Copy tootape:** If you have a tape library or a stand-alone tape drive attached and configured on MABS, hello recovery point will be copied tooa free tape.</span></span>

    ![Scegliere la replica online](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="9d2f6-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9d2f6-165">Next steps</span></span>
* [<span data-ttu-id="9d2f6-166">Backup di Azure - Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="9d2f6-166">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
