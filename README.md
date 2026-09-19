# Atividade 4 — Padrões 802.3 e Redes Hierárquicas

## 📋 Sobre a Atividade

Esta atividade tem como objetivo colocar em prática o conhecimento adquirido sobre os padrões 802.3, utilizando o simulador **Cisco Packet Tracer** para montar uma rede completa com os elementos necessários para uma rede hierárquica funcional, contemplando **escalabilidade, hierarquia, redundância e disponibilidade**.

Trata-se da simulação de um ambiente hierárquico de rede local, representando a etapa de planejamento de implementação de uma rede em um contexto real.

- **Assunto:** Padrões 802.3 e redes hierárquicas
- **Tempo previsto:** 4 horas
- **Prazo de entrega:** 27/08/2026

---

## 🎯 Tarefas / Requisitos da Atividade

Para esta etapa, é exigida **apenas a configuração das ligações físicas** entre os dispositivos (sem configuração de equipamentos ainda), respeitando os seguintes requisitos:

1. Construir uma rede que tenha, de forma visível, a estrutura hierárquica, respeitando as características de cada camada (**núcleo, distribuição e borda**).
2. Incluir um **roteador com duas interfaces FastEthernet**, ligando-se a dois switches de núcleo diferentes.
3. Os dois switches de núcleo devem ter **ligação física entre si**, preparada para ativação futura de uma agregação de link (*link aggregation*) de **4 Gbps**.
4. Os dois switches de núcleo devem ser conectados **individualmente** a outros dois switches de distribuição, por meio de **interfaces de fibra óptica**, preparadas para ativação futura de uma agregação de link de **2 Gbps**.
5. Disponibilizar **quatro switches de borda**, sem qualquer recurso de redundância.
6. Disponibilizar **quatro computadores desktop, quatro notebooks e um servidor**, todos conectados com fio à rede.

**Extra (opcional):** configurar os endereços IP em cada dispositivo final de forma que eles se comuniquem entre si (teste via `ping`) — vale 10% de bônus na pontuação da atividade.

---

## 🗺️ Topologia Implementada


                                   [Router0 - 2811]
                              (2x interfaces FastEthernet)
                                    /              \
                             Fa0/0 /                \ Fa0/1
                                  /                  \
                    +------------------+      +------------------+
                    |  Switch0         |======|  Switch0(1)      |
                    |  (Núcleo)        | 4Gbps|  (Núcleo)        |
                    +------------------+      +------------------+
                          |        \          /        |
                          |         \        /         |
                     fibra|          \      /          |fibra
                     2Gbps|           \    /           |2Gbps
                          |            \  /            |
                          |             \/             |
                          |             /\             |
                          |            /  \            |
                    +------------------+      +------------------+
                    |  Switch0(2)      |      |  Switch0(3)      |
                    |  (Distribuição)  |      |  (Distribuição)  |
                    +------------------+      +------------------+
                       /            \            /            \
                      /              \          /              \
              +-----------+    +-----------+  +-----------+   +-----------+
              | Switch1   |    | Switch2   |  | Switch3   |   | Switch4   |
              | (Borda)   |    | (Borda)   |  | (Borda)   |   | (Borda)   |
              +-----------+    +-----------+  +-----------+   +-----------+
                /       \        /       \      /       \       /   |    \
              PC0    PC0(1)   PC0(2)  PC0(3) Laptop0 Laptop0(1) L0(2) L0(3) Server0

### Dispositivos utilizados

| Papel | Dispositivo | Modelo |
|---|---|---|
| Roteador | Router0 | Cisco 2811 |
| Núcleo | Switch0, Switch0(1) | Switch-PT-Empty |
| Distribuição | Switch0(2), Switch0(3) | Switch-PT-Empty |
| Borda | Switch1, Switch2, Switch3, Switch4 | 2960-24TT |
| Desktops | PC0, PC0(1), PC0(2), PC0(3) | PC-PT |
| Notebooks | Laptop0, Laptop0(1), Laptop0(2), Laptop0(3) | Laptop-PT |
| Servidor | Server0 | Server-PT |

---

## 🔌 Tabela de Conexões

### Núcleo, Distribuição e Servidor

