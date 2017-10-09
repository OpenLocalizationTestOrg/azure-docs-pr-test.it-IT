## <a name="network-security-group"></a>Gruppo di sicurezza di rete
Una risorsa di gruppo consente la creazione di hello del limite di sicurezza per i carichi di lavoro, implementando consentire e le regole di negazione. Tali regole possono essere applicati tooa macchina virtuale, una scheda di rete o subnet.

| Proprietà | Descrizione | Valori di esempio |
| --- | --- | --- |
| **subnet** |Elenco di ID di subnet hello gruppo viene applicato a. |/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd |
| **securityRules** |Elenco di regole di sicurezza che costituiscono hello NSG |Vedere [Regola di sicurezza](#Security-rule) di seguito |
| **defaultSecurityRules** |Elenco delle regole di sicurezza predefinite presenti in ogni gruppo di sicurezza di rete |Vedere [Regole di sicurezza predefinite](#Default-security-rules) di seguito |

* **Regola di sicurezza** : in un gruppo di sicurezza di rete possono essere definite più regole di sicurezza. Ogni regola può consentire o negare diversi tipi di traffico.

### <a name="security-rule"></a>Regola di sicurezza
Una regola di sicurezza è una risorsa figlio di un gruppo che contiene proprietà hello riportato di seguito.

| Proprietà | Descrizione | Valori di esempio |
| --- | --- | --- |
| **description** |Descrizione della regola hello |Consentire il traffico in ingresso per tutte le macchine virtuali nella subnet X |
| **protocol** |Protocollo toomatch per regola hello |TCP, UDP o * |
| **sourcePortRange** |Toomatch intervallo porte di origine per la regola hello |80, 100-200, * |
| **destinationPortRange** |Toomatch intervallo porte di destinazione per la regola hello |80, 100-200, * |
| **sourceAddressPrefix** |Toomatch di prefisso di indirizzo di origine per la regola hello |10.10.10.1, 10.10.10.0/24, VirtualNetwork |
| **destinationAddressPrefix** |Toomatch di prefisso di indirizzo di destinazione per la regola hello |10.10.10.1, 10.10.10.0/24, VirtualNetwork |
| **direction** |Direzione del traffico toomatch per regola hello |in ingresso o in uscita |
| **priority** |Priorità per la regola di hello. Le regole vengono controllate nell'ordine di priorità. Una volta che viene applicata una regola, non viene verificata la corrispondenza di altre regole. |10, 100, 65000 |
| **access** |Tipo di accesso tooapply se hello regola corrispondente |consentire o negare |

Gruppo di sicurezza di rete di esempio in formato JSON:

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a>Regole di sicurezza predefinite

Regole di sicurezza predefinite sono hello stesse proprietà disponibili nelle regole di sicurezza. Connettività di base tra le risorse che hanno applicato NSGs toothem tooprovide esistenti. Assicurarsi di conoscere le [regole di sicurezza predefinite](../articles/virtual-network/virtual-networks-nsg.md#default-rules) esistenti.

### <a name="additional-resources"></a>Risorse aggiuntive
* Altre informazioni sui [gruppi di sicurezza di rete](../articles/virtual-network/virtual-networks-nsg.md).
* Hello lettura [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt163615.aspx) per NSGs.
* Hello lettura [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt163580.aspx) per le regole di sicurezza.
