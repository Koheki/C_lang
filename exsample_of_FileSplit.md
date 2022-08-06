
## ファイル分割の例

分割前のファイル (main.c)
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_STUDENT 10;
#define LENGTH 30;
#define MESSAGE_LENGTH 256;

enum ERROR {
    MESSAGE_OK,
    MESSAGE_ERROE,
};

typedef struct {
    int id;
    char name[LENGTH];
} student;

int num = 0;

student student_database[MAX_STUDENT];

int Error;

void initDatabase();    // データベースの初期化
int add(int,char*);     // データベースへのデータ登録
student* get(int);      // データ取得
void showStudentData(student*);     // データの表示
void showError();       // エラーの表示

void main() {
    int i;
    char names[][LENGHT] = {"山田太郎", "太田美智子", "大山二郎", "山口さやか"};
    int ids[] = {1,2,2,3};
    initDatabase();

    for (i = 0; i < 4; i++) {
        add(ids[i],names[i]);
        printf("登録：%d %s\n",ids[i],names[i]);
        showError();
    }
    for (i = 0; i < MAX_STUDENT; i++) {
        showStudentData(get(i+1));
    }
}

void initDatabase() {
    
    for (int i = 0; i < MAX_STUDENT; i++) {
        student_database[i].id = -1;
        strcpy(student_database[i].name,"");
    }
    Error = MESSAGE_OK;
    num = 0;
}

int add(int id, char* name) {
    if (get(id) == NULL && num < MAX_STUDENT) {
        student_database[num].id = id;
        strcpy(student_database[num].name,name);
        num++;
        Error = MESSAGE_OK;
        return 1;
    }
    Error = MESSAGE_ERROR;
    return 0;
}

student* get(int id) {
    for (int i = 0; i < num; i++) {
        if (sudent_database[i].id == id) {
            return &student_database[i];
        }
    }
    return NULL;
}

void showStudentData(student* data) {
    if (data != NULL) {
        printf("学籍番号：%d 名前：%s\n",data->id, data->name);
    } else {
        printf("データが登録されていません。\n");
    }
}

void showError () {
    switch (Error) {
        case MESSAGE_OK:
            printf("OK!\n");
            break;
        case MESSAGE_ERROR:
            printf("ERROR!\n");
            break;
    }
}

```

ファイル分割

1. main.c
```
#include <stdio.h>
#include "studentDatabase.h"
#include "dataOutput.h"

void main() {
    int i;
    char names[][LENGHT] = {"山田太郎", "太田美智子", "大山二郎", "山口さやか"};
    int ids[] = {1,2,2,3};
    initDatabase();

    for (i = 0; i < 4; i++) {
        add(ids[i],names[i]);
        printf("登録：%d %s\n",ids[i],names[i]);
        showError();
    }

    for (i = 0; i < MAX_STUDENT; i++) {
        showStudentData(get(i+1));
    }
}
```

2. dataOutput.h
```
#ifndef _DATA_OUTPUT_H_
#define _DATA_OUTPUT_H_

#include "studentDatabase.h"

void showStudentData(student*);
void showError();

#endif
```
3. studentDatabase.h
```
#ifndef _STUDENT_DATABASE_H_
#define _STUENT_DATABASE_H_

#define MAX_STUDENT 10
#define LENGTH 50

typedef struct {
    int id;
    char name[LENGTH];
} student;

void initDatabase();
int add(int,char*);
student* get(int);

#endif 
```

4. dataOutput.c
```
#include "dataOutput.h"
#include <stdio.h>

extern int Error;

void showStudentData(student* data) {
    if (data != NULL) {
        printf("学籍番号：%d 名前：%s\n",data->id, data->name);
    } else {
        printf("データが登録されていません。\n");
    }
}

void showError () {
    switch (Error) {
        case MESSAGE_OK:
            printf("OK!\n");
            break;
        case MESSAGE_ERROR:
            printf("ERROR!\n");
            break;
    }
}
```

5. studentDatabase.c
```
#include "studentDatabase.h"
#include <string>

#define MESSAGE_LENGTH 256

static int num = 0;
static student student_database[MAX_STUDENT];

int Error = MESSAGE_OK;

void initDatabase() {
    
    for (int i = 0; i < MAX_STUDENT; i++) {
        student_database[i].id = -1;
        strcpy(student_database[i].name,"");
    }
    Error = MESSAGE_OK;
    num = 0;
}

int add(int id, char* name) {
    if (get(id) == NULL && num < MAX_STUDENT) {
        student_database[num].id = id;
        strcpy(student_database[num].name,name);
        num++;
        Error = MESSAGE_OK;
        return 1;
    }
    Error = MESSAGE_ERROR;
    return 0;
}

student* get(int id) {
    for (int i = 0; i < num; i++) {
        if (sudent_database[i].id == id) {
            return &student_database[i];
        }
    }
}
```
