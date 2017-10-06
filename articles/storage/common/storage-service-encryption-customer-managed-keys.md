---
title: la crittografia del servizio di archiviazione aaaAzure utilizzando cliente gestito chiavi nell'insieme di credenziali chiave di Azure | Documenti Microsoft
description: "Utilizzare hello la crittografia del servizio di archiviazione di Azure funzionalità tooencrypt l'archiviazione Blob di Azure sul lato servizio hello quando si archiviano dati hello decrittografarlo durante il recupero dei dati di hello cliente utilizzando chiavi gestite."
services: storage
documentationcenter: .net
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: lakasa
ms.openlocfilehash: eb2e0ad27df40e61f9c08b9db7ca7a7568adad9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storage-service-encryption-using-customer-managed-keys-in-azure-key-vault"></a>Crittografia del servizio di archiviazione con chiavi gestite dall'utente in Azure Key Vault

Microsoft Azure viene eseguito il commit toohelping protetto e proteggere i dati toomeet la sicurezza dell'organizzazione e impegni di conformità.  È possibile proteggere i dati inattivi è toouse archiviazione servizio di crittografia (SSE), che crittografa i dati durante la scrittura di toostorage automaticamente e consente di decrittografare i dati quando questi vengono recuperati. Hello crittografia e decrittografia è automatico, è completamente trasparente e utilizza 256 bit [crittografia AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), uno di blocco più forte hello gli algoritmi di crittografia disponibili.

È possibile usare con SSE le chiavi di crittografia gestite da Microsoft oppure con le proprie chiavi di crittografia. Questo articolo illustra hello quest'ultimo. Per altre informazioni sull'utilizzo di chiavi gestite da Microsoft o sulla crittografia SSE in generale, vedere [Crittografia del servizio di archiviazione di Azure per dati inattivi](../storage-service-encryption.md).

tooprovide hello possibilità toouse proprie chiavi di crittografia, SSE per l'archiviazione Blob è integrato con insieme di credenziali chiave di Azure (insieme). È possibile creare proprie chiavi di crittografia e averle archiviate nell'insieme oppure è possibile utilizzare le chiavi di crittografia toogenerate API dell'insieme. Non solo AKV consentono toomanage e controllare le chiavi, consente inoltre di tooaudit l'utilizzo della chiave. 

Perché è consigliabile toocreate chiavi personalizzate? Offre una maggiore flessibilità, consentendo toocreate, ruotare, disabilitare e definire i controlli di accesso. Consente inoltre di che chiavi di crittografia hello tooaudit utilizzato tooprotect i dati.

## <a name="sse-with-customer-managed-keys-preview"></a>Crittografia SSE con anteprima delle chiavi gestite dal cliente

Questa funzionalità è attualmente in anteprima. toouse tale funzionalità, è necessario toocreate un nuovo account di archiviazione. È possibile creare un nuovo insieme di credenziali chiave e una nuova chiave oppure usare un insieme di credenziali e una chiave esistenti. account di archiviazione Hello e l'insieme di credenziali chiave hello devono trovarsi in hello stessa area, ma può essere in diverse sottoscrizioni.

Nell'anteprima hello contatto tooparticipate [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com). Verrà fornito un collegamento speciale tooparticipate in anteprima hello.

