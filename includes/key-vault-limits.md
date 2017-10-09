Transazioni chiave (transazioni max consentite entro 10 secondi, per ogni insieme di credenziali e per ogni area<sup>1</sup>):

|Tipo di chiave|Chiave HSM<br>Chiave CREATE|Chiave HSM<br>Tutte le altre transazioni|Chiave software<br>Chiave CREATE|Chiave software<br>Tutte le altre transazioni|
|:---|---:|---:|---:|---:|
|RSA a 2048 bit|5|1000|10|2000|
|RSA a 3072 bit|5|250|10|500|
|RSA a 4096 bit|5|125|10|250|
|

Segreti, chiavi di account di archiviazione gestiti e transazioni dell'insieme di credenziali:
| Tipo di transazioni | Transazioni max consentite entro 10 secondi, per ogni archivio per ogni area<sup>1</sup> |
| --- | --- |
| Tutte le transazioni |2000 |
|

<sup>1</sup> La sottoscrizione prevede un limite globale per tutti i tipi di transazione, ovvero un valore 5 volte superiore al limite dell'insieme di credenziali delle chiavi. Ad esempio, HSM - altre transazioni per ogni sottoscrizione sono transazioni too5000 limitato entro 10 secondi per ogni sottoscrizione.
