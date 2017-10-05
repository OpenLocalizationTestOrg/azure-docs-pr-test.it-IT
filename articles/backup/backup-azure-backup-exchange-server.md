---
title: Eseguire il backup di un server di Exchange in Backup di Azure con System Center 2012 R2 DPM |Documentazione Microsoft
description: Informazioni su come eseguire il backup di un server di Exchange in Backup di Azure con System Center 2012 R2 DPM
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
ms.openlocfilehash: 2a0e416440e55cfde70cbd20d40c99fb29b4229c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-an-exchange-server-to-azure-backup-with-system-center-2012-r2-dpm"></a><span data-ttu-id="391d8-103">Eseguire il backup di un server di Exchange in Backup di Azure con System Center 2012 R2 DPM</span><span class="sxs-lookup"><span data-stu-id="391d8-103">Back up an Exchange server to Azure Backup with System Center 2012 R2 DPM</span></span>
<span data-ttu-id="391d8-104">Questo articolo descrive come configurare un server di System Center 2012 R2 Data Protection Manager (DPM) per eseguire il backup di un server di Microsoft Exchange per Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="391d8-104">This article describes how to configure a System Center 2012 R2 Data Protection Manager (DPM) server to back up a Microsoft Exchange server to  Azure Backup.</span></span>  

## <a name="updates"></a><span data-ttu-id="391d8-105">Aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="391d8-105">Updates</span></span>
<span data-ttu-id="391d8-106">Per registrare correttamente il server DPM con Backup di Azure, è necessario installare l'aggiornamento cumulativo più recente per System Center 2012 R2 DPM e la versione più recente dell'agente di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="391d8-106">To successfully register the DPM server with Azure Backup, you must install the latest update rollup for System Center 2012 R2 DPM and the latest version of the Azure Backup Agent.</span></span> <span data-ttu-id="391d8-107">Ottenere l'aggiornamento cumulativo più recente dal [catalogo Microsoft](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span><span class="sxs-lookup"><span data-stu-id="391d8-107">Get the latest update rollup from the [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span></span>

