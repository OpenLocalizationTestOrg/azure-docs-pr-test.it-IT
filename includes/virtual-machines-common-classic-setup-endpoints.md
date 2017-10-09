
Ogni endpoint ha una *porta pubblica* e una *porta privata*:

* porta pubblica Hello viene utilizzata da toolisten di bilanciamento carico di Azure hello per macchina di virtuale toohello traffico in ingresso da hello Internet.
* porta privata Hello viene utilizzata da hello toolisten di macchina virtuale per il traffico in ingresso, applicazione tooan destinati in genere o il servizio in esecuzione nella macchina virtuale hello.

I valori predefiniti per hello protocollo IP e porte TCP o UDP per i protocolli di rete noti vengono fornite quando si crea l'endpoint con hello portale di Azure. Per gli endpoint personalizzati, è necessario toospecify hello corretto indirizzo IP (TCP o UDP) e porte pubbliche e private hello. toodistribute il traffico in ingresso in modo casuale tra più macchine virtuali, è necessario toocreate un set con carico bilanciato costituito da più endpoint.

Dopo aver creato un endpoint, è possibile utilizzare un accesso (ACL) elenco toodefine regole di controllo di cui consentono o negare il traffico in ingresso hello toohello porta pubblica dell'endpoint hello in base al relativo indirizzo IP di origine. Tuttavia, se macchina virtuale hello è in una rete virtuale di Azure, è necessario utilizzare gruppi di sicurezza di rete. Per altre informazioni, vedere [Informazioni sui gruppi di sicurezza di rete](../articles/virtual-network/virtual-networks-nsg.md).

> [!NOTE]
> La configurazione del firewall per le macchine virtuali di Azure viene eseguita automaticamente per le porte associate agli endpoint di connettività remota configurati automaticamente da Azure. Per le porte specificate per tutti gli altri endpoint, viene eseguita alcuna configurazione automaticamente toohello firewall della macchina virtuale hello. Quando si crea un endpoint per la macchina virtuale hello, sarà necessario tooensure che hello firewall della macchina virtuale hello consente anche il traffico di hello per protocollo hello e configurazione di endpoint toohello corrispondente porta privata. tooconfigure hello firewall, vedere la documentazione di hello o la Guida in linea per sistema operativo hello in esecuzione nella macchina virtuale hello.
>
>

## <a name="create-an-endpoint"></a>Creare un endpoint
1. Se non già stato fatto, accedere toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **macchine virtuali**, quindi fare clic su nome hello della macchina virtuale hello che si desidera tooconfigure.
3. Fare clic su **endpoint** in hello **impostazioni** gruppo. Hello **endpoint** pagina vengono elencati tutti gli endpoint corrente di hello per la macchina virtuale hello. Questo esempio è relativo a una VM Windows. Una macchina virtuale Linux mostrerà per impostazione predefinita un endpoint per SSH.

   <!-- ![Endpoints](./media/virtual-machines-common-classic-setup-endpoints/endpointswindows.png) -->
   ![Endpoint](./media/virtual-machines-common-classic-setup-endpoints/endpointsblade.png)

4. Nella barra dei comandi hello sopra le voci di endpoint hello, fare clic su **Aggiungi**.
5. In hello **aggiungere endpoint** , digitare un nome per l'endpoint hello **nome**.
6. In **Protocollo** scegliere **TCP** o **UDP**.
7. In **porta pubblica**, digitare il numero di porta hello hello il traffico in ingresso da Internet hello. In **porta privata**, digitare il numero di porta hello su quale hello macchina virtuale è in ascolto. Questi numeri di porta possono essere diversi. Verificare che hello firewall nella macchina virtuale hello è stato configurato tooallow hello traffico toohello protocollo corrispondente (nel passaggio 6) e porta privata.
10. Fare clic su **OK**.

nuovo endpoint Hello verrà elencata nella hello **endpoint** pagina.

![Creazione dell'endpoint completata](./media/virtual-machines-common-classic-setup-endpoints/endpointcreated.png)

## <a name="manage-hello-acl-on-an-endpoint"></a>Gestire hello ACL su un endpoint
set di hello toodefine dei computer in cui può inviare il traffico, hello ACL su un endpoint può limitare il traffico in base all'indirizzo IP di origine. Seguire questi passaggi tooadd, modificare o rimuovere un ACL per un endpoint.

> [!NOTE]
> Se l'endpoint di hello fa parte di un set con carico bilanciato, le modifiche apportate toohello ACL sull'endpoint vengono applicati tooall endpoint nel set di hello.
>
>

Se hello virtuale è in una rete virtuale di Azure, si consiglia di gruppi di sicurezza di rete anziché gli ACL. Per altre informazioni, vedere [Informazioni sui gruppi di sicurezza di rete](../articles/virtual-network/virtual-networks-nsg.md).

1. Se non già stato fatto, accedere toohello portale di Azure.
2. Fare clic su **macchine virtuali**, quindi fare clic su nome hello della macchina virtuale hello che si desidera tooconfigure.
3. Fare clic su **Endpoint**. Dall'elenco di hello, selezionare l'endpoint appropriato hello. l'elenco ACL Hello è nella parte inferiore di hello della pagina hello.

   ![specificare i dettagli di ACL](./media/virtual-machines-common-classic-setup-endpoints/aclpreentry.png)

4. Utilizzare le righe in hello elenco tooadd, eliminazione o Modifica regole per un ACL e modificarne l'ordine. Hello **Subnet remota** valore è un intervallo di indirizzi IP per il traffico in ingresso da hello Internet hello toopermit di utilizza Bilanciamento carico di Azure o negare il traffico di hello in base al relativo indirizzo IP di origine. Impossibile verificare toospecify hello intervallo di indirizzi IP in formato CIDR, noto anche come formato di prefisso di indirizzo. Un esempio è `10.1.0.0/8`.

 ![Nuova voce ACL](./media/virtual-machines-common-classic-setup-endpoints/newaclentry.png)


È possibile utilizzare le regole tooallow solo il traffico da computer specifici corrispondente tooyour computer il traffico Internet o toodeny hello da intervalli di indirizzi specifici e noti.

Hello regole vengono valutate nell'ordine a partire dalla prima regola hello e che termina con l'ultima regola hello. Ciò significa che le regole devono essere ordinate da toomost meno restrittivo restrittivo. Per alcuni esempi e altre informazioni, vedere [Informazioni sugli elenchi di controllo di accesso di rete (ACL)](../articles/virtual-network/virtual-networks-acl.md).
