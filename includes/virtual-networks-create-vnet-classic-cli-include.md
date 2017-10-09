## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a>Come toocreate una rete virtuale classica mediante Azure CLI
È possibile utilizzare hello Azure CLI toomanage le risorse di Azure dal prompt dei comandi di hello da qualsiasi computer che eseguono Windows, Linux o OSX. una rete virtuale tramite l'interfaccia CLI di Azure, hello toocreate procedura hello riportata di seguito.

1. Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../articles/cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.
2. Eseguire hello **creazione della rete virtuale di rete di azure** comando toocreate una rete virtuale e una subnet, come illustrato di seguito. elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    Output previsto:
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * **--vnet**. Nome di hello toobe di rete virtuale creata. Per questo scenario, *TestVNet*
   * **-e (o --address-space)**. Spazio degli indirizzi della rete virtuale. Per questo scenario, *192.168.0.0*
   * **-i (o -cidr)**. Maschera di rete nel formato CIDR. Per questo scenario, *16*
   * **- n (o --subnet-name**). Nome della subnet prima hello. Per questo scenario, *FrontEnd*.
   * **-p (or --subnet-start-ip)**. Indirizzo IP iniziale per la subnet o spazio di indirizzi della subnet. Per questo scenario, *192.168.1.0*
   * **-r (o --subnet-cidr)**. Maschera di rete nel formato CIDR per la subnet. Per questo scenario, *24*
   * **-l (o --location)**. Area di Azure in cui verrà creato hello rete virtuale. Per questo scenario, *Central US*.
3. Eseguire hello **subnet di rete virtuale di rete di azure creare** toocreate comando una subnet, come illustrato di seguito. elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    Ecco l'output di hello previsto per comando hello sopra indicato:
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * **-t (o --vnet-name**. Nome della rete virtuale in cui verrà creata la subnet hello hello. Per questo scenario, *TestVNet*.
   * **-n (o --nome)**. Nome della nuova subnet hello. Per questo scenario, *BackEnd*.
   * **-a (o --address-prefix)**. Blocco CIDR della subnet. Per questo scenario, *192.168.2.0/24*.
4. Eseguire hello **Mostra di rete virtuale di rete di azure** comando proprietà hello tooview di hello nuova rete virtuale, come illustrato di seguito.
   
            azure network vnet show
   
    Ecco l'output di hello previsto per comando hello sopra indicato:
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

