## <a name="create-a-ruby-application"></a><span data-ttu-id="9dc1b-101">Creare un'applicazione Ruby</span><span class="sxs-lookup"><span data-stu-id="9dc1b-101">Create a Ruby application</span></span>
<span data-ttu-id="9dc1b-102">Per istruzioni, vedere [Creare un'applicazione Ruby in Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="9dc1b-102">For instructions, see [Create a Ruby Application on Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="9dc1b-103">Configurare il tooUse applicazione Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="9dc1b-103">Configure Your application tooUse Service Bus</span></span>
<span data-ttu-id="9dc1b-104">toouse Service Bus, scaricare e usare il pacchetto Azure Ruby hello, che include un set di librerie di praticità che comunicano con servizi REST di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="9dc1b-104">toouse Service Bus, download and use hello Azure Ruby package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="9dc1b-105">Utilizzare un pacchetto di hello tooobtain RubyGems</span><span class="sxs-lookup"><span data-stu-id="9dc1b-105">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="9dc1b-106">Usare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="9dc1b-106">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="9dc1b-107">Digitare "indicatore installa azure" dipendenze e l'indicatore di hello comando finestra tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="9dc1b-107">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="9dc1b-108">Importa pacchetto di hello</span><span class="sxs-lookup"><span data-stu-id="9dc1b-108">Import hello package</span></span>
<span data-ttu-id="9dc1b-109">Utilizzando un editor di testo, aggiungere hello seguente toohello cima hello Ruby file in cui si intende toouse archiviazione:</span><span class="sxs-lookup"><span data-stu-id="9dc1b-109">Using your favorite text editor, add hello following toohello top of hello Ruby file in which you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="9dc1b-110">Configurare una stringa di connessione per il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="9dc1b-110">Set up a Service Bus connection</span></span>
<span data-ttu-id="9dc1b-111">Esempio di codice seguente hello di utilizzare i valori hello tooset dello spazio dei nomi, nome di hello key, key, firmatario e host:</span><span class="sxs-lookup"><span data-stu-id="9dc1b-111">Use hello following code tooset hello values of namespace, name of hello key, key, signer and host:</span></span>

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

<span data-ttu-id="9dc1b-112">Impostare il valore toohello valore dello spazio dei nomi di hello che anziché l'intero URL hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="9dc1b-112">Set hello namespace value toohello value you created rather than hello entire URL.</span></span> <span data-ttu-id="9dc1b-113">Ad esempio, usare **"yourexamplenamespace"** e non "yourexamplenamespace.servicebus.windows.net".</span><span class="sxs-lookup"><span data-stu-id="9dc1b-113">For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".</span></span>
