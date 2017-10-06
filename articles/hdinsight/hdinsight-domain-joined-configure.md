---
title: cluster HDInsight dominio aaaConfigure - Azure | Documenti Microsoft
description: Informazioni su come tooset e configurare il cluster HDInsight appartenenti a un dominio
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 0cbb49cc-0de1-4a1a-b658-99897caf827c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/02/2016
ms.author: saurinsh
ms.openlocfilehash: 8c4b3d269a7662d27a49b839e5cd05a3e24f7023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-domain-joined-hdinsight-clusters-preview"></a>Configurare i cluster HDInsight aggiunti al dominio (anteprima)

Informazioni su come tooset backup un Azure HDInsight cluster con Azure Active Directory (Azure AD) e [cane Apache](http://hortonworks.com/apache/ranger/) tootake sfruttare l'autenticazione avanzata e i criteri di controllo degli accessi di un accesso basato sui ruoli.  HDInsight aggiunto al dominio può essere configurato solo nei cluster basati su Linux. Per altre informazioni, consultare [Introduce Domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md) (Introduzione ai cluster HDInsight aggiunti al dominio).

> [!IMPORTANT]
> Oozie non è abilitato su HDInsight appartenente al dominio.

In questo articolo viene prima esercitazione di hello di una serie:

* Creare un tooAzure di cluster connessi AD HDInsight (tramite funzionalità di servizi di dominio di Azure Directory hello) con Apache cane abilitato.
* Creare e applicare i criteri tramite cane Apache Hive e consentire agli utenti (ad esempio, gli esperti di dati) tooHive tooconnect utilizzando gli strumenti basati su ODBC, ad esempio Excel, e così via Tableau. Microsoft sta lavorando non appena l'aggiunta di altri carichi di lavoro, ad esempio HBase Spark e Storm, unita tooDomain HDInsight.

Un esempio di topologia finale hello è simile al seguente:

![Topologia di HDInsight aggiunto al dominio](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-topology.png)

Dal momento che attualmente Azure AD supporta solo le reti virtuali classiche mentre i cluster HDInsight basati su Linux supportano solo reti virtuali basate su Azure Resource Manager, l'integrazione di Azure AD HDInsight richiede due reti virtuali e il peering tra di loro. Per informazioni sul confronto hello tra modelli di distribuzione hello due, vedere [Azure Resource Manager e distribuzione classica: comprendere i modelli di distribuzione e lo stato delle risorse di hello](../azure-resource-manager/resource-manager-deployment-model.md). devono essere di due reti virtuali in hello Hello stessa area hello Azure Active Directory.

I nomi dei servizi di Azure devono essere globalmente univoci. Hello seguente i nomi viene utilizzato in questa esercitazione. Contoso è un nome fittizio. È necessario sostituire *contoso* con un nome diverso quando si passa all'esercitazione hello. 

**Nomi:**

| Proprietà | Valore |
| --- | --- |
| Rete virtuale di Azure AD |contosoaadvnet |
| Gruppo di risorse della rete virtuale di Azure AD |contosoaadrg |
| Directory di Azure AD |contosoaaddirectory |
| Nome di dominio di Azure AD |contoso (contoso.onmicrosoft.com) |
| Rete virtuale di HDInsight |contosohdivnet |
| Gruppo di risorse della rete virtuale di HDInsight |contosohdirg |
| Cluster HDInsight |contosohdicluster |

In questa esercitazione viene descritta la procedura hello per la configurazione di un cluster di HDInsight appartenenti a un dominio. Ogni sezione contiene articoli tooother collegamenti con informazioni di base.

## <a name="prerequisite"></a>Prerequisiti:
* Acquisire familiarità con [Azure AD Domain Services](https://azure.microsoft.com/services/active-directory-ds/) e con la struttura dei [prezzi](https://azure.microsoft.com/pricing/details/active-directory-ds/).
* Assicurarsi che la sottoscrizione sia consentita per questa anteprima pubblica. È possibile farlo mediante l'invio di un messaggio di posta elettronica toohdipreview@microsoft.com con l'ID sottoscrizione.
* Un certificato SSL firmato da un'autorità di firma per il dominio. Hello richieste tramite la configurazione di accesso LDAP sicuro. Non è possibile usare certificati autofirmati.

## <a name="procedures"></a>Procedures
1. Creare una rete virtuale classica di Azure per Azure AD.  
2. Creare e configurare Azure AD e Azure AD DS.
3. Creare un HDInsight VNet in modalità di gestione risorse di Azure hello.
4. Peer hello due reti virtuali.
5. Creare un cluster HDInsight

> [!NOTE]
> In questa esercitazione si presuppone che non sia disponibile un account Azure. Se si dispone di uno, è possibile ignorare la parte hello nel passaggio 2.
> 
> 

È disponibile uno script di PowerShell che automatizza i passaggi da 3 a 7.  Per altre informazioni, vedere l'articolo su come [configurare i cluster HDInsight aggiunti al dominio con Azure PowerShell](hdinsight-domain-joined-configure-use-powershell.md).

## <a name="create-an-azure-virtual-network-classic"></a>Creare una rete virtuale di Azure (versione classica)
In questa sezione è creare una rete virtuale (classica) utilizzando hello portale di Azure. Nella sezione successiva hello, si abilita hello Azure Active Directory per Azure Active Directory nella rete virtuale hello. Per ulteriori informazioni su hello procedura e l'utilizzo di altri metodi di creazione della rete virtuale, vedere [creare una rete virtuale (classico) tramite il portale di Azure hello](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).

**una rete virtuale classica toocreate**

1. Accesso toohello [portale di Azure](https://portal.azure.com). 
2. Fare clic su **Nuovo** > **Rete** > **Rete virtuale**.
3. In **Selezionare un modello di distribuzione** scegliere **Classico**, quindi fare clic su **Crea**.
4. Immettere o selezionare hello seguenti valori:
   
   * **Nome**: contosoaadvnet
   * **Spazio indirizzi**: 10.1.0.0/16
   * **Nome subnet**: Subnet1
   * **Intervallo di indirizzi subnet**: 10.1.0.0/24
   * **Sottoscrizione**: (selezionare una sottoscrizione usata per creare la rete virtuale.)
   * **Gruppo di risorse**: contosoaadrg
   * **Posizione**: (selezionare un'area per il cluster HDInsight.)
     
     > [!IMPORTANT]
     > È necessario scegliere una posizione che supporti Azure AD DS. Per altre informazioni, vedere [Prodotti disponibili in base all'area](https://azure.microsoft.com/en-us/regions/services/). 
     > 
     > Entrambi hello classic rete virtuale e hello rete virtuale di gruppo di risorse deve essere in hello stessa area hello Azure Active Directory.
     > 
     > 
5. Fare clic su **crea** toocreate hello rete virtuale.

## <a name="create-and-configure-azure-ad-ds-for-your-azure-ad"></a>Creare e configurare Azure AD DS per Azure AD
In questa sezione si svolgeranno le seguenti operazioni:

1. Creare Azure AD.
2. Creare utenti di Azure AD. Questi utenti sono gli utenti del dominio. Primo utente hello utilizzato per configurare il cluster di HDInsight hello con hello Azure AD.  Hello altri due utenti sono facoltativi per questa esercitazione. Verranno usati in [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md) (Configurare criteri Hive per cluster HDInsight aggiunti al dominio) quando si creano criteri Apache Ranger.
3. Creare il gruppo di amministratori di controller di dominio di AAD hello e aggiungere hello Azure AD utente toohello gruppo. Utilizzare l'unità organizzativa utente toocreate hello.
4. Abilitare i servizi di dominio Azure Active Directory (Azure AD DS) per hello Azure AD.
5. Configurare LDAPS per hello Azure AD. Hello Lightweight Directory Access Protocol (LDAP) è tooread utilizzati da e scrittura tooAzure Active Directory.

Se si preferisce toouse un esistente AD Azure, è possibile ignorare i passaggi 1 e 2.

**toocreate un Azure AD**

1. Da hello [portale di Azure classico](https://manage.windowsazure.com), fare clic su **New** > **servizi App** > **Active Directory**  >  **Directory** > **creazione personalizzata**. 
2. Immettere o selezionare hello seguenti valori:
   
   * **Nome**: contosoaaddirectory
   * **Nome di dominio**: contoso.  Il nome deve essere univoco a livello globale.
   * **Paese o area geografica**: selezionare il paese o l'area.
3. Fare clic su **Complete**.

**Creare un utente di Azure AD**

1. Da hello [portale di Azure classico](https://manage.windowsazure.com), fare clic su **Active Directory** -> **contosoaaddirectory**. 
2. Fare clic su **utenti** menu principale di hello.
3. Fare clic su **Aggiungi utente**.
4. Immettere il **nome utente**, quindi fare clic su **Avanti**. 
5. Configurare il profilo utente. In **Ruolo** selezionare **Amministratore globale**, quindi **Avanti**.  il ruolo di amministratore globale di Hello è necessario toocreate le unità organizzative.
6. Fare clic su **crea** tooget una password temporanea.
7. Creare una copia della password hello e quindi fare clic su **completa**. Più avanti in questa esercitazione si utilizzerà questo cluster HDInsight di hello toocreate di utente di amministratore globale.

Seguire hello stessa procedura toocreate due più utenti con hello **utente** ruolo hiveuser1 e hiveuser2. Hello utenti seguenti verranno utilizzati [Hive configurare criteri per i cluster HDInsight dominio](hdinsight-domain-joined-run-hive.md).

**toocreate hello gruppo degli amministratori di controller di dominio Azure ad e aggiungere un utente di Azure AD**

1. Da hello [portale di Azure classico](https://manage.windowsazure.com), fare clic su **Active Directory** > **contosoaaddirectory**. 
2. Fare clic su **gruppi** menu principale di hello.
3. Fare clic su **Aggiungi un gruppo** o **Aggiungi gruppo**.
4. Immettere o selezionare hello seguenti valori:
   
   * **Nome**: AAD DC Administrators.  Non modificare il nome di gruppo hello.
   * **Tipo di gruppo**: sicurezza.
5. Fare clic su **Complete**.
6. Fare clic su **gli amministratori di controller di dominio di AAD** gruppo hello tooopen.
7. Fare clic su **Aggiungi membri**.
8. Selezionare l'utente prima di hello creato nel passaggio precedente hello e quindi fare clic su **completa**.
9. Ripetizione hello chiamato un altro gruppo stesso passaggi toocreate **HiveUsers**, e aggiungere due hello Hive utenti toohello gruppo.

Per ulteriori informazioni, vedere [servizi di dominio Active Directory di Azure (anteprima) - creare hello 'Administrators di controller di dominio di AAD' gruppo](../active-directory-domain-services/active-directory-ds-getting-started.md).

**tooenable Azure Active Directory per Azure AD**

1. Da hello [portale di Azure classico](https://manage.windowsazure.com), fare clic su **Active Directory** > **contosoaaddirectory**. 
2. Fare clic su **configura** menu principale di hello.
3. Scorrere verso il basso troppo**servizi di dominio**, e set hello seguenti valori:
   
   * **Abilita Servizi di dominio per la directory**: Sì.
   * **Nome di dominio DNS di servizi di dominio**: Mostra nome DNS predefinito di hello di hello directory Azure. Ad esempio, contoso.onmicrosoft.com.
   * **Connettere la rete virtuale toothis servizi di dominio**: selezionare hello classic rete virtuale creata in precedenza, ad esempio **contosoaadvnet**.
4. Fare clic su **salvare** dal basso hello della pagina hello. Si noterà **in sospeso...**  Avanti troppo**Abilita servizi di dominio per questa directory**.  
5. Attendere che non sia più visualizzato **In sospeso...** e che compaiano dati nel campo **Indirizzo IP**. Verranno inseriti due indirizzi IP. Questi sono gli indirizzi IP hello hello dei controller di dominio eseguito il provisioning dei servizi di dominio. Ogni indirizzo IP sarà visibile dopo che il controller di dominio corrispondente di hello è disponibile e pronta. Annotare gli indirizzi IP due hello. saranno necessarie più avanti.

Per altre informazioni vedere [Azure AD Domain Services (anteprima) - Abilitare Azure AD Domain Services](../active-directory-domain-services/active-directory-ds-getting-started-enableaadds.md).

**password toosynchronize**

Se si utilizza il proprio dominio, è necessario password hello toosynchronize. Vedere [Abilita servizi di dominio Active Directory tooAzure sincronizzazione password per un solo cloud di Azure directory AD](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md).

**tooconfigure LDAPS per hello Azure AD**

1. Ottenere un certificato SSL firmato da un'autorità di firma per il dominio. Se si desidera toouse un certificato autofirmato, raggiungere toohdipreview@microsoft.com per un'eccezione.
2. Da hello [portale di Azure classico](https://manage.windowsazure.com), fare clic su **Active Directory** > **contosoaaddirectory**. 
3. Fare clic su **configura** menu principale di hello.
4. Scorrere troppo**servizi di dominio**.
5. Fare clic su **Configura certificato**.
6. Seguire i file di certificato di hello istruzioni toospecify hello e una password hello. Si noterà **in sospeso...**  Avanti troppo**Abilita servizi di dominio per questa directory**.  
7. Attendere che non sia più visualizzato **In sospeso...** e che compaiano dati nel campo **Certificato LDAP sicuro**.  Questa operazione può richiedere 10 minuti o più.

> [!NOTE]
> Se alcune attività in background vengono eseguiti su hello Azure Active Directory, potrebbe essere visualizzato un errore durante il caricamento del certificato - <i>è un'operazione viene eseguita per questo tenant. Please try again later</i> (È in corso un'operazione per questo tenant. Riprovare più tardi).  Nel caso in cui si verificasse questo errore, riprovare più tardi. Hello che secondo IP di controller di dominio può richiedere fino a too3 ore toobe il provisioning.
> 
> 

Per altre informazioni, vedere [Configurare l'accesso LDAP sicuro (LDAPS) per un dominio gestito di Azure AD Domain Services](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md).

## <a name="create-a-resource-manager-vnet-for-hdinsight-cluster"></a>Creare una rete virtuale di Resource Manager per un cluster HDInsight
In questa sezione si creerà un VNet Gestione risorse di Azure che verrà utilizzato per il cluster HDInsight hello. Per altre informazioni sulla creazione di una rete virtuale di Azure usando altri metodi, vedere [Creare una rete virtuale](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)

Dopo la creazione di reti virtuali hello, sarà necessario configurare Gestione risorse VNet toouse hello stessi DNS server per la rete virtuale di Azure AD hello hello. Se è stata seguita la procedura hello in questa esercitazione toocreate hello classico rete virtuale e hello Azure AD, i server DNS hello sono 10.1.0.4 e 10.1.0.5.

**toocreate VNet un gestore delle risorse**

1. Accesso toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **Nuovo**, quindi su **Rete** e infine su **Rete virtuale**. 
3. In **Selezionare un modello di distribuzione** scegliere **Resource Manager** e quindi fare clic su **Crea**.
4. Digitare o selezionare hello seguenti valori:
   
   * **Nome**: contosohdivnet
   * **Spazio indirizzi**: 10.2.0.0/16. Verificare che l'intervallo di indirizzo hello non può sovrapporsi all'intervallo di indirizzi IP hello di hello classic rete virtuale.
   * **Nome subnet**: Subnet1
   * **Intervallo di indirizzi subnet**: 10.2.0.0/24
   * **Sottoscrizione**: (selezionare una sottoscrizione di Azure.)
   * **Gruppo di risorse**: contosohdirg
   * **Percorso**: (selezionare hello nello stesso percorso di rete virtuale di Azure AD, ad esempio contosoaadvnet hello.)
5. Fare clic su **Crea**.

**tooconfigure DNS per hello VNet Gestione risorse**

1. Da hello [portale di Azure](https://portal.azure.com), fare clic su **più servizi** -> **le reti virtuali**. Assicurarsi di non tooclick **le reti virtuali (classico)**.
2. Fare clic su **contosohdivnet**.
3. Fare clic su **server DNS** dal lato sinistro di nuovo pannello hello hello.
4. Fare clic su **personalizzata**, quindi immettere hello seguenti valori:
   
   * 10.1.0.4
   * 10.1.0.5
     
     Questi indirizzi IP del server DNS devono corrispondere i server DNS toohello hello rete virtuale di Azure Active Directory (VNet classico).
5. Fare clic su **Salva**.

## <a name="peer-hello-azure-ad-vnet-and-hello-hdinsight-vnet"></a>Peer hello rete virtuale di Azure AD e hello HDInsight VNet
**toopeer hello due reti virtuali**

1. Accesso toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **più servizi** dal menu a sinistra di hello.
3. Fare clic su **Reti virtuali**. Non fare clic su **Reti virtuali (classico)**.
4. Fare clic su **contosohdivnet**.  Si tratta di hello HDInsight VNet.
5. Fare clic su **peering** nel menu a sinistra del pannello hello hello.
6. Fare clic su **Aggiungi** menu principale di hello. Viene aperto hello **aggiungere peering** blade.
7. In hello **Aggiungi peering** blade, hello impostato o seleziona i valori seguenti:
   
   * **Nome**: ContosoAADHDIVNetPeering
   * **Modello di distribuzione della rete virtuale**: classica
   * **Sottoscrizione**: selezionare il nome della sottoscrizione utilizzato per la rete virtuale di hello classic (Azure AD).
   * **Rete virtuale**: contosoaadvnet.
   * **Consenti accesso alla rete virtuale**: (selezionare)
   * **Consenti traffico inoltrato**: (selezionare). Lasciare hello altre due caselle di controllo deselezionata.
8. Fare clic su **OK**.

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
     * **Versione**: HDI 3.6. HDInsight aggiunto al dominio è supportato solo nei cluster HDInsight versione 3.6.
     * **Tipo di cluster**: PREMIUM
       
       Fare clic su **selezionare** modifiche hello toosave.
   * **Credenziali**: configurare le credenziali di hello per sia hello cluster sia utente hello SSH.
   * **Origine dati**: creare un nuovo account di archiviazione o usare un account di archiviazione esistente come account di archiviazione predefinito per il cluster HDInsight hello hello. percorso Hello devono essere hello uguali a quelli hello due reti virtuali.  Hello è anche hello percorso del cluster HDInsight hello.
   * **Prezzi**: selezionare hello numero di nodi di lavoro del cluster.
   * **Configurazioni avanzate**: 
     
     * **Aggiunta al dominio e rete virtuale/subnet**: 
       
       * **Impostazioni dominio**: 
         
         * **Nome dominio**: contoso.onmicrosoft.com
         * **Domain user name** (Nome utente dominio): immettere il nome dell'utente del dominio. Questo dominio deve avere hello seguenti privilegi: dominio toohello macchine e inserire tali elementi nell'unità organizzativa hello specificate durante la creazione del cluster. Creare entità di servizio all'interno di unità di organizzazione hello specificate durante la creazione del cluster. Creare voci DNS inverse. L'utente di dominio diventeranno messaggio per l'amministratore di dominio del cluster HDInsight.
         * **Password del dominio**: immettere una password utente di dominio hello.
         * **Unità organizzativa**: immettere il nome distinto di hello di hello unità Organizzativa che si desidera toouse con cluster HDInsight. Ad esempio: OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com. Se questa unità Organizzativa non esiste, il cluster HDInsight tenterà toocreate questa unità Organizzativa. Assicurarsi che hello unità Organizzativa è già presente o account di dominio di hello disponga delle autorizzazioni toocreate uno nuovo. Se si utilizza l'account di dominio hello che fa parte di amministratori AADDC, disporrà delle autorizzazioni necessarie toocreate hello unità Organizzativa.
         * **URL LDAPS**: ldaps://contoso.onmicrosoft.com:636
         * **Gruppo di accesso utente**: specificare il gruppo di sicurezza di hello cui gli utenti si desidera toosync toohello cluster. Ad esempio, HiveUsers.
           
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
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-domain-joined-hdinsight-cluster.json" target="_blank"><img src="./media/hdinsight-domain-joined-configure/deploy-to-azure.png" alt="Deploy tooAzure"></a>
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
   * **Gruppo di utenti cluster DNs**: [\"UtentiHive\"]
   * **URL LDAP**: ["ldaps://contoso.onmicrosoft.com:636"]
   * **DomainAdminUserName**: (nome utente amministratore di dominio hello invio)
   * **DomainAdminPassword**: (invio password utente amministratore di dominio hello)
   * **Accetto le condizioni indicate in precedenza toohello**: (controllo)
   * **PIN toodashboard**: (controllo)
3. Fare clic su **Acquista**. Verrà visualizzato un nuovo riquadro con nome **Distribuzione dell'entità Distribuzione modello in corso**. Dovrà trascorrere circa toocreate circa 20 minuti di un cluster. Una volta creato il cluster hello, è possibile fare clic su Pannello cluster hello in tooopen portale hello è.

Dopo aver completato l'esercitazione hello, è consigliabile cluster hello toodelete. Con HDInsight, i dati vengono archiviati in Archiviazione di Azure ed è possibile eliminare tranquillamente un cluster quando non viene usato. Vengono addebitati i costi anche per i cluster HDInsight che non sono in uso. Poiché gli addebiti di hello per cluster hello sono spesso più addebiti hello per l'archiviazione, è opportuno economica toodelete cluster quando non sono in uso. Per istruzioni hello di eliminazione di un cluster, vedere [hello di cluster di gestire Hadoop in HDInsight mediante il portale di Azure](hdinsight-administer-use-management-portal.md#delete-clusters).

## <a name="next-steps"></a>Passaggi successivi
* Per configurare i criteri ed eseguire query Hive, vedere [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md) (Configurare criteri Hive per cluster HDInsight aggiunti al dominio).
* Per l'uso di SSH tooconnect unita tooDomain i cluster HDInsight, vedere [utilizzo di SSH con basati su Linux, Hadoop in HDInsight da OS X, Linux o Unix](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).

