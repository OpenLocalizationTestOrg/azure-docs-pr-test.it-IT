## <a name="nic"></a>NIC
Una risorsa di scheda di interfaccia rete fornisce una subnet esistente tooan connettività di rete in una risorsa di rete virtuale. Sebbene sia possibile creare una scheda di rete come oggetto autonomo, è necessario tooassociate è tooanother oggetto tooactually fornisce la connettività. Una scheda di rete può essere utilizzato tooconnect tooa subnet VM, un indirizzo IP pubblico o un servizio di bilanciamento del carico.  

| Proprietà | Descrizione | Valori di esempio |
| --- | --- | --- |
| **virtualMachine** |Hello VM NIC è associato. |/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1 |
| **macAddress** |Indirizzo MAC per hello NIC |qualsiasi valore compreso tra 4 e 30. |
| **networkSecurityGroup** |Toohello associata gruppo NIC |/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1 |
| **dnsSettings** |Impostazioni DNS per hello NIC |vedere [PIP](#Public-IP-address) |

Una scheda di interfaccia di rete o scheda di rete, rappresenta un'interfaccia di rete che può essere associati tooa virtual machine (VM). Una macchina virtuale può avere una o più schede di interfaccia di rete.

![Scheda di interfaccia di rete in una macchina virtuale singola](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a>Configurazioni IP
Schede di rete dispone di un oggetto figlio denominato **configurazioni IP** contenente hello le proprietà seguenti:

| Proprietà | Descrizione | Valori di esempio |
| --- | --- | --- |
| **subnet** |Hello subnet scheda di rete è connessa a. |/Subscriptions/{GUID}/../microsoft.Network/virtualNetworks/myvnet1/Subnets/mysub1 |
| **privateIPAddress** |Indirizzo IP per subnet hello Ciao NIC |10.0.0.8 |
| **privateIPAllocationMethod** |Metodo di allocazione degli indirizzi IP |Dinamico o statico |
| **enableIPForwarding** |Se è possibile utilizzare per il routing hello NIC |true o false |
| **primary** |Se è hello NIC hello schede di rete primaria per hello VM |true o false |
| **publicIPAddress** |PIP associato hello NIC |vedere [Impostazioni DNS](#DNS-settings) |
| **loadBalancerBackendAddressPools** |Eseguire il backup hello pool di indirizzi fine A che NIC è associata | |
| **loadBalancerInboundNatRules** |Connessioni in entrata hello regole NAT bilanciamento di carico A che NIC è associata | |

Indirizzo IP pubblico di esempio in formato JSON:

    {
        "name": "lb-nic1-be",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkInterfaces",
        "location": "eastus",
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "ipConfigurations": [
                {
                    "name": "NIC-config",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/NIC-config",
                    "etag": "W/\"0027f1a2-3ac8-49de-b5d5-fd46550500b1\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "privateIPAddress": "10.0.0.4",
                        "privateIPAllocationMethod": "Dynamic",
                        "subnet": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet"
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1"
                            }
                        ]
                    }
                }
            ],
            "dnsSettings": { ... },
            "macAddress": "00-0D-3A-10-F1-29",
            "enableIPForwarding": false,
            "primary": true,
            "virtualMachine": {
                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Compute/virtualMachines/web1"
            }
        }
    }

### <a name="additional-resources"></a>Risorse aggiuntive
* Hello lettura [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt163579.aspx) per schede di rete.

