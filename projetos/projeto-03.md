<div align="center">

<h1>🔐 Projeto Parcial</h1>
<h2>Armário Inteligente de Equipamentos</h2>
<p><strong>Construa um sistema que ajude a proteger os equipamentos e componentes eletrônicos da escola.</strong></p>
<p><code>Arduino</code> • <code>Sensores</code> • <code>Botão</code> • <code>LEDs</code> • <code>Buzzer</code> • <code>Simulador e montagem física</code></p>

</div>

---

## 🎯 Situação-problema

A escola guarda placas Arduino, componentes eletrônicos, cabos e outros materiais em um armário. Em alguns momentos, a porta pode ficar aberta depois que alguém retira um equipamento. Além de facilitar a perda de materiais, a abertura deixa entrar mais luz e pode indicar que o armário não foi fechado corretamente.

Sua equipe foi convidada a desenvolver o protótipo de um **sistema de monitoramento para esse armário**. O sistema deverá utilizar um sensor de luminosidade para perceber a condição do ambiente interno, permitir o ajuste da sensibilidade e avisar quando encontrar uma situação que precisa de atenção.

O projeto poderá ser construído e testado em **um dos ambientes**:

1. no simulador Tinkercad;
2. em um Arduino físico.

> [!IMPORTANT]
> Este é um protótipo didático. Ele representa o funcionamento de um sistema de proteção, mas não deve ser utilizado como dispositivo real de segurança, controle de acesso ou proteção contra incêndio.

## 💡 O que o sistema pode resolver

O protótipo poderá:

- identificar uma mudança de luminosidade que represente a abertura do armário;
- permitir que o usuário ajuste a sensibilidade da detecção;
- indicar visualmente quando a condição estiver normal ou em alerta;
- emitir um aviso sonoro quando o armário parecer aberto;
- permitir o silenciamento temporário durante uma inspeção autorizada;
- mostrar as leituras e decisões no monitor serial;
- opcionalmente controlar uma trava representada por um servo ou monitorar a temperatura interna.

## 🧭 Visão geral

| Item | Orientação |
| --- | --- |
| 👥 Organização | Solo, dupla, trio ou quarteto |
| ⏱️ Tempo previsto | Três aulas de 50 minutos |
| 📋 Tipo de avaliação | Atividade parcial |
| 📦 Produto | Circuito, código, tabela de testes e apresentação |
| 🧩 Extensão | Escolher servo ou sensor de temperatura |

## 🚀 Objetivos de aprendizagem

Ao concluir o projeto, você deverá ser capaz de:

- planejar um sistema embarcado a partir de uma situação-problema;
- montar entradas e saídas em uma protoboard;
- realizar leitura digital e leitura analógica;
- utilizar condições para decidir o comportamento do sistema;
- ajustar um limite utilizando um potenciômetro;
- utilizar LEDs e buzzer para comunicar uma condição;
- organizar uma parte da leitura ou conversão em uma função;
- utilizar o monitor serial para testar e diagnosticar o circuito;
- transferir um projeto do simulador para o Arduino físico;
- identificar diferenças entre valores simulados e valores medidos no ambiente real.

## 🧰 Componentes

### Componentes obrigatórios

- 1 Arduino Uno;
- 1 placa de ensaio;
- 1 LDR / Fotoresistor;
- 1 resistor para formar o divisor de tensão do LDR;
- 1 potenciômetro;
- 1 botão;
- 1 buzzer;
- 1 LED verde;
- 1 LED vermelho;
- 2 resistores para os LEDs;
- jumpers;
- cabo de dados compatível com a placa.

O LED RGB poderá substituir os LEDs verde e vermelho, desde que as cores e conexões sejam utilizadas corretamente.

### Escolha uma extensão obrigatória

A equipe deverá escolher **uma** das opções:

#### Opção A — Trava com servo

- 1 servo motor.

O servo representará a trava do armário. O botão deverá permitir uma abertura autorizada e temporária.

#### Opção B — Monitoramento de temperatura

- 1 sensor de temperatura compatível com o simulador ou com o kit físico;
- resistor adicional, caso o sensor físico necessite de divisor de tensão.

O sistema também deverá alertar quando a temperatura ultrapassar um limite definido no código.

