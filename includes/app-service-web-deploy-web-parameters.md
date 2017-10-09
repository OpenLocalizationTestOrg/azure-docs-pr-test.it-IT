Con Gestione risorse di Azure, si definiscono i parametri per i valori si desidera toospecify quando viene distribuito il modello di hello. modello Hello include una sezione denominata parametri che contiene tutti i valori di parametro hello.
È necessario definire un parametro per i valori che variano in base progetto hello che si distribuisce o Hello che si distribuisce ambiente di hello. Non definire parametri per i valori che saranno sempre hello stesso. Ogni valore del parametro viene utilizzato in hello modello toodefine hello le risorse distribuite. 

Quando si definiscono i parametri, utilizzare hello **allowedValues** toospecify campo che i valori di un utente può fornire durante la distribuzione. Hello utilizzare **defaultValue** campo tooassign un parametro di valore toohello, se viene fornito alcun valore durante la distribuzione.

Si descrive ogni parametro di modello hello.

### <a name="sitename"></a>siteName
nome Hello di hello web app che si desidera toocreate.

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a>hostingPlanName
nome Hello del servizio App hello pianificare toouse per l'hosting hello web app.

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a>sku
Hello piano tariffario per hello piano di hosting.

    "sku": {
      "type": "string",
      "allowedValues": [
        "F1",
        "D1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3",
        "P1",
        "P2",
        "P3",
        "P4"
      ],
      "defaultValue": "S1",
      "metadata": {
        "description": "hello pricing tier for hello hosting plan."
      }
    }

modello Hello definisce i valori consentiti per questo parametro hello e assegna un valore predefinito (S1) se viene specificato alcun valore.

### <a name="workersize"></a>workerSize
dimensioni delle istanze Hello di hello (piccola, Media o grande) di piano di hosting.

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

modello Hello definisce i valori hello consentiti per questo parametro (0, 1 o 2) e assegna un valore predefinito (0) se viene specificato alcun valore. i valori Hello corrispondono toosmall, medie e grandi dimensioni.

