#include <stdio.h>
#include <stdlib.h>
#include <conio.h>
#include <time.h>

#define tam 100000

typedef struct arvore{
    int num;
    struct arvore *esq, *dir;
}arvore;

arvore* inserir(arvore* aux, int num){
    if(aux == NULL){
        aux = (arvore *) malloc(sizeof(arvore));
        aux->num = num;
        aux->dir = NULL;
        aux->esq = NULL;
    }else if(num < aux->num){
        aux->esq = inserir(aux->esq, num);
    }else{
        aux->dir = inserir(aux->dir, num);
    }

    return aux;
}

int consultar(arvore *aux, int num, int achou){
    if(aux != NULL && achou == 0){
        if(aux->num == num){
            achou = 1;
        }else if(num < aux->num){
            achou = consultar(aux->esq, num, achou);
        }else{
            achou = consultar(aux->dir, num, achou);
        }
    }

    return achou;
}

void emOrdem(arvore *aux){
    if(aux != NULL){
        emOrdem(aux->esq);
        printf("\n%d", aux->num);
        emOrdem(aux->dir);
    }
}

void preOrdem(arvore *aux){
    if(aux != NULL){
        printf("\n%d", aux->num);
        preOrdem(aux->esq);
        preOrdem(aux->dir);
    }
}

void posOrdem(arvore *aux){
    if(aux != NULL){
        posOrdem(aux->esq);
        posOrdem(aux->dir);
        printf("\n%d", aux->num);
    }
}

arvore* remover(arvore *aux, int num){
    arvore *p, *p2;
    if(aux->num == num){
        if(aux->esq == aux->dir){
            free(aux);
            return NULL;
        }else if(aux->esq == NULL){
            p = aux->dir;
            free(aux);
            return p;
        }else if(aux->dir == NULL){
            p = aux->esq;
            free(aux);
            return p;
        }else{
            p2 = aux->dir;
            p  = aux->dir;
            while(p->esq != NULL){
                p = p->esq;
            }
            p->esq = aux->esq;
            free(aux);
            return p2;
        }
    }else if(aux->num < num){
        aux->dir = remover(aux->dir, num);
    }else{
        aux->esq = remover(aux->esq, num);
    }

    return aux;
}

arvore* desalocar(arvore* aux){
    if(aux != NULL){
        aux->esq = desalocar(aux->esq);
        aux->dir = desalocar(aux->dir);
        free(aux);
    }

    return NULL;
}

int main()
{
    srand(time(NULL));

    arvore *raiz = NULL, *aux;
    int op, achou, aleatorios[tam];
    double inicio, fim, total;

    for(int i = 0; i < tam; i++){
        aleatorios[i] = rand() % 10000;
    }

    do{
        system("cls");
        printf("\nMENU DE OPCOES\n");
        printf("\n1 - INSERIR NUMEROS ALEATORIOS NA ARVORE");
        printf("\n2 - CONSULTAR TODA A ARVORE");
        printf("\n3 - EXCLUIR TODOS OS ELEMENTOS DA ARVORE");
        printf("\n4 - ESVAZIAR ARVORE");
        printf("\n5 - SAIR");
        printf("\nINFORME SUA OPCAO: ");
        scanf("%d", &op);

        if(op < 1 || op > 5){
            printf("\nOPCAO INVALIDA");
        }else if(op == 1){
            inicio = (double) clock() / CLOCKS_PER_SEC;

            for(int i = 0; i < tam; i++){
                raiz = inserir(raiz, aleatorios[i]);
            }

            fim = (double) clock() / CLOCKS_PER_SEC;

            total = fim - inicio;

            printf("\nVETOR ALEATORIO INSERIDO NA ARVORE");
            printf("\nTEMPO DE INSERCAO: %f", total);
        }else if(op == 2){
            if(raiz == NULL){
                printf("\nARVORE VAZIA !!");
            }else{
                inicio = (double) clock() / CLOCKS_PER_SEC;

                for(int i = 0; i < tam; i++){
                    achou = 0;
                    achou = consultar(raiz, aleatorios[i], achou);
                }

                fim = (double) clock() / CLOCKS_PER_SEC;

                total = fim - inicio;

                printf("\nTEMPO DE BUSCA: %f", total);
            }
        }else if(op == 3){
            if(raiz == NULL){
                printf("\nARVORE VAZIA !!");
            }else{
                inicio = (double) clock() / CLOCKS_PER_SEC;

                for(int i = 0; i < tam; i++){
                    achou = 0;
                    achou = consultar(raiz, aleatorios[i], achou);
                    if(achou != 0){
                        raiz = remover(raiz, aleatorios[i]);
                    }
                }

                fim = (double) clock() / CLOCKS_PER_SEC;

                total = fim - inicio;

                printf("\nTEMPO DE EXCLUSAO DE TODOS OS ELEMENTOS: %f", total);
            }
        }else if(op == 4){
            if(raiz == NULL){
                printf("\nARVORE VAZIA !!");
            }else{
                raiz =  desalocar(raiz);

                printf("\nARVORE ESVAZIADA !!");
            }
        }

        printf("\n\n");
        system("pause");
    }while(op != 5);

    raiz = desalocar(raiz);
    return 0;
}
