## <a name="deployment-considerations"></a>Considerazioni sulla distribuzione

* Per la disponibilità delle VM serie N, vedere [Prodotti disponibili in base all'area](https://azure.microsoft.com/en-us/regions/services/).

* Macchine virtuali serie N possono essere distribuite solo nel modello di distribuzione di gestione risorse di hello.

* Quando la creazione di una macchina virtuale della serie N usando hello portale Azure hello **nozioni di base** pannello, seleziona un **il tipo di disco di macchina virtuale** di **HDD**. dimensioni di una serie di N disponibile toochoose, su hello **dimensioni** pannello, fare clic su **visualizzare tutti**.

* Le VM serie N non supportano i dischi di VM supportati da Archiviazione Premium di Azure.

* Se si desidera toodeploy più macchine virtuali di serie di N, prendere in considerazione una sottoscrizione prepagata o altre opzioni di acquisto. Con un [account gratuito di Azure](https://azure.microsoft.com/free/)è possibile usare solo un numero limitato di core di calcolo di Azure.

* Si potrebbe essere necessario quota di core hello tooincrease (regione) nella sottoscrizione di Azure e aumentare la quota di separato hello per NC o NV Core. aumentare la quota toorequest, [aprire una richiesta di supporto clienti online](../articles/azure-supportability/how-to-create-azure-support-request.md) senza alcun costo. I limiti predefiniti possono variare in base alla categoria della sottoscrizione.

* Un'immagine di macchina virtuale, è possibile distribuire in macchine virtuali serie N è hello [macchina virtuale di analisi scientifica dei dati di Azure](../articles/machine-learning/machine-learning-data-science-virtual-machine-overview.md). Hello macchina virtuale di analisi scientifica dei dati viene preinstallato dal e configura molti analisi scientifica dei dati comuni e completo di strumenti di apprendimento. Preinstalla anche i driver GPU NVIDIA Tesla per le istanze NC.





