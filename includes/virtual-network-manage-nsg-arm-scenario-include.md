## <a name="sample-scenario"></a>Scenario di esempio
toobetter viene illustrato come NSGs toomanage, in questo articolo viene utilizzato hello scenario riportato di seguito.

![Scenario di una rete virtuale](./media/virtual-networks-create-nsg-scenario-include/figure1.png)

In questo scenario verrà creato un gruppo per ogni subnet in hello **TestVNet** rete virtuale, come illustrato di seguito: 

* **NSG-FrontEnd**. Hello front-end di gruppo saranno applicata toohello *front-end* , subnet e contenere due regole:    
  * **regola-rdp**. Questa regola consente toohello il traffico RDP *front-end* subnet.
  * **regola-web**. Questa regola consente toohello il traffico HTTP *front-end* subnet.
* **Back-end di NSG**. back-end di Hello gruppo saranno applicata toohello *back-end* , subnet e contenere due regole:    
  * **regola sql**. Questa regola consente il traffico SQL solo da hello *front-end* subnet.
  * **regola-web**. Questa regola Nega tutte internet al traffico in uscita da hello *back-end* subnet.

combinazione Hello di queste regole creare uno scenario di tipo rete Perimetrale, in cui può solo ricevere il traffico in ingresso per il traffico SQL dalla subnet front-end hello subnet back-end hello e non ha toohello accesso Internet, mentre subnet front-end hello può comunicare con hello Internet e ricevere solo le richieste HTTP in ingresso.

scenario di hello toodeploy descritto in precedenza, seguire [questo collegamento](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), fare clic su **distribuire tooAzure**, sostituire i valori di parametro predefiniti hello se necessario e seguire le istruzioni di hello nel portale di hello. Le istruzioni di esempio seguente, il modello di hello hello è stato utilizzato toodeploy una risorsa i nomi dei gruppi **RG NSG**. 

