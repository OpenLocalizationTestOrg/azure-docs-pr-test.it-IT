Una zona DNS è utilizzato toohost hello DNS record per un particolare dominio. toostart hosting del dominio DNS di Azure, è necessario toocreate una zona DNS per il nome di dominio. Ogni record DNS per il dominio viene quindi creato all'interno di questa zona DNS.

Ad esempio, hello dominio 'contoso.com' può contenere più record DNS, ad esempio 'mail.contoso.com' (per un server di posta elettronica) e 'www.contoso.com' (per un sito web).

Creazione di una zona DNS in DNS di Azure:

* nome Hello della zona hello deve essere univoco nel gruppo di risorse hello e zona hello non deve esistere già. Hello in caso contrario, l'operazione ha esito negativo.
* Hello stesso nome della zona può essere riutilizzata in un gruppo di risorse diverso o un'altra sottoscrizione di Azure.
* In più aree di condividano hello stesso nome, ogni istanza viene assegnato indirizzi server dei nomi diversi. Un solo set di indirizzi può essere configurato con nome di dominio di hello.

> [!NOTE]
> Non si dispone tooown un toocreate di nome di dominio una zona DNS con lo stesso nome di dominio in DNS di Azure. Tuttavia, è necessario tooown hello dominio tooconfigure hello Azure server dei nomi DNS come server dei nomi corretto per il nome di dominio hello con nome di dominio di hello hello.
> 
> Per ulteriori informazioni, vedere [tooAzure un dominio DNS delegato](../articles/dns/dns-domain-delegation.md).
