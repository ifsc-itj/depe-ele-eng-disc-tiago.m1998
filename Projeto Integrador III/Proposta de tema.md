> toda proposta de tema de projeto de PI3 deve seguir o padrão abaixo.

# Proposta de Tema de PI3
Título:

Aluno(s): Lucas H. Mendes e Tiago Moro

Orientador: Prof. Saimon Miranda Fagundes

# Objetivo geral
 - Construir uma réplica miniatura da bobina de tesla para fins didáticos sobre alta tensão

# Objetivos específicos
 - Definir características construtivas da bobina de tesla; 
 - Definir circuito gerador de tensão para o primário da bobina; 
 - Simular circuito em software de simulação eletrônico; 
 - Imprimir PCB do circuito; 
 - Verificar e melhorar a segurança para o uso da bobina.

# Metodologia

O desenvolvimento do projeto será conduzido em diversas etapas estruturadas para garantir a 
construção eficiente da bobina de Tesla em miniatura. As etapas incluem pesquisa, projeto, 
simulação, construção e testes, conforme descrito a seguir:

# 1. Pesquisa e Definição de Parâmetros
  - Levantamento teórico sobre o funcionamento da bobina de Tesla, princípios de alta tensão e 
aplicações didáticas.
  - Análise de diferentes configurações de bobinas de Tesla (clássica, ressonante, SSTC, 
DRSSTC) para escolha do modelo mais adequado.
  - Definição das características construtivas, incluindo dimensões, materiais, potência de 
operação e tipo de alimentação.
# 2. Projeto do Circuito e Especificação de Componentes
 - Desenvolvimento do circuito elétrico para excitação do primário da bobina, considerando 
fontes de alta tensão, transistores e drivers.
 - Escolha dos componentes eletrônicos e materiais para construção, como fio esmaltado, 
núcleo de PVC, capacitor de acoplamento, etc.
 - Definição da configuração do secundário (número de espiras, altura, relação de 
transformação).
# 3.  Simulação e Análise do Circuito
  - Utilização de software de simulação eletrônica (LTSpice, Proteus, Multisim ou outro) para 
validar o comportamento do circuito antes da construção.
  - Análise da ressonância entre o primário e o secundário para otimizar a eficiência da bobina.
  - Identificação e correção de possíveis problemas no projeto, como sobrecarga de 
componentes e perdas elétricas.
# 4. Fabricação da Placa de Circuito Impresso (PCB)
  - Desenvolvimento do layout da PCB utilizando software apropriado (KiCad, Eagle, Altium, 
etc.).
  - Impressão e fabricação da PCB utilizando método químico ou CNC, conforme 
disponibilidade.
  - Soldagem e montagem dos componentes eletrônicos na PCB.
# 5. Construção da Bobina de Tesla
  - Enrolamento das bobinas primária e secundária, garantindo isolamento adequado.
  - Montagem mecânica da estrutura e fixação dos componentes.
  - Interligação do circuito com a bobina e fontes de alimentação.
# 6. Testes e Ajustes
  -  Testes de funcionamento inicial, verificando tensão de saída e comportamento da bobina.
  -  Ajuste fino dos parâmetros para otimização do desempenho.
  -  Análise da emissão eletromagnética e possíveis interferências.
# 7.  Análise de Segurança e Melhorias
  - Identificação dos principais riscos associados à operação da bobina (choques elétricos, 
interferência em equipamentos, segurança contra incêndio).
  - Implementação de medidas de segurança, como blindagem eletromagnética, isolamento 
elétrico e proteções contra curto-circuito.
  - Elaboração de um manual de boas práticas para uso didático da bobina.

# Cronograma
Clique [aqui](https://github.com/orgs/ifsc-itj/projects/8/views/1) para acessar o cronograma.

# Lista de materiais

| Item | Descrição | Unidade | Valor Unitário (Calculado) | Quantidade | Total |
| :--- | :------------------------------------- | :---------- | :------------------------- | :---------- | :---------- |
| 01   | UCC27524                               | unidade     | R$ 5,18                    | 5           | R$ 25,91    |
| 02   | Capacitor 25V 470uF                    | unidade     | R$ 0,80                    | 20          | R$ 15,98    |
| 03   | KBU810                                 | peça        | R$ 2,41                    | 10          | R$ 24,10    |
| 04   | TBLOCK 2                               | peça        | R$ 3,50                    | 5           | R$ 17,48    |
| 05   | Interruptor ON/OFF                     | peça        | R$ 6,46                    | 2           | R$ 12,91    |
| 06   | Capacitor Filme Metalizado 400V 0.82uF | peça        | R$ 1,34                    | 10          | R$ 13,36    |
| 07   | Kit de capacitor monolítico            | kit         | R$ 19,25                   | 1 (180pçs)  | R$ 19,25    |
| 08   | Potenciômetro 50k                      | peça        | R$ 3,02                    | 5           | R$ 15,09    |
| 09   | Transformador eletrônico 220v para 12v | peça        | R$ 19,64                   | 1           | R$ 19,64    |
| 10   | Capacitor 25v 220uF                    | peça        | R$ 0,26                    | 50          | R$ 13,11    |
| 11   | Dissipador de calor                    | peça        | R$ 3,74                    | 10          | R$ 37,40    |
| 12   | Kit de diodos schottky                 | kit         | R$ 19,60                   | 1 (100pçs)  | R$ 19,60    |
| 13   | FGA60N65                               | peça        | R$ 8,16                    | 5           | R$ 40,82    |
| 14   | NE555                                  | peça        | R$ 2,52                    | 10          | R$ 25,22    |
| 15   | SN74HC14N                              | peça        | R$ 1,42                    | 10          | R$ 14,20    |
| 16   | Kit resistor 1/4W                      | kit         | R$ 25,40                   | 1 (600pçs)  | R$ 25,40    |
| 17   | Filamento PLA                          | rolo (1kg)  | R$ 110,44                  | 1           | R$ 110,44   |
| 18   | Cano PVC 75mm                          | metro       | R$ 10,00                   | 1           | R$ 10,00    |
| 19   | Fio de cobre esmaltado 34AWG           | rolo (100g) | R$ 64,18                   | 1           | R$ 64,18    |
| 20   | Fio de cobre esmaltado 14AWG           | rolo (100g) | R$ 65,90                   | 1           | R$ 65,90    |
| 21   | PCB impresso                           | unidade     | R$ 131.91                  | 5           | R$ 131.91   |
|      | Total                                  |             |                            |             | **R$ 681,90** |

# Unidades curriculares envolvidas
> liste as unidades curriculares envolvidas com o tema escolhido
- Eletromagnetismo;
- Circuitos Elétricos;
- Eletrônica;
- Eletrônica de Potência;
- Conversão eletromecânica.