> [!WARNING]
> TMP36 e NTC de 10 kΩ são componentes diferentes. Se o simulador e o kit físico utilizarem sensores diferentes, a equipe deverá adaptar a montagem e a função de conversão. Não reutilize a fórmula do TMP36 em um NTC.

## ⚙️ Comportamento obrigatório

### 1. Leitura de luminosidade

O LDR deverá representar a condição interna do armário.

- Menor entrada de luz deverá representar o armário fechado.
- Maior entrada de luz deverá representar o armário aberto.
- A equipe deverá observar os valores reais antes de decidir qual comparação utilizar.

> [!NOTE]
> Dependendo da posição do LDR no divisor de tensão, o valor poderá aumentar ou diminuir quando houver mais luz. O código deve seguir o comportamento observado no circuito da equipe.

### 2. Ajuste pelo potenciômetro

O potenciômetro deverá ajustar o limite que separa a condição normal da condição de alerta.

O monitor serial deverá mostrar o valor lido pelo LDR e o limite selecionado pelo potenciômetro.

### 3. Sinalização visual

- O LED verde deverá indicar condição normal.
- O LED vermelho deverá indicar condição de alerta.
- Os dois LEDs não poderão permanecer ligados ao mesmo tempo durante o funcionamento comum.

### 4. Alerta sonoro

O buzzer deverá ser acionado quando o sistema detectar a condição de alerta.

Não é obrigatório produzir notas musicais. Se o kit físico utilizar um buzzer ativo, controle-o apenas como ligado ou desligado.

### 5. Botão de inspeção

Enquanto o botão estiver pressionado:

- o buzzer deverá permanecer silenciado;
- o monitor serial deverá informar `INSPECAO_AUTORIZADA`;
- a leitura do LDR deverá continuar sendo realizada;
- o LED deverá continuar mostrando a condição encontrada.

Ao soltar o botão, o alerta sonoro deverá voltar caso a condição de alerta ainda exista.

### 6. Monitor serial

O monitor serial deverá apresentar informações com nomes compreensíveis.

Exemplo:

```text
LDR=735 | LIMITE=620 | BOTAO=SOLTO | ESTADO=ALERTA | BUZZER=LIGADO
```

A mensagem não precisa ser idêntica ao exemplo, mas deverá permitir que outra pessoa compreenda o que o sistema está lendo e fazendo.

### 7. Organização do código

O código deverá:

- possuir nomes de variáveis compreensíveis;
- utilizar `setup()` somente para configurações iniciais;
- manter o funcionamento contínuo dentro de `loop()`;
- utilizar condições para decidir as saídas;
- possuir pelo menos uma função criada pela equipe;
- conter comentários curtos nas partes mais importantes;
- evitar trechos repetidos desnecessariamente.

A função poderá, por exemplo:

- realizar uma leitura;
- converter uma leitura analógica em tensão;
- atualizar os LEDs;
- acionar ou desligar o alerta;
- apresentar os dados no monitor serial.

## 🧩 Extensão escolhida

### Opção A — Trava representada pelo servo

Além dos requisitos principais:

- o servo deverá permanecer na posição de armário fechado durante o funcionamento normal;
- enquanto o botão estiver pressionado, o servo deverá movimentar-se para representar a abertura da trava;
- ao soltar o botão, o servo deverá retornar à posição fechada;
- a equipe deverá escolher e registrar os ângulos utilizados;
- o servo não poderá ser alimentado por um pino de entrada ou saída digital.

Na montagem física, conecte o sinal do servo ao pino definido no código, mantenha o GND em comum e utilize a alimentação indicada pelo professor. Caso o servo provoque tremores ou reinicializações, interrompa o teste e solicite a conferência da alimentação.

### Opção B — Monitoramento de temperatura

Além dos requisitos principais:

- o sensor deverá ser lido por uma entrada analógica;
- a conversão para temperatura deverá ficar em uma função;
- o monitor serial deverá apresentar a temperatura com a unidade utilizada;
- o código deverá possuir uma variável com o limite de temperatura;
- o alerta deverá ser acionado quando houver luminosidade de armário aberto **ou** temperatura acima do limite;
- a equipe deverá testar valores abaixo e acima do limite.

