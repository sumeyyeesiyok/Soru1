#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void birlestirmeliSiralama(int dizi[], int boyut);
void secmeliSiralama(int dizi[], int boyut);

int main() {
    int X[500], Y[500];
    int i, n = 500;

    srand(time(NULL));
    printf("Rastgele olusturulan 500 tamsayi:\n");
    for (i = 0; i < n; i++) {
        X[i] = rand() % 1001;
        printf("%d ", X[i]);
    }
    printf("\n");

    clock_t baslangic = clock();
    birlestirmeliSiralama(X, n);
    clock_t bitis = clock();
    double birlestirmeli_sure = (double)(bitis - baslangic) / CLOCKS_PER_SEC;

    printf("\nBirlestirmeli Siralama sonucu:\n");
    for (i = 0; i < n; i++) {
        printf("%d ", X[i]);
    }
    printf("\nBirlestirmeli Siralama Suresi: %f saniye\n", birlestirmeli_sure);

    srand(time(NULL));
    printf("\nRastgele olusturulan 500 tamsayi:\n");
    for (i = 0; i < n; i++) {
        Y[i] = rand() % 1001;
        printf("%d ", Y[i]);
    }
    printf("\n");

    baslangic = clock();
    secmeliSiralama(Y, n);
    bitis = clock();
    double secmeli_sure = (double)(bitis - baslangic) / CLOCKS_PER_SEC;

    printf("\nSecmeli Siralama sonucu:\n");
    for (i = 0; i < n; i++) {
        printf("%d ", Y[i]);
    }
    printf("\nSecmeli Siralama Suresi: %f saniye\n", secmeli_sure);

    return 0;
}

void birlestirmeliSiralama(int dizi[], int boyut) {
    int i, j, gecici;
    for (i = 1; i < boyut; i++) {
        gecici = dizi[i];
        j = i - 1;
        while (j >= 0 && dizi[j] > gecici) {
            dizi[j + 1] = dizi[j];
            j = j - 1;
        }
        dizi[j + 1] = gecici;
    }
}

void secmeliSiralama(int dizi[], int boyut) {
    int i, j, minIndex, gecici;
    for (i = 0; i < boyut - 1; i++) {
        minIndex = i;
        for (j = i + 1; j < boyut; j++) {
            if (dizi[j] < dizi[minIndex]) {
                minIndex = j;
            }
        }
        gecici = dizi[minIndex];
        dizi[minIndex] = dizi[i];
        dizi[i] = gecici;
    }
}
