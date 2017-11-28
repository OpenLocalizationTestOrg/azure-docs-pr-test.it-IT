---
title: cluster HDInsight dominio aaaManage - Azure | Documenti Microsoft
description: Informazioni su come toomanage HDInsight dominio cluster
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 6ebc4d2f-2f6a-4e1e-ab6d-af4db6b4c87c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 233ddf0953e981f9a24b77d9dde194d590e5e6d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a><span data-ttu-id="370ba-103">Gestione dei cluster HDInsight aggiunti al dominio (anteprima)</span><span class="sxs-lookup"><span data-stu-id="370ba-103">Manage Domain-joined HDInsight clusters (Preview)</span></span>
<span data-ttu-id="370ba-104">Informazioni su hello utenti e ruoli di hello in HDInsight appartenenti a un dominio, e come toomanage HDInsight dominio cluster.</span><span class="sxs-lookup"><span data-stu-id="370ba-104">Learn hello users and hello roles in Domain-joined HDInsight, and how toomanage domain-joined HDInsight clusters.</span></span>

## <a name="users-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="370ba-105">Utenti dei cluster HDInsight aggiunti al dominio</span><span class="sxs-lookup"><span data-stu-id="370ba-105">Users of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="370ba-106">Un cluster di HDInsight non aggiunti al dominio è disponibili due account utente creati durante la creazione di cluster hello:</span><span class="sxs-lookup"><span data-stu-id="370ba-106">An HDInsight cluster that is not domain-joined has two user accounts that are created during hello cluster creation:</span></span>

* <span data-ttu-id="370ba-107">**Amministratore Ambari**: questo account è denominato anche *Utente Hadoop* o *Utente HTTP*.</span><span class="sxs-lookup"><span data-stu-id="370ba-107">**Ambari admin**: This account is also known as *Hadoop user* or *HTTP user*.</span></span> <span data-ttu-id="370ba-108">Questo account può essere utilizzato toolog su tooAmbari in https://&lt;clustername >. cluster>.azurehdinsight.NET.</span><span class="sxs-lookup"><span data-stu-id="370ba-108">This account can be used toolog on tooAmbari at https://&lt;clustername>.azurehdinsight.net.</span></span> <span data-ttu-id="370ba-109">Può anche essere utilizzati toorun query sulle viste Ambari, eseguire i processi tramite strumenti esterni (ad esempio PowerShell, Templeton, Visual Studio) e l'autenticazione con il driver ODBC Hive hello e strumenti di Business Intelligence (ad esempio Excel, Power BI o Tableau).</span><span class="sxs-lookup"><span data-stu-id="370ba-109">It can also be used toorun queries on Ambari views, execute jobs via external tools (i.e. PowerShell, Templeton, Visual Studio), and authenticate with hello Hive ODBC driver and BI tools (i.e. Excel, PowerBI, or Tableau).</span></span>
* <span data-ttu-id="370ba-110">**Utente SSH**: questo account può essere usato con SSH e per eseguire comandi sudo.</span><span class="sxs-lookup"><span data-stu-id="370ba-110">**SSH user**:  This account can be used with SSH, and execute sudo commands.</span></span> <span data-ttu-id="370ba-111">Dispone di privilegi di radice toohello le macchine virtuali Linux.</span><span class="sxs-lookup"><span data-stu-id="370ba-111">It has root privileges toohello Linux VMs.</span></span>

<span data-ttu-id="370ba-112">Un cluster di HDInsight dominio dispone di tre nuovi utenti dell'utente di amministrazione e SSH tooAmbari aggiunta.</span><span class="sxs-lookup"><span data-stu-id="370ba-112">A domain-joined HDInsight cluster has three new users in addition tooAmbari Admin and SSH user.</span></span>

