## <a name="scenario"></a>Scenario
toobetter viene illustrato come UDRs toocreate, questo documento verrà utilizzato uno scenario di hello riportato di seguito.

![DESCRIZIONE DELL’IMMAGINE](./media/virtual-network-create-udr-scenario-include/figure1.png)

In questo scenario si creerà un UDR per hello *subnet di Front end* UDR un'altra per hello e *subnet di Back end* , come descritto di seguito: 

* **UDR-FrontEnd**. Hello front-end UDR sarà applicato toohello *front-end* , subnet e contenere una route:    
  * **RouteToBackend**. Questa route invia tutto il traffico toohello back-end subnet toohello **FW1** macchina virtuale.
* **Back-end di UDR**. back-end di Hello UDR sarà applicato toohello *back-end* , subnet e contenere una route:    
  * **RouteToFrontend**. Questa route invia tutto il traffico toohello front-end subnet toohello **FW1** macchina virtuale.

combinazione di Hello di queste route garantisce che tutto il traffico destinato da una subnet tooanother indirizzato toohello **FW1** macchina virtuale, in cui viene utilizzata come appliance virtuale. È inoltre necessario tooturn in inoltro dell'indirizzo IP per la macchina virtuale, tooensure può ricevere il traffico destinato a macchine virtuali tooother.

