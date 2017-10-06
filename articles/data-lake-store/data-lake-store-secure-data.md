---
title: dati aaaSecuring archiviati nell'archivio Azure Data Lake | Documenti Microsoft
description: Informazioni su come elenchi di controllo toosecure dati nell'archivio Azure Data Lake utilizza i gruppi e accesso
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ca35e65f-3986-4f1b-bf93-9af6066bb716
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 2b4ed7e322e1843ca47d6968ec8801ac19ea6399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="securing-data-stored-in-azure-data-lake-store"></a>Protezione dei dati presenti in Archivio Data Lake di Azure
La protezione dei dati presenti in Archivio Data Lake di Azure prevede un approccio suddiviso in tre fasi.

1. Creazione di gruppi di sicurezza in Azure Active Directory, Questi gruppi di sicurezza vengono utilizzati tooimplement controllo di accesso basato sui ruoli (RBAC) nel portale di Azure. Per altre informazioni, vedere [Controllo degli accessi in base al ruolo in Microsoft Azure](../active-directory/role-based-access-control-configure.md).
2. Assegnare account archivio Azure Data Lake di hello AAD sicurezza gruppi toohello. Controlla l'account di accesso toohello archivio Data Lake dalle operazioni di gestione e portale hello dal portale di hello o le API.
3. Assegnare gruppi di sicurezza AAD hello come elenchi di controllo di accesso (ACL) nel file system di hello archivio Data Lake.
4. È inoltre possibile impostare un intervallo di indirizzi IP per i client che è possono accedere ai dati hello in archivio Data Lake.

In questo articolo vengono fornite istruzioni su come toouse hello hello tooperform portale Azure sopra l'attività. Per informazioni dettagliate su come archivio Data Lake implementa la protezione a livello di account e dati hello, vedere [protezione nell'archivio Azure Data Lake](data-lake-store-security-overview.md). Per informazioni di approfondimento su come vengono implementati gli elenchi di controllo di accesso in Azure Data Lake Store, vedere la panoramica sul [controllo di accesso in Data Lake Store](data-lake-store-access-control.md).

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione, è necessario disporre delle seguenti hello:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Un account Azure Data Lake Store**. Per istruzioni su come toocreate uno, vedere [introduzione archivio Azure Data Lake](data-lake-store-get-started-portal.md)

## <a name="create-security-groups-in-azure-active-directory"></a>Creare gruppi di sicurezza in Azure Active Directory
Per istruzioni su come gruppi di sicurezza AAD toocreate e come gruppo toohello di tooadd utenti, vedere [la gestione dei gruppi di sicurezza in Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).

> [!NOTE] 
> È possibile aggiungere utenti e altri gruppi tooa gruppo di Azure AD usando hello portale di Azure. Tuttavia, in ordine tooadd un gruppo di tooa dell'entità servizio, utilizzare [modulo PowerShell di Azure AD](../active-directory/active-directory-accessmanagement-groups-settings-v2-cmdlets.md).
> 
> ```powershell
> # Get hello desired group and service principal and identify hello correct object IDs
> Get-AzureADGroup -SearchString "<group name>"
> Get-AzureADServicePrincipal -SearchString "<SPI name>"
> 
> # Add hello service principal toohello group
> Add-AzureADGroupMember -ObjectId <Group object ID> -RefObjectId <SPI object ID>
> ```
 
## <a name="assign-users-or-security-groups-tooazure-data-lake-store-accounts"></a>Assegnare gli utenti o gruppi di protezione account archivio Data Lake tooAzure
Quando è possibile assegnare gli utenti o gruppi di protezione account archivio Data Lake tooAzure, controllare le operazioni di gestione di accesso toohello account hello utilizzando hello portale di Azure e le API di gestione risorse di Azure. 

1. Aprire un account di Archivio Data Lake di Azure. Nel riquadro di sinistra hello, fare clic su **Sfoglia**, fare clic su **archivio Data Lake**, dal Pannello di archivio Data Lake hello, quindi fare clic su hello account nome toowhich desiderato tooassign un utente o gruppo di protezione.