## ✅ Requisitos obrigatórios

### Planejamento

- [ ] A equipe compreendeu a situação-problema.
- [ ] As entradas e saídas foram identificadas antes da montagem.
- [ ] Os pinos utilizados foram registrados.
- [ ] A equipe escolheu a extensão com servo ou temperatura.
- [ ] Cada integrante recebeu uma responsabilidade inicial.

### Implementação no Tinkercad

- [ ] O circuito foi montado no Tinkercad.
- [ ] O LDR funciona como entrada analógica.
- [ ] O potenciômetro modifica o limite.
- [ ] O botão ativa a inspeção autorizada.
- [ ] Os LEDs indicam as condições normal e de alerta.
- [ ] O buzzer é acionado na condição de alerta.
- [ ] A extensão escolhida funciona.
- [ ] O monitor serial apresenta os dados necessários.
- [ ] O link do projeto foi salvo.

### Implementação no Arduino físico

- [ ] A montagem foi refeita na protoboard física.
- [ ] Os resistores dos LEDs foram utilizados.
- [ ] A polaridade dos componentes foi conferida.
- [ ] O circuito foi conferido antes da conexão do cabo USB.
- [ ] O LDR foi calibrado novamente no ambiente real.
- [ ] O limite foi testado com o potenciômetro físico.
- [ ] O botão, os LEDs e o buzzer funcionam.
- [ ] A extensão escolhida foi implementada ou teve sua falha diagnosticada.
- [ ] As diferenças em relação ao simulador foram registradas.

### Código e testes

- [ ] O código possui nomes de variáveis compreensíveis.
- [ ] Existe pelo menos uma função criada pela equipe.
- [ ] `setup()` e `loop()` são utilizados corretamente.
- [ ] Todas as leituras aparecem no monitor serial.
- [ ] A equipe executou todos os casos de teste.
- [ ] Pelo menos um problema foi corrigido ou explicado.
- [ ] Cada integrante consegue explicar uma parte do projeto.

## 🪜 Etapas do projeto

### 🟦 Planejamento e núcleo no simulador

1. Ler a situação-problema.
2. Identificar entradas, processamento e saídas.
3. Escolher a extensão da equipe.
4. Registrar os pinos que serão utilizados.
5. Montar LDR, potenciômetro, botão e LEDs no Tinkercad.
6. Programar as leituras e apresentá-las no monitor serial.
7. Implementar as condições normal e de alerta.
8. Salvar o link do projeto.

### 🟧 Alerta, extensão e testes no simulador

1. Acrescentar o buzzer.
2. Implementar o silenciamento durante a inspeção autorizada.
3. Implementar a extensão escolhida.
4. Organizar pelo menos uma parte do código em uma função.
5. Executar os casos de teste.
6. Solicitar a revisão de outra equipe.
7. Corrigir ou registrar os problemas encontrados.

### 🟩 Montagem e validação no Arduino físico

1. Desligar a alimentação antes de alterar conexões.
2. Refazer a montagem na protoboard física.
3. Solicitar a conferência do circuito antes da conexão USB.
4. Enviar o código para o Arduino.
5. Observar os valores físicos do LDR.
6. Ajustar comparações ou limites sem remover os requisitos.
7. Executar novamente os casos de teste.
8. Registrar pelo menos uma diferença entre simulador e circuito físico.
9. Demonstrar o sistema ao professor.

## 🧪 Casos de teste obrigatórios

| Teste | Condição preparada | Resultado esperado | Tinkercad | Arduino físico |
| --- | --- | --- | :---: | :---: |
| 1 | LDR representando armário fechado | LED verde ligado e buzzer desligado | ☐ | ☐ |
| 2 | LDR representando armário aberto | LED vermelho ligado e buzzer acionado | ☐ | ☐ |
| 3 | Alterar o potenciômetro | O limite apresentado e o momento do alerta mudam | ☐ | ☐ |
| 4 | Alerta ativo e botão pressionado | Buzzer silenciado e estado de inspeção informado | ☐ | ☐ |
| 5 | Soltar o botão com o armário ainda aberto | O alerta sonoro volta a ser acionado | ☐ | ☐ |
| 6 | Testar a extensão escolhida | Servo movimenta ou temperatura altera o alerta | ☐ | ☐ |