| Origem            | Porta  | Cabo   | Porta  | Destino                    |
|-------------------|--------|--------|--------|----------------------------|
| SW-NUCLEO-02      | Fa7/1  | Cobre  | Fa0/1  | R-BORDA-WAN (Router 1841)  |
| SW-NUCLEO-02(1)   | Fa0/1  | Cobre  | Fa0/0  | R-BORDA-WAN (Router 1841)  |
| SW-NUCLEO-02(1)   | Fa6/1  | Cobre  | Fa0/1  | SW-NUCLEO-02               |
| SW-NUCLEO-02(1)   | Fa7/1  | Cobre  | Fa8/1  | SW-NUCLEO-02               |
| SW-NUCLEO-02(1)   | Fa8/1  | Cobre  | Fa9/1  | SW-NUCLEO-02               |
| SW-NUCLEO-02(1)   | Fa9/1  | Cobre  | Fa6/1  | SW-NUCLEO-02               |
| SW-NUCLEO-02      | Fa2/1  | Fibra  | Fa4/1  | Switch7                    |
| SW-NUCLEO-02(1)   | Fa2/1  | Fibra  | Fa5/1  | Switch8                    |
| Switch7           | Fa5/1  | Fibra  | Fa1/1  | SW-NUCLEO-02               |
| Switch8           | Fa4/1  | Fibra  | Fa1/1  | SW-NUCLEO-02(1)            |
| Server1           | Fa0    | Cobre  | Fa5/1  | SW-NUCLEO-02(1)            |

### Acesso (switches de borda para PCs/Laptops)

| Origem    | Porta  | Cabo  | Porta  | Destino  |
|-----------|--------|-------|--------|----------|
| Switch8   | Fa0/1  | Cobre | Fa0/1  | Switch9  |
| Switch8   | Fa1/1  | Cobre | Fa0/3  | Switch10 |
| Switch7   | Fa0/1  | Cobre | Fa0/3  | Switch11 |
| Switch7   | Fa1/1  | Cobre | Fa0/3  | Switch12 |
| PC1       | Fa0    | Cobre | Fa0/2  | Switch9  |
| PC2       | Fa0    | Cobre | Fa0/3  | Switch9  |
| PC3       | Fa0    | Cobre | Fa0/1  | Switch10 |
| PC4       | Fa0    | Cobre | Fa0/2  | Switch10 |
| Laptop1   | Fa0    | Cobre | Fa0/1  | Switch11 |
| Laptop2   | Fa0    | Cobre | Fa0/2  | Switch11 |
| Laptop3   | Fa0    | Cobre | Fa0/1  | Switch12 |
| Laptop4   | Fa0    | Cobre | Fa0/2  | Switch12 |

---

## 🌐 Endereçamento IP (Extra)

Rede: **192.168.10.0/24**
Máscara de sub-rede: **255.255.255.0**

| Dispositivo | Endereço IP | Máscara | DNS |
|---|---|---|---|
| PC0 | 192.168.10.2 | 255.255.255.0 | — |
| PC0(1) | 192.168.10.3 | 255.255.255.0 | — |
| PC0(2) | 192.168.10.4 | 255.255.255.0 | — |
| PC0(3) | 192.168.10.5 | 255.255.255.0 | — |
| Laptop0 | 192.168.10.6 | 255.255.255.0 | — |
| Laptop0(1) | 192.168.10.7 | 255.255.255.0 | — |
| Laptop0(2) | 192.168.10.8 | 255.255.255.0 | — |
| Laptop0(3) | 192.168.10.9 | 255.255.255.0 | — |
| Server0 | 192.168.10.100 | 255.255.255.0 | 8.8.8.8 |

---

## ✅ Checklist de Requisitos Atendidos

- [x] Estrutura hierárquica visível (núcleo, distribuição, borda)
- [x] Roteador com duas interfaces FastEthernet ligadas a dois switches de núcleo
- [x] Ligação física entre os switches de núcleo (preparada para 4 Gbps)
- [x] Ligação individual dos switches de núcleo aos switches de distribuição via fibra óptica (preparada para 2 Gbps)
- [x] Quatro switches de borda sem redundância
- [x] Quatro desktops, quatro notebooks e um servidor conectados com fio
- [x] Endereçamento IP configurado nos dispositivos finais (extra)

---

## 🛠️ Ferramentas

- Cisco Packet Tracer

---
