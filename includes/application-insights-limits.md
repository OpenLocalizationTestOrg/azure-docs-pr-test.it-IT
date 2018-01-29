Esistono alcuni limiti sul numero di metriche e eventi per applicazione (ovvero, per ogni chiave di strumentazione). I limiti dipendono dal [piano tariffario](https://azure.microsoft.com/pricing/details/application-insights/) scelto.

| **Risorsa** | **Limite predefinito** | **Nota**
| --- | --- | --- |
| Totale dati al giorno | 100 GB | È possibile ridurre i dati impostando un limite. Se è necessario più spazio, è possibile aumentare il limite fino a 1.000 GB dal portale. Per capacità superiori a 1.000 GB, inviare un messaggio di posta elettronica a AIDataCap@microsoft.com.
| Dati gratuiti al mese<br/> (piano tariffario base) | 1 GB | Vengono applicati addebiti per ogni gigabyte di dati aggiuntivi.
| Limitazione | 32.000 eventi/secondo | Il limite viene misurato nell'arco di un minuto.
| Conservazione dei dati | 90 giorni | Questa risorsa è destinata a [Ricerca](../articles/application-insights/app-insights-diagnostic-search.md), [Analisi](../articles/application-insights/app-insights-analytics.md) e [Esplora metriche](../articles/application-insights/app-insights-metrics-explorer.md).
| Conservazione dei risultati dettagliati di [test di disponibilità in più passi](../articles/application-insights/app-insights-monitor-web-app-availability.md#multi-step-web-tests) | 90 giorni | Questa risorsa fornisce risultati dettagliati per ogni passaggio.
| Dimensioni massime dell'evento | 64 K | 
| Lunghezza nomi di proprietà e metriche | 150 | Vedere gli [schemi per tipo](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/EndpointSpecs/Schemas/Docs/)
| Lunghezza stringa valore di proprietà | 8.192 | Vedere gli [schemi per tipo](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/EndpointSpecs/Schemas/Docs/)
| Lunghezza messaggio di traccia e di eccezione | 10.000 | Vedere gli [schemi per tipo](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/EndpointSpecs/Schemas/Docs/)
| Numero di [test di disponibilità](../articles/application-insights/app-insights-monitor-web-app-availability.md) per app  | 100 |
| Conservazione dati [profiler](../articles/application-insights/app-insights-profiler.md) | 5 giorni |
| Dati [profiler](../articles/application-insights/app-insights-profiler.md) inviati al giorno | 10 GB |

Per altre informazioni, vedere [Informazioni su prezzi e quote in Application Insights](../articles/application-insights/app-insights-pricing.md).

