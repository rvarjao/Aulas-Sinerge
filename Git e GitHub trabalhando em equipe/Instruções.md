# Aula prática — Git e GitHub trabalhando em equipe

## 🎯 Desafio: Catálogo de Filmes

Nesta atividade vocês irão desenvolver um pequeno **site de catálogo de filmes utilizando HTML e CSS**.

Mas o principal objetivo da aula **não é o HTML**.

O objetivo é aprender como uma equipe de desenvolvimento trabalha no mesmo projeto utilizando:

* Git
* GitHub
* VS Code
* branches
* commits
* push e pull
* Pull Requests
* merge
* resolução de conflitos

Ao final da atividade, todo o site deverá estar integrado em um único repositório.

---

# 1. O problema

Imagine que quatro desenvolvedores estejam trabalhando no mesmo sistema.

Um está criando a página inicial.

Outro está criando a página de detalhes de um filme.

Outro está criando a página de lançamentos.

Outro está criando a página de favoritos.

Como todos podem trabalhar ao mesmo tempo sem ficar enviando arquivos pelo WhatsApp, e-mail ou Google Drive?

É justamente esse tipo de problema que o **Git** ajuda a resolver.

---

# 2. Regra principal da atividade

Durante esta atividade existe uma regra muito importante:

> 🚫 Ninguém deverá desenvolver diretamente na branch `main`.

A `main` representa a versão principal e estável do projeto.

Cada integrante deverá criar uma **branch própria para desenvolver sua tarefa**.

Exemplo:

```text
main
│
├── feature/home
├── feature/lancamentos
├── feature/detalhes-filme
└── feature/favoritos
```

Quando uma funcionalidade estiver pronta, ela deverá ser enviada para revisão antes de entrar na `main`.

---

# 3. Organização das equipes

Formem equipes de **3 a 5 integrantes**.

Escolham um integrante para criar inicialmente o repositório.

Esse aluno será apenas o responsável pela criação inicial.

Ele **não será o dono do projeto**.

O projeto pertence à equipe.

---

# 4. Projeto que será desenvolvido

Vocês irão criar o site:

# 🎬 CineHub

Um pequeno catálogo de filmes.

O projeto poderá ter a seguinte estrutura:

```text
cinehub/
│
├── index.html
├── lancamentos.html
├── filme.html
├── favoritos.html
├── sobre.html
│
├── css/
│   └── style.css
│
└── images/
```

Não é necessário criar todas as páginas caso a equipe tenha menos integrantes.

---

# 5. Divisão das tarefas

Uma possível divisão para uma equipe de quatro integrantes:

| Integrante | Página               | Branch                   |
| ---------- | -------------------- | ------------------------ |
| Aluno 1    | Página inicial       | `feature/home`           |
| Aluno 2    | Lançamentos          | `feature/lancamentos`    |
| Aluno 3    | Detalhes de um filme | `feature/detalhes-filme` |
| Aluno 4    | Favoritos            | `feature/favoritos`      |

Caso exista um quinto integrante:

| Integrante | Página          | Branch          |
| ---------- | --------------- | --------------- |
| Aluno 5    | Sobre o projeto | `feature/sobre` |

Cada aluno deve desenvolver **apenas a tarefa definida inicialmente**.

---

# 6. Criando o repositório no GitHub

Um integrante deverá acessar o GitHub e criar um novo repositório.

Nome sugerido:

```text
cinehub-nome-da-equipe
```

Exemplo:

```text
cinehub-equipe-3
```

Marque a opção para criar o arquivo:

```text
README.md
```

Depois clique em:

**Create repository**

---

# 7. Adicionando os integrantes da equipe

No repositório criado, acesse:

```text
Settings
→ Collaborators
→ Add people
```

Adicione o usuário do GitHub de cada integrante da equipe.

Os colegas deverão aceitar o convite.

---

# 8. Clonando o projeto no computador

Agora **cada integrante** deverá ter uma cópia do projeto em seu computador.

No VS Code:

1. Abra o VS Code.
2. Pressione:

```text
Ctrl + Shift + P
```

3. Pesquise:

```text
Git: Clone
```

4. Escolha:

```text
Clone from GitHub
```

5. Selecione o repositório da equipe.
6. Escolha uma pasta no computador.
7. Abra o projeto.

Agora vocês possuem uma **cópia local do repositório**.

---

# 9. Git não é Google Drive

Até agora vocês talvez tenham utilizado o GitHub da seguinte maneira:

