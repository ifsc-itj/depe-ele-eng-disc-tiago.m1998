# Título do Trabalho

## Introdução

[Apresentar o tema do trabalho.]

## Revisão da literatura

# Revisão da Literatura: Análise Comparativa de Topologias e Implementações de Bobinas de Tesla de Estado Sólido para Aplicações Didáticas

## 1.0 Introdução: A Evolução para Topologias de Estado Sólido e a Justificativa do Projeto

A bobina de Tesla, inventada por Nikola Tesla em 1891, é um transformador ressonante com núcleo de ar capaz de gerar tensões extremamente elevadas em altas frequências. Tradicionalmente, o acionamento desses dispositivos era realizado por meio de um centelhador (*spark gap*), que atuava como uma chave de alta velocidade para descarregar um capacitor no enrolamento primário. Embora historicamente significativa, essa topologia clássica, conhecida como Spark Gap Tesla Coil (SGTC), apresenta limitações em termos de controle, eficiência e ruído.

O avanço da eletrônica de potência permitiu o desenvolvimento de topologias de estado sólido (Solid State Tesla Coil - SSTC), que substituem o centelhador por semicondutores como MOSFETs ou IGBTs, oferecendo um controle superior. O projeto em análise propõe a construção de uma bobina de Tesla em miniatura para fins didáticos, utilizando um circuito oscilador com o CI 555 e um IGBT para o chaveamento. A escolha pela topologia de estado sólido é fundamental para permitir a modulação por áudio, um dos objetivos do projeto.

Uma análise comparativa entre uma Rotary Spark Gap Tesla Coil (RSGTC) e uma Double Resonant Solid State Tesla Coil (DRSSTC) demonstra a superioridade da abordagem de estado sólido. A DRSSTC apresentou quase o dobro da eficácia (relação entre o comprimento do arco e a potência de entrada), operação mais silenciosa e menor estresse sobre os componentes. A vantagem mais pertinente é a **maior controlabilidade**, um pré-requisito técnico para a modulação de áudio, que é alcançada pelo controle instantâneo da frequência e duração dos pulsos de potência. Em contraste, uma RSGTC fica presa a uma frequência de modulação baixa e fixa, tornando a reprodução de áudio fiel impossível. Portanto, a adoção de uma topologia de estado sólido é uma necessidade funcional para o projeto.

---

## 2.0 Análise de Circuitos de Acionamento: O Oscilador como Coração Eletrônico

O núcleo de qualquer SSTC é seu circuito de acionamento (*driver*), que define a estabilidade, eficiência e complexidade do sistema. O projeto em questão propõe uma arquitetura de oscilador externo não ressonante, utilizando o CI 555.

### 2.1 Estudo de Caso de Alta Relevância: A SSTC Musical de "Electroboom"

Um trabalho análogo relevante é a SSTC musical de pequena escala documentada por "Electroboom" (2015), que serve como uma valiosa fonte de dados comparativos. O objetivo do trabalho foi construir uma SSTC capaz de modular arcos elétricos para produzir música.

**Diferenças com o Projeto em Análise:**

1.  **Circuito Oscilador:** Utiliza um oscilador com comparador *trigger de Schmitt* (CI MCP6562) em vez do 555. A frequência é ajustável para sintonizar a ressonância da bobina (~1 MHz).
2.  **Chave de Potência:** Utiliza quatro MOSFETs em paralelo (SCT2450KEC, 1200 V, 10 A) em vez de um único IGBT, para distribuir a corrente e o calor.

**Resultados e Análise:**

* **Pontos Positivos:** O trabalho oferece um guia prático e detalhado de construção, lista de componentes, esquemático e dicas cruciais de montagem e depuração. Recomendações como o uso de ferramentas de plástico para sintonia e a necessidade de um bom dissipador de calor são diretamente aplicáveis.
* **Pontos Negativos (Oportunidade/Desafio):** O autor descreve o circuito como "muito difícil de sintonizar e operar e pode explodir facilmente". A causa é a falta de um mecanismo de feedback para autoajuste da frequência de ressonância, que varia dinamicamente. Como o oscilador tem frequência fixa (ajustada manualmente), qualquer desvio da ressonância real diminui drasticamente a eficiência e aumenta o estresse nos componentes. Este é o desafio técnico central que o projeto com o CI 555 também enfrentará.

