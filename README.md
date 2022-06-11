# CPU-Scheduling-FCFS
#include<stdio.h> #include<stdlib.h> struct s {

int p,at,bt,ct,tat,wt; }; float* fcfs(struct s* s,int n){

int i,j,temp;

for(i=0;i<n;i++){

for(j=0;j<n-i-1;j++)

{

if(s[j].at > s[j+1].at){

temp = s[j].at;

s[j].at = s[j+1].at;

s[j+1].at = temp;

temp = s[j].bt;

s[j].bt = s[j+1].bt;

s[j+1].bt = temp;

temp = s[j].p;

s[j].p = s[j+1].p;

s[j+1].p = temp;

}

}

int sum = 0;

for(i=0;i<n;i++) { sum+=s[i].bt;

s[i].ct = sum;

s[i].tat = s[i].ct - s[i].at;

s[i].wt = s[i].tat - s[i].bt;

}

int tot1=0,tot2=0;

float* avg =(float*)malloc(sizeof(float));

for(i=0;i<n;i++) {

tot1 += s[i].wt;

tot2 +=s[i].tat; }

avg[0] = tot1 / n;

avg[1] = tot2 / n;

return avg;

} int main() {

int n,i; printf("Enter the number of procedure: "); scanf("%d",&n);

struct s* s=(struct s*)malloc(n*sizeof(struct s));

for(i=0;i<n;i++){

s[i].p = i+1;

printf("Enter the arrival_time and burst_time of %d: ",i+1); scanf("%d %d",&s[i].at,&s[i].bt);

} float* avg_wt = fcfs(s,n); printf("P\tAT\tBT\tCT\tTAT\tWT\n"); for(i=0;i<n;i++){ printf("%d\t%d\t%d\t%d\t%d\t%d\t\n",s[i].p,s[i].at,s[i].bt,s[i].ct,s[i].tat,s[i].wt); } printf("Ganttchart:\n"); for(i=0;i<n;i++){ printf("%d | ",s[i].p); } printf("\nAverage Wait Time = %.2f\nAverage Turn Around Time = %.2f\n",avg_wt[0],avg_wt[1]);
 }
