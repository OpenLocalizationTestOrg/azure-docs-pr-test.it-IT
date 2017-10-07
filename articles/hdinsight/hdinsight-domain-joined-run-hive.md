---
title: criteri di aaaConfigure Hive in HDInsight dominio - Azure | Documenti Microsoft
description: Informazioni su...
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3fade1e5-c2e1-4ad5-b371-f95caea23f6d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 56f2bf9d872abc5f772b886fcf91c2e2422092f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a><span data-ttu-id="2f307-103">Configurare criteri Hive in HDInsight aggiunto al dominio (anteprima)</span><span class="sxs-lookup"><span data-stu-id="2f307-103">Configure Hive policies in Domain-joined HDInsight (Preview)</span></span>
<span data-ttu-id="2f307-104">Informazioni su come criteri cane Apache tooconfigure per l'Hive.</span><span class="sxs-lookup"><span data-stu-id="2f307-104">Learn how tooconfigure Apache Ranger policies for Hive.</span></span> <span data-ttu-id="2f307-105">In questo articolo, creare due cane criteri toorestrict accesso toohello hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="2f307-105">In this article, you create two Ranger policies toorestrict access toohello hivesampletable.</span></span> <span data-ttu-id="2f307-106">Hello hivesampletable viene fornito con i cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2f307-106">hello hivesampletable comes with HDInsight clusters.</span></span> <span data-ttu-id="2f307-107">Dopo aver configurato i criteri di hello, utilizzare Excel e ODBC driver tooconnect tooHive le tabelle in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2f307-107">After you have configured hello policies, you use Excel and ODBC driver tooconnect tooHive tables in HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f307-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2f307-108">Prerequisites</span></span>
* <span data-ttu-id="2f307-109">Un cluster HDInsight aggiunto al dominio.</span><span class="sxs-lookup"><span data-stu-id="2f307-109">A Domain-joined HDInsight cluster.</span></span> <span data-ttu-id="2f307-110">Vedere [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configurare i cluster HDInsight aggiunti al dominio).</span><span class="sxs-lookup"><span data-stu-id="2f307-110">See [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="2f307-111">Una workstation con Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone oppure Office 2010 Professional Plus.</span><span class="sxs-lookup"><span data-stu-id="2f307-111">A workstation with Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="connect-tooapache-ranger-admin-ui"></a><span data-ttu-id="2f307-112">Connettersi tooApache cane interfaccia utente di amministrazione</span><span class="sxs-lookup"><span data-stu-id="2f307-112">Connect tooApache Ranger Admin UI</span></span>
<span data-ttu-id="2f307-113">**tooconnect tooRanger Admin UI**</span><span class="sxs-lookup"><span data-stu-id="2f307-113">**tooconnect tooRanger Admin UI**</span></span>

1. <span data-ttu-id="2f307-114">Da un browser, connettersi tooRanger Admin UI.</span><span class="sxs-lookup"><span data-stu-id="2f307-114">From a browser, connect tooRanger Admin UI.</span></span> <span data-ttu-id="2f307-115">Hello URL è https://&lt;ClusterName >.azurehdinsight.net/Ranger/.</span><span class="sxs-lookup"><span data-stu-id="2f307-115">hello URL is https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2f307-116">Ranger usa credenziali diverse da quelle del cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2f307-116">Ranger uses different credentials than Hadoop cluster.</span></span> <span data-ttu-id="2f307-117">tooprevent browser utilizzando credenziali memorizzate nella cache di Hadoop, utilizzare toohello tooconnect finestra del browser inprivate nuova interfaccia utente di amministrazione cane.</span><span class="sxs-lookup"><span data-stu-id="2f307-117">tooprevent browsers using cached Hadoop credentials, use new inprivate browser window tooconnect toohello Ranger Admin UI.</span></span>
   >
   >
2. <span data-ttu-id="2f307-118">Accedere con la password e nome utente di dominio amministratore cluster hello:</span><span class="sxs-lookup"><span data-stu-id="2f307-118">Log in using hello cluster administrator domain user name and password:</span></span>

    ![Home page di Ranger con dominio aggiunto a HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    <span data-ttu-id="2f307-120">Attualmente, Ranger è compatibile solo con Yarn e Hive.</span><span class="sxs-lookup"><span data-stu-id="2f307-120">Currently, Ranger only works with Yarn and Hive.</span></span>

## <a name="create-domain-users"></a><span data-ttu-id="2f307-121">Creazione di utenti del dominio</span><span class="sxs-lookup"><span data-stu-id="2f307-121">Create Domain users</span></span>
<span data-ttu-id="2f307-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Configurare i cluster HDInsight aggiunti al dominio) sono stati creati hiveruser1 e hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="2f307-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), you have created hiveruser1 and hiveuser2.</span></span> <span data-ttu-id="2f307-123">Si utilizzerà l'account utente due hello in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2f307-123">You will use hello two user account in this tutorial.</span></span>

## <a name="create-ranger-policies"></a><span data-ttu-id="2f307-124">Creazione dei criteri di Ranger</span><span class="sxs-lookup"><span data-stu-id="2f307-124">Create Ranger policies</span></span>
<span data-ttu-id="2f307-125">In questa sezione verranno creati due criteri di Ranger per accedere a hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="2f307-125">In this section, you will create two Ranger policies for accessing hivesampletable.</span></span> <span data-ttu-id="2f307-126">Vengono concesse autorizzazioni di selezione su diversi set di colonne.</span><span class="sxs-lookup"><span data-stu-id="2f307-126">You give select permission on different set of columns.</span></span> <span data-ttu-id="2f307-127">Entrambi gli utenti sono stati creati nella procedura [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Configurare i cluster HDInsight aggiunti al dominio).</span><span class="sxs-lookup"><span data-stu-id="2f307-127">Both users were created in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span></span>  <span data-ttu-id="2f307-128">Nella sezione successiva hello, verranno testati due criteri di hello in Excel.</span><span class="sxs-lookup"><span data-stu-id="2f307-128">In hello next section, you will test hello two policies in Excel.</span></span>

<span data-ttu-id="2f307-129">**criteri cane toocreate**</span><span class="sxs-lookup"><span data-stu-id="2f307-129">**toocreate Ranger policies**</span></span>

1. <span data-ttu-id="2f307-130">Aprire l'interfaccia utente di amministrazione di Ranger.</span><span class="sxs-lookup"><span data-stu-id="2f307-130">Open Ranger Admin UI.</span></span> <span data-ttu-id="2f307-131">Vedere [connettersi tooApache dell'interfaccia utente amministrazione cane](#connect-to-apache-ranager-admin-ui).</span><span class="sxs-lookup"><span data-stu-id="2f307-131">See [Connect tooApache Ranger Admin UI](#connect-to-apache-ranager-admin-ui).</span></span>
2. <span data-ttu-id="2f307-132">Fare clic su **&lt;ClusterName>_hive** in **Hive**.</span><span class="sxs-lookup"><span data-stu-id="2f307-132">Click **&lt;ClusterName>_hive**, under **Hive**.</span></span> <span data-ttu-id="2f307-133">Verranno visualizzati due criteri preconfigurati.</span><span class="sxs-lookup"><span data-stu-id="2f307-133">You shall see two pre-configure policies.</span></span>
3. <span data-ttu-id="2f307-134">Fare clic su **Aggiungi nuovo criterio**, quindi immettere hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="2f307-134">Click **Add New Policy**, and then enter hello following values:</span></span>

   * <span data-ttu-id="2f307-135">Nome criterio: read-hivesampletable-all</span><span class="sxs-lookup"><span data-stu-id="2f307-135">Policy name: read-hivesampletable-all</span></span>
   * <span data-ttu-id="2f307-136">Database Hive: predefinito</span><span class="sxs-lookup"><span data-stu-id="2f307-136">Hive Database: default</span></span>
   * <span data-ttu-id="2f307-137">Tabella: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="2f307-137">table: hivesampletable</span></span>
   * <span data-ttu-id="2f307-138">Colonna Hive: *</span><span class="sxs-lookup"><span data-stu-id="2f307-138">Hive column: *</span></span>
   * <span data-ttu-id="2f307-139">Seleziona utente: hiveuser1</span><span class="sxs-lookup"><span data-stu-id="2f307-139">Select User: hiveuser1</span></span>
   * <span data-ttu-id="2f307-140">Autorizzazioni: selezionare</span><span class="sxs-lookup"><span data-stu-id="2f307-140">Permissions: select</span></span>

     ![Configurazione dei criteri di Hive Ranger con dominio aggiunto a HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png)<span data-ttu-id="2f307-142">.</span><span class="sxs-lookup"><span data-stu-id="2f307-142">.</span></span>

     > [!NOTE]
     > <span data-ttu-id="2f307-143">Se un utente di dominio non viene popolato in Seleziona utente, attendere alcuni istanti per cane toosync con AAD.</span><span class="sxs-lookup"><span data-stu-id="2f307-143">If a domain user is not populated in Select User, wait a few moments for Ranger toosync with AAD.</span></span>
     >
     >
4. <span data-ttu-id="2f307-144">Fare clic su **Aggiungi** criteri hello toosave.</span><span class="sxs-lookup"><span data-stu-id="2f307-144">Click **Add** toosave hello policy.</span></span>
5. <span data-ttu-id="2f307-145">Ripetere l'operazione hello ultimi due passaggi toocreate un altro criterio con hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="2f307-145">Repeat hello last two steps toocreate another policy with hello following properties:</span></span>

   * <span data-ttu-id="2f307-146">Nome criterio: read-hivesampletable-devicemake</span><span class="sxs-lookup"><span data-stu-id="2f307-146">Policy name: read-hivesampletable-devicemake</span></span>
   * <span data-ttu-id="2f307-147">Database Hive: predefinito</span><span class="sxs-lookup"><span data-stu-id="2f307-147">Hive Database: default</span></span>
   * <span data-ttu-id="2f307-148">Tabella: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="2f307-148">table: hivesampletable</span></span>
   * <span data-ttu-id="2f307-149">Colonna Hive: clientid, devicemake</span><span class="sxs-lookup"><span data-stu-id="2f307-149">Hive column: clientid, devicemake</span></span>
   * <span data-ttu-id="2f307-150">Seleziona utente: hiveuser2</span><span class="sxs-lookup"><span data-stu-id="2f307-150">Select User: hiveuser2</span></span>
   * <span data-ttu-id="2f307-151">Autorizzazioni: selezionare</span><span class="sxs-lookup"><span data-stu-id="2f307-151">Permissions: select</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="2f307-152">Creare un'origine dati Hive ODBC</span><span class="sxs-lookup"><span data-stu-id="2f307-152">Create Hive ODBC data source</span></span>
<span data-ttu-id="2f307-153">istruzioni di Hello sono reperibile [origine dati ODBC di Hive creare](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="2f307-153">hello instructions can be found in [Create Hive ODBC data source](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>  

    <span data-ttu-id="2f307-154">Proprietà</span><span class="sxs-lookup"><span data-stu-id="2f307-154">Property</span></span>|<span data-ttu-id="2f307-155">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f307-155">Description</span></span>
    ---|---
    <span data-ttu-id="2f307-156">Data Source Name</span><span class="sxs-lookup"><span data-stu-id="2f307-156">Data Source Name</span></span>|<span data-ttu-id="2f307-157">Fornire un'origine dati di nome tooyour</span><span class="sxs-lookup"><span data-stu-id="2f307-157">Give a name tooyour data source</span></span>
    <span data-ttu-id="2f307-158">Host</span><span class="sxs-lookup"><span data-stu-id="2f307-158">Host</span></span>|<span data-ttu-id="2f307-159">Immettere &lt;HDInsightClusterName>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="2f307-159">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="2f307-160">Ad esempio, myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="2f307-160">For example, myHDICluster.azurehdinsight.net</span></span>
    <span data-ttu-id="2f307-161">Porta</span><span class="sxs-lookup"><span data-stu-id="2f307-161">Port</span></span>|<span data-ttu-id="2f307-162">Utilizzare <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="2f307-162">Use <strong>443</strong>.</span></span> <span data-ttu-id="2f307-163">(Questa porta è stata modificata da too443 563).</span><span class="sxs-lookup"><span data-stu-id="2f307-163">(This port has been changed from 563 too443.)</span></span>
    <span data-ttu-id="2f307-164">Database</span><span class="sxs-lookup"><span data-stu-id="2f307-164">Database</span></span>|<span data-ttu-id="2f307-165">Usare l'<strong>impostazione predefinita</strong>.</span><span class="sxs-lookup"><span data-stu-id="2f307-165">Use <strong>Default</strong>.</span></span>
    <span data-ttu-id="2f307-166">Hive Server Type</span><span class="sxs-lookup"><span data-stu-id="2f307-166">Hive Server Type</span></span>|<span data-ttu-id="2f307-167">Selezionare <strong>Hive Server 2</strong></span><span class="sxs-lookup"><span data-stu-id="2f307-167">Select <strong>Hive Server 2</strong></span></span>
    <span data-ttu-id="2f307-168">Mechanism</span><span class="sxs-lookup"><span data-stu-id="2f307-168">Mechanism</span></span>|<span data-ttu-id="2f307-169">Selezionare <strong>Azure HDInsight Service</strong></span><span class="sxs-lookup"><span data-stu-id="2f307-169">Select <strong>Azure HDInsight Service</strong></span></span>
    <span data-ttu-id="2f307-170">HTTP Path</span><span class="sxs-lookup"><span data-stu-id="2f307-170">HTTP Path</span></span>|<span data-ttu-id="2f307-171">Lasciare vuoto.</span><span class="sxs-lookup"><span data-stu-id="2f307-171">Leave it blank.</span></span>
    <span data-ttu-id="2f307-172">User Name</span><span class="sxs-lookup"><span data-stu-id="2f307-172">User Name</span></span>|<span data-ttu-id="2f307-173">Immettere hiveuser1@contoso158.onmicrosoft.com. Aggiornare il nome di dominio hello se è diverso.</span><span class="sxs-lookup"><span data-stu-id="2f307-173">Enter hiveuser1@contoso158.onmicrosoft.com. Update hello domain name if it is different.</span></span>
    <span data-ttu-id="2f307-174">Password</span><span class="sxs-lookup"><span data-stu-id="2f307-174">Password</span></span>|<span data-ttu-id="2f307-175">Immettere la password di hello per hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="2f307-175">Enter hello password for hiveuser1.</span></span>
    </table>

<span data-ttu-id="2f307-176">Verificare che tooclick **Test** prima di salvare l'origine dati hello.</span><span class="sxs-lookup"><span data-stu-id="2f307-176">Make sure tooclick **Test** before saving hello data source.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="2f307-177">Importazione di dati in Excel da HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f307-177">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="2f307-178">Nell'ultima sezione hello, è stato configurato due criteri.</span><span class="sxs-lookup"><span data-stu-id="2f307-178">In hello last section, you have configured two policies.</span></span>  <span data-ttu-id="2f307-179">hiveuser1 hello selezionare autorizzazione su tutte le colonne di hello, che hiveuser2 ha hello selezionare l'autorizzazione per due colonne.</span><span class="sxs-lookup"><span data-stu-id="2f307-179">hiveuser1 has hello select permission on all hello columns, and hiveuser2 has hello select permission on two columns.</span></span> <span data-ttu-id="2f307-180">In questa sezione è rappresentare hello due utenti tooimport dati in Excel.</span><span class="sxs-lookup"><span data-stu-id="2f307-180">In this section, you impersonate hello two users tooimport data into Excel.</span></span>

1. <span data-ttu-id="2f307-181">Aprire una cartella di lavoro nuova o esistente in Excel.</span><span class="sxs-lookup"><span data-stu-id="2f307-181">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="2f307-182">Da hello **dati** scheda, fare clic su **da altre origini dati**, quindi fare clic su **da connessione guidata dati** toolaunch hello **connessione guidata dati**.</span><span class="sxs-lookup"><span data-stu-id="2f307-182">From hello **Data** tab, click **From Other Data Sources**, and then click **From Data Connection Wizard** toolaunch hello **Data Connection Wizard**.</span></span>

    <span data-ttu-id="2f307-183">![Aprire Connessione guidata dati][img-hdi-simbahiveodbc.excel.dataconnection]</span><span class="sxs-lookup"><span data-stu-id="2f307-183">![Open data connection wizard][img-hdi-simbahiveodbc.excel.dataconnection]</span></span>
3. <span data-ttu-id="2f307-184">Selezionare **DSN ODBC** come origine dati hello e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2f307-184">Select **ODBC DSN** as hello data source, and then click **Next**.</span></span>
4. <span data-ttu-id="2f307-185">Origini dati ODBC, creato nel passaggio precedente hello il nome dell'origine dati selezionare hello e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2f307-185">From ODBC data sources, select hello data source name that you created in hello previous step, and then  click **Next**.</span></span>
5. <span data-ttu-id="2f307-186">Immettere nuovamente la password hello per cluster hello nella procedura guidata hello e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f307-186">Re-enter hello password for hello cluster in hello wizard, and then click **OK**.</span></span> <span data-ttu-id="2f307-187">Attendere hello **seleziona Database e tabella** tooopen finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="2f307-187">Wait for hello **Select Database and Table** dialog tooopen.</span></span> <span data-ttu-id="2f307-188">Questa operazione potrebbe richiedere alcuni secondi.</span><span class="sxs-lookup"><span data-stu-id="2f307-188">This can take a few seconds.</span></span>
6. <span data-ttu-id="2f307-189">Selezionare **hivesampletable**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2f307-189">Select **hivesampletable**, and then click **Next**.</span></span>
7. <span data-ttu-id="2f307-190">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="2f307-190">Click **Finish**.</span></span>
8. <span data-ttu-id="2f307-191">In hello **l'importazione dei dati** finestra di dialogo, è possibile modificare o specificare query hello.</span><span class="sxs-lookup"><span data-stu-id="2f307-191">In hello **Import Data** dialog, you can change or specify hello query.</span></span> <span data-ttu-id="2f307-192">Questa operazione, scegliere toodo **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="2f307-192">toodo so, click **Properties**.</span></span> <span data-ttu-id="2f307-193">Questa operazione potrebbe richiedere alcuni secondi.</span><span class="sxs-lookup"><span data-stu-id="2f307-193">This can take a few seconds.</span></span>
9. <span data-ttu-id="2f307-194">Fare clic su hello **definizione** scheda hello testo del comando è:</span><span class="sxs-lookup"><span data-stu-id="2f307-194">Click hello **Definition** tab. hello command text is:</span></span>

       SELECT * FROM "HIVE"."default"."hivesampletable"

   <span data-ttu-id="2f307-195">Criteri di cane hello che è definito, hiveuser1 dispone dell'autorizzazione select per tutte le colonne di hello.</span><span class="sxs-lookup"><span data-stu-id="2f307-195">By hello Ranger policies you defined,  hiveuser1 has select permission on all hello columns.</span></span>  <span data-ttu-id="2f307-196">Pertanto, questa query funziona con le credenziali di hiveuser1, ma non con quelle di hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="2f307-196">So this query works with hiveuser1's credentials, but this query does not not work with hiveuser2's credentials.</span></span>

   <span data-ttu-id="2f307-197">![Proprietà di connessione][img-hdi-simbahiveodbc-excel-connectionproperties]</span><span class="sxs-lookup"><span data-stu-id="2f307-197">![Connection Properties][img-hdi-simbahiveodbc-excel-connectionproperties]</span></span>
10. <span data-ttu-id="2f307-198">Fare clic su **OK** tooclose finestra di dialogo Proprietà connessione hello.</span><span class="sxs-lookup"><span data-stu-id="2f307-198">Click **OK** tooclose hello Connection Properties dialog.</span></span>
11. <span data-ttu-id="2f307-199">Fare clic su **OK** tooclose hello **l'importazione dei dati** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="2f307-199">Click **OK** tooclose hello **Import Data** dialog.</span></span>  
12. <span data-ttu-id="2f307-200">Digitare nuovamente la password di hello per hiveuser1 e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f307-200">Reenter hello password for hiveuser1, and then click **OK**.</span></span> <span data-ttu-id="2f307-201">Alcuni secondi prima del recupero dei dati importati tooExcel necessario.</span><span class="sxs-lookup"><span data-stu-id="2f307-201">It takes a few seconds before data gets imported tooExcel.</span></span> <span data-ttu-id="2f307-202">Al termine, verranno visualizzate 11 colonne di dati.</span><span class="sxs-lookup"><span data-stu-id="2f307-202">When it is done, you shall see 11 columns of data.</span></span>

<span data-ttu-id="2f307-203">tootest hello secondo criteri (read-hivesampletable-devicemake) creati nell'ultima sezione hello</span><span class="sxs-lookup"><span data-stu-id="2f307-203">tootest hello second policy (read-hivesampletable-devicemake) you created in hello last section</span></span>

1. <span data-ttu-id="2f307-204">Aggiungere un nuovo foglio in Excel.</span><span class="sxs-lookup"><span data-stu-id="2f307-204">Add a new sheet in Excel.</span></span>
2. <span data-ttu-id="2f307-205">Seguire i dati hello tooimport hello ultima procedura.</span><span class="sxs-lookup"><span data-stu-id="2f307-205">Follow hello last procedure tooimport hello data.</span></span>  <span data-ttu-id="2f307-206">modifica solo del Hello che si apporterà è credenziali del hiveuser2 toouse invece del hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="2f307-206">hello only change you will make is toouse hiveuser2's credentials instead of hiveuser1's.</span></span> <span data-ttu-id="2f307-207">L'operazione non riuscirà perché hiveuser2 ha solo due colonne di autorizzazione toosee.</span><span class="sxs-lookup"><span data-stu-id="2f307-207">This will fail because hiveuser2 only has permission toosee two columns.</span></span> <span data-ttu-id="2f307-208">Si deve ottenere hello errore seguente:</span><span class="sxs-lookup"><span data-stu-id="2f307-208">You shall get hello following error:</span></span>

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. <span data-ttu-id="2f307-209">Seguire hello stesso dati tooimport stored procedure.</span><span class="sxs-lookup"><span data-stu-id="2f307-209">Follow hello same procedure tooimport data.</span></span> <span data-ttu-id="2f307-210">Questa volta, utilizzare le credenziali del hiveuser2 e inoltre modificare hello from dell'istruzione select:</span><span class="sxs-lookup"><span data-stu-id="2f307-210">This time, use hiveuser2's credentials, and also modify hello select statement from:</span></span>

        SELECT * FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="2f307-211">in:</span><span class="sxs-lookup"><span data-stu-id="2f307-211">to:</span></span>

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="2f307-212">Al termine, verranno visualizzate due colonne di dati importati.</span><span class="sxs-lookup"><span data-stu-id="2f307-212">When it is done, you shall see two columns of data imported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f307-213">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2f307-213">Next steps</span></span>
* <span data-ttu-id="2f307-214">Per configurare un cluster HDInsight aggiunto al dominio, vedere [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configurare i cluster HDInsight aggiunti al dominio).</span><span class="sxs-lookup"><span data-stu-id="2f307-214">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="2f307-215">Per gestire cluster HDInsight aggiunti al dominio, vedere [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Gestire i cluster HDInsight aggiunti al dominio).</span><span class="sxs-lookup"><span data-stu-id="2f307-215">For managing a Domain-joined HDInsight clusters, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>
* <span data-ttu-id="2f307-216">Per eseguire query Hive usando SSH nei cluster HDInsight aggiunti al dominio, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="2f307-216">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
* <span data-ttu-id="2f307-217">Per la connessione Hive tramite Hive JDBC, vedere [connettersi tooHive in Azure HDInsight utilizza hello Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="2f307-217">For Connecting Hive using Hive JDBC, see [Connect tooHive on Azure HDInsight using hello Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)</span></span>
* <span data-ttu-id="2f307-218">Per l'utilizzo di ODBC Hive connessione tooHadoop di Excel, vedere [tooHadoop Excel connettersi con unità di Microsoft ODBC Hive hello](hdinsight-connect-excel-hive-odbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="2f307-218">For connecting Excel tooHadoop using Hive ODBC, see [Connect Excel tooHadoop with hello Microsoft Hive ODBC drive](hdinsight-connect-excel-hive-odbc-driver.md)</span></span>
* <span data-ttu-id="2f307-219">Per la connessione tooHadoop di Excel tramite Power Query, vedere [tooHadoop Excel connettersi tramite Power Query](hdinsight-connect-excel-power-query.md)</span><span class="sxs-lookup"><span data-stu-id="2f307-219">For connecting Excel tooHadoop using Power Query, see [Connect Excel tooHadoop by using Power Query](hdinsight-connect-excel-power-query.md)</span></span>
