#include <stdio.h>
#include <stdlib.h>
#include <conio.h>
#include <time.h>

//ENDEREÇAMENTO ABERTO -> POSIÇÃO = (POS+I)%TAM

#define tam 100000
int stop = 0;

typedef struct hash{
    int chave;
    char livre;
}hash;

typedef char TipoChave[100];

int transformacao(TipoChave chave){
    int i, soma = 0;

    for(i = 0; i < strlen(chave); i++){
        soma += chave[i];
    }

    return soma%tam;
}

int funcao_hashing(int num){
    return num % tam;
}

void mostrar_hash(hash tabela[]){
    for(int i = 0; i < tam; i++){
        if(tabela[i].livre == 'O'){
            printf("\nENTRADA %d: %d", i, tabela[i].chave);
        }
    }
}

void inserir(hash tabela[], int pos, int n){
    int i = 0;
    while(i < tam && tabela[(pos+i)%tam].livre != 'L' && tabela[(pos+i)%tam].livre != 'R'){
        i = i + 1;
    }

    if(i < tam){
        tabela[(pos+i)%tam].chave = n;
        tabela[(pos+i)%tam].livre = 'O';
    }else{
        printf("\nTABELA CHEIA !!");
    }
}

int buscar(hash tabela[], int n){
    int i = 0;
    int pos = funcao_hashing(n);

    while(i < tam && tabela[(pos+i)%tam].livre != 'L' && tabela[(pos+i)%tam].chave != n){
        i = i + 1;
    }

    if(tabela[(pos+i)%tam].chave == n && tabela[(pos+i)%tam].livre != 'R'){
        return (pos + i) % tam;
    }else{
        return tam;
    }
}

void remover(hash tabela[], int n){
    int posicao = buscar(tabela, n);

    if(posicao < tam){
        tabela[posicao].livre = 'R';
    }else{
        printf("\nELEMENTO NÃO ESTA PRESENTE");
    }
}

int main()
{
    hash tabela[tam];

    int op, pos, num, i;

    srand(time(NULL));
    int numAleatorio, aleatorio[tam - 1];

    for(i = 0; i < tam - 1; i++){
        numAleatorio = rand() % 100;
        aleatorio[i] = numAleatorio;
    }

    double inicio, fim, total;

    for(i = 0; i < tam; i++){
        tabela[i].livre = 'L';
    }

    do{
        system("cls");
        printf("\nMENU DE OPCOES\n");
        printf("\n1 - INSERIR ELEMENTOS ALEATORIOS");
        printf("\n2 - BUSCAR TODOS OS ELEMENTOS");
        printf("\n3 - MOSTRAR TABELA HASHING");
        printf("\n4 - EXCLUIR ELEMENTO");
        printf("\n5 - SAIR");
        printf("\nINFORME SUA OPCAO: ");
        scanf("%d", &op);

        if(op < 1 || op > 5){
            printf("\nOPCAO INVALIDA !!");
        }else{
            switch(op){
                case 1:
                    if(stop != 0){
                        printf("\nJA FORAM INSERIDOS %d NUMEROS", tam - 1);
                        printf("\nTEMPO TOTAL DE INSERCAO: %f", total);
                        break;
                    }else{
                        inicio = (double) clock() / CLOCKS_PER_SEC;

                        for(i = 0; i < tam - 1; i++){
                            inserir(tabela, funcao_hashing(aleatorio[i]), aleatorio[i]);
                        }

                        fim = (double) clock() / CLOCKS_PER_SEC;

                        total = fim - inicio;

                        printf("TEMPO TOTAL DE INSERCAO: %f", total);

                        stop = 1;

                        break;
                    }
                case 2:
                    inicio = (double) clock() / CLOCKS_PER_SEC;

                    for(i = 0; i < tam - 1; i++){
                        buscar(tabela, aleatorio[i]);
                    }

                    fim = (double) clock() / CLOCKS_PER_SEC;

                    total = fim - inicio;

                    printf("TEMPO TOTAL DE BUSCA: %f", total);

                    break;
                case 3:
                    mostrar_hash(tabela);
                    break;
                case 4:
                    printf("\nDIGITE UM NUMERO: ");
                    scanf("%d", &num);
                    remover(tabela, num);
                    break;
                default:
                    return 0;
            }
        }

        getch();
    }while(op != 5);
    return 0;
}
