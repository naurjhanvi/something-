#include <stdio.h>

int main() {

    float weight[50], profit[50], ratio[50];
    float Totalvalue = 0, temp, capacity;
    int n, i, j;

    printf("Enter the number of items: ");
    scanf("%d", &n);

    for (i = 0; i < n; i++) {
        printf("Enter Weight and Profit for item[%d]:\n", i);
        scanf("%f %f", &weight[i], &profit[i]);
    }

    printf("Enter the capacity of knapsack:\n");
    scanf("%f", &capacity);

    for (i = 0; i < n; i++)
        ratio[i] = profit[i] / weight[i];

    for (i = 0; i < n; i++) {
        for (j = i + 1; j < n; j++) {
            if (ratio[i] < ratio[j]) {

                temp = ratio[i];
                ratio[i] = ratio[j];
                ratio[j] = temp;

                temp = weight[i];
                weight[i] = weight[j];
                weight[j] = temp;

                temp = profit[i];
                profit[i] = profit[j];
                profit[j] = temp;
            }
        }
    }

    printf("\nKnapsack problem using Greedy Algorithm:\n");

    for (i = 0; i < n; i++) {
        if (weight[i] > capacity)
            break;
        else {
            Totalvalue += profit[i];
            capacity -= weight[i];
        }
    }

    if (i < n)
        Totalvalue += ratio[i] * capacity;

    printf("\nThe maximum value is: %f\n", Totalvalue);

    return 0;
}
