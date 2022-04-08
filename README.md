#include <stdio.h>
#include<stdlib.h>

typedef struct pro{
   int identifiant ;
   int temprestant ;
   int date_arrive ;
   int priorite ;
   struct pro *suiv ;
}process;

typedef struct File  {
  process *tete ;
  process *que  ;
 
   };

typedef struct File *file ;

int size ;

process *create_process(int id ,int r_time ,int a_time,int p ){
   process *proc ;
   proc=(process *)malloc(sizeof(process));
   if(proc==NULL){printf("ALLO NON REUSSI !!");}
   proc->identifiant=id ;
   proc->temprestant= r_time ;
   proc->date_arrive=a_time ;
   proc->priorite=p ;
   proc->suiv=NULL ;
   return proc ;
};



file ini_file(int n ){
   file f ;
   f=(file)malloc(sizeof(file));
   if(f==NULL){printf("ALO non reussi !!");};
   f->tete=NULL ;
   f->que=NULL ;
   size=n ;
   return f ;
};

void enfiler(file f , process *p ){
  
   if(f->que==NULL){f->que=p;
                    f->tete=p; 
                    
                    }else{f->que->suiv=p;
                                      f->que=p;};
                                      
   }; 

process *read_process(file f){
   process *p ;
   if(f->que==NULL){
       printf("File est vide !!");
       exit(1);
     }else{
        p=f->tete ;
     }; 
     return p ;
};

process *pop_process(file f){
   process *temp ;
   if(f->tete== NULL){printf("La Fille est vide !! ");
   exit(1);
   }else{
     temp=f->tete;
     f->tete=f->tete->suiv ;
   };
   
   return temp;
};


   


file creer_file(int n){
  int identifiant ;
 int temprestant ;
   int date_arrive ;
   int priorite ;
  int i ;
  file F ;
  F=ini_file(n);
  process *pr ;
  for(i=0;i<n;i++){
   printf("Remplissage du processus num %d :\n",i+1);
   printf("\n\t\t\tDonner l'identifiant :");
   scanf("%d",&identifiant);
   printf("\n\t\t\tDonner le temp restant :\n");
   scanf("%d",&temprestant);
   printf("\n\t\tDonner la date d'arrivee :\n");
   scanf("%d",&date_arrive);
   printf("\n\t\tDonner la priorite :\n");
   scanf("%d",&priorite);
   pr=create_process(identifiant,temprestant,date_arrive,priorite);
   enfiler(F,pr);
  };
  return F ;
};

void push_fifo(file f){
   int i ,j;
   process *val ;
   int n,som ;
   som=0 ;
   process *tab[size];
   printf("\n\n\n\nLa taille est %d\n",size);
   for(i=0;i<size;i++){
     
      tab[i]=pop_process(f);
   };

   for(i=0;i<size;i++){
        for(j=i;j<size;j++){
        if(tab[i]->date_arrive>=tab[j]->date_arrive){
            val=tab[i];
            tab[i]=tab[j];
            tab[j]=val ;
        };
        };
    };

   for(i=0;i<som;i++){
      som+=tab[i]->temprestant ;
      printf("\n\n;;;;;;;LA SOMME EST %d ///..............\n\n",som);
   };
         
   printf("Process\t:\t1\t2\t3\t4\t5 \n");
   for(i=0;i<20;i++){ 
      printf("%d",i+1);
      printf("             "); 
      for(j=0 ; j<size ;j++){
              if(((tab[j]->temprestant) > 0 ) && ((tab[j]->date_arrive) >= i )){
              if(j==0){                   printf("O\t"); 
                                          (tab[j]->temprestant)-- ; }else{
                                             if(((tab[j-1])->temprestant > 0)){printf("X\t");}else{printf("o\t");
                                             (tab[j]->temprestant)-- ;};
                                 };}else{ printf("\t\t");  
                                    }; 
      }; printf("\n");};};
   


void affiche(file f){
   int i,j ;
   file t;
   t=f;
   process *tab[size];
   process *val ;
  
   
   
   for(i=0;i<size;i++){
      
      tab[i]=pop_process(f);
   }; 
   
   for(i=0;i<size;i++){
        for(j=i;j<size;j++){
        if(tab[i]->date_arrive>=tab[j]->date_arrive){
            val=tab[i];
            tab[i]=tab[j];
            tab[j]=val ;
        };
        };
    };
   for(i=0;i<size;i++){
      printf("%d\n",tab[i]->identifiant);
      printf("%d\n",tab[i]->date_arrive);
      printf("%d\n",tab[i]->priorite);
    
       
   };
};


int main(){
  int n ;
  file F;
  process *p ;  
  p=(process *)malloc(sizeof(process));
  printf("Doonner le nombre des elements des processuses :");
  scanf("%d",&size);
  F=creer_file(size);
  push_fifo(F);
  return 0 ;
};
