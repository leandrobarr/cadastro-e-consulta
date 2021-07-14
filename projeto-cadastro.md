#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <locale.h>
#define MAX 200

typedef struct dados
{
    int codigo;
    char titulo[50];
    char descricao[50];
    char ano[6];
    int status;
    char responsavel[30];
    char prazo[30];
    char local[30];
    int custo;

} base_projetos;

int posicao = 0;

void cadastrarProjeto(base_projetos cadastro[MAX]);
void relatorioProjeto(base_projetos cadastro[MAX]);
void buscarCodigo(base_projetos cadastro[MAX]);
void buscarTitulo(base_projetos cadastro[MAX]);
void buscarStatus(base_projetos cadastro[MAX]);

int main()
{
    setlocale(LC_ALL, "Portuguese");
    base_projetos cadastro[MAX];

    int escolha;
    
    system("cls");
    do
    {
        system("cls");
        printf("###############################################################");
        printf("\n\tSISTEMA DE CADASTRO E ARMAZENAMENTO DE PROJETOS");
        printf("\n===============================================================");
        printf("\nMENU:\n");
        printf("===============================================================");
        printf("\n 1 - Cadastrar projeto");
        printf("\n 2 - Projetos cadastrados");
        printf("\n 3 - Buscar projeto por Codigo");
        printf("\n 4 - Buscar projeto por Titulo");
        printf("\n 5 - Buscar projeto por Status");
        printf("\n 6 - Sair");
        printf("\n << Escolha uma opcao do menu: ");
        scanf("%d", &escolha);
    
        switch (escolha)
        {
        case 1:
            cadastrarProjeto(cadastro);
            break;
        case 2:
            relatorioProjeto(cadastro);
            break;
        case 3:
            buscarCodigo(cadastro);
            break;
        case 4:
            buscarTitulo(cadastro);
            break;
        case 5:
            buscarStatus(cadastro);
            break;
        case 6:
            printf("\nSaindo da Aplicacao\n");
            system("Pause");
            break;
        default:
            printf("\nEscolha errada!!!\n");
            system("Pause");
        }
    } while (escolha != 6);
    return 0;
}

void cadastrarProjeto(base_projetos cadastro[MAX])
{
    system("cls");
    printf("***************************************");
    printf("\n CADASTRAR PROJETO");
    printf("\n***************************************");
    char resp = 's';

    while (resp == 's' && posicao <= MAX)
    {
        posicao++;
        printf("\nCodigo: %d ", posicao);
        //scanf("%d", &cadastro[posicao].codigo);
        cadastro[posicao].codigo = posicao;
        printf("\nInforme o titulo do projeto: ");
        fflush(stdin);
        gets(cadastro[posicao].titulo);
        printf("\nInforme a descricao do projeto: ");
        fflush(stdin);
        gets(cadastro[posicao].descricao);
        printf("\nInforme o ano do projeto: ");
        fflush(stdin);
        gets(cadastro[posicao].ano);
        printf("\nEscolha o Status do Projeto => [1] A fazer [2] Fazendo [3] Concluido: ");
        scanf("%d", &cadastro[posicao].status);
        printf("\nInforme o gerente responsavel do projeto: ");
        fflush(stdin);
        gets(cadastro[posicao].responsavel);
        printf("\nInforme o prazo do projeto: ");
        fflush(stdin);
        gets(cadastro[posicao].prazo);
        printf("\nInforme o local do projeto: ");
        fflush(stdin);
        gets(cadastro[posicao].local);
        printf("\nInforme o custo do projeto: ");
        scanf("%d", &cadastro[posicao].custo);
    
        if (posicao < MAX)
        {
            printf("\n\nDeseja cadastrar novo Projeto? [s] Sim [n] Nao: ");
            fflush(stdin);
            scanf("%c", &resp);
        }
        else
        {
            printf("\nSua base de Dados ja chegou ao limite!!!\n");
            resp = 'n';
        }
    }
}
void relatorioProjeto(base_projetos cadastro[MAX])
{
    system("cls");
    printf("***************************************");
    printf("\n PROJETOS CADASTRADOS ");
    printf("\n***************************************\n");
    int linha = 1;

    if (posicao >= 1)
    {
        while (linha <= posicao)
        {
            printf("Codigo: %d\nTitulo: %s\nDescricao: %s\nAno: %s\nStatus: %d\nGerente ResponsÃ¡vel: %s\nPrazo: %s\nLocal: %s\nCusto: %d\n\n", cadastro[linha].codigo, cadastro[linha].titulo, cadastro[linha].descricao, cadastro[linha].ano, cadastro[linha].status, cadastro[linha].responsavel, cadastro[linha].prazo, cadastro[linha].local, cadastro[linha].custo);
            linha++;
        }
    }
    else
    {
        printf("\nSem Registros Cadastrados\n");
    }
    system("Pause");
}

