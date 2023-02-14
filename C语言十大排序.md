# �����㷨
### ð������
+ ð�������ظ����߷ù�Ҫ��������У�һ�αȽ�����Ԫ�أ�������ǵ�˳�����Ͱ����ǽ����������߷����еĹ������ظ��ؽ���ֱ��û������Ҫ������Ҳ����˵�������Ѿ�������ɡ�����㷨��������������ΪԽС��Ԫ�ػᾭ�ɽ������������������еĶ��ˡ�
1. �Ƚ����ڵ�Ԫ�ء������һ���ȵڶ����󣬾ͽ�������������
2. ��ÿһ������Ԫ����ͬ���Ĺ������ӿ�ʼ��һ�Ե���β�����һ�ԣ�����������Ԫ��Ӧ�û�����������
3. ������е�Ԫ���ظ����ϵĲ��裬�������һ����
4. �ظ�����1~3��ֱ��������ɡ�
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
### ѡ������
+ ѡ������(Selection-sort)��һ�ּ�ֱ�۵������㷨�����Ĺ���ԭ��������δ�����������ҵ���С����Ԫ�أ���ŵ��������е���ʼλ�ã�Ȼ���ٴ�ʣ��δ����Ԫ���м���Ѱ����С����Ԫ�أ�Ȼ��ŵ����������е�ĩβ���Դ����ƣ�ֱ������Ԫ�ؾ�������ϡ�
+ n����¼��ֱ��ѡ������ɾ���n-1��ֱ��ѡ������õ���������
1. ��ʼ״̬��������ΪR[1..n]��������Ϊ�գ�
2. ��i������(i=1,2,3��n-1)��ʼʱ����ǰ���������������ֱ�ΪR[1..i-1]��R(i..n������������ӵ�ǰ��������-ѡ���ؼ�����С�ļ�¼ R[k]���������������ĵ�1����¼R������ʹR[1..i]��R[i+1..n)�ֱ��Ϊ��¼��������1�������������ͼ�¼��������1��������������
3. n-1�˽��������������ˡ�
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
### ��������
+ ��������Insertion-Sort�����㷨������һ�ּ�ֱ�۵������㷨�����Ĺ���ԭ����ͨ�������������У�����δ�������ݣ��������������дӺ���ǰɨ�裬�ҵ���Ӧλ�ò����롣
+ һ����˵���������򶼲���in-place��������ʵ�֡�
1. �ӵ�һ��Ԫ�ؿ�ʼ����Ԫ�ؿ�����Ϊ�Ѿ�������
2. ȡ����һ��Ԫ�أ����Ѿ������Ԫ�������дӺ���ǰɨ�裻
3. �����Ԫ�أ������򣩴�����Ԫ�أ�����Ԫ���Ƶ���һλ�ã�
4. �ظ�����3��ֱ���ҵ��������Ԫ��С�ڻ��ߵ�����Ԫ�ص�λ�ã�
5. ����Ԫ�ز��뵽��λ�ú�
6. �ظ�����2~5��
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
### ϣ������
+ ϣ�������Ǽ򵥲�������ĸĽ��棻�����������Ĳ�֮ͬ�����ڣ��������ȱȽϾ����Զ��Ԫ�أ�ϣ�������ֽ���С��������
+ �Ƚ�����������ļ�¼���зָ��Ϊ���������зֱ����ֱ�Ӳ�������
1. ѡ��һ����������t1��t2������tk������ti>tj��tk=1��
2. ���������и���k�������н���k ������
3. ÿ�����򣬸��ݶ�Ӧ������ti�����������зָ�����ɳ���Ϊm �������У��ֱ�Ը��ӱ����ֱ�Ӳ������򡣽���������Ϊ1 ʱ������������Ϊһ�������������ȼ�Ϊ�������еĳ��ȡ�
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
### �鲢����
+ �鲢�����ǽ����ڹ鲢�����ϵ�һ����Ч�������㷨�����㷨�ǲ��÷��η���Divide and Conquer����һ���ǳ����͵�Ӧ�á���������������кϲ����õ���ȫ��������У�����ʹÿ��������������ʹ�����жμ������������������ϲ���һ���������Ϊ2-·�鲢�� 
1. �ѳ���Ϊn���������зֳ���������Ϊn/2�������У�
2. �������������зֱ���ù鲢����
3. ����������õ������кϲ���һ�����յ��������С�
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
### ��������
+ ��������Ļ���˼�룺ͨ��һ�����򽫴��ż�¼�ָ��ɶ����������֣�����һ���ּ�¼�Ĺؼ��־�����һ���ֵĹؼ���С����ɷֱ���������ּ�¼�������������Դﵽ������������
+ ��������ʹ�÷��η�����һ������list����Ϊ�����Ӵ���sub-lists����
1. ������������һ��Ԫ�أ���Ϊ ����׼����pivot����
2. �����������У�����Ԫ�رȻ�׼ֵС�İڷ��ڻ�׼ǰ�棬����Ԫ�رȻ�׼ֵ��İ��ڻ�׼�ĺ��棨��ͬ�������Ե���һ�ߣ�������������˳�֮�󣬸û�׼�ʹ������е��м�λ�á������Ϊ������partition��������
3. �ݹ�أ�recursive����С�ڻ�׼ֵԪ�ص������кʹ��ڻ�׼ֵԪ�ص�����������
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
### ������
+ ������Heapsort����ָ���ö��������ݽṹ����Ƶ�һ�������㷨���ѻ���һ��������ȫ�������Ľṹ����ͬʱ����ѻ������ʣ����ӽ��ļ�ֵ����������С�ڣ����ߴ��ڣ����ĸ��ڵ㡣
1. ����ʼ������ؼ�������(R1,R2��.Rn)�����ɴ󶥶ѣ��˶�Ϊ��ʼ����������
2. ���Ѷ�Ԫ��R[1]�����һ��Ԫ��R[n]��������ʱ�õ��µ�������(R1,R2,����Rn-1)���µ�������(Rn),������R[1,2��n-1]<=R[n]��
3. ���ڽ������µĶѶ�R[1]����Υ���ѵ����ʣ������Ҫ�Ե�ǰ������(R1,R2,����Rn-1)����Ϊ�¶ѣ�Ȼ���ٴν�R[1]�����������һ��Ԫ�ؽ������õ��µ�������(R1,R2��.Rn-2)���µ�������(Rn-1,Rn)�������ظ��˹���ֱ����������Ԫ�ظ���Ϊn-1�����������������ɡ�
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
### ��������
+ ���������ǻ��ڱȽϵ������㷨����������ڽ����������ֵת��Ϊ���洢�ڶ��⿪�ٵ�����ռ��С� ��Ϊһ������ʱ�临�Ӷȵ����򣬼�������Ҫ����������ݱ�������ȷ����Χ��������
1. �ҳ��������������������С��Ԫ�أ�
2. ͳ��������ÿ��ֵΪi��Ԫ�س��ֵĴ�������������C�ĵ�i�
3. �����еļ����ۼӣ���C�еĵ�һ��Ԫ�ؿ�ʼ��ÿһ���ǰһ����ӣ���
4. �������Ŀ�����飺��ÿ��Ԫ��i����������ĵ�C(i)�ÿ��һ��Ԫ�ؾͽ�C(i)��ȥ1��
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
### Ͱ����
+ Ͱ�����Ǽ�������������档�������˺�����ӳ���ϵ����Ч���Ĺؼ����������ӳ�亯����ȷ����
+ Ͱ���� (Bucket sort)�Ĺ�����ԭ�������������ݷ��Ӿ��ȷֲ��������ݷֵ�����������Ͱ�ÿ��Ͱ�ٷֱ������п�����ʹ�ñ�������㷨�����Եݹ鷽ʽ����ʹ��Ͱ��������ţ���
1. ����һ�����������鵱����Ͱ��
2. �����������ݣ����Ұ�����һ��һ���ŵ���Ӧ��Ͱ��ȥ��
3. ��ÿ�����ǿյ�Ͱ��������
4. �Ӳ��ǿյ�Ͱ����ź��������ƴ�������� 
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
### ��������
+ ���������ǰ��յ�λ������Ȼ���ռ����ٰ��ո�λ����Ȼ�����ռ����������ƣ�ֱ�����λ����ʱ����Щ�����������ȼ�˳��ģ��Ȱ������ȼ������ٰ������ȼ��������Ĵ�����Ǹ����ȼ��ߵ���ǰ�������ȼ���ͬ�ĵ����ȼ��ߵ���ǰ��
1.ȡ�������е����������ȡ��λ����
2. arrΪԭʼ���飬�����λ��ʼȡÿ��λ���radix���飻
3. ��radix���м����������ü�������������С��Χ�����ص㣩�� 
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