> [!NOTE]
> <span data-ttu-id="391d8-108">Per gli esempi in questo articolo, è installata la versione 2.0.8719.0 dell'agente di Backup di Azure e l'aggiornamento cumulativo 6 è installato in System Center 2012 R2 DPM.</span><span class="sxs-lookup"><span data-stu-id="391d8-108">For the examples in this article, version 2.0.8719.0 of the Azure Backup Agent is installed, and Update Rollup 6 is installed on System Center 2012 R2 DPM.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="391d8-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="391d8-109">Prerequisites</span></span>
<span data-ttu-id="391d8-110">Prima di continuare, assicurarsi che tutti i [prerequisiti](backup-azure-dpm-introduction.md#prerequisites) per l'uso di Backup di Microsoft Azure per proteggere i carichi di lavoro siano stati soddisfatti.</span><span class="sxs-lookup"><span data-stu-id="391d8-110">Before you continue, make sure that all the [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup to protect workloads have been met.</span></span> <span data-ttu-id="391d8-111">I prerequisiti includono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="391d8-111">These prerequisites include the following:</span></span>

* <span data-ttu-id="391d8-112">È stato creato un insieme di credenziali per il backup nel sito di Azure.</span><span class="sxs-lookup"><span data-stu-id="391d8-112">A backup vault on the Azure site has been created.</span></span>
* <span data-ttu-id="391d8-113">Le credenziali dell'agente e dell'insieme di credenziali sono state scaricate nel server DPM.</span><span class="sxs-lookup"><span data-stu-id="391d8-113">Agent and vault credentials have been downloaded to the DPM server.</span></span>
* <span data-ttu-id="391d8-114">L'agente è installato nel server DPM.</span><span class="sxs-lookup"><span data-stu-id="391d8-114">The agent is installed on the DPM server.</span></span>
* <span data-ttu-id="391d8-115">Le credenziali dell'insieme di credenziali sono state usate per registrare il server DPM.</span><span class="sxs-lookup"><span data-stu-id="391d8-115">The vault credentials were used to register the DPM server.</span></span>
* <span data-ttu-id="391d8-116">Se si sta proteggendo Exchange 2016, eseguire l'aggiornamento a DPM 2012 R2 UR9 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="391d8-116">If you are protecting Exchange 2016, please upgrade to DPM 2012 R2 UR9 or later</span></span>

## <a name="dpm-protection-agent"></a><span data-ttu-id="391d8-117">Agente protezione DPM</span><span class="sxs-lookup"><span data-stu-id="391d8-117">DPM protection agent</span></span>
<span data-ttu-id="391d8-118">Per installare l'agente protezione DPM nel server di Exchange, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="391d8-118">To install the DPM protection agent on the Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="391d8-119">Assicurarsi che i firewall siano configurati correttamente.</span><span class="sxs-lookup"><span data-stu-id="391d8-119">Make sure that the firewalls are correctly configured.</span></span> <span data-ttu-id="391d8-120">Vedere [Configurare le eccezioni del firewall per l'agente](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="391d8-120">See [Configure firewall exceptions for the agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="391d8-121">Per installare l'agente nel server di Exchange, fare clic su **Gestione > Agenti > Installa** nella Console amministrazione DPM.</span><span class="sxs-lookup"><span data-stu-id="391d8-121">Install the agent on the Exchange server by clicking **Management > Agents > Install** in DPM Administrator Console.</span></span> <span data-ttu-id="391d8-122">Per la procedura dettagliata, vedere [Installare l'agente protezione DPM](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) .</span><span class="sxs-lookup"><span data-stu-id="391d8-122">See [Install the DPM protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-the-exchange-server"></a><span data-ttu-id="391d8-123">Creare un gruppo di protezione per il server di Exchange</span><span class="sxs-lookup"><span data-stu-id="391d8-123">Create a protection group for the Exchange server</span></span>
1. <span data-ttu-id="391d8-124">Nella Console amministrazione DPM fare clic su **Protezione** e quindi fare clic su **Nuovo** nella barra multifunzione per aprire la procedura guidata **Crea nuovo gruppo protezione dati**.</span><span class="sxs-lookup"><span data-stu-id="391d8-124">In the DPM Administrator Console, click **Protection**, and then click **New** on the tool ribbon to open the **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="391d8-125">Nella schermata **iniziale** della procedura guidata fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="391d8-125">On the **Welcome** screen of the wizard click **Next**.</span></span>
3. <span data-ttu-id="391d8-126">Nella schermata **Selezione tipo di gruppo protezione dati** selezionare **Server** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="391d8-126">On the **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="391d8-127">Selezionare il database di Exchange Server che si vuole proteggere e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="391d8-127">Select the Exchange server database that you want to protect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="391d8-128">Se si vuole proteggere Exchange 2013, controllare i [Prerequisiti di Exchange 2013](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="391d8-128">If you are protecting Exchange 2013, check the [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="391d8-129">Nell'esempio seguente è selezionato il database di Exchange 2010.</span><span class="sxs-lookup"><span data-stu-id="391d8-129">In the following example, the Exchange 2010 database is selected.</span></span>

    ![Seleziona membri del gruppo](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="391d8-131">Selezionare il metodo di protezione dati.</span><span class="sxs-lookup"><span data-stu-id="391d8-131">Select the data protection method.</span></span>

    <span data-ttu-id="391d8-132">Assegnare un nome al gruppo protezione dati e quindi selezionare entrambe le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="391d8-132">Name the protection group, and then select both of the following options:</span></span>

   * <span data-ttu-id="391d8-133">Protezione dati breve termine tramite: Disco.</span><span class="sxs-lookup"><span data-stu-id="391d8-133">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="391d8-134">Protezione dati online.</span><span class="sxs-lookup"><span data-stu-id="391d8-134">I want online protection.</span></span>
6. <span data-ttu-id="391d8-135">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="391d8-135">Click **Next**.</span></span>
7. <span data-ttu-id="391d8-136">Selezionare l'opzione **Esegui Eseutil per controllare l'integrità dei dati** se si vuole controllare l'integrità dei database di Exchange Server.</span><span class="sxs-lookup"><span data-stu-id="391d8-136">Select the **Run Eseutil to check data integrity** option if you want to check the integrity of the Exchange Server databases.</span></span>

    <span data-ttu-id="391d8-137">Dopo aver selezionato questa opzione, la verifica coerenza del backup verrà eseguito nel server DPM per evitare il traffico di I/O che viene generato eseguendo il comando **eseutil** sul server di Exchange.</span><span class="sxs-lookup"><span data-stu-id="391d8-137">After you select this option, backup consistency checking will be run on the DPM server to avoid the I/O traffic that’s generated by running the **eseutil** command on the Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="391d8-138">Per usare questa opzione, è necessario copiare i file Ese.dll and Eseutil.exe nella directory C:\Programmi\Microsoft System Center 2012 R2\DPM\DPM\bin nel server DPM.</span><span class="sxs-lookup"><span data-stu-id="391d8-138">To use this option, you must copy the Ese.dll and Eseutil.exe files to the C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin directory on the DPM server.</span></span> <span data-ttu-id="391d8-139">In caso contrario, viene generato l'errore seguente: </span><span class="sxs-lookup"><span data-stu-id="391d8-139">Otherwise, the following error is triggered:</span></span>  
   > <span data-ttu-id="391d8-140">![Errore di Eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="391d8-140">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="391d8-141">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="391d8-141">Click **Next**.</span></span>
9. <span data-ttu-id="391d8-142">Selezionare il database per **Backup di copia**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="391d8-142">Select the database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="391d8-143">Se non si seleziona "Backup completo" per almeno una copia del gruppo di disponibilità dei database di un database, i registri non verranno troncati.</span><span class="sxs-lookup"><span data-stu-id="391d8-143">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="391d8-144">Configurare gli obiettivi per **Backup a breve termine**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="391d8-144">Configure the goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="391d8-145">Controllare lo spazio disponibile su disco e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="391d8-145">Review the available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="391d8-146">Selezionare l'ora in cui il server DPM dovrà creare la replica iniziale e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="391d8-146">Select the time at which the DPM server will create the initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="391d8-147">Selezionare le opzioni di verifica coerenza e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="391d8-147">Select the consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="391d8-148">Scegliere il database di cui si vuole eseguire il backup in Azure e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="391d8-148">Choose the database that you want to back up to Azure, and then click **Next**.</span></span> <span data-ttu-id="391d8-149">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="391d8-149">For example:</span></span>

    ![Specifica i dati da proteggere online](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="391d8-151">Definire la pianificazione per **Backup di Azure**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="391d8-151">Define the schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="391d8-152">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="391d8-152">For example:</span></span>

    ![Specificare la pianificazione dei backup online](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="391d8-154">Tenere presente che i punti di ripristino online sono basati sui punti di ripristino di backup completo rapido.</span><span class="sxs-lookup"><span data-stu-id="391d8-154">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="391d8-155">È quindi necessario pianificare il punto di ripristino in linea dopo il tempo specificato per il punto di ripristino di backup completo rapido.</span><span class="sxs-lookup"><span data-stu-id="391d8-155">Therefore, you must schedule the online recovery point after the time that’s specified for the express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="391d8-156">Configurare i criteri di conservazione per **Backup di Azure**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="391d8-156">Configure the retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="391d8-157">Scegliere un'opzione di replica online e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="391d8-157">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="391d8-158">Un database di grandi dimensioni potrebbe richiedere molto tempo per creare il backup iniziale in rete.</span><span class="sxs-lookup"><span data-stu-id="391d8-158">If you have a large database, it could take a long time for the initial backup to be created over the network.</span></span> <span data-ttu-id="391d8-159">Per evitare questo problema, è possibile creare un backup offline.</span><span class="sxs-lookup"><span data-stu-id="391d8-159">To avoid this issue, you can create an offline backup.</span></span>  

    ![Specificare i criteri di mantenimento online](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="391d8-161">Verificare le impostazioni e quindi fare clic su **Crea gruppo**.</span><span class="sxs-lookup"><span data-stu-id="391d8-161">Confirm the settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="391d8-162">Fare clic su **Close**.</span><span class="sxs-lookup"><span data-stu-id="391d8-162">Click **Close**.</span></span>

## <a name="recover-the-exchange-database"></a><span data-ttu-id="391d8-163">Ripristinare il database di Exchange</span><span class="sxs-lookup"><span data-stu-id="391d8-163">Recover the Exchange database</span></span>
1. <span data-ttu-id="391d8-164">Per ripristinare un database di Exchange, fare clic su **Ripristino** nella Console amministrazione DPM.</span><span class="sxs-lookup"><span data-stu-id="391d8-164">To recover an Exchange database, click **Recovery** in the DPM Administrator Console.</span></span>
2. <span data-ttu-id="391d8-165">Individuare il database di Exchange che si vuole ripristinare.</span><span class="sxs-lookup"><span data-stu-id="391d8-165">Locate the Exchange database that you want to recover.</span></span>
3. <span data-ttu-id="391d8-166">Selezionare un punto di ripristino online dall'elenco a discesa *Ora ripristino* .</span><span class="sxs-lookup"><span data-stu-id="391d8-166">Select an online recovery point from the *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="391d8-167">Fare clic su **Ripristina** per avviare il **Ripristino guidato**.</span><span class="sxs-lookup"><span data-stu-id="391d8-167">Click **Recover** to start the **Recovery Wizard**.</span></span>

<span data-ttu-id="391d8-168">Per i punti di ripristino online sono disponibili cinque tipi:</span><span class="sxs-lookup"><span data-stu-id="391d8-168">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="391d8-169">**Ripristina nel percorso originale di Exchange Server:** i dati verranno ripristinati nel server di Exchange originale.</span><span class="sxs-lookup"><span data-stu-id="391d8-169">**Recover to original Exchange Server location:** The data will be recovered to the original Exchange server.</span></span>
* <span data-ttu-id="391d8-170">**Ripristina in un altro database in un Server di Exchange:** i dati verranno ripristinati in un altro database in un altro server di Exchange.</span><span class="sxs-lookup"><span data-stu-id="391d8-170">**Recover to another database on an Exchange Server:** The data will be recovered to another database on another Exchange server.</span></span>
* <span data-ttu-id="391d8-171">**Ripristina in un database di ripristino:** i dati verranno ripristinati in un database di ripristino di Exchange (RDB).</span><span class="sxs-lookup"><span data-stu-id="391d8-171">**Recover to a Recovery Database:** The data will be recovered to an Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="391d8-172">**Copia in una cartella di rete:** i dati verranno ripristinati in una cartella di rete.</span><span class="sxs-lookup"><span data-stu-id="391d8-172">**Copy to a network folder:** The data will be recovered to a network folder.</span></span>
* <span data-ttu-id="391d8-173">**Copia su nastro:** se si ha una libreria di nastri o un'unità nastro autonoma collegata e configurata nel server DPM, il punto di ripristino verrà copiato su un nastro disponibile.</span><span class="sxs-lookup"><span data-stu-id="391d8-173">**Copy to tape:** If you have a tape library or a stand-alone tape drive attached and configured on the DPM server, the recovery point will be copied to a free tape.</span></span>

    ![Scegliere la replica online](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="391d8-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="391d8-175">Next steps</span></span>
* [<span data-ttu-id="391d8-176">Backup di Azure - Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="391d8-176">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
