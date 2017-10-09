## <a name="virtual-network"></a>Rete virtuale
Le reti virtuali e le risorse subnet consentono di definire un limite di sicurezza per i carichi di lavoro in esecuzione in Azure. Una rete virtuale è caratterizzata da una raccolta di spazi di indirizzi, definiti come blocchi CIDR. 

> [!NOTE]
> Gli amministratori di rete hanno familiarità con la notazione CIDR. Se non si ha familiarità con CIDR, è possibile [ottenere maggiori informazioni](http://whatismyipaddress.com/cidr).
> 
> 

![Reti virtuali con più subnet](./media/resource-groups-networking/Figure4.png)

Le reti virtuali contengono hello le proprietà seguenti.

| Proprietà | Descrizione | Valori di esempio |
| --- | --- | --- |
| **addressSpace** |Raccolta di prefissi di indirizzo che costituiscono hello rete virtuale nella notazione CIDR |192.168.0.0/16 |
| **subnet** |Raccolta di subnet che costituiscono hello rete virtuale |vedere [subnet](#Subnets) di seguito. |
| **ipAddress** |Indirizzo IP assegnato tooobject. La proprietà è di sola lettura. |104.42.233.77 |

### <a name="subnets"></a>Subnet
Una subnet è una risorsa figlio di una rete virtuale e consente di definire i segmenti degli spazi di indirizzi all'interno di un blocco CIDR, usando i prefissi degli indirizzi IP. Schede di rete possono essere aggiunte toosubnets e tooVMs connesso, fornisce la connettività per diversi carichi di lavoro.

Subnet contengono hello le proprietà seguenti. 

| Proprietà | Descrizione | Valori di esempio |
| --- | --- | --- |
| **addressPrefix** |Singolo prefisso di indirizzo di subnet hello in notazione CIDR |192.168.1.0/24 |
| **networkSecurityGroup** |Subnet toohello NSG applicato |vedere [NSG](#Network-Security-Group) |
| **routeTable** |Tabella di route applicato toohello subnet |vedere [UDR](#Route-table) |
| **ipConfigurations** |Raccolta di oggetti di configurazione IP usati da schede di rete connessa toohello subnet |vedere [UDR](#Route-table) |

Rete virtuale di esempio in formato JSON:

    {
        "name": "TestVNet",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/virtualNetworks",
        "location": "westus",
        "tags": {
            "displayName": "VNet"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "addressSpace": {
                "addressPrefixes": [
                    "192.168.0.0/16"
                ]
            },
            "subnets": [
                {
                    "name": "FrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "networkSecurityGroup": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "routeTable": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                        },
                        "ipConfigurations": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                            },
                            ...]
                    }
                },
                ...]
        }
    }

### <a name="additional-resources"></a>Risorse aggiuntive
* Altre informazioni sulle [reti virtuali](../articles/virtual-network/virtual-networks-overview.md).
* Hello lettura [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt163650.aspx) per le reti virtuali.
* Hello lettura [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt163618.aspx) per subnet.

