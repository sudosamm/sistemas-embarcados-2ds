<div align="center">

<h1>🍔 Projeto 04</h1>
<h2>Painel Interativo para Fast Food</h2>
<p><strong>Crie um painel no qual o cliente escolhe itens, confirma o pedido e acompanha o tempo de preparo.</strong></p>
<p><code>Arduino</code> • <code>LCD I²C</code> • <code>Botões</code> • <code>Arrays</code> • <code>Funções</code></p>

</div>

---

## 🎯 Situação-problema

Um pequeno fast food deseja disponibilizar um painel simples para que seus clientes possam escolher um item sem precisar utilizar teclado, tela sensível ao toque ou computador.

O equipamento possuirá somente **dois botões** e um **display LCD 16×2 com comunicação I²C**. Um botão será utilizado para avançar entre as opções ou responder “Sim”, enquanto o outro será utilizado para confirmar, responder “Não” ou receber o pedido.

Sua tarefa é desenvolver a simulação desse painel. O cliente deverá escolher um item, decidir se deseja adicionar algo mais, acompanhar uma contagem de 10 segundos e confirmar o recebimento do pedido.

> [!IMPORTANT]
> O projeto representa apenas o funcionamento da interface de um terminal de autoatendimento. Ele não realizará pagamentos nem controlará equipamentos reais de uma cozinha.

## 🧭 Visão geral

| Item | Orientação |
| --- | --- |
| 👤 Organização | Atividade individual ou em dupla |
| 📦 Produto | Circuito simulado, código e registro dos testes |
| 🖥️ Interface | Display LCD 16×2 com módulo I²C |
| 🎛️ Entradas | Dois botões |

## 🚀 Objetivos de aprendizagem

Ao concluir o projeto, você deverá ser capaz de:

- utilizar um array para armazenar os itens de um cardápio;
- percorrer os elementos de um array por meio de um botão;
- utilizar o mesmo botão com funções diferentes de acordo com a tela atual;
- organizar o programa em estados ou etapas de funcionamento;
- apresentar informações em um display LCD I²C;
- atualizar somente as partes necessárias da tela;
- construir uma contagem regressiva de 10 segundos;
- impedir que um único acionamento seja contado várias vezes;
- organizar partes do programa em funções;
- testar o fluxo completo de uma interface interativa.

## 🧰 Componentes

- 1 Arduino Uno;
- 1 display LCD 16×2 com módulo I²C;
- 2 botões;
- 1 placa de ensaio;
- jumpers.

Os botões podem ser configurados com `INPUT_PULLUP`. Nesse caso, o estado pressionado será `LOW` e não será necessário utilizar resistores externos para eles.

## 🍟 Cardápio

Os itens disponíveis deverão ser armazenados em um array. A equipe poderá escolher os produtos, mas deverá possuir pelo menos quatro opções.

Exemplo:

```cpp
const char* itensCardapio[] = {
  "Hamburguer",
  "Batata frita",
  "Refrigerante",
  "Sorvete"
};
```

Todos os nomes precisam ser legíveis no LCD. Abrevie um nome quando ele possuir mais de 16 caracteres.

Ao chegar ao último elemento do array e pressionar novamente o botão de avançar, a seleção deverá retornar ao primeiro item.

## 🎛️ Função dos botões

Os mesmos botões terão ações diferentes de acordo com a tela apresentada.

| Tela atual | Botão esquerdo | Botão direito |
| --- | --- | --- |
| Tela inicial | Sem ação | Iniciar o pedido |
| Escolha do item | Próximo item | Confirmar o item |
| Pergunta “Algo mais?” | Sim, escolher outro item | Não, finalizar o pedido |
| Preparando | Sem ação | Sem ação |
| Pedido pronto | Sem ação | Confirmar o recebimento |
| Agradecimento | Sem ação | Sem ação |

> [!NOTE]
> Neste projeto, a pergunta `Algo mais?` seguirá o mapeamento mostrado na Tela 3: o botão esquerdo significa **Sim** e o botão direito significa **Não**.

## 🖥️ Telas obrigatórias

### Tela 1 — Início

```text
Fast Food
Faça seu pedido
```

O botão direito deverá iniciar a escolha dos itens.

> [!NOTE]
> Se o display ou a biblioteca utilizada não apresentar corretamente o caractere `ç`, utilize `Faca seu pedido` e registre essa adaptação na entrega.

### Tela 2 — Escolha do item

```text
Hamburguer
<-Next | Conf->
```

A primeira linha deverá apresentar o item selecionado no array.

- O botão esquerdo mostra o próximo item.
- O botão direito confirma o item apresentado.

`Hamburguer` é apenas um exemplo. A primeira linha deverá mudar conforme a posição atual do array.

### Tela 3 — Adicionar outro item

```text
Algo mais?
<-Sim | Nao->
```

- Ao pressionar o botão esquerdo, o sistema deverá retornar à Tela 2 para permitir a escolha de outro item.
- Ao pressionar o botão direito, o pedido deverá ser finalizado e o preparo será iniciado.

