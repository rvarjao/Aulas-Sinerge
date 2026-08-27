
# Cenários para modelagem de banco de dados

Faça a modelagem de banco de dados para os seguintes cenários. Para cada cenário, identifique as entidades, atributos e relacionamentos. Em seguida, desenhe o diagrama entidade-relacionamento (DER) correspondente.

Utilize a ferramenta drawdb.app


### 1. Biblioteca escolar — básico

Uma escola quer controlar os livros disponíveis em sua biblioteca. Cada livro possui título, ISBN, ano de publicação e pertence a uma editora. Uma editora pode publicar vários livros.

Os alunos da escola podem pegar livros emprestados. Para cada aluno devem ser armazenados nome, matrícula, turma e e-mail. Um aluno pode realizar vários empréstimos ao longo do tempo, e um mesmo livro também pode ser emprestado várias vezes, mas em momentos diferentes.

Para cada empréstimo devem ser registradas a data do empréstimo, a data prevista para devolução e a data em que o livro foi efetivamente devolvido.

**Desafio:** modelar o sistema permitindo consultar quem está atualmente com determinado livro.

---

### 2. Clínica médica — relacionamentos diferentes

Uma clínica deseja controlar seus pacientes, médicos e consultas.

Cada paciente possui CPF, nome, data de nascimento, telefone e endereço. Cada médico possui CRM, nome e uma especialidade. Uma especialidade pode estar associada a vários médicos.

As consultas são realizadas entre um paciente e um médico. Uma consulta deve registrar data, horário, motivo da consulta e observações feitas pelo médico.

Cada paciente também possui **um único prontuário**, criado quando ele realiza sua primeira consulta. O prontuário pertence exclusivamente àquele paciente.

**Desafio:** identificar onde aparecem relacionamentos **1:1** e **1:N**.

---

### 3. Loja virtual — relacionamento N:N

Uma loja virtual vende produtos pela internet. Cada produto possui nome, descrição, preço e quantidade disponível em estoque.

Os clientes possuem nome, CPF, e-mail e telefone. Um cliente pode realizar vários pedidos. Cada pedido possui data, status e endereço de entrega.

Um pedido pode conter vários produtos, e um mesmo produto pode aparecer em vários pedidos.

Porém, não basta saber que um produto está em um pedido: é necessário registrar **a quantidade comprada e o preço daquele produto no momento da compra**.

**Desafio:** perceber que o relacionamento entre pedido e produto precisa de uma **tabela intermediária com atributos próprios**.

---

### 4. Campeonato de futebol — relacionamento com informações do evento

Uma escola organiza um campeonato entre suas turmas. Cada time possui nome, turma e ano escolar. Cada jogador pertence a um time e possui nome, número da camisa e posição.

Durante o campeonato, os times disputam partidas. Cada partida possui data, horário e local e envolve exatamente dois times.

O sistema deve registrar o placar da partida, mas também precisa registrar os gols. Para cada gol é necessário saber qual jogador marcou, em qual partida ocorreu e em qual minuto do jogo.

Também podem ser registrados cartões. Para cada cartão deve ser informado o jogador, a partida, o minuto e se o cartão foi amarelo ou vermelho.

**Desafio:** pensar se **gol** e **cartão** devem ser apenas atributos ou se fazem sentido como entidades próprias.

---

### 5. Sistema de streaming — mais aberto

Uma plataforma de streaming possui filmes e séries. Todo conteúdo possui título, classificação indicativa, ano de lançamento e gênero.

As séries possuem temporadas, e cada temporada possui vários episódios. Cada episódio possui título, número, duração e data de lançamento.

Os usuários podem criar perfis dentro de suas contas. Uma conta pode possuir vários perfis.

Um perfil pode assistir a vários conteúdos. O sistema precisa guardar o histórico informando **o que foi assistido, quando foi assistido e até qual minuto o usuário chegou**. Um perfil também pode adicionar conteúdos à sua lista de favoritos.

No caso de uma série, o histórico precisa permitir saber exatamente qual episódio foi assistido.
