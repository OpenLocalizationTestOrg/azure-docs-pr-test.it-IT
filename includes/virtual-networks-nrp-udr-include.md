## <a name="route-tables"></a>Tabelle di route
Risorse tabella route contiene le route utilizzate toodefine come flussi di traffico all'interno dell'infrastruttura di Azure. È possibile utilizzare toosend route (UDR) definito dall'utente tutto il traffico da un determinata subnet tooa dispositivo virtuale, ad esempio un sistema di rilevamento delle intrusioni o di firewall (ID). È possibile associare un toosubnets tabella di route. 

Tabelle di route contengono hello le proprietà seguenti.

| Proprietà | Descrizione | Valori di esempio |
| --- | --- | --- |
| **routes** |Raccolta di utenti definiti route nella tabella di route hello |vedere [route definite dall'utente](#User-defined-routes) |
| **subnet** |Raccolta della tabella di routing hello subnet viene applicata troppo|vedere [subnet](#Subnets) |

### <a name="user-defined-routes"></a>route definite dall'utente
È possibile creare toospecify UDRs cui traffico deve essere inviato, in base al relativo indirizzo di destinazione. È possibile considerare una route come definizione del gateway predefinito hello basate sull'indirizzo di destinazione hello di un pacchetto di rete.

UDRs contengono hello le proprietà seguenti. 

| Proprietà | Descrizione | Valori di esempio |
| --- | --- | --- |
| **addressPrefix** |Prefisso dell'indirizzo o indirizzo IP completo per la destinazione di hello |192.168.1.0/24, 192.168.1.101 |
| **nextHopType** |Tipo di dispositivo hello traffico verrà inviato troppo|VirtualAppliance, Gateway VPN, Internet |
| **nextHopIpAddress** |Indirizzo IP dell'hop successivo hello |192.168.1.4 |

Tabella di route di esempio in formato JSON:

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a>Risorse aggiuntive
* Altre informazioni sulle [route definite dall'utente](../articles/virtual-network/virtual-networks-udr-overview.md).
* Hello lettura [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt502549.aspx) per le tabelle di route.
* Hello lettura [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt502539.aspx) per l'utente definito route (UDRs).

