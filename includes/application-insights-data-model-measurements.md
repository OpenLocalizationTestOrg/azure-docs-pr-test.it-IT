Raccolta di misure personalizzate. Utilizzare questo tooreport raccolta denominata misura associata a elemento di dati di telemetria hello. Casi d'uso tipici sono i seguenti:
- dimensione Hello del payload di dati di telemetria
- numero di Hello di elementi della coda elaborati da richiedere dati di telemetria
- tempo cliente ha toocomplete hello passaggio Completamento passaggio guidata dati di telemetria di eventi.

È possibile eseguire query sulle [misure personalizzate](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) in Analisi applicazione:

```
customEvents
| where customMeasurements != ""
| summarize avg(todouble(customMeasurements["Completion Time"]) * itemCount)
```

 > [!NOTE]
 > Misure personalizzate sono associate con elemento di dati di telemetria hello che appartengono. Oggetto toosampling con elemento di dati di telemetria hello contenente tali misure sono. una misura con un valore indipendente dagli altri tipi di dati di telemetria, utilizzare tootrack [telemetria metrica](../articles/application-insights/app-insights-api-custom-events-metrics.md).

Lunghezza massima della chiave: 150
