
struct為可同時儲存多種複合資料的類型，這篇文章會詳細介紹struct基本使用方法、struct陣列、 struct指標 、struct指標陣列等內容。

# 基本常用結構運用
在main外定義名為「Student」的結構
```c
struct Student{ //tag
    //資料型態 變數名稱
    char name[10];
    int score;
};
```
在main中宣告名為cookie的變數，其型態為Student結構
```c
struct Student cookie;//這行跟在上段程式碼;前亦可
```
取得其中變數
```
結構變數名.成員名
```
簡單常用範例
```c
#include <stdio.h>
struct Student {
    //資料型態 變數名稱
    char name[10];
    int score;
};
int main(){
    struct Student cookie={"cookie",87};
    printf("%s,%d\n",cookie.name,cookie.score);
}
```
---

# Struct進階解析

其實結構可以沒有tag(結構名稱)，即匿名結構變數，它無法被其他變數指派或指派值給其他變數，亦無法當作參數或回傳值 。
在結構裡面放結構可以用到
```c
#include <stdio.h>
struct human{
    char name[10];
    int age;
    struct {//匿名結構變數
        float height;
        float weight;
    }More;
};
int main(){
    struct human my_neighbor;
    my_neighbor.age = 15;
    my_neighbor.More.height = 138.5;
    printf("%d , %f\n",my_neighbor.age,my_neighbor.More.height);
}
```
----

## typedef
typedef可以重新定義「宣告的行為」有效優化程式碼可讀性。

使用格式
```
typedef typedeclaration; //typedef 類型宣告
```
使用範例
```c
typedef unsigned long long ULL;//定義ULL
ULL a;//利用ULL宣告變數
```

結構typedef使用範例
```c
#include <stdio.h>
typedef struct student{
    char name[10];
    int score;
} STUDENT;//將struct student 取名為 Student

int main(){
    STUDENT cookie;
    cookie.score=87;
    printf("%d\n",cookie.score);
}
```
上述兩個區段可以這樣看

![](https://upload.cc/i1/2020/04/22/pLDbhI.png)


注意 此動作是將struct student 取名為 Student，相當於上方的把unsigned long long 取名為 ULL，因此匿名空間可以typedef，為匿名取一個新名，這個struct即可自由使用。
```c
#include <stdio.h>
typedef struct{//沒有tag
    char name[10];
    int score;
} STUDENT;//將匿名struct 取名為 Student

int main(){
    STUDENT cookie;
    cookie.score=87;
    printf("%d\n",cookie.score);//可正常操作
}
```
*若在struct中就要使用該struct，乖乖取結構名稱，不要用這招

----

## 結構指標
結構本身是Call by Value的，像一般變數而非陣列，將a結構指定給b結構，實際上是複製a的值至b。

結構指標的使用跟一般指標的使用幾乎完全相同
```c
#include <stdio.h>
typedef struct{
    char name[10];
    int score;
} STUDENT;//將匿名struct 取名為 Student

int main(){
    STUDENT cookie={"cookie",87};
    STUDENT *cooker = &cookie;//建立cooker結構指標
```
結構指標的特別處是在取值的方式，接續上方的程式碼，若要取得結構中的姓名，有下列兩者寫法:
```
(*cooker).name//要用括號包起來
cooker->name
```
