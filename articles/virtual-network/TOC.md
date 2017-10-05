# Panoramica
## [Reti virtuali](virtual-networks-overview.md)
## [Route definite dall'utente e inoltro IP](virtual-networks-udr-overview.md)
## [Peering di rete virtuale](virtual-network-peering-overview.md)
## [Continuità aziendale](virtual-network-disaster-recovery-guidance.md)
## [Domande frequenti](virtual-networks-faq.md)
## [Indirizzamento IP](virtual-network-ip-addresses-overview-arm.md)
## Classico
### [Indirizzamento IP](virtual-network-ip-addresses-overview-classic.md)
### [Elenchi di controllo di accesso](virtual-networks-acl.md)

# Attività iniziali
## [Creare la prima rete virtuale](virtual-network-get-started-vnet-subnet.md)

# Procedure
## Pianificare e progettare
### [Reti virtuali](virtual-network-vnet-plan-design-arm.md)
### [Gruppi di sicurezza di rete](virtual-networks-nsg.md)

## Distribuire
### [Reti virtuali](virtual-networks-create-vnet-arm-pportal.md)
#### [PowerShell](virtual-networks-create-vnet-arm-ps.md)
#### [CLI](virtual-networks-create-vnet-arm-cli.md)
#### [Modello](virtual-networks-create-vnet-arm-template-click.md)

### Gruppi di sicurezza di rete
#### [Portale](virtual-networks-create-nsg-arm-pportal.md)
#### [PowerShell](virtual-networks-create-nsg-arm-ps.md)
#### [CLI](virtual-networks-create-nsg-arm-cli.md)
#### [Modello](virtual-networks-create-nsg-arm-template.md)
#### Classico
##### [PowerShell](virtual-networks-create-nsg-classic-ps.md)
##### [CLI](virtual-networks-create-nsg-classic-cli.md)

### Route definite dall'utente
#### [PowerShell](virtual-network-create-udr-arm-ps.md)
#### [CLI](virtual-network-create-udr-arm-cli.md)
#### [Modello](virtual-network-create-udr-arm-template.md)
#### Classico
##### [PowerShell](virtual-network-create-udr-classic-ps.md)
##### [CLI](virtual-network-create-udr-classic-cli.md)

### Peering di rete virtuale
#### [Stesso modello di distribuzione e stessa sottoscrizione](virtual-network-create-peering.md)
#### [Stesso modello di distribuzione e diversa sottoscrizione](create-peering-different-subscriptions.md)
#### [Modelli di distribuzione diversi e stessa sottoscrizione](create-peering-different-deployment-models.md)
#### [Modelli di distribuzione diversi e diverse sottoscrizioni](create-peering-different-deployment-models-subscriptions.md)

### Macchine virtuali
#### Creare una VM con un indirizzo IP pubblico statico
##### [Portale](virtual-network-deploy-static-pip-arm-portal.md)
##### [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
##### [CLI](virtual-network-deploy-static-pip-arm-cli.md)
##### [Modello](virtual-network-deploy-static-pip-arm-template.md)
##### Classico
###### [PowerShell](virtual-networks-reserved-public-ip.md)

#### Creare una VM con un indirizzo IP privato statico
##### [Portale](virtual-networks-static-private-ip-arm-pportal.md)
##### [PowerShell](virtual-networks-static-private-ip-arm-ps.md)
##### [CLI](virtual-networks-static-private-ip-arm-cli.md)
##### Classico
###### [Portale](virtual-networks-static-private-ip-classic-pportal.md)
###### [PowerShell](virtual-networks-static-private-ip-classic-ps.md)
###### [CLI](virtual-networks-static-private-ip-classic-cli.md)

#### Creare una VM con più interfacce di rete
##### [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
##### [CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
##### Classico
###### [PowerShell](virtual-network-deploy-multinic-classic-ps.md)
###### [CLI](virtual-network-deploy-multinic-classic-cli.md)

#### Creare una macchina virtuale con più indirizzi IP
##### [Portale di Azure](virtual-network-multiple-ip-addresses-portal.md)
##### [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)
##### [CLI](virtual-network-multiple-ip-addresses-cli.md)
##### [Modello](virtual-network-multiple-ip-addresses-template.md)

#### [Creare una VM con rete accelerata](virtual-network-create-vm-accelerated-networking.md)

### Scenari di connettività
#### [Da rete virtuale a rete virtuale](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [Da rete virtuale (Resource Manager) a rete virtuale (versione classica)](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [Da rete virtuale a rete locale (VPN)](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [Da rete virtuale a rete locale (ExpressRoute)](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [Architettura di rete ibrida a disponibilità elevata](../guidance/guidance-hybrid-network-expressroute-vpn-failover.md?toc=%2fazure%2fvirtual-network%2ftoc.json)

