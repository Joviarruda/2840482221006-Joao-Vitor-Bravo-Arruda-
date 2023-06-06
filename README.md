# 2840482221006-Joao-Vitor-Bravo-Arruda-

#include <iostream>
#include <cstdlib>
#define MAX 9

using namespace std;

//"struct" para armaznar as variáveis e melhorar a otimização do código
typedef struct banco_de_dados{
  /* 
    quant_produto = armazenar quantos protutos tem armazenado 
    valor_produto = armazenar o valor de cada produto
    lucro = armzenar quanto a máquina lucrou
    nome_produtos = armazenar os nomes de cada produto
  */
  int quant_produto[MAX];
  double valor_produto[MAX], lucro;
  string nome_produtos[MAX];
}banco;



//uma "função void" para armazenar o nome dos produtos 
void nomes(banco *n){
  //A variavel nomeada como "n", será usada para puxar o ederenço de memória das variaveis na struct
  n->nome_produtos[0]= "Chá Matte";
  n->nome_produtos[1]= "Chá de Camomila";
  n->nome_produtos[2]= "Chá de Hortelã";
  n->nome_produtos[3]= "Isoporitos";
  n->nome_produtos[4]= "Canceritos";
  n->nome_produtos[5]= "Polvitos";
  n->nome_produtos[6]= "Guataná";
  n->nome_produtos[7]= "Coca-vida";
  n->nome_produtos[8]= "Fanta uva";
}



//uma "função void" para melhorar a otimização do código, realizar a "compra" do usuário e calcular o lucro 
void comprar(banco *c, int num){
  //A variavel nomeada como "c", será usada para puxar o ederenço de memória das variaveis na struct

  double inserido=0;

  //A variável "inserir" servira para armazenar quanto de dinheiro o usuário irá inserir na máquina
  printf("\nInsira o valor do pagamento\n");
  cin >> inserido;

  //Um comando "while" para verificar se o dinheiro inserido é maior que o produto
  while (c->valor_produto[num] > inserido){
    printf("\nValor da nota abaixo do valor do produto\nInsira uma valor maior\n");
    cin >> inserido;
  }

  //Calcular e armazenar o lucro
  c->lucro = c->lucro + c->valor_produto[num];

  //Calcular e armazenar o lucro
  c->quant_produto[num] = c->quant_produto[num] - 1;

  //system("clear||cls") serve para limpar as informações anteriores e melhorar o entendimento do usuário
  system("clear||cls");
  
  //"printf" para informar ao usuário a compra, troco e onde achar o produto
  printf("Compra efetuada :D!!\n\nSeu troco é de R$%0.2lf", inserido-c->valor_produto[num]);
  cout << "\n\nPegue seu produto " << c->nome_produtos[num] << " na abertura abaixo!\n\n";
}



