CP4---Edge Computing
---

## 👥 Equipe

| Nome Completo | RM |
| :--- | :--- |
| `[Matheus Tonsa Martini]` | `[564454]` |
| `[Arthur Albertini Soares Pereira]` | `[565954]` |
| `[Sebastian Iriarte Gonzales]` | `[563619]` |
| `[Fabio Pereira Rogério Júnior]` | `[564005]` |
| `[Kauã Veloso Lima]` | `[561954]` |
---

## 📜 Sobre o Projeto

Este projeto, desenvolvido para o **Checkpoint 4**, implementa uma solução completa de Internet das Coisas (IoT) para o **monitoramento inteligente de vinherias**. Utilizando a plataforma **FIWARE** como backend, o sistema coleta dados ambientais em tempo real e permite o controle remoto de atuadores, simulando um ambiente de produção conectado e automatizado.

A solução é fundamentada no padrão **NGSI-v2** para garantir a interoperabilidade e escalabilidade, seguindo as melhores práticas de modelagem de dados inteligentes.

---

## 🏛️ Arquitetura da Solução

O fluxo de dados e comandos segue a arquitetura abaixo:

<div align="center">
  <img src="" src="https://github.com/user-attachments/assets/c9443e4c-1548-4578-8da2-33ed1eed6f30" />
" alt="Arquitetura da Solução" width="800"/>
</div>

1.  **Dispositivo de Borda (Edge):** Um **ESP32** com sensor LDR mede a luminosidade e envia os dados via protocolo MQTT.
2.  **IoT Agent:** Recebe os dados, traduz o protocolo e os repassa ao Orion Context Broker.
3.  **Orion Context Broker:** Gerencia o estado atual da entidade (`SmartLamp`), tratando-a como um "Digital Twin".
4.  **STH-Comet:** Uma subscrição no Orion garante que todas as alterações de `luminosity` sejam enviadas para o banco de dados de séries temporais, criando um histórico para análises.
5.  **Controle (Cloud-to-Edge):** Um usuário (via **Postman**) envia um comando (`on`/`off`) para a API do Orion, que o repassa ao IoT Agent e, finalmente, ao ESP32 para acionar o LED.

---

## 🛠️ Tecnologias e Ferramentas

| Categoria | Tecnologia/Ferramenta | Descrição |
| :--- | :--- | :--- |
| **Plataforma IoT** | **FIWARE** | Orquestra os componentes de backend para gerenciamento de contexto. |
| | ↳ Orion Context Broker | Gerencia entidades e seus estados em tempo real. |
| | ↳ IoT Agent for MQTT | Atua como gateway, traduzindo o protocolo MQTT para o padrão NGSI. |
| | ↳ STH-Comet | Armazena dados históricos de telemetria para consultas temporais. |
| **Hardware** | **ESP32 DEVKIT V1** | Microcontrolador com Wi-Fi integrado, atuando como dispositivo de borda. |
| **Simulador** | **Wokwi** | Plataforma online para simulação de circuitos eletrônicos e firmware. |
| **Cloud** | **Microsoft Azure** | Ambiente de nuvem onde a instância do FIWARE foi provisionada. |
| **API Client** | **Postman** | Ferramenta para testar, provisionar e interagir com a API do FIWARE. |

---

## 🚀 Como Executar

### Pré-requisitos

*   Uma instância do **FIWARE Descomplicado** rodando na nuvem.
*   **Postman** instalado para interagir com a API.
*   **Arduino IDE** ou **VS Code com PlatformIO** para o firmware.

### 1. Configuração do Backend FIWARE

A plataforma foi instalada seguindo o tutorial **FIWARE Descomplicado**. Para configurar a entidade e as subscrições, importe a coleção `FIWARE_Descomplicado.json` no Postman e execute os seguintes requests na ordem:

1.  `[IOT Agent MQTT] -> 2. Provisioning a Service Group`
2.  `[IOT Agent MQTT] -> 3. Provisioning a Smart Lamp`
3.  `[STH-Comet] -> 2. Subscribe Luminosity`

### 2. Configuração do Firmware

1.  Clone este repositório: `git clone [URL_DO_SEU_REPOSITORIO]`
2.  Abra o arquivo `firmware/esp32-ldr-sensor.ino`.
3.  Atualize as credenciais de Wi-Fi e o IP do seu servidor:
    ```cpp
    // Insira as credenciais da sua rede
    const char* ssid = "NOME_DA_SUA_REDE_WIFI";
    const char* password = "SENHA_DA_SUA_REDE_WIFI";
    
    // Insira o IP público do seu servidor FIWARE
    const char* fiware_host = "SEU_IP_AQUI";
    ```
4.  Faça o upload do firmware para o seu ESP32 ou cole o código no simulador Wokwi.

---

## 🎬 Links e Demonstração

Confira a solução em ação através dos links abaixo:

| Recurso | Link |
| :--- | :--- |
| 🌐 **Simulação no Wokwi** | (https://wokwi.com/projects/441246875648066561) |
| 🎥 **Vídeo de Demonstração** | `[COLE AQUI O LINK PÚBLICO DO SEU VÍDEO NO YOUTUBE/DRIVE]` |
| 📂 **Repositório de Referência** | [GitHub - FIWARE Descomplicado](https://github.com/fabiocabrini/fiware) |

---

Este README foi criado para ser claro, informativo e visualmente atraente. Espero que goste!

---
O que acha desta versão? Podemos ajustar mais algum detalhe ou adicionar outra seção se precisar.
