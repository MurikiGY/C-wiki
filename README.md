# C-wiki

# índice
- [Importação de bibliotecas](#importação-de-bibliotecas)
- [Função Main](#a-função-main)
- [Compilação](#compilação)
- [Headers](#Arquivos-de-cabeçalho-\(Headers\))

## Importação de bibliotecas:
Para importar uma biblioteca em c, basta inserir no inicio do arquivo.
EX:
```
#include <stdio.h>
#include <math.h>
#include <string.h>
```

OBS: Algumas bibliotecas como math.h necessitam de flags de compilação



## A função Main
Função onde ocorre toda a execução do programa.
Exemplo:
```
int main(){

   return 0;
}
```
### Retorno para o sistema:
O codigo ```return 0``` serve para responder ao sistema que a execução do programa foi um sucesso. Para testar, execute no terminal depois do programa terminar:
```
echo $?
```
### Passagem de parametros na execução do terminal:
Na função main também é possivel realizar a passagem de parametros pela execução com os argumentos argc e argv.
```
int main(int argc, char **argv){

   return 0;
}
```

Onde argc é um inteiro com o número de parâmetros passados e argv é um vetor de strings que guarda os parâmetros passados. Exemplo:
```
./a.out -a teste
```
- argc conterá o valor 5
- argv será um vetor, onde:
- argv[0] == ./a.out
- argv[1] == -a
- argv[2] == teste

Para evitar falhas de segmentação também é aconselhavel realizar o teste de parametros na chamada de execução com a função getopt conforme se segue:
```
#include <unistd.h>

int option;
while( (option = getopt(argc, argv, "abc:")) != -1)
   switch(option){
      case 'a':
         command1;
         command2;
      case 'b':
         command1;
         command2;
      case 'c':
         command1;
         command2;
      default:
         fprintf (stderr, "Usage: %s -a -b -c value\n", argv[0]);
         exit(1);
    }
```
Onde na execução ./a.out é possivel passar os parametros -a, -b e -c.

OBS:

- Quando há o caracter de dois pontos ':' na string de passagem de parâmetros de getopt, entende-se que o parâmetro acompanhará um valor, podendo ser um inteiro ou uma string. Neste exemplo espera-se que sempre que houver a chamada de execução com -c, logo em seguida haverá um valor que será armazenado na variavel global "optarg".
```
./a.out -c <vallue>
```

- Quando há mais de um parâmatro com dois pontos ```("a:b:c:")``` a variável optarg conterá o valor do parâmetro de acordo com o switch case. Por exemplo, imagine uma chamada de execução ```./a.out -a <valor_a> -b <valor_b> -c <valor_c>```
```
   switch(option){
      case 'a':
         command1;   //Aqui, optarg conterá o valor <valor_a>
         command2;
      case 'b':
         command1;   //Aqui, optarg conterá o valor <valor_b>
         command2;
      case 'c':
         command1;   //Aqui, optarg conterá o valor <valor_c>
         command2;
      default:
         fprintf (stderr, "Usage: %s -a -b -c value\n", argv[0]);
         exit(1);
    }
```



## Operações em diretórios
Em C é possivel criar, excluir ou alterar diretórios.

### Criação de diretórios
```
#include <sys/stat.h>
#include <sys/types.h>

mkdir (const char *filename, mode_t mode)
```

Exemplo:
```
#include <sys/stat.h>
#include <sys/types.h>

int main (){
    int err;   //Saida de erro

    err = mkdir(nome, 0777);
    if (err == -1){
        perror("mkdir");
        exit(1);
    }
}
```

OBS:

- mkdir retorna 0 para sucesso e -1 para falha.

- filename representa o caminho relativo com o nome do diretório a ser criado.

- mode representa as permissões que o diretório possuirá, por exemplo 0777 (0 é a representação em octal e 7 é a permissão de ler, escrever e executar).

### Remoção de diretórios (vazios)
De maneira semelhante a criação de arquivos: 
```
int main (){
    int err;   //Saida de erro

    err = rmdir(nome);
    if (err == -1){
        perror("rmdir");
        exit(1);
    }
}
```

### Abertura da stream de diretórios
Diretórios são abertos através de streams de tipo DIR*, definido em <dirent.h>. Os programas não devem alocar variáveis desse tipo, apenas ponteiros para variáveis alocadas pela biblioteca.
Exemplo de abertura de uma stream:
```
int main (){
    DIR * dirstream;

    dirstream = opendir(const char <pathtodir>);
    if (!dirstream){
        perror("Não foi possivel acesssar o diretorio\n");
        exit(2);
    }
```



## Condicionais
### if-else
Com a estrutura if-else é possivel criar condições na execução. Exemplos:
```
if (<condiction>)
   command;

if (<condiction>){
   command1;
   command2;
}

if (<condiction1>)
   if (<condiction2>){
      command1;
      command2;
   }

if (<condiction>)
   command1;
else
   command2;

if (<condiction1>)
   if (<condiction2>)
      command1;
   else
      command2;
else
   command3;
```
Observações:
- Como a cláusula else fecha um if, ele sempre corresponderá a última ocorrencia de um if, a não ser que seja utilizado chaves ({..}) para fechamento do código em blocos.

### switch-case



## Resposta de execução
Para criar uma resposta de execução de programa interessante basta utilizar o seguinte código:
```
    while(conditional){
      printf("\rExecutando instruções");
      fflush(stdout);
      ...
    }
```
Onde o ```\r``` irá fazer com que o pontador pontador retorne para o inicio da linha.



## Loops




## Strings



## Streams
### Leitura da entrada padrão

### Escrita na saída padrão

### Leitura de arquivos

### Escrita em arquivos



## Algoritmos
A seguir alguns dos algoritmos mais usados em programas

### Quick sort
Uma das formas de utilizar o Quick Sort em C é por meio da função:
```
#include <stdlib.h>

static int compar(const void *p1, const void *p2){
    return strcmp(*(const char **) p1, *(const char **) p2);
}

void qsort(void *base, size_t nmemb, size_t size, int (*compar)(const void *, const void *))
```
Onde:
- *Base: Ponteiro para o primeiro elemento do vetor
- nmemb: Numero de elementos do vetor
- size:  Tamanho em bytes de um elemento do vetor (Normalmente utilizado com sizeof(tipo))
- (*compar)(const void *, const void *): Função de comparação entre os elementos retornando um valor inteiro, onde:
Menor que 0: O primeiro elemento precede o segundo pelo critério estabelecido
Igual a 0: Os dos elementos são iguais
Maior que 0: O primeiro elemento suceder o segundo pelo critério estabelecido

Exemplos de uso:
- Exemplo 1
```
#include <stdlib.h>

struct print {
    int chave;
    int index;
    int table;
};
typedef struct print print_t;

static int compare(const void *p1, const void *p2){
    return strcmp(p1, p2);
}

int main(){
    int j = <size>;
    print_t dataArr[j];

    ...

    qsort(dataArr, j, sizeof(print_t), compare);

    return 0;
}
```
OBS: Como não fora especificado na funcao ```compare``` qual variavel ordenar, a primeira variavel da estrutura é escolhida por padrão(int chave).

- Exemplo 2
```
#include <stdlib.h>

struct log {
    char   *Nome;
    char   *Data;
    int    distancia;
    int    velMedia;
    int    velMax;
    int    hrMedio;
    int    hrMax;
    int    cadMedia;
    int    subAcumulada;
};
typedef struct log log_t;

static int cmpstring(const void *p1, const void *p2){
    const log_t *a = p1;
    const log_t *b = p2;
    return strcmp(a->Nome, b->Nome);
}

int main (){
    int logTam = <size>;
    log_t vLog[logTam];

    qsort(vLog, logTam, sizeof(log_t), cmpstring);

    return 0;
}
```



## Bibliografia
- Material da WIKI de programação do professor Carlos Maziero, professor da UFPR.
[Wiki do professor](http://wiki.inf.ufpr.br/maziero/doku.php?id=prog2:start)

- [http://www.dpi.inpe.br/~carlos/Academicos/Cursos/LinguagemC/Cap_11.html](http://www.dpi.inpe.br/~carlos/Academicos/Cursos/LinguagemC/Cap_11.html)

- [Permissões 0777 vs 777](https://digitalfortress.tech/php/difference-file-mode-0777-vs-777/)

- [Rotinas de ordenação em C](https://www.dca.fee.unicamp.br/cursos/EA876/apostila/HTML/node25.html)
