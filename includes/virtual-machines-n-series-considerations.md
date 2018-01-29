## <a name="deployment-considerations"></a>Considerazioni sulla distribuzione

* Per la disponibilità delle VM serie N, vedere [Prodotti disponibili in base all'area](https://azure.microsoft.com/en-us/regions/services/).

* Le VM serie N possono essere distribuite solo nel modello di distribuzione Resource Manager.

* Quando si crea una VM serie N usando il portale di Azure, nel pannello **Informazioni di base** in **Tipo di disco della macchina virtuale** selezionare **HDD**. Per scegliere una dimensione serie N disponibile, nel pannello **Dimensioni** fare clic su **Visualizza tutto**.

* Contesto dei nomi e le macchine virtuali non Volatile non supportano i dischi di macchina virtuale sono supportati da archiviazione Premium di Azure.

* Per distribuire numerose VM serie N, prendere in considerazione una sottoscrizione con pagamento in base al consumo o altre opzioni di acquisto. Con un [account gratuito di Azure](https://azure.microsoft.com/free/)è possibile usare solo un numero limitato di core di calcolo di Azure.

* Potrebbe essere necessario aumentare la quota di core nella sottoscrizione di Azure (regione) e aumentare la quota separata per core NC, NCv2, ND o Volatile. Per richiedere un aumento della quota, è possibile [aprire una richiesta di assistenza clienti online](../articles/azure-supportability/how-to-create-azure-support-request.md) senza alcun addebito. I limiti predefiniti possono variare in base alla categoria della sottoscrizione.

* Un'immagine VM che è possibile distribuire nelle VM serie N è la [macchina virtuale per l'analisi scientifica dei dati di Azure](../articles/machine-learning/data-science-virtual-machine/overview.md). La macchina virtuale per l'analisi scientifica dei dati preinstalla e configura numerosi strumenti comuni per l'analisi scientifica dei dati e l'apprendimento avanzato. Inoltre viene preinstallato dal driver NVIDIA Tesla GPU.





