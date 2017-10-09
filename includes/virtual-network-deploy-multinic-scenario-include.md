## <a name="scenario"></a>Scenario
In questo documento verrà illustrata una distribuzione che usa più schede di rete nelle macchine virtuali in uno scenario specifico. In questo scenario, si ha a disposizione un carico di lavoro IaaS a due livelli ospitato in Azure. Ogni livello viene distribuito nella propria subnet in una rete virtuale (VNet). livello front end Hello è composta da più server web, raggruppati in un bilanciamento del carico impostato per la disponibilità elevata. livello di back-end Hello è composta da più server di database. Questi server di database verrà distribuito con due schede di rete, uno per l'accesso al database, altri hello per la gestione. scenario di Hello include anche rete sicurezza gruppi toocontrol il traffico è consentito nella distribuzione hello tooeach subnet e NIC. Figura Hello seguente mostra l'architettura di base di hello di questo scenario.  

![Scenario MultiNIC](./media/virtual-network-deploy-multinic-scenario-include/Figure1.png)

