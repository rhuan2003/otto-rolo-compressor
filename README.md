# 🤖 Manual de Montagem e Modelagem: Otto Rolo Compressor

Este guia detalha o processo de montagem mecânica, eletrônica e a manipulação dos arquivos digitais no Autodesk Fusion 360 para a construção da variante do robô Otto com tração por rodas/esteiras e rolo compressor frontal.

---

## 📐 Etapa 1: Visualização e Projeto no Autodesk Fusion 360

Como os componentes estruturais deste robô não foram impressos em 3D de forma convencional, o modelo digital serve como gabarito exato para estudo físico, medições e adaptações em outros materiais (como MDF, acrílico ou papelão paraná).

### Como abrir e explorar o projeto:
1. **Instalação:** Baixe e instale o software [Autodesk Fusion 360](https://autodesk.com) (gratuito para estudantes e hobbistas).
2. **Importação:** No painel lateral de dados (*Data Panel*), clique em **Upload** e selecione o arquivo do robô (formatos `.f3d` ou `.step` localizados na pasta `3D_Models/`).
3. **Navegação (Órbita):** Utilize a ferramenta **Orbit** (atalho: segure a tecla `Shift` + botão do meio do mouse) para girar o robô em 360° e entender como o rolo compressor se encaixa no chassi inferior.

### Medição para Fabricação Manual:
* Ative a ferramenta **Measure** (atalho: tecla `I`) no Fusion 360.
* Clique nas arestas, faces ou diâmetros do chassi e do rolo compressor.
* Anote as dimensões em milímetros (mm) para recortar ou adaptar os blocos de materiais físicos que substituirão a impressão 3D.

---

## 🛠️ Etapa 2: Preparação dos Componentes Físicos

Antes de iniciar a montagem estrutural, separe todos os itens técnicos necessários:

* **Peças Estruturais:** Chassi inferior, cabeça do Otto e o conjunto do rolo compressor (projetados no Fusion 360).
* **Motores:** 2x Motores DC amarelos (com caixa de redução) e rodas de alta aderência.
* **Driver de Potência:** 1x Ponte H L298N (para o controle de velocidade e sentido dos motores).
* **Cérebro do Robô:** 1x Arduino Nano (acompanhado de seu Shield de expansão I/O).
* **Sensores e Comunicação:** 1x Sensor ultrassônico HC-SR04 e 1x Módulo Bluetooth HC-05.
* **Energia:** 1x Bateria LiPo 7.4V (ou duas células 18650) e cabos jumpers do tipo macho-fêmea.

---

## ⚙️ Etapa 3: Montagem Mecânica

Siga a sequência abaixo utilizando o modelo tridimensional do Fusion 360 como referência visual de posicionamento:

1. **Instalação dos Motores:** Posicione os dois motores DC amarelos nas cavidades laterais internas da base do chassi.
2. **Fixação Mecânica:** Utilize parafusos longos ou abraçadeiras plásticas de nylon para prender os motores firmemente à estrutura.
3. **Rodas:** Encaixe as rodas laterais sob pressão diretamente nos eixos dos motores DC.
4. **Mecanismo Frontal:** Alinhe o braço de suporte frontal e passe um eixo centralizado pelo rolo compressor para que ele gire livremente.
5. **Olhos do Robô:** Fixe o sensor ultrassônico HC-SR04 nos vãos circulares localizados na parte frontal da cabeça do robô.

---

## ⚡ Etapa 4: Conexões Eletrônicas

Realize o mapeamento elétrico dos cabos utilizando o guia de pinagem abaixo:

### Conexão dos Motores na Ponte H L298N
* **Motor Esquerdo:** Conecte os dois fios diretamente nos bornes de parafuso **OUT1** e **OUT2**.
* **Motor Direito:** Conecte os dois fios diretamente nos bornes de parafuso **OUT3** e **OUT4**.

### Conexão de Controle (Ponte H ao Arduino)
* **Pino IN1:** Conectar no pino digital **D2** do Arduino.
* **Pino IN2:** Conectar no pino digital **D3** do Arduino.
* **Pino IN3:** Conectar no pino digital **D4** do Arduino.
* **Pino IN4:** Conectar no pino digital **D5** do Arduino.

### Conexão do Sensor Ultrassônico (Olhos)
* **VCC:** Conectar no pino **5V** do Shield do Arduino.
* **Trigger:** Conectar no pino digital **D8** do Arduino.
* **Echo:** Conectar no pino digital **D9** do Arduino.
* **GND:** Conectar no pino **GND** do Shield do Arduino.

### Conexão do Módulo Bluetooth HC-05
* **VCC:** Conectar no pino **5V** do Arduino.
* **GND:** Conectar no pino **GND** do Arduino.
* **TXD:** Conectar no pino digital **D11** (Configurado como RX por software).
* **RXD:** Conectar no pino digital **D12** (Configurado como TX por software).

---

## 🔋 Etapa 5: Sistema de Alimentação e Energia

Siga este esquema para evitar quedas de conexão ou reinicializações do Arduino:

1. Conecte o cabo positivo (Vermelho) da bateria no borne marcado como **12V** da Ponte H L298N.
2. Conecte o cabo negativo (Preto) da bateria no borne marcado como **GND** da Ponte H.
3. Puxe um fio jumper do terminal **GND** da Ponte H para qualquer pino **GND** do Arduino (Aterramento unificado).
4. Puxe um fio jumper da saída regulada **5V** da Ponte H para o pino **VIN** ou **5V** do Arduino para alimentá-lo.

---

## 💻 Etapa 6: Programação e Testes

Finalize o projeto carregando o firmware no microcontrolador:

1. Conecte o cabo USB no Arduino Nano e plugue-o no computador.
2. Abra o código do robô na **Arduino IDE**.
3. Em *Ferramentas > Placa*, selecione **Arduino Nano** (Se necessário, mude o processador para *ATmega328P Old Bootloader*).
4. Selecione a **Porta COM** correta correspondente ao seu dispositivo.
5. Clique no botão de **Carregar (Seta para a direita)** e aguarde a mensagem de conclusão.
6. Desconecte o USB, ative a chave da bateria e coloque o robô em uma área aberta para testar.
