# CrawlerYAPO
Script em Python 3 para recuperar dados de anuncios da [YAPO](https://www.yapo.cl/) com base em uma planilha de entrada.

### Indice
* Sobre o código
* Instalação
	* Requisições
* Configurações
* Uso
	* Planillha de entrada
	* Processamento de dados
	* O que fazer caso o robô caia no meio de uma solicitação
* Como implementar
* Depêndencias
* Páginas fonte
* Contato

## Sobre o código
O script foi inteiramente desenvolvido em Python 3. Nomes de funções e variaveis estão em Inglês Americano, porém todos os comentários em blocos de código estão em Português do Brasil.

O script lê dados da planilha de entrada recursivamente, ou seja, funciona com multiplas linhas de uma só vez, gravando os arquivos conforme a busca atual é encerrada.

Os caminhos de inclusão dos scripts abaico partem do prinicípio que todos os arquivos estejam no mesmo diretório. Caso isso não seja possível, ou o usuário simplesmente prefira outra estruturação de diretórios, será necessário alterar as linha que possuem a keyword *require_once*, onde os caminhos são definidos.

## Instalação
Para instalar o CrawlerYAPO, basta baixar ou clonar esse repositório e copiar os arquivos para alguma hospedagem.

* **Microsoft Windows**:
> 1. Instalar o [Python 3] (https://www.python.org/downloads/release/python-390/)
> 2. Baixar esse repositório.

* **Debian/Ubuntu linux based**:
> 1. sudo apt-get install python3 -y
> 2. sudo apt-get install pip pip3 -y
> 3. git clone https://github.com/eEmmy/CrawlerYAPO.git

* **Arch linux**:
> 1. sudo pacman -S python3
> 2. sudo pacman -S pip pip3
> 3. git clone https://github.com/eEmmy/CrawlerYAPO.git

#### Requisitos
Para usar o CrawlerYAPO, deve instalar os seguintes pacotes pip:
> pip install beautifulsoup4
> pip install xlsxwritter
> pip install openpyxl

## Uso
É importante lembrar que as planilhas devem sempre estar com formato XLSX, não sendo compátivel com planilhas de outros formatos (XLS, CSV, etc.).

#### Planilha de dados
A planilha de entrada deve conter a seguintes colunas: NOME_SITE, ID_PRODUTO, ID_MARCA, PG e OUTPUT_FILE. Sendo essas seguidas imediatamente pelos itens das buscas.

Vale ressaltar que mesmo que os parametros realmente usados sejam NOME_SITE e OUTPUT_FILE, todas as colunas devem estar presentes, sendo que as outras podem ser definidas como vazias.

#### Processamento de dados
A extração dos dados, consiste numa série de requisições HTTP, que podem ser divididas em duas partes.

Primeiramente, ao iniciar a extração de dados, o script fará uma busca pelo produto dentro do site da OLX. Em seguida, calculará quantas páginas existem, para então começar a gravar os dados dentro do array de saída. Essa primeira parte retornará um dicionário com a maioria dos dados dos anuncios.

Na segunda parte do script, esse dicionário será usado como parametro de busca (Nota: Na prática, apenas o link será usado, computando menos dados e consequentemente, diminuindo o tempo do processo). Então, será feita uma solicitação HTTP para cada anúncio, e dentro da página retornada, o crawler extrai o nome do anunciante. Será retornado então, o array de dados final.

O processo de extração de dados por busca é bem longo, tendo demorado cerca de 1 minuto para retornar resultados da busca por 16 itens.

#### O que fazer caso o robô caia no meio de uma solicitação
Caso o robô caia no meio de uma solicitação, há duas linhas de ação a se seguir

1. Apagar os arquivos gerados (caso haja algum) e reiniciar as buscas.
2. Alterar as permissões da pasta dentro do servidor, para permitir que o próprio script sobrescreva os arquivos gerados anteriormente.

Como se trata de um script recursivo, independente de definir uma página inicial mais á frente da primeira, o tempo de execução do processo será o mesmo, por isso é recomendado que o script tenha permissões para sobrescrever os arquivos.

## Como implementar
A implementação é bem simples, o uso do robo deve ser feito via terminal em ambos os sistemas:

* **Todos os sistemas**:
> cd caminho/para/Crawler
> python3 bot.py

## Contato
* Email para contato: mailto:aou-emmy@outlook.com
* Telefone para contato: +55 (11) 95837-8163