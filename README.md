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

```
                              [Router0 - 2811]
                         (2 interfaces FastEthernet)
                                   |
                 -----------------------------------
                 |                                 |
         [Switch0 - Núcleo] ==(link 4Gbps)== [Switch0(1) - Núcleo]
                 |  \                       /   |
                 |   \   (fibra, 2Gbps)    /    |
                 |    \                   /     |
                 |     \                 /      |
     [Switch0(2) - Distribuição]   [Switch0(3) - Distribuição]
             /        \                    /        \
      [Switch1]   [Switch2]          [Switch3]   [Switch4]
        (borda)     (borda)           (borda)     (borda)
        /    \       /    \            /    \      /  |  \
     PC0   PC0(3) PC0(2) PC0(1)  Laptop0 Laptop0(3) L0(2) L0(1) Server0
```

### Camadas da rede

| Camada | Função | Dispositivos |
|---|---|---|
| **Núcleo** | Interliga o roteador à rede e concentra o backbone com link preparado para agregação de 4 Gbps | Switch0, Switch0(1) |
| **Distribuição** | Recebe as conexões de fibra óptica dos switches de núcleo (2 Gbps) e distribui para a borda | Switch0(2), Switch0(3) |
| **Borda (acesso)** | Conecta diretamente os dispositivos finais, sem redundância | Switch1, Switch2, Switch3, Switch4 |
| **Dispositivos finais** | Estações de trabalho e servidor conectados por cabo | 4 desktops, 4 notebooks, 1 servidor |

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

## 👤 Autor

Atividade desenvolvida como parte da disciplina de **Comutação de Redes**.
