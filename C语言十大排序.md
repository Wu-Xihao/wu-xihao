# 排序算法
### 冒泡排序
+ 冒泡排序重复地走访过要排序的数列，一次比较两个元素，如果它们的顺序错误就把它们交换过来。走访数列的工作是重复地进行直到没有再需要交换，也就是说该数列已经排序完成。这个算法的名字由来是因为越小的元素会经由交换慢慢“浮”到数列的顶端。
1. 比较相邻的元素。如果第一个比第二个大，就交换它们两个；
2. 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对，这样在最后的元素应该会是最大的数；
3. 针对所有的元素重复以上的步骤，除了最后一个；
4. 重复步骤1~3，直到排序完成。
```c
  void BubbleSort(int *arr, int size)  
{  
    int i, j, tmp;  
    for (i = 0; i < size - 1; i++) {  
        for (j = 0; j < size - i - 1; j++) {  
            if (arr[j] > arr[j+1]) {  
                tmp = arr[j];  
                arr[j] = arr[j+1];  
                arr[j+1] = tmp;  
            }  
        }  
    }  
}  
```
### 选择排序
+ 选择排序(Selection-sort)是一种简单直观的排序算法。它的工作原理：首先在未排序序列中找到最小（大）元素，存放到排序序列的起始位置，然后，再从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序序列的末尾。以此类推，直到所有元素均排序完毕。
+ n个记录的直接选择排序可经过n-1趟直接选择排序得到有序结果。
1. 初始状态：无序区为R[1..n]，有序区为空；
2. 第i趟排序(i=1,2,3…n-1)开始时，当前有序区和无序区分别为R[1..i-1]和R(i..n）。该趟排序从当前无序区中-选出关键字最小的记录 R[k]，将它与无序区的第1个记录R交换，使R[1..i]和R[i+1..n)分别变为记录个数增加1个的新有序区和记录个数减少1个的新无序区；
3. n-1趟结束，数组有序化了。
```c
void SelectionSort(int *arr, int size)
{
    int i, j, k, tmp;
    for (i = 0; i < size - 1; i++) {
        k = i;
        for (j = i + 1; j < size; j++) {
            if (arr[j] < arr[k]) {
                k = j;
            }
        }
        tmp = arr[k];
        arr[k] = arr[i];
        arr[i] = tmp;
    }
}
```
### 插入排序
+ 插入排序（Insertion-Sort）的算法描述是一种简单直观的排序算法。它的工作原理是通过构建有序序列，对于未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入。
+ 一般来说，插入排序都采用in-place在数组上实现。
1. 从第一个元素开始，该元素可以认为已经被排序；
2. 取出下一个元素，在已经排序的元素序列中从后向前扫描；
3. 如果该元素（已排序）大于新元素，将该元素移到下一位置；
4. 重复步骤3，直到找到已排序的元素小于或者等于新元素的位置；
5. 将新元素插入到该位置后；
6. 重复步骤2~5。
```c
void InsertionSort(int *arr, int size)    
{    
    int i, j, tmp;    
    for (i = 1; i < size; i++) {    
        if (arr[i] < arr[i-1]) {    
            tmp = arr[i];    
            for (j = i - 1; j >= 0 && arr[j] > tmp; j--) {  
                arr[j+1] = arr[j];    
            }  
            arr[j+1] = tmp;    
        }          
    }    
}    
```
### 希尔排序
+ 希尔排序是简单插入排序的改进版；它与插入排序的不同之处在于，它会优先比较距离较远的元素；希尔排序又叫缩小增量排序。
+ 先将整个待排序的记录序列分割成为若干子序列分别进行直接插入排序
1. 选择一个增量序列t1，t2，…，tk，其中ti>tj，tk=1；
2. 按增量序列个数k，对序列进行k 趟排序；
3. 每趟排序，根据对应的增量ti，将待排序列分割成若干长度为m 的子序列，分别对各子表进行直接插入排序。仅增量因子为1 时，整个序列作为一个表来处理，表长度即为整个序列的长度。
```c
void ShellSort(int *arr, int size)  
{  
    int i, j, tmp, increment;  
    for (increment = size/ 2; increment > 0; increment /= 2) {    
        for (i = increment; i < size; i++) {  
            tmp = arr[i];  
            for (j = i - increment; j >= 0 && tmp < arr[j]; j -= increment) {  
                arr[j + increment] = arr[j];  
            }  
            arr[j + increment] = tmp;
        }  
    }  
}  
```
### 归并排序
+ 归并排序是建立在归并操作上的一种有效的排序算法。该算法是采用分治法（Divide and Conquer）的一个非常典型的应用。将已有序的子序列合并，得到完全有序的序列；即先使每个子序列有序，再使子序列段间有序。若将两个有序表合并成一个有序表，称为2-路归并。 
1. 把长度为n的输入序列分成两个长度为n/2的子序列；
2. 对这两个子序列分别采用归并排序；
3. 将两个排序好的子序列合并成一个最终的排序序列。
```c
#define MAXSIZE 100  

void Merge(int *SR, int *TR, int i, int middle, int rightend) 
{
    int j, k, l;  
    for (k = i, j = middle + 1; i <= middle && j <= rightend; k++) {  
        if (SR[i] < SR[j]) {
            TR[k] = SR[i++];
        } else { 
            TR[k] = SR[j++];
        }  
    }  
    if (i <= middle) {
        for (l = 0; l <= middle - i; l++) {
            TR[k + l] = SR[i + l];
        }  
    }  
    if (j <= rightend) {
        for (l = 0; l <= rightend - j; l++) {
            TR[k + l] = SR[j + l];  
        }
    }  
}  

void MergeSort(int *SR, int *TR1, int s, int t) 
{  
    int middle;  
    int TR2[MAXSIZE + 1];  
    if (s == t) {
        TR1[s] = SR[s]; 
    } else {  
        middle = (s + t) / 2;
        MergeSort(SR, TR2, s, middle);
        MergeSort(SR, TR2, middle + 1, t);
        Merge(TR2, TR1, s, middle, t);
    }  
}  
```
### 快速排序
+ 快速排序的基本思想：通过一趟排序将待排记录分隔成独立的两部分，其中一部分记录的关键字均比另一部分的关键字小，则可分别对这两部分记录继续进行排序，以达到整个序列有序。
+ 快速排序使用分治法来把一个串（list）分为两个子串（sub-lists）。
1. 从数列中挑出一个元素，称为 “基准”（pivot）；
2. 重新排序数列，所有元素比基准值小的摆放在基准前面，所有元素比基准值大的摆在基准的后面（相同的数可以到任一边）。在这个分区退出之后，该基准就处于数列的中间位置。这个称为分区（partition）操作；
3. 递归地（recursive）把小于基准值元素的子数列和大于基准值元素的子数列排序。
```c
void QuickSort(int *arr, int maxlen, int begin, int end)  
{  
    int i, j;  
    if (begin < end) {  
        i = begin + 1;  
        j = end;        
        while (i < j) {  
            if(arr[i] > arr[begin]) {  
                swap(&arr[i], &arr[j]); 
                j--;  
            } else {  
                i++; 
            }  
        }  
        if (arr[i] >= arr[begin]) {  
            i--;  
        }  
        swap(&arr[begin], &arr[i]);      
        QuickSort(arr, maxlen, begin, i);  
        QuickSort(arr, maxlen, j, end);  
    }  
}  
 
void swap(int *a, int *b)    
{  
    int temp;  
    temp = *a;  
    *a = *b;  
    *b = temp;  
}  
```
### 堆排序
+ 堆排序（Heapsort）是指利用堆这种数据结构所设计的一种排序算法。堆积是一个近似完全二叉树的结构，并同时满足堆积的性质：即子结点的键值或索引总是小于（或者大于）它的父节点。
1. 将初始待排序关键字序列(R1,R2….Rn)构建成大顶堆，此堆为初始的无序区；
2. 将堆顶元素R[1]与最后一个元素R[n]交换，此时得到新的无序区(R1,R2,……Rn-1)和新的有序区(Rn),且满足R[1,2…n-1]<=R[n]；
3. 由于交换后新的堆顶R[1]可能违反堆的性质，因此需要对当前无序区(R1,R2,……Rn-1)调整为新堆，然后再次将R[1]与无序区最后一个元素交换，得到新的无序区(R1,R2….Rn-2)和新的有序区(Rn-1,Rn)。不断重复此过程直到有序区的元素个数为n-1，则整个排序过程完成。
```c
void Heapify(int *arr, int m, int size)  
{  
    int i, tmp;  
    tmp = arr[m];  
    for (i = 2 * m; i <= size; i *= 2) {  
        if (i + 1 <= size && arr[i] < arr[i+1]) {  
            i++;  
        }  
        if (arr[i] < tmp) {  
            break;  
        }  
        arr[m] = arr[i];  
        m = i;  
    }  
    arr[m] = tmp;  
}  
  
void BulidHeap(int *arr, int size)
{  
    int i;  
    for (i = n / 2; i > 0; i--) {  
        Heapify(arr, i, size);  
    }  
}  
    
void swap(int *arr, int i, int j)  
{  
    int tmp;  
    tmp = arr[i];  
    arr[i] = arr[j];  
    arr[j] = tmp;  
}  
  
void HeapSort(int *arr, int size)  
{  
    int i;  
    BulidHeap(arr, size);  
    for (i = size; i > 1; i--) {  
        swap(arr, 1, i);
        Heapify(arr, 1, i - 1);
    }  
}  
```
### 计数排序
+ 计数排序不是基于比较的排序算法，其核心在于将输入的数据值转化为键存储在额外开辟的数组空间中。 作为一种线性时间复杂度的排序，计数排序要求输入的数据必须是有确定范围的整数。
1. 找出待排序的数组中最大和最小的元素；
2. 统计数组中每个值为i的元素出现的次数，存入数组C的第i项；
3. 对所有的计数累加（从C中的第一个元素开始，每一项和前一项相加）；
4. 反向填充目标数组：将每个元素i放在新数组的第C(i)项，每放一个元素就将C(i)减去1。
```c
void CountingSort(int *A, int *B, int n, int k)  
{  
    int *C = (int *)malloc(sizeof(int) * (k + 1));  
    int i;  
    for (i = 0; i <= k; i++) {  
        C[i] = 0;  
    }  
    for (i = 0; i < n; i++) {  
        C[A[i]]++;  
    }  
    for (i = 1; i <= k; i++) {  
        C[i] = C[i] + C[i - 1];  
    }  
    for (i = n - 1; i >= 0; i--) {  
        B[C[A[i]] - 1] = A[i];  
        C[A[i]]--;  
    }  
}  
```
### 桶排序
+ 桶排序是计数排序的升级版。它利用了函数的映射关系，高效与否的关键就在于这个映射函数的确定。
+ 桶排序 (Bucket sort)的工作的原理：假设输入数据服从均匀分布，将数据分到有限数量的桶里，每个桶再分别排序（有可能再使用别的排序算法或是以递归方式继续使用桶排序进行排）。
1. 设置一个定量的数组当作空桶；
2. 遍历输入数据，并且把数据一个一个放到对应的桶里去；
3. 对每个不是空的桶进行排序；
4. 从不是空的桶里把排好序的数据拼接起来。 
```c
void bucketSort(int *arr, int size, int max)
{
    int i,j;
    int buckets[max];
    memset(buckets, 0, max * sizeof(int));
    for (i = 0; i < size; i++) {
        buckets[arr[i]]++; 
    }
    for (i = 0, j = 0; i < max; i++) {
        while((buckets[i]--) >0)
            arr[j++] = i;
    }
}
```
### 基数排序
+ 基数排序是按照低位先排序，然后收集；再按照高位排序，然后再收集；依次类推，直到最高位。有时候有些属性是有优先级顺序的，先按低优先级排序，再按高优先级排序。最后的次序就是高优先级高的在前，高优先级相同的低优先级高的在前。
1.取得数组中的最大数，并取得位数；
2. arr为原始数组，从最低位开始取每个位组成radix数组；
3. 对radix进行计数排序（利用计数排序适用于小范围数的特点）； 
```c
int get_index(int num, int dec, int order)
{
    int i, j, n;
    int index;
    int div;
    for (i = dec; i > order; i--) {
        n = 1;
        for (j = 0; j < dec - 1; j++)
            n *= 10;
        div = num / n;
        num -= div * n;
        dec--;
    }
    n = 1;
    for (i = 0; i < order - 1; i++)
        n *= 10;
    index = num / n;
    return index;
}
 
void RadixSort(int *arr, int len, int dec, int order)
{
    int i, j;
    int index; 
    int tmp[len]; 
    int num[10];
    memset(num, 0, 10 * sizeof(int)); 
    memset(tmp, 0, len * sizeof(int));
 
    if (dec < order) {
        return;
    }
    for (i = 0; i < len; i++) {
        index = get_index(arr[i], dec, order);
        num[index]++; 
    }
 
    for (i = 1; i < 10; i++) {
        num[i] += num[i-1];
    }
    for (i = len - 1; i >= 0; i--) {
        index = get_index(arr[i], dec, order); 
        j = --num[index]; 
        tmp[j] = arr[i]; 
    }
 
    for (i = 0; i < len; i++) {
        arr[i] = tmp[i]; 
    }
    RadixSort(arr, len, dec, order+1);
}
```




