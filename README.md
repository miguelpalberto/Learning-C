# Learning-C
Copy of the code:
```
//This is the result of a set of exercises taken to train and understand vectors and structures in C.
//This program requests the data for a list of students, showing at the end said data

#include <stdio.h>
#include <stdlib.h>

#define MAX_ESTUDANTES 100

typedef struct
{
    int dia;
    char mes[10]; //tambem podia ser um int e punhamos numero
    int ano;
} tipoData;

typedef struct
{
    int numero;
    char nome[50];
    tipoData dataAvaliacao;
    int nota;
} tipoEstudante;

int lerQuantidadeAvaliados();
int lerInteiro(int min, int max);
void limpaBufferStdin(void);
tipoEstudante lerDadosEstudante(tipoEstudante vetorEstudante[MAX_ESTUDANTES], int nAvaliados, int aluno);
tipoEstudante lerNotas(tipoEstudante vetorEstudantes[MAX_ESTUDANTES], int nAvaliados, int aluno);
void mostrarDados(tipoEstudante vetorEstudantes[MAX_ESTUDANTES], int nAvaliados, int aluno);


int main()
{
    tipoEstudante vetorEstudante[MAX_ESTUDANTES];
    int nAvaliados, aluno = 0;

    nAvaliados = lerQuantidadeAvaliados();

    for(aluno=0; aluno<nAvaliados; aluno++)
    {
        vetorEstudante[aluno] = lerDadosEstudante(vetorEstudante, nAvaliados, aluno);
    }
    for(aluno=0; aluno<nAvaliados; aluno++)
    {
        vetorEstudante[aluno] = lerNotas(vetorEstudante, nAvaliados, aluno);
    }
    for(aluno=0; aluno<nAvaliados; aluno++)
    {
        mostrarDados(vetorEstudante, nAvaliados, aluno);
    }

    return 0;
}

////////////////////////////////////////////////////////////////
/////   lerQuantidadeAvaliados
int lerQuantidadeAvaliados()
{
    int nAvaliados=0;
    do
    {
        printf("\nInsira numero total de alunos a serem avaliados (max 100): ");
        nAvaliados = lerInteiro(0, 100);
    }
    while(nAvaliados<0 || nAvaliados>100);
    return nAvaliados;
}
/////   lerInteiro  /////
int lerInteiro(int min, int max)
{
    int numero,controlo;
    do
    {
        controlo = scanf("%d", &numero);
        limpaBufferStdin();
    }
    while (numero<min || numero>max || controlo==0);
    return numero;
}
////    limpaBuffer  /////
void limpaBufferStdin(void)
{
    char lixo;
    do
    {
        lixo = getchar();
    }
    while (lixo!='\n' && lixo!=EOF);
}
/////
///// lerDadosEstudante  /////
tipoEstudante lerDadosEstudante(tipoEstudante vetorEstudante[MAX_ESTUDANTES], int nAvaliados, int aluno)
{

    tipoEstudante dadosEstudante;

    printf("\nNumero escolar do estudante (1 a 9999) %d: ", aluno);
    dadosEstudante.numero = lerInteiro(1,9999);
    printf("Nome do estudante %d: ", aluno);
    fgets(dadosEstudante.nome, 50, stdin); //stdin -> uma propriedade do fgets - neste caso pomos para 50 ser o maximo e a partir dai ir tudo para o stdin/buffer
    return dadosEstudante;
}
/////
/////   lerNotas  /////
tipoEstudante lerNotas(tipoEstudante vetorEstudantes[MAX_ESTUDANTES], int nAvaliados, int aluno)
{

    tipoEstudante dadosEstudante;

    printf("\nData da avaliacao do estudante %d: \n", aluno);
    printf("\tDia: ");
    dadosEstudante.dataAvaliacao.dia = lerInteiro(1,9999);
    printf("\tMes: ");
    fgets(dadosEstudante.dataAvaliacao.mes, 10, stdin);
    printf("\tAno: ");
    dadosEstudante.dataAvaliacao.ano = lerInteiro(1,9999);

    printf("\nNota da avaliacao do estudante %d: ", aluno);
    dadosEstudante.nota = lerInteiro(1,9999);

    return dadosEstudante;
}
/////
///// mostrarDados  /////
void mostrarDados(tipoEstudante vetorEstudantes[MAX_ESTUDANTES], int nAvaliados, int aluno)
{

    if (nAvaliados == 0)
    {
        printf("\n Nao existem estudantes avaliados.");
    }
    else
    {
        printf("\nDADOS ESTUDANTE %d:\n", aluno);
        printf("Numero: %d \t\t", vetorEstudantes[aluno].numero);
        printf("Nome: %s", vetorEstudantes[aluno].nome);
        printf("\nData Avaliacao: %d-%s-%d\n", vetorEstudantes[aluno].dataAvaliacao.dia, vetorEstudantes[aluno].dataAvaliacao.mes, vetorEstudantes[aluno].dataAvaliacao.ano);
        printf("Nota: %d \n", vetorEstudantes[aluno].nota);
    }
}
```
