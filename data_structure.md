# Basic Data Structure

## Array
```c++
//initialization
int myints[] = {1,2,3};
int myints[3] = {1,2,3};
int myints[10][10];

array<int,3> = {1,2,3};//这样是调用了class，才可以访问成员函数
//operation
arr.swap(arr1) //linear time in size
arr.empty()
arr.size();arr.max_size()
```

## Vector
```c++
// initialization
vector(int num, value)；
vector<vector<bool>> mark (Nrow, vector<bool>(Ncol, false));
int myints[] ={1,2,3}; vector<int>v(myints, myints+3);
vector<pair<int,int>> vec(map.begin(), map.end())

// operation
vec.push_back(); vec.pop_back();
vec.size(); vec.capacity();vec.clear()
iterator insert (iterator pos, const value_type& val); //insert before
void insert (pos,n,val)
```

## Map
```c++
// initialization
map<key_type,value_type> mymap;
//operation
map::iterator it = map.find(key_value); if(it!=map.end()) cout<<it->second<<endl;
map.erase(key) // or erase iterator
map[key] = value
map[key]++;    //useful to count! 如果key不存在，第一次call key对应的value会直接变成1
map.insert(make_pair<int, string>(222, "Songhao"))
map.count(key_value) //will only return 0 or 1

//iteration
for (iter = map.begin(); iter != map.end(); ++iter){iter -> first;}
```
## Set
set, unordered_set, multiset
```c++
//initialization
std::unordered_multiset<st::string> first;
//operation
set.count(key);
set.insert(arr.begin(),arr.end())
set.erase(iter);set.erase(key)
set.find(key) == set.end()

for (int x: myset) std::cout << " " << x; 
for (const int& x: myset) std::cout << " " << x; 
```
## Dequeue
```c++
std::deque<int> dq (num,val);

dq.front();dq.back();
dq.pop_back();dq.push_back();dq.push_front();dq.pop_front();
```
## List
```c++
list.pop_back();list.push_back();list.push_front();list.pop_front(); 
iterator insert (iterator position, const value_type& val);
void insert (iterator position, InputIterator first, InputIterator last);

list.erase(iterator position) //efficient
list.remove(val);//all elements == val

```

## priority_queue
```c++
priority_queue<pair<int,int>, vector<pair<int,int>>,decltype(&cmp)> q(cmp);
q.top();q.pop();q.emplace(first,second)
```
## comments
### vector vs list vs dequeue 
vector: push_back and pop_back takes O(1), insert and erase takes O(n), access takes O(1)
list: double linked list, not continuous, insert and erase takes O(1) anywhere, cannot access[]
dequeue: push/pop front/back takes O(1), other == vector, space consuming

access: vector
insert/remove: list
work on front: dequeue

# Abstract Data Structure
## Queue
first in first out
queue<string> q;
q.front(), q.pop(), q.push()

## Stack
s.top(), s.pop(), s.push()


# Tools
## iterator
```c++
auto it = vec.begin();
while (it!=vec.end){cout << *it << endl;it++;}

*it;//解引用
iter->mem == (*iter).mem

auto mid = next(window.begin(), k / 2);
mid++;mid--

for (int x: myset) std::cout << " " << x;
for (const int& x: myset) std::cout << " " << x;
```
## sort
### sort
```c++
sort(vec.begin(),vec.end());//默认小在前
bool myfunc (int i, int j) {return i<j;}//bool == whether the first should go before the second
sort(vec.begin(),vec.end()，myfunc)
```
### heap
```c++
make_heap(v.begin(), v.end(), less<int>());//这样在前面的是最大的
make_heap(v.begin(),v.end(), greater<int>());//在前面是最小的
//heap的话自己定义的函数和sort的用法相反 true对应的在后面 

//push
v.push_back(val);push_heap(v.begin(),v.end())

//pop
pop_heap(v.begin(),v.end());v.pop_back();
//pop_heap()把堆顶的放到尾，然后vec.back();vec.pop_back()
```
make_heap再sort_heap可以实现排序