2. Nel pannello delle impostazioni dell'account Data Lake Store fare clic su **Controllo di accesso (IAM)**. Pannello Hello dagli elenchi predefiniti **gli amministratori delle sottoscrizioni** gruppo come proprietario.
   
    ![Assegnare account archivio Data Lake tooAzure gruppo di protezione](./media/data-lake-store-secure-data/adl.select.user.icon.png "assegnare account archivio Data Lake tooAzure gruppo di protezione")

    Esistono due modi tooadd un gruppo e assegnare i ruoli pertinente.
   
    * Aggiungere un account di utente/gruppo toohello e quindi assegnare un ruolo, o
    * Aggiungere un ruolo e quindi assegnare utenti o gruppi toorole.
     
    In questa sezione verranno esaminate primo approccio hello, aggiunta di un gruppo e l'assegnazione di ruoli. È possibile eseguire simile passaggi toofirst selezionare un ruolo e quindi assegnare il ruolo di toothat gruppi.
4. In hello **utenti** pannello, fare clic su **Aggiungi** tooopen hello **aggiungere accesso** blade. In hello **aggiungere accesso** pannello, fare clic su **selezionare un ruolo**, quindi selezionare un ruolo per il gruppo/utente hello.
   
    ![Aggiungere un ruolo utente hello](./media/data-lake-store-secure-data/adl.add.user.1.png "aggiungere un ruolo utente hello")
   
    Hello **proprietario** e **collaboratore** ruolo fornisce l'accesso tooa numerose funzioni di amministrazione in account hello data lake. Per gli utenti che interagiscono con i dati nel servizio di data lake hello, è possibile aggiungerli toohello * * lettore * * ruolo. ambito di Hello di questi ruoli è limitato toohello Gestione operazioni correlate toohello account archivio Azure Data Lake.
   
    Per i dati delle autorizzazioni di sistema i singoli file operazioni definiscono operazioni eseguibili dagli utenti hello. Pertanto, un utente con un ruolo di lettore possono solo visualizzare le impostazioni amministrative associate account hello ma può potenzialmente lettura e scrittura dei dati in base alle autorizzazioni del file system assegnate toothem. Le autorizzazioni del file di archivio Data Lake sono descritte nel [l'assegnazione gruppo di sicurezza come toohello ACL di sistema di file di archivio Azure Data Lake](#filepermissions).
5. In hello **aggiungere accesso** pannello, fare clic su **aggiungere utenti** tooopen hello **aggiungere utenti** blade. In questo pannello, cercare il gruppo di sicurezza hello creata precedentemente in Azure Active Directory. Se si dispone di molti gruppi toosearch da, è possibile utilizzare la casella di testo hello nella hello toofilter superiore sul nome di gruppo hello. Fare clic su **Seleziona**.
   
    ![Aggiungere un gruppo di sicurezza](./media/data-lake-store-secure-data/adl.add.user.2.png "Aggiungere un gruppo di sicurezza")
   
    Se si desidera tooadd gruppo/utente che non è elencato, è possibile invitarli utilizzando hello **invitare** icona e specificando l'indirizzo di posta elettronica hello hello utente/gruppo.
6. Fare clic su **OK**. Verrà visualizzato il gruppo di sicurezza hello aggiunto come illustrato di seguito.
   
    ![Gruppo di sicurezza aggiunto](./media/data-lake-store-secure-data/adl.add.user.3.png "Gruppo di sicurezza aggiunto")

7. Il gruppo di sicurezza/utente dispone ora di account di accesso toohello archivio Azure Data Lake. Si desidera tooprovide accesso toospecific utenti, è possibile aggiungere il gruppo di sicurezza toohello. Analogamente, se si desidera accedere toorevoke per un utente, è possibile rimuoverli dal gruppo di sicurezza hello. È inoltre possibile assegnare più gruppi di sicurezza tooan account. 

## <a name="filepermissions"></a>Assegnare gli utenti o gruppo di sicurezza come toohello ACL di sistema di file di archivio Azure Data Lake
Tramite l'assegnazione di gruppi di sicurezza dell'utente o sistema di file di Azure Data Lake toohello, impostare il controllo di accesso ai dati hello archiviati nell'archivio Azure Data Lake.

1. Nel pannello dell'account di Archivio Data Lake, fare clic su **Esplora dati**.
   
    ![Creare directory nell'account Data Lake Store](./media/data-lake-store-secure-data/adl.start.data.explorer.png "Creare directory nell'account Data Lake Store")
2. In hello **Esplora dati** pannello, fare clic su hello file o una cartella per cui si desidera tooconfigure hello ACL e quindi fare clic su **accesso**. file di tooa tooassign ACL, è necessario fare clic su **accesso** da hello **anteprima File** blade.
   
    ![Configurare elenchi di controllo di accesso nel file system di Data Lake](./media/data-lake-store-secure-data/adl.acl.1.png "Configurare elenchi di controllo di accesso nel file system di Data Lake")
3. Hello **accesso** pannello elenca accesso standard di hello e toohello radice già assegnato l'accesso personalizzato. Fare clic su hello **Aggiungi** personalizzata a livello di icona tooadd ACL.
   
    ![Elencare gli accessi standard e personalizzati](./media/data-lake-store-secure-data/adl.acl.2.png "Elencare gli accessi standard e personalizzati")
   
   * **Accesso standard** è hello UNIX l'accesso di tipo, consente di leggere, scrivere, eseguire le classi utente distinte di toothree (rwx): proprietario, gruppo e altri.
   * **Accesso personalizzato** corrisponde toohello POSIX ACL che consente le autorizzazioni tooset per specifici utenti o gruppi e non solo hello proprietario del file o gruppo. 
     
     Per altre informazioni, vedere l'articolo sugli [elenchi di controllo di accesso HDFS](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists). Per altre informazioni sull'implementazione degli elenchi di controllo di accesso in Data Lake Store, vedere [Controllo di accesso in Data Lake Store](data-lake-store-access-control.md).
4. Fare clic su hello **Aggiungi** hello tooopen icona **aggiungere accesso personalizzato** blade. In questo pannello, fare clic su **Seleziona utente o gruppo**, quindi nel **Seleziona utente o gruppo** pannello, cercare il gruppo di sicurezza hello creata precedentemente in Azure Active Directory. Se si dispone di molti gruppi toosearch da, è possibile utilizzare la casella di testo hello nella hello toofilter superiore sul nome di gruppo hello. Fare clic su gruppo hello tooadd desiderato e quindi fare clic su **selezionare**.
   
    ![Aggiungere un gruppo](./media/data-lake-store-secure-data/adl.acl.3.png "Aggiungere un gruppo")
5. Fare clic su **selezionare autorizzazioni**, selezionare le autorizzazioni di hello e se si desidera che le autorizzazioni di hello tooassign come un ACL predefinito, accedere ACL o entrambi. Fare clic su **OK**.
   
    ![Assegnare autorizzazioni toogroup](./media/data-lake-store-secure-data/adl.acl.4.png "assegnare autorizzazioni toogroup")
   
    Per altre informazioni sulle autorizzazioni in Data Lake Store e gli ACL predefiniti/di accesso, vedere [Controllo di accesso in Data Lake Store](data-lake-store-access-control.md).
6. In hello **aggiungere accesso personalizzato** pannello, fare clic su **OK**. Hello appena aggiunti, gruppo, con le autorizzazioni di hello associata, verrà ora elencato nella hello **accesso** blade.
   
    ![Assegnare autorizzazioni toogroup](./media/data-lake-store-secure-data/adl.acl.5.png "assegnare autorizzazioni toogroup")
   
   > [!IMPORTANT]
   > Nella versione corrente di hello, è possibile avere solo 9 voci in **accesso personalizzato**. Se si desidera tooadd più di 9, è consigliabile creare gruppi di sicurezza, aggiungere gruppi di utenti toosecurity, fornire l'accesso toothose gruppi di sicurezza per hello account archivio Data Lake.
   > 
   > 
7. Se necessario, è anche possibile modificare le autorizzazioni di accesso hello dopo aver aggiunto il gruppo di hello. Casella di controllo hello deselezionare o selezionare per ogni autorizzazione digitare (lettura, scrittura, esecuzione) in base che si voglia tooremove o assegnare a tale gruppo di sicurezza toohello di autorizzazione. Fare clic su **salvare** modifiche hello toosave, o **annullare** modifiche hello tooundo.

## <a name="set-ip-address-range-for-data-access"></a>Impostare l'intervallo di indirizzi IP per l'accesso ai dati
Archivio Azure Data Lake consente toofurther bloccare archivio dati tooyour di accesso a livello di rete. È possibile abilitare il firewall, specificare un indirizzo IP e definire un intervallo di indirizzi IP per i client attendibili. Una volta abilitato, solo i client che dispongono degli indirizzi IP hello all'interno di intervallo definita possono connettersi toohello store.

![Impostazioni del firewall e accesso IP](./media/data-lake-store-secure-data/firewall-ip-access.png "Impostazioni del firewall e indirizzo IP")

## <a name="remove-security-groups-for-an-azure-data-lake-store-account"></a>Rimuovere gruppi di sicurezza da un account di Archivio Data Lake di Azure
Quando si rimuovono i gruppi di sicurezza dall'account archivio Azure Data Lake, si modifica solo operazioni di gestione accesso toohello account hello utilizzando hello portale di Azure e le API di gestione risorse di Azure.

1. Nel pannello dell'account di Data Lake Store fare clic su **Impostazioni**. Da hello **impostazioni** pannello, fare clic su **utenti**.
   
    ![Assegnare account Data Lake tooAzure gruppo di protezione](./media/data-lake-store-secure-data/adl.select.user.icon.png "assegnare account Data Lake tooAzure gruppo di protezione")
2. In hello **utenti** pannello selezionare il gruppo di protezione hello desiderato tooremove.
   
    ![Sicurezza gruppo tooremove](./media/data-lake-store-secure-data/adl.add.user.3.png "tooremove gruppo di sicurezza")
3. Nel Pannello di hello hello gruppo di sicurezza, fare clic su **rimuovere**.
   
    ![Gruppo di sicurezza rimosso](./media/data-lake-store-secure-data/adl.remove.group.png "Gruppo di sicurezza rimosso")

## <a name="remove-security-group-acls-from-azure-data-lake-store-file-system"></a>Rimuovere elenchi di controllo di accesso di gruppi di sicurezza dal file system di Archivio Data Lake di Azure
Quando si rimuovono i gruppi di sicurezza ACL dal file system di archivio Azure Data Lake, si modificano i dati di toohello di accesso in hello archivio Data Lake.

1. Nel pannello dell'account di Archivio Data Lake, fare clic su **Esplora dati**.
   
    ![Creare directory nell'account Data Lake](./media/data-lake-store-secure-data/adl.start.data.explorer.png "Creare directory nell'account Data Lake")
2. In hello **Esplora dati** pannello, fare clic su file hello o una cartella per cui si desidera tooremove hello ACL e quindi nel pannello account, fare clic su hello **accesso** icona. tooremove ACL per un file, è necessario fare clic su **accesso** da hello **anteprima File** blade.
   
    ![Configurare elenchi di controllo di accesso nel file system di Data Lake](./media/data-lake-store-secure-data/adl.acl.1.png "Configurare elenchi di controllo di accesso nel file system di Data Lake")
3. In hello **accesso** pannello da hello **accesso personalizzato** fare clic sul gruppo di sicurezza hello desiderato tooremove. In hello **accesso personalizzato** pannello, fare clic su **rimuovere** e quindi fare clic su **OK**.
   
    ![Assegnare autorizzazioni toogroup](./media/data-lake-store-secure-data/adl.remove.acl.png "assegnare autorizzazioni toogroup")

## <a name="see-also"></a>Vedere anche
* [Panoramica di Archivio Data Lake di Azure](data-lake-store-overview.md)
* [Copiare i dati da un archivio Azure archiviazione BLOB tooData Lake](data-lake-store-copy-data-azure-storage-blob.md)
* [Usare Azure Data Lake Analytics con Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usare Azure HDInsight con Archivio Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Introduzione ad Archivio Data Lake mediante PowerShell](data-lake-store-get-started-powershell.md)
* [Introduzione ad Archivio Data Lake mediante .NET SDK](data-lake-store-get-started-net-sdk.md)
* [Accesso ai log di diagnostica per Azure Data Lake Store](data-lake-store-diagnostic-logs.md)

