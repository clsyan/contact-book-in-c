#include <stdio.h>
#include <stdlib.h>
#include <string.h>


struct Contato;
void buscaContatoTel(int qtdContatos, struct Contato *inicio), removerContato(int qtdContatos, struct Contato *inicio), listarContatos(int qtdContatos, struct Contato *inicio), buscaContato(int qtdContatos, struct Contato *inicio), menu(int qtdContatos, struct Contato *inicio), adicionarContato(int qtdContatos, struct Contato *inicio);
					
typedef struct Contato{
  char nome[50], telefone[50];
  int idade,dia, mes, ano;
  struct Contato *prox, *ant;
}contato;


int main(){
  int qtdContatos;
  contato *inicio = (contato*)malloc(sizeof(contato));
  
  menu(qtdContatos, inicio);
  return 0;
}
void menu(int qtdContatos, contato *inicio){
	int op;
  
  
  
  printf("%i contatos\n", qtdContatos);

	printf("1 - adicionar contato\n2 - buscar contato\n3 - remover contato\n");
	scanf("%i", &op);
	switch(op){
		case 1:
			adicionarContato(qtdContatos, inicio);
			break;
		case 2:
			printf("1 - buscar por nome\n2 - buscar por telefone\n3 - listar contatos\n");
			scanf("%i", &op);
			switch(op){
				case 1:
          
					buscaContato(qtdContatos, inicio);
					break;

				case 2:
					
					buscaContatoTel(qtdContatos, inicio);
					break;
				case 3:
					listarContatos(qtdContatos, inicio);
					break;
			}
			break;
		case 3:
			
			removerContato(qtdContatos, inicio);
	}
}
void removerContato(int qtdContatos, contato *inicio){

	contato *atual = inicio;
  
  char nome[50];

  printf("digite o nome: ");
	scanf("%s", nome);
  while(atual != NULL){ 
    if(strcmp(atual->nome, nome) == 0){
      if(atual == inicio){
        
        inicio = (contato*)malloc(sizeof(contato));
        free(atual);
        qtdContatos--;
        menu(qtdContatos, inicio);
      }
      atual->ant->prox = atual->prox;
      atual->prox->ant = atual->ant;
    
      free(atual);
      qtdContatos--;
      menu(qtdContatos, inicio);
    }
    else{
      atual = atual->prox;	
    }
  }
  menu(qtdContatos, inicio);
}
void listarContatos(int qtdContatos, contato *inicio){
	contato *atual = inicio;
  
	while(atual->prox != NULL){
    
		printf("------------\n%s\n%s\n%i\n%i/%i/%i\n------------\n", atual->nome, atual->telefone, atual->idade, atual->dia, atual->mes, atual->ano);

		atual = atual->prox;
	}
	menu(qtdContatos, inicio);
}

void buscaContato(int qtdContatos, contato *inicio){
  char nome[50];
	contato *atual = inicio;
  printf("digite o nome: ");
	scanf("%s", nome);
  while(atual->prox != NULL){
    if(strcmp(atual->nome, nome)==0){
      printf("%s\n%s\n%i\n%i/%i/%i\n", atual->nome, atual->telefone, atual->idade, atual->dia, atual->mes,atual->ano);
    }
    atual = atual->prox;
  }
	menu(qtdContatos, inicio);
}
void buscaContatoTel(int qtdContatos, contato *inicio){
  char tel[50];
	contato *atual = inicio;
  printf("digite o telefone: ");
	scanf("%s", tel);
  while(atual->prox != NULL){
    if(strcmp(atual->telefone, tel)==0){
      printf("%s\n%s\n%i\n%i/%i/%i\n", atual->nome, atual->telefone, atual->idade, atual->dia, atual->mes,atual->ano);
    }
    atual = atual->prox;
  }
	menu(qtdContatos, inicio);
} 
void adicionarContato(int qtdContatos, contato *inicio){

	contato *novo = (contato*)malloc(sizeof(contato));


	printf("\ndigite o nome: ");
	scanf("%s", novo->nome);
	printf("\ndigite o telefone: ");
	scanf("%s", novo->telefone);
	printf("\ndigite a idade: ");
	scanf("%i", &novo->idade);
	printf("digite a data de nascimento: ");
	scanf("%i/%i/%i", &novo->dia, &novo->mes, &novo->ano);
	
	if (inicio == NULL){
		novo->prox = NULL;
		novo->ant = NULL;

		inicio = novo;
	}
	else{
    novo->prox = inicio;
    novo->ant = NULL;
    inicio->ant = novo;
    inicio = novo;
	}
  qtdContatos++;
	menu(qtdContatos, inicio);
}