//fução void para repor o estoque
void repor(banco *r){
  //A variavel nomeada como "r", será usada para puxar o ederenço de memória das variaveis na struct

  system("clear||cls");
  
  //num = irá armazenar qual produto sera reposto
  //reposicao = irá armzenar quanto será resposto
  int num=0, reposicao=0;
   
  printf(""" * * * * * Menu Produtos * * * * * \n\n0 - Chá Matte\t\t1 - Chá de Camomila\t\t2 - Chá de Hortelã\
    \n\tR$%0.2lf\t\t\t\tR$%0.2lf\t\t\t\t\tR$%0.2lf\n\
    \n3 - Isoporitos\t\t4 - Canceritos\t\t\t5 - Polvitos\
    \n\tR$%0.2lf\t\t\t\tR$%0.2lf\t\t\t\t\tR$%0.2lf\n\
    \n6 - Guataná\t\t\t7 - Coca-Vita\t\t\t8 - Fanta uva\
    \n\tR$%0.2lf\t\t\t\tR$%0.2lf\t\t\t\t\tR$%0.2lf\n\n9 - Sair\n""", r->valor_produto[0],r->valor_produto[1],r->valor_produto[2],r->valor_produto[3],r->valor_produto[4],r->valor_produto[5], r->valor_produto[6],r->valor_produto[7],r->valor_produto[8]);
  cin >> num;

  //"while" para caso o usuário queira repor mais de 1 produto
  while(num != 9){

    //impedir que o numero não seja uma das opções
    if(num>=0 && num<9){
      printf("\nQuanto deseja acidionar ao estoque?\n");
      cin >> reposicao;

      //adiciona ao estoque
      r->quant_produto[num] = r->quant_produto[num] + reposicao;
      
      system("clear||cls");
      
      printf("\nInserido com sucesso!!\n");
    }
    else {
      system("clear||cls");
      printf("\nInsira uma opção válida!!\n");
    }
    
    printf("""\n * * * * * Menu Produtos * * * * * \n\n0 - Chá Matte\t\t1 - Chá de Camomila\t\t2 - Chá de Hortelã\
      \n\tR$%0.2lf\t\t\t\tR$%0.2lf\t\t\t\t\tR$%0.2lf\n\
      \n3 - Isoporitos\t\t4 - Canceritos\t\t\t5 - Polvitos\
      \n\tR$%0.2lf\t\t\t\tR$%0.2lf\t\t\t\t\tR$%0.2lf\n\
      \n6 - Guataná\t\t\t7 - Coca-Vita\t\t\t8 - Fanta uva\
      \n\tR$%0.2lf\t\t\t\tR$%0.2lf\t\t\t\t\tR$%0.2lf\n\n9 - Sair\n""", r->valor_produto[0],r->valor_produto[1],r->valor_produto[2],r->valor_produto[3],r->valor_produto[4],r->valor_produto[5], r->valor_produto[6],r->valor_produto[7],r->valor_produto[8]);
    cin >> num;
  }
  
  system("clear||cls");
}



//fução void para mostrar o que está armzenado no estoque
void inventario(banco i){
  //A variavel nomeada como "i", será usada para puxar o ederenço de memória das variaveis na struct
  
  system("clear||cls");
  int x=0;

  printf("* * * * * Inventário * * * * *\n\n");
  
  //Imprimir o inventário
  for (x=0; x<MAX; x++){
    cout << i.nome_produtos[x];
    printf(": %i\n", i.quant_produto[x]);
    
  }
  printf("\n\n");
}



//fução void para mostrar o lucro e quanto ainda pode lucrar
void lista_lucro(banco *l){
  //A variavel nomeada como "l", será usada para puxar o ederenço de memória das variaveis na struct
  
  system("clear||cls");
  
  //faturar = irá armazenar quanto ainda pode lucrar 
  double faturar=0;
  
  printf("Lucro: R$%0.2lf", l->lucro);

  //"for" calcular o quanto ainda pode lucrar
  for(int x=0; x<MAX ; x++){
    faturar = faturar + (l->valor_produto[x]*l->quant_produto[x]);
  }

  printf("\nAinda tem a faturar: R$%0.2lf", faturar);
  printf("\n\n");
}



