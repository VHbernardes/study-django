## DOCUMENTAÇÃO

1 - Criação de um ambiente virtual venv
2 - Ativação do ambiente virtual (.\nome_da_venv\Scripts(ou bin)\activate)
3 - Instalação do Django
    - pip install Django
    - django-admin startproject nome_projeto (criação do projeto em django)
    - python manage.py migrate (criação do banco de dados do django - SQLlite3)
    - python manage.py runserver
4 - Download do DB Browser for SQLite para a visualização do nosso banco de dados
5 - Criação do app principal do django
    - python manage.py startapp nome_do_app
6 - Inserimos o nome do app dentro de settings.py, mais especificamente na parte 'INSTALLED_APPS';
7 - Criação de um modelo dentro de models.py (que será uma tabela dentro do banco de dados)
    - text = models.CharField... e date_added = models.DateTimeField... 
    - python manage.py makemigrations nome do app
    - python manage.py migrate (atualizar e colocar a nova tabela no banco de dados)
8 - Acessando o painel administrativo do Django (http://127.0.0.1:8000/admin)
9 - Criando um usuário e senha para acessar esse painel;
    - python manage.py createsuperuser
    - colocar o usuario, email(opcional) e senha;
10 - Acesso o admin.py dentro do app e importo a Classe que criei dentro de models.py para visualizar o modelo dentro do painel administrativo;
    - from learning_logs.models import Topic
    - admin.site.register(Topic) (criar a aba Tópicos dentro da página)
11 - criação de um novo modelo com o intuito de armazenar várias informoções de um mesmo tópico ou outros;
    - utilização de uma ForeignKey para atribuir as informações a um tópico específico;  
    - topic = models.ForeignKey(Topic, on_delete=models.CASCADE);
12 - Acessei a aba urls.py dentro da pasta do nosso projeto, criei um novo caminho para anexar uma página feita por nós no página principal do django;
    - importei o método include();
    - criei novo caminho (path('/', include('learning_logs.urls')));
13 - Copiei a aba urls.py da pasta do projeto principal para anexa-lá na pasta do app;
14 - Ao anexa-lá, podemos retirar o método include e deixar vazio o caminho do path, pois iremos importar a aba views.py, pois nela estará nossa página que iremos fazer;
15 - Dentro da views.py, iremos criar uma função com o nome index, que irá fazer uma requisação e renderização da nossa página inicial;
16 - Agora temos que criar uma pasta dentro do app com o nome de templates, onde o django irá sempre procurar e ler nossas páginas html, onde utilizaremos nossa função index da views.py;
17 - Dentro de templates, vamos criar uma nova pasta com o nome do app e vamos criar um index.html dentro, onde ela será nossa página inicial;
18 - Também dentro de templates, vamos criar outro arquivo, o base.html, onde ele irá herdar coisas de outras páginas html e vice-versa;
19 - "Tag de templates";
20 - Agora, vou na aba de urls.py, crio um no path que será a página onde mostra todos os tópicos;
21 - Após isso, crio uma nova função dentro de views.py, onde ela irá fazer a renderização e a requisição de nova página;
    - Falando um pouco em si do código, criei uma nova variável topics, onde ela irá ordenar todos os tópicos feitos pela data de criação. Depois, criei um dicionário de chave e valor, que irá armazenar esses tópicos. Enfim, utilizei o mesmo return da página principal, onde ele faz uma render(renderização) e um request(requisição) para criar nossa nova página;
22 - Vou para templates, dentro da nossa pasta do app e crio uma nova página html, o topics.html;
23 - Adicionamos linhas de código nessa página nova, utilizando um for para adicionar os tópicos a essa página;
24 - Voltamos a aba de urls.py e criamos um novo path, que no caso é o caminho para a página que mostre um tópico específico. Para isso, vamos utilizar a ID do tópico apresentada no banco de dados;
25 - Seguindo a mesma lógica do 21, criamos uma nova função na views.py para essa nova página de um tópico exclusivo;
    - A diferença está que primeiro criamos a váriavel topic e utilizamos o get, pois só queremos um único tópico, vindo do seu ID. Após isso, criamos uma váriavel para as entradas(descrições dos tópicos) que leva a mesma lógica do 21, a única mudança esta no "-data_added", pois estamos ordenando inversamente a data. Enfim, o resto continua o mesmo.
26 - Criamos na pasta template a página topic.html e inserimos as linhas de código em block para que ela funcione;
    - Falando mais sobre o código, criamos novamente um for para adicionar o conteúdo de acordo com a quantidade criada pelo usuário. Mas dessa vez, utlizamos tanto o date_added e o text formatados para adicionarmos na nova variável criada no for, o entry.
27 - Agora, colocamos links para todas os tópicos e entradas do nosso projeto;
28 - Enfim, um dos passos mais importantes. a criação de formulários;
29 - O primeiro será a criação de tópicos pelos usuários;
30 - Primeiro vamos criar um arquivo chamado forms.py, onde iremos implementar ele todo aqui dentro. Após isso, importamos do django o método Forms, que utilizaremos para a criação, validação e manipulação dos nossos formulários. Depois, importamos de models.py, a função Topic, pois queremos criar uma interface de usuário que permita aos usuários inserir ou modificar dados relacionados a esse modelo específico;
31 - Após, criamos uma nova view, onde iremos verificar se nosso formulário é do tipo get(recebe vazio) ou do tipo post(enviamos dados). Colocamos um método de validação do forms para validar/salvar o forms e retornar um httpresponse de acordo somente com o nome do tópico;
32 - Criamos o novo template com o nome de new_topics.html, e nele seguimos as lógicas dos outros, extendemos da base.html e criamos um block. Depois criar nosso linha de código que irá criar o formulário e utilizá-lo;
33 - Dentro de forms.py, criamos um novo formulário, esse para o usuário poder escrever anotações de um tópico selecionado.
34 - Após, criamos um novo path, ou seja, um novo caminho para essa página, adicionando um parâmetro, que no caso é a ID do tópico que você está inserido e onde você quer criar anotações;
35 - Agora, criamos uma nova view, seguindo a lógica do primeiro formulário, com a diferença que vamos primeiro criar uma váriavel onde ele irá pegar usando o método get um único só tópico com o seu ID, que foi selecionado, para poder criar novas anotações a ele. Outra diferença é na validação do formulário, que quando ele validar e ver que é true, ele irá criar um novo objeto e irá salvar os dados desse formulário nesse objeto, mas não irá gravar-los no banco de dados ainda. Após isso, irá associar esse novo objeto com o tópico escolhido, depois irá salvar o objeto esses novos dados e o tópico escolhido no banco de dados. Por fim, irá redirecionar o usuário com o reverse para a página do tópico após adicionar a anotação com sucesso;
36 - Criamos de novo um template para essa view, e implementamos a lógica igual algumas outras páginas;



