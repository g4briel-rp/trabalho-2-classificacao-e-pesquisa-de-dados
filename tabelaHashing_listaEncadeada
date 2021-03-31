#include <stdio.h>
#include <stdlib.h>
#include <conio.h>
#include <time.h>
#include <string.h>

#define tam 100000
int stop = 0;

typedef struct hash{
    int chave;
    struct hash* prox;
}hash;

typedef char TipoChave[100];

int transformacao(TipoChave chave){
    int i, soma = 0;

    for(i = 0; i < strlen(chave); i++){
        soma += chave[i];
    }

    return soma%tam;
}

void inserir(hash* tabela[], int pos, int n){
    hash *novo = (hash *) malloc(sizeof(hash));
    novo->chave = n;
    novo->prox = tabela[pos];
    tabela[pos] = novo;
}

int funcao_hashing(int num){
    return num % tam;
}

void mostrar_hash(hash* tabela[]){
    hash* aux;

    for(int i = 0; i < tam; i++){
        aux = tabela[i];
        while(aux != NULL){
            printf("\nENTRADA %d: %d", i, aux->chave);
            aux = aux->prox;
        }
    }

    printf("\n");
}

void excluir_hash(hash* tabela[], int num){
    int pos = funcao_hashing(num);
    hash* aux;

    if(tabela[pos] != NULL){
        if(tabela[pos]->chave == num){
            aux = tabela[pos];
            tabela[pos] = tabela[pos]->prox;
            free(aux);
        }else{
            aux = tabela[pos]->prox;
            hash* ant = tabela[pos];
            while(aux != NULL && aux->chave != num){
                ant = aux;
                aux = aux->prox;
            }

            if(aux != NULL){
                ant->prox = aux->prox;
                free(aux);
            }else{
                printf("\nNUMERO NAO ENCONTRADO");
            }
        }
    }else{
        printf("\nNUMERO NAO ENCONTRADO");
    }
}

int buscar(hash* tabela[], int num){
    int pos = funcao_hashing(num);
    hash* aux;

    if(tabela[pos] != NULL){
        if(tabela[pos]->chave == num){
            return pos;
        }else{
            aux = tabela[pos]->prox;
            hash* ant = tabela[pos];
            while(aux != NULL && aux->chave != num){
                ant = aux;
                aux = aux->prox;
                pos = funcao_hashing(aux);
            }

            if(aux != NULL){
                return pos;
            }else{
                return tam;
            }
        }
    }else{
        return tam;
    }
}

int main()
{
    hash* tabela[tam];
    hash* aux;
    int op, pos, num, i;

    srand(time(NULL));
    int numAleatorio, aleatorio[tam - 1];

    for(i = 0; i < tam - 1; i++){
        numAleatorio = rand() % 100;
        aleatorio[i] = numAleatorio;
    }

    double inicio, fim, total;

    for(i = 0; i< tam; i++){
        tabela[i] = NULL;
    }

    do{
        system("pause");
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
                        printf("\nTEMPO TOTAL DE INSERCAO: %f\n\n", total);
                    }else{
                        inicio = (double) clock() / CLOCKS_PER_SEC;

                        for(i = 0; i < tam - 1; i++){
                            inserir(tabela, funcao_hashing(aleatorio[i]), aleatorio[i]);
                        }

                        fim = (double) clock() / CLOCKS_PER_SEC;

                        total = fim - inicio;

                        printf("TEMPO TOTAL DE INSERCAO: %f\n\n", total);

                        stop = 1;
                    }
                    break;
                case 2:
                    inicio = (double) clock() / CLOCKS_PER_SEC;

                    for(i = 0; i < tam - 1; i++){
                        buscar(tabela, aleatorio[i]);
                    }

                    fim = (double) clock() / CLOCKS_PER_SEC;

                    total = fim - inicio;

                    printf("TEMPO TOTAL DE BUSCA: %f\n\n", total);
                    break;
                case 3:
                    mostrar_hash(tabela);
                    getch();
                    break;
                case 4:
                    printf("\nDIGITE UM NUMERO: ");
                    scanf("%d", &num);
                    excluir_hash(tabela, num);
                    break;
                default:
                    return 0;
            }
        }
    }while(op != 5);

    for(i = 0; i < tam; i++){
        while(tabela[i] != NULL){
            aux = tabela[i];
            tabela[i] = tabela[i]->prox;
            free(aux);
        }

        tabela[i] = NULL;
    }

    return 0;
}