toolearn informazioni, vedere toohello [domande frequenti su](#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).

> [!IMPORTANT]
> È necessario iscriversi a hello anteprima precedente toofollowing hello passaggi descritti in questo articolo. Senza accesso all'anteprima, non sarà possibile tooenable in grado di questa funzionalità nel portale di hello.

## <a name="getting-started"></a>Introduzione
## <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a>Passaggio 1: [Creare un nuovo account di archiviazione](../storage-create-storage-account.md)

## <a name="step-2-enable-encryption"></a>Passaggio 2: Abilitare la crittografia
È possibile abilitare SSE per account di archiviazione di hello utilizzando hello [portale di Azure](https://portal.azure.com). Nel pannello delle impostazioni hello hello account di archiviazione, come illustrato nella seguente figura, fare clic di crittografia di hello cercare hello sezione servizio Blob.

![Screenshot del portale che illustra l'opzione Crittografia](./media/storage-service-encryption-customer-managed-keys/ssecmk1.png)
<br/>*Abilitare la crittografia SSE per il servizio BLOB*

Se si desidera tooprogrammatically Abilita o disabilita hello la crittografia del servizio di archiviazione in un account di archiviazione, è possibile utilizzare hello [API REST del Provider di risorse archiviazione Azure](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN), hello [libreria Client di Provider di risorse di archiviazione per .NET](https://docs.microsoft.com/en-us/dotnet/api/?redirectedfrom=MSDN), [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview?view=azurermps-4.0.0), o hello [CLI di Azure](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli).

In questa schermata, se non è possibile visualizzare hello "Usa la propria chiave" casella di controllo non approvate per l'anteprima di hello. Invia messaggio di posta elettronica troppo[ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) e richiedere l'approvazione.

![Screenshot del portale che visualizza l'anteprima della crittografia](./media/storage-service-encryption-customer-managed-keys/ssecmk1.png)

Per impostazione predefinita, SSE usa le chiavi gestite da Microsoft. toouse chiavi personalizzate hello casella. Quindi è possibile specificare l'URI della chiave, o selezionare una chiave e un insieme di credenziali chiave dalla selezione di hello.

## <a name="step-3-select-your-key"></a>Passaggio 3: Selezionare la chiave

![Screenshot del portale che visualizza l'opzione di crittografia Usare una chiave personalizzata](./media/storage-service-encryption-customer-managed-keys/ssecmk2.png)

![Screenshot del portale che visualizza l'opzione di crittografia Immettere l'URI della chiave](./media/storage-service-encryption-customer-managed-keys/ssecmk3.png)

Se l'account di archiviazione hello non dispone di accesso toohello insieme di credenziali chiave, è possibile eseguire l'esempio hello comando mediante Azure Powershell toogrant toohello archiviazione gli account di accesso toohello necessarie insieme di credenziali chiave.

![Screenshot del portale che visualizza l'accesso negato all'insieme di credenziali delle chiavi](./media/storage-service-encryption-customer-managed-keys/ssecmk4.png)

È inoltre possibile concedere l'accesso tramite il portale di Azure hello toohello insieme credenziali chiavi Azure nel portale di Azure hello e concessione dell'accesso toohello account di archiviazione.

## <a name="step-4-copy-data-toostorage-account"></a>Passaggio 4: Copiare account toostorage dati
Se si desidera tootransfer dati nel nuovo account di archiviazione in modo che è crittografato, fare riferimento troppo[passaggio 3 della Guida introduttiva alla crittografia del servizio di archiviazione per i dati inattivi](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-3-copy-data-to-storage-account).

## <a name="step-5-query-hello-status-of-hello-encrypted-data"></a>Passaggio 5: Eseguire una Query sullo stato di hello di dati crittografato hello
stato hello tooquery di hello i dati crittografati, fare riferimento troppo[passaggio 4 della Guida introduttiva alla crittografia del servizio di archiviazione per i dati inattivi](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-4-query-the-status-of-the-encrypted-data).

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a>Domande frequenti su Crittografia del servizio di archiviazione per i dati inattivi
**D: È possibile usare SSE con chiavi gestite dal cliente se si usa l'archiviazione Premium?**

R: Sì, la crittografia SSE con chiavi gestite da Microsoft e chiavi gestite dal cliente è supportata sia nell'archiviazione Standard sia nell'archiviazione Premium. 

**D: È possibile creare nuovi account di archiviazione con crittografia SSE con chiavi gestite dal cliente abilitata usando Azure PowerShell e l'interfaccia della riga di comando di Azure?**

A: Sì.

**D: Qual è il costo aggiuntivo dell'Archiviazione di Azure se si abilita la crittografia SSE con chiavi gestite dal cliente?**

R: Per l'uso di Azure Key Vault è previsto un costo. Per altre informazioni, visitare la [pagina relativa ai prezzi di Key Vault](https://azure.microsoft.com/en-us/pricing/details/key-vault/). Per l'uso della crittografia SSE non sono previsti costi aggiuntivi.

**D: posso revoca dell'accesso toohello chiavi di crittografia?**

R: Sì, è possibile revocare l'accesso in qualsiasi momento. Esistono diversi modi toorevoke tooyour tasti di scelta. Fare riferimento troppo[insieme di credenziali chiave di Azure PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.0.0) e [CLI insieme di credenziali chiave di Azure](https://docs.microsoft.com/en-us/cli/azure/keyvault) per altri dettagli. Revoca dell'accesso in modo efficace bloccherà accesso tooall BLOB nell'account di archiviazione hello come hello chiave di crittografia di Account non è accessibile da archiviazione di Azure.

**D: È possibile creare un account di archiviazione e una chiave in aree diverse?**

R: no, account di archiviazione hello e chiave/chiave di insieme di credenziali necessario toobe in hello stessa area. 

**D: è possibile abilitare SSE con chiavi gestito dal cliente durante la creazione di account di archiviazione hello?**

R: No. Quando si abilita SSE durante la creazione di account di archiviazione hello, è possibile utilizzare solo chiavi gestita da Microsoft. Se si desidera toouse gestito dal cliente chiavi, è necessario aggiornare le proprietà account di archiviazione hello. È possibile usare REST o uno dei tooprogrammatically librerie client di hello archiviazione aggiornare l'account di archiviazione o aggiornare le proprietà account di archiviazione hello tramite hello portale di Azure dopo la creazione di account hello.

**D: è possibile disabilitare la crittografia mentre si usa la crittografia SSE con chiavi gestite dal cliente?**

R: No, non è possibile disabilitare la crittografia mentre si usa la crittografia SSE con chiavi gestite dal cliente. crittografia toodisable, è necessario passare le chiavi di toousing gestita da Microsoft. È possibile farlo con hello portale di Azure o PowerShell.

**D: La funzionalità Crittografia del servizio di archiviazione è abilitata per impostazione predefinita quando si crea un nuovo account di archiviazione?**

R: SSE non è abilitato per impostazione predefinita. è possibile utilizzare hello tooenable portale Azure è. Anche a livello di codice, è possibile abilitare questa funzionalità utilizzando hello API REST di Provider di risorse di archiviazione. 

**D: Non è possibile abilitare la crittografia sull'account di archiviazione.**

R: Se si tratta di un account di archiviazione di Resource Manager, gli account di archiviazione di tipo classico non sono supportati. La crittografia SSE con chiavi gestite dal cliente può anche essere attivata solo sugli account di archiviazione di Gestione risorse appena creati.

**D: La crittografia SSE con chiavi gestite dal cliente è disponibile solo in aree specifiche?**

R: In questa versione di anteprima la crittografia SSE è disponibile solo in determinate aree per l'archiviazione BLOB. Messaggio di posta elettronica [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) toocheck per la disponibilità e i dettagli sull'anteprima. 

**D: come si può contattare un utente se verificano problemi o si desidera tooprovide feedback?**

R: contatto [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) per eventuali problemi correlati tooStorage la crittografia del servizio. 

## <a name="next-steps"></a>Passaggi successivi

*   Per ulteriori informazioni su un set completo di hello di sicurezza funzionalità che consentono agli sviluppatori di compilare applicazioni protette, vedere hello [Guida alla protezione di archiviazione](https://docs.microsoft.com/en-us/azure/storage/storage-security-guide).
*   Per informazioni generali su Azure Key Vault , vedere [Cos'è l'insieme di credenziali chiave di Azure?](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)
*   Per la guida introduttiva di Azure Key Vault, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure](../../key-vault/key-vault-get-started.md).