### 2.2 O Circuito Integrado 555: Compromisso entre Simplicidade e Estabilidade

A escolha do CI 555 representa um compromisso entre a simplicidade de implementação e o baixo custo, ideais para um projeto de aprendizado, e a estabilidade de desempenho.

A literatura confirma que um 555 pode ser usado, mas alerta para duas questões: a necessidade de um **driver de gate** dedicado para a chave de potência e as limitações de frequência do próprio CI (o NE555 opera confiavelmente até ~500 kHz). Soluções com 555 são vistas como funcionais, mas menos precisas e estáveis que alternativas mais avançadas.

O principal desafio é que a topologia de oscilador fixo é inerentemente sensível a desalinhamentos de frequência. Qualquer desvio da ressonância dinâmica da bobina aumenta a impedância vista pelo estágio de potência, reduzindo a transferência de energia e podendo levar à falha do IGBT por superaquecimento. Isso torna a etapa de **Testes e Ajustes** a fase mais crítica do desenvolvimento, focada em implementar um método de sintonia fina e caracterizar a sensibilidade do sistema.

---

## 3.0 Análise do Estágio de Potência: A Escolha do IGBT e Topologias de Acionamento

A escolha do componente de chaveamento é crítica para a frequência de operação e a capacidade de potência. O projeto especifica o uso de um IGBT.

IGBTs são comuns em SSTCs de maior potência, geralmente em configurações de ponte-H ou meia-ponte, que são mais complexas. Em contraste, projetos de baixa potência, como o de "Electroboom", costumam usar MOSFETs. A combinação de um oscilador simples (555) com um IGBT (geralmente para maior potência) é uma dissonância que apresenta desafios.

IGBTs são geralmente mais lentos que MOSFETs, o que limita a frequência máxima de operação. Enquanto sistemas com IGBTs podem operar a frequências mais baixas (ex: 22 kHz), para arcos visualmente atraentes, frequências de 100 kHz a 500 kHz são desejáveis. Portanto, é imperativo selecionar um IGBT **fast-switching** (de comutação rápida).

Além disso, o desempenho de comutação depende criticamente do **circuito de gate driver**, que deve ser capaz de fornecer e drenar picos de corrente significativos para carregar e descarregar o gate do IGBT rapidamente. Um driver inadequado causa perdas de potência, superaquecimento e falha do dispositivo. A metodologia do projeto deve prever o projeto cuidadoso de um gate driver robusto.

---

## 4.0 Benchmarking de Desempenho e Otimização do Projeto Físico

O desempenho de uma bobina de Tesla não é determinado apenas pela eletrônica, mas também, de forma crítica, pela geometria e construção dos enrolamentos.

### 4.1 Benchmarks de Tensão e Frequência

A literatura fornece pontos de referência para contextualizar os resultados:

* **Pranoto et al. (2023):** Sistema com IGBT gerando 150 kV a 22 kHz.
* **Plangklang et al. (2024):** Simulação de uma bobina para atingir 120 kV a 120 kHz.

O projeto deverá medir sua frequência de operação e estimar a tensão de saída (aproximadamente 10 kV por polegada de arco) para uma avaliação qualitativa em comparação com esses benchmarks.

### 4.2 Otimização da Geometria dos Enrolamentos

O trabalho de Plangklang et al. (2024) destaca que negligenciar a otimização do transformador é um erro comum. O estudo buscou otimizar o campo elétrico entre os enrolamentos para evitar descargas internas (*flashover*) que podem danificar o dispositivo.

* **Conclusão Principal:** A geometria física tem um impacto direto no desempenho. Um **enrolamento primário com formato cônico (ângulo de 60 graus)** resulta em uma distribuição de campo elétrico mais favorável, reduzindo o risco de descarga interna e permitindo maior tensão de saída em comparação com um enrolamento plano tradicional.