```text
Criar arquivo
↓
Entrar no GitHub
↓
Upload do arquivo
↓
Substituir arquivo antigo
```

Esse não é o fluxo normal de desenvolvimento com Git.

A partir de agora utilizaremos:

```text
Editar arquivos no VS Code
        ↓
Git identifica as alterações
        ↓
Commit
        ↓
Push
        ↓
GitHub
```

O Git registra **alterações no projeto**, não apenas arquivos.

---

# 10. Antes de começar: verifique a branch

No canto inferior esquerdo do VS Code aparecerá o nome da branch atual.

Provavelmente:

```text
main
```

⚠️ Não comece a desenvolver nela.

Cada integrante deverá criar sua própria branch.

---

# 11. Criando uma branch

Clique sobre o nome:

```text
main
```

no canto inferior esquerdo do VS Code.

Escolha:

```text
Create new branch
```

Digite o nome da branch.

Exemplo:

```text
feature/home
```

Outro integrante poderá criar:

```text
feature/lancamentos
```

Outro:

```text
feature/detalhes-filme
```

---

# 12. O que é uma branch?

Imagine que o projeto principal esteja assim:

```text
A ─── B ─── C
            ↑
           main
```

Um desenvolvedor precisa criar uma nova funcionalidade.

Ele cria uma branch:

```text
A ─── B ─── C
            │
            └── D ─── E
                feature/home
```

Enquanto isso, outro desenvolvedor pode trabalhar em outra branch:

```text
A ─── B ─── C
            │
            ├── D ─── E
            │   feature/home
            │
            └── F ─── G
                feature/lancamentos
```

Assim os dois conseguem trabalhar **sem alterar diretamente a versão principal do projeto**.

---

# 13. Desenvolvendo sua página

Cada integrante deverá agora criar a página correspondente à sua tarefa.

Exemplo de página inicial:

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CineHub</title>
    <link rel="stylesheet" href="css/style.css">
</head>

<body>

<header>
    <h1>CineHub</h1>

    <nav>
        <a href="index.html">Início</a>
        <a href="lancamentos.html">Lançamentos</a>
        <a href="favoritos.html">Favoritos</a>
        <a href="sobre.html">Sobre</a>
    </nav>
</header>

<main>

    <h2>Filmes em destaque</h2>

    <section>
        <article>
            <h3>Nome do Filme</h3>
            <p>Descrição do filme.</p>
            <a href="filme.html">Ver detalhes</a>
        </article>
    </section>

</main>

</body>
</html>
```

Vocês podem personalizar completamente o projeto.

---

# 14. Salvando uma versão com Git

Depois de realizar algumas alterações, clique no ícone:

**Source Control**

na lateral esquerda do VS Code.

Atalho:

```text
Ctrl + Shift + G
```

Você verá os arquivos alterados.

Por exemplo:

```text
M index.html
```

O `M` significa:

```text
Modified
```

ou seja:

> o arquivo foi modificado.

---

# 15. Stage

Antes de criar um commit, precisamos escolher quais alterações entrarão nele.

Clique no símbolo:

```text
+
```

ao lado do arquivo.

O arquivo passará para:

```text
Staged Changes
```

Isso significa:

> esta alteração fará parte do próximo commit.

---

# 16. Commit

Agora escreva uma mensagem descrevendo o que foi feito.

Exemplo:

```text
Cria estrutura da página inicial
```

Clique em:

```text
Commit
```

Um commit representa um **ponto no histórico do projeto**.

Exemplo:

```text
Cria estrutura inicial
        ↓
Adiciona menu
        ↓
Adiciona cards de filmes
        ↓
Corrige links do menu
```

Cada alteração importante deve gerar um commit.

---

# 17. Mensagens de commit

Evite mensagens como:

```text
alteração
```

```text
teste
```

```text
aaa
```

```text
final
```

```text
agora vai
```

Prefira mensagens que expliquem o que aconteceu:

```text
Cria página de lançamentos
```

```text
Adiciona menu de navegação
```

```text
Corrige links dos cards de filmes
```

```text
Adiciona informações do filme
```

---

# 18. Push

O commit existe inicialmente no computador de vocês.

Precisamos enviar essa alteração para o GitHub.

Utilize:

```text
Push
```

ou:

```text
Publish Branch
```

Na primeira vez que uma nova branch for enviada.

Depois disso, abra o repositório no GitHub.

Sua branch deverá aparecer lá.

---

# 19. Pull Request

Agora sua funcionalidade está pronta.

Mas ainda **não está na `main`**.

No GitHub aparecerá normalmente a opção:

```text
Compare & pull request
```

Clique nela.

Crie o Pull Request.

Título sugerido:

```text
Cria página de lançamentos
```

Na descrição informe rapidamente o que foi desenvolvido.

Exemplo:

```text
Foi criada a página de lançamentos contendo:

