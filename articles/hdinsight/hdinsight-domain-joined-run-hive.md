---
title: Configurare criteri Hive in HDInsight aggiunto al dominio - Azure | Microsoft Docs
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
ms.openlocfilehash: de537d5e39dd0d3f75ff802948c7372e4d65d127
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a><span data-ttu-id="daa7b-103">Configurare criteri Hive in HDInsight aggiunto al dominio (anteprima)</span><span class="sxs-lookup"><span data-stu-id="daa7b-103">Configure Hive policies in Domain-joined HDInsight (Preview)</span></span>
<span data-ttu-id="daa7b-104">Informazioni su come configurare i criteri di Apache Ranger per Hive.</span><span class="sxs-lookup"><span data-stu-id="daa7b-104">Learn how to configure Apache Ranger policies for Hive.</span></span> <span data-ttu-id="daa7b-105">In questo articolo vengono creati due criteri di Ranger per limitare l'accesso a hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="daa7b-105">In this article, you create two Ranger policies to restrict access to the hivesampletable.</span></span> <span data-ttu-id="daa7b-106">La tabella hivesampletable è disponibile con i cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="daa7b-106">The hivesampletable comes with HDInsight clusters.</span></span> <span data-ttu-id="daa7b-107">Dopo aver configurato i criteri, usare Excel e il driver ODBC per connettersi alle tabelle Hive in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="daa7b-107">After you have configured the policies, you use Excel and ODBC driver to connect to Hive tables in HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="daa7b-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="daa7b-108">Prerequisites</span></span>
* <span data-ttu-id="daa7b-109">Un cluster HDInsight aggiunto al dominio.</span><span class="sxs-lookup"><span data-stu-id="daa7b-109">A Domain-joined HDInsight cluster.</span></span> <span data-ttu-id="daa7b-110">Vedere [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configurare i cluster HDInsight aggiunti al dominio).</span><span class="sxs-lookup"><span data-stu-id="daa7b-110">See [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="daa7b-111">Una workstation con Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone oppure Office 2010 Professional Plus.</span><span class="sxs-lookup"><span data-stu-id="daa7b-111">A workstation with Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="connect-to-apache-ranger-admin-ui"></a><span data-ttu-id="daa7b-112">Connettersi all'interfaccia utente di amministrazione di Apache Ranger</span><span class="sxs-lookup"><span data-stu-id="daa7b-112">Connect to Apache Ranger Admin UI</span></span>
<span data-ttu-id="daa7b-113">**Per connettersi all'interfaccia utente di amministrazione di Ranger**</span><span class="sxs-lookup"><span data-stu-id="daa7b-113">**To connect to Ranger Admin UI**</span></span>

1. <span data-ttu-id="daa7b-114">Da un browser, connettersi all'interfaccia utente di amministrazione di Ranger.</span><span class="sxs-lookup"><span data-stu-id="daa7b-114">From a browser, connect to Ranger Admin UI.</span></span> <span data-ttu-id="daa7b-115">L'URL è https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span><span class="sxs-lookup"><span data-stu-id="daa7b-115">The URL is https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span></span>

   > [!NOTE]
   > <span data-ttu-id="daa7b-116">Ranger usa credenziali diverse da quelle del cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="daa7b-116">Ranger uses different credentials than Hadoop cluster.</span></span> <span data-ttu-id="daa7b-117">Per evitare che i browser usino credenziali memorizzate nella cache di Hadoop, connettersi all'interfaccia utente di amministrazione di Ranger da una nuova finestra del browser anonima.</span><span class="sxs-lookup"><span data-stu-id="daa7b-117">To prevent browsers using cached Hadoop credentials, use new inprivate browser window to connect to the Ranger Admin UI.</span></span>
   >
   >
2. <span data-ttu-id="daa7b-118">Eseguire l'accesso usando il nome utente e la password di amministratore cluster:</span><span class="sxs-lookup"><span data-stu-id="daa7b-118">Log in using the cluster administrator domain user name and password:</span></span>

    ![Home page di Ranger con dominio aggiunto a HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    <span data-ttu-id="daa7b-120">Attualmente, Ranger è compatibile solo con Yarn e Hive.</span><span class="sxs-lookup"><span data-stu-id="daa7b-120">Currently, Ranger only works with Yarn and Hive.</span></span>

## <a name="create-domain-users"></a><span data-ttu-id="daa7b-121">Creazione di utenti del dominio</span><span class="sxs-lookup"><span data-stu-id="daa7b-121">Create Domain users</span></span>
<span data-ttu-id="daa7b-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Configurare i cluster HDInsight aggiunti al dominio) sono stati creati hiveruser1 e hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="daa7b-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), you have created hiveruser1 and hiveuser2.</span></span> <span data-ttu-id="daa7b-123">In questa esercitazione verranno usati i due account utente.</span><span class="sxs-lookup"><span data-stu-id="daa7b-123">You will use the two user account in this tutorial.</span></span>

## <a name="create-ranger-policies"></a><span data-ttu-id="daa7b-124">Creazione dei criteri di Ranger</span><span class="sxs-lookup"><span data-stu-id="daa7b-124">Create Ranger policies</span></span>
<span data-ttu-id="daa7b-125">In questa sezione verranno creati due criteri di Ranger per accedere a hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="daa7b-125">In this section, you will create two Ranger policies for accessing hivesampletable.</span></span> <span data-ttu-id="daa7b-126">Vengono concesse autorizzazioni di selezione su diversi set di colonne.</span><span class="sxs-lookup"><span data-stu-id="daa7b-126">You give select permission on different set of columns.</span></span> <span data-ttu-id="daa7b-127">Entrambi gli utenti sono stati creati nella procedura [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Configurare i cluster HDInsight aggiunti al dominio).</span><span class="sxs-lookup"><span data-stu-id="daa7b-127">Both users were created in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span></span>  <span data-ttu-id="daa7b-128">Nella sezione successiva verranno verificati i due criteri in Excel.</span><span class="sxs-lookup"><span data-stu-id="daa7b-128">In the next section, you will test the two policies in Excel.</span></span>

<span data-ttu-id="daa7b-129">**Per creare criteri di Ranger**</span><span class="sxs-lookup"><span data-stu-id="daa7b-129">**To create Ranger policies**</span></span>

1. <span data-ttu-id="daa7b-130">Aprire l'interfaccia utente di amministrazione di Ranger.</span><span class="sxs-lookup"><span data-stu-id="daa7b-130">Open Ranger Admin UI.</span></span> <span data-ttu-id="daa7b-131">Vedere [Connettersi all'interfaccia utente di amministrazione di Apache Ranger](#connect-to-apache-ranager-admin-ui).</span><span class="sxs-lookup"><span data-stu-id="daa7b-131">See [Connect to Apache Ranger Admin UI](#connect-to-apache-ranager-admin-ui).</span></span>
2. <span data-ttu-id="daa7b-132">Fare clic su **&lt;ClusterName>_hive** in **Hive**.</span><span class="sxs-lookup"><span data-stu-id="daa7b-132">Click **&lt;ClusterName>_hive**, under **Hive**.</span></span> <span data-ttu-id="daa7b-133">Verranno visualizzati due criteri preconfigurati.</span><span class="sxs-lookup"><span data-stu-id="daa7b-133">You shall see two pre-configure policies.</span></span>
3. <span data-ttu-id="daa7b-134">Fare clic su **Aggiungi nuovo criterio**, quindi immettere i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="daa7b-134">Click **Add New Policy**, and then enter the following values:</span></span>

   * <span data-ttu-id="daa7b-135">Nome criterio: read-hivesampletable-all</span><span class="sxs-lookup"><span data-stu-id="daa7b-135">Policy name: read-hivesampletable-all</span></span>
   * <span data-ttu-id="daa7b-136">Database Hive: predefinito</span><span class="sxs-lookup"><span data-stu-id="daa7b-136">Hive Database: default</span></span>
   * <span data-ttu-id="daa7b-137">Tabella: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="daa7b-137">table: hivesampletable</span></span>
   * <span data-ttu-id="daa7b-138">Colonna Hive: *</span><span class="sxs-lookup"><span data-stu-id="daa7b-138">Hive column: *</span></span>
   * <span data-ttu-id="daa7b-139">Seleziona utente: hiveuser1</span><span class="sxs-lookup"><span data-stu-id="daa7b-139">Select User: hiveuser1</span></span>
   * <span data-ttu-id="daa7b-140">Autorizzazioni: selezionare</span><span class="sxs-lookup"><span data-stu-id="daa7b-140">Permissions: select</span></span>

     ![Configurazione dei criteri di Hive Ranger con dominio aggiunto a HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png)<span data-ttu-id="daa7b-142">.</span><span class="sxs-lookup"><span data-stu-id="daa7b-142">.</span></span>

     > [!NOTE]
     > <span data-ttu-id="daa7b-143">Se l'utente di un dominio non compare in Seleziona utente, attendere alcuni istanti per la sincronizzazione di Ranger con AAD.</span><span class="sxs-lookup"><span data-stu-id="daa7b-143">If a domain user is not populated in Select User, wait a few moments for Ranger to sync with AAD.</span></span>
     >
     >
4. <span data-ttu-id="daa7b-144">Fare clic su **Aggiungi** per salvare il criterio.</span><span class="sxs-lookup"><span data-stu-id="daa7b-144">Click **Add** to save the policy.</span></span>
5. <span data-ttu-id="daa7b-145">Ripetere gli ultimi due passaggi per creare un altro criterio con le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="daa7b-145">Repeat the last two steps to create another policy with the following properties:</span></span>

   * <span data-ttu-id="daa7b-146">Nome criterio: read-hivesampletable-devicemake</span><span class="sxs-lookup"><span data-stu-id="daa7b-146">Policy name: read-hivesampletable-devicemake</span></span>
   * <span data-ttu-id="daa7b-147">Database Hive: predefinito</span><span class="sxs-lookup"><span data-stu-id="daa7b-147">Hive Database: default</span></span>
   * <span data-ttu-id="daa7b-148">Tabella: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="daa7b-148">table: hivesampletable</span></span>
   * <span data-ttu-id="daa7b-149">Colonna Hive: clientid, devicemake</span><span class="sxs-lookup"><span data-stu-id="daa7b-149">Hive column: clientid, devicemake</span></span>
   * <span data-ttu-id="daa7b-150">Seleziona utente: hiveuser2</span><span class="sxs-lookup"><span data-stu-id="daa7b-150">Select User: hiveuser2</span></span>
   * <span data-ttu-id="daa7b-151">Autorizzazioni: selezionare</span><span class="sxs-lookup"><span data-stu-id="daa7b-151">Permissions: select</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="daa7b-152">Creare un'origine dati Hive ODBC</span><span class="sxs-lookup"><span data-stu-id="daa7b-152">Create Hive ODBC data source</span></span>
<span data-ttu-id="daa7b-153">Le istruzioni sono disponibili in [Creare un'origine dati Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="daa7b-153">The instructions can be found in [Create Hive ODBC data source](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>  

    <span data-ttu-id="daa7b-154">Proprietà</span><span class="sxs-lookup"><span data-stu-id="daa7b-154">Property</span></span>|<span data-ttu-id="daa7b-155">Descrizione</span><span class="sxs-lookup"><span data-stu-id="daa7b-155">Description</span></span>
    ---|---
    <span data-ttu-id="daa7b-156">Data Source Name</span><span class="sxs-lookup"><span data-stu-id="daa7b-156">Data Source Name</span></span>|<span data-ttu-id="daa7b-157">Assegnare un nome all'origine dati</span><span class="sxs-lookup"><span data-stu-id="daa7b-157">Give a name to your data source</span></span>
    <span data-ttu-id="daa7b-158">Host</span><span class="sxs-lookup"><span data-stu-id="daa7b-158">Host</span></span>|<span data-ttu-id="daa7b-159">Immettere &lt;HDInsightClusterName>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="daa7b-159">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="daa7b-160">Ad esempio, myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="daa7b-160">For example, myHDICluster.azurehdinsight.net</span></span>
    <span data-ttu-id="daa7b-161">Porta</span><span class="sxs-lookup"><span data-stu-id="daa7b-161">Port</span></span>|<span data-ttu-id="daa7b-162">Utilizzare <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="daa7b-162">Use <strong>443</strong>.</span></span> <span data-ttu-id="daa7b-163">Questa porta è passata da 563 a 443.</span><span class="sxs-lookup"><span data-stu-id="daa7b-163">(This port has been changed from 563 to 443.)</span></span>
    <span data-ttu-id="daa7b-164">Database</span><span class="sxs-lookup"><span data-stu-id="daa7b-164">Database</span></span>|<span data-ttu-id="daa7b-165">Usare l'<strong>impostazione predefinita</strong>.</span><span class="sxs-lookup"><span data-stu-id="daa7b-165">Use <strong>Default</strong>.</span></span>
    <span data-ttu-id="daa7b-166">Hive Server Type</span><span class="sxs-lookup"><span data-stu-id="daa7b-166">Hive Server Type</span></span>|<span data-ttu-id="daa7b-167">Selezionare <strong>Hive Server 2</strong></span><span class="sxs-lookup"><span data-stu-id="daa7b-167">Select <strong>Hive Server 2</strong></span></span>
    <span data-ttu-id="daa7b-168">Mechanism</span><span class="sxs-lookup"><span data-stu-id="daa7b-168">Mechanism</span></span>|<span data-ttu-id="daa7b-169">Selezionare <strong>Azure HDInsight Service</strong></span><span class="sxs-lookup"><span data-stu-id="daa7b-169">Select <strong>Azure HDInsight Service</strong></span></span>
    <span data-ttu-id="daa7b-170">HTTP Path</span><span class="sxs-lookup"><span data-stu-id="daa7b-170">HTTP Path</span></span>|<span data-ttu-id="daa7b-171">Lasciare vuoto.</span><span class="sxs-lookup"><span data-stu-id="daa7b-171">Leave it blank.</span></span>
    <span data-ttu-id="daa7b-172">User Name</span><span class="sxs-lookup"><span data-stu-id="daa7b-172">User Name</span></span>|<span data-ttu-id="daa7b-173">Immettere hiveuser1@contoso158.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="daa7b-173">Enter hiveuser1@contoso158.onmicrosoft.com.</span></span> <span data-ttu-id="daa7b-174">Se diverso, aggiornare il nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="daa7b-174">Update the domain name if it is different.</span></span>
    <span data-ttu-id="daa7b-175">Password</span><span class="sxs-lookup"><span data-stu-id="daa7b-175">Password</span></span>|<span data-ttu-id="daa7b-176">Immettere la password per hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="daa7b-176">Enter the password for hiveuser1.</span></span>
    </table>

<span data-ttu-id="daa7b-177">Assicurarsi di fare clic su **Test** prima di salvare l'origine dati.</span><span class="sxs-lookup"><span data-stu-id="daa7b-177">Make sure to click **Test** before saving the data source.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="daa7b-178">Importazione di dati in Excel da HDInsight</span><span class="sxs-lookup"><span data-stu-id="daa7b-178">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="daa7b-179">Nell'ultima sezione, sono stati configurati due criteri.</span><span class="sxs-lookup"><span data-stu-id="daa7b-179">In the last section, you have configured two policies.</span></span>  <span data-ttu-id="daa7b-180">hiveuser1 dispone dell'autorizzazione di selezione in tutte le colonne, mentre hiveuser2 solo in due di loro.</span><span class="sxs-lookup"><span data-stu-id="daa7b-180">hiveuser1 has the select permission on all the columns, and hiveuser2 has the select permission on two columns.</span></span> <span data-ttu-id="daa7b-181">In questa sezione vengono rappresentati due utenti che importano dati in Excel.</span><span class="sxs-lookup"><span data-stu-id="daa7b-181">In this section, you impersonate the two users to import data into Excel.</span></span>

1. <span data-ttu-id="daa7b-182">Aprire una cartella di lavoro nuova o esistente in Excel.</span><span class="sxs-lookup"><span data-stu-id="daa7b-182">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="daa7b-183">Nella scheda **Dati** fare clic su **From Other Data Sources** (Da altre origini dati) e quindi su **From Data Connection Wizard** (Da Connessione guidata dati) per avviare la **Connessione guidata dati**.</span><span class="sxs-lookup"><span data-stu-id="daa7b-183">From the **Data** tab, click **From Other Data Sources**, and then click **From Data Connection Wizard** to launch the **Data Connection Wizard**.</span></span>

    <span data-ttu-id="daa7b-184">![Aprire Connessione guidata dati][img-hdi-simbahiveodbc.excel.dataconnection]</span><span class="sxs-lookup"><span data-stu-id="daa7b-184">![Open data connection wizard][img-hdi-simbahiveodbc.excel.dataconnection]</span></span>
3. <span data-ttu-id="daa7b-185">Selezionare **Nome origine dati ODBC DSN** come origine dati e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="daa7b-185">Select **ODBC DSN** as the data source, and then click **Next**.</span></span>
4. <span data-ttu-id="daa7b-186">Nelle origini dati ODBC selezionare il nome dell'origine dati creato nel passaggio precedente e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="daa7b-186">From ODBC data sources, select the data source name that you created in the previous step, and then  click **Next**.</span></span>
5. <span data-ttu-id="daa7b-187">Immettere nuovamente la password per il cluster nella procedura guidata e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="daa7b-187">Re-enter the password for the cluster in the wizard, and then click **OK**.</span></span> <span data-ttu-id="daa7b-188">Attendere l'apertura della finestra di dialogo **Seleziona database e tabella** .</span><span class="sxs-lookup"><span data-stu-id="daa7b-188">Wait for the **Select Database and Table** dialog to open.</span></span> <span data-ttu-id="daa7b-189">Questa operazione potrebbe richiedere alcuni secondi.</span><span class="sxs-lookup"><span data-stu-id="daa7b-189">This can take a few seconds.</span></span>
6. <span data-ttu-id="daa7b-190">Selezionare **hivesampletable**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="daa7b-190">Select **hivesampletable**, and then click **Next**.</span></span>
7. <span data-ttu-id="daa7b-191">Fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="daa7b-191">Click **Finish**.</span></span>
8. <span data-ttu-id="daa7b-192">Nella finestra di dialogo **Importa dati** è possibile modificare o specificare la query.</span><span class="sxs-lookup"><span data-stu-id="daa7b-192">In the **Import Data** dialog, you can change or specify the query.</span></span> <span data-ttu-id="daa7b-193">A questo scopo, fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="daa7b-193">To do so, click **Properties**.</span></span> <span data-ttu-id="daa7b-194">Questa operazione potrebbe richiedere alcuni secondi.</span><span class="sxs-lookup"><span data-stu-id="daa7b-194">This can take a few seconds.</span></span>
9. <span data-ttu-id="daa7b-195">Fare clic sulla scheda **Definizione**.</span><span class="sxs-lookup"><span data-stu-id="daa7b-195">Click the **Definition** tab.</span></span> <span data-ttu-id="daa7b-196">Il testo del comando è:</span><span class="sxs-lookup"><span data-stu-id="daa7b-196">The command text is:</span></span>

       SELECT * FROM "HIVE"."default"."hivesampletable"

   <span data-ttu-id="daa7b-197">In base ai criteri di Ranger che sono stati definiti, hiveuser1 dispone dell'autorizzazione di selezione su tutte le colonne.</span><span class="sxs-lookup"><span data-stu-id="daa7b-197">By the Ranger policies you defined,  hiveuser1 has select permission on all the columns.</span></span>  <span data-ttu-id="daa7b-198">Pertanto, questa query funziona con le credenziali di hiveuser1, ma non con quelle di hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="daa7b-198">So this query works with hiveuser1's credentials, but this query does not not work with hiveuser2's credentials.</span></span>

   <span data-ttu-id="daa7b-199">![Proprietà di connessione][img-hdi-simbahiveodbc-excel-connectionproperties]</span><span class="sxs-lookup"><span data-stu-id="daa7b-199">![Connection Properties][img-hdi-simbahiveodbc-excel-connectionproperties]</span></span>
10. <span data-ttu-id="daa7b-200">Fare clic su **OK** per chiudere la finestra di dialogo Proprietà connessione.</span><span class="sxs-lookup"><span data-stu-id="daa7b-200">Click **OK** to close the Connection Properties dialog.</span></span>
11. <span data-ttu-id="daa7b-201">Fare clic su **OK** per chiudere la finestra di dialogo **Importa dati**.</span><span class="sxs-lookup"><span data-stu-id="daa7b-201">Click **OK** to close the **Import Data** dialog.</span></span>  
12. <span data-ttu-id="daa7b-202">Reimmettere la password per hiveuser1, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="daa7b-202">Reenter the password for hiveuser1, and then click **OK**.</span></span> <span data-ttu-id="daa7b-203">L'importazione dei dati in Excel potrebbe richiedere alcuni secondi.</span><span class="sxs-lookup"><span data-stu-id="daa7b-203">It takes a few seconds before data gets imported to Excel.</span></span> <span data-ttu-id="daa7b-204">Al termine, verranno visualizzate 11 colonne di dati.</span><span class="sxs-lookup"><span data-stu-id="daa7b-204">When it is done, you shall see 11 columns of data.</span></span>

<span data-ttu-id="daa7b-205">Per il test del secondo criterio (read-hivesampletable-devicemake) creato nell'ultima sezione</span><span class="sxs-lookup"><span data-stu-id="daa7b-205">To test the second policy (read-hivesampletable-devicemake) you created in the last section</span></span>

1. <span data-ttu-id="daa7b-206">Aggiungere un nuovo foglio in Excel.</span><span class="sxs-lookup"><span data-stu-id="daa7b-206">Add a new sheet in Excel.</span></span>
2. <span data-ttu-id="daa7b-207">Seguire l'ultima procedura per importare i dati.</span><span class="sxs-lookup"><span data-stu-id="daa7b-207">Follow the last procedure to import the data.</span></span>  <span data-ttu-id="daa7b-208">L'unica differenza è che verranno usate le credenziali di hiveuser2 anziché quelle di hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="daa7b-208">The only change you will make is to use hiveuser2's credentials instead of hiveuser1's.</span></span> <span data-ttu-id="daa7b-209">L'esito sarà negativo perché hiveuser2 dispone solo dell'autorizzazione per visualizzare due colonne.</span><span class="sxs-lookup"><span data-stu-id="daa7b-209">This will fail because hiveuser2 only has permission to see two columns.</span></span> <span data-ttu-id="daa7b-210">Verrà visualizzato l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="daa7b-210">You shall get the following error:</span></span>

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. <span data-ttu-id="daa7b-211">Seguire la stessa procedura per importare i dati.</span><span class="sxs-lookup"><span data-stu-id="daa7b-211">Follow the same procedure to import data.</span></span> <span data-ttu-id="daa7b-212">Questa volta usare le credenziali di hiveuser2 e modificare l'istruzione di selezione da:</span><span class="sxs-lookup"><span data-stu-id="daa7b-212">This time, use hiveuser2's credentials, and also modify the select statement from:</span></span>

        SELECT * FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="daa7b-213">in:</span><span class="sxs-lookup"><span data-stu-id="daa7b-213">to:</span></span>

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="daa7b-214">Al termine, verranno visualizzate due colonne di dati importati.</span><span class="sxs-lookup"><span data-stu-id="daa7b-214">When it is done, you shall see two columns of data imported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="daa7b-215">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="daa7b-215">Next steps</span></span>
* <span data-ttu-id="daa7b-216">Per configurare un cluster HDInsight aggiunto al dominio, vedere [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configurare i cluster HDInsight aggiunti al dominio).</span><span class="sxs-lookup"><span data-stu-id="daa7b-216">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="daa7b-217">Per gestire cluster HDInsight aggiunti al dominio, vedere [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Gestire i cluster HDInsight aggiunti al dominio).</span><span class="sxs-lookup"><span data-stu-id="daa7b-217">For managing a Domain-joined HDInsight clusters, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>
* <span data-ttu-id="daa7b-218">Per eseguire query Hive usando SSH nei cluster HDInsight aggiunti al dominio, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="daa7b-218">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
* <span data-ttu-id="daa7b-219">Per connettere Hive usando JDBC, vedere [Connettersi a Hive in Azure HDInsight con il driver Hive JDBC](hdinsight-connect-hive-jdbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="daa7b-219">For Connecting Hive using Hive JDBC, see [Connect to Hive on Azure HDInsight using the Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)</span></span>
* <span data-ttu-id="daa7b-220">Per connettere Excel a Hadoop usando ODBC, vedere [Connettere Excel a Hadoop mediante Microsoft Hive ODBC Driver](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="daa7b-220">For connecting Excel to Hadoop using Hive ODBC, see [Connect Excel to Hadoop with the Microsoft Hive ODBC drive](hdinsight-connect-excel-hive-odbc-driver.md)</span></span>
* <span data-ttu-id="daa7b-221">Per connettere Excel a Hadoop usando Power Query, vedere [Connettere Excel a Hadoop mediante Power Query](hdinsight-connect-excel-power-query.md).</span><span class="sxs-lookup"><span data-stu-id="daa7b-221">For connecting Excel to Hadoop using Power Query, see [Connect Excel to Hadoop by using Power Query](hdinsight-connect-excel-power-query.md)</span></span>