* <span data-ttu-id="370ba-113">**Amministrazione cane**: questo account è hello locale Apache cane amministratore account.</span><span class="sxs-lookup"><span data-stu-id="370ba-113">**Ranger admin**:  This account is hello local Apache Ranger admin account.</span></span> <span data-ttu-id="370ba-114">Non si tratta di un utente del dominio di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="370ba-114">It is not an active directory domain user.</span></span> <span data-ttu-id="370ba-115">Questo account può essere toosetup utilizzato criteri e verificare altri utenti amministratori o gli amministratori delegati (in modo che gli utenti possono gestire i criteri).</span><span class="sxs-lookup"><span data-stu-id="370ba-115">This account can be used toosetup policies and make other users admins or delegated admins (so that those users can manage policies).</span></span> <span data-ttu-id="370ba-116">Per impostazione predefinita, il nome utente hello è *admin* e la password di hello è hello stesso hello Ambari password di amministratore.</span><span class="sxs-lookup"><span data-stu-id="370ba-116">By default, hello username is *admin* and hello password is hello same as hello Ambari admin password.</span></span> <span data-ttu-id="370ba-117">password Hello può essere aggiornata dalla pagina Impostazioni hello cane.</span><span class="sxs-lookup"><span data-stu-id="370ba-117">hello password can be updated from hello Settings page in Ranger.</span></span>
* <span data-ttu-id="370ba-118">**Utente di dominio amministratore cluster**: questo account è un utente di dominio active directory designato come amministratore di cluster Hadoop inclusi Ambari e cane hello.</span><span class="sxs-lookup"><span data-stu-id="370ba-118">**Cluster admin domain user**: This account is an active directory domain user designated as hello Hadoop cluster admin including Ambari and Ranger.</span></span> <span data-ttu-id="370ba-119">Durante la creazione del cluster, è necessario fornire le credenziali dell'utente.</span><span class="sxs-lookup"><span data-stu-id="370ba-119">You must provide this user’s credentials during cluster creation.</span></span> <span data-ttu-id="370ba-120">A questo utente è hello seguenti privilegi:</span><span class="sxs-lookup"><span data-stu-id="370ba-120">This user has hello following privileges:</span></span>

  * <span data-ttu-id="370ba-121">Aggiunta a dominio toohello macchine e inserirli in hello unità Organizzativa specificata durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="370ba-121">Join machines toohello domain and place them within hello OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="370ba-122">Creare entità di servizio all'interno di hello unità Organizzativa specificata durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="370ba-122">Create service principals within hello OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="370ba-123">Creazione delle voci DNS inverse.</span><span class="sxs-lookup"><span data-stu-id="370ba-123">Create reverse DNS entries.</span></span>

    <span data-ttu-id="370ba-124">Hello nota altri utenti di Active Directory dispongano anche di questi privilegi.</span><span class="sxs-lookup"><span data-stu-id="370ba-124">Note hello other AD users also have these privileges.</span></span>

    <span data-ttu-id="370ba-125">Esistono alcuni punti di fine all'interno di cluster hello (ad esempio, Templeton) che non sono gestiti da cane e pertanto non sono protetti.</span><span class="sxs-lookup"><span data-stu-id="370ba-125">There are some end points within hello cluster (for example, Templeton) which are not managed by Ranger, and hence are not secure.</span></span> <span data-ttu-id="370ba-126">Questi punti vengono bloccati per tutti gli utenti tranne l'utente di dominio amministratore cluster hello.</span><span class="sxs-lookup"><span data-stu-id="370ba-126">These end points are locked down for all users except hello cluster admin domain user.</span></span>