- título da página;
- menu de navegação;
- quatro filmes;
- links para detalhes dos filmes.
```

---

# 20. O que é um Pull Request?

Um Pull Request significa aproximadamente:

> "Eu terminei esta alteração. Podemos colocar isso no projeto principal?"

Ele permite que outros integrantes da equipe analisem as alterações antes que elas entrem na `main`.

O fluxo será:

```text
Branch
   ↓
Desenvolvimento
   ↓
Commit
   ↓
Push
   ↓
Pull Request
   ↓
Revisão
   ↓
Merge
   ↓
main
```

---

# 21. Revisão por outro integrante

Antes de realizar o merge, outro integrante deverá abrir o Pull Request.

Observe:

```text
Files changed
```

Veja quais arquivos foram adicionados ou modificados.

O colega deverá verificar pelo menos:

* se a página funciona;
* se os links estão corretos;
* se não existe código estranho;
* se a tarefa solicitada foi realizada.

Se estiver tudo correto, poderá aprovar.

---

# 22. Merge

Depois da revisão, realize:

```text
Merge pull request
```

A alteração passará a fazer parte da:

```text
main
```

Exemplo:

Antes:

```text
main
  │
  └──── feature/lancamentos
```

Depois:

```text
main
  │
  ├── index.html
  └── lancamentos.html
```

A funcionalidade criada por outro integrante agora faz parte do projeto principal.

---

# 23. Atualizando seu projeto

Imagine a seguinte situação:

Maria terminou `lancamentos.html` e realizou o merge.

João ainda está trabalhando em `index.html`.

O computador de João ainda **não possui a página criada por Maria**.

Ele precisa atualizar seu projeto.

Primeiro volte para:

```text
main
```

Depois utilize:

```text
Pull
```

ou:

```text
Sync Changes
```

Agora a versão local será atualizada.

---

# 24. Antes de iniciar uma nova tarefa

Utilizem sempre este fluxo:

```text
1. Voltar para main

2. Atualizar a main

3. Criar uma nova branch

4. Desenvolver

5. Commit

6. Push

7. Pull Request

8. Revisão

9. Merge
```

Não reutilize eternamente a mesma branch.

Cada nova funcionalidade deve preferencialmente possuir sua própria branch.

---

# 25. Desafio da equipe

Quando todas as páginas estiverem prontas, o projeto deverá permitir navegar entre elas.

Exemplo:

```text
Home
 │
 ├── Lançamentos
 │
 ├── Favoritos
 │
 ├── Filme
 │
 └── Sobre
```

Todos deverão possuir o mesmo menu.

Exemplo:

```html
<nav>
    <a href="index.html">Início</a>
    <a href="lancamentos.html">Lançamentos</a>
    <a href="favoritos.html">Favoritos</a>
    <a href="sobre.html">Sobre</a>
</nav>
```

---

# 26. Agora vamos provocar um problema

Depois que todas as páginas estiverem funcionando, cada equipe deverá provocar propositalmente um **conflito de Git**.

Dois integrantes deverão criar branches diferentes.

Exemplo:

```text
feature/altera-titulo-a
```

e:

```text
feature/altera-titulo-b
```

Os dois deverão modificar **a mesma linha** do arquivo:

```text
index.html
```

Por exemplo:

Aluno A:

```html
<h1>CineHub - Os melhores filmes</h1>
```

Aluno B:

```html
<h1>CineHub - Seu portal de cinema</h1>
```

O aluno A deverá:

```text
commit
↓
push
↓
Pull Request
↓
merge
```

Depois o aluno B tentará integrar sua alteração.

---

# 27. Merge Conflict

O Git poderá informar:

```text
Merge conflict
```

Isso significa que existem duas alterações diferentes para a mesma parte do código.

O Git não sabe qual delas escolher.

Essa decisão precisa ser tomada por uma pessoa.

Pode ser necessário escolher:

```html
<h1>CineHub - Os melhores filmes</h1>
```

ou:

```html
<h1>CineHub - Seu portal de cinema</h1>
```

ou até combinar as duas:

```html
<h1>CineHub - Seu portal com os melhores filmes</h1>
```

Depois de resolver o conflito:

```text
salvar
↓
commit
↓
push
```

---

# 28. Por que conflitos acontecem?

Conflitos normalmente acontecem quando duas pessoas modificam a mesma região de um arquivo.

Por exemplo:

```text
João
   └── altera linha 25

