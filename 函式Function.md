初學者在學習程式時，都是以寫在main中為主，我們會習慣是int main，並在其中編寫我們要的功能，但事實上main外面也別有一番天地，這就function。

使用函式可使程式碼更簡潔且更容易維護，今天要一步步教大家了解如何實作函式。


首先，先假設我們要寫一個程式:
輸入一個數字，只要此數字是1.2.3，即輸出我程式碼中寫的三行字。
```c
#include<stdio.h>
int main(){
    int input;
    printf("請輸入一個數字:");
    scanf("%d",&input);
    if(input==1){
        printf("嗨!n");
        printf("這裡是餅乾教學區n");
        printf("你好");
    }
    else if(input==2){
        printf("嗨!n");
        printf("這裡是餅乾教學區n");
        printf("你好");
    }
    else if(input==3){
        printf("嗨!n");
        printf("這裡是餅乾教學區n");
        printf("你好");
    }
    else
        printf("這不是123");
    return 0;
}
```
照上述的程式碼寫固然不會有什麼問題，但是仔細觀看會發現，程式碼中重複的部分太多，如果發現有錯字，我需要把三個部份分別改，非常麻煩。 因此，嘗試用函式來寫這個程式看看吧
```c
#include<stdio.h>
void output_hey(){
    printf("嗨!n");
    printf("這裡是餅乾教學區n");
    printf("你好");
}
int main(){
    int input;
    printf("請輸入一個數字:");
    scanf("%d",&input);
    if(input==1){
        output_hey();
    }
    else if(input==2){
        output_hey();
    }
    else if(input==3){
        output_hey();
    }
    else
        printf("這不是123");
    return 0;
}
```
上述兩段程式碼的輸出會完全一樣，而下者更為簡潔及好維護。

---

## 函式的實際使用方式:

事實上，程式中的函式跟數學中的函式是很像的，都是輸入值，然後輸出其對應的值。
![](https://i0.wp.com/1.bp.blogspot.com/-Wp1ZlLOV04E/XhXkm_bnzPI/AAAAAAAAAYk/lfglLErvXKIGIVbnR_YReYzVd0mSXlXKQCLcBGAsYHQ/s1600/1.png?w=640&ssl=1)

而在C語言中，寫函式的規範是:
![](https://i0.wp.com/1.bp.blogspot.com/-Gn6MmZymkcw/XhXlkdJNY5I/AAAAAAAAAYs/RL4MMGFpxPYEZ4paN6SUvuiW5LBJebeKgCLcBGAsYHQ/s1600/2.png?w=640&ssl=1)

接下來來看個簡單範例吧! 嘗試寫個程式，輸入兩數，輸出其中較大的那個，如果兩者相等，輸出兩者相加。
```c
#include<stdio.h>
/*創建一個名為"Calculation"的函式  其輸入的型態為兩個int
  輸出型態為int*/
int Calculation(int a,int b){
    if(a>b)//當a>b時
        return a;//傳回a的值
    else if(b>a)//當b>a時
        return b;//傳回b的值
    else//兩者相等時
        return a+b;//傳回兩者想加的值
}
int main(){
    while(1){
        int data1,data2;
        scanf("%d%d",&data1,&data2);
        printf("最終結果為:%dnn",Calculation(data1,data2));
    }
}
```
```c
//此為實際運作output
1 3
最終結果為:3
20 988
最終結果為:988
50 50
最終結果為:100
94 87
最終結果為:94
```
其中左側的int代表該函式的型態，因此可看到我在輸出時，直接在printf中寫了%d直接輸出

中間則為函式的名稱，可隨意取 後方為欲輸入進去的型態，看你要int.double.char都可以，也可以輸入多種不同的值及型態。

在main中使用函式時，只要寫出函式名稱(輸入的值)即可。

這個程式的a.b純粹是在Calculation函式中使用的，他會在main中偵測輸入的的值(括號中的值)複製一份，再放到函式中去做處理。

輸入輸出一定要有值嗎?我可不可以單純處理或印東西
你當然可以不輸入任何值或不傳出任何值，這篇文章開頭的範例即是如此，只要在函式的開頭寫void即為不傳出任何值，函式最後的括號裡保持空的即為不傳入任何值。

其實在實作function時，可能會慢慢遇到區域變數及全域變數甚至是指標的問題，這我們待日後文章在做說明。
