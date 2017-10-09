## <a name="scenario"></a>Scenario
Una macchina virtuale con una singola scheda di rete viene creato e connesso tooa rete virtuale. Hello VM richiede tre diverse *privata* IP indirizzi e due *pubblica* gli indirizzi IP. gli indirizzi IP Hello assegnati toohello seguendo le configurazioni IP:

* **IPConfig-1:** assegna un indirizzo IP privato *statico* e un indirizzo IP pubblico *statico*.
* **IPConfig-2:** assegna un indirizzo IP privato *statico* e un indirizzo IP pubblico *statico*.
* **IPConfig-3:** assegna un indirizzo IP privato *statico* e nessun indirizzo IP pubblico.
  
    ![Più indirizzi IP](./media/virtual-network-multiple-ip-addresses-scenario/multiple-ipconfigs.png)

le configurazioni IP Hello sono associato toohello NIC quando hello NIC viene creato e hello NIC non è collegato toohello VM hello macchina virtuale viene creato. tipi di Hello di indirizzi IP utilizzati per uno scenario di hello sono a scopo illustrativo. È possibile assegnare qualsiasi tipo di assegnazione e indirizzo IP desiderato.

> [!NOTE]
> Anche se hello i passaggi questo articolo assegna tutti tooa di configurazioni IP singola scheda di rete, è inoltre possibile assegnare più tooany di configurazioni IP NIC in una macchina virtuale multi-NIC. modalità di lettura di una macchina virtuale con più schede di rete, toocreate toolearn hello [creare una macchina virtuale con più schede di rete](../articles/virtual-network/virtual-network-deploy-multinic-arm-ps.md) articolo.
