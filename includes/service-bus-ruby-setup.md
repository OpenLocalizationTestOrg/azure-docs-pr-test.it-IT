## <a name="create-a-ruby-application"></a><span data-ttu-id="9fac1-101">Creare un'applicazione Ruby</span><span class="sxs-lookup"><span data-stu-id="9fac1-101">Create a Ruby application</span></span>
<span data-ttu-id="9fac1-102">Per istruzioni, vedere [Creare un'applicazione Ruby in Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="9fac1-102">For instructions, see [Create a Ruby Application on Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="9fac1-103">Configurare l'applicazione per l'uso del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="9fac1-103">Configure Your application to Use Service Bus</span></span>
<span data-ttu-id="9fac1-104">Per usare il bus di servizio, scaricare e usare il pacchetto Ruby di Azure, che comprende un set di pratiche librerie che comunicano con i servizi REST di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9fac1-104">To use Service Bus, download and use the Azure Ruby package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="9fac1-105">Utilizzare RubyGems per ottenere il pacchetto</span><span class="sxs-lookup"><span data-stu-id="9fac1-105">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="9fac1-106">Usare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="9fac1-106">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="9fac1-107">Digitare "gem install azure" nella finestra di comando per installare la gemma e le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="9fac1-107">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="9fac1-108">Importare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="9fac1-108">Import the package</span></span>
<span data-ttu-id="9fac1-109">Usando l'editor di testo preferito aggiungere quanto segue alla parte superiore del file Ruby dove si intende usare l'archiviazione:</span><span class="sxs-lookup"><span data-stu-id="9fac1-109">Using your favorite text editor, add the following to the top of the Ruby file in which you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="9fac1-110">Configurare una stringa di connessione per il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="9fac1-110">Set up a Service Bus connection</span></span>
<span data-ttu-id="9fac1-111">Usare il codice seguente per impostare i valori dello spazio dei nomi, il nome della chiave, la chiave, il firmatario e l'host:</span><span class="sxs-lookup"><span data-stu-id="9fac1-111">Use the following code to set the values of namespace, name of the key, key, signer and host:</span></span>

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

<span data-ttu-id="9fac1-112">Impostare il valore dello spazio dei nomi sul valore creato invece che sull'intero URL.</span><span class="sxs-lookup"><span data-stu-id="9fac1-112">Set the namespace value to the value you created rather than the entire URL.</span></span> <span data-ttu-id="9fac1-113">Ad esempio, usare **"yourexamplenamespace"** e non "yourexamplenamespace.servicebus.windows.net".</span><span class="sxs-lookup"><span data-stu-id="9fac1-113">For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".</span></span>
