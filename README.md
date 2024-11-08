# Avaliação SISCOM

```JSON
{
  "aluno":"Ruan David da Silva",
  "ra":"22051922",
  "matéria":"Sistemas de Comunicação",
  "Professor":"Klayton Rodrigues de Castro",
}
```

- [Resumo](#resumo)
- [Tarefas](#tarefas)
- [Configuração no Roteador Mikrotik CHR](#configuração-no-roteador-mikrotik-chr)
- [Testes](#testes)
- [Topologia da rede](#topologia-da-rede)

## Resumo
Utilizei as documentações disponíveis no github do professor para inicializar o laboratório, as tecnologias utilizadas foram: **git**, **cli**, **docker**, **gns3** e **conceitos de redes**. O laboratório tem como objetivo avaliar a compreensão do aluno com conceitos de configuração de ips estáticos nos equipamentos (o professor também aceita assimilação de ips utilizando DHCP), estruturação da topologia da rede (Conexão física entre as máquinas) e se a comunicação entre os dispositivos não apresenta erro. 

Após terminar o laboratório eu me senti capaz de configurar um firewall em casa, podemos considerar qualquer switch que utilizei no laborátorio e imaginar que ele funcionaria como um dispositivo diferente rodando um firewall, configurando apenas um gateway todo o tráfego passara por esse dispositivo (raspberrypi?) e assim melhoraria a segurança da sua rede doméstica, porém isso foi apenas um sentimento após o término do laboratório. 

O lab é uma simulação de uma rede no DF entre unidades do governo, onde é composta por: um roteador em uma região não especificada, mas com certeza em "alcance" MAN e trios compostos por, um switch e 2 PCs que funcionam como LAN e estão conectadas ao roteador que interliga os 3 switches e provisiona os endereços de ip pra cada máquina via servidor DHCP.


## Tarefas

- Passos de configuração do GNS3
  - Topologia (via GUI)
      - Importar a imagem do Mikrotk CHR para a bliblioteca do GNS3.
      - Importar o dispositivo virtual do Mikrotik, que será nosso roteador central.
      - Importar 3 switches, cada um representando uma região diferente do DF, Taguatinga, Asa Norte e Asa Sul, respectivamente.
      - Importar 2 VPCs para cada switch, que serão nossas máquinas virtuais.
      - Conectar os cabos lógicos de cada dispositivo:
        - Roteador Central ethernet 1 - Switch Taguatinga
        - Roteador Central ethernet 2 - Switch Asa Norte
        - Roteador Central ethernet 3 - Switch Asa Sul
        - Switch Taguatinga ethernet n - VPc n 
        - Switch Asa Norte ethernet n - VPc n 
        - Switch Asa Sul ethernet n - VPc n
  - Configuração via CLI para servidor DHCP e ping simulando comunicação entre as VPCs localmente e entre unidades.

## Configuração no Roteador Mikrotik CHR

<details>
<summary> <b>Assimilando ips as interfaces</b> </summary>

  ```shell
    ip address add address=192.168.10.1/24 interface=ether1
  ```

</details>

<details>
<summary> <b>Criação das pools de Ips dinâmicos</b> </summary>

  ```shell
    ip pool add name=dhcp_pool_taguatinga ranges-192.168.10.100-192.168.10.200
  ```

</details>

<details>
<summary> <b>Criação do servidor DHCP na interface</b> </summary>

  ```shell
    ip dhcp-server add name=dhcp_server_taguatinga interface=ether1 address-pool=dhcp_pool_taguatinga lease-time=1h
  ```

</details>

<details>
<summary> <b>Assimilação das redes de cada servidor DHCP</b> </summary>

  ```shell
    ip dhcp-server network add address=192.168.10.0/24 gateway=192.168.10.1
  ```

</details>

## Testes

<details>
<summary> <b>Teste Após solicitar ip nas máquinas 1, 5 e 3</b> </summary>

  ![teste_dhcp_lease](/assets/teste_impar.png)

</details>

<details>
<summary> <b>Solicitando IP no restante das máquinas</b> </summary>

![dhcp_pc02](/assets/pc02.png)
<hr>

![dhcp_pc04](/assets/pc04.png)
<hr>

![dhcp_pc06](/assets/pc06.png)

</details>

<details>
<summary> <b>Tentando comunicação entre as máquinas</b> </summary>

![ping_pc01](/assets//ping_pc01.png)
<hr>

![ping_pc04](/assets/ping_pc04.png)
<hr>

![ping_pc06](/assets/ping_pc06.png)
<hr>

</details>

<details>
<summary> <b>Verificando leases pós ping</b> </summary>

![lease_pos](/assets/teste_pos_ping.png)

</details>

<details>
<summary> <b>Vantagens sob o uso do DHCP</b> </summary>

Fazendo a configuração do DHCP mesmo em uma rede pequena, na minha opinião é uma boa prática, já que minimiza erros da configuração manual de ips, na minha primeira tentativa, configurando manualmente acabei fazendo um overlapping nos endereços, resolvi resetando o mikrotik via cli e depois utilizando o dhcp conforme a documentação do professor. 

Os principais pontos positivos do DHCP são: redução de erros, economia de tempo e caso a rede aumente ou um usuário deseja receber um ip especifico o DHCP é a ferramenta ideal.

</details>

## Topologia da rede

![Topologia](/assets/topologiaGNS3.png)