Cada item confirmado deverá ser considerado parte do pedido antes que essa pergunta seja apresentada.

### Tela 4 — Preparando

Ao iniciar o preparo, o display deverá apresentar uma contagem regressiva de 10 segundos.

Exemplo inicial:

```text
Preparando...
Aguarde: 10s
```

Depois, a segunda linha deverá mostrar `9s`, `8s`, `7s` e assim por diante, até chegar a `0s`.

Durante essa contagem, os botões não deverão mudar de tela nem alterar o pedido.

### Tela 5 — Pedido pronto

```text
Pedido Pronto
Receber ->
```

O sistema deverá permanecer nessa tela até que o botão direito seja pressionado.

### Tela 6 — Agradecimento

```text
Obrigado
Pela compra
```

A mensagem deverá permanecer visível por um pequeno intervalo. Depois disso, o sistema deverá limpar os dados do pedido e retornar à Tela 1.

## 🔄 Fluxo obrigatório

```text
Tela inicial
    |
    | botão direito
    v
Escolha do item <----------------------+
    |                                  |
    | confirmar                        | deseja algo mais
    v                                  | botão esquerdo
Pergunta "Algo mais?" ----------------+
    |
    | botão direito: não
    v
Preparando — contagem de 10 segundos
    |
    v
Pedido pronto
    |
    | botão direito: receber
    v
Agradecimento
    |
    v
Tela inicial
```

## ⚙️ Requisitos obrigatórios

### Cardápio e pedido

- [ ] Possuir pelo menos quatro itens no cardápio.
- [ ] Armazenar os nomes dos itens em um array.
- [ ] Utilizar uma variável para indicar a posição selecionada no array.
- [ ] Retornar ao primeiro item depois de ultrapassar o último.
- [ ] Permitir a inclusão de mais de um item no mesmo pedido.
- [ ] Limpar o pedido anterior antes de iniciar um novo atendimento.

### Botões

- [ ] Utilizar dois botões.
- [ ] Fazer o botão esquerdo avançar entre os itens na Tela 2.
- [ ] Fazer o botão direito confirmar o item na Tela 2.
- [ ] Fazer o botão esquerdo representar “Sim” na Tela 3.
- [ ] Fazer o botão direito representar “Não” na Tela 3.
- [ ] Fazer o botão direito confirmar o recebimento na Tela 5.
- [ ] Garantir que um toque no botão produza apenas uma ação.

### Display

- [ ] Inicializar corretamente o LCD I²C.
- [ ] Utilizar as seis telas definidas no projeto.
- [ ] Apresentar o item selecionado na primeira linha da Tela 2.
- [ ] Manter as orientações dos botões na segunda linha.
- [ ] Apresentar no display a contagem de 10 até 0.
- [ ] Manter a Tela 5 visível até o cliente confirmar o recebimento.
- [ ] Retornar à Tela 1 depois do agradecimento.

### Organização do código

- [ ] Utilizar nomes de variáveis compreensíveis.
- [ ] Manter no `setup()` somente as configurações iniciais.
- [ ] Utilizar o `loop()` para controlar o funcionamento contínuo.
- [ ] Criar funções para organizar a apresentação das telas.
- [ ] Utilizar uma variável que identifique a tela ou estado atual.
- [ ] Evitar executar `lcd.clear()` continuamente dentro do `loop()`.
- [ ] Comentar as partes mais importantes da lógica.

## 🧠 Organização sugerida

O programa poderá utilizar uma variável para representar a etapa atual, por exemplo:

```cpp
int telaAtual = 1;
```

Outra possibilidade é utilizar constantes com nomes compreensíveis:

```cpp
const int TELA_INICIAL = 1;
const int TELA_ESCOLHA = 2;
const int TELA_ALGO_MAIS = 3;
const int TELA_PREPARANDO = 4;
const int TELA_PRONTO = 5;
const int TELA_AGRADECIMENTO = 6;
```

Também é recomendado criar funções como:

```text
mostrarTelaInicial()
mostrarItemSelecionado()
mostrarPerguntaAlgoMais()
prepararPedido()
mostrarPedidoPronto()
mostrarAgradecimento()
```

Os nomes podem ser diferentes, desde que permitam compreender a responsabilidade de cada função.

## 🛒 Registro de vários itens

Quando o cliente confirma um produto, sua posição no cardápio poderá ser armazenada em um segundo array.

Exemplo de planejamento:

```cpp
int pedido[5];
int quantidadeItens = 0;
```

Nesse exemplo, o pedido poderá possuir até cinco itens. Ao confirmar um produto, o índice selecionado poderá ser salvo em `pedido[quantidadeItens]`, e a quantidade deverá ser atualizada.

Se for adotado um limite, o programa deverá impedir a escrita além do tamanho do array. Ao atingir o limite, o sistema poderá finalizar o pedido automaticamente ou informar que o pedido está completo.

## 🖱️ Tratamento dos botões