**Implicações para o Projeto:** A etapa de "Definir características construtivas da bobina de tesla" deve ser vista como uma oportunidade para investigação experimental. A metodologia pode ser enriquecida para incluir a construção e o teste de diferentes geometrias de enrolamento primário, medindo o impacto no desempenho.

---




### Recomendações Finais

1.  **Metodologia de Sintonia:** Dedicar uma parte substancial dos testes à caracterização quantitativa da sensibilidade à frequência do oscilador. Recomenda-se desenvolver um procedimento de sintonia manual robusto, utilizando um potenciômetro de precisão, e documentar o desempenho em função de desvios da frequência de ressonância.
2.  **Seleção e Acionamento de Componentes:** A escolha do IGBT deve ser refinada para um modelo *fast-switching*. O projeto do circuito de gate driver não pode ser subestimado e deve ser projetado para fornecer a corrente de pico especificada pelo fabricante para garantir comutação rápida e minimizar perdas.
3.  **Otimização Experimental da Construção Física:** O projeto pode ser enriquecido ao incorporar uma fase de otimização experimental, testando empiricamente diferentes geometrias para o enrolamento primário (e.g., helicoidal plano vs. cônico).
4.  **Reforço dos Protocolos de Segurança:** A metodologia de segurança deve ser reforçada com base nas advertências práticas, incluindo os riscos de queimaduras graves por RF (que não requerem contato direto) e a necessidade de usar ferramentas de ajuste não condutivas, conforme destacado por "Electroboom". A interferência eletromagnética (EMI) gerada também é um risco que deve ser comunicado.

---

## Referências

1.  **Plangklang, A., Pattanadech, N., & Yutthagowith, P. (2024).** *Simulation and Analysis of the Optimal Electric Field from Modifications to the Winding Design for the Tesla Transformer*. Applied Sciences, 14(3), 1279.
2.  **Wasatonic, E. (2014).** *Comparison of Tesla Coil Driver Topologies*. High Voltage Hot Dog.
3.  **Electroboom. (2015, May 26).** *Making a Solid State Tesla Coil that Plays Music*. Electroboom.com.
4.  **Pranoto, H. et al. (2023).** *COMPARISON OF INSULATION TESTING IN LABORATORY*. IJICIC.
5.  **Pranoto, H. et al. (2023).** *Development of musical solid-state Tesla coil based on pulse...*.


## Materiais e Métodos

### Materiais

# Lista de materiais

| Componente | Quantidade |
| --- | --- |
| IGBT de alta potência (FGA60N65SMD) | 2 |
| CI driver de gate (UCC27425) | 1 |
| CI inversor hexagonal Schmitt trigger (SN74HC14AN) | 1 |
| Temporizador 555 (NE555P) | 1 |
| Regulador de tensão linear de 12V (L7812CV) | 1 |
| Regulador de tensão linear de 5V (L7805CV) | 1 |
| Diodo (1N4148) | 4 |
| Diodo (1N4007) | 2 |
| Capacitor eletrolítico (25V/220uF) | 1 |
| Capacitor eletrolítico (25V/470uF) | 2 |
| Resistor (5K Ω) | 1 |
| Resistor (6.8 Ω) | 2 |
| Resistor (50K Ω) | 1 |
| Resistor (2.2K Ω) | 1 |
| Resistor (1K Ω) | 1 |
| Potenciômetro (1M Ω) | 2 |
| Potenciômetro (50K Ω) | 1 |
| Chave Liga/Desliga | 2 |
| Capacitor cerâmico (1uF) | 1 |
| Capacitor de filme (0.1uF) | 2 |
| Capacitor cerâmico (0.33uF) | 1 |
| Capacitor cerâmico (10uF) | 1 |
| Capacitor de filme (0.82uF) | 2 |
| Núcleo de ferrite toroidal | 1 |
| Dissipador de calor (TO-247) | 2 |
| Soquete para CI (DIP-14) | 1 |
| Soquete para CI (DIP-8) | 2 |
| Conector borne em bloco | 3 |
| Transformador (12VAC) | 1 |
| Ponte retificadora (>25V) | 1 |
| Capacitor eletrolítico (>250V / >500uF) | 2 |
| Termistor de Inrush (SL32 1 ohm) | 1 |
| Ponte retificadora (10A / 1000V) | 1 |

