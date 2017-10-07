---
title: cluster di HDInsight appartenenti a un dominio con PowerShell - Azure aaaConfigure | Documenti Microsoft
description: Informazioni su come tooset e configurare cluster di HDInsight appartenenti a un dominio con Azure PowerShell
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: a13b2f7a-612d-4800-bc92-7fc0524f3e89
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/02/2016
ms.author: saurinsh
ms.openlocfilehash: 49da3439513d1e51171f0f7f7f9c3d967d55cb7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-domain-joined-hdinsight-clusters-preview-using-azure-powershell"></a>Configurare cluster HDInsight aggiunti al dominio (anteprima) usando Azure PowerShell
Informazioni su come tooset backup un Azure HDInsight cluster con Azure Active Directory (Azure AD) e [cane Apache](http://hortonworks.com/apache/ranger/) con Azure PowerShell. Configurazione di hello toomake più veloce e meno soggetto a errori, viene fornito uno script di PowerShell di Azure. HDInsight aggiunto al dominio può essere configurato solo nei cluster basati su Linux. Per altre informazioni, consultare [Introduce Domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md) (Introduzione ai cluster HDInsight aggiunti al dominio).

> [!IMPORTANT]
> Oozie non è abilitato su HDInsight appartenente al dominio.

Una configurazione del cluster HDInsight dominio tipico prevede hello alla procedura seguente:

1. Creare una rete virtuale classica di Azure per Azure AD.  
2. Creare e configurare Azure AD e Azure AD DS.
3. Aggiungere una macchina virtuale toohello classico rete virtuale per la creazione di un'unità organizzativa. 
4. Creare un'unità organizzativa per Azure AD DS.
5. Creare un HDInsight VNet in modalità di gestione risorse di Azure hello.
6. Configurare le zone DNS inverso per hello Azure Active Directory.
7. Peer hello due reti virtuali.
8. Creare un cluster HDInsight

Hello fornito uno script di PowerShell esegue i passaggi da 3 a 7. È necessario eseguire manualmente i passaggi 1 e 2.  Se si preferisce non toouse Azure PowerShell, vedere [cluster HDInsight configurare dominio](hdinsight-domain-joined-configure.md). 

Un esempio di topologia finale hello è simile al seguente:

![Topologia di HDInsight aggiunto al dominio](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-topology.png)

Dal momento che attualmente Azure AD supporta solo le reti virtuali classiche mentre i cluster HDInsight basati su Linux supportano solo reti virtuali basate su Azure Resource Manager, l'integrazione di Azure AD HDInsight richiede due reti virtuali e il peering tra di loro. Per informazioni sul confronto hello tra modelli di distribuzione hello due, vedere [Azure Resource Manager e distribuzione classica: comprendere i modelli di distribuzione e lo stato delle risorse di hello](../azure-resource-manager/resource-manager-deployment-model.md). devono essere di due reti virtuali in hello Hello stessa area hello Azure Active Directory.

> [!NOTE]
> In questa esercitazione si presuppone che non sia disponibile un account Azure. Se si dispone di uno, è possibile ignorare la parte hello nel passaggio 2.
> 
> 

## <a name="prerequisites"></a>Prerequisiti
È necessario disporre di hello toogo gli elementi di questa esercitazione seguente:

* Acquisire familiarità con [Azure AD Domain Services](https://azure.microsoft.com/services/active-directory-ds/) e con la struttura dei [prezzi](https://azure.microsoft.com/pricing/details/active-directory-ds/).
* Assicurarsi che la sottoscrizione sia consentita per questa anteprima pubblica. È possibile farlo mediante l'invio di un messaggio di posta elettronica toohdipreview@microsoft.com con l'ID sottoscrizione.
* Un certificato SSL firmato da un'autorità di firma per il dominio. Hello richieste tramite la configurazione di accesso LDAP sicuro. Non è possibile usare certificati autofirmati.
* Azure PowerShell.  Vedere [Install and configure Azure PowerShell](/powershell/azure/overview) (Installare e configurare Azure PowerShell).

## <a name="create-an-azure-classic-vnet-for-your-azure-ad"></a>Creare una rete virtuale classica di Azure per Azure AD.
Per istruzioni hello, vedere [qui](hdinsight-domain-joined-configure.md#create-an-azure-virtual-network-classic).

## <a name="create-and-configure-azure-ad-and-azure-ad-ds"></a>Creare e configurare Azure AD e Azure AD DS.
Per istruzioni hello, vedere [qui](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).

## <a name="run-hello-powershell-script"></a>Eseguire script PowerShell hello
Hello script di PowerShell può essere scaricato da [GitHub](https://github.com/hdinsight/DomainJoinedHDInsight). Estrarre il file zip hello e salvare localmente i file hello.

**hello tooedit script di PowerShell**

1. Aprire run.ps1 usando Windows PowerShell ISE o qualsiasi editor di testo.
2. Riempire i valori hello per hello seguenti variabili:
   
   * **$SubscriptionName** : hello nome della sottoscrizione di Azure in cui si desidera toocreate cluster HDInsight hello. È stato già creato una rete virtuale classica in questa sottoscrizione e creazione di una rete virtuale di Azure Resource Manager per il cluster HDInsight hello nella sottoscrizione.
   * **$ClassicVNetName** -hello classic rete virtuale che contiene hello Azure Active Directory. Questa rete virtuale deve essere in hello stessa sottoscrizione che viene fornito in precedenza. Questa rete virtuale deve essere creata tramite hello portale di Azure e non tramite il portale classico. Se si segue l'istruzione hello in [cluster HDInsight configurare dominio (anteprima)](hdinsight-domain-joined-configure.md#create-an-azure-virtual-network-classic), nome predefinito hello è contosoaadvnet.
   * **$ClassicResourceGroupName** : nome del gruppo di gestione risorse di hello per hello classic rete virtuale a cui è indicato in precedenza. ad esempio contosoaadrg. 
   * **$ArmResourceGroupName** : nome del gruppo di risorse di hello entro il quale, si desidera toocreate hello HDInsight cluster. È possibile utilizzare hello $ArmResourceGroupName stesso gruppo di risorse.  Se il gruppo di risorse hello non esiste, script hello Crea gruppo di risorse hello.
   * **$ArmVNetName** -nome di rete virtuale di gestione risorse hello entro il quale si desidera che toocreate hello HDInsight cluster. Questa rete virtuale verrà inserita in $ArmResourceGroupName.  Se hello rete virtuale non esiste, script di PowerShell hello creerà. Se esiste, deve essere parte del gruppo di risorse hello forniti sopra.
   * **$AddressVnetAddressSpace** : hello spazio degli indirizzi per la rete virtuale di hello Gestione risorse di rete. Assicurarsi che questo spazio indirizzi sia disponibile. Questo spazio di indirizzi non può sovrapporsi hello classic virtuale spazio indirizzi della rete. Ad esempio, "10.1.0.0/16".
   * **$ArmVnetSubnetName** -nome subnet rete virtuale di gestione delle risorse di hello entro il quale si desidera tooplace hello HDInsight cluster macchine virtuali. Se non esiste una subnet hello, script di PowerShell hello creerà. Se esiste, deve essere parte della rete virtuale hello forniti sopra.
   * **$AddressSubnetAddressSpace** : hello intervallo di indirizzi di subnet della rete virtuale hello Gestione risorse di rete. cluster HDInsight Hello che gli indirizzi IP della VM sarà da questo intervallo di indirizzi della subnet. Ad esempio, "10.1.0.0/24".
   * **$ActiveDirectoryDomainName** : il nome di dominio hello Azure AD che si desidera hello toojoin HDInsight le macchine virtuali del cluster. Ad esempio, "contoso.onmicrosoft.com".
   * **$ClusterUsersGroups** – nome comune di hello hello dei gruppi di sicurezza da Active Directory che si desidera toosync toohello HDInsight cluster. gli utenti di Hello all'interno di questo gruppo di sicurezza saranno in grado di toolog nel dashboard di cluster toohello utilizzando le credenziali di dominio active directory. Questi gruppi di sicurezza devono essere presente in active directory di hello. Ad esempio, "hiveusers" o "clusteroperatorusers".
   * **$OrganizationalUnitName** -unità organizzativa nel dominio hello, entro il quale si desidera cluster di HDInsight tooplace hello macchine virtuali e le entità di servizio utilizzate dal cluster hello hello hello. Se non esiste, Hello script di PowerShell creerà in questa unità Organizzativa. Ad esempio, "HDInsightOU".
3. Salvare le modifiche di hello.

**script hello toorun**

1. Eseguire **Windows PowerShell** come amministratore.
2. Sfoglia cartella toohello di run.ps1. 
3. Eseguire script hello digitando il nome di file hello e quindi premere **invio**.  Vengono visualizzate 3 finestre di dialogo di accesso:
   
   1. **Accedi al portale classico tooAzure** : immettere le credenziali che si utilizzano toosign nel portale classico tooAzure. È necessario avere creato hello Azure AD e Azure Active Directory utilizzando queste credenziali.
   2. **Accedi al portale di gestione risorse tooAzure** : immettere le credenziali che si utilizzano toosign nel portale di gestione risorse tooAzure.
   3. **Nome utente di dominio** : immettere le credenziali di hello hello utente del nome di dominio che si desidera che un amministratore nel cluster HDInsight hello toobe. Se è stata creata un'istanza di Azure AD da zero, questo utente deve essere stato creato usando questa documentazione. 
      
      > [!IMPORTANT]
      > Immettere nome utente hello nel formato seguente: 
      > 
      > Nomedominio\nomeutente (ad esempio, contoso.onmicrosoft.com\clusteradmin)
      > 
      > 
      
      L'utente deve disporre dei privilegi di 3: toojoin macchine toohello fornito il dominio di Active Directory. le entità servizio toocreate e gli oggetti computer all'interno di hello fornito un'unità organizzativa. e le regole del proxy tooadd inverse DNS.

Mentre richiederà la creazione le zone DNS inverse, script hello tooenter un'ID di rete. Questo ID di rete deve essere il prefisso di indirizzo hello di gestione delle risorse della rete virtuale. Ad esempio, se lo spazio degli indirizzi di subnet di rete virtuale di gestione risorse è 10.2.0.0/24, 10.2.0.0/24 immettere quando hello verrà chiesto di hello ID di rete. 

## <a name="create-hdinsight-cluster"></a>Creare un cluster HDInsight
In questa sezione si crea un cluster basati su Linux, Hadoop in HDInsight mediante uno hello portale di Azure o [modello di Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Per altri metodi di creazione del cluster e informazioni sulle impostazioni di hello, vedere [cluster HDInsight creare](hdinsight-hadoop-provision-linux-clusters.md). Per ulteriori informazioni sull'utilizzo di gestione risorse modello toocreate Hadoop cluster in HDInsight, vedere [cluster creare Hadoop in HDInsight mediante modelli di gestione risorse](hdinsight-hadoop-create-windows-clusters-arm-templates.md)

**un cluster HDInsight dominio mediante toocreate hello portale di Azure**

1. Accesso toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **Nuovo**, **Intelligence e analisi**, quindi su **HDInsight**.
3. Da hello **cluster HDInsight nuova** pannello, immettere o selezionare hello seguenti valori:
   
   * **Nome del cluster**: immettere un nuovo nome del cluster per cluster di HDInsight dominio hello.
   * **Sottoscrizione**: selezionare la sottoscrizione di Azure usata per creare il cluster.
   * **Configurazione cluster**:
     
     * **Tipo di cluster**: Hadoop. HDInsight aggiunto al dominio è attualmente supportato solo nei cluster Hadoop.
     * **Sistema operativo**: Linux.  HDInsight aggiunto al dominio è supportato solo nei cluster HDInsight basati su Linux.
     * **Versione**: Hadoop 2.7.3 (HDI 3.5). HDInsight aggiunto al dominio è supportato solo nei cluster HDInsight versione 3.5.
     * **Tipo di cluster**: PREMIUM
       
       Fare clic su **selezionare** modifiche hello toosave.
   * **Credenziali**: configurare le credenziali di hello per sia hello cluster sia utente hello SSH.
   * **Origine dati**: creare un nuovo account di archiviazione o usare un account di archiviazione esistente come account di archiviazione predefinito per il cluster HDInsight hello hello. percorso Hello devono essere hello uguali a quelli hello due reti virtuali.  Hello è anche hello percorso del cluster HDInsight hello.
   * **Prezzi**: selezionare hello numero di nodi di lavoro del cluster.
   * **Configurazioni avanzate**: 
     
     * **Aggiunta al dominio e rete virtuale/subnet**: 
       
       * **Impostazioni dominio**: 
         
         * **Nome dominio**: contoso.onmicrosoft.com
         * **Domain user name** (Nome utente dominio): immettere il nome dell'utente del dominio. Questo dominio deve avere hello seguenti privilegi: dominio toohello macchine e inserire tali elementi nell'unità organizzativa hello configurati in precedenza; Creare entità di servizio all'interno di unità di organizzazione hello configurati in precedenza; Creare voci DNS inverse. L'utente di dominio diventeranno messaggio per l'amministratore di dominio del cluster HDInsight.
         * **Password del dominio**: immettere una password utente di dominio hello.
         * **Unità organizzativa**: immettere il nome distinto di hello di hello OU configurata in precedenza. Ad esempio: OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com
         * **URL LDAPS**: ldaps://contoso.onmicrosoft.com:636
         * **Gruppo di accesso utente**: specificare il gruppo di sicurezza hello cui gli utenti che si desidera toosync toohello cluster. Ad esempio, HiveUsers.
           
           Fare clic su **selezionare** modifiche hello toosave.
           
           ![Configurazione dell'impostazione del dominio nel portale HDInsight aggiunto al dominio](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-portal-domain-setting.png)
       * **Rete virtuale**: contosohdivnet
       * **Subnet**: Subnet1
         
         Fare clic su **selezionare** modifiche hello toosave.        
         Fare clic su **selezionare** modifiche hello toosave.
   * **Gruppo di risorse**: gruppo di risorse selezionare hello utilizzato per hello HDInsight VNet (contosohdirg).
4. Fare clic su **Crea**.  

Un'altra opzione per la creazione di cluster HDInsight appartenenti a un dominio è il modello di gestione delle risorse Azure toouse. Hello seguente procedura illustra come:

**toocreate un cluster HDInsight dominio utilizzando un modello di gestione delle risorse**

1. Fare clic su hello seguente immagine tooopen un modello di gestione risorse di hello portale di Azure. il modello di gestione risorse di Hello si trova in un contenitore di blob pubblici. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-domain-joined-hdinsight-cluster.json" target="_blank"><img src="./media/hdinsight-domain-joined-configure-use-powershell/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Da hello **parametri** pannello immettere hello seguenti valori:
   
   * **Sottoscrizione**: (selezionare una sottoscrizione di Azure).
   * **Gruppo di risorse**: fare clic su **utilizzare esistente**e specificare hello stesso gruppo di risorse è stato utilizzato.  Ad esempio, contosohdirg. 
   * **Posizione**: specificare la posizione del gruppo di risorse.
   * **Nome del cluster**: immettere un nome per i cluster Hadoop hello che verrà creato. Ad esempio, contosohdicluster.
   * **Tipo di cluster**: selezionare un tipo di cluster.  valore predefinito di Hello è **hadoop**.
   * **Percorso**: selezionare un percorso per il cluster hello.  account di archiviazione predefinito Hello utilizza hello nello stesso percorso.
   * **Numero di nodi di lavoro del cluster**: selezionare hello numero di nodi di lavoro.
   * **Nome account di accesso e la password del cluster**: nome di account di accesso predefinito hello **admin**.
   * **Nome utente SSH e password**: nome utente predefinito hello **sshuser**.  È possibile rinominarlo. 
   * **ID rete virtuale**: /subscriptions/&lt;SubscriptionID&gt;/resourceGroups/&lt;ResourceGroupName&gt;/providers/Microsoft.Network/virtualNetworks/&lt;VNetName&gt;
   * **Subnet rete virtuale**: /subscriptions/&lt;SubscriptionID&gt;/resourceGroups/&lt;ResourceGroupName&gt;/providers/Microsoft.Network/virtualNetworks/&lt;VNetName&gt;/subnets/Subnet1
   * **Nome dominio**: contoso.onmicrosoft.com
   * **Organization Unit DN** (DN unità organizzativa): OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com
   * **Cluster Users Group D Ns** (DN gruppo di utenti cluster): "\"CN=HiveUsers,OU=AADDC Users,DC=<DomainName>,DC=onmicrosoft,DC=com\""
   * **URL LDAP**: ["ldaps://contoso.onmicrosoft.com:636"]
   * **DomainAdminUserName**: (nome utente amministratore di dominio hello invio)
   * **DomainAdminPassword**: (invio password utente amministratore di dominio hello)
   * **Accetto le condizioni indicate in precedenza toohello**: (controllo)
   * **PIN toodashboard**: (controllo)
3. Fare clic su **Acquista**. Verrà visualizzato un nuovo riquadro con nome **Distribuzione dell'entità Distribuzione modello in corso**. Dovrà trascorrere circa toocreate circa 20 minuti di un cluster. Una volta creato il cluster hello, è possibile fare clic su Pannello cluster hello in tooopen portale hello è.

Dopo aver completato l'esercitazione hello, è consigliabile cluster hello toodelete. Con HDInsight, i dati vengono archiviati in Archiviazione di Azure ed è possibile eliminare tranquillamente un cluster quando non viene usato. Vengono addebitati i costi anche per i cluster HDInsight che non sono in uso. Poiché gli addebiti di hello per cluster hello sono spesso più addebiti hello per l'archiviazione, è opportuno economica toodelete cluster quando non sono in uso. Per istruzioni hello di eliminazione di un cluster, vedere [hello di cluster di gestire Hadoop in HDInsight mediante il portale di Azure](hdinsight-administer-use-management-portal.md#delete-clusters).

## <a name="next-steps"></a>Passaggi successivi

* Per configurare i criteri ed eseguire query Hive, vedere [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md) (Configurare criteri Hive per cluster HDInsight aggiunti al dominio).
* Per l'uso di SSH tooconnect unita tooDomain i cluster HDInsight, vedere [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).

