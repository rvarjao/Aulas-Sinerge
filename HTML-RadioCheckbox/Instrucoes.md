# Continuação da aula sobre Select e Input

## Tema

Formulários HTML com:

```text
select
input
checkbox
radio
```

## Objetivo da aula

Na aula anterior, usamos:

```html
<select>
<input>
```

para escolher um produto e preencher automaticamente o preço.

Agora vamos continuar o mesmo exemplo da lanchonete, adicionando:

```text
checkbox → informações adicionais do pedido
radio    → forma de pagamento
```

Ao final da aula, o aluno deverá entender:

```text
select   → escolher uma opção em uma lista
input    → digitar ou receber um valor
checkbox → marcar várias opções
radio    → escolher apenas uma opção
```

---

# Parte 1 — Projeto da aula anterior

Vamos continuar com os mesmos arquivos:

```text
index.html
index.js
```

Na aula anterior, o HTML tinha algo parecido com isto:

```html
<form>
    <div>
        <label for="produto">Produto</label>
        <select id="produto">
            <option value="">Selecione um produto</option>
            <option value="6.00">Coxinha</option>
            <option value="8.00">Suco</option>
            <option value="4.00">Pão de queijo</option>
            <option value="7.00">Refrigerante</option>
            <option value="15.00">Sanduíche</option>
        </select>
    </div>

    <div>
        <label for="preco">Preço</label>
        <input type="number" id="preco" readonly>
    </div>

    <div>
        <label for="quantidade">Quantidade</label>
        <input type="number" id="quantidade">
    </div>

    <div>
        <label for="total">Total</label>
        <input type="number" id="total" readonly>
    </div>
</form>
```

E o JavaScript preenchia o preço e calculava o total.

---

# Parte 2 — Adicionar informações adicionais com checkbox

Agora vamos adicionar algumas opções extras do pedido.

No `index.html`, abaixo do campo `total`, adicione:

```html
<h3>Informações adicionais</h3>

<label>
    <input type="checkbox" value="Pago" class="info-adicional">
    Pago
</label>

<br>

<label>
    <input type="checkbox" value="Entregue" class="info-adicional">
    Entregue
</label>

<br>

<label>
    <input type="checkbox" value="Para viagem" class="info-adicional">
    Para viagem
</label>

<br>

<label>
    <input type="checkbox" value="Pedido urgente" class="info-adicional">
    Pedido urgente
</label>

<p id="resultado-info"></p>
```

---

# Parte 3 — Entender o checkbox

O `checkbox` permite marcar:

```text
nenhuma opção
uma opção
várias opções
```

Exemplo:

```text
[x] Pago
[x] Para viagem
[ ] Entregue
[ ] Pedido urgente
```

Isso é diferente do `select`, porque no `select` normalmente escolhemos uma opção principal.

No `checkbox`, cada opção é independente.

---

# Parte 4 — Pegar os checkboxes no JavaScript

No `index.js`, adicione:

```javascript
const checkboxesInfo = document.querySelectorAll('.info-adicional');
```

Aqui estamos pegando todos os elementos que possuem a classe:

```html
class="info-adicional"
```

---

# Parte 5 — Criar função para pegar as opções marcadas

No `index.js`, adicione:

```javascript
function pegarInformacoesAdicionais() {
    const informacoes = [];

    checkboxesInfo.forEach(function(checkbox) {
        if (checkbox.checked) {
            informacoes.push(checkbox.value);
        }
    });

    return informacoes;
}
```

---

# Parte 6 — Entender a função

Criamos um array vazio:

```javascript
const informacoes = [];
```

Depois percorremos todos os checkboxes:

```javascript
checkboxesInfo.forEach(function(checkbox) {
```

Verificamos se o checkbox está marcado:

```javascript
if (checkbox.checked) {
```

Se estiver marcado, adicionamos seu valor ao array:

```javascript
informacoes.push(checkbox.value);
```

Exemplo de resultado:

```javascript
["Pago", "Para viagem"]
```

---

# Parte 7 — Mostrar as informações escolhidas na tela

Adicione esta função no `index.js`:

```javascript
function atualizarInformacoes() {
    const informacoes = pegarInformacoesAdicionais();

    const resultado = document.getElementById('resultado-info');

    resultado.textContent = informacoes.join(', ');
}
```

O `join(', ')` transforma o array em texto.

Exemplo:

```javascript
["Pago", "Para viagem"]
```

vira:

```text
Pago, Para viagem
```

---

# Parte 8 — Atualizar quando marcar ou desmarcar

