---
title: Guida per gli sviluppatori di aaaAzure chiave dell'insieme di credenziali
description: Gli sviluppatori possono utilizzare le chiavi crittografiche insieme credenziali chiavi Azure toomanage nell'ambiente di Microsoft Azure hello.
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 631cea1315964cd0b97e8b2cf3311754230fb801
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-developers-guide"></a>Guida per gli sviluppatori dell'insieme di credenziali delle chiavi di Azure

Insieme di credenziali chiave consente toosecurely accesso informazioni sensibili all'interno delle applicazioni:

- Chiavi e segreti sono protette senza dover codice hello toowrite manualmente e si è in grado di facilmente toouse usarle dalle applicazioni.
- Si sono in grado di toohave ai propri clienti e gestire le rispettive chiavi in modo da permettere di concentrarsi sulla funzionalità hello core software. In questo modo, le applicazioni non diventerà proprietario responsabilità hello o potenziali responsabilità per i segreti e tutte le chiavi tenant dei clienti.
- L'applicazione può utilizzare chiavi per la firma e crittografia ancora mantiene la gestione delle chiavi hello esterno dall'applicazione, consentendo il toobe soluzione adatto come un'app distribuita geograficamente.
- A partire dalla versione di settembre 2016 hello dell'insieme di credenziali chiave, le applicazioni possono ora utilizzare insieme di credenziali chiave [certificati](https://docs.microsoft.com/rest/api/keyvault/certificate-operations). Per i dettagli, vedere l'articolo relativo alle [informazioni su chiavi, segreti e certificati](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates).

Per altre informazioni generali sull'insieme di credenziali delle chiavi di Azure, vedere l'articolo [Cos'è l'insieme di credenziali chiave di Azure?](key-vault-whatis.md)

## <a name="public-previews"></a>Anteprime pubbliche

Periodicamente, viene rilasciata un'anteprima pubblica di una nuova funzionalità di Key Vault. Provarle e comunicare il feedback all'azienda all'indirizzo e-mail azurekeyvault@microsoft.com, dedicato ai commenti e ai suggerimenti.

### <a name="storage-account-keys---july-10-2017"></a>Chiavi degli account di archiviazione - 10 luglio 2017

>[!NOTE]
>Per questo aggiornamento di hello solo insieme credenziali chiavi Azure **chiavi dell'Account di archiviazione** funzionalità è disponibile in anteprima.

