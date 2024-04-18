## DOCUMENTAÇÃO

1 - Criação de um ambiente virtual venv;

2 - Ativação do ambiente virtual (.\nome_da_venv\Scripts(ou bin)\activate);

3 - Instalação do Django;
    - pip install Django;
    - django-admin startproject nome_projeto (criação do projeto em django);
    - python manage.py migrate (criação do banco de dados do django - SQLlite3);
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

37 - Criamos um novo path para podermos editar as anotações, então criamos um novo path em urls.py, onde colocamos o caminho do navegador como new_edit/<entry_id>, onde esse entry_id será o ID que irá especificar qual anotação estamos editando;

38 - Após, criamos uma nova view, onde implementamos uma nova função new_edit, seguindo a lógica do new_topic, mas com a diferença que antes da verificação do método post, temos um objeto para pegar uma só anotação e outro objeto que receberá a anotação e associará com o tópico dessa anotação;

39 - Agora criamos um novo template seguindo basicamente todos os passos que seguimos com os outros templates;

40 - A diferença dessa implementação é que para ela não precisamos criar um novo forms, já que iremos utilizar o forms das anotações já, onde iremos apenas modifica-la;

41 - Agora vamos fazer nossa página de login, e para isso devemos criar um novo app django, utilizando o manage.py startapp nomeDoApp;

42 - Após isso, devemos ir para pasta da aplicação do projeto, onde está o settings.py, para colocar nosso novo app dentro de 'INSTALLED_APPS', para o django reconhecer nosso novo app;

43 - Vamos na urls.py da aplicação, onde está o caminho da página inicial e da admin, e criamos um novo caminho, com o nome de users/;

44 - Agora, criamos um urls.py dentro da pasta do app users, importamos o django.urls e o django.contrib.auth, onde importaremos as views dessa biblioteca. Ela apresenta métodos prontos para efetuar o login;

45 - Criamos depois uma pasta templates e users dentro do nosso app users, para em si podermos criar a página de login. Para a criação dela, primeiro vamos extender também da base.html do nosso outro app, depois abrir nosso block content para enfim começar a implementa-la. Após isso, começamos com a lógica dos outros templates, com a diferença de incluimos um imput do tipo hidden, que irá nos redirecionar para a página inicial caso o login seja concluido corretamente;

46 - Agora precisamos fazer o logout do usuário, para isso vamos criar um novo caminho em urls.py, dentro do app users. Depois, iremos criar uma view utilizando o método logout do django, que além de ser simples na implementação, irá deixar mais simples nosso projeto. Para finalizar nosso logout, implementamos ele na base.html, que fica no nosso outro app, onde colocamos dentro do if que autentica o usuário, então quando ele for autenticado, agora conseguirá quebrar a sessão e deslogar;

47 - Agora vamos criar um registrador de usuários, para novos usuários puderem se cadastrar no site. Para isso, vamos criar um novo caminho na urls.py do app users. Após, vamos criar sua view, onde vamos utilizar novos métodos do django, o UserCreationForm, o login e o authenticate, e vamos utilizar a lógica das views antigas relacionadas com os formulários;
    - Outra diferença perceptível no código é quando vamos usar o authenticate, que para isso, criamos uma nova variável chamada new_user, que irá armazenar o formulário no banco de dados depois de validado;

48 - Criamos o register.html nos templates do app users, copiamos a página de login pois ela apresenta a mesma lógica que iremos utilizar, trocamos apenas a primeira url para poder voltar o cadastro e as strings;

49 - Por fim, criamos uma referência dela dentro da base.html, dentro do else do login caso não consiga logar, assim ele conseguirá se cadastrar;

50 - Agora vamos restringir funções para os usuários que estam logados. Primeiro temos que visualizar e teorizar o que queremos e não queremos restringir, e após isso, vamos na views onde está as funcionalidades que queremos restringir. Agora iremos importar o método login_required, que vai de uma forma simples restringir o que queremos, apenas adicionando no código o @login_required. OBS.: O LOGIN REQUIRED TEM DE SER COLOCADO ANTES DAS FUNCIONALIDADES QUE QUEREMOS RESTRINGIR, COMO ESTÁ NO CÓDIGO;

51 - Fugindo um pouco, vamos agora dar um dono para todos os tópicos que já temos criado no banco de dados. Primeiro vamo na aba models.py, que está no app learning_logs, ai criamos logo na classe Topic, uma variável com o nome de owner, onde ela também receberá uma ForeignKey, seguindo a mesma lógica do topic dentro da class Entry, mas aqui colocaremos como parâmetro o método User do django que importamos. Agora vamos abrir o shell no terminal, vamos fazer um código onde ele irá mostrar todos os usuários e todas as suas IDs. Após, vamos usar fazer um makemigrations, escolher a opção 1 e depois armazenar tudo em uma só ID, assim será possível uma pessoa ter feito todos os tópicos;
    - O código utilizado no shell: 
        from django.contrib.auth.models import User
        User.objects.all()
        for user in User.objects.all():
            print(user.username, user.id)

52 - Agora estamos fazendo uma proteção das informações que os usuários adicionam ao site. Para isso, importamos o HTTP404, que irá aparecer caso alguma pessoa tente acessar as informações de outro usuário, seja seus tópicos, suas anotações, a página de editar anotações. Para implementar isso, criamos um if onde ele irá verificar se o dono do tópico é diferente da pessoa que está tendo requisitar pela url essa página;