void buscarCodigo(base_projetos cadastro[MAX])
{
    system("cls");
    int codigo, achou;
    printf("***************************************");
    printf("\n BUSCAR PROJETO POR CODIGO ");
    printf("\n***************************************");
    printf("\nEntre com o codigo: ");
    scanf("%d", &codigo);
    achou = 0;
    int j = 0;
    while ((achou == 0) && (j <= posicao))
    {
        if (codigo == cadastro[j].codigo)
        {
            printf("Codigo: %d\nTitulo: %s\nDescricao: %s\nAno: %s\nStatus: %d\nGerente ResponsÃ¡vel: %s\nPrazo: %s\nLocal: %s\nCusto: %d\n\n", cadastro[j].codigo, cadastro[j].titulo, cadastro[j].descricao, cadastro[j].ano, cadastro[j].status, cadastro[j].responsavel, cadastro[j].prazo, cadastro[j].local, cadastro[j].custo);
            system("Pause");
        }
        j++;
    }
    if (achou == 0)
    {
        printf("\nRegistro nao encontrado com o codigo %d \n", codigo);
        system("Pause");
    }
}
void buscarTitulo(base_projetos cadastro[MAX])
{
    system("cls");
    char titulo[50];
    int achou, j;
    printf("***************************************");
    printf("\n BUSCAR PROJETO POR TITULO ");
    printf("\n***************************************");
    printf("\nEntre com o titulo (identico ao digitado): ");
    fflush(stdin);
    gets(titulo);
    achou = 0;
    j = 0;
    while ((achou == 0) && (j < MAX))
    {
        if (strcmp(cadastro[j].titulo, titulo) == 0)
        {
            printf("Codigo: %d\nTitulo: %s\nDescricao: %s\nAno: %s\nStatus: %d\nGerente ResponsÃ¡vel: %s\nPrazo: %s\nLocal: %s\nCusto: %d\n\n", cadastro[j].codigo, cadastro[j].titulo, cadastro[j].descricao, cadastro[j].ano, cadastro[j].status, cadastro[j].responsavel, cadastro[j].prazo, cadastro[j].local, cadastro[j].custo);
            system("Pause");
        }
        j++;
    }
    if (achou == 0)
    {
        printf("\nRegistro nao encontrado com o nome %s \n", titulo);
        system("Pause");
    }
}    
void buscarStatus(base_projetos cadastro[MAX])
{
    system("cls");
    int status, achou;
    printf("***************************************");
    printf("\n BUSCAR PROJETO POR STATUS ");
    printf("\n***************************************");
    printf("\nEntre com o status\n [1] a fazer [2] Fazendo [3] Concluido: ");
    scanf("%d", &status);
    achou = 0;
    int j = 0;
    while ((achou == 0) && (j <= posicao))
    {
        if (status == cadastro[j].status)
        {
            printf("Codigo: %d\nTitulo: %s\nDescricao: %s\nAno: %s\nStatus: %d\nGerente ResponsÃ¡vel: %s\nPrazo: %s\nLocal: %s\nCusto: %d\n\n", cadastro[j].codigo, cadastro[j].titulo, cadastro[j].descricao, cadastro[j].ano, cadastro[j].status, cadastro[j].responsavel, cadastro[j].prazo, cadastro[j].local, cadastro[j].custo);
            system("Pause");
        }
        j++;
    }
    if (achou == 0)
    {
        printf("\nRegistro nao encontrado com o status %d \n", status);
        system("Pause");
    }
 return(0);
}