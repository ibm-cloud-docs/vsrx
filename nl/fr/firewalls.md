---

copyright:
  years: 2018
lastupdated: "2018-10-22"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Fonctionnement des pare-feux
{: #working-with-firewalls}

IBM® Cloud Juniper vSRX s'appuie sur le concept de zones de sécurité, où chaque interface vSRX est mappée à une "zone" pour le traitement des pare-feux avec état. Les pare-feux sans état sont contrôlés par des filtres de pare-feu.

Les politiques sont utilisées pour autoriser et bloquer le trafic entre ces zones définies, et les règles définies ici sont avec état.

Dans IBM Cloud, un vSRX est conçu pour avoir quatre zones de sécurité différentes :

| Zone                     | Interface autonome | Interface haute disponibilité |
| :---                     |        :----:        |         ---: |
| SL-Private (non balisée)    | ge-0/0/0.0           | reth0.0      |
| SL-Public (non balisée)     | ge-0/0/1.0           | reth1.0      |
| Customer-Private (balisée)| ge-0/0/0.1           | reth2.1      |
| Customer-Public (balisée) | ge-0/0/1.1           | reth3.1      |

## Politiques de zone
Pour configurer un pare-feu avec état, procédez comme suit :

1. Créez des zones de sécurité et affectez-leur les interfaces respectives :

	Scénario autonome :
	```
	set security zones security-zone CUSTOMER-PRIVATE interfaces ge-0/0/0.1
	set security zones security-zone CUSTOMER-PUBLIC interfaces ge-0/0/1.1
	```
	Scénario haute disponibilité :
	```
	set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.1
	set security zones security-zone CUSTOMER-PUBLIC interfaces reth2.1
	```
2. Définissez la politique et les règles entre deux zones différentes.

	The following example illustrates pinging traffic from the zone `Customer-Private` to `Customer-Public`:

	```
	set security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PUBLIC policy ALLOW_ICMP match source-address any destination-address any application junos-icmp

	set security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PUBLIC policy ALLOW_ICMP then permit
	```

Voici quelques-uns des attributs pouvant être définis dans vos politiques :

* Adresses source
* Adresses de destination
* Applications
* Action (autoriser/refuser/rejeter/comptabiliser/consigner)

Comme il s'agit d'une opération avec état, il n'est pas nécessaire d'autoriser les paquets de retour (dans ce cas, l'écho répond).

Utilisez les commandes suivantes pour autoriser le trafic dirigé vers le vSRX :

Cas autonome :
```
set security zones security-zone CUSTOMER-PRIVATE interfaces ge-0/0/0.0 host-inbound-traffic system-services all
```
Cas haute disponibilité :
```
set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.0 host-inbound-traffic system-services all
```

Pour autoriser les protocoles, OSPF ou BGP notamment, exécutez la commande ci-dessous :

Cas autonome :
```
set security zones security-zone trust interfaces ge-0/0/0.0 host-inbound-traffic protocols all
```
Cas haute disponibilité :
```
set security zones security-zone trust interfaces reth2.0 host-inbound-traffic protocols all
```

## Filtres de pare-feu
Par défaut, IBM Cloud Juniper vSRX accepte les commandes ping, les protocoles SSH et HTTPS, et supprime tout autre trafic en appliquant le filtre `PROTECT-IN` à l'interface `lo`.

Pour configurer un nouveau pare-feu sans état, procédez comme suit :

1. Créez le filtre et le terme du pare-feu (le filtre ci-dessous autorise uniquement le protocole ICMP et supprime le reste du trafic).
	```
	set firewall filter ALLOW-PING term ICMP from protocol icmp
	set firewall filter ALLOW-PING term ICMP then accept
	```

2. Appliquez la règle de filtrage à l'interface (la commande suivante applique le filtre à l'ensemble du trafic du réseau privé).
	```
	set interfaces ge-0/0/0 unit 0 family inet filter input ALLOW-PING
	```
