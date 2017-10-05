---
title: Eseguire il backup di un server di Exchange in Backup di Azure con il server di Backup di Azure | Documentazione Microsoft
description: Informazioni su come eseguire il backup di un server di Exchange in Backup di Azure con il server di Backup di Azure
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
ms.openlocfilehash: 60b784fd00013c2b9504f8635c6b5c4c592563be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-an-exchange-server-to-azure-backup-with-azure-backup-server"></a><span data-ttu-id="7b9de-103">Eseguire il backup di un server Exchange in Backup di Azure con il server di Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="7b9de-103">Back up an Exchange server to Azure Backup with Azure Backup Server</span></span>
<span data-ttu-id="7b9de-104">Questo articolo descrive come configurare il server di Backup di Microsoft Azure (MABS) per eseguire il backup di un server Microsoft Exchange in Azure.</span><span class="sxs-lookup"><span data-stu-id="7b9de-104">This article describes how to configure Microsoft Azure Backup Server (MABS) to back up a Microsoft Exchange server to Azure.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="7b9de-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7b9de-105">Prerequisites</span></span>
<span data-ttu-id="7b9de-106">Prima di continuare, assicurarsi che il Server di Backup di Azure sia [installato e pronto](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="7b9de-106">Before you continue, make sure that Azure Backup Server is [installed and prepared](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="mabs-protection-agent"></a><span data-ttu-id="7b9de-107">Agente protezione MABS</span><span class="sxs-lookup"><span data-stu-id="7b9de-107">MABS protection agent</span></span>
<span data-ttu-id="7b9de-108">Per installare l'agente protezione MABS nel server di Exchange, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="7b9de-108">To install the MABS protection agent on the Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="7b9de-109">Assicurarsi che i firewall siano configurati correttamente.</span><span class="sxs-lookup"><span data-stu-id="7b9de-109">Make sure that the firewalls are correctly configured.</span></span> <span data-ttu-id="7b9de-110">Vedere [Configurare le eccezioni del firewall per l'agente](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b9de-110">See [Configure firewall exceptions for the agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="7b9de-111">Per installare l'agente nel server di Exchange, fare clic su **Gestione > Agenti > Installa** nella Console amministrazione MABS.</span><span class="sxs-lookup"><span data-stu-id="7b9de-111">Install the agent on the Exchange server by clicking **Management > Agents > Install** in MABS Administrator Console.</span></span> <span data-ttu-id="7b9de-112">Per la procedura dettagliata, vedere [Installare l'agente protezione MABS](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) .</span><span class="sxs-lookup"><span data-stu-id="7b9de-112">See [Install the MABS protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-the-exchange-server"></a><span data-ttu-id="7b9de-113">Creare un gruppo di protezione per il server di Exchange</span><span class="sxs-lookup"><span data-stu-id="7b9de-113">Create a protection group for the Exchange server</span></span>
1. <span data-ttu-id="7b9de-114">Nella Console amministrazione MABS fare clic su **Protezione** e quindi fare clic su **Nuovo** nella barra multifunzione per aprire la procedura guidata **Crea nuovo gruppo protezione dati**.</span><span class="sxs-lookup"><span data-stu-id="7b9de-114">In the MABS Administrator Console, click **Protection**, and then click **New** on the tool ribbon to open the **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="7b9de-115">Nella schermata **iniziale** della procedura guidata fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="7b9de-115">On the **Welcome** screen of the wizard click **Next**.</span></span>
3. <span data-ttu-id="7b9de-116">Nella schermata **Selezione tipo di gruppo protezione dati** selezionare **Server** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="7b9de-116">On the **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="7b9de-117">Selezionare il database di Exchange Server che si vuole proteggere e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="7b9de-117">Select the Exchange server database that you want to protect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7b9de-118">Se si vuole proteggere Exchange 2013, controllare i [Prerequisiti di Exchange 2013](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b9de-118">If you are protecting Exchange 2013, check the [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="7b9de-119">Nell'esempio seguente è selezionato il database di Exchange 2010.</span><span class="sxs-lookup"><span data-stu-id="7b9de-119">In the following example, the Exchange 2010 database is selected.</span></span>

    ![Seleziona membri del gruppo](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="7b9de-121">Selezionare il metodo di protezione dati.</span><span class="sxs-lookup"><span data-stu-id="7b9de-121">Select the data protection method.</span></span>

    <span data-ttu-id="7b9de-122">Assegnare un nome al gruppo protezione dati e quindi selezionare entrambe le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7b9de-122">Name the protection group, and then select both of the following options:</span></span>

   * <span data-ttu-id="7b9de-123">Protezione dati breve termine tramite: Disco.</span><span class="sxs-lookup"><span data-stu-id="7b9de-123">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="7b9de-124">Protezione dati online.</span><span class="sxs-lookup"><span data-stu-id="7b9de-124">I want online protection.</span></span>
6. <span data-ttu-id="7b9de-125">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="7b9de-125">Click **Next**.</span></span>
7. <span data-ttu-id="7b9de-126">Selezionare l'opzione **Esegui Eseutil per controllare l'integrità dei dati** se si vuole controllare l'integrità dei database di Exchange Server.</span><span class="sxs-lookup"><span data-stu-id="7b9de-126">Select the **Run Eseutil to check data integrity** option if you want to check the integrity of the Exchange Server databases.</span></span>

    <span data-ttu-id="7b9de-127">Dopo aver selezionato questa opzione, la verifica coerenza del backup verrà eseguito in MABS per evitare il traffico di I/O che viene generato eseguendo il comando **eseutil** sul server di Exchange.</span><span class="sxs-lookup"><span data-stu-id="7b9de-127">After you select this option, backup consistency checking will be run on MABS to avoid the I/O traffic that’s generated by running the **eseutil** command on the Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7b9de-128">Per usare questa opzione, è necessario copiare i file Ese.dll and Eseutil.exe nella directory C:\Programmi\Microsoft Azure Backup\DPM\DPM\bin nel server MAB.</span><span class="sxs-lookup"><span data-stu-id="7b9de-128">To use this option, you must copy the Ese.dll and Eseutil.exe files to the C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin directory on the MAB server.</span></span> <span data-ttu-id="7b9de-129">In caso contrario, viene generato l'errore seguente: </span><span class="sxs-lookup"><span data-stu-id="7b9de-129">Otherwise, the following error is triggered:</span></span>  
   > <span data-ttu-id="7b9de-130">![Errore di Eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="7b9de-130">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="7b9de-131">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="7b9de-131">Click **Next**.</span></span>
9. <span data-ttu-id="7b9de-132">Selezionare il database per **Backup di copia**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="7b9de-132">Select the database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7b9de-133">Se non si seleziona "Backup completo" per almeno una copia del gruppo di disponibilità dei database di un database, i registri non verranno troncati.</span><span class="sxs-lookup"><span data-stu-id="7b9de-133">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="7b9de-134">Configurare gli obiettivi per **Backup a breve termine**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="7b9de-134">Configure the goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="7b9de-135">Controllare lo spazio disponibile su disco e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="7b9de-135">Review the available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="7b9de-136">Selezionare l'ora in cui il server MAB dovrà creare la replica iniziale e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="7b9de-136">Select the time at which the MAB Server will create the initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="7b9de-137">Selezionare le opzioni di verifica coerenza e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="7b9de-137">Select the consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="7b9de-138">Scegliere il database di cui si vuole eseguire il backup in Azure e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="7b9de-138">Choose the database that you want to back up to Azure, and then click **Next**.</span></span> <span data-ttu-id="7b9de-139">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="7b9de-139">For example:</span></span>

    ![Specifica i dati da proteggere online](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="7b9de-141">Definire la pianificazione per **Backup di Azure**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="7b9de-141">Define the schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="7b9de-142">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="7b9de-142">For example:</span></span>

    ![Specificare la pianificazione dei backup online](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="7b9de-144">Tenere presente che i punti di ripristino online sono basati sui punti di ripristino di backup completo rapido.</span><span class="sxs-lookup"><span data-stu-id="7b9de-144">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="7b9de-145">È quindi necessario pianificare il punto di ripristino in linea dopo il tempo specificato per il punto di ripristino di backup completo rapido.</span><span class="sxs-lookup"><span data-stu-id="7b9de-145">Therefore, you must schedule the online recovery point after the time that’s specified for the express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="7b9de-146">Configurare i criteri di conservazione per **Backup di Azure**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="7b9de-146">Configure the retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="7b9de-147">Scegliere un'opzione di replica online e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="7b9de-147">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="7b9de-148">Un database di grandi dimensioni potrebbe richiedere molto tempo per creare il backup iniziale in rete.</span><span class="sxs-lookup"><span data-stu-id="7b9de-148">If you have a large database, it could take a long time for the initial backup to be created over the network.</span></span> <span data-ttu-id="7b9de-149">Per evitare questo problema, è possibile creare un backup offline.</span><span class="sxs-lookup"><span data-stu-id="7b9de-149">To avoid this issue, you can create an offline backup.</span></span>  

    ![Specificare i criteri di mantenimento online](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="7b9de-151">Verificare le impostazioni e quindi fare clic su **Crea gruppo**.</span><span class="sxs-lookup"><span data-stu-id="7b9de-151">Confirm the settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="7b9de-152">Fare clic su **Close**.</span><span class="sxs-lookup"><span data-stu-id="7b9de-152">Click **Close**.</span></span>

## <a name="recover-the-exchange-database"></a><span data-ttu-id="7b9de-153">Ripristinare il database di Exchange</span><span class="sxs-lookup"><span data-stu-id="7b9de-153">Recover the Exchange database</span></span>
1. <span data-ttu-id="7b9de-154">Per ripristinare un database di Exchange, fare clic su **Ripristino** nella Console amministrazione MAB.</span><span class="sxs-lookup"><span data-stu-id="7b9de-154">To recover an Exchange database, click **Recovery** in the MABS Administrator Console.</span></span>
2. <span data-ttu-id="7b9de-155">Individuare il database di Exchange che si vuole ripristinare.</span><span class="sxs-lookup"><span data-stu-id="7b9de-155">Locate the Exchange database that you want to recover.</span></span>
3. <span data-ttu-id="7b9de-156">Selezionare un punto di ripristino online dall'elenco a discesa *Ora ripristino* .</span><span class="sxs-lookup"><span data-stu-id="7b9de-156">Select an online recovery point from the *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="7b9de-157">Fare clic su **Ripristina** per avviare il **Ripristino guidato**.</span><span class="sxs-lookup"><span data-stu-id="7b9de-157">Click **Recover** to start the **Recovery Wizard**.</span></span>

<span data-ttu-id="7b9de-158">Per i punti di ripristino online sono disponibili cinque tipi:</span><span class="sxs-lookup"><span data-stu-id="7b9de-158">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="7b9de-159">**Ripristina nel percorso originale di Exchange Server:** i dati verranno ripristinati nel server di Exchange originale.</span><span class="sxs-lookup"><span data-stu-id="7b9de-159">**Recover to original Exchange Server location:** The data will be recovered to the original Exchange server.</span></span>
* <span data-ttu-id="7b9de-160">**Ripristina in un altro database in un Server di Exchange:** i dati verranno ripristinati in un altro database in un altro server di Exchange.</span><span class="sxs-lookup"><span data-stu-id="7b9de-160">**Recover to another database on an Exchange Server:** The data will be recovered to another database on another Exchange server.</span></span>
* <span data-ttu-id="7b9de-161">**Ripristina in un database di ripristino:** i dati verranno ripristinati in un database di ripristino di Exchange (RDB).</span><span class="sxs-lookup"><span data-stu-id="7b9de-161">**Recover to a Recovery Database:** The data will be recovered to an Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="7b9de-162">**Copia in una cartella di rete:** i dati verranno ripristinati in una cartella di rete.</span><span class="sxs-lookup"><span data-stu-id="7b9de-162">**Copy to a network folder:** The data will be recovered to a network folder.</span></span>
* <span data-ttu-id="7b9de-163">**Copia su nastro:** se si ha una libreria di nastri o un'unità nastro autonoma collegata e configurata in MABS, il punto di recupero verrà copiato su un nastro disponibile.</span><span class="sxs-lookup"><span data-stu-id="7b9de-163">**Copy to tape:** If you have a tape library or a stand-alone tape drive attached and configured on MABS, the recovery point will be copied to a free tape.</span></span>

    ![Scegliere la replica online](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="7b9de-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7b9de-165">Next steps</span></span>
* [<span data-ttu-id="7b9de-166">Backup di Azure - Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="7b9de-166">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