Adicione no `index.js`:

```javascript
checkboxesInfo.forEach(function(checkbox) {
    checkbox.addEventListener('change', function() {
        atualizarInformacoes();
    });
});
```

Agora, sempre que o aluno marcar ou desmarcar uma opção, o texto será atualizado.

---

# Parte 9 — Adicionar forma de pagamento com radio

Agora vamos adicionar a forma de pagamento.

No `index.html`, abaixo das informações adicionais, adicione:

```html
<h3>Forma de pagamento</h3>

<label>
    <input type="radio" name="pagamento" value="Dinheiro">
    Dinheiro
</label>

<br>

<label>
    <input type="radio" name="pagamento" value="Pix">
    Pix
</label>

<br>

<label>
    <input type="radio" name="pagamento" value="Cartão">
    Cartão
</label>

<br>

<label>
    <input type="radio" name="pagamento" value="Fiado">
    Fiado
</label>

<p id="resultado-pagamento"></p>
```

---

# Parte 10 — Entender o radio

O `radio` é usado quando o usuário deve escolher apenas uma opção.

Exemplo:

```text
( ) Dinheiro
(o) Pix
( ) Cartão
( ) Fiado
```

A diferença principal é:

```text
checkbox → várias opções podem ser marcadas
radio    → apenas uma opção pode ser marcada
```

---

# Parte 11 — A importância do name no radio

Observe que todos os radios usam o mesmo `name`:

```html
name="pagamento"
```

Isso é muito importante.

Quando vários radios têm o mesmo `name`, o navegador entende que eles fazem parte do mesmo grupo.

Por isso, só uma forma de pagamento pode ser selecionada.

---

# Parte 12 — Pegar a forma de pagamento escolhida

No `index.js`, adicione:

```javascript
function pegarFormaPagamento() {
    const pagamentoSelecionado = document.querySelector('input[name="pagamento"]:checked');

    if (pagamentoSelecionado) {
        return pagamentoSelecionado.value;
    }

    return '';
}
```

---

# Parte 13 — Entender o querySelector com :checked

Este trecho:

```javascript
document.querySelector('input[name="pagamento"]:checked')
```

significa:

```text
procure um input
que tenha name igual a pagamento
e que esteja marcado
```

A parte:

```text
:checked
```

indica que queremos apenas o radio selecionado.

---

# Parte 14 — Mostrar a forma de pagamento na tela

Adicione esta função:

```javascript
function atualizarFormaPagamento() {
    const pagamento = pegarFormaPagamento();

    const resultado = document.getElementById('resultado-pagamento');

    if (pagamento === '') {
        resultado.textContent = '';
    } else {
        resultado.textContent = 'Forma de pagamento: ' + pagamento;
    }
}
```

---

# Parte 15 — Atualizar quando escolher uma forma de pagamento

Adicione no `index.js`:

```javascript
const radiosPagamento = document.querySelectorAll('input[name="pagamento"]');

radiosPagamento.forEach(function(radio) {
    radio.addEventListener('change', function() {
        atualizarFormaPagamento();
    });
});
```

---

# Parte 16 — Código JavaScript completo da aula

Considerando que a aula anterior já tinha o cálculo de preço e total, o `index.js` pode ficar assim:

```javascript
const selectProduto = document.getElementById('produto');
const inputPreco = document.getElementById('preco');
const inputQuantidade = document.getElementById('quantidade');
const inputTotal = document.getElementById('total');

function calcularTotal() {
    const preco = Number(inputPreco.value);
    const quantidade = Number(inputQuantidade.value);

    const total = preco * quantidade;

    inputTotal.value = total.toFixed(2);
}

selectProduto.addEventListener('change', function() {
    inputPreco.value = selectProduto.value;
    calcularTotal();
});

inputQuantidade.addEventListener('input', function() {
    calcularTotal();
});

const checkboxesInfo = document.querySelectorAll('.info-adicional');

function pegarInformacoesAdicionais() {
    const informacoes = [];

    checkboxesInfo.forEach(function(checkbox) {
        if (checkbox.checked) {
            informacoes.push(checkbox.value);
        }
    });

    return informacoes;
}

function atualizarInformacoes() {
    const informacoes = pegarInformacoesAdicionais();

    const resultado = document.getElementById('resultado-info');

    resultado.textContent = informacoes.join(', ');
}

checkboxesInfo.forEach(function(checkbox) {
    checkbox.addEventListener('change', function() {
        atualizarInformacoes();
    });
});

function pegarFormaPagamento() {
    const pagamentoSelecionado = document.querySelector('input[name="pagamento"]:checked');

    if (pagamentoSelecionado) {
        return pagamentoSelecionado.value;
    }

    return '';
}

function atualizarFormaPagamento() {
    const pagamento = pegarFormaPagamento();

    const resultado = document.getElementById('resultado-pagamento');

    if (pagamento === '') {
        resultado.textContent = '';
    } else {
        resultado.textContent = 'Forma de pagamento: ' + pagamento;
    }
}

const radiosPagamento = document.querySelectorAll('input[name="pagamento"]');

radiosPagamento.forEach(function(radio) {
    radio.addEventListener('change', function() {
        atualizarFormaPagamento();
    });
});
```

