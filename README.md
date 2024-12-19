#  实验五 数组
## 一、实验目的
1、掌握- -维数组和二维数组的定义、赋值和输入输出的方法。
2、掌握字符数组和字符串函数的使用。
3、掌握与数组有关的算法(特别是排序算法)。
##二、实验准备
1、复习数组的基本知识。
2、复习字符串数组的特点和常用的字符串处理函数。
##三、实验内容
#include <stdio.h>
#include <string.h>

// 1. 选择法对10个整数排序
void selectionSort(int arr[], int n) {
    int i, j, min_idx, temp;
    for (i = 0; i < n - 1; i++) {
        min_idx = i;
        for (j = i + 1; j < n; j++) {
            if (arr[j] < arr[min_idx])
                min_idx = j;
        }
        if (min_idx!= i) {
            temp = arr[i];
            arr[i] = arr[min_idx];
            arr[min_idx] = temp;
        }
    }
}

// 2. 折半查找法查找元素在数组中的位置
int binarySearch(int arr[], int n, int key) {
    int low = 0, high = n - 1, mid;
    while (low <= high) {
        mid = (low + high) / 2;
        if (arr[mid] == key)
            return mid;
        else if (arr[mid] < key)
            low = mid + 1;
        else
            high = mid - 1;
    }
    return -1;
}

// 3. 连接两个字符串
void concatStrings(char str1[], char str2[]) {
    int len1 = strlen(str1);
    int i;
    for (i = 0; str2[i]!= '\0'; i++) {
        str1[len1 + i] = str2[i];
    }
    str1[len1 + i] = '\0';
}

// 4. 查找二维数组鞍点
void findSaddlePoint(int arr[][4], int rows, int cols) {
    int i, j, k, flag;
    for (i = 0; i < rows; i++) {
        int max_col = 0;
        for (j = 1; j < cols; j++) {
            if (arr[i][j] > arr[i][max_col])
                max_col = j;
        }
        flag = 1;
        for (k = 0; k < rows; k++) {
            if (arr[k][max_col] < arr[i][max_col]) {
                flag = 0;
                break;
            }
        }
        if (flag) {
            printf("鞍点为：arr[%d][%d] = %d\n", i, max_col, arr[i][max_col]);
            return;
        }
    }
    printf("该二维数组没有鞍点\n");
}

int main() {
    // 1. 选择法排序测试
    int arr1[10];
    printf("请输入10个整数用于选择法排序：\n");
    for (int i = 0; i < 10; i++) {
        scanf("%d", &arr1[i]);
    }
    selectionSort(arr1, 10);
    printf("排序后的数组为：\n");
    for (int i = 0; i < 10; i++) {
        printf("%d ", arr1[i]);
    }
    printf("\n");

    // 2. 折半查找测试
    int arr2[15] = { 1, 3, 5, 7, 9, 11, 13, 15, 17, 19, 21, 23, 25, 27, 29 };
    int num;
    printf("请输入一个数用于折半查找：\n");
    scanf("%d", &num);
    int result = binarySearch(arr2, 15, num);
    if (result!= -1)
        printf("该数是数组中第 %d 个元素的值\n", result + 1);
    else
        printf("无此数\n");

    // 3. 字符串连接测试
    char str1[50] = "Hello, ";
    char str2[20];
    printf("请输入一个字符串用于连接：\n");
    scanf("%s", str2);
    concatStrings(str1, str2);
    printf("连接后的字符串为：%s\n", str1);

    // 4. 二维数组鞍点查找测试
    int arr3[3][4] = { { 1, 2, 3, 4 },
                       { 5, 6, 7, 8 },
                       { 9, 10, 11, 12 } };
    findSaddlePoint(arr3, 3, 4);

    return 0;
}
问:请分析该代码:
1. 选择法排序
selectionSort 函数实现了选择排序算法。它通过不断找出未排序部分的最小元素，并与当前位置元素交换，来逐步将数组排序。外层循环控制排序轮数，内层循环用于找出每一轮的最小元素位置。
2. 折半查找
binarySearch 函数实现了折半查找算法。它利用数组已排序的特性，通过不断缩小查找区间（每次取中间元素与目标元素比较），来确定目标元素的位置。如果最终未找到，则返回 -1。
3. 字符串连接
concatStrings 函数实现了字符串连接功能。先获取第一个字符串的长度，然后将第二个字符串的字符逐个复制到第一个字符串的末尾，并添加字符串结束符 '\0'。
4. 二维数组鞍点查找
findSaddlePoint 函数先在每一行中找出最大值所在列，然后检查该列上对应元素是否在该列中最小，如果满足则是鞍点。若遍历完整个二维数组都未找到符合条件的元素，则说明没有鞍点。
在 main 函数中，分别对上述四个功能进行了测试，按照要求从用户输入获取相应数据，调用对应函数完成操作，并输出结果。
请注意，实际应用中可根据需求对代码进行进一步优化，比如添加更多的错误处理逻辑等。