# Projeto Bobina de Tesla SSTC - Relatório Técnico

Este documento descreve a concepção, os testes e os resultados obtidos no desenvolvimento do protótipo de uma Bobina de Tesla de Estado Sólido (SSTC), baseada no projeto de referência "LabCoatz SSTC2.0 (Mjolnir)".

## 1. Descrição do Protótipo (Placa de Controle Principal - PCB)

O circuito de controle principal da SSTC foi selecionado por sua abordagem simplificada, que utiliza a própria frequência de ressonância da bobina secundária para o controle do chaveamento de potência, eliminando a necessidade de circuitos osciladores complexos.

O fluxo de operação do circuito é o seguinte:

1.  **Captura de Sinal:** Uma antena próxima à bobina secundária capta o campo eletromagnético, que contém a frequência de ressonância natural do sistema.
2.  **Filtragem e Condicionamento:** O sinal da antena é direcionado a um circuito integrado **74HC14 (Porta Lógica NOT com Schmitt Trigger)**. O sinal passa por duas portas inversoras em sequência. A função do Schmitt Trigger é garantir um sinal digital limpo, livre de ruídos, enquanto a dupla inversão restaura a fase original do sinal.
3.  **Circuito de Interrupção (555 Timer):** Em paralelo, um oscilador baseado no circuito integrado **555** gera um sinal de interrupção com frequência ajustável entre 30 Hz e 100 Hz e um ciclo de trabalho (duty cycle) variável de 10% a 50%. Este sinal é enviado ao pino "Enable" do driver dos IGBTs para controlar a potência total do sistema.
4.  **Driver de Potência (Gate Driver):** O sinal de ressonância (do 74HC14) e o sinal de interrupção (do 555) são enviados a um driver de IGBTs, responsável por fornecer a corrente necessária para acionar os transistores de potência.
5.  **Acoplamento e Isolação (GDT):** A saída do driver alimenta um **Gate Driver Transformer (GDT)**. Este transformador isola galvanicamente o circuito de controle (baixa tensão) do circuito de potência (alta tensão), protegendo os componentes de controle.
6.  **Chaveamento de Potência (IGBTs):** O GDT aciona os gates de dois IGBTs **FGA60N65**, que são responsáveis por chavear a alta tensão na bobina primária na frequência de ressonância.

## 2. Descrição dos Testes, Análise e Problemas Encontrados

Os testes foram focados na validação sequencial do circuito de controle e na operação inicial da bobina em baixa potência.

### 2.1. Teste de Chaveamento em Baixa Frequência
* **Objetivo:** Validar a lógica de funcionamento do circuito de controle.
* **Metodologia:** Utilizou-se o sinal de 60 Hz da rede elétrica, captado pelo circuito, para observar o comportamento do chaveamento em baixa frequência.
* **Resultado e Primeiro Problema Identificado:** Durante este teste, foi detectado um erro crítico de projeto relacionado ao componente do driver.
    * **Componente Esperado:** UCC27425 (possui uma saída normal e uma invertida).
    * **Componente Utilizado:** UCC27524 (adquirido por engano, possui duas saídas não-invertidas).
    * **Consequência:** A diferença de potencial nos terminais do GDT era sempre nula, impedindo o acionamento dos IGBTs.

### 2.2. Tentativa de Solução e Segundo Problema
* **Solução Implementada:** Foi realizada uma modificação ("jumper") para alimentar uma das entradas do driver com um sinal já invertido da primeira porta do 74HC14.
* **Resultado:** A modificação gerou com sucesso sinais invertidos na saída do driver, mas introduziu um novo problema: **Atraso de Propagação (Delay)**.
* **Análise do Problema:** Um sinal passava por uma porta lógica (delay ~83 ns), enquanto o outro passava por duas. Essa defasagem, em alta frequência, causa "tempos mortos", perda de potência e estresse nos componentes de potência.

