<h1> Git e Github </h1> 

Artigo por Kimi. 

------

Observação: perdoem os erros (de português e de code), é somente minhas anotações de aulas. 

------

### Benefícios 

1. Controle de Versão
2. Armazenamento em Nuvem
3. Trabalho em equipe
4. Melhora seu código
5. Reconhecimento.

### Comandos Básicos para um bom desempenho no terminal

O Git é um CLI (Comand Line Interface), ou seja, na maior ele não possui interface gráfica, é utilizado por linhas de comando. Para navegar no programa é necessário aprender alguns comandos, como: mudar de pastas, listar as pastas, criar e deletar pastar/arquivos.

- **Para listar todos os arquivos de uma pasta**

  No prompt de comando, vamos listar, para podemos se situar dentro do sistema operacional. no windows o comando é o "dir", no linux o comando é o "ls".****

- **Para navegar entre as pastas**

  Se utiliza o comando "cd /" (valido para windows e linux). se quisermos ir para uma pastar, é so colocar "cd nomedapasta" e dar enter. Para voltar pra onde estava, é so colocar "cd ..", nesse caso só volta um.

- **Para limpar o prompt de comando**

  No windows usa "cls", no linux é o "clear".

um atalho "tab" ajuda a completar o nome da pasta.

- **Para criar uma pasta**

  Se utiliza o seguinte comando "mkdir nomedapasta" (valido nos dois sistemas operacionais), se der tudo certo, o terminal não vai acusar nada.

- **Para criar um arquivo dentro de uma pasta**

  Vamos utilizar o comando "echo"  que simplesmente printa de volta no terminal uma frase ou texto que vc passa, usaremos depois o redirecionamento de fluxo com ">" e colocar o hello dentro de um arquivo txt.

  ```visual-basic
  C:\\workspacce>echo hello
  hello
  C:\\workspace > echo hello > hello.txt 
  ```

  Assim criaremos um arquivo do tipo txt no diretório.

- Para deletar tudo dentro de uma pasta (windows)

  Para deletar toodos os arquivos de uma pasta, vamos usar o comando "del" (apenas Windows).

  ```visual-basic
  c:\\>del workspace
  c:\\workspace\\*, Tem certeza (s/n)?
  ```

Para visualizar os comandos já executados é só e usar a setinha para cima.

- Para excluir um diretório

  Utilizaremos o comando "rmdir nomedapasta", no linux utiliza o "rmm -rf nomedapasta"

  ```visual-basic
  C:\\>rmdir workspace /S /Q
  ```

  Esse S e esse Q eu não sei o que é não, só sei que funciona.

  Para visualizar, só listar o repositório

------

## Instalando o Git no Linux

Primeiro, vai no site https://git-scm.com/download/linux e pega o código referente ao eu sistema operacional. Abre o prompt de comando no seu computador usa o "sudo su" para pegar a permissão e coloca o link que está no site.

Instalando o Git no MacOs.

## Instalando o Git no MacOs

Primeiro instala o HomeBrew, é um gerenciador de pacotes. Depois só copiar o código e rodar no HomeBrew.

## Entendendo como o GIT funciona por baixo dos panos

## SHA

O SHA (Sicure Hash Algorithm) é um conjunto de funções hash criptográficas projetas pela NSA (Agência de Segurança Nacional dos UEA).

A grosso modo, o algoritmo pega seu arquivo e embaralha ele de uma forma muito especifica,  a encriptação gera um conjunto de caracteres identificador de 40 dígitos, de forma única. Os arquivos são encriptografados de forma segura e rápida, é uma forma curta de representar um arquivo.

```bash
Echo "ola mundo" | openssl sha1
> (studin)= f9fc856e559b950175f2b7cd7dad61facbe58e7b
```

Essa string gigante é uma forma de representar o arquivo. através desse comando "openssl sha1 nomedoarquivo" é usado para verificar se houve alteração em arquivos, já que para cada modificação é gerado um novo código.

### Objetos Internos do Git

Os objetos garatem a segurança dos arquivos. É possível também observar as alterações.

- ##### BLOBS

  Para entender o BLOBS, observe o seguinte algoritmo:

  ```basic
  echo 'conteudo' | git hash-object --stdin
  > fc31e91b26cf85a55e072476de7f263c89260eb1
  
  echo -e 'conteudo' | openssl sha1
  > 65b0d0dda479cc03cce59528e28961e498155f5c
  ```

  A função 'echo' que vai pegar uma string e cuspir essa output dessa string e a vai colocar essa output em uma função do Git, no caso "hash-object", essa stdin é para que a função entenda que a gente espera receber um arquivo.

  Quando utilizamos a função "openssl sha1" podemos verificar que o conjunto de caracteres gerados é diferente do gerado pela função "hash-object"

  Isso acontece porque a função "hash-object" é um tipo de objeto utilizado para armazenar o conteúdo de um arquivo em um repositório, ele realiza o "hash sha1"  para criptografar o arquivo,  os arquivo encriptografados é colocado dentro de um objeto chamado Blob que contém metadados dentro dele, ou seja, vai estar incluído o tipo de objeto, o tamanho do arquivo, uma '/0' e o conteúdo de fato do arquivo. Podemos verificar dessa forma:

  ```basic
  echo 'conteudo' | git hash-object --stdin
  > fc31e91b26cf85a55e072476de7f263c89260eb1
  
  echo  -e 'blob9\\0conteudo' | openssl sha1
  >  fc31e91b26cf85a55e072476de7f263c89260eb1
  ```

- ##### TREES

  As Tree armazenas os Blobs, e contém também os metadados, tem também o \0, aponta para o blobs, o sha1 e o nome do arquivo.

  A Tree (arvore) são responsáveis por estruturar a localização dos arquivos. As arvores podem apontar tanto para Blobs como para outras arvores.  As arvores também tem uma criptografia sha1, ou seja, uma arvore, com um blobs e com um arquivo txt, se nesse arquivo mudar uma virgula, a criptografia do blobs muda e a criptografia sha1 da arvore também muda.

- ##### COMMITS

  O mais importantes de todos, é o que junta tudo, aponta por uma arvore, para um parente ( o ultimo commit que veio antes), aponta para um autor, e aponta para uma mensagem também. O sha1 desse commit é o hash de toda a essa informação. Também possui metadados.

  Uma modificação de um arquivo numa blobs, muda o sha1 da blobs, que muda o sha1 da arvore, que muda o sha1 do commit.



Fonte: Digital Innovation One

Professor: Otávio Reis 