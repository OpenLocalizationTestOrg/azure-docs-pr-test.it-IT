
>[!NOTE]
>Log Analytics era noto in precedenza come Operational Insights.
>
>

Hello seguendo i limiti si applica le risorse Analitica tooLog per ogni sottoscrizione:

| Risorsa | Limite predefinito | Commenti
| --- | --- | --- |
| Numero di aree di lavoro gratuite per sottoscrizione | 10 | Non è possibile aumentare questo limite |
| Numero di aree di lavoro a pagamento per sottoscrizione | N/D | Sono limitati dal numero di hello delle risorse all'interno di un gruppo di risorse e numero di gruppi di risorse per ogni sottoscrizione | 


Hello seguendo i limiti si applica dell'area di lavoro di tooeach Analitica Log:

|  | Free | Standard | Premium | Autonoma | OMS |
| --- | --- | --- | --- | --- | --- |
| Volume di dati raccolti ogni giorno |500 MB<sup>1</sup> |None |None | None | Nessuno
| Periodo di conservazione dei dati |7 giorni |1 mese |12 mesi | 1 mese<sup>2</sup> | 1 mese <sup>2</sup>|

<sup>1</sup> quando i clienti raggiungono il limite di trasferimento dati giornaliero 500 MB, analisi dei dati viene arrestata e riprende all'inizio di hello di hello giorno successivo. Un giorno si basa su UTC.

<sup>2</sup> periodo di conservazione hello per hello autonomo e i piani tariffari OMS può essere maggiore di too730 giorni.

| Categoria | Limiti | Commenti
| --- | --- | --- |
| API dell'Agente di raccolta dati | La dimensione massima per un singolo post è di 30 MB<br>La dimensione massima per i valori dei campi è di 32 KB | Dividere i volumi più grandi in più post<br>I campi con una lunghezza superiore a 32 KB vengono troncati. |
| API di ricerca | 5000 record restituiti per i dati non aggregati<br>500000 record per i dati aggregati | I dati aggregati sono una ricerca che include hello `measure` comando
 
