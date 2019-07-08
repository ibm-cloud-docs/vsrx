---

copyright:
  years: 2018
lastupdated: "2018-11-06"

keywords: limitations, problems

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:note: .note}
{:important: .important}

# Limitações conhecidas para o IBM Cloud Juniper vSRX
{: #known-limitations-for-ibm-cloud-juniper-vsrx}

Limitações atuais para o {{site.data.keyword.cloud}} IBM® Cloud Juniper vSRX:

* O gatewya Juniper vSRX é implementado com virtualização de rede usando a ponte Linux. A virtualização de rede baseada em ponte Linux pode alcançar somente um rendimento limitado e nunca o rendimento da taxa da linha.

* Não há nenhum suporte para fazer upgrade do modo independente para o modo de alta disponibilidade.

* O Gateway IBM Cloud Juniper vSRX é implementado com as opções do Junos OS da versão `15.1` ou `18.4`. Atualmente, não há suporte de upgrade/downgrade para uma versão diferente.

* A licença de avaliação de 60 dias pode fazer com que o kernel gere mensagens de ERRO, mesmo quando houver outra licença (válida) no sistema. Deve-se remover todas as licenças de avaliação de 60 dias para evitar esse problema. Para fazer isso, execute o procedimento a seguir:

1. Faça login em seu dispositivo de gateway vSRX.

2. Entre no modo de CLI executando o comando `cli` no prompt do console.

3. Execute o comando para obter o identificador de licença:

```
show system license
```
A saída deve ser semelhante à seguinte:

```
License usage:
                                 Licenses     Licenses    Licenses    Expiry
  Feature name                       used    installed      needed
  logical-system                        0            3           0    permanent
  Virtual Appliance                     1            1           0    2021-10-18 00:00:00 UTC
  remote-access-ipsec-vpn-client        0            2           0    permanent

Licenses installed:
  License identifier: E2018101804
  License version: 4
  Software Serial Number: SUB00024128768
  Customer ID: IBM_SL_10G
  Features:
    Virtual Appliance - Virtual Appliance
      date-based, 2018-10-18 00:00:00 UTC - 2021-10-18 00:00:00 UTC
```

4. Copie o identificador da licença que deseja excluir e execute o comando:

```
request system license delete <license identifier>
```
