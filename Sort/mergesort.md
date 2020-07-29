```c++
void sort(vector<int> &vec){
    int n = vec.size();
    if (n <=1 ) return;;
    vector<int> v1;
    vector<int> v2;

    for (int i = 0; i< n; i++){
        if (i < 2/n) v1.push_back(vec[i]);
        else v2.push_back(vec[i]);
    }

    sort(v1);
    sort(v2);
    vec.clear();
    //v1，v2已经按顺序排好
    //两个已经排序好的vector，merge的复杂度是n
    merge(vec, v1, v2);
}


void merge(vector<int> vec, vector<int> &v1, vector<int> &v2){
    //对比头部。复杂度是O(n)
    int n1 = v1.size();
    int n2 = v2.size();
    int p1 = 0;
    int p2 = 0;

    while (p1 < n1 && p2 < n2>) {
        if (v1[p1] < v2[p2]) vec.push_back(v1[p1++]);
        else                 vec.push_back(v2[p2++]);
    }
    while (p1 < n1) vec.push_back(v1[p1++]);
    while (p2 < n2) vec.push_back(v2[p2++]);
}
