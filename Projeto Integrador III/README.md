<div align="center">
  <h1>⚡ Bobina de Tesla SSTC Auto-Ressonante ⚡</h1>
  <h3>Um projeto sobre altas tensões e eletrônica de potência.</h3>
</div>

![WhatsApp Image 2025-07-15 at 15 45 51](https://github.com/user-attachments/assets/64fe321e-3e05-499b-8fcf-7dbae68f992a)
<div align="center">
  <p>🤖 IMAGEM GERADA POR IA 🤖</p>
</div>

<div align="center">
  <kbd>Eletrônica de Potência</kbd>
  <kbd>SSTC</kbd>
  <kbd>Projeto Acadêmico</kbd>
  <kbd>Alta Tensão</kbd>
  <kbd>IGBT</kbd>
</div>

<br>

<div align="center">
  <p>Este repositório documenta a aventura de projetar, construir e testar uma Bobina de Tesla de Estado Sólido (SSTC) baseada no projeto <b>"LabCoatz SSTC2.0 (Mjolnir)"</b>. O objetivo era criar um dispositivo funcional e, mais importante, aprender com o processo. E aprendizados não faltaram!</p>
</div>

---

## 🎬 O Resultado (Antes da Catástrofe)
Apesar dos desafios, a bobina funcionou! Conseguimos gerar arcos em baixa potência, validando o conceito fundamental do circuito auto-ressonante.

<div align="center">

https://github.com/user-attachments/assets/8da18443-600b-4ca2-9458-0d70e077268a

</div>

---

## 🎯 O Projeto em Resumo

* **Objetivo:** Construir uma Bobina de Tesla de Estado Sólido (SSTC) funcional.
* **Design de Referência:** [LabCoatz SSTC2.0 (Mjolnir)](https://www.instructables.com/Building-the-Ultimate-Solid-State-Tesla-Coil-MUSIC/).
* **Característica Principal:** Topologia **auto-ressonante**, onde o próprio feedback da bobina secundária controla o chaveamento, eliminando a necessidade de sintonia fina manual.
* **Status Final:** Operação parcial alcançada, seguida de uma cascata de falhas que se tornou uma excelente oportunidade de aprendizado.

---

## 🛠️ A Saga: Desafios e Diagnósticos
A engenharia real raramente segue o plano. Nossa jornada foi uma série de diagnósticos e soluções improvisadas.

<details>
<summary><strong>Problema 1: O Driver de IGBT Trocado</strong></summary>

- **O que aconteceu?** Compramos o CI driver `UCC27524` por engano, em vez do `UCC27425`. A diferença? O nosso CI tinha duas saídas iguais, enquanto o projeto exigia uma saída invertida da outra.
- **Consequência:** A diferença de potencial no transformador de gate (GDT) era sempre zero, e os IGBTs não chaveavam.
- **Diagnóstico:** As imagens do osciloscópio confirmaram que ambos os sinais de saída estavam em fase.

  | Saída 1 do Driver | Saída 2 do Driver |
  | :---: | :---: |
  | ![TEK0000](https://github.com/user-attachments/assets/b88411ab-c314-4f71-87cc-1b6a5fb81397) | ![TEK0001](https://github.com/user-attachments/assets/9357936c-9bb7-4fe2-a54b-4e049bcc59eb) |

</details>

<details>
<summary><strong>Problema 2: O Delay da Solução Improvisada</strong></summary>

- **O que fizemos?** Para inverter um dos sinais, fizemos um "jumper" pegando o sinal de um ponto anterior do circuito (após uma única porta inversora do 74HC14).
- **Consequência:** Funcionou, mas criou um **atraso de propagação (~83 ns)** entre os dois sinais, pois um passava por mais portas lógicas que o outro. Em alta frequência, isso causou perda de potência e estresse nos componentes.
- **Diagnóstico:** O osciloscópio mostrou claramente a defasagem entre os sinais de acionamento.

  <div align="center">
    <img src="https://github.com/user-attachments/assets/9221af4a-b3bb-411a-98b9-fda863bf625a" alt="Atraso de Propagação" width="600"/>
  </div>

</details>

<details>
<summary><strong>Problema 3: O Golpe Final e a Falha em Cascata</strong></summary>

- **O que aconteceu?** Mesmo com os problemas, testamos a bobina com tensão reduzida. Ela funcionou, mas descobrimos que o **enrolamento secundário estava fisicamente danificado**.
- **Consequência:** Os fios rompidos causaram curtos-circuitos internos (arcos entre as espiras), gerando surtos de corrente que o circuito de controle não suportou.
- **Resultado Final:** Queima de **4 drivers, 3 IGBTs e 1 regulador de tensão**. Um final explosivo para uma grande jornada de aprendizado.
  
</details>

---

## 📚 Relatório Completo e Análise Técnica

Toda a análise detalhada, revisão de literatura, esquemáticos e conclusões estão documentados no relatório completo do projeto.

➡️ **[Acesse o Relatório Técnico Completo aqui](./Entrega%20final.md)**

---
