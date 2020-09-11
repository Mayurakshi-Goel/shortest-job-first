# shortest-job-first
#include<stdio.h>
#include<conio.h>
void main(){
	int p_id[15],bt[15],wt[15],tat[15],temp,n,i,j,t;
	double avg_wt,avg_tat;
	avg_wt=0;
	avg_tat=0;
	printf("Enter the number of processes (max 15): ");
	scanf("%d",&n);
	printf("\n\n");
	for(i=0;i<n;i++){
		p_id[i]=i;
		printf("Enter the burst time of process %d:\t",i);
		scanf("%d",&bt[i]);
	}
	for(i=0;i<n;i++){
		for(j=i+1;j<n;j++){
			if(bt[j]<bt[i]){
				t=bt[i];
				bt[i]=bt[j];
				bt[j]=t;
				
				temp=p_id[i];
				p_id[i]=p_id[j];
				p_id[j]=temp;
			}
		}
	}
	wt[0]=0;
	tat[0]=bt[0];
	for(i=1;i<n;i++){
		wt[i]=wt[i-1]+bt[i-1];
		tat[i]=wt[i]+bt[i];
	}
	for(i=0;i<n;i++){
		avg_wt=avg_wt+wt[i];
		avg_tat=avg_tat+tat[i];
	}
	avg_wt=avg_wt/n;
	avg_tat=avg_tat/n;
	printf("\n\nprocess id\tburst time\twaiting time\tturn around time\n");
	for(i=0;i<n;i++){
		printf("%d\t\t%d\t\t%d\t\t%d\n",p_id[i],bt[i],wt[i],tat[i]);
	}
	printf("\n\nAverage waiting time is: %lf\n",avg_wt);
	printf("Average turn around time is: %lf",avg_tat);
}
