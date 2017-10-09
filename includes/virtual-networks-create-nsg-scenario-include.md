## <a name="scenario"></a>Scenario
toobetter viene illustrato come NSGs toocreate, questo documento verrà utilizzato uno scenario di hello riportato di seguito.

![Scenario di una rete virtuale](./media/virtual-networks-create-nsg-scenario-include/figure1.png)

In questo scenario verrà creato un gruppo per ogni subnet in hello **TestVNet** rete virtuale, come illustrato di seguito: 

* **NSG-FrontEnd**. Hello front-end di gruppo saranno applicata toohello *front-end* , subnet e contenere due regole:    
  * **regola-rdp**. Questa regola consente toohello il traffico RDP *front-end* subnet.
  * **regola-web**. Questa regola consente toohello il traffico HTTP *front-end* subnet.
* **Back-end di NSG**. back-end di Hello gruppo saranno applicata toohello *back-end* , subnet e contenere due regole:    
  * **regola sql**. Questa regola consente il traffico SQL solo da hello *front-end* subnet.
  * **regola-web**. Questa regola Nega tutte internet al traffico in uscita da hello *back-end* subnet.

combinazione di queste regole Hello creare uno scenario simile rete Perimetrale, dove subnet back-end hello può solo ricevere il traffico in ingresso per SQL dalla subnet front-end hello e non ha toohello accesso Internet, mentre subnet front-end hello può comunicare con Internet hello, e ricevere solo le richieste HTTP in ingresso.