### Scenari di sicurezza
#### [Proteggere le reti con appliance virtuali](virtual-network-scenario-udr-gw-nva.md)
#### [Rete perimetrale tra Azure e Internet](../guidance/guidance-iaas-ra-secure-vnet-dmz.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [Servizio cloud e sicurezza di rete](../best-practices-network-security.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
##### [Rete perimetrale semplice con gruppi di sicurezza di rete](virtual-networks-dmz-nsg-asm.md)
##### [Rete perimetrale con firewall e gruppi di sicurezza di rete](virtual-networks-dmz-nsg-fw-asm.md)
##### [Rete perimetrale con firewall, UDR e gruppi di sicurezza di rete](virtual-networks-dmz-nsg-fw-udr-asm.md)
##### [Applicazione di esempio](virtual-networks-sample-app.md)

### Classico
#### [Rete virtuale](create-virtual-network-classic.md)
##### [Portale](virtual-networks-create-vnet-classic-pportal.md)
##### [PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md)
##### [CLI](virtual-networks-create-vnet-classic-cli.md)

## Configurare
### Macchine virtuali
#### [Aggiungere o rimuovere interfacce di rete](virtual-network-network-interface-vm.md)
#### [Risoluzione dei nomi per macchine virtuali e servizi cloud](virtual-networks-name-resolution-for-vms-and-role-instances.md)
#### [Ottimizzare la velocità effettiva della rete](virtual-network-optimize-network-bandwidth.md)
#### [Visualizzare e modificare i nomi host](virtual-networks-viewing-and-modifying-hostnames.md)
### Classico
#### Elenchi di controllo di accesso
##### [Portale](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
##### [PowerShell](virtual-networks-acl-powershell.md)

## Manage
### [Reti virtuali](virtual-network-manage-network.md)
#### [Subnet](virtual-network-manage-subnet.md)
#### [Peering](virtual-network-manage-peering.md)
#### Classico
##### [File di configurazione di rete](virtual-networks-using-network-configuration-file.md)
##### [Eseguire la migrazione da un gruppo di affinità a un'area](virtual-networks-migrate-to-regional-vnet.md)
### Gruppi di sicurezza di rete
#### [Portale](virtual-network-manage-nsg-arm-portal.md)
#### [PowerShell](virtual-network-manage-nsg-arm-ps.md)
#### [Interfaccia della riga di comando](virtual-network-manage-nsg-arm-cli.md)
#### [Log](virtual-network-nsg-manage-log.md)
### Interfacce di rete (NIC)
#### [Creare, modificare o eliminare interfacce di rete](virtual-network-network-interface.md)
#### [Aggiungere, modificare o rimuovere indirizzi IP](virtual-network-network-interface-addresses.md)
### Macchine virtuali
#### [Spostare una macchina virtuale in una subnet diversa](virtual-networks-move-vm-role-to-subnet.md)
### [Indirizzi IP pubblici](virtual-network-public-ip-address.md)

## Risoluzione dei problemi
### Gruppi di sicurezza di rete
#### [Portale](virtual-network-nsg-troubleshoot-portal.md)
#### [PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
### Route
#### [Portale](virtual-network-routes-troubleshoot-portal.md)
#### [PowerShell](virtual-network-routes-troubleshoot-powershell.md)
### [Test della velocità effettiva](virtual-network-bandwidth-testing.md)
### [Non è possibile eliminare le reti virtuali](virtual-network-troubleshoot-cannot-delete-vnet.md)
### [Problemi di connettività da VM a VM](virtual-network-troubleshoot-connectivity-problem-between-vms.md)

# riferimento
## [Esempi di codice](https://azure.microsoft.com/en-us/resources/samples/?service=virtual-network)
## [PowerShell (Resource Manager)](/powershell/module/azurerm.network)
## [PowerShell (classico)](/powershell/module/azure/)
## [Interfaccia della riga di comando di Azure](/cli/azure/network)
## [Java](/java/api/)
## [REST (Resource Manager)](https://msdn.microsoft.com/library/mt163658.aspx)
## [REST (classico)](https://msdn.microsoft.com/library/jj157182.aspx)


# Risorse correlate
## [Macchine virtuali](/azure/virtual-machines/)
## [Gateway applicazione](/azure/application-gateway/)
## [DNS di Azure](/azure/dns/)
## [Gestione traffico](/azure/traffic-manager/)
## [Bilanciamento del carico](/azure/load-balancer/)
## [Gateway VPN](/azure/vpn-gateway/)
## [ExpressRoute](/azure/expressroute/)

# Risorse
## [Roadmap per Azure](https://azure.microsoft.com/roadmap/?category=networking)
## [Blog sulle reti](http://azure.microsoft.com/blog/topics/networking)
## [Forum sulle reti](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesVirtualNetwork)
## [Prezzi](https://azure.microsoft.com/pricing/details/virtual-network)
## [Calcolatore prezzi](https://azure.microsoft.com/pricing/calculator/)
## [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-virtual-network)