Maria
   └── altera linha 25
```

O Git consegue combinar automaticamente muitas alterações.

Mas nem sempre consegue decidir qual versão é a correta.

---

# 29. Git não serve apenas para equipes

Imagine que você esteja desenvolvendo sozinho.

Segunda-feira:

```text
Sistema funcionando
```

Terça-feira:

```text
Você altera 15 arquivos
```

Quarta-feira:

```text
O sistema para de funcionar
```

Com Git podemos investigar:

```text
O que mudou?
Quem alterou?
Quando alterou?
Por que alterou?
```

Também podemos recuperar versões anteriores.

---

# 30. Git x GitHub

Agora responda:

### Git

É um **sistema de controle de versões**.

Ele acompanha as alterações realizadas nos arquivos de um projeto.

Pode funcionar no seu próprio computador.

---

### GitHub

É uma plataforma online utilizada para hospedar e compartilhar repositórios Git.

Ela também oferece recursos para colaboração, como:

* Pull Requests;
* Issues;
* revisão de código;
* gerenciamento de projetos;
* histórico de alterações.

Portanto:

```text
Git ≠ GitHub
```

---

# 31. Analogia

Podemos imaginar:

```text
Git
│
├── controla versões
├── registra alterações
├── cria branches
├── faz merges
└── mantém histórico
```

Enquanto:

```text
GitHub
│
├── hospeda o repositório
├── permite colaboração
├── compartilha o código
├── permite Pull Requests
└── facilita revisões
```

---

# 32. Pesquisa e reflexão individual

Depois de concluir o desafio em equipe, cada integrante deverá responder
individualmente ao questionário sobre Git, GitHub e desenvolvimento colaborativo.

👉 **Questionário:** [Acessar Google Forms](https://forms.gle/hCTqKk9EvSgNggnV7)

O questionário deverá ser respondido individualmente.

Antes de responder, pesquise e revise os conceitos utilizados durante a atividade:

- Git e GitHub;
- repositório local e remoto;
- commit;
- branch;
- `main`;
- push e pull;
- Pull Request;
- merge;
- merge conflict;
- desenvolvimento colaborativo.

> Não basta decorar os termos. Procure relacionar cada conceito com o que aconteceu
> durante o desenvolvimento do projeto da sua equipe.

---

# 33. Explique o fluxo

Utilizando suas próprias palavras, explique o seguinte fluxo:

```text
main
  ↓
branch
  ↓
alteração
  ↓
stage
  ↓
commit
  ↓
push
  ↓
Pull Request
  ↓
review
  ↓
merge
  ↓
main
```

---

# 34. Entrega

A equipe deverá entregar:

* link do repositório no GitHub;
* todos os integrantes cadastrados como colaboradores;
* pelo menos uma branch criada por cada integrante;
* pelo menos dois commits por integrante;
* pelo menos um Pull Request por integrante;
* histórico de merges;
* site funcionando após a integração das páginas;
* pelo menos um conflito criado e resolvido pela equipe.

---

# 35. O que será observado

Mais importante do que deixar o site bonito será demonstrar que a equipe utilizou corretamente o fluxo de desenvolvimento.

Será observado:

### Organização do Git

```text
Branches
Commits
Pull Requests
Merges
```

### Trabalho em equipe

```text
Divisão das tarefas
Revisão das alterações
Integração do código
```

### Projeto

```text
Navegação funcionando
HTML organizado
Arquivos organizados
```

---

# 36. Regra para os próximos projetos

A partir desta atividade, adotaremos o seguinte fluxo nos projetos da disciplina:

```text
Nunca desenvolver diretamente na main.

Uma tarefa
     ↓
Uma branch
     ↓
Commits
     ↓
Push
     ↓
Pull Request
     ↓
Revisão
     ↓
Merge
```

O Git não deve ser utilizado como um local onde simplesmente guardamos arquivos.

Ele deve registrar **a evolução do projeto**.

---

# ✅ Resultado esperado

Ao final desta aula, vocês deverão conseguir explicar a diferença entre:

```text
Git
GitHub
commit
branch
push
pull
Pull Request
merge
merge conflict
```

Mas, principalmente, deverão ter utilizado cada um desses conceitos **em um projeto real desenvolvido em equipe**.
