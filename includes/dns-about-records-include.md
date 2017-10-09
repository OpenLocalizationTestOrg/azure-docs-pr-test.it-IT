### <a name="record-names"></a>Nomi dei record

Nel servizio DNS di Azure i record vengono specificati usando nomi relativi. Oggetto *completo* il nome di dominio (FQDN) include nome della zona hello, mentre un *relativo* non nome. Ad esempio, nome del record relativo hello 'www' nell'area di hello 'contoso.com' assegna il nome di un record completo hello 'www.contoso.com'.

Un *apice* record è un record DNS radice hello (o *apice*) di una zona DNS. Ad esempio, in hello DNS zona 'contoso.com', un record di apice include anche il nome completo di hello 'contoso.com' (talvolta detta un *naked* dominio).  Per convenzione, hello nome relativo ' @' è utilizzato toorepresent record vertice.

### <a name="record-types"></a>Tipi di record

Ogni record DNS ha un nome e un tipo. I record sono organizzati in vari tipi di base toohello dati in che essi contenuti. tipo più comune di Hello è un record 'A', che esegue il mapping di un indirizzo IPv4 di tooan nome. Un altro tipo comune è un record 'MX', che esegue il mapping di un server di posta elettronica tooa nome.

DNS di Azure supporta tutti i tipi di record DNS comuni: A, AAAA, CNAME, MX, NS, PTR, SOA, SRV e TXT. Si noti che i [record SPF vengono rappresentati usando record TXT](../articles/dns/dns-zones-records.md#spf-records).

### <a name="record-sets"></a>Set di record

Talvolta è necessario toocreate più di un record DNS con un nome e tipo specificati. Si supponga, ad esempio, sito web di 'www.contoso.com' hello è ospitato in due diversi indirizzi IP. sito Web di Hello due diversi richiede un record, uno per ogni indirizzo IP. Ecco un esempio di un set di record:

    www.contoso.com.        3600    IN    A    134.170.185.46
    www.contoso.com.        3600    IN    A    134.170.188.221

DNS di Azure gestisce tutti i record DNS usando *set di record*. Un set di record (noto anche come un *risorse* set di record) è hello raccolta dei record DNS in una zona con hello stesso nome e sono di hello stesso tipo. La maggior parte dei set di record contiene un singolo record. Tuttavia, esempi di hello in precedenza, in cui un set di record contiene più di un record, non sono comuni.

Ad esempio, si supponga che un record A 'www' è già stato creato nella zona hello 'contoso.com', che punta toohello IP indirizzi '134.170.185.46' (hello primo record precedente).  toocreate hello secondo record aggiungere tale record come record esistente toohello impostato, anziché creare un set di record aggiuntivi.

Hello SOA e tipi di record CNAME sono eccezioni. standard DNS Hello non consentono di utilizzare più record con stesso nome per questi tipi di hello, pertanto questi set di record può contenere solo un singolo record.