### 2.3. Teste de Operação em Baixa Potência e Falha dos Componentes
* **Metodologia:** O protótipo foi testado com uma tensão de entrada reduzida (aprox. 150 Vac) apesar da defasagem de sinal.
* **Resultado:** A bobina funcionou e gerou faíscas, validando que o conceito geral era funcional.
* **Problemas Finais e Falha em Cascata:** Durante a operação, foi observado que a bobina secundária estava fisicamente danificada (fio rompido).
    * **Consequências do Dano:** Os rompimentos causaram arcos internos (curtos-circuitos), levando a surtos de corrente no circuito primário e à **queima de múltiplos componentes:** 4 drivers UCC27524, 1 regulador de tensão 7812 e 3 IGBTs.

## 3. Tabela Resumo dos Problemas

| Problema Identificado        | Causa Raiz                                                        | Solução Tentada / Próximo Passo                   | Resultado / Consequência                                          |
| :--------------------------- | :---------------------------------------------------------------- | :------------------------------------------------ | :---------------------------------------------------------------- |
| **Driver de IGBT Incorreto** | Compra do componente errado (UCC27524 em vez de UCC27425).         | Jumper utilizando sinal invertido do 74HC14.      | Gerou o problema de Atraso de Propagação (Delay).                 |
| **Atraso de Propagação** | Diferença no número de portas lógicas no caminho de cada sinal.     | N/A (requer componente correto).                  | Perda de potência no GDT, tempos mortos, estresse nos componentes. |
| **Bobina Secundária Rompida** | Dano físico preexistente ou ocorrido durante o manuseio.          | N/A (requer reparo/reconstrução da bobina).         | Curtos-circuitos internos, perda de potência, instabilidade.      |
| **Queima de Componentes** | Surtos de corrente causados pela combinação dos problemas acima. | Interrupção dos testes.                           | Perda de 4 drivers, 1 regulador e 3 IGBTs.                        |

## 4. Conclusão dos Testes

Apesar dos resultados práticos limitados, os testes permitiram validar a lógica fundamental do circuito e identificar com precisão uma cadeia de falhas. O aprendizado principal aponta para a necessidade da **substituição do driver pelo modelo correto (UCC27425)** e o **reparo ou reconstrução da bobina secundária** como passos cruciais para a continuidade e sucesso do projeto.
### Sugestões para trabalhos futuros

## 5. Sugestões de Trabalhos Futuros

Com base nos resultados e aprendizados obtidos, são propostos os seguintes trabalhos futuros para a correção, melhoria e evolução do projeto.

### 5.1. Correções e Melhorias Imediatas

Estes são os passos essenciais para tornar o protótipo atual funcional, estável e seguro.

* **Substituição do Driver de IGBTs:**
    * **Ação:** Substituir o CI `UCC27524` pelo modelo correto especificado no projeto original, o **`UCC27425`**.
    * **Justificativa:** Esta correção é fundamental para eliminar a defasagem de sinal (delay), garantir um chaveamento anti-fase perfeito (push-pull) no GDT e maximizar a transferência de potência para os IGBTs, resolvendo a causa raiz da ineficiência do circuito.

* **Reconstrução da Bobina Secundária:**
    * **Ação:** Construir uma nova bobina secundária, garantindo a integridade do enrolamento e a qualidade do isolamento.
    * **Justificativa:** Uma bobina secundária íntegra, com fio contínuo e múltiplas camadas de verniz de alta isolação, é vital para evitar arcos internos (curtos-circuitos), maximizar a ressonância e a tensão de saída, e prevenir surtos de corrente que danificam o circuito de controle.

