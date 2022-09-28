# C-wiki

# índice
- [Importação de bibliotecas](#a função Main)


# Importação de bibliotecas:
Para importar uma biblioteca em c, basta inserir no inicio do arquivo.
EX:
```
#include <stdio.h>
#include <math.h>
#include <string.h>
```

OBS: Algumas bibliotecas como math.h necessitam de flags de compilação



# A função Main
Função onde ocorre toda a execução do programa.
Exemplos:
```
int main(){

   return 0;
}
```
```
int main(int argc, char **argv){

   return 0;
}
```
### Retorno para o sistema:
O codigo ```return 0``` serve para responder ao sistema que a execução do programa foi um sucesso. Para testar, execute no terminal depois do programa terminar:
```
echo $?
```

### Passagem de parametros na execução do terminal:
Na função main é possivel realizar a passagem de parametros com o terminal com os argumentos argc e argv.



# Compilação

### Sistema Make



# Arquivos de cabeçalho (Headers)


