---
layout: post
title: "Controlando minhas finanças com Rails"
lead: Usando Ruby para me ajudar a controlar meu dinheiro
date: 2025-01-01 12:00:00 +0000
categories: blog update
---

<p>Todo ínicio de ano eu sempre me deparo o quão negligente fui com meu <b>dinheiro</b> no ano anterior e tento usar alguma <b>planilha</b> ou <b>aplicativo</b>
para tentar controlar minhas finanças, mas geralmente acabo falhando, seja pelo fato de não gostar de planilhas(sou ruim no Excel 😅), ou pelo fato dos aplicativos geralmente possuirem o modelo FREEMIUM* de négocio.</p>
<p>Esse ano decidi que vou fazer um controle melhor, e como estou de recesso do trabalho devido as festividades de 🎉 fim de ano 🎉, vou ter um tempinho pra fazer isso.</p>

<img src="/assets/files/posts/my_money/naruto_sem_money.jpg" class="img-thumbnail">

## Passos íniciais

<p>Pensei em criar uma aplicação básica de ínicio para evitar um conflito desnecessário comigo mesmo em procrastinar no desenvolvimento.</p>
<div style="width: 50%;">
  <img src="/assets/files/posts/my_money/shikamaru.jpg" class="img-thumbnail">
</div>
<p>A primeira coisa que pensei foi qual tecnologias iria usar para o desenvolvimento da aplicação web. Mais uma vez pensando na simplicidade pensei em 3 tecnologias que eu já sei alguma coisa: <b>Ruby</b>, <b>Python</b> ou <b>Kotlin</b>.</p>
<div style="display: flex; gap: 10px; flex-wrap: wrap; justify-content: center;">
  <img src="/assets/files/posts/my_money/kotlin.png" class="img-thumbnail" style="width: 100px; height: 100px; object-fit: contain;">
  <img src="/assets/files/posts/my_money/python.png" class="img-thumbnail" style="width: 100px; height: 100px; object-fit: contain;">
  <img src="/assets/files/posts/my_money/ruby.png" class="img-thumbnail" style="width: 100px; height: 100px; object-fit: contain;">
</div>
<p>O primeiro critério que usei para tentar resolver o qual iria usar, foi que a linguagem tivesse um framework Fullstack, que me permitisse criar um monolito, sem precisar criar um backend e um frontend, pois não quero gastar com hospedagem mais que o básico e facilitar minha vida pra aproveitar o fim de ano.</p>
<p>Daí já tirei o kotlin, por não dominar o suficiente o Spring e não ter tempo pra aprender.</p>
<div style="display: flex; gap: 10px; flex-wrap: wrap; justify-content: center;">
  <img src="/assets/files/posts/my_money/python.png" class="img-thumbnail" style="width: 100px; height: 100px; object-fit: contain;">
  <img src="/assets/files/posts/my_money/ruby.png" class="img-thumbnail" style="width: 100px; height: 100px; object-fit: contain;">
</div>
<p>Sobraram o <b>Ruby</b> e o <b>Python</b>, por fazer alguns projetinhos recentes em python usando o Django, eu estava bem confortável em usa-lo, mas faz um tempinho que não codava em <b>Ruby</b>, então decidi usar o <b>Rails</b> , que é o framework que mais domino.</p>

<div style="display: flex; gap: 10px; flex-wrap: wrap; justify-content: center;">
  <img src="/assets/files/posts/my_money/ruby.png" class="img-thumbnail" style="width: 100px; height: 100px; object-fit: contain;">
  <img src="/assets/files/posts/my_money/postgres.png" class="img-thumbnail" style="width: 100px; height: 100px; object-fit: contain;">
  <img src="/assets/files/posts/my_money/bootstrap.png" class="img-thumbnail" style="width: 100px; height: 100px; object-fit: contain;">
</div>
<p>Pronto, agora com a tecnologia escolhida e meio que por default, já fiz algumas escolhas baseada na mesma,como o banco de dados Postgres e para o frontend fui de Bootstrap, usei bastante no passado e ele ajudava muito pra quem não é full frontend, já com algumas classes defaults e estilos definidos.</p>

