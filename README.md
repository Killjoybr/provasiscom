# Roteamento Estático entre Unidades Regionais do Governo do Distrito Federal

## Contexto do Problema:

O cenário envolve um cenário hipotético de conexão entre três unidades regionais do Governo do Distrito Federal (GDF), distribuídas em diferentes regiões administrativas:

  1. Taguatinga: Unidade responsável pelos serviços administrativos e de atendimento ao público na região.
  1. Asa Norte: Unidade focada nos serviços de planejamento e coordenação de projetos no DF.
  1. Asa Sul: Unidade encarregada dos serviços de suporte técnico e infraestrutura de TI.

Para garantir uma comunicação eficiente e segura entre as unidades, foi configurado um roteador central para realizar o roteamento entre as sub-redes das três regiões, com suporte ao gerenciamento e ao tráfego de dados entre elas.

## Objetivo da Simulação:

Configurar e validar a comunicação entre as unidades do GDF (Taguatinga, Asa Norte, Asa Sul) utilizando o simulador GNS3. A topologia será composta por um roteador central (MikroTik CHR) e três switches Ethernet conectados a dispositivos VPCS (Virtual PC Simulator) que simulam computadores ou dispositivos de cada unidade.
Tarefas a serem Realizadas:

  - Instalação do Roteador Mikrotik CHR no GNS3:
        - Acesse as instruções e arquivos necessários no repositório siscom/routing no GitHub do professor. 
        - Baixe o arquivo chr-7.11.2.img.zip ou chr-7.14.3.img.zip, e descompacte-o com o comando unzip.
        - Importe a imagem do roteador MikroTik CHR no GNS3 seguindo as orientações disponíveis no repositório.

  - Configuração da Topologia no GNS3:
        - Crie um novo projeto no GNS3.
- Adicione os dispositivos necessários:
    - 1 roteador (MikroTik CHR).
    - 3 switches Ethernet.
    - 6 VPCS (2 para cada unidade regional).
    - Conexões:
      - Conecte o switch de Taguatinga à Interface Ether1 do Router.
        - Conecte o switch de Asa Norte à Interface Ether2 do Router.
        - Conecte o switch de Asa Sul à Interface Ether3 do Router.

    Configuração do Roteamento Estático:
  - Configure o protocolo de roteamento estático no roteador central para direcionar o tráfego entre as três sub-redes.
  - Defina as interfaces de rede que estarão envolvidas no roteamento estático entre as unidades.

    Configuração de IPs e Testes:

    Atribua IPs aos VPCS para simular dispositivos de cada unidade, como segue:
    - Unidade Taguatinga: IP na faixa 192.168.10.10/24 com gateway 192.168.10.1
    - Unidade Asa Norte: IP na faixa 192.168.20.10/24 com gateway 192.168.20.1
    - Unidade Asa Sul: IP na faixa 192.168.30.10/24 com gateway 192.168.30.1
    
    Teste a comunicação entre dispositivos das três unidades e entre dispositivos de cada unidade.

## Critérios de Avaliação:

  Corretude da Configuração:
    - A topologia foi implementada de acordo com as especificações?
    - As rotas estáticas foram configuradas corretamente para permitir o roteamento entre as sub-redes das três unidades regionais?
    - A comunicação entre os dispositivos das unidades está funcionando corretamente?

  Relatório:
- Inclua descrições dos passos de configuração no GNS3.
- Detalhe o processo de configuração do roteamento estático e atribuição de IPs, utilizando referências e capturas de tela da configuração.
- Avalie as vantagens observadas no uso do roteamento estático para este cenário.


  Suporte:
      Estarei disponível por e-mail: redacted e celular (WhatsApp): redacted das 13h às 16h de seg-qui para sanar eventuais dúvidas na implementação.

Observação: A avaliação consiste na realização do experimento e entrega do relatório sucinto contendo as descrições e evidências (prints) das configurações e testes realizados.
