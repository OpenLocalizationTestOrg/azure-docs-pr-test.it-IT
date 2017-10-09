## <a name="incremental-and-complete-deployments"></a>Distribuzioni incrementali e complete
Quando si distribuisce le risorse, specificare che la distribuzione di hello è un aggiornamento incrementale o un aggiornamento completo. Hello principale differenza tra queste due modalità è come Gestione risorse gestisce le risorse esistenti nel gruppo di risorse hello che non sono presenti nel modello hello:

* In modalità completa, gestione delle risorse **Elimina** le risorse che esisterebbero nel gruppo di risorse hello ma non sono specificate nel modello di hello. 
* In modalità incrementale, Gestione risorse **lascia invariato** le risorse che esisterebbero nel gruppo di risorse hello ma non sono specificate nel modello di hello.

Per entrambe le modalità, Gestione risorse tenta tooprovision tutte le risorse specificate nel modello di hello. Se la risorsa hello esiste già nel gruppo di risorse hello e le relative impostazioni sono identiche, operazione hello comporta alcuna modifica. Se si modificano le impostazioni di hello per una risorsa, viene eseguito il provisioning di risorse hello con le nuove impostazioni. Se si tenta di percorso hello tooupdate o un tipo di una risorsa esistente, la distribuzione di hello genera un errore. In alternativa, distribuire una nuova risorsa con il percorso di hello o digitare che è necessario.

Per impostazione predefinita, Gestione risorse Usa modalità incrementale hello.

differenza hello tooillustrate tra le modalità incrementale e completa, prendere in considerazione hello seguente scenario.

Il **gruppo di risorse esistente** contiene:

* Risorsa A
* Risorsa B
* Risorsa C

Il **modello** definisce:

* Risorsa A
* Risorsa B
* Risorsa D

Quando vengono distribuiti in **incrementale** modalità gruppo di risorse hello contiene:

* Risorsa A
* Risorsa B
* Risorsa C
* Risorsa D

Quando viene implementato in modalità **completa**, la risorsa C viene eliminata. il gruppo di risorse di Hello contiene:

* Risorsa A
* Risorsa B
* Risorsa D