## Tabelas

<p>Pensei em três tabelas iniciais para representar minhas finanças:</p>

- <b>Category</b> ->  Onde salvarei as categorias com que gastei ou ganhei dinheiro. Ex: Alimentação
- <b>MoneyIn</b> - > Com o que ganhei dinheiro, Ex: salário, freela.
- <b>MoneyOut</b> ->  Com o que gastei dinheiro, Ex: Ps5

<p class= "fs-6">Representação básica das tabelas</p>
<img src="/assets/files/posts/my_money/tables.png" class="img-thumbnail">

## Desenvolvimento
<div style="width: 50%; margin: 0 auto;">
  <img src="/assets/files/posts/my_money/invocation.jpeg" class="img-thumbnail">
</div>


Após rodar os comandos iniciais do rails de inicialização do projeto 

<pre><code>rails new projeto</code></pre>
<pre><code>cd projeto/</code></pre>
<pre><code>bundle install</code></pre>

<p>Vamos criar as tabelas e a estrutura básica</p>

<pre><code>rails g scaffold categoy name description</code></pre>

<pre><code>rails g scaffold money_in label description amount:float category_id:references money_date:date</code></pre>

<pre><code>rails g scaffold money_out label description amount:float category_id:references money_date:date</code></pre>

<p>Pronto, com isso já temos o Crud básico, agora só precisamos estilizar com bootstrap e adicionar alguns gráficos com a gem <a href="https://chartkick.com/" class="link-primary link-offset-2 link-underline-opacity-25 link-underline-opacity-100-hover">Chartkick.</a></p>

<img src="/assets/files/posts/my_money/despesas.png" class="img-thumbnail">

<p>Também adicionei a gem de busca <a href="https://github.com/activerecord-hackery/ransack" class="link-primary link-offset-2 link-underline-opacity-25 link-underline-opacity-100-hover">Ransack</a> para facilitar as buscas e criei um formulário de busca para Receitas e Despesas, com agluns filtros que achei legais no momento.</p>

```erb
<%= search_form_for @q do |f| %>

  <%= f.label :label_or_description_cont, "Descrição Ou Nome", class: "form-label" %>
  <%= f.search_field :label_or_description_cont, class: "form-control" %>

  <div class="row mt-2">
    <div class="col-md-6">
      <%= f.label :money_date_gteq, "Data Inicial", class: "form-label" %>
      <%= f.search_field :money_date_gteq, type: :date, class: "form-control" %>
    </div>
    <div class="col-md-6">
      <%= f.label :money_date_lteq, "Data Final", class: "form-label" %>
      <%= f.search_field :money_date_lteq, type: :date, class: "form-control" %>
    </div>
  </div>

  <%= f.label :category_id_eq, "Categoria", class: "form-label" %>
  <%= f.select :category_id_eq, options_from_collection_for_select(@categories, :id, :name, params.dig(:q, :category_id_eq)), { include_blank: "Todas" }, class: "form-select" %>

  <div class="row mt-2">
    <div class="col-md-6">
      <%= f.label :amount_gteq, "Valor Mínimo", class: "form-label" %>
      <%= f.search_field :amount_gteq, type: :number, step: :any, class: "form-control" %>
    </div>
    <div class="col-md-6">
      <%= f.label :amount_lteq, "Valor Máximo", class: "form-label" %>
      <%= f.search_field :amount_lteq, type: :number, step: :any, class: "form-control" %>
    </div>
  </div>

  <%= f.submit "Buscar", class: "btn btn-primary mt-2" %>
<% end %>
```

<img src="/assets/files/posts/my_money/search.png" class="img-thumbnail">

<p class= "fs-6"><b>Legenda:</b></p>
<p class= "fs-6">FREEMIUM = é um modelo de negócio que oferece um produto ou serviço básico gratuitamente, atraindo muitos usuários, mas cobra por recursos avançados, funcionalidades extras.</p>
