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



