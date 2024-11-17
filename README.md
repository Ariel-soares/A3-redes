# A3-redes
[![NPM](https://img.shields.io/npm/l/react)](https://github.com/Ariel-soares/A3-redes/blob/main/LICENSE) 

# Sobre o projeto

Feito em resposta à proposta da atividade A3 da matéria de Ambientes Computacionais e Conectividade.

O projeto consiste em uma rede composta por outras 4, 1 rede metropolitana, 2 redes empresariais e uma rede que consiste no uso de IOT(Internet das Coisas).

# Tecnologias utilizadas
- Cisco Packet Tracer

## Como foi feito

### Primeira fase

1º A equipe arquitetou uma topologia para a rede aonde cada aparelho foi escolhido de maneira específica por suas características e propriedades.

2º Foi montada a rede metropolitana, aonde utilizamos roteadores do modelo ROTER-PT, adicionando a ele 5 módulos de expansão de portas gigabit Ethernet, ao mesmo tempo que abriamos a configuração de cada um dles e ligavamos as respectivas portas.

3º Como um dos requisitos funcionais do projeto era de que a rede metropolitana tivesse 4 roteadores com redundância fizemos a interligação entre os mesmos para que acontecesse a redundância.

4º Após isto foram feitas as redes empresarias com suas devidas individualidades.

5º E por fim foi feita a rede doméstica, que por sua vez utiliza-se de IOT, logo, as conexões são wireless.

--------------------------------------------------------------------------------------------------------------------------

### Segunda fase

1º Para configurar a rede metropolitana com IPs públicos seguimos a seguinte configuração:

| **Link**   | **Sub-rede (CIDR)** | **Interface Roteador A** | **Interface Roteador B** |
|------------|----------------------|--------------------------|--------------------------|
| R1 ↔ R2    | 200.10.0.0/30       | R1: 200.10.0.1           | R2: 200.10.0.2           |
| R1 ↔ R3    | 200.10.0.4/30       | R1: 200.10.0.5           | R3: 200.10.0.6           |
| R1 ↔ R4    | 200.10.0.8/30       | R1: 200.10.0.9           | R4: 200.10.0.10          |
| R2 ↔ R3    | 200.10.0.12/30      | R2: 200.10.0.13          | R3: 200.10.0.14          |
| R2 ↔ R4    | 200.10.0.16/30      | R2: 200.10.0.17          | R4: 200.10.0.18          |
| R3 ↔ R4    | 200.10.0.20/30      | R3: 200.10.0.21          | R4: 200.10.0.22          |

2º O próximo passo seria configurar o protocolo OSPF na rede metropolitana, e assim foi feito, cada roteador recebeu as devidas configurações para que cada interface que pertence ao backbone metropolitano fosse configurado apropriadamente.

3º Aqui então decidimos dar conta da configuração de IPs das empresas, tomando os devidos cuidados para que uma delas tivesse o range apropriado para que não extrapolassemos demais o máximo de 100 usuários enquanto na outra deveria ter pelo menos 500

4º Neste momento a rede metropolitana e as redes empresariais já estavam funcionais e operável, então partimos para a rede que implementa IOT, escolhemos então alguns aparelhos IOT que faziam parte da proposta da atividade e os conectamos a um aparelho via wifi.

# Autores

Membros da equipe:

- Ariel Soares Franco - 12722210594
- Manuelle Reis Santana - 
- Yara Carolina -
- Marcela -
- Gabriel Coutinho -
