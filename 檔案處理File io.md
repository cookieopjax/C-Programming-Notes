# 檔案處理
檔案處理有3步：
* 開啟檔案
* 讀寫檔案
* 關閉檔案

## 1.開啟檔案
```c
FILE *name = fopen("檔案名", "模式");
```

常用的mode
| 讀文字檔案 | 清空後寫文字檔案 | 於文字檔案末端寫入 |
| ---------- | ---------- | ------------------ |
| r          | w          | a                      |

## 2-1.讀檔案
```c
fscanf(檔案指標, 型態 ,欲儲存位置);//跟scanf很像
```

## 2-2.寫檔案
```c
fprintf(檔案指標, 型態, 欲寫到檔案中之資料)//跟printf很像
```

## 3.關閉檔案
```c
fclose(檔案指標);
```

---    
# 實際演練
```
將putin.txt中的數個字串資料讀入，計算其長度，輸出到output.txt
```

putin.txt
```
pig kirto fuck areyoukiddingme
```

解:
```c
#include <stdio.h>
#include <string.h>
int main(){
    FILE *input = fopen("putin.txt","r");//建立讀入用檔案指標
    FILE *output = fopen("output.txt","w");//建立寫入用檔案指標
    char temp[20][20] = {0};
    int countLength[20] = {0};
    int x = 0;

    if(input == NULL || output == NULL){//檢查檔案是否有讀入
        printf("開檔失敗!\n");
        return -1;
    }

    while(fscanf(input,"%s",temp[x])!=EOF)//從input讀入檔案至temp[x]陣列
        x++;

    printf("字串長度->");
    for(int i=0;i<x;i++){
        countLength[i] = strlen(temp[i]);//計算每個字串的長度
        fprintf(output, "%d", countLength[i]);//將countLength[i]寫入至output
        printf("%d ", countLength[i]);//(僅為確認用)在螢幕上印出
    }
    //關閉檔案
    fclose(input);
    fclose(output);
}
```

output.txt
```
3 5 4 15
```