### Registro de diferenças

| Aspecto observado | Tinkercad | Arduino físico | Adaptação realizada |
| --- | --- | --- | --- |
| Valor com o armário fechado | | | |
| Valor com o armário aberto | | | |
| Limite escolhido | | | |
| Comportamento do buzzer | | | |
| Extensão | | | |

> [!TIP]
> Valores diferentes entre o simulador e o circuito físico não representam automaticamente um erro. Luz ambiente, posição dos componentes, tolerância dos resistores, alimentação e tipo de sensor podem alterar as leituras. O importante é medir, registrar e adaptar o sistema de forma justificada.

## 🔎 Revisão por outra equipe

| Verificação | Sim | Corrigir |
| --- | :---: | :---: |
| O monitor serial permite entender as leituras e decisões. | ☐ | ☐ |
| O potenciômetro realmente modifica o limite. | ☐ | ☐ |
| Os LEDs não indicam normal e alerta ao mesmo tempo. | ☐ | ☐ |
| O buzzer é silenciado somente durante a inspeção autorizada. | ☐ | ☐ |
| A extensão escolhida possui uma função coerente com o problema. | ☐ | ☐ |
| O código possui nomes compreensíveis e pelo menos uma função. | ☐ | ☐ |
| Os casos de teste foram executados. | ☐ | ☐ |

**Problema encontrado:** ________________________________________________

**Correção ou explicação:** _____________________________________________

## 📦 Entrega

A equipe deverá entregar:

1. link compartilhável do projeto no Tinkercad;
2. código final utilizado no Arduino físico;
3. duas capturas do simulador: uma em condição normal e outra em alerta;
4. uma fotografia da montagem física, sem rostos ou informações pessoais;
5. tabela dos casos de teste preenchida nos dois ambientes;
6. registro de pelo menos uma adaptação feita na passagem para o circuito físico;
7. demonstração do funcionamento ou diagnóstico da falha ao professor;
8. explicação da contribuição de cada integrante.

> [!IMPORTANT]
> A entrega precisa conter evidências do Tinkercad **OU** do Arduino físico. Uma falha de componente não causa perda automática dos pontos da montagem física quando a equipe apresenta o circuito, os testes realizados, o diagnóstico e a validação do professor.

## ⚠️ Cuidados na montagem física

- Desconecte o cabo USB antes de alterar a montagem.
- Utilize resistor em série com cada LED.
- Confira a polaridade dos LEDs e do buzzer.
- Não conecte diretamente os terminais de alimentação.
- Não alimente servo, buzzer ou outro atuador por um pino digital.
- Mantenha o GND comum quando for utilizada alimentação externa autorizada.
- Não utilize bateria de 9 V diretamente no servo.
- Interrompa o teste se a placa reiniciar, aquecer ou apresentar comportamento inesperado.
- Solicite a conferência do professor antes de energizar uma montagem sobre a qual a equipe tenha dúvida.

## ⭐ Desafios adicionais

Depois de concluir todos os requisitos, a equipe poderá:

- [ ] utilizar um LED RGB no lugar dos dois LEDs;
- [ ] acrescentar servo e temperatura no mesmo projeto;
- [ ] criar uma terceira condição visual de atenção;
- [ ] gerar um padrão de pulsos no buzzer;
- [ ] apresentar também a tensão calculada do sensor no monitor serial;
- [ ] construir uma pequena maquete de papelão para representar o armário, sem prender carga ao servo.

## 📚 Referências

- [Arduino — exemplos integrados de entradas, saídas, sensores e condições](https://docs.arduino.cc/built-in-examples)
- [Arduino — referência da linguagem](https://docs.arduino.cc/language-reference/)
- [Arduino — fundamentos de servo, alimentação e entradas analógicas](https://docs.arduino.cc/learn)
- [Autodesk — simulação e programação de Arduino no Tinkercad Circuits](https://www.autodesk.com/solutions/circuit-design-software)

---

<div align="center">

<h3>🧪 Simular, montar, medir e adaptar</h3>
<p><strong>O circuito físico não precisa repetir os mesmos números do simulador. Ele precisa demonstrar a mesma lógica e ser testado com cuidado.</strong></p>

</div>
