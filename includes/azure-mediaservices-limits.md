>[!NOTE]
>Per le risorse che non sono corretti, è possibile chiedere che hello quote toobe generato, aprendo un ticket di supporto. Eseguire **non** creare altri account di servizi multimediali di Azure nel tentativo limiti più elevati tooobtain.

| Risorsa | Limite predefinito | 
| --- | --- | 
| Account di Servizi multimediali di Azure in una singola sottoscrizione | 25 (fisso) |
| Unità riservate multimediali per account AMS |25 (S1, S2)<br/>10 (S3) <sup>(1)</sup> | 
| Processi per ogni account di Servizi multimediali di Azure | 50.000<sup>(2)</sup> |
| Attività concatenate per processo | 30 (fisso) |
| Asset per ogni account di Servizi multimediali di Azure | 1.000.000|
| Asset per attività | 50 |
| Asset per processo | 100 |
| Localizzatori univoci associati a un asset contemporaneamente | 5<sup>(4)</sup> |
| Canali live per ogni account AMS  |5|
| Programmi con stato arrestato per canale  |50|
| Programmi con stato in esecuzione per canale  |3|
| Endpoint di streaming con stato in esecuzione per ogni account AMS |2|
| Unità di streaming per endpoint di streaming  |10 |
| Account di archiviazione | 1.000<sup>(5)</sup> (fisso) |
| Criteri | 1.000.000<sup>(6)</sup> |
| Dimensioni complete| In alcuni scenari è previsto un limite alle dimensioni massime del file hello è supportata per l'elaborazione in servizi multimediali. <sup>7</sup> |
  
<sup>1</sup> Le unità riservate S3 non sono disponibili in India occidentale. limiti RU max Hello reimpostati se cliente hello Cambia tipo di hello (ad esempio, da tooS1 S2). 

<sup>2</sup> Questo numero include i processi in coda, terminati, attivi e annullati. Non include invece i processi eliminati. È possibile eliminare i processi di hello precedente mediante **IJob.Delete** o hello **eliminare** richiesta HTTP.

A partire dal 1 aprile 2017, qualsiasi record di processo più vecchi di 90 giorni account vengono eliminate automaticamente, insieme ai relativi record di attività associato, anche se il numero di record hello sotto la quota massima di hello. Se sono necessarie informazioni di processi/attività hello tooarchive, è possibile utilizzare codice hello descritto [qui](../articles/media-services/media-services-dotnet-manage-entities.md).

<sup>3</sup> quando si effettua una richiesta di entità Job toolist, verrà restituito un massimo di 1.000 per ogni richiesta. Se è necessario tookeep traccia di tutti i processi inviati, come descritto in, è possibile utilizzare top/skip [opzioni di query di sistema OData](http://msdn.microsoft.com/library/gg309461.aspx).

<sup>4</sup> I localizzatori non sono progettati per gestire il controllo di accesso per utente. toogive gli utenti tooindividual diritti di accesso diverso, usare le soluzioni di Digital Rights Management (DRM). Per altre informazioni, vedere [questa](../articles/media-services/media-services-content-protection-overview.md) sezione.

<sup>5</sup> gli account di archiviazione hello devono essere compreso hello stessa sottoscrizione di Azure.

<sup>6</sup> È previsto un limite di 1.000.000 criteri per i diversi criteri di servizi multimediali di Azure (ad esempio, per i criteri Locator o ContentKeyAuthorizationPolicy). 

>[!NOTE]
> È consigliabile utilizzare hello stesso ID di criteri, se si utilizza sempre hello stesso giorni / le autorizzazioni di accesso e così via. Per informazioni e un esempio, vedere [questa](../articles/media-services/media-services-dotnet-manage-entities.md#limit-access-policies) sezione.

<sup>7</sup>se si sta caricando contenuto tooan le risorse multimediali di Azure servizi con tooprocess preventivo hello con uno dei processori di contenuti multimediali hello in servizio (ad esempio codificatori come motori Media Encoder Standard e flusso di lavoro Premium del codificatore multimediale o analisi come tipo di carattere Rilevatore), quindi è necessario essere consapevoli del vincolo hello sulla dimensione massima di hello. 

A partire da 15 maggio 2017, dimensione massima di hello è supportato per un singolo blob è 195 TB - con largers file superiore al limite specificato, l'attività avrà esito negativo. Stiamo lavorando tooaddress una correzione di questo limite. Inoltre, hello vincolo sulla dimensione massima di hello di hello Asset è come indicato di seguito.

| Unità riservata multimediale | Dimensioni massime input (GB)| 
| --- | --- | 
|S1 | 325|
|S2 | 640|
|S3 | 260|