int main() {
  /* 
    num_produto = armzenzar e indicar qual produto deseja comprar
    modo = armzenar e indicar qual modo de operção deseja utilizar
  */
  int num_produto=1, modo=0, opcao=0, y;

  //inicializar a struct
  banco_de_dados banco;

  //inicializar a função nomes
  nomes(&banco);
  
  //adicionar valores aleatórios para as variáveis "valor_produto" e "quant_produto"
  for(int x=0; x<MAX; x++){
    banco.valor_produto[x] = 1.0+rand()%6;
    banco.quant_produto[x] = rand()%10;
  }

  //Escolher qual modo o usuário deseja utilizar
  printf(" * * * * * Qual modo deseja utilizar? * * * * * \n\n1 - Modo Usuário\n2 - Modo Administrador\n0 - Sair\n");
  cin >> modo;

  //Estrutura de repetição para caso o usuário deseje mudar de modo no meio da utilização
  while (modo!=0){
    
    //"switch" para derecionar e acinar qual modo o usuário deseja
    switch (modo){
      
      //"case 1" = modo usuário"
      case 1: {

        system("clear||cls");
        
        printf(""" * * * * * Menu Produtos * * * * * \n\n0 - Chá Matte\t\t1 - Chá de Camomila\t\t2 - Chá de Hortelã\
          \n\tR$%0.2lf\t\t\t\tR$%0.2lf\t\t\t\t\tR$%0.2lf\n\
          \n3 - Isoporitos\t\t4 - Canceritos\t\t\t5 - Polvitos\
          \n\tR$%0.2lf\t\t\t\tR$%0.2lf\t\t\t\t\tR$%0.2lf\n\
          \n6 - Guataná\t\t\t7 - Coca-Vita\t\t\t8 - Fanta uva\
          \n\tR$%0.2lf\t\t\t\tR$%0.2lf\t\t\t\t\tR$%0.2lf\n\n9 - Sair\n""", banco.valor_produto[0],banco.valor_produto[1],banco.valor_produto[2],banco.valor_produto[3],banco.valor_produto[4],banco.valor_produto[5], banco.valor_produto[6],banco.valor_produto[7],banco.valor_produto[8]);
        cin >> num_produto;
        
        //Estrutura de repetição para caso o usuário deseje fazer multiplas compras 
        while (num_produto!=MAX){

          //"if" para verificar se o produto esta dentro das opções
          if (num_produto >= 0 && num_produto <MAX){

            //"if" para verificar se o produto está no estoque
            if (banco.quant_produto[num_produto] == 0){
              printf("Produto em falto de estoque no momento!!\n\n");
            }
            else{
              comprar(&banco, num_produto);
            }
          }
          else{
            printf("Insira um dos produtos indicados na tela!!\n");
          }
          
          printf(""" * * * * * Menu Produtos * * * * * \n\n0 - Chá Matte\t\t1 - Chá de Camomila\t\t2 - Chá de Hortelã\
          \n\tR$%0.2lf\t\t\t\tR$%0.2lf\t\t\t\t\tR$%0.2lf\n\
          \n3 - Isoporitos\t\t4 - Canceritos\t\t\t5 - Polvitos\
          \n\tR$%0.2lf\t\t\t\tR$%0.2lf\t\t\t\t\tR$%0.2lf\n\
          \n6 - Guataná\t\t\t7 - Coca-Vita\t\t\t8 - Fanta uva\
          \n\tR$%0.2lf\t\t\t\tR$%0.2lf\t\t\t\t\tR$%0.2lf\n\n9 - Sair\n""", banco.valor_produto[0],banco.valor_produto[1],banco.valor_produto[2],banco.valor_produto[3],banco.valor_produto[4],banco.valor_produto[5], banco.valor_produto[6],banco.valor_produto[7],banco.valor_produto[8]);
          cin >> num_produto;
        }
        //"break" serve para finalizar o "switch"
        break;
      }


      
      //"case 2" = modo administrador"
      case 2:{

        system("clear||cls");
        
        printf(" * * * * * Menu ADM * * * * * \n\n1 - Repor produtos\n2 - Listar Inventário\n3 - Listar Lucro\n0 - Sair\n");
        cin >> opcao;

        //Estrutura de repetição para caso o usuário deseje realizar mais de uma ação
        while(opcao != 0){

          //"if == 1" = irá para um função onde podera selecionar qual produto deseja repor/adicionar
          if(opcao == 1){
            repor(&banco);
          }

          //"if == 2" = irá para um função ira imprimir o inventário
          else if(opcao == 2){
            inventario(banco);
          }

          //"if == 3" = irá para um função para listar o lucro e a o que ainda pode lucrar
          else if(opcao == 3){
            lista_lucro(&banco);
          }
            
          else{
            printf("Insira um dos opções indicados na tela!!\n");
          }
          
          printf(" * * * * * Menu ADM * * * * * \n1 - Repor produtos\n2 - Listar Inventário\n3 - Listar Lucro\n0 - Sair\n");
          cin >> opcao;
        }
        break;
      }
    }

    system("clear||cls");
    
    printf(" * * * * * Qual modo deseja utilizar? * * * * * \n\n1 - Modo Usuário\n2 - Modo Administrador\n0 - Sair\n");
    cin >> modo;
  }
}
