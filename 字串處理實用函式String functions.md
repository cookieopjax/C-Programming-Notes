## 陣列比對
可直接比對兩陣列是否相同

```c
#include <string.h>
strcmp()  -  strcmp( 被比較字串, 被比較字串 ) //若相同回傳整數值0，不同依據大小回傳正號或負號
```
```c
#include<stdio.h>
#include<string.h>
int main(){
    char input[10];
    while(1){
        scanf("%s",input);
        if(strcmp(input,"cookie")==0)
            printf("你輸入的是cookie\n");
        else
            printf("你輸入的不是cookie\n");
    }
}
```

## 陣列轉數字
將char字串中的數值轉型成各種型態的數字
```c
#include <stdlib.h>
atoi()  -  atoi(字串) //str to int <-最常用
atol()  -  atol(字串) //str to long int
atof()  -  atof(字串) //str to double
strtoul() - strtoul(字串) //str to unsigned long int
```
```c
#include<stdio.h>
#include<stdlib.h>
int main(){
    char input[5]={'1','2','3','4','5'};
    int output;
    output=atoi(input);
    printf("%d",output);
}
```
## 數字轉陣列
將各種型態的數字轉型到char字串中
```c
#include <stdio.h>
sprintf() - sprintf(欲輸出字串,"來源型態指定詞",來源數字)
#include<stdio.h>
int main() {
    char output[10];
    int num=879487;
    sprintf(output,"%d",num);
    printf("此陣列為:%s",output);
}
```

## 陣列清空或強制換成統一字符
此方法可歸零字串，或將內存空間全部設置為某個字符
```c
#include <string.h>
memset() - memset(輸入字串,0,sizeof(輸入字串)//清空字串
memset() - memset(輸入字串,欲設定字符,記憶體區段大小)
//記憶體區段的單位為Byte，且目標值介於0~255(含)之間
```
```c
#include<stdio.h>
#include<string.h>
int main() {
    char a[3]={'1','2','3'};
    memset(a, 0, sizeof(a));
    printf("%c",a[0]);
}
```

## 字串輸入的幾種辦法
對於初學者來說直覺都會直接用scanf，但其問題在碰到空格就會停止，在此提供幾個解法
### 1. 最推薦的fgets
```c
#include <stdio.h>
fgets() - fgets(字串名稱,陣列長度,stdin)
fgets函數會讀取換行符 ，字串中會包含換行，輸出時要注意，此範例程式碼的輸出就沒換行，因為字串裡就有了
#include<stdio.h>
int main() {
    char line[100];
    while(fgets(line,100,stdin)!=NULL){
        printf("%s",line);
    }
    return 0;
}
```
```
/*輸出
test tse
test tse
ok gooed
ok gooed
^Z＊／
```

### 2. gets
```c
#include <stdio.h>
gets() - gets(字串名稱)
有緩衝區溢位之問題，較不建議使用，另外字串中不會包括換行符號
```
```c
#include<stdio.h>
int main() {
    char line[100];
    while(gets(line)!=NULL){
        printf("%s\n",line);
    }
    return 0;
}
```
### 3.邪門歪道scanf法
```c
#include <stdio.h>
scanf() - scanf("%[^\n]",字串名稱);
讓輸入遇到換行才停止，參考資料
此寫法不會吃掉換行，因此若要寫成迴圈要加getchar()吃掉換行符號
```
```c
#include <stdio.h>
#include <stdlib.h>
int main() {
    char line[100];
    while(scanf("%[^\n]",line)!=EOF){
        getchar();
        printf("%s\n",line);
    }
    return 0;
}
```
