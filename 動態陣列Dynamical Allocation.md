```
指標陣列=儲存指標型態的陣列
雙重指標=指標的指標
```
```c
int **a;//建立雙重指標
```
...| a | *a | **a 
--------------|:-----:|-----:| ----
值    | 5|  1460 |   1200 
位址  | 1460 | 1200 | 100
... |相當於”行” | 相當於”列” 

設**a存著3個*a，相當於有3列
設*a存著4個a，相當於有4行

－－－－

## 如何建立動態空間?

C語言中，有幾個函式可以動態配置空間，其中malloc最常使用
```c
void *malloc(size_t size) 
配置size大小的空間儲存陣列

配置一個int空間(單一個變數or長度為1的陣列)
int *ptr=malloc(sizeof(int))

配置五個int空間(長度為5的陣列)
int *ptr=malloc(5*sizeof(int))

其他
void *calloc(size_t nitems, size_t size)
類似malloc配置空間，但都會被初始化為0
前面放要分配幾個，後面放sizeof(型態)，不用像malloc一樣用*的

void *realloc(void *ptr, size_t size)
改變已配置的記憶體空間為新的size

void free(void *ptr)
釋放動態記憶體空間
```
範例
分配一個3*2的int陣列空間，並將其每個元素設為8
```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
int main(){
    int **a;
    a=malloc(3*sizeof(int *));//分配3列,使用sizeof(int *)
    for(int i=0;i<3;i++)//針對每1列，個別開出2個int空間，即2行,使用sizeof(int)
        a[i]=malloc(2*sizeof(int));
    printf("完成分配");

    for(int i=0;i<3;i++){
        for(int j=0;j<2;j++){
            a[i][j]=8;//將每個位置設為8
        }
    }
    printf("\n輸出每個元素:\n");
    for(int i=0;i<3;i++){
        for(int j=0;j<2;j++){
            printf("%d ",a[i][j]);
        }
        printf("\n");
    }
    for(int i=0;i<3;i++)//釋放列(第二維)
        free(a[i]);
    free(a);//釋放行(第一維)
}
```
非矩形動態陣列
分配三列空間，分別存放a,aa,aaa，配置剛好的記憶體空間
```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
int main(){
    char **a,k=2;
    a=malloc(3*sizeof(char *));//分配3列
    for(int i=0;i<3;i++){//a[0]分配兩格(保留\0空間),a[1]分配三格，以此類推
        a[i]=calloc(k,sizeof(char));
        k++;
    }
    printf("完成分配");
    strcpy(a[0],"a");
    strcpy(a[1],"aa");
    strcpy(a[2],"aaa");

    printf("\n輸出每個元素:\n");
    for(int i=0;i<3;i++)
        printf("%s\n",a[i]);

    for(int i=0;i<3;i++)//釋放列(第二維)
        free(a[i]);
    free(a);//釋放行(第一維)
}
```
