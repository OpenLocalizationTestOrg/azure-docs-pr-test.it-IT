## <a name="public-ip-address"></a>Indirizzo IP pubblico
Una risorsa di indirizzo IP pubblico fornisce un indirizzo IP pubblico con connessione a internet riservato o dinamico. Sebbene sia possibile creare un indirizzo IP pubblico come oggetto autonomo, è necessario tooassociate è tooanother oggetto tooactually utilizzare indirizzo hello. È possibile associare un bilanciamento del carico tooa indirizzo IP pubblico, gateway applicazione o una scheda di rete tooprovide Internet accedere toothose alle risorse.  

| Proprietà | Descrizione | Valori di esempio |
| --- | --- | --- |
| **publicIPAllocationMethod** |Definisce se l'indirizzo IP hello è *statico* o *dinamica*. |statico, dinamico |
| **idleTimeoutInMinutes** |Definisce hello timeout di inattività, con un valore predefinito di 4 minuti. Se non più pacchetti per una determinata sessione viene ricevuto entro questo intervallo, hello sessione terminata. |qualsiasi valore compreso tra 4 e 30. |
| **ipAddress** |Indirizzo IP assegnato tooobject. La proprietà è di sola lettura. |104.42.233.77 |

### <a name="dns-settings"></a>Impostazioni DNS
Gli indirizzi IP pubblici dispongono di un oggetto figlio denominato **dnsSettings** contenente hello le proprietà seguenti:

| Proprietà | Descrizione | Valori di esempio |
| --- | --- | --- |
| **domainNameLabel** |Host denominato utilizzato per la risoluzione dei nomi. |www, ftp, vm1 |
| **fqdn** |Nome completo per l'IP pubblico hello. |www.westus.cloudapp.azure.com |
| **reverseFqdn** |Nome di dominio completo che consente di risolvere l'indirizzo IP toohello e viene registrato in DNS come un record PTR. |www.contoso.com |

Indirizzo IP pubblico di esempio in formato JSON:

    {
       "name": "PIP01",
       "location": "North US",
       "tags": { "key": "value" },
       "properties": {
          "publicIPAllocationMethod": "Static",
          "idleTimeoutInMinutes": 4,
          "ipAddress": "104.42.233.77",
          "dnsSettings": {
             "domainNameLabel": "mylabel",
             "fqdn": "mylabel.westus.cloudapp.azure.com",
             "reverseFqdn": "contoso.com."
          }
       }
    } 

### <a name="additional-resources"></a>Risorse aggiuntive
* Ottenere ulteriori informazioni sugli [indirizzi IP pubblici](../articles/virtual-network/virtual-networks-reserved-public-ip.md).
* Informazioni sugli [indirizzi IP pubblici a livello di istanza](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).
* Hello lettura [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt163638.aspx) per indirizzo IP pubblico indirizzi.

