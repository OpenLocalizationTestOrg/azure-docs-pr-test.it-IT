Hello [libreria di Configuration Manager di Microsoft Azure per .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) fornisce una classe per l'analisi di una stringa di connessione da un file di configurazione. Hello [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) classe analizza le impostazioni di configurazione indipendentemente dal fatto se un'applicazione hello client è in esecuzione sul desktop di hello, in un dispositivo mobile, in una macchina virtuale di Azure o in un servizio cloud di Azure.

tooreference hello CloudConfigurationManager pacchetto, aggiungere il seguente hello `using` direttiva:

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

Di seguito è riportato un esempio che illustra come tooretrieve una stringa di connessione da un file di configurazione:

```csharp
// Parse hello connection string and return a reference toohello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

Utilizzo di hello Azure Configuration Manager è facoltativo. È inoltre possibile utilizzare un'API come hello .NET Framework [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) classe.

