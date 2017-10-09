istanza di Cache Redis di Azure tooan tooconnect, i client della cache necessitino nome host hello, porte e le chiavi della cache di hello. Alcuni client possono fare riferimento a elementi toothese dai nomi leggermente diversi. È possibile recuperare queste informazioni nel portale di Azure hello o utilizzando gli strumenti da riga di comando, ad esempio CLI di Azure.

### <a name="retrieve-host-name-ports-and-access-keys-using-hello-azure-portal"></a>Recuperare il nome host, porte e le chiavi di accesso tramite hello portale di Azure
tooretrieve e nome host, porte, le chiavi di accesso tramite il portale di Azure, hello [Sfoglia](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour cache di hello [portale di Azure](https://portal.azure.com) e fare clic su **le chiavi di accesso** e  **Proprietà** in hello **menu risorse**. 

![Impostazioni della Cache Redis](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a>Recuperare il nome dell'host, le porte e le chiavi di accesso usando l'interfaccia della riga di comando di Azure
nome host di tooretrieve hello e le porte che utilizzano Azure CLI 2.0 è possibile chiamare [Mostra redis az](https://docs.microsoft.com/cli/azure/redis#show)e le chiavi di hello tooretrieve è possibile chiamare [az redis elenco chiavi](https://docs.microsoft.com/cli/azure/redis#list-keys). lo script seguente Hello chiama questi due comandi e un'indicazione hello nome host, porte e le chiavi toohello console.

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

Per ulteriori informazioni su questo script, vedere [ottenere hello hostname, porte e le chiavi per Cache Redis di Azure](../articles/redis-cache/scripts/cache-keys-ports.md). Per altre informazioni sull'interfaccia della riga di comando di Azure 2.0, vedere [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Installare l'interfaccia della riga di comando di Azure 2.0) e [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) (Introduzione all'interfaccia della riga di comando di Azure 2.0).
