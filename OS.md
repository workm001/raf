```c
#include <stdio.h>

void input(int at[], int bt[], int rt[], int n);
void srtf(int at[], int bt[], int rt[], int ct[], int tat[], int wt[], int n);
void display(int at[], int bt[], int ct[], int tat[], int wt[], int n);

int main() {
    int n;
    printf("Enter number of processes: ");
    scanf("%d", &n);

    int at[100], bt[100], rt[100], ct[100], tat[100], wt[100];

    input(at, bt, rt, n);
    srtf(at, bt, rt, ct, tat, wt, n);
    display(at, bt, ct, tat, wt, n);

    return 0;
}

void input(int at[], int bt[], int rt[], int n) {
    for (int i = 0; i < n; i++) {
        printf("Enter arrival time and burst time for process %d: ", i + 1);
        scanf("%d%d", &at[i], &bt[i]);
        rt[i] = bt[i]; // Initialize remaining time
    }
}

void srtf(int at[], int bt[], int rt[], int ct[], int tat[], int wt[], int n) {
    int completed = 0, time = 0, shortest = -1, min_rt;
    
    while (completed != n) {
        shortest = -1;
        min_rt = 99999;

        for (int i = 0; i < n; i++) {
            if (at[i] <= time && rt[i] > 0 && rt[i] < min_rt) {
                min_rt = rt[i];
                shortest = i;
            }
        }

        if (shortest == -1) {
            time++;
            continue;
        }

        rt[shortest]--;
        time++;

        if (rt[shortest] == 0) {
            completed++;
            ct[shortest] = time;
            tat[shortest] = ct[shortest] - at[shortest];
            wt[shortest] = tat[shortest] - bt[shortest];
        }
    }
}

void display(int at[], int bt[], int ct[], int tat[], int wt[], int n) {
    float total_tat = 0, total_wt = 0;

    printf("\n-------------------------------\n");
    printf("| P# | AT | BT | CT | TAT | WT |\n");
    printf("-------------------------------\n");

    for (int i = 0; i < n; i++) {
        printf("| P%-2d| %-3d| %-3d| %-3d| %-4d| %-3d|\n", i + 1, at[i], bt[i], ct[i], tat[i], wt[i]);
        total_tat += tat[i];
        total_wt += wt[i];
    }

    printf("-------------------------------\n");
    printf("Average Turnaround Time: %.2f\n", total_tat / n);
    printf("Average Waiting Time   : %.2f\n", total_wt / n);
}
```
