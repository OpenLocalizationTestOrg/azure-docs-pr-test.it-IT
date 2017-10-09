### <a name="azure-storage-linked-service"></a>Servizio collegato Archiviazione di Azure
Hello **servizio collegato di archiviazione di Azure** consente toolink un'archiviazione di Azure account tooan data factory di Azure tramite hello **chiave dell'account**, che consente di data factory di hello con accesso globale toohello Azure Spazio di archiviazione. Hello nella tabella seguente fornisce una descrizione JSON elementi specifici tooAzure servizio collegato di archiviazione.

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| type |proprietà di tipo Hello deve essere impostata su: **AzureStorage** |Sì |
| connectionString |Specificare le informazioni necessarie tooconnect tooAzure archiviazione per la proprietà connectionString hello. |Sì |

Vedere l'articolo per la chiave account hello tooview o copia di passaggi seguente per una risorsa di archiviazione di Azure hello: [visualizzare, copiare e rigenerare le chiavi di accesso di archiviazione](../articles/storage/common/storage-create-storage-account.md#manage-your-storage-account).

**Esempio:**  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

### <a name="azure-storage-sas-linked-service"></a>Servizio collegato di firma di accesso condiviso Archiviazione di Azure
Una firma di accesso condiviso (SAS) fornisce l'accesso delegato tooresources nell'account di archiviazione. In questo modo si toogrant un client limitato tooobjects autorizzazioni nell'account di archiviazione per un determinato periodo di tempo e con un set specificato di autorizzazioni, senza dovere tooshare le chiavi di accesso di account. Hello firma di accesso condiviso è un URI che include i parametri di query di tutte le informazioni di hello necessarie per la risorsa di archiviazione tooa l'accesso autenticato. risorse di archiviazione tooaccess con hello SAS, hello client deve disporre solo toopass nel metodo o costruttore di hello SAS toohello appropriato. Per informazioni dettagliate sulla firma di accesso condiviso, vedere [firme di accesso condiviso: hello comprensione del modello di firma di accesso condiviso](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md)

> [!IMPORTANT]
> Azure Data Factory supporta attualmente solo il **servizio di firma di accesso condiviso**, ma non la firma di accesso condiviso dell'account. Vedere [tipi di firme di accesso condiviso](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md#types-of-shared-access-signatures) per informazioni dettagliate su questi due tipi e come tooconstruct. Nota hello URL SAS generable dal portale Azure Storage Explorer è una firma di accesso condiviso, che non è supportato.
> 

servizio sa di archiviazione di Azure collegati Hello consente toolink un Account di archiviazione Azure tooan data factory di Azure tramite una firma di accesso condiviso (SAS). Fornisce data factory di hello con accesso limitato/scadenza tooall/specifiche risorse (blob/contenitore) nell'archiviazione hello. Hello nella tabella seguente fornisce una descrizione JSON tooAzure specifico di elementi del servizio di archiviazione SAS collegato. 

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| type |proprietà di tipo Hello deve essere impostata su: **AzureStorageSas** |Sì |
| sasUri |Specificare le risorse di archiviazione di Azure toohello URI firma di accesso condiviso, ad esempio una tabella, contenitore o blob.  |Sì |

**Esempio:**

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<Specify SAS URI of hello Azure Storage resource>"   
        }  
    }  
}  
```

Quando si crea un **URI SAS**, prendere in considerazione i seguenti hello:  

* Impostare in lettura/scrittura appropriate **autorizzazioni** per gli oggetti in base a come hello collegato del servizio (lettura, scrittura o lettura/scrittura) viene utilizzato per la data factory.
* Impostare **Ora di scadenza** in modo appropriato. Assicurarsi che gli oggetti di archiviazione hello accesso tooAzure non scade entro il periodo attivo di hello della pipeline hello.
* URI deve essere creato alla destra hello contenitore/blob o il livello di tabella in base a hello necessario. Un blob di Azure di tooan Uri SAS consente tooaccess servizio Data Factory di hello blob specifico. Un contenitore di blob di Azure tooan Uri SAS consente tooiterate servizio Data Factory di hello tramite i BLOB nel contenitore. Se è necessario l'accesso tooprovide più/meno gli oggetti in un secondo momento o aggiornamento hello SAS URI, ricordare di servizio collegato hello tooupdate con hello nuovo URI.   

