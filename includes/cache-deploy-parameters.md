
### <a name="cacheskuname"></a><span data-ttu-id="bcd67-101">cacheSKUName</span><span class="sxs-lookup"><span data-stu-id="bcd67-101">cacheSKUName</span></span>
<span data-ttu-id="bcd67-102">Piano tariffario della nuova Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="bcd67-102">The pricing tier of the new Azure Redis Cache.</span></span>

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "The pricing tier of the new Azure Redis Cache."
      }
    },

<span data-ttu-id="bcd67-103">Il modello definisce i valori consentiti per questo parametro (Basic o Standard) e assegna un valore predefinito (Basic) se non viene specificato alcun valore.</span><span class="sxs-lookup"><span data-stu-id="bcd67-103">The template defines the values that are permitted for this parameter (Basic or Standard), and assigns a default value (Basic) if no value is specified.</span></span> <span data-ttu-id="bcd67-104">Basic fornisce un singolo nodo con più dimensioni disponibili fino a 53 GB.</span><span class="sxs-lookup"><span data-stu-id="bcd67-104">Basic provides a single node with multiple sizes available up to 53 GB.</span></span>
<span data-ttu-id="bcd67-105">Standard fornisce due nodi di replica/primario con più dimensioni disponibili fino a 53 GB e contratto di servizio con disponibilità del 99,9%.</span><span class="sxs-lookup"><span data-stu-id="bcd67-105">Standard provides two-node Primary/Replica with multiple sizes available up to 53 GB and 99.9% SLA.</span></span>

### <a name="cacheskufamily"></a><span data-ttu-id="bcd67-106">cacheSKUFamily</span><span class="sxs-lookup"><span data-stu-id="bcd67-106">cacheSKUFamily</span></span>
<span data-ttu-id="bcd67-107">Famiglia dello SKU.</span><span class="sxs-lookup"><span data-stu-id="bcd67-107">The family for the sku.</span></span>

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "The family for the sku."
      }
    },


### <a name="cacheskucapacity"></a><span data-ttu-id="bcd67-108">cacheSKUCapacity</span><span class="sxs-lookup"><span data-stu-id="bcd67-108">cacheSKUCapacity</span></span>
<span data-ttu-id="bcd67-109">Dimensioni dell'istanza della nuova Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="bcd67-109">The size of the new Azure Redis Cache instance.</span></span> 

    "cacheSKUCapacity": {
      "type": "int",
      "allowedValues": [
        0,
        1,
        2,
        3,
        4,
        5,
        6
      ],
      "defaultValue": 0,
      "metadata": {
        "description": "The size of the new Azure Redis Cache instance. "
      }
    }


<span data-ttu-id="bcd67-110">Il modello definisce i valori consentiti per questo parametro (0, 1, 2, 3, 4, 5 o 6) e assegna un valore predefinito (1) se non viene specificato alcun valore.</span><span class="sxs-lookup"><span data-stu-id="bcd67-110">The template defines the values that are permitted for this parameter (0, 1, 2, 3, 4, 5 or 6), and assigns a default value (1) if no value is specified.</span></span> <span data-ttu-id="bcd67-111">Questi numeri corrispondono alle dimensioni della cache seguenti: 0 = 250 MB, 1 = 1 GB, 2 = 2,5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span><span class="sxs-lookup"><span data-stu-id="bcd67-111">Those numbers correspond to following cache sizes: 0 = 250 MB, 1 = 1 GB, 2 = 2.5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span></span>