* **Otimização da Placa Retificadora de Tensão:**
    * **Ação:** Redesenhar ou aprimorar o circuito de retificação de entrada.
    * **Melhorias Sugeridas:**
        * **Aumentar a Capacitância:** Adicionar mais capacitores de filtro para reduzir o *ripple* da tensão DC, fornecendo uma alimentação mais estável para a ponte de IGBTs.
        * **Implementar um Soft-Start:** Adicionar um circuito de partida suave (por exemplo, com um resistor de potência e um relé, ou um termistor NTC) para limitar a corrente de partida (*inrush current*) que carrega os capacitores, evitando que disjuntores desarmem e reduzindo o estresse sobre os diodos retificadores.
        * **Diodos Robustos:** Utilizar diodos de ponte retificadora com maior capacidade de corrente e tensão para aumentar a margem de segurança.

### 5.2. Evoluções e Aplicações Avançadas

Após a validação do protótipo corrigido, o projeto pode evoluir para incorporar funcionalidades mais complexas e explorar aplicações fascinantes.

* **Implementação:** Substituir o circuito interrupter baseado no 555 por uma interface que aceite uma entrada de áudio, idealmente utilizando fibra óptica para isolamento e segurança do equipamento de som (PC, celular).

* **Implementação de Proteções Robustas:**
    * **Conceito:** Adicionar circuitos de proteção ativa para evitar a queima de componentes em caso de falhas.
    * **Implementação:** Desenvolver um circuito de **proteção contra sobrecorrente (OCD - Over-Current Detection)**. Utilizando um transformador de corrente no primário da bobina, o circuito pode desligar o sinal do interrupter instantaneamente se a corrente ultrapassar um limite seguro.

* **Evolução para DRSSTC (Dual Resonant Solid State Tesla Coil):**
    * **Conceito:** O próximo passo em performance. Adicionar um capacitor de ressonância em série com a bobina primária, criando um segundo circuito ressonante.
    * **Benefício:** A dupla ressonância permite uma transferência de energia muito mais eficiente entre o primário e o secundário, resultando em arcos elétricos significativamente maiores e mais potentes com a mesma alimentação.

* **Exploração de Transmissão de Energia Sem Fio:**
    * **Conceito:** Utilizar o campo eletromagnético de alta frequência gerado pela bobina para alimentar dispositivos à distância.
    * **Demonstração:** Realizar experimentos práticos como acender lâmpadas fluorescentes, incandescentes ou LEDs a metros de distância da bobina, sem qualquer conexão física, demonstrando os princípios de Nikola Tesla.

## Referências

### Tabela 1: Matriz Comparativa de Trabalhos de Referência

| Referência (Autor, Ano) | Topologia Principal | Circuito Oscilador | Chave de Potência | Desempenho Notável | Pontos Fortes (Relevância para o Projeto) | Pontos Fracos (Oportunidades/Desafios para o Projeto) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Wasatonic, Ε. (2014)** | DRSSTC vs. RSGTC | Feedback / Gerador de Função | IGBT (Ponte-H) | Análise comparativa de eficácia e ruído | Justifica a escolha da tecnologia de estado sólido pela sua controlabilidade e eficiência superiores. | Foco na topologia DRSSTC, que é mais complexa que a SSTC proposta; a análise não é diretamente aplicável ao driver simples. |
| **"Electroboom" (2015)** | SSTC Musical | Trigger de Schmitt (Não-Ressonante) | MOSFETs (Paralelo) | Modulação de áudio com PWM; operação >32V. | Análogo mais próximo; guia prático de construção e depuração; demonstração da modulação de áudio. | Instabilidade de sintonia (sem feedback), exigindo ajuste manual constante. Desafio central para o projeto. |
| **Pranoto, H. et al. (2023)** | SSTC (Teste de Isolação) | Driver de Ponte-H | IGBTs (Ponte-H) | 150 kV @ 22 kHz. | Fornece um benchmark de desempenho para um sistema baseado em IGBT; valida o uso de IGBTs para alta tensão. | Escala industrial; frequência de operação muito baixa para uma aplicação musical; topologia de driver complexa. |
| **Plangklang, A. et al. (2024)** | SSTC (Simulação) | N/A (Foco em geometria) | N/A | Otimização de campo elétrico via geometria do enrolamento. | Destaca a importância crítica da construção física (ângulo do primário) para o desempenho, além da eletrônica. | Requer software de simulação FEM especializado; o método não é diretamente replicável, mas o princípio sim. |

