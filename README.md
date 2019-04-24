# Coisas que eu esqueço
* COISAS QUE EU ESQUEÇO
* COISAS PARA TREINAR
* COISAS QUE EU APRENDI
* COISAS DE COISAR



# Comando para criar um ambiente virtual: 
- python3 -m venv nomeDoAmbiente
- . nomeDoAmbiente/bin/activate
- Para desativar so digitar deactivate no terminal

# Instalando Django
- pip install django
- django-admin startproject
- python3 manage.py createsuperuser
- python3 manage.py runserver

# Criar arquivo de requerimentos do meu sistema.
- pip freeze > requirements.txt

- **Instalar os requerimentos do meu sistema caso eu passe para alguem.**
- pip install -r requirements-dev.txt

# Criando minha APP
- python manage.py startapp nomeDaMinhaAPP

# git inicio do projeto, não esquecer
git init -> cria a inicialização do versionamento do codigo.

# Criar arquivo .gitignore
- *.sqlite3
- *.venv
- *pyc
- .DS_Store
- media
- .env

# Settings.py

- LANGUAGE_CODE = 'pt-br'

- TIME_ZONE = 'America/Sao_Paulo'

- STATIC_URL = '/static/'
- MEDIA_URL = '/media/'
- STATICFILES_DIRS = [os.path.join(BASE_DIR, 'static')]
- STATIC_ROOT = os.path.join(BASE_DIR, 'static_root')
- MEDIA_ROOT = os.path.join(BASE_DIR, 'media_root')


A pasta static e a pasta media, devem ficar na raiz do seu projeto. (mesmo nivel do manage.py)

# Templates

### Dentro do arquivo.html
- Você não pode esquecer de colocar no começo dele {% load static %}

### Exemplo de como carregar um arquivo que está dentro dos seus arquivos estaticos, 
- nesse exemplo o my_app é uma sub-pasta da minha pasta estaticos.

<img src="{% static "my_app/example.jpg %}" alt="My image"/>


# Arquivos de media

### Media_url é o caminho que vc vai usar pra carregar as medias (ex: fotos)
MEDIA_URL = '/media/'

# Media é a pasta onde vc vai salvar os arquivos de media.
MEDIA_ROOT = 'media'

### Ao adicionar um campo no seu models sendo ImageField, 
- vc deve instalar o Pillow (**pip install Pillow**)

### Agora no models.py criar um campo de photo.
photo = models.ImageField(**upload_to='clients_photos'**)

**OBS:A parte que está uploat_to é o seguinte, o django vai criar uma pasta  caso ela não exista com o nome que vc colocou e todas as imagens, que foram adicionadas nesse formulario será salvada JUNTAS dessa pasta.**
- para deixar um campo opcional basta colocar: null=True, blank=True

# Gambiarra para conseguir servir imagens durante o desenvolvimento do sistema.
### No arquivo urls.py
**importar:**
- from django.conf import settings
- from django.conf.urls.static import static

### No final do urlpattern colocar esse codigo:
+ static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)

# Ajudas pra ganhar tempo e não precisar ficar digitando.

### urls que geralmente crio, listar, criar, detalhes, atualizar, deletar.
**dependendo posso usar a update para detalhes ai tem depende do projeto.**

- from myapp.views import Create, Delete, Update

- urls.py

- urlpatterns = [
    -  path('myapp/list/', PersonList.as_view(), name='myapp_list'),
    -  path('myapp/create/', PersonCreate.as_view(), name='myapp_create'),
    -  path('myapp/detail/<int:pk>/', PersonDetail.as_view(), name='myapp_detail'),
    -  path('myapp/update/<int:pk>/', PersonUpdate.as_view(), name='myapp_update'),
    -  path('myapp/delete/<int:pk>/', PersonDelete.as_view(), name='myapp_delete'),
]


### models.py

    ESCRITA = models.CharField(max_length=30, null=True, blank=True)
    NUM_INT = models.IntegerField(null=True, blank=True)
    NUM_DEC = models.DecimalField(max_digits=5, decimal_places=2)
    TEXTO = models.TextField(null=True, blank=True)
    FOTO = models.ImageField(upload_to='clients_photos', null=True, blank=True)
    FK = models.OneToOneField(Documento, null=True, blank=True, on_delete=models.CASCADE)


# ENTREGAR UM TEMPLATE DIRETO SEM PRECISAR CRIAR UMA VIEW:

### Caso não precise criar uma view posso mandar direto um template assim:
    path('home2/', TemplateView.as_view(template_name='home2.html'), name='home2'),
    
**obs: não esquecer de criar o arquivo .html e colocar na pasta da app.**
