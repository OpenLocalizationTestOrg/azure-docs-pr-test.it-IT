<span data-ttu-id="08440-101">Hello [libreria di Configuration Manager di Microsoft Azure per .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) fornisce una classe per l'analisi di una stringa di connessione da un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="08440-101">hello [Microsoft Azure Configuration Manager Library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) provides a class for parsing a connection string from a configuration file.</span></span> <span data-ttu-id="08440-102">Hello [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) classe analizza le impostazioni di configurazione indipendentemente dal fatto se un'applicazione hello client è in esecuzione sul desktop di hello, in un dispositivo mobile, in una macchina virtuale di Azure o in un servizio cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="08440-102">hello [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) class parses configuration settings regardless of whether hello client application is running on hello desktop, on a mobile device, in an Azure virtual machine, or in an Azure cloud service.</span></span>

<span data-ttu-id="08440-103">tooreference hello CloudConfigurationManager pacchetto, aggiungere il seguente hello `using` direttiva:</span><span class="sxs-lookup"><span data-stu-id="08440-103">tooreference hello CloudConfigurationManager package, add hello following `using` directive:</span></span>

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

<span data-ttu-id="08440-104">Di seguito è riportato un esempio che illustra come tooretrieve una stringa di connessione da un file di configurazione:</span><span class="sxs-lookup"><span data-stu-id="08440-104">Here's an example that shows how tooretrieve a connection string from a configuration file:</span></span>

```csharp
// Parse hello connection string and return a reference toohello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

<span data-ttu-id="08440-105">Utilizzo di hello Azure Configuration Manager è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="08440-105">Using hello Azure Configuration Manager is optional.</span></span> <span data-ttu-id="08440-106">È inoltre possibile utilizzare un'API come hello .NET Framework [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="08440-106">You can also use an API like hello .NET Framework's [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) class.</span></span>

