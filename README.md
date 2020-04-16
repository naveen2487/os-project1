# os-project1

#include<stdio.h>

struct process
{
    char name;
    int AT,BT,WT,TAT,RT,CT;
}Q1[10],Q2[10],Q3[10];

int n;
void sortByArrival()
{
struct process temp;
int i,j;
for(i=0;i<n;i++)
    {
        for(j=i+1;j<n;j++)
            {
                if(Q1[i].AT>Q1[j].AT)
                    {
                          temp=Q1[i];
                          Q1[i]=Q1[j];
                          Q1[j]=temp;
                    }
            }
    }
}

int main()
{
     int i,j,k=0,r=0,time=0,tq1=5,tq2=8,flag1=0;
     char c;
     printf("Enter the number of processes=");
     scanf("%d",&n);
     for(i=0,c='A';i<n;i++,c++)
     {
         Q1[i].name=c;
         printf("\nEnter the arrival time and burst time of the process repectively %c: ",Q1[i].name);
         scanf("%d%d",&Q1[i].AT,&Q1[i].BT);
         Q1[i].RT=Q1[i].BT; /*save the burst time in the remaining time for each process*/

    }
sortByArrival();
time=Q1[0].AT;
printf("Process_in_the_first_queue_following_the_Round-Robin_process_with_the_time-quantum=5seconds");
printf("\nProcess\tResponse Time\tWaiting Time\tTurn Around TimeAT\t\t");
for(i=0;i<n;i++)
{

  if(Q1[i].RT<=tq1)
  {

       time+=Q1[i].RT;
       Q1[i].RT=0;
       Q1[i].WT=time-Q1[i].AT-Q1[i].BT; /*amount of the time the  process has been waiting in the first queue*/
       Q1[i].TAT=time-Q1[i].AT; /*the amount of time taken to execute the process*/
       printf("\n%c\t\t%d\t\t%d\t\t%d",Q1[i].name,Q1[i].BT,Q1[i].WT,Q1[i].TAT);

  }
  else /*process will move to the second queue with time quantum=8seconds*/
  {
      Q2[k].WT=time;
      time+=tq1;
      Q1[i].RT-=tq1;
      Q2[k].BT=Q1[i].RT;
      Q2[k].RT=Q2[k].BT;
      Q2[k].name=Q1[i].name;
      k=k+1;
      flag1=1;
   }
}
if(flag1==1)
 {printf("\nProcess_in_the_second_queue_following_Round-Robin_with_time-quantum=8seconds");
  printf("\nProcess\tResponse Time\tWaiting Time\tTurn Around Time\t\t");
}for(i=0;i<k;i++)
   {
    if(Q2[i].RT<=tq2)
     {
       time+=Q2[i].RT;
       Q2[i].RT=0;
       Q2[i].WT=time-tq1-Q2[i].BT;/*amount of time the process has been waiting in the ready queue*/
       Q2[i].TAT=time-Q2[i].AT;/*amount of time required to execute the process*/
       printf("\n%c\t\t%d\t\t%d\t\t%d",Q2[i].name,Q2[i].BT,Q2[i].WT,Q2[i].TAT);

    }
    else/*process moves to queue 3 with FCFS*/
    {
      Q3[r].AT=time;
      time+=tq2;
      Q2[i].RT-=tq2;
      Q3[r].BT=Q2[i].RT;
      Q3[r].RT=Q3[r].BT;
      Q3[r].name=Q2[i].name;
      r=r+1;
      flag1=2;
    }
  }

{if(flag1==2)
printf("\nProcess_in_the_third_queue_following_First-Come-First-Serve ");
printf("\nProcess\tResponse Time\tWaiting Time\tTurn Around Time\t\t");
}
for(i=0;i<r;i++)
{
    if(i==0)
            Q3[i].CT=Q3[i].BT+time-tq1-tq2;
        else
            Q3[i].CT=Q3[i-1].CT+Q3[i].BT;

}

for(i=0;i<r;i++)
    {
        Q3[i].TAT=Q3[i].CT;
        Q3[i].WT=Q3[i].TAT-Q3[i].BT;
        printf("\n%c\t\t%d\t\t%d\t\t%d\t\t",Q3[i].name,Q3[i].BT,Q3[i].WT,Q3[i].TAT);

    }

}