Os botões configurados com `INPUT_PULLUP` apresentam:

- `HIGH` quando estão soltos;
- `LOW` quando estão pressionados.

O código deverá impedir que manter um botão pressionado faça o sistema avançar várias vezes. Para isso, você poderá:

- comparar o estado atual com o estado anterior;
- executar a ação somente no momento em que o botão passa de `HIGH` para `LOW`;
- ou aguardar o botão ser solto antes de permitir uma nova ação.

## 🪜 Etapas sugeridas

### 1. Planejamento

1. Escolha pelo menos quatro itens para o cardápio.
2. Verifique se os nomes cabem no display.
3. Registre os pinos do LCD e dos dois botões.
4. Desenhe o fluxo entre as seis telas.
5. Defina como o programa identificará a tela atual.

### 2. Cardápio interativo

1. Monte o LCD e os botões no simulador.
2. Crie o array do cardápio.
3. Apresente o primeiro item.
4. Faça o botão esquerdo percorrer o array.
5. Faça o botão direito confirmar o item.

### 3. Confirmação e pedido

1. Apresente a pergunta `Algo mais?`.
2. Faça o botão esquerdo retornar ao cardápio.
3. Faça o botão direito iniciar o preparo.
4. Registre os itens confirmados.
5. Defina um limite seguro para a quantidade de itens.

### 4. Preparo e finalização

1. Construa a contagem regressiva de 10 segundos.
2. Ignore os botões durante o preparo.
3. Apresente a Tela 5 ao terminar a contagem.
4. Aguarde a confirmação de recebimento.
5. Apresente o agradecimento.
6. Limpe o pedido e retorne à tela inicial.

### 5. Testes e correções

1. Execute todos os casos de teste.
2. Verifique se um toque gera somente uma ação.
3. Teste o retorno do último para o primeiro item.
4. Confirme se um novo cliente inicia com o pedido vazio.
5. Registre pelo menos um erro encontrado e sua correção.

## 🧪 Casos de teste obrigatórios

| Teste | Ação realizada | Resultado esperado | Resultado observado |
| --- | --- | --- | --- |
| 1 | Iniciar a simulação | Apresentar `Fast Food` e `Faça seu pedido` | |
| 2 | Pressionar o botão direito na Tela 1 | Abrir a seleção no primeiro item | |
| 3 | Pressionar o botão esquerdo na Tela 2 | Mostrar o próximo elemento do array | |
| 4 | Avançar depois do último item | Retornar ao primeiro elemento | |
| 5 | Confirmar um item | Apresentar `Algo mais?` | |
| 6 | Pressionar o botão esquerdo na Tela 3 | Voltar à seleção para adicionar outro item | |
| 7 | Pressionar o botão direito na Tela 3 | Iniciar a contagem de 10 segundos | |
| 8 | Pressionar botões durante o preparo | Não alterar o pedido nem interromper a contagem | |
| 9 | Aguardar a contagem terminar | Apresentar `Pedido Pronto` | |
| 10 | Não pressionar o botão na Tela 5 | Permanecer aguardando o recebimento | |
| 11 | Pressionar o botão direito na Tela 5 | Mostrar o agradecimento e retornar ao início | |
| 12 | Iniciar um novo atendimento | Não manter itens do pedido anterior | |

## 📦 Entrega

Entregue:

1. link compartilhável da simulação no tinkercad;
2. código completo e organizado em arquivo com extensão .cpp;
3. captura da Tela 2 mostrando um item do array;
4. captura da contagem regressiva;
5. captura da tela `Pedido Pronto`;
6. tabela de testes preenchida;
7. breve descrição de um problema encontrado e da solução utilizada.

Caso não seja possível compartilhar o link, envie o arquivo do código e capturas legíveis da simulação.

## 📊 Critérios de avaliação

| Critério | Pontuação |
| --- | ---: |
| Uso correto do array e navegação entre os itens | 1,0 |
| Funcionamento dos dois botões em cada tela | 1,0 |
| Organização das seis telas e do fluxo do pedido | 1,0 |
| Contagem regressiva e finalização do atendimento | 1,0 |
| Organização do código, testes e registro da atividade | 1,0 |
| **Total** | **5,0** |

## ⭐ Desafios adicionais (possível pontuação extra)

Depois de concluir todos os requisitos, você poderá:

- [ ] mostrar a quantidade de itens adicionados ao pedido;
- [ ] acrescentar os preços e calcular o valor total;
- [ ] adicionar um buzzer para avisar que o pedido está pronto;
- [ ] permitir o cancelamento antes do início do preparo;
- [ ] substituir a espera bloqueante por uma contagem controlada com `millis()`;
- [ ] apresentar um resumo do pedido antes da confirmação final.

---

<div align="center">

<h3>🍔 Escolher, confirmar, aguardar e receber</h3>
<p><strong>Uma boa interface deixa claro o que está acontecendo e qual botão o usuário deve pressionar.</strong></p>

</div>