* <span data-ttu-id="370ba-127">**Normale**: durante la creazione del cluster, è possibile specificare più gruppi di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="370ba-127">**Regular**: During cluster creation, you can provide multiple active directory groups.</span></span> <span data-ttu-id="370ba-128">gli utenti di Hello di questi gruppi verranno sincronizzati tooRanger e Ambari.</span><span class="sxs-lookup"><span data-stu-id="370ba-128">hello users in these groups will be synced tooRanger and Ambari.</span></span> <span data-ttu-id="370ba-129">Questi utenti sono utenti di dominio e avranno accesso tooonly gestiti cane endpoint (ad esempio, Hiveserver2).</span><span class="sxs-lookup"><span data-stu-id="370ba-129">These users are domain users and will have access tooonly Ranger-managed endpoints (for example, Hiveserver2).</span></span> <span data-ttu-id="370ba-130">Tutti i criteri RBAC di hello e il controllo sarà utenti toothese applicabile.</span><span class="sxs-lookup"><span data-stu-id="370ba-130">All hello RBAC policies and auditing will be applicable toothese users.</span></span>

## <a name="roles-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="370ba-131">Ruoli dei cluster HDInsight aggiunti al dominio</span><span class="sxs-lookup"><span data-stu-id="370ba-131">Roles of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="370ba-132">HDInsight dominio hanno hello seguenti ruoli:</span><span class="sxs-lookup"><span data-stu-id="370ba-132">Domain-joined HDInsight have hello following roles:</span></span>

* <span data-ttu-id="370ba-133">Amministratore del cluster</span><span class="sxs-lookup"><span data-stu-id="370ba-133">Cluster Administrator</span></span>
* <span data-ttu-id="370ba-134">Operatore del cluster</span><span class="sxs-lookup"><span data-stu-id="370ba-134">Cluster Operator</span></span>
* <span data-ttu-id="370ba-135">Amministratore del servizio</span><span class="sxs-lookup"><span data-stu-id="370ba-135">Service Administrator</span></span>
* <span data-ttu-id="370ba-136">Operatore del servizio</span><span class="sxs-lookup"><span data-stu-id="370ba-136">Service Operator</span></span>
* <span data-ttu-id="370ba-137">Utente del cluster</span><span class="sxs-lookup"><span data-stu-id="370ba-137">Cluster User</span></span>

<span data-ttu-id="370ba-138">**autorizzazioni di hello toosee di questi ruoli**</span><span class="sxs-lookup"><span data-stu-id="370ba-138">**toosee hello permissions of these roles**</span></span>

