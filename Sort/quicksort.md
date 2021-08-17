给定一段序列：第一个值作为pivot
目标：找到一个位置，使得pivot左边的数字都比他小，右边的数字都比他大
实现：左右双指针往内走，停止直到左指针>pivot>右指针，交换左右指针的值
```c++
void sort(vector<int> &vec);
void quicksort(vector<int> &vec, int start, int finish);
int partition(vector<int> &vec, int start, int finish);

void sort(vector<int> &vec){
    quicksort(vec, 0, vec.size()-1);
}

int quicksort(vector<int> &vec, int start, int finish) {
    if (start >= finish) return;
    int boundary = partition(vec, start, finish);
    quicksort(vec, start, boundary - 1);
    quicksort(vec, boundary + 1, finish); 
};

int partition (vector<int> &vec, int start, int finish) {
    int pivot = int[start];
    int lh = start + 1;
    int rh = finish;

    while(true) {
        while (lh < rh && vec[rh] >= pivot) rh--;
        while (lh < rh && vec[lh] < pivot) lh++;
        if (lh == rh) break;
        int tmp = vec[lh];
        vec[lh] = vec[rh];
        vec[rh] = tmp;
    }

    // element left of lh: < pivot
    // element right of lh: > pivot
    
    if (vec[lh] >= pivot) return start; //pivot is essentially the smallest, and boundary is the start
    
    vec[start] = vec[lh];
    vec[lh] = pivot;                    //place pivot at the boundary

    return lh;

}
```