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

//argc conterá o valor 5
//argv será um vetor, onde:
//argv[0] == ./a.out
//argv[1] == -a
//argv[2] == teste
```

Também é possivel realizar o teste de parametros na chamada de execução com ./ conforme se segue:
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
Para abrir uma stream de 




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


## Loops




## Strings
### Leitura da entrada padrão

### Escrita na saída padrão

### Leitura de arquivos

### Escrita em arquivos

## Bibliografia
- Material da WIKI de programação do professor Carlos Maziero, professor da UFPR.
[Wiki do professor](http://wiki.inf.ufpr.br/maziero/doku.php?id=prog2:start)

- [http://www.dpi.inpe.br/~carlos/Academicos/Cursos/LinguagemC/Cap_11.html](http://www.dpi.inpe.br/~carlos/Academicos/Cursos/LinguagemC/Cap_11.html)

- [Permissões 0777 vs 777](https://digitalfortress.tech/php/difference-file-mode-0777-vs-777/)