---

# Parte 17 — Código HTML completo da aula

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Select, Checkbox e Radio</title>
    <script src="index.js" defer></script>
</head>
<body>
    <h1>Lanchonete</h1>

    <form>
        <div>
            <label for="produto">Produto</label>
            <select id="produto">
                <option value="">Selecione um produto</option>
                <option value="6.00">Coxinha</option>
                <option value="8.00">Suco</option>
                <option value="4.00">Pão de queijo</option>
                <option value="7.00">Refrigerante</option>
                <option value="15.00">Sanduíche</option>
            </select>
        </div>

        <div>
            <label for="preco">Preço</label>
            <input type="number" id="preco" readonly>
        </div>

        <div>
            <label for="quantidade">Quantidade</label>
            <input type="number" id="quantidade">
        </div>

        <div>
            <label for="total">Total</label>
            <input type="number" id="total" readonly>
        </div>

        <h3>Informações adicionais</h3>

        <label>
            <input type="checkbox" value="Pago" class="info-adicional">
            Pago
        </label>

        <br>

        <label>
            <input type="checkbox" value="Entregue" class="info-adicional">
            Entregue
        </label>

        <br>

        <label>
            <input type="checkbox" value="Para viagem" class="info-adicional">
            Para viagem
        </label>

        <br>

        <label>
            <input type="checkbox" value="Pedido urgente" class="info-adicional">
            Pedido urgente
        </label>

        <p id="resultado-info"></p>

        <h3>Forma de pagamento</h3>

        <label>
            <input type="radio" name="pagamento" value="Dinheiro">
            Dinheiro
        </label>

        <br>

        <label>
            <input type="radio" name="pagamento" value="Pix">
            Pix
        </label>

        <br>

        <label>
            <input type="radio" name="pagamento" value="Cartão">
            Cartão
        </label>

        <br>

        <label>
            <input type="radio" name="pagamento" value="Fiado">
            Fiado
        </label>

        <p id="resultado-pagamento"></p>
    </form>
</body>
</html>
```

---

# Parte 18 — Testes da aula

Teste os seguintes pontos:

1. escolha um produto;
2. veja se o preço aparece;
3. digite a quantidade;
4. veja se o total é calculado;
5. marque `Pago`;
6. marque `Para viagem`;
7. veja se as duas informações aparecem;
8. escolha `Pix`;
9. veja se aparece `Forma de pagamento: Pix`;
10. escolha `Dinheiro`;
11. veja se `Pix` é desmarcado automaticamente.

---

# Parte 19 — Comparação final

```text
select
Usado para escolher uma opção dentro de uma lista.

input
Usado para digitar ou exibir um valor.

checkbox
Usado para opções independentes.
Pode marcar nenhuma, uma ou várias.

radio
Usado para escolha única.
Só uma opção do grupo pode ser marcada.
```

---

# Desafio 1

Adicione mais uma informação adicional:

```text
Com desconto
```

---

# Desafio 2

Adicione mais uma forma de pagamento:

```text
Vale-lanche
```

---

# Desafio 3

Mostre no console um resumo do pedido:

```javascript
console.log('Produto:', selectProduto.options[selectProduto.selectedIndex].text);
console.log('Preço:', inputPreco.value);
console.log('Quantidade:', inputQuantidade.value);
console.log('Total:', inputTotal.value);
console.log('Informações:', pegarInformacoesAdicionais());
console.log('Pagamento:', pegarFormaPagamento());
```

---

# Fechamento da aula

Nesta aula, continuamos o projeto iniciado com `select` e `input`.

Agora o formulário ficou mais completo, porque ele consegue representar diferentes tipos de escolha:

```text
produto escolhido
preço automático
quantidade
total
informações adicionais
forma de pagamento
```

Essa estrutura já se parece mais com um formulário usado em sistemas reais.
