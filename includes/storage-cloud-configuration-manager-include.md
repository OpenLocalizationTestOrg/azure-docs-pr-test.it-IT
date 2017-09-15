<span data-ttu-id="5b750-101">La [libreria di Gestione configurazione di Microsoft Azure per .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) fornisce una classe per l'analisi della stringa di connessione da un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="5b750-101">The [Microsoft Azure Configuration Manager Library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) provides a class for parsing a connection string from a configuration file.</span></span> <span data-ttu-id="5b750-102">La classe [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) analizza le impostazioni di configurazione indipendentemente dal fatto che l'applicazione client sia in esecuzione sul PC desktop, su un dispositivo mobile, in una macchina virtuale di Azure o in un servizio cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="5b750-102">The [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) class parses configuration settings regardless of whether the client application is running on the desktop, on a mobile device, in an Azure virtual machine, or in an Azure cloud service.</span></span>

<span data-ttu-id="5b750-103">Per fare riferimento al pacchetto CloudConfigurationManager, aggiungere l'istruzione `using` seguente:</span><span class="sxs-lookup"><span data-stu-id="5b750-103">To reference the CloudConfigurationManager package, add the following `using` directive:</span></span>

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

<span data-ttu-id="5b750-104">Ecco un esempio che illustra come recuperare una stringa di connessione da un file di configurazione:</span><span class="sxs-lookup"><span data-stu-id="5b750-104">Here's an example that shows how to retrieve a connection string from a configuration file:</span></span>

```csharp
// Parse the connection string and return a reference to the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

<span data-ttu-id="5b750-105">L'uso di Gestione configurazione di Azure è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="5b750-105">Using the Azure Configuration Manager is optional.</span></span> <span data-ttu-id="5b750-106">È anche possibile usare un'API, ad esempio la classe [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) di .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="5b750-106">You can also use an API like the .NET Framework's [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) class.</span></span>

