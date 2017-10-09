## <a name="scenario"></a>Scenario
toobetter illustrare come toocreate una rete virtuale e le subnet, in questo documento verrà utilizzato uno scenario di hello riportato di seguito.

![Scenario di una rete virtuale](./media/virtual-networks-create-vnet-scenario-include/vnet-scenario.png)

In questo scenario verrà creata una rete virtuale denominata **TestVNet** con blocco CIDR riservato **192.168.0.0./16**. La rete virtuale conterrà hello seguenti subnet: 

* **FrontEnd**, che usa **192.168.1.0/24** come blocco CIDR.
* **BackEnd**, che usa **192.168.2.0/24** come blocco CIDR.