Questa versione di anteprima include la nuova funzionalità di chiavi degli account di archiviazione, disponibile tramite queste interfacce: [.NET/C#](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault/), [REST](https://docs.microsoft.com/rest/api/keyvault/) e [PowerShell](https://docs.microsoft.com/powershell/module/azurerm.keyvault/). 

Per ulteriori informazioni sulla funzionalità di hello nuove chiavi dell'Account di archiviazione, vedere [Panoramica di chiavi di account di archiviazione insieme credenziali chiavi Azure](key-vault-ovw-storage-keys.md).

## <a name="videos"></a>Video

In questo video viene illustrato come toocreate la propria chiave dell'insieme di credenziali e come toouse dall'applicazione di esempio 'Insieme di credenziali chiave Hello' hello.

- [Guida introduttiva per gli sviluppatori di Key Vault](https://channel9.msdn.com/Blogs/Azure/Azure-Key-Vault-Developer-Quick-Start/player)

Risorse citate nel video precedente:

- [Azure PowerShell](http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409)
- [Codice di esempio dell'insieme di credenziali delle chiavi di Azure](http://go.microsoft.com/fwlink/?LinkId=521527&clcid=0x409)

## <a name="creating-and-managing-key-vaults"></a>Creazione e gestione di insiemi di credenziali delle chiavi

Prima di utilizzare l'insieme di credenziali chiave di Azure nel codice, è possibile creare e gestire gli insiemi di credenziali tramite REST, modelli di gestione risorse, PowerShell o l'interfaccia CLI, come descritto in hello seguenti articoli:

- [Creare e gestire insiemi di credenziali chiave con REST](https://docs.microsoft.com/rest/api/keyvault/)
- [Creare e gestire insiemi di credenziali chiave con PowerShell](key-vault-get-started.md)
- [Creare e gestire insiemi di credenziali chiave con l’interfaccia della riga di comando](key-vault-manage-with-cli2.md)
- [Creare un insieme di credenziali delle chiavi e aggiungere un segreto tramite un modello di Azure Resource Manager](../azure-resource-manager/resource-manager-template-keyvault.md)

> [!NOTE]
> Le operazioni sugli insiemi di credenziali delle chiavi vengono autenticate tramite AAD e autorizzate tramite i criteri di accesso dell'insieme di credenziali delle chiavi, definiti per ogni insieme di credenziali.

## <a name="coding-with-key-vault"></a>Codifica con l'insieme di credenziali delle chiavi

sistema di gestione di insieme di credenziali chiave per i programmatori Hello è costituito da diverse interfacce, con REST di base hello. Tramite l'interfaccia REST hello, tutte le risorse di insiemi di credenziali chiave è accessibile; le chiavi, i segreti e certificati. [Informazioni di riferimento sull'API REST di Key Vault](https://docs.microsoft.com/rest/api/keyvault/). 

### <a name="supported-programming-languages"></a>Linguaggi di programmazione supportati

#### <a name="net"></a>.NET

- [Informazioni di riferimento sulle API .NET per Key Vault](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault) 

Per ulteriori informazioni sulla versione 2. x hello di hello .NET SDK, vedere hello [note sulla versione](key-vault-dotnet2api-release-notes.md).

#### <a name="java"></a>Java

- [Java SDK per Key Vault](https://docs.microsoft.com/java/api/com.microsoft.azure.keyvault)

#### <a name="nodejs"></a>Node.js

In Node.js, API di gestione dell'insieme di credenziali hello e oggetto insieme di credenziali hello API sono separati. Gestione dell'insieme di credenziali delle chiavi consente la creazione e l'aggiornamento dell'insieme di credenziali delle chiavi. L'API delle operazioni di Key Vault funziona con oggetti dell'insieme di credenziali come ad esempio chiavi, segreti e certificati. 

- [Informazioni di riferimento sulle API Node.js per Gestione di Key Vault](http://azure.github.io/azure-sdk-for-node/azure-arm-keyvault/latest/)
- [Informazioni di riferimento sulle API Node.js per le operazioni di Key Vault](http://azure.github.io/azure-sdk-for-node/azure-keyvault/latest/) 

### <a name="quick-start"></a>Avvio rapido

- [Creare un insieme di credenziali delle chiavi](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
- [Introduzione a Key Vault in Node.js](https://azure.microsoft.com/en-us/resources/samples/key-vault-node-getting-started/)

### <a name="code-examples"></a>Esempi di codice

Per esempi completi che usano l'insieme di credenziali delle chiavi con le applicazioni, vedere:

- [Esempi di codice di Azure Key Vault](http://www.microsoft.com/download/details.aspx?id=45343): applicazione .NET di esempio *HelloKeyVault* ed esempio di servizio Web di Azure. 
- [Utilizzare l'insieme di credenziali chiave di Azure da un'applicazione Web](key-vault-use-from-web-application.md) -toohelp esercitazione si apprenderà come toouse Azure chiave dell'insieme di credenziali da un'applicazione web in Azure. 

## <a name="how-tos"></a>Procedure

Hello scenari e gli articoli seguenti forniscono linee guida specifiche per attività per l'utilizzo con l'insieme di credenziali chiave di Azure:

- [Modificare l'insieme di credenziali chiave tenant ID dopo la sottoscrizione spostare](key-vault-subscription-move-fix.md) : se si sposta la sottoscrizione di Azure da tenant un tootenant B, insieme di credenziali chiave esistente sono inaccessibili da entità hello (utenti e applicazioni) nel tenant correzione B. questa operazione utilizzando questa Guida.
- [Insieme di credenziali chiave di accesso protetto da firewall](key-vault-access-behind-firewall.md) -tooaccess una chiave dell'insieme di credenziali la chiave dell'insieme di credenziali client applicazione esigenze toobe in grado di tooaccess più endpoint per varie funzionalità.
- [Come tooGenerate e le chiavi Transfer HSM-Protected per insieme credenziali chiavi Azure](key-vault-hsm-protected-keys.md) -Ciò consentirà di pianificare, generare e trasferire la propria toouse chiavi HSM protette insieme di credenziali chiave di Azure.
- [In che modo toopass protette valori (ad esempio le password) durante la distribuzione](../azure-resource-manager/resource-manager-keyvault-parameter.md) : quando è necessario un valore sicuro (ad esempio una password) toopass come parametro durante la distribuzione, è possibile archiviare tale valore come una chiave privata in un valore di hello insieme credenziali chiavi Azure e di riferimento in altre Modelli di gestione risorse.
- [Come toouse insieme di credenziali chiave di extensible key management con SQL Server](https://msdn.microsoft.com/library/dn198405.aspx) -hello connettore SQL Server per insieme credenziali chiavi Azure consente a SQL Server e SQL in VM tooleverage hello insieme credenziali chiavi Azure del servizio come provider di Extensible Key Management (EKM) tooprotect la crittografia di chiavi per il collegamento di applicazioni. Transparent Data Encryption, crittografia dei Backup e la crittografia a livello di colonna.
- [Come toodeploy certificati tooVMs dall'insieme di credenziali chiave](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/) : un'applicazione cloud in esecuzione in una macchina virtuale in Azure esigenze di un certificato. Come ottenere oggi il certificato per questa VM?
- [Come tooset di insieme di credenziali chiave con fine tooend chiave rotazione e il controllo](key-vault-key-rotation-log-monitoring.md) -questo illustra in dettaglio come tooset di rotazione della chiave e il controllo insieme di credenziali chiave di Azure.
- [Deploying Azure Web App Certificate through Key Vault]( https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/) (Distribuzione del certificato dell'app Web di Azure tramite l'insieme di credenziali delle chiavi) offre istruzioni dettagliate per la distribuzione dei certificati archiviati nell'insieme di credenziali delle chiavi come parte dell'offerta del [certificato del servizio app](https://azure.microsoft.com/blog/internals-of-app-service-certificate/).
- [Concedere l'autorizzazione toomany applicazioni tooaccess un insieme di credenziali chiave](key-vault-group-permissions-for-apps.md) criteri di controllo di accesso di chiave dell'insieme di credenziali supporta solo le voci di 16. È tuttavia possibile creare un gruppo di sicurezza di Azure Active Directory. Aggiungere tutti hello associata gruppo di sicurezza toothis entità servizio e quindi concesse l'accesso toothis sicurezza gruppo tooKey insieme di credenziali.
- Per indicazioni specifiche sulle attività relative all'integrazione e all'uso dell'insieme di credenziali delle chiavi con Azure, vedere gli [esempi di modelli di Azure Resource Manager di Ryan Jones per l'insieme di credenziali delle chiavi](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).
- [Come insieme di credenziali chiave toouse soft-eliminazione con CLI](key-vault-soft-delete-cli.md) semplificato utilizzare hello e ciclo di vita di un insieme di credenziali chiave e i vari oggetti dell'insieme di credenziali delle chiavi con soft-eliminazione abilitata.
- [Come insieme di credenziali chiave toouse soft-delete con PowerShell](key-vault-soft-delete-powershell.md) semplificato utilizzare hello e ciclo di vita di un insieme di credenziali chiave e i vari oggetti dell'insieme di credenziali delle chiavi con soft-eliminazione abilitata.

## <a name="integrated-with-key-vault"></a>Integrazione con l'insieme di credenziali delle chiavi

Questi articoli illustrano altri scenari e servizi che usano o si integrano con Key Vault.

- [Crittografia disco Azure](../security/azure-security-disk-encryption.md) si basa su hello standard di settore [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) funzionalità di Windows e hello [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) funzionalità di crittografia del volume tooprovide Linux per hello del sistema operativo e dati hello dischi. soluzione hello è integrato con insieme credenziali chiavi Azure toohelp è controllare e gestire i segreti e tutte le chiavi di crittografia disco hello nella sottoscrizione di insieme di credenziali delle chiavi, assicurando che tutti i dati nei dischi di macchina virtuale hello vengono crittografati a riposo nell'archiviazione Azure.
- [Archivio Azure Data Lake](../data-lake-store/data-lake-store-get-started-portal.md) fornisce l'opzione per la crittografia dei dati archiviati nell'account hello. Gestione delle chiavi, archivio Data Lake fornisce due modalità per la gestione delle chiavi di crittografia master (MEKs), che sono necessari per decrittografare i dati archiviati in hello archivio Data Lake. È possibile consentire archivio Data Lake gestirà automaticamente MEKs hello oppure scegliere la proprietà tooretain di hello MEKs con l'account insieme credenziali chiavi Azure. Specificare la modalità di gestione delle chiavi hello durante la creazione di un account archivio Data Lake. 
- [Azure Information Protection](/information-protection/plan-design/plan-implement-tenant-key) consente toomanager la propria chiave del tenant. Anziché affidare a Microsoft la gestione della chiave del tenant (impostazione predefinita hello), ad esempio, è possibile gestire la propria toocomply chiave tenant a specifiche normative applicabili tooyour organizzazione. Gestire la propria chiave del tenant è anche tooas cui bring your own key, BYOK.

## <a name="key-vault-overviews-and-concepts"></a>Panoramiche e concetti su Key Vault

- [Il comportamento di soft-Elimina insieme di credenziali chiave](key-vault-ovw-soft-delete.md) descrive una funzionalità che consente il recupero di oggetti eliminati, se è stata l'eliminazione di hello accidentali o intenzionali.
- [La limitazione delle richieste client di insieme di credenziali chiave](key-vault-ovw-throttling.md) descrive i concetti di base toohello della limitazione delle richieste e offre un approccio per l'app.
- [Panoramica di chiavi di account di archiviazione insieme di credenziali chiave](key-vault-ovw-storage-keys.md) descritte hello insieme di credenziali chiave integrazione Azure gli account di archiviazione chiavi.
- [Ambienti di sicurezza separati insieme di credenziali chiave](key-vault-ovw-security-worlds.md) descrive hello relazioni tra le aree e le aree di sicurezza.

## <a name="social"></a>Social media

- [Blog sull'insieme di credenziali delle chiavi](http://aka.ms/kvblog)
- [Forum sull'insieme di credenziali delle chiavi](http://aka.ms/kvforum)

## <a name="supporting-libraries"></a>Supporto di librerie

- [Microsoft Azure Key Vault Core Library](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core) include le interfacce **IKey** e **IKeyResolver** per individuare le chiavi dagli identificatori ed eseguire operazioni con le chiavi.
- [Microsoft Azure Key Vault Extensions](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions) fornisce funzionalità estese per Insieme di credenziali delle chiavi di Azure.


