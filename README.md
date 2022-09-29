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



## Compilação
### Sistema Make



## Arquivos de cabeçalho (Headers)




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
Na função main é possivel realizar a passagem de parametros pela execução com os argumentos argc e argv.
```
int main(int argc, char **argv){

   return 0;
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


## Loops




## Strings
### Leitura da entrada padrão

### Escrita na saída padrão

### Leitura de arquivos

### Escrita em arquivos