1. <span data-ttu-id="370ba-139">Aprire l'interfaccia utente Gestione Ambari hello.</span><span class="sxs-lookup"><span data-stu-id="370ba-139">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="370ba-140">Vedere [aprire hello dell'interfaccia utente Gestione Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="370ba-140">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="370ba-141">Scegliere dal menu a sinistra hello **ruoli**.</span><span class="sxs-lookup"><span data-stu-id="370ba-141">From hello left menu, click **Roles**.</span></span>
3. <span data-ttu-id="370ba-142">Fare clic su hello blu punto interrogativo toosee hello autorizzazioni:</span><span class="sxs-lookup"><span data-stu-id="370ba-142">Click hello blue question mark toosee hello permissions:</span></span>

    ![Autorizzazioni dei ruoli dei cluster HDInsight aggiunti al dominio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-hello-ambari-management-ui"></a><span data-ttu-id="370ba-144">Aprire l'interfaccia utente Gestione Ambari hello</span><span class="sxs-lookup"><span data-stu-id="370ba-144">Open hello Ambari Management UI</span></span>
1. <span data-ttu-id="370ba-145">Accesso toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="370ba-145">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="370ba-146">Aprire il cluster HDInsight in un pannello.</span><span class="sxs-lookup"><span data-stu-id="370ba-146">Open your HDInsight cluster in a blade.</span></span> <span data-ttu-id="370ba-147">Vedere [Elencare e visualizzare i cluster](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="370ba-147">See [List and show clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span></span>
3. <span data-ttu-id="370ba-148">Fare clic su **Dashboard** dal menu principale di hello tooopen Ambari.</span><span class="sxs-lookup"><span data-stu-id="370ba-148">Click **Dashboard** from hello top menu tooopen Ambari.</span></span>
4. <span data-ttu-id="370ba-149">Accedere utilizzando la password e nome utente di dominio amministratore cluster hello tooAmbari.</span><span class="sxs-lookup"><span data-stu-id="370ba-149">Log on tooAmbari using hello cluster administrator domain user name and password.</span></span>
5. <span data-ttu-id="370ba-150">Fare clic su hello **Admin** menu a discesa da hello angolo superiore destro e quindi fare clic su **gestire Ambari**.</span><span class="sxs-lookup"><span data-stu-id="370ba-150">Click hello **Admin** dropdown menu from hello upper right corner, and then click **Manage Ambari**.</span></span>

    ![Gestire Ambari nel cluster HDInsight aggiunto al dominio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    <span data-ttu-id="370ba-152">Hello dell'interfaccia utente simile a:</span><span class="sxs-lookup"><span data-stu-id="370ba-152">hello UI looks like:</span></span>

    ![Interfaccia utente della gestione di Ambari nel cluster HDInsight aggiunto al dominio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-hello-domain-users-synchronized-from-your-active-directory"></a><span data-ttu-id="370ba-154">Elenco utenti del dominio hello sincronizzati da Active Directory</span><span class="sxs-lookup"><span data-stu-id="370ba-154">List hello domain users synchronized from your Active Directory</span></span>
1. <span data-ttu-id="370ba-155">Aprire l'interfaccia utente Gestione Ambari hello.</span><span class="sxs-lookup"><span data-stu-id="370ba-155">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="370ba-156">Vedere [aprire hello dell'interfaccia utente Gestione Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="370ba-156">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="370ba-157">Scegliere dal menu a sinistra hello **utenti**.</span><span class="sxs-lookup"><span data-stu-id="370ba-157">From hello left menu, click **Users**.</span></span> <span data-ttu-id="370ba-158">Vedrai tutti gli utenti di hello sincronizzati da cluster HDInsight toohello Active Directory.</span><span class="sxs-lookup"><span data-stu-id="370ba-158">You shall see all hello users synced from your Active Directory toohello HDInsight cluster.</span></span>

    ![Elenco degli utenti dell'interfaccia per la gestione di Ambari nel cluster HDInsight aggiunto al dominio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-hello-domain-groups-synchronized-from-your-active-directory"></a><span data-ttu-id="370ba-160">Elenco di gruppi di dominio hello sincronizzati da Active Directory</span><span class="sxs-lookup"><span data-stu-id="370ba-160">List hello domain groups synchronized from your Active Directory</span></span>
1. <span data-ttu-id="370ba-161">Aprire l'interfaccia utente Gestione Ambari hello.</span><span class="sxs-lookup"><span data-stu-id="370ba-161">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="370ba-162">Vedere [aprire hello dell'interfaccia utente Gestione Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="370ba-162">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="370ba-163">Scegliere dal menu a sinistra hello **gruppi**.</span><span class="sxs-lookup"><span data-stu-id="370ba-163">From hello left menu, click **Groups**.</span></span> <span data-ttu-id="370ba-164">Vedrai tutti i gruppi di hello sincronizzati da cluster HDInsight toohello Active Directory.</span><span class="sxs-lookup"><span data-stu-id="370ba-164">You shall see all hello groups synced from your Active Directory toohello HDInsight cluster.</span></span>

    ![Elenco dei gruppi dell'interfaccia utente per la gestione di Ambari nel cluster HDInsight aggiunto al dominio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a><span data-ttu-id="370ba-166">Configurare le autorizzazioni delle viste Hive</span><span class="sxs-lookup"><span data-stu-id="370ba-166">Configure Hive Views permissions</span></span>
1. <span data-ttu-id="370ba-167">Aprire l'interfaccia utente Gestione Ambari hello.</span><span class="sxs-lookup"><span data-stu-id="370ba-167">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="370ba-168">Vedere [aprire hello dell'interfaccia utente Gestione Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="370ba-168">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="370ba-169">Scegliere dal menu a sinistra hello **viste**.</span><span class="sxs-lookup"><span data-stu-id="370ba-169">From hello left menu, click **Views**.</span></span>
3. <span data-ttu-id="370ba-170">Fare clic su **HIVE** dettagli hello tooshow.</span><span class="sxs-lookup"><span data-stu-id="370ba-170">Click **HIVE** tooshow hello details.</span></span>

    ![Viste Hive dell'interfaccia utente per la gestione di Ambari nel cluster HDInsight aggiunto al dominio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. <span data-ttu-id="370ba-172">Fare clic su hello **visualizzazione Hive** collegamento tooconfigure Hive viste.</span><span class="sxs-lookup"><span data-stu-id="370ba-172">Click hello **Hive View** link tooconfigure Hive Views.</span></span>
5. <span data-ttu-id="370ba-173">Scorrere verso il basso toohello **autorizzazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="370ba-173">Scroll down toohello **Permissions** section.</span></span>

    ![Configurare le autorizzazioni delle viste Hive nell'interfaccia utente per la gestione di Ambari nel cluster HDInsight aggiunto al dominio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. <span data-ttu-id="370ba-175">Fare clic su **Aggiungi utente** o **Aggiungi gruppo**, quindi specificare hello utenti o gruppi che è possono utilizzare viste Hive.</span><span class="sxs-lookup"><span data-stu-id="370ba-175">Click **Add User** or **Add Group**, and then specify hello users or groups that can use Hive Views.</span></span>

## <a name="configure-users-for-hello-roles"></a><span data-ttu-id="370ba-176">Configurare gli utenti per i ruoli di hello</span><span class="sxs-lookup"><span data-stu-id="370ba-176">Configure users for hello roles</span></span>
 <span data-ttu-id="370ba-177">vedere un elenco di ruoli e le relative autorizzazioni, toosee [cluster HDInsight ruoli di dominio](#roles-of-domain---joined-hdinsight-clusters).</span><span class="sxs-lookup"><span data-stu-id="370ba-177">toosee a list of roles and their permissions, see [Roles of Domain-joined HDInsight clusters](#roles-of-domain---joined-hdinsight-clusters).</span></span>

1. <span data-ttu-id="370ba-178">Aprire l'interfaccia utente Gestione Ambari hello.</span><span class="sxs-lookup"><span data-stu-id="370ba-178">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="370ba-179">Vedere [aprire hello dell'interfaccia utente Gestione Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="370ba-179">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="370ba-180">Scegliere dal menu a sinistra hello **ruoli**.</span><span class="sxs-lookup"><span data-stu-id="370ba-180">From hello left menu, click **Roles**.</span></span>
3. <span data-ttu-id="370ba-181">Fare clic su **Aggiungi utente** o **Aggiungi gruppo** tooassign utenti e gruppi toodifferent i ruoli.</span><span class="sxs-lookup"><span data-stu-id="370ba-181">Click **Add User** or **Add Group** tooassign users and groups toodifferent roles.</span></span>

## <a name="next-steps"></a><span data-ttu-id="370ba-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="370ba-182">Next steps</span></span>
* <span data-ttu-id="370ba-183">Per configurare un cluster HDInsight aggiunto al dominio, vedere [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configurare i cluster HDInsight aggiunti al dominio).</span><span class="sxs-lookup"><span data-stu-id="370ba-183">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="370ba-184">Per configurare i criteri ed eseguire query Hive, vedere [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md) (Configurare criteri Hive per cluster HDInsight aggiunti al dominio).</span><span class="sxs-lookup"><span data-stu-id="370ba-184">For configuring Hive policies and run Hive queries, see [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md).</span></span>
* <span data-ttu-id="370ba-185">Per eseguire query Hive usando SSH nei cluster HDInsight aggiunti al dominio, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="370ba-185">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
