<span data-ttu-id="fce70-101">istanza di Cache Redis di Azure tooan tooconnect, i client della cache necessitino nome host hello, porte e le chiavi della cache di hello.</span><span class="sxs-lookup"><span data-stu-id="fce70-101">tooconnect tooan Azure Redis Cache instance, cache clients need hello host name, ports, and keys of hello cache.</span></span> <span data-ttu-id="fce70-102">Alcuni client possono fare riferimento a elementi toothese dai nomi leggermente diversi.</span><span class="sxs-lookup"><span data-stu-id="fce70-102">Some clients may refer toothese items by slightly different names.</span></span> <span data-ttu-id="fce70-103">È possibile recuperare queste informazioni nel portale di Azure hello o utilizzando gli strumenti da riga di comando, ad esempio CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="fce70-103">You can retrieve this information in hello Azure portal or by using command-line tools such as Azure CLI.</span></span>

### <a name="retrieve-host-name-ports-and-access-keys-using-hello-azure-portal"></a><span data-ttu-id="fce70-104">Recuperare il nome host, porte e le chiavi di accesso tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="fce70-104">Retrieve host name, ports, and access keys using hello Azure Portal</span></span>
<span data-ttu-id="fce70-105">tooretrieve e nome host, porte, le chiavi di accesso tramite il portale di Azure, hello [Sfoglia](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour cache di hello [portale di Azure](https://portal.azure.com) e fare clic su **le chiavi di accesso** e  **Proprietà** in hello **menu risorse**.</span><span class="sxs-lookup"><span data-stu-id="fce70-105">tooretrieve host name, ports, and access keys using hello Azure Portal, [browse](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour cache in hello [Azure portal](https://portal.azure.com) and click **Access keys** and **Properties** in hello **Resource menu**.</span></span> 

![Impostazioni della Cache Redis](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a><span data-ttu-id="fce70-107">Recuperare il nome dell'host, le porte e le chiavi di accesso usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="fce70-107">Retrieve host name, ports, and access keys using Azure CLI</span></span>
<span data-ttu-id="fce70-108">nome host di tooretrieve hello e le porte che utilizzano Azure CLI 2.0 è possibile chiamare [Mostra redis az](https://docs.microsoft.com/cli/azure/redis#show)e le chiavi di hello tooretrieve è possibile chiamare [az redis elenco chiavi](https://docs.microsoft.com/cli/azure/redis#list-keys).</span><span class="sxs-lookup"><span data-stu-id="fce70-108">tooretrieve hello host name and ports using Azure CLI 2.0 you can call [az redis show](https://docs.microsoft.com/cli/azure/redis#show), and tooretrieve hello keys you can call [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys).</span></span> <span data-ttu-id="fce70-109">lo script seguente Hello chiama questi due comandi e un'indicazione hello nome host, porte e le chiavi toohello console.</span><span class="sxs-lookup"><span data-stu-id="fce70-109">hello following script calls these two commands and echos hello hostname, ports, and keys toohello console.</span></span>

```azurecli
#/bin/bash

# Retrieve hello hostname, ports, and keys for contosoCache located in contosoGroup

# Retrieve hello hostname and ports for an Azure Redis Cache instance
redis=($(az redis show --name contosoCache --resource-group contosoGroup --query [hostName,enableNonSslPort,port,sslPort] --output tsv))

# Retrieve hello keys for an Azure Redis Cache instance
keys=($(az redis list-keys --name contosoCache --resource-group contosoGroup --query [primaryKey,secondaryKey] --output tsv))

# Display hello retrieved hostname, keys, and ports
echo "Hostname:" ${redis[0]}
echo "Non SSL Port:" ${redis[2]}
echo "Non SSL Port Enabled:" ${redis[1]}
echo "SSL Port:" ${redis[3]}
echo "Primary Key:" ${keys[0]}
echo "Secondary Key:" ${keys[1]}
```

<span data-ttu-id="fce70-110">Per ulteriori informazioni su questo script, vedere [ottenere hello hostname, porte e le chiavi per Cache Redis di Azure](../articles/redis-cache/scripts/cache-keys-ports.md).</span><span class="sxs-lookup"><span data-stu-id="fce70-110">For more information about this script, see [Get hello hostname, ports, and keys for Azure Redis Cache](../articles/redis-cache/scripts/cache-keys-ports.md).</span></span> <span data-ttu-id="fce70-111">Per altre informazioni sull'interfaccia della riga di comando di Azure 2.0, vedere [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Installare l'interfaccia della riga di comando di Azure 2.0) e [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) (Introduzione all'interfaccia della riga di comando di Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="fce70-111">For more information on Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>
