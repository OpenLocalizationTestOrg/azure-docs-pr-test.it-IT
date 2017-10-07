---
title: Considerazioni sulla aaaSecurity per lo spostamento dei dati in Data Factory di Azure | Documenti Microsoft
description: Informazioni su come proteggere lo spostamento dei dati in Azure Data Factory.
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 4bfce8884df14ad5b94e28ad3dfcf7025e2130a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---security-considerations-for-data-movement"></a>Azure Data Factory: considerazioni sulla sicurezza dello spostamento dei dati
## <a name="introduction"></a>Introduzione
Questo articolo descrive l'infrastruttura di sicurezza di base che servizi di spostamento dei dati in Data Factory di Azure usare toosecure i dati. Le risorse di gestione di Azure Data Factory si basano sull'infrastruttura di sicurezza di Azure e ricorrono a tutte le misure di sicurezza offerte da Azure.

In una soluzione Data Factory si creano una o più [pipeline](data-factory-create-pipelines.md)di dati. Una pipeline è un raggruppamento logico di attività che insieme eseguono un compito. Queste pipeline si trovano nell'area di hello in hello data factory è stata creata. 

Anche se Data Factory è disponibile solo in **Stati Uniti occidentali**, **Stati Uniti orientali**, e **Europa settentrionale** aree, è disponibile il servizio di spostamento dati hello [globalmente in più aree](data-factory-data-movement-activities.md#global). Data Factory di servizio garantisce che i dati non lasciano un'area geografica o area a meno che non in modo esplicito hello servizio toouse un'area alternativa se il servizio di spostamento dati hello non ancora distribuito toothat area. 

Azure Data Factory non archivia i dati ad eccezione delle credenziali del servizio collegato per gli archivi di dati cloud, che vengono crittografate tramite l'uso di certificati. Consente di creare flussi di lavoro basati su dati tooorchestrate spostamento dei dati tra [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) e l'elaborazione dei dati mediante [servizi di calcolo](data-factory-compute-linked-services.md) in altre aree o in un locale ambiente. Consente inoltre troppo[monitorare e gestire i flussi di lavoro](data-factory-monitor-manage-pipelines.md) utilizzando sia a livello di codice e i meccanismi di interfaccia utente.

Lo spostamento dei dati con Azure Data Factory è stato **certificato** per:
-   [HIPAA/HITECH](https://www.microsoft.com/en-us/trustcenter/Compliance/HIPAA)  
-   [ISO/IEC 27001](https://www.microsoft.com/en-us/trustcenter/Compliance/ISO-IEC-27001)  
-   [ISO/IEC 27018](https://www.microsoft.com/en-us/trustcenter/Compliance/ISO-IEC-27018) 
-   [CSA STAR](https://www.microsoft.com/en-us/trustcenter/Compliance/CSA-STAR-Certification)
     
Se si è interessati in conformità di Azure e in che modo Azure protegge la propria infrastruttura, visitare la pagina hello [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/default.aspx). 

In questo articolo è esaminare le considerazioni sulla sicurezza in hello seguenti due scenari di spostamento di dati: 

- **Scenario cloud**: in questo scenario, l'origine e la destinazione sono accessibili pubblicamente tramite internet. Sono inclusi i servizi di archiviazione cloud gestiti come Archiviazione di Azure, Azure SQL Data Warehouse, Database SQL di Azure, Azure Data Lake Store, Amazon S3, Amazon Redshift, i servizi SaaS come Salesforce e i protocolli Web, ad esempio FTP e OData. L'elenco completo delle origini dati supportate è disponibile [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats).
- **Scenario ibrido**: In questo scenario, l'origine o destinazione si trova dietro un firewall o all'interno di un locale rete o hello i dati aziendali archivio è in una rete privata virtuale (in genere origine hello) di rete e non è accessibile pubblicamente . Anche i server di database ospitati nelle macchine virtuali rientrano in questo scenario.

## <a name="cloud-scenarios"></a>Scenari cloud
###<a name="securing-data-store-credentials"></a>Proteggere le credenziali dell'archivio dati
Azure Data Factory protegge le credenziali dell'archivio dati **crittografandoli** con i **certificati gestiti da Microsoft**. Questi certificati ruotano ogni **due anni** (in questo arco temporale è compreso il rinnovo del certificato e la migrazione delle credenziali). Queste credenziali crittografate vengono archiviate in modo sicuro all'interno di un'**Archiviazione di Azure gestita dai servizi di gestione di Azure Data Factory**. Per altre informazioni sulla sicurezza di Archiviazione di Azure, vedere [Panoramica sulla sicurezza di Archiviazione di Azure](../security/security-storage-overview.md).

### <a name="data-encryption-in-transit"></a>Crittografia di dati in transito
Se l'archivio dati di cloud hello supporta HTTPS o TLS, trasferimenti di tutti i dati tra servizi lo spostamento dei dati in Data Factory e un archivio dati cloud sono tramite un canale sicuro HTTPS o TLS.

> [!NOTE]
> Tutte le connessioni troppo**Database SQL di Azure** e **Azure SQL Data Warehouse** richiedono sempre la crittografia SSL/TLS (), mentre i dati sono in transito tooand dal database hello. Durante la creazione di una pipeline utilizzando un editor JSON, aggiungere hello **crittografia** proprietà e impostarla troppo**true** in hello **stringa di connessione**. Quando si utilizza hello [Copia guidata](data-factory-azure-copy-wizard.md), per impostazione predefinita, la procedura guidata hello imposta questa proprietà. Per **di archiviazione di Azure**, è possibile utilizzare **HTTPS** nella stringa di connessione hello.

### <a name="data-encryption-at-rest"></a>Crittografia di dati inattivi
Alcuni archivi di dati supportano la crittografia dei dati inattivi. È consigliabile abilitare il meccanismo di crittografia dei dati per gli archivi dati. 

#### <a name="azure-sql-data-warehouse"></a>Azure SQL Data Warehouse
Consente di Transparent Data Encryption (TDE) in Azure SQL Data Warehouse con protezione contro minacce hello di attività dannose eseguendo la crittografia in tempo reale e la decrittografia dei dati inattivi. Questo comportamento è trasparente toohello client. Per altre informazioni, vedere [Proteggere un database in SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md).

#### <a name="azure-sql-database"></a>Database SQL di Azure
Database SQL di Azure supporta anche la crittografia dati trasparente (TDE), agevola la protezione contro minacce hello di attività dannose eseguendo la crittografia in tempo reale e la decrittografia dei dati hello senza richiedere modifiche toohello applicazione. Questo comportamento è trasparente toohello client. Per altre informazioni, vedere [Transparent Data Encryption con il database SQL di Azure](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database). 

#### <a name="azure-data-lake-store"></a>Archivio Azure Data Lake
Archivio Azure Data Lake offre anche la crittografia per i dati archiviati nell'account hello. Quando abilitata, archivio Data Lake automaticamente crittografa i dati prima di rendere permanenti e decrittografa prima di recupero, rendendo trasparente toohello client l'accesso ai dati hello. Per altre informazioni, vedere [Sicurezza in Archivio Azure Data Lake](../data-lake-store/data-lake-store-security-overview.md). 

#### <a name="azure-blob-storage-and-azure-table-storage"></a>Archiviazione BLOB di Azure e Archiviazione tabelle di Azure
Archiviazione di Azure nell'archiviazione Blob e tabelle di Azure supporta la crittografia del Servizio archiviazione (SSE), che crittografa automaticamente i dati prima di salvare in modo permanente toostorage e decrittografa prima il recupero. Per altre informazioni, vedere [Crittografia del servizio di archiviazione di Azure per dati inattivi](../storage/common/storage-service-encryption.md).

#### <a name="amazon-s3"></a>Amazon S3
Amazon S3 supporta la crittografia client e server dei dati inattivi. Per altre informazioni, vedere [Protezione dei dati mediante la crittografia](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingEncryption.html). Attualmente, Data Factory non supporta Amazon S3 all'interno di un cloud privato virtuale (VPC).

#### <a name="amazon-redshift"></a>Amazon Redshift
Amazon Redshift supporta la crittografia cluster per i dati inattivi. Per altre informazioni, vedere [Amazon Redshift Database Encryption](http://docs.aws.amazon.com/redshift/latest/mgmt/working-with-db-encryption.html) (Crittografia database Amazon Redshift). Attualmente, Data Factory non supporta Amazon Redshift all'interno di un cloud privato virtuale (VPC). 

#### <a name="salesforce"></a>Salesforce
Salesforce supporta il servizio Shield Platform Encryption, che consente la crittografia di tutti i file, gli allegati e i campi personalizzati. Per ulteriori informazioni, vedere [hello comprensione del flusso di autenticazione di OAuth Web Server](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_web_server_oauth_flow.htm).  

## <a name="hybrid-scenarios-using-data-management-gateway"></a>Scenari ibridi (usando il gateway di gestione dati)
Scenari ibridi richiedono toobe Gateway di gestione dati installato in una rete locale o all'interno di una rete virtuale (Azure) o un cloud privato virtuale (Amazon). gateway Hello deve essere in grado di tooaccess archivi di dati locali hello. Per ulteriori informazioni sul gateway hello, vedere [Gateway di gestione dati](data-factory-data-management-gateway.md). 

![Canali del gateway di gestione dati](media/data-factory-data-movement-security-considerations/data-management-gateway-channels.png)

Hello **canale comando** consente la comunicazione tra servizi lo spostamento dei dati in Data Factory e i Gateway di gestione dati. comunicazione Hello contiene informazioni correlate toohello attività. canale dati Hello viene utilizzato per trasferire dati tra archivi dati locali e gli archivi dati cloud.    

### <a name="on-premises-data-store-credentials"></a>Credenziali dell'archivio dati locale
credenziali di Hello per gli archivi dati locali vengono archiviate in locale (non nel cloud di hello). possono essere impostate in tre modi diversi. 

- Usando **testo normale** (meno sicuro) tramite HTTPS dal portale di Azure/Copia guidata. Hello credenziali vengono passate in gateway locale toohello testo normale.
- Usando la **libreria JavaScript per la crittografia da Copia guidata**.
- Usando l'**app di gestione delle credenziali basata su un solo clic**. Fare clic su Hello-dopo l'applicazione viene eseguita in hello nel computer locale che dispone di un gateway di accesso toohello e imposta le credenziali per l'archivio dati hello. Questa opzione e hello successiva sono hello opzioni più sicure. applicazione di gestione delle credenziali di Hello, per impostazione predefinita, utilizza porta hello 8050 computer hello con gateway per proteggere le comunicazioni.  
- Utilizzare [New AzureRmDataFactoryEncryptValue](/powershell/module/azurerm.datafactories/New-AzureRmDataFactoryEncryptValue) credenziali tooencrypt cmdlet di PowerShell. cmdlet di Hello Usa certificato hello che tale gateway è configurato toouse tooencrypt hello credenziali. È possibile utilizzare le credenziali crittografato hello restituite da questo cmdlet e aggiungerlo troppo**EncryptedCredential** elemento di hello **connectionString** nel file JSON hello utilizzati con hello [ Nuovo AzureRmDataFactoryLinkedService](/powershell/module/azurerm.datafactories/new-azurermdatafactorylinkedservice) cmdlet o nel frammento di codice JSON hello in hello Editor delle Data Factory nel portale di hello. Scegliere questa opzione e hello-dopo l'applicazione sono opzioni più sicure hello. 

#### <a name="javascript-cryptography-library-based-encryption"></a>Crittografia basata sulla libreria JavaScript per la crittografia
È possibile crittografare le credenziali di archivio dati utilizzando [libreria JavaScript crittografia](https://www.microsoft.com/download/details.aspx?id=52439) da hello [Copia guidata](data-factory-copy-wizard.md). Quando si seleziona questa opzione, hello Copia guidata recupera hello chiave pubblica del gateway e Usa credenziali dell'archivio dati tooencrypt hello. le credenziali di Hello vengono decrittografate dal computer del gateway hello e protetti tramite Windows [DPAPI](https://msdn.microsoft.com/library/ms995355.aspx).

**Browser supportati:** IE8, IE9, IE10, IE11, Microsoft Edge e l'ultima versione di Firefox, Chrome, Opera, Safari. 

#### <a name="click-once-credentials-manager-app"></a>App di gestione delle credenziali con un solo clic
È possibile avviare fare clic su hello-una volta in base a credenziali manager app dal portale di Azure o Copia guidata durante la creazione di pipeline. Questa applicazione assicura che le credenziali non vengono trasferite in testo normale in transito hello. Per impostazione predefinita, Usa la porta hello **8050** nel computer di hello con gateway per la comunicazione protetta. Se necessario, è possibile cambiare porta.  
  
![Porta HTTPS per il gateway hello](media/data-factory-data-movement-security-considerations/https-port-for-gateway.png)

Attualmente, il gateway di gestione dati usa un singolo **certificato**. Questo certificato viene creato durante l'installazione del gateway hello (si applica tooData Gateway di gestione creato dopo novembre 2016 e 2.4.xxxx.x versione o versioni successive). È possibile sostituire il certificato con il proprio certificato SSL/TLS. Questo certificato viene usato per fare clic su hello-una volta toosecurely applicazione di gestione delle credenziali di connessione toohello computer del gateway per l'impostazione delle credenziali dell'archivio dati. Archivia i dati delle credenziali dell'archivio sicuro locale tramite Windows hello [DPAPI](https://msdn.microsoft.com/library/ms995355.aspx) computer hello con gateway. 

> [!NOTE]
> I gateway precedenti sono stati installati prima di novembre 2016 o versione 2.3.xxxx.x continuano toouse credenziali crittografate e archiviate nel cloud. Anche se si esegue l'aggiornamento di versione più recente di hello gateway toohello, hello credenziali non sono migrati tooan nel computer locale    
  
| Versione del gateway (durante la creazione) | Credenziali memorizzate | Crittografia/sicurezza delle credenziali | 
| --------------------------------- | ------------------ | --------- |  
| < = 2.3.xxxx.x | Nel cloud | Crittografata con il certificato (diversa dalle hello uno utilizzato dall'applicazione di gestione delle credenziali) | 
| > = 2.4.xxxx.x | Locale | Protette tramite DPAPI | 
  

### <a name="encryption-in-transit"></a>Crittografia in transito
Tutti i trasferimenti di dati sono tramite un canale sicuro **HTTPS** e **TLS su TCP** attacchi man-in-the-middle tooprevent durante la comunicazione con servizi di Azure.
 
È inoltre possibile utilizzare [VPN IPSec](../vpn-gateway/vpn-gateway-about-vpn-devices.md) o [Express Route](../expressroute/expressroute-introduction.md) canale di comunicazione sicuro hello toofurther tra la rete locale e Azure.

Rete virtuale è una rappresentazione logica della rete nel cloud hello. È possibile connettersi a un tooyour di rete locale rete virtuale di Azure (VNet) mediante la configurazione VPN IPSec (site-to-site) o Express Route (Peering privato)       

Hello nella tabella seguente sono riepilogate hello rete e gateway configurazione indicazioni in base alle diverse combinazioni di percorsi di origine e destinazione per lo spostamento dei dati ibrido.

| Sorgente | Destination | Network configuration | Configurazione del gateway |
| ------ | ----------- | --------------------- | ------------- | 
| Locale | Servizi cloud e macchine virtuali distribuiti nelle reti virtuali | VPN IPSec (da punto a sito o da sito a sito) | Il gateway può essere installato in locale o in una VM di Azure nella VNet | 
| Locale | Servizi cloud e macchine virtuali distribuiti nelle reti virtuali | ExpressRoute (peering privato) | Il gateway può essere installato in locale o in una macchina virtuale di Azure nella VNet | 
| Locale | Servizi basati su Azure con un endpoint pubblico | ExpressRoute (peering pubblico) | Il gateway deve essere installato in locale | 

Hello immagini seguenti mostrano utilizzo hello del Gateway di gestione dati per lo spostamento dei dati tra un database locale e servizi di Azure tramite expressroute e VPN IPSec (con la rete virtuale):

**ExpressRoute:**
 
![usare Express Route con il gateway](media/data-factory-data-movement-security-considerations/express-route-for-gateway.png) 

**VPN IPSec:**

![VPN IPSec con gateway](media/data-factory-data-movement-security-considerations/ipsec-vpn-for-gateway.png)

### <a name="firewall-configurations-and-whitelisting-ip-address-of-gateway"></a>Configurazioni del firewall e inserimento nell'elenco elementi consentiti dell'indirizzo IP del gateway

#### <a name="firewall-requirements-for-on-premisesprivate-network"></a>Requisiti del firewall per la rete locale/privata  
In un'organizzazione, un **firewall aziendale** viene eseguito sul router centrale di hello dell'organizzazione hello. E, **Windows firewall** eseguito come daemon computer hello locale in cui hello è installato gateway. 

Hello nella tabella seguente vengono **porta in uscita** e requisiti di dominio per hello **firewall aziendale**.

| Nomi di dominio | Porte in uscita | Descrizione |
| ------------ | -------------- | ----------- | 
| `*.servicebus.windows.net` | 443, 80 | Richieste dai servizi hello gateway tooconnect toodata lo spostamento in Data Factory |
| `*.core.windows.net` | 443 | Utilizzato da hello gateway tooconnect tooAzure Account di archiviazione quando si utilizza hello [staging copia](data-factory-copy-activity-performance.md#staged-copy) funzionalità. | 
| `*.frontend.clouddatahub.net` | 443 | Richiesto da hello gateway tooconnect toohello servizio Azure Data Factory. | 
| `*.database.windows.net` | 1433   | (OPZIONALE) necessaria quando la destinazione è il database SQL di Azure o Azure SQL Data Warehouse. Hello utilizzare staging copia funzionalità toocopy dati tooAzure SQL Database/Azure SQL Data Warehouse senza dover aprire la porta 1433 hello. | 
| `*.azuredatalakestore.net` | 443 | (OPTIONALE) necessaria quando la destinazione è Azure Data Lake Store | 

> [!NOTE] 
> È possibile toomanage porte / domini whitelist hello livello firewall aziendale come richiesto dalle origini dati. Nella tabella sono riportati solo esempi di database SQL di Azure, Azure SQL Data Warehouse e Azure Data Lake Store.   

Hello nella tabella seguente vengono **porta in ingresso** requisiti per hello **firewall windows**.

| Porte in ingresso | Descrizione | 
| ------------- | ----------- | 
| 8050 (TCP) | Richiesto da hello credenziale Gestione applicazione toosecurely le credenziali impostate per gli archivi dati locali nel gateway hello. | 

![Requisiti relativi alla porta del gateway](media\data-factory-data-movement-security-considerations/gateway-port-requirements.png) 

#### <a name="ip-configurations-whitelisting-in-data-store"></a>Inserimento nell'elenco elementi consentiti/configurazioni IP nell'archivio dati
Alcuni archivi dati nel cloud hello richiedono inoltre whitelist dell'indirizzo IP del computer hello accedervi. Verificare che l'indirizzo IP di hello del gateway hello è abilitata o configurate in firewall in modo appropriato.

Hello archivi dati cloud seguenti richiedono whitelist dell'indirizzo IP del computer del gateway hello. Alcuni di questi archivi dati, per impostazione predefinita, potrebbero non richiedere whitelist degli indirizzi IP hello. 

- [Database SQL di Azure](../sql-database/sql-database-firewall-configure.md) 
- [Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md#create-a-server-level-firewall-rule-in-the-azure-portal)
- [Archivio Data Lake di Azure](../data-lake-store/data-lake-store-secure-data.md#set-ip-address-range-for-data-access)
- [Azure Cosmos DB](../documentdb/documentdb-firewall-support.md)
- [Amazon Redshift](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) 

## <a name="frequently-asked-questions"></a>Domande frequenti

**Domanda:** hello Gateway può essere condivisi tra diversi data factory?
**Risposta:** questa funzionalità non è ancora supportata, ma Microsoft ci sta lavorando attivamente.

**Domanda:** quali sono i requisiti delle porte hello per toowork gateway hello?
**Risposta:** Gateway rende tooopen le connessioni basate su HTTP internet. Hello **porte in uscita 443 e 80** devono essere aperte per gateway toomake questa connessione. Aprire **8050 di porta in ingresso** solo a livello di computer hello (non a livello di firewall aziendale) per l'applicazione di gestione credenziali. Se viene utilizzato il Database di SQL Azure o Azure SQL Data Warehouse come origine / destinazione, sarà necessario tooopen **1433** anche la porta. Per altre informazioni, vedere la sezione [Configurazioni del firewall e inserimento nell'elenco elementi consentiti degli indirizzi IP](#firewall-configurations-and-whitelisting-ip-address-of gateway). 

**Domanda:** quali sono i requisiti relativi al certificato per il gateway?
**Risposta:** gateway corrente richiede un certificato che viene utilizzato dall'applicazione di gestione delle credenziali hello per impostare in modo sicuro le credenziali dell'archivio dati. Questo certificato è un certificato autofirmato creato e configurato dal programma di installazione di hello gateway. In alternativa, è possibile usare il proprio certificato TLS/SSL. Per altre informazioni, vedere la sezione dedicata all'[applicazione di gestione delle credenziali con un solo clic](#click-once-credentials-manager-app). 

## <a name="next-steps"></a>Passaggi successivi
Per informazioni sulle prestazioni dell'attività di copia, vedere [Guida alle prestazioni dell'attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).

 
