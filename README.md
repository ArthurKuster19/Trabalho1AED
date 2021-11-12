# Trabalho1AED
Descrição : Sistema de academia em C# que terá class matricula que vai coletar os dados acerca do usuário a class treinos que vai especificar o que vai ocorrer nas modalidades, class main que operar as outras classes.

Relatório 1:  Foi iniciado um brainstorm sobre o planejamento dos atribuitos e tipos de métodos que serao implementado no projetos eo que deve ser seguido para a conclusão do projeto.

Relatorio 2:Termino da primeira class ea segunda classe em andamento para o final.




using System;
using System.IO;
using System.Collections.Generic;
using System.Linq;


class Matricula{
  
  private string nome;
  private string modalidade;
  private string aux;
  private float preco;
  private int periodo;
  public string arqdados;
  
 public void Obterdados(){
  
   Console.WriteLine("Digite seu nome e sobrenome: ");
    nome=Console.ReadLine();
    
   Console.WriteLine("Digite a modalidade desejada: (Digite (m) para musculaçao e (z) para zumba ");
    aux=Console.ReadLine();
        switch(aux){
            case "m":
            modalidade = "musculaçao";
               break;
            case "z":
            modalidade = "zumba";
               break;
   }      
   Console.WriteLine("Digite o periodo de tempo (em meses) que prentede fazer(alunos que optarem por 12 meses ou mais receberao um desconto de  (15 R$) em todas as suas mensalidades): ");
    periodo=int.Parse(Console.ReadLine());
    
 }
 public void Calcularprec() {
    switch(aux){
     case "m":
      preco = 100;
       break;
     case "z":
      preco = 80;
       break;
   }         
   if(periodo >= 12){
     preco=(preco-15);
   }
 }
 
 public void Exibirdados(){
    Console.WriteLine("----------------------------");   
    Console.WriteLine("Matricula realizada");
    Console.WriteLine("nome: {0} | modalidade: {1} | periodo: {2} meses | preço das mensalidades: {3}",nome ,modalidade, periodo, preco);
    Console.WriteLine("----------------------------"); 
 }

 public void Gravar(){
  this.arqdados = "bancodedados.txt";
  StreamWriter escrv = new StreamWriter(this.arqdados,true);
  escrv.WriteLine(nome + ";" + modalidade);   

  escrv.Close();

 }
}
 class Banco{
  private string nomealuno;
  public string nomee;
  public string modalidadee;
 public void encontrar(string name){
    TextReader Leitor = new StreamReader("bancodedados.txt", true);
  
  int Linhas = 0;
  
  nomealuno = name;

  while (Leitor.Peek() != -1) {//Enquanto o arquivo não acabar, o Peek não retorna -1 sendo adequando para o loop while...
    Linhas++;
    Leitor.ReadLine();
}
  Leitor.Close();
 
  string[] pessoas = File.ReadAllLines("bancodedados.txt");
      for(int i = 0; i < Linhas;i++){
        
        if(pessoas[i] == (nomealuno +";"+"zumba") ){
              nomee = nomealuno;   
              modalidadee = "zumba"; 
                
        }
        if(pessoas[i] == (nomealuno +";"+"musculaçao")){
              nomee = nomealuno;
              modalidadee = "musculaçao";
   }
  }
 }
  public void retornanome(){
     Console.WriteLine("Nome: {0}",nomee);
     Console.WriteLine("Modaliade: {0}",modalidadee);
  }

}
class Treino{
  private string mod;
  private string [] dias = new string [5] ;
  private string treinoA; 
  private string treinoB;
  private int tipodetreino;
  private string exibir;
 
 public void Escolhertreino(string mn){
  mod = mn;
   switch(mod){
     case "musculaçao":
        treinoA= "Maratona";
        treinoB= "Pesos";
       Console.WriteLine("Você deseja ter uma carga de treino mais voltada para: Emagrecimento(digite 1) ou Ganho Muscular (Digite 2)");
       tipodetreino=int.Parse(Console.ReadLine());
       
       if(tipodetreino == 1){
          for(int i = 0; i < 5; i++){
            if(i < 2){
             dias[i] = treinoB;

            }else{
            dias[i] = treinoA;
            }
        
          }
       }
       if(tipodetreino == 2){
          for(int i = 0; i < 5; i++){
            if(i < 2){
             dias[i] = treinoA;

            }else{
            dias[i] = treinoB;
            }
          }
          
       }
       break;
     case "zumba":
        treinoA= "Danças Simples";
        treinoB= "Exercios com música";
       Console.WriteLine("Você deseja ter uma carga de treino mais voltada para: Exercios com musica (digite 1) ou Coreografia (Digite 2)");
        tipodetreino=int.Parse(Console.ReadLine());

       if(tipodetreino == 1){
          for(int i = 0; i < 5; i++){
            if(i < 2){
             dias[i] = treinoB;

            }else{
            dias[i] = treinoA;
            }
        
          }
       }
       if(tipodetreino == 2){
          for(int i = 0; i < 5; i++){
            if(i < 2){
             dias[i] = treinoA;

            }else{
            dias[i] = treinoB;
            }
          }
       }
       break;
   }         
 } 
 public void Exibirtreino() {
   for(int i = 0; i < 5; i++){
     exibir = dias[i];
     switch(i){
        case 0 :
     Console.WriteLine("Sengunda-Feira - {0}", exibir);
        break;
        case 1 :
     Console.WriteLine("Terça-Feira - {0}", exibir);
        break;
        case 2 :
     Console.WriteLine("Quarta-Feira - {0}", exibir);
        break;
        case 3 :
     Console.WriteLine("Quinta-Feira - {0}", exibir);
        break;
        case 4 :
     Console.WriteLine("Sexta-Feira - {0}", exibir);
        break;
        
     }
   }
 }
}

class Central{
  
 public static void Main() {
   
   Console.WriteLine("Você deseja realizar uma matricula Sim (digite 1) ou Não (Digite 2)");
      int confirmar1=int.Parse(Console.ReadLine());

      if(confirmar1 == 1){
         Matricula m1=new Matricula();
           m1.Obterdados();
           m1.Calcularprec();
           m1.Exibirdados();
           m1.Gravar();
      }
   Console.WriteLine("Você deseja escolher as especificações do treino desta semana se Sim (digite 1) ou Não (Digite 2)");
      int confirmar2=int.Parse(Console.ReadLine());
      
      if(confirmar2 == 1){
          Console.WriteLine("Digite o nome e sobrenome da pessoa para obter o treino semanal programado :");
            string buscarnome = Console.ReadLine();
              Banco b1 = new Banco();
              Treino t1=new Treino();
             
              b1.encontrar(buscarnome);
              t1.Escolhertreino(b1.modalidadee);
             
              Console.WriteLine("----------------------------"); 
              Console.WriteLine("--ROTINA DE TREINO SEMANAIS--");
              
              b1.retornanome();
              t1.Exibirtreino();
              
              Console.WriteLine("----------------------------"); 
      }
      
  }
}
