# A3-redes
[![NPM](https://img.shields.io/npm/l/react)](https://github.com/Ariel-soares/A3-redes/blob/main/LICENSE) 

# Sobre o projeto

Feito em resposta à proposta da atividade A3 da matéria de Ambientes Computacionais e Conectividade.

O projeto consiste em uma rede composta por outras 4, 1 rede metropolitana, 2 redes empresariais e uma rede que consiste no uso de IOT(Internet das Coisas).

# Tecnologias utilizadas
- Cisco Packet Tracer

## Como foi feito

### Primeira fase - Arquitetura

1º A equipe arquitetou uma topologia para a rede aonde cada aparelho foi escolhido de maneira específica por suas características e propriedades.

2º Foi montada a rede metropolitana, aonde utilizamos roteadores do modelo ROTER-PT, adicionando a ele 5 módulos de expansão de portas gigabit Ethernet, ao mesmo tempo que abriamos a configuração de cada um ligávamos as respectivas portas.

3º Como um dos requisitos funcionais do projeto era de que a rede metropolitana tivesse 4 roteadores com redundância fizemos a interligação entre os mesmos para que esta acontecesse.

4º Após isto foram feitas as redes empresarias com suas devidas individualidades.

5º E por fim foi feita a rede doméstica, que por sua vez utiliza-se de IOT, logo, as conexões são wireless.

Ao fim desta fase temos a topologia base da rede metropolitana, redes empresariais e rede IOT criadas, porém não configuradas.

--------------------------------------------------------------------------------------------------------------------------

### Segunda fase - Endereçamentos

1º Para configurar a rede metropolitana com IPs públicos seguimos a seguinte abordagem:

| **Link**   | **Sub-rede (CIDR)** | **Interface Roteador A** | **Interface Roteador B** |
|------------|----------------------|--------------------------|--------------------------|
| R1 ↔ R2    | 200.10.0.0/30       | R1: 200.10.0.1           | R2: 200.10.0.2           |
| R1 ↔ R3    | 200.10.0.4/30       | R1: 200.10.0.5           | R3: 200.10.0.6           |
| R1 ↔ R4    | 200.10.0.8/30       | R1: 200.10.0.9           | R4: 200.10.0.10          |
| R2 ↔ R3    | 200.10.0.12/30      | R2: 200.10.0.13          | R3: 200.10.0.14          |
| R2 ↔ R4    | 200.10.0.16/30      | R2: 200.10.0.17          | R4: 200.10.0.18          |
| R3 ↔ R4    | 200.10.0.20/30      | R3: 200.10.0.21          | R4: 200.10.0.22          |

2º O próximo passo seria configurar o protocolo OSPF na rede metropolitana, e assim foi feito, cada roteador recebeu as devidas configurações para que cada interface que pertence ao backbone metropolitano fosse registrada apropriadamente.

Ao final desta fase temos a rede metropolitana atuando como centro do projeto, já que esta atua diretamente encurtando rotas e as automatizando, tudo isto devido à utilização do protocolo OSPF.

--------------------------------------------------------------------------------------------------------------------------

### Terceira fase - Endereçamentos das empresas

1º Aqui então decidimos dar conta da configuração de IPs das empresas, tomando os devidos cuidados para que uma delas tivesse o range apropriado para que não extrapolassemos demais o máximo de 100 usuários enquanto na outra deveria ter pelo menos 500. E para isso a escolha das redes foi essencial. 

2º A primeira empresa será uma locadora de filmes e video-jogos, nesta haverão no máximo 100 hosts simultaneos, por isso a escolha de rede foi 192.168.1.0 submáscara 255.255.255.128. Esta combinação nos dá um range de 126 endereços utilizáveis, não faltando e nem extrapolando demais o número necessário.

3º A segunda empresa será uma Lan house e nela teremos um máximo de 500 hosts simultâneos, logo nossa escolha foi 192.168.2.0 com a máscara 255.255.254.0. Esta combinação admite 510 endereços utilizáveis, também não extrapolando e nem faltando endereços.

4º As redes empresariais são conectadas à rede metropolitana através de um roteador principal cada, ou seja, este atuaria como o ponto de acesso e saída(Default Gateway).

5º Levando em conta que a manioria dos Hosts nas empresas não precisam ter endereços fixos, utilizamos alguns endereços estáticos específicos na rede e deixamos que o resto adquirisse um endereço dinâmico, e para isso foi utilizado o protocolo DHCP. O mesmo irá prover para os Hosts endereços IPs dinâmicos assim como também o endereço estático do Gateway e do DNS que ainda viria a ser criado.

6º Neste momento já é possível que haja comunicação entre os Hosts da empresa, porém, para que houvesse comunicação com redes exteriores seria necessário ainda a configuração tanto de rotas estáticas no roteador principal de cada empresa como a tradução dos endereços IPs privados para que os mesmos pudessem ser publicados na rede metropolitana. E para tal foi utilizado o protocolo NAT, que viria a ser o responsável por conseguirmos enviar pacotes da rede privada para a rede pública fora da empresa, então foi configurada uma porta como entrada e duas para saída já que os roteadores principais das empresas estão ligados em outros dois da rede metropolitana, roteadores estes que receberam uma rota estática aonde os endereços das redes privadas seriam redirecionados via tradução.

Ao final desta fase temos as redes empresariais se comunicando com a rede metropolitana através da tradução de IPs privados para Ips públicos graças ao protocolo NAT nas empresas e ao roteamento dos roteadores metropolitanos.

--------------------------------------------------------------------------------------------------------------------------

### Quarta fase - Criação de serviços e servidores

1º Agora que todas as redes estavam se comunicando com redundância e pouca ou nenhuma latência, faltava criar e configurar os servidores HTTP de cada empresa e o servidor DNS que atuará como registro de domínios, e assim foi feito, ainda na rede metropolitana criamos uma rede auxiliar com o endereço 190.190.190.0 e máscara 255.255.255.252, aonde haverá 3 servidores, um deles será o provedor do serviço DNS asim como também o servidor de domínio da rede metropolitana, e a ele atribuimos o IP 190.190.190.2, os outros dois servidores seriam apenas os servidores do domínio das empresas, receberam os IPs 190.190.190.5 e .190.190.190.6.

2º Nos servidores das empresas temos apenas o endereço HTTP ativo e a página index.html com uma página de apresentação codificada nela.

2º No servidor DNS foram criados os respectivos domínios das empresas assim como seus devídos endereços IP.

Ao fim desta fase é possível acessar a página de apresentação de cada empresa apenas acessando seus domínios via web browser sem a necessidade de entrar com o IP do servidor em questão

# Autores

Membros da equipe:

- Ariel Soares Franco - 12722210594
- Manuelle Reis Santana - 1272116405
- Yara Carolina Leite dos Santos - 12724136783
- Marcela Tourinho Machado Barreto -12724139040
- Gabriel Coutinho - 1272412136
