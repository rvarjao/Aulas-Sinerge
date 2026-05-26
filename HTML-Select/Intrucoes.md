# Select simples com preço automático

## Objetivo

Criar uma página com:

* um campo `select` com produtos;
* um campo `input` para mostrar o preço;
* JavaScript para preencher o preço automaticamente quando o produto for escolhido.

---

# Parte 1 — Criar os arquivos

Crie dois arquivos:

```
index.html
index.js
```

---

# Parte 2 — Criar o HTML

No arquivo `index.html`, escreva:

```
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Select simples</title>
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
    </form>
</body>
</html>
```

---

# Parte 3 — Entender o select

O campo `select` tem várias opções:

```
<select id="produto">
    <option value="">Selecione um produto</option>
    <option value="6.00">Coxinha</option>
    <option value="8.00">Suco</option>
    <option value="4.00">Pão de queijo</option>
    <option value="7.00">Refrigerante</option>
    <option value="15.00">Sanduíche</option>
</select>
```

Cada `<option>` tem duas partes importantes.

O texto visível:

```
Coxinha
```

E o valor escondido:

```
value="6.00"
```

Ou seja, o usuário vê:

```
Coxinha
```

Mas o JavaScript pega:

```
6.00
```

---

# Parte 4 — Criar o JavaScript

No arquivo `index.js`, escreva:

```
const selectProduto = document.getElementById('produto');
const inputPreco = document.getElementById('preco');

selectProduto.addEventListener('change', function() {
    inputPreco.value = selectProduto.value;
});
```

---

# Parte 5 — Entender o JavaScript

Pegamos o select:

```
const selectProduto = document.getElementById('produto');
```

Pegamos o input do preço:

```
const inputPreco = document.getElementById('preco');
```

Criamos um evento para quando o produto mudar:

```
selectProduto.addEventListener('change', function() {
```

Quando o usuário escolhe um produto, copiamos o valor do select para o input:

```
inputPreco.value = selectProduto.value;
```

---

# Parte 6 — Testar

Abra o `index.html` com Live Server.

Depois:

1. escolha `Coxinha`;
2. veja se aparece `6.00` no preço;
3. escolha `Suco`;
4. veja se aparece `8.00`;
5. escolha `Sanduíche`;
6. veja se aparece `15.00`.

---

# Parte 7 — Adicionar quantidade

Agora adicione no HTML, abaixo do preço:

```
<div>
    <label for="quantidade">Quantidade</label>
    <input type="number" id="quantidade">
</div>
```

E adicione também o total:

```
<div>
    <label for="total">Total</label>
    <input type="number" id="total" readonly>
</div>
```

---

# Parte 8 — Atualizar o JavaScript para calcular o total

Troque o código do `index.js` por:

```
const selectProduto = document.getElementById('produto');
const inputPreco = document.getElementById('preco');
const inputQuantidade = document.getElementById('quantidade');
const inputTotal = document.getElementById('total');

function calcularTotal() {
    const preco = Number(inputPreco.value);
    const quantidade = Number(inputQuantidade.value);

    const total = preco * quantidade;

    inputTotal.value = total;
}

selectProduto.addEventListener('change', function() {
    inputPreco.value = selectProduto.value;
    calcularTotal();
});

inputQuantidade.addEventListener('input', function() {
    calcularTotal();
});
```

---

# Parte 9 — Testar o total

Agora teste:

1. escolha `Coxinha`;
2. digite quantidade `2`;
3. o total deve aparecer como `12`;
4. escolha `Suco`;
5. o total deve mudar para `16`.

---

# Parte 10 — Melhorar casas decimais

No JavaScript, troque:

```
inputTotal.value = total;
```

por:

```
inputTotal.value = total.toFixed(2);
```

Assim o total aparece com duas casas decimais.

---

# Código final do HTML

```
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Select simples</title>
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
    </form>
</body>
</html>
```

# Código final do JavaScript

```
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
```

# Desafio final

Adicione dois campos:

```
Valor pago
Troco
```

O cálculo deve ser:

```
troco = valor pago - total
```

Exemplo:

```
Produto: Coxinha
Preço: 6.00
Quantidade: 2
Total: 12.00
Valor pago: 20.00
Troco: 8.00
```
