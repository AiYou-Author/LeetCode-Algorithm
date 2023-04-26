# 基础算法笔记

##  1.排序算法





 





### 0.基本概念





#### 时间复杂度

​		一般情况下，算法中基本操作重复执行的次数是问题规模n的某个函数，用T(n)表示，若有某个辅助函数f(n),使得当n趋近于无穷大时，T（n)/f(n)的极限值为不等于零的常数，则称f(n)是T(n)的同数量级函数。记作T(n)=Ｏ(f(n)),称Ｏ(f(n)) 为算法的渐进时间复杂度，简称时间复杂度。

##### 最坏时间复杂度和平均时间复杂度

　最坏情况下的时间复杂度称最坏时间复杂度。一般不特别说明，讨论的时间复杂度均是最坏情况下的时间复杂度。

​	这样做的原因是：最坏情况下的时间复杂度是算法在任何输入实例上运行时间的上界，这就保证了算法的运行时间不会比任何更长。

##### 平均时间复杂度

　平均时间复杂度是指所有可能的输入实例均以等概率出现的情况下，算法的期望运行时间。设每种情况的出现的概率为pi,平均时间复杂度则为sum(pi*f(n))







#### 空间复杂度

​	一个程序的空间复杂度是指运行完一个程序所需内存的大小。利用程序的空间复杂度，可以对程序的运行所需要的内存多少有个预先估计。一个程序执行时除了需要存储空间和存储本身所使用的指令、常数、变量和输入数据外，还需要一些对数据进行操作的工作单元和存储一些为现实计算所需信息的辅助空间。程序执行时所需存储空间包括以下两部分。　　

（1）固定部分。这部分空间的大小与输入/输出的数据的个数多少、数值无关。主要包括指令空间（即代码空间）、数据空间（常量、简单变量）等所占的空间。这部分属于静态空间。

（2）可变空间，这部分空间的主要包括动态分配的空间，以及递归栈所需的空间等。这部分的空间大小与算法有关。

一个算法所需的存储空间用f(n)表示。S(n)=O(f(n))　　其中n为问题的规模，S(n)表示空间复杂度。 









#### 稳定性

所谓稳定性是指待排序的序列中有两元素相等,排序之后它们的先后顺序不变.





#### 小结

![img](https://s2.loli.net/2022/05/01/fC6vlOKekc7YVL9.png)











### 1.选择排序

从待排序的数据元素中找到最大的一个元素与序列的首位进行交换，再将剩余序列中最大的元素与第二个元素交换，以此类推。

时间复杂度O(N^2)，额外空间复杂度O(1)



```c++
//选择排序
void SelectionSort(int arr[], int size)
{
	int MaxTemp = 0;

	for (int i = 0; i < size; i++)
	{
		MaxTemp = i;
		for (int j = i; j < size; j++)
		{
			MaxTemp = arr[MaxTemp] > arr[j] ? MaxTemp : j;
		}
		swap(arr[i], arr[MaxTemp]);
	}
}
```







### 2.冒泡排序

依次比较相邻的元素，按大小交换，直至结尾，将最大（最小）排至队尾。依次比较前N-1个相邻元素，按大小交换，以此类推。

时间复杂度O(N^2)，额外空间复杂度O(1)



```c++
void BubbleSort(int arr[], int size)
{
	for (int i = 0; i < size-1; i++)
	{
		for (int j = 0; j < size-i-1; j++)
		{
			if (arr[j] > arr[j + 1])
				swap(arr[j], arr[j + 1]);
		}
	}
}
```







### 3.插入排序

将待排序的数据插入到前面已经排序好的序列中，无序序列的首元素与有序序列比较插入到合适位置。

时间复杂度O(N^2)，额外空间复杂度O(1)

最好时间复杂度O(N)

```c++
void InsertSort(int arr[], int size)
{
	for (int i = 0; i < size; i++)
	{
		for (int j = i; j > 0; j--)
		{
			if (arr[j] > arr[j - 1])
				std::swap(arr[j], arr[j - 1]);
		}
	}
}
```







### 4.归并排序

归并排序是建立在递归的条件下，将序列持续两分，之后合并并排序。

时间负载度O(N*logN),额外空间复杂度O(N)

```c++
void Merge(int arr[], int l, int mid, int r)
{
	int *TempArr = new int[r - l + 1];
	int i = 0;
	int p1 = l;
	int p2 = mid+1;
	while (p1 <= mid && p2 <= r)
	{
		TempArr[i++] = arr[p1] < arr[p2] ? arr[p1++] : arr[p2++];
	}
	while (p1 <= mid)
	{
		TempArr[i++] = arr[p1++];
	}
	while (p2<=r)
	{
		TempArr[i++] = arr[p2++];
	}
	for (int i = 0; i < (r - l + 1); i++)
	{
		arr[l + i] = TempArr[i];
	}
    delete []TempArr;
}


void MergeSort(int arr[], int l, int r)
{
	if (l == r)
		return;
	int mid = (l + r) >> 1;
	MergeSort(arr, l, mid);
	MergeSort(arr, mid+1, r);
	Merge(arr, l, mid, r);
}
```







#### 小和问题和逆序对问题 

##### 小和问题 

在一个数组中，每一个数左边比当前数小的数累加起来，叫做这个数组 的小和。求一个数组 的小和。 例子:[1,3,4,2,5] 1左边比1小的数，没有; 3左边比3小的数，1; 4左 边比4小的数，1、3; 2左边比2小的数，1; 5左边比5小的数，1、3、4、 2; 所以小和为1+1+3+1+1+3+4+2=16

```c++
int SmallSum(int arr[], int l, int mid, int r)
{
	int *TempArr = new int[r - l + 1];
	int ans = 0;
	int i = 0;
	int p1 = l;
	int p2 = mid + 1;
	while (p1 <= mid && p2 <= r)
	{
		ans += arr[p1] < arr[p2] ? (r - p2 + 1)*arr[p1] : 0;
		TempArr[i++] = arr[p1] < arr[p2] ? arr[p1++] : arr[p2++];
	}
	while (p1 <= mid)
	{
		TempArr[i++] = arr[p1++];
	}
	while (p2 <= r)
	{
		TempArr[i++] = arr[p2++];
	}
	for (int i = 0; i < (r - l + 1); i++)
	{
		arr[l + i] = TempArr[i];
	}
	return ans;
}

int SmallSumProcess(int arr[], int l, int r)
{
	if (l == r)
		return 0;
	int mid = (l + r) >> 1;
	int AnsL = 0, AnsR = 0,Ans;
	AnsL = SmallSumProcess(arr, l, mid);
	AnsR = SmallSumProcess(arr, mid + 1, r);
	Ans=SmallSum(arr, l, mid, r);

	return (AnsL + AnsR + Ans);
}
```



```c++
//对数器
int Comparator(int arr[], int size)
{
	int ans=0;
	for (int i = 0; i < size; i++)
	{
		for (int j = i; j < size; j++)
		{
			ans += arr[i] < arr[j] ? arr[i] : 0;
		}
	}
	return ans;
}
```

使用归并排序类似算法求小和的时间复杂度为O(N*logN)，对数器时间复杂度为O(N^2)







##### 逆序对

逆序对问题 在一个数组中，左边的数如果比右边的数大，则折两个数 构成一个逆序对，请打印所有逆序 对。











### 5.堆（堆排序）

1，堆结构就是用数组实现的完全二叉树结构 

2，完全二叉树中如果每棵子树的最大值都在顶部就是大根堆 

3，完全二叉树中如果每棵子树的最小值都在顶部就是小根堆 

4，heapInsert从上到下建立堆

5，heapify从下到上建立堆

6，堆结构的增大和减少 

7，优先级队列结构，就是堆结构



完全二叉树中，第i个节点的左孩子2i+1，右孩子2i+2，父节点(i-1)/2



#### HeapInsert 从上到下建立堆

1. 首先增加堆的长度，在最末尾的地方加入最新插入的元素。
2. 比较当前元素和它的父结点值，如果比父结点值大，则交换两个元素，否则返回。
3. 重复步骤2

```c++
void HeapInsert(int arr[], int size, int index)
{
	while (arr[index] > arr[(index - 1) / 2])
	{
		swap(arr[index] , arr[(index - 1) / 2]);
		index = (index - 1) / 2;
	}

}


for(int i=0;i<length;i++)
{
    HeapInsert(arr,i);
}
```

建立一个大根堆的时间复杂度是O(NlogN)=log1+log2+...+log(N-1)

时间复杂度为O(NlogN)







#### Heapify从下到上建立堆

比如大根堆中，索引位置为 i 的元素的值发生了改变（变小），则将其与左右两个孩子进行比较，将其与较大的孩子进行交换。 左孩子的索引位置为 2i+1 , 右孩子的索引位置为 2i+2.

```c++
void Heapify(int arr[], int size, int index)
{
	int left = index * 2 + 1;
	int largest;
	while (left < size)
	{
		largest = (left + 1 < size) && arr[left + 1] > arr[left] ? left + 1: left;
		largest = arr[largest] > arr[index] ? largest : index;
		if (largest == index)
		{
			break;
		}
		swap(arr[largest], arr[index]);	
		index = largest;
		left = index * 2 + 1;
	}
}


for (int i = length-1; i >= 0; i--)
{
	Heapify(arr1, length, i);
}
```

时间复杂度为O(N)



#### 堆排序

1，先让整个数组都变成大根堆结构，建立堆的过程: 1)从上到下的方法，时间复杂度为O(NlogN) 2)从下到上的方法，时间复杂度为O(N)

 2，把堆的最大值和堆末尾的值交换，然后减少堆的大小之后，再去调 整堆，一直周而复始，时间复杂度为O(N*logN)

 3，堆的大小减小成0之后，排序完成

```c++
void HeapSort(int arr[], int size)
{
	for (int i = 0; i < size; i++)
	{
		HeapInsert(arr,size,i);
	}
	for (int i = 0; i < size; i++)
	{
		swap(arr[0], arr[size - i - 1]);
		Heapify(arr, size - i - 1, 0);
	}
}
```

时间复杂度O(N*logN)



##### 堆示例

​	已知一个几乎有序的数组，几乎有序是指，如果把数组排好顺序的话，每个元素移动的距离可以不超过k，并且k相对于数组来说比较小。请选择一个合适的排序算法针对这个数据进行排序。

解：假设k为6，取前7个元素进行小根堆，将首个元素取出，再将数组中下个元素步入小根堆，周而复始，得到排序结果。

```c++
void SortArrayDistanceLessK(int arr[],int size,int k)
{
	priority_queue<int, vector<int>, greater<int>> Heap;
	int i = 0;
	for (i = 0; i < min(size,k); i++)
	{
		Heap.push(arr[i]);
	}
	int j = 0;
	for (j = 0; i < size; i++, j++)
	{
		Heap.push(arr[i]);
		arr[j] = Heap.top();
		Heap.pop();
	}
	while (!Heap.empty())
	{
		arr[j++] = Heap.top();
		Heap.pop();
	}
}
```





#### 小根堆

```c++
priority_queue<int,vector<int>,greater<int>>;
```



### 6.快速排序

#### 不改进的快速排序

1）把数组范围中的最后一个数作为划分值，然后把数组通过荷兰国旗问题分成三个部 分： 左侧<划分值、中间==划分值、右侧>划分值 

2）对左侧范围和右侧范围，递归执行

最好的时间复杂度为O(NlogN)，每次num选择为数组中间的数，T(N)=2T(N/2)+O(N)=O(NlogN)；

最差的时间复杂度为O(N^2)，每次num都选择为边界值;

```c++
//不改进的快速排序
int *QuickSortProcess(int arr[], int l, int r)
{
	int num = arr[l];
	int l_size = l, r_size = r;
	int i = l;
	while (i <= r_size)
	{
		if (arr[i] < num)
			swap(arr[l_size++], arr[i++]);
		else if (arr[i] > num)
			swap(arr[r_size--], arr[i]);
		else
			i++;
	}
	return new int[2]{ l_size,r_size };
}
void QuickSort(int arr[], int l, int r)
{
	if (l < r)
	{
		int *pos=QuickSortProcess(arr, l, r);
		QuickSort(arr, l, pos[0] - 1);
		QuickSort(arr, pos[1] + 1, r);
	}
}
```





#### 随即快速排序

1）在数组范围中，等概率随机选一个数作为划分值，然后把数组通过荷兰国旗问题分 成三个部分： 左侧<划分值、中间==划分值、右侧>划分值 

2）对左侧范围和右侧范围，递归执行 

3）时间复杂度为O(N*logN)

```c++
int num=arr[rand()%(r-l)+l];

srand((unsigned)time(NULL));
```











#### 荷兰国旗问题

给定一个数组arr，和一个数num，请把小于等于num的数放在数 组的左边，大于num的 数放在数组的右边。要求额外空间复杂度O(1)，时间复杂度O(N)

```c++
void NetherlandsFlag(int arr[], int l, int r)
{
	int num = arr[l];
	int l_size = l, r_size = r;
	int i = l;
	while(l_size < r_size)
	{
		if (arr[i] < num)
			swap(arr[l_size++], arr[i++]);
		else if (arr[i] > num)
			swap(arr[r_size--], arr[i]);
		else
			i++;
	}
}
```



























### 7.计数排序

遍历整个序列，寻找整个数组的计数范围。

再次遍历序列，记录整个范围数组各个元素出现的次数

最后将计数数组导出得到排序序列

```c++
void CountSort(int arr[], int size)
{
	int Max = INT_MIN;
	for (int i = 0; i < size; i++)
	{
		Max = Max > arr[i] ? Max : arr[i];
	}
	
	int *CountVec = new int[Max + 1]();

	for (int i = 0; i < size; i++)
	{
		CountVec[arr[i]]++;
		
	}
	int j = 0;
	for (int i = 0; i < Max+1; i++)
	{
		while (CountVec[i]-- > 0)
		{
			arr[j++] = i;
		}
	}
}
```











### 8.基数排序

根据数组序列从个位开始，将他们按照大小关系放至桶中，排序。

然后根据十位，依次进桶排序。循环往复。

时间复杂度为O(N)，额外空间复杂度为O(M)



1）首先判断有几位数

- 对个位数进行排序：设置一个0~9的频率数组count，之后对其积分得到，各个数字在序列中的位置

| 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 1    | 1    | 2    | 1    | 0    | 0    | 2    | 1    | 0    | 0    |

| 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 1    | 2    | 4    | 5    | 5    | 5    | 7    | 8    | 8    | 8    |

个位为0的在序列中位置为1；个位为2的在序列中位置为3,4

```c++
bucket[count[j]-1]=arr[i];
count[j]--;
arr=bucket;
```

- 循环，进行十位数排序
- 进行百位排序

```c++
int Maxbit(int arr[],int size)
{
	int Max = INT_MIN;
	for (int i = 0; i < size; i++)
	{
		Max = Max > arr[i] ? Max : arr[i];
	}

	int res = 0;
	while (Max > 0)
	{
		res++;
		Max /= 10;
	}
	return res;
}

int getDigit(int num, int d) 
{
	return (num / (int)pow(10, d)) % 10;
}

void RadixSort(int arr[], int size)
{
	int j = 0;
	int sum = 0;
	for (int d = 0; d < Maxbit(arr,size); d++)
	{
		int *count = new int[10]();
		int *bucket = new int[size]();

		for (int i = 0; i < size; i++)
		{
			j = getDigit(arr[i], d);
			count[j] ++;
		}

		for (int i = 0; i < 10; i++)
		{
			sum += count[i];
			count[i] = sum;
		}

		for (int i = size-1; i >= 0; i--)
		{
			j = getDigit(arr[i], d);
			bucket[count[j] - 1] = arr[i];
			count[j]--;
		}

		for (int i = 0; i < size; i++)
		{
			arr[i] = bucket[i];
		}
		
		delete[]count;
		delete[]bucket;
	}
}
```







## 2.哈希表

1）哈希表在使用层面上可以理解为一种集合结构

2）如果只有key，没有伴随数据value，可以使用HashSet结构(C++中叫UnOrderedSet) 

3）如果既有key，又有伴随数据value，可以使用HashMap结构(C++中叫UnOrderedMap)

4）有无伴随数据，是HashMap和HashSet唯一的区别，底层的实际结构是一回事 

5）使用哈希表增(put)、删(remove)、改(put)和查(get)的操作，可以认为时间复杂度为 O(1)，但是常数时间比较大 

6）放入哈希表的东西，如果是基础类型，内部按值传递，内存占用就是这个东西的大小 7）放入哈希表的东西，如果不是基础类型，内部按引用传递，内存占用是这个东西内存地 址的大小

#### 常见的哈希结构

|     集合      | 底层实现 | 是否有序 | 数值是否可以重复 | 能否更改数值 | 查询效率 | 增删效率 |
| :-----------: | :------: | :------: | :--------------: | :----------: | :------: | :------: |
|      set      |  红黑树  |   有序   |        否        |      否      | O(logn)  | O(logn)  |
|   multiset    |  红黑树  |   有序   |        是        |      否      | O(logn)  | O(logn)  |
| unordered_set |  哈希表  |   无序   |        否        |      否      |   O(1)   |   O(1)   |

|     集合      | 底层实现 | 是否有序 | 数值是否可以重复 | 能否更改数值 | 查询效率 | 增删效率 |
| :-----------: | :------: | :------: | :--------------: | :----------: | :------: | :------: |
|      map      |  红黑树  | key有序  |   key不可重复    | key不可修改  | O(logn)  | O(logn)  |
|   multimap    |  红黑树  | key有序  |    key可重复     | key不可修改  | O(logn)  | O(logn)  |
| unordered_map |  哈希表  | key无序  |   key不可重复    | key不可修改  |   O(1)   |   O(1)   |













## 3.链表



单链表节点结构

```c++
template<typename T>
struct Node
{
	T val;
	Node* next;
	Node(int data):val(data),next(NULL) {}
};

```

双链表结构

```c++
template<typename T>
struct Node
{
	T val;
	Node* next;
    Node* last;
	Node(int data):val(data),next(NULL) {}
};

```

#### 1.打印链表

```c++
void PrintNode(Node<int>*head)
{
	while (head != NULL)
	{
		cout << head->val << " ";
		head = head->next;
	}
	cout << endl;
}
```





#### 2.反转单向和双向链表

链表长度为N，时间复杂度为O(N)，额外空间复杂度为O(1)

```c++
Node<int>* ReveseList(Node<int>* head)
{
	Node<int> *pre = NULL;
	Node<int> *next = NULL;
	while (head != NULL)
	{
		next = head->next;
		head->next = pre;
		pre = head;
		head = next;
	}
	return pre;
}
```

```c++
DoubleNode<int>* ReveseDoubleList(DoubleNode<int>* head)
{
	DoubleNode<int> *pre = NULL;
	DoubleNode<int> *next = NULL;
	while (head != NULL)
	{
		next = head->next;
		head->next = pre;
		head->last = next;
		pre = head;
		head = next;
	}
	return pre;
}
```









#### 3.打印两个有序链表的公共部分

【题目】 给定两个有序链表的头指针head1和head2，打印两个链表的公共部分。 

【要求】 如果两个链表的长度之和为N，时间复杂度要求为O(N)，额外空间复杂度要求为O(1)

```c++
void PrintCommonPart(Node<int> *head1,Node<int> *head2)
{
	while (head1 != NULL && head2 != NULL)
	{
		if (head1->val == head2->val)
		{
			cout << head1->val << " ";
			head1 = head1->next;
			head2 = head2->next;
		}
		else
		{
			head1->val > head2->val ? head2 = head2->next : head1 = head1->next;
		}
		
	}
	cout << endl;
}
```





#### 4.判断链表是否为回文结构

【题目】给定一个单链表的头节点head，请判断该链表是否为回文结构。 

【例子】1->2->1，返回true； 1->2->2->1，返回true；15->6->15，返回true； 1->2->3，返回false。 

【例子】如果链表长度为N，时间复杂度达到O(N)，额外空间复杂度达到O(1)。

ps：利用快慢指针，寻找链表的中点

```c++
//将链表压入栈，栈与原链表相比较,额外空间复杂度高O(n)
bool IsPalindromeList1(Node<int> *head)
{
	Node<int> *cur = head;
	stack<Node<int>*> *ReverseStack=new stack<Node<int>*>;
	while (cur != NULL)
	{
		ReverseStack->push(cur);
		cur = cur->next;
	}
	cur = head;
	while (!ReverseStack->empty())
	{
		if (cur->val != ReverseStack->top()->val)
		{
			
			delete ReverseStack;
			return false;
		}	
		ReverseStack->pop();
		cur = cur->next;
		
	}

	delete ReverseStack;
	return true;
}

//将链表的后半部分压入栈，额外空间复杂度稍高O(n/2)
bool IsPalindromeList2(Node<int> *head)
{
	Node<int> *low = head;
	Node<int> *fast = head->next;
	stack<Node<int>*> *ReverseStack = new stack<Node<int>*>;
	while (fast->next != NULL&&fast->next->next!=NULL)
	{
		low = low->next;
		fast = fast->next->next;
	}

	while (low != NULL)
	{
		ReverseStack->push(low);
		low = low->next;
	}
	low = head;
	while (!ReverseStack->empty())
	{
		if (low->val != ReverseStack->top()->val)
		{

			delete ReverseStack;
			return false;
		}
		ReverseStack->pop();
		low = low->next;

	}

	delete ReverseStack;
	return true;
}

//将链表的后半部分反转，额外空间复杂度低为O(1)
bool IsPalindromeList3(Node<int> *head)
{
	Node<int> *pre = NULL;
	Node<int> *low = head;
	Node<int> *fast = head->next;
	while (fast->next != NULL && fast->next->next != NULL)
	{
		low = low->next;
		fast = fast->next->next;
	}
	while (low != NULL)
	{
		fast = low->next;
		low->next = pre;
		pre = low;
		low = fast;
	}
	low = head;
	while (pre != NULL & low != NULL)
	{
		if (pre->val != low->val)
		{
			return false;
		}
		pre = pre->next;
		low = low->next;
	}
	return true;
}

```



#### 5.单向链表按值划分大小

将单向链表按某值划分成左边小、中间相等、右边大的形式 

【题目】给定一个单链表的头节点head，节点的值类型是整型，再给定一个整 数pivot。实现一个调整链表的函数，将链表调整为左部分都是值小于pivot的 节点，中间部分都是值等于pivot的节点，右部分都是值大于pivot的节点。 

【进阶】在实现原问题功能的基础上增加如下的要求 

【要求】调整后所有小于pivot的节点之间的相对顺序和调整前一样 

【要求】调整后所有等于pivot的节点之间的相对顺序和调整前一样 

【要求】调整后所有大于pivot的节点之间的相对顺序和调整前一样 

【要求】时间复杂度请达到O(N)，额外空间复杂度请达到O(1)。

```c++
//法一：将节点放入数组进行快速排序，再将数组链接
void QuickSort(Node<int>* arr[], int size,int pivot)
{
	int l = 0;
	int r = size-1;
	int i = 0;	
	while (i<=r)
	{
		if (arr[i]->val < pivot)
		{
			swap(arr[l++], arr[i++]);
		}
		else if(arr[i]->val == pivot)
		{
			i++;
		}
		else
		{
			swap(arr[r--], arr[i]);
		}
	}
}


Node<int> * SmallerEqualBigger1(Node<int> *head, int pivot)
{
	Node<int>*cur = head;
	int size=0;
	while (cur!=NULL)
	{
		size++;
		cur = cur->next;
	}
	cur = head;
	Node<int>* *arr = new Node<int>*[size];
	for (int i = 0; i < size; i++)
	{
		arr[i]=cur;
		cur = cur->next;
	}
	QuickSort(arr, size, pivot);

	for (int i = 0; i < size-1; i++)
	{
		arr[i]->next = arr[i + 1];
	}
	arr[size - 1]->next = NULL;

	return arr[0];
}
```



```C++
//法2：使用六个指针，小于，等于，大于区域的头尾指针，额外空间复杂度为O(1),时间复杂度为O(N)
Node<int> * SmallerEqualBigger2(Node<int> *head, int pivot)
{
	listNode *SH=NULL, *ST = NULL, *EH = NULL, *ET = NULL, *MH = NULL, *MT = NULL;//小于，等于，大于区域的头尾指针
	listNode *cur = head;
	listNode *next;
	while (cur!=NULL)
	{
		next = cur->next;
		cur->next = NULL;
		if (cur->val < pivot)
		{
			if (SH == NULL && ST == NULL)
			{
				SH = cur;
				ST = cur;
			}
			else
			{
				ST->next = cur;
				ST = ST->next;	
			}
		}
		else if(cur->val == pivot)
		{
			if (EH == NULL && ET == NULL)
			{
				EH = cur;
				ET = cur;
			}
			else
			{
				ET->next = cur;
				ET = ET->next;
			}
		}
		else
		{
			if (MH == NULL && MT == NULL)
			{
				MH = cur;
				MT = cur;
			}
			else
			{
				MT->next = cur;
				MT = MT->next;
			}
		}
		cur = next;
	}

	if (ST != NULL)
	{
		ST->next = EH;
		ET = ET == NULL ? ST : ET;
	}

	if (ET != NULL)
	{
		ET->next = MH;
	}

	SH = SH != NULL ? SH : EH != NULL ? EH : MH;

	return SH;
}
```



#### 6.复制含有随机指针节点的链表

【题目】一种特殊的单链表节点类描述如下 

```c++
class Node { 
    int value; 
    Node next; 
    Node rand; 
    Node(int val) 
    { value = val; } 
}
```

rand指针是单链表节点结构中新增的指针，rand可能指向链表中的任意一个节 点，也可能指向null。给定一个由Node节点类型组成的无环单链表的头节点 head，请实现一个函数完成这个链表的复制，并返回复制的新链表的头节点。

【要求】时间复杂度O(N)，额外空间复杂度O(1)

解题思路：利用map，key存储当前节点，value存储复制节点

```c++
Node<int>* copyListWithRand(Node<int>*head)
{
	Node<int>*cur = head;
	map<Node<int>*, Node<int>*> m1;
	
	while (cur != NULL)
	{
		m1.insert(make_pair(cur, new Node<int>(cur->val)));
		cur = cur->next;
	}
	
	cur = head;
	while (cur->next != NULL)
	{
		(*m1.find(cur)).second->next = (*m1.find(cur->next)).second;
		cur = cur->next;
	}
	return (*m1.find(head)).second;
}
```









#### 7.两个链表相交

【题目】给定两个可能有环也可能无环的单链表，头节点head1和head2。请实 现一个函数，如果两个链表相交，请返回相交的 第一个节点。如果不相交，返 回null 

【要求】如果两个链表长度之和为N，时间复杂度请达到O(N)，额外空间复杂度 请达到O(1)。

```c++
//判断是否有环，有环返回入环点，无环返回NULL
listNode* HasCircle(listNode*head)
{
	listNode* low = head;
	listNode* fast = head;
	while (fast != NULL)
	{
		low = low->next;
		fast = fast->next->next;
		if (low == fast)
		{
			fast = head;
			while (low != fast)
			{
				low = low->next;
				fast = fast->next;
			}
			return low;
		}
	}
	return NULL;
}

listNode* NoLoop(listNode*head1, listNode*head2)
{
	int n = 0;
	listNode* cur1 = head1;
	listNode* cur2 = head2;
	while (cur1->next != NULL)
	{
		n++;
		cur1 = cur1->next;
	}
	
	while (cur2->next != NULL)
	{
		n--;
		cur2 = cur2->next;
	}
	if (cur1 != cur2)
		return NULL;
	//判断谁更长
	cur1 = n > 0 ? head1 : head2;
	cur2 = cur1 == head1 ? head2 : head1;
	n = abs(n);
	while (n != 0)
	{
		n--;
		cur1 = cur1->next;
	}
	while (cur1 !=cur2)
	{
		cur1 = cur1->next;
		cur2 = cur2->next;
	}
	return cur1;

}

listNode* BothLoop(listNode*head1, listNode*head2, listNode*loop1, listNode*loop2)
{
	int n = 0;
	listNode* cur1 = head1;
	listNode* cur2 = head2;
	if (loop1 == loop2)
	{
		while (cur1->next != loop1)
		{
			n++;
			cur1 = cur1->next;
		}

		while (cur2->next != loop2)
		{
			n--;
			cur2 = cur2->next;
		}
		if (cur1 != cur2)
			return loop1;
		//判断谁更长
		cur1 = n > 0 ? head1 : head2;
		cur2 = cur1 == head1 ? head2 : head1;
		n = abs(n);
		while (n != 0)
		{
			n--;
			cur1 = cur1->next;
		}
		while (cur1 != cur2)
		{
			cur1 = cur1->next;
			cur2 = cur2->next;
		}
		return cur1;
	}
	else
	{
		
		cur1 = loop1->next;
		while (cur1 != loop1)
		{
			if (cur1 == loop2)
				return loop1;
			cur1 = cur1->next;
		}
		return NULL;
	}
}

listNode* FindFirstIntersectNode(listNode*head1, listNode*head2)
{
	//判断是否有环
	listNode* loop1 = HasCircle(head1);
	listNode* loop2 = HasCircle(head2);
	/*cout << loop1->val << endl;
	cout << loop2->val << endl;*/
	if (loop1 == NULL && loop2 == NULL)
	{
		return NoLoop(head1, head2);
	}
	else if(loop1 != NULL && loop2 != NULL)
	{
		
		return BothLoop(head1,head2,loop1,loop2);
	}
	else
	{
		return NULL;
	}
}

```







#### 快慢指针



#### 面试技巧

面试时链表解题的方法论 

1）对于笔试，不用太在乎空间复杂度，一切为了时间复杂度 

2）对于面试，时间复杂度依然放在第一位，但是一定要找到空间最省的方法 

重要技巧： 

1）额外数据结构记录（哈希表等）

2）快慢指针























## 4.二叉树

```c++
template<class T>
struct Node
{
	T value;
	Node* left;
	Node* right;
	Node(int val) :value(val), left(NULL), right(NULL) {}
};
```



#### 0.二叉树递归序

```c++
void OrderRecur(TreeNode *head)
{
	if (head == NULL)
		return;
	cout << head->value << " ";
	OrderRecur(head->left);
	cout << head->value << " ";
	OrderRecur(head->right);
	cout << head->value << " ";
}
```







#### 1.使用递归和非递归方式实现二叉树的先序，中序和后序遍历

递归方法：二叉树先序取递归序首先出现的位置，中序取第二次出现的位置，后序取第三次出现的位置

```c++
//先序遍历
void preOrderRecur(TreeNode *head)
{
	if (head == NULL)
		return;
	cout << head->value << " ";
	preOrderRecur(head->left);
	preOrderRecur(head->right);
}

//中序遍历
void inOrderRecur(TreeNode *head)
{
	if (head == NULL)
		return;
	inOrderRecur(head->left);
	cout << head->value << " ";
	inOrderRecur(head->right);
}

//后序遍历
void posOrderRecur(TreeNode *head)
{
	if (head == NULL)
		return;
	posOrderRecur(head->left);
	posOrderRecur(head->right);
	cout << head->value << " ";
}
```



非递归方法：

先序：将头结点压如栈中

1. 弹出栈顶cur
2. 打印处理cur
3. 将cur的右节点和左节点依次压入栈
4. 重复步骤1-3，直至栈空

```c++
void preOrderUnRecur(TreeNode *head)
{
	stack<TreeNode*> s1;
	TreeNode* cur;
	s1.push(head);
	while (!s1.empty())
	{
		cur = s1.top();
		cout << cur->value << " ";
		s1.pop();
		if(cur->right!=NULL)
			s1.push(cur->right);
		if (cur->left != NULL)
			s1.push(cur->left);
	}
}
```



中序：设置头结点为cur

1. 将cur的整个左边界压入栈中，直至左节点为空
2. 弹出栈顶cur
3. 打印处理cur
4. cur=cur.right
5. 重复步骤1-4，直至栈为空且cur为空

```c++
void inOrderUnRecur(TreeNode *head)
{
	stack<TreeNode*> s1;
	TreeNode* cur;
	//s1.push(head);
	cur = head;
	while (!s1.empty()||cur!=NULL)
	{
		if (cur!=NULL)
		{
			s1.push(cur);
			cur = cur->left;
		}
		else
		{
			cur = s1.top();
			cout << cur->value << " ";
			s1.pop();
			//if(cur->right =NULL)
			cur = cur->right;
		}
	}
}
```



后序：将头结点压入栈1

1. 弹出栈1顶cur
2. 将cur压入栈2
3. 将cur的左节点和右节点依次压入栈1
4. 重复1-3，直至栈1空
5. 按顺序弹出栈2，并打印

```c++
void podOrderUnRecur(TreeNode *head)
{
	stack<TreeNode*> s1;
	stack<TreeNode*> s2;
	TreeNode* cur;
	s1.push(head);
	while (!s1.empty())
	{
		cur = s1.top();
		s2.push(cur);
		s1.pop();
		if (cur->left != NULL)
			s1.push(cur->left);
		if (cur->right != NULL)
			s1.push(cur->right);
	}
	while (!s2.empty())
	{
		cout << s2.top()->value << " ";
		s2.pop();
	}
}
```



#### 2.宽度优先遍历

1. 准备一个队列，插入头结点
2. 弹出队列头cur，并打印
3. 将cur的左右子节点压入队列
4. 重复2-3，直至队列为空

```c++
void BFS(TreeNode*head)
{
	queue<TreeNode*> *que = new queue<TreeNode*>;
	que->push(head);
	while (!que->empty())
	{
		head = que->front();
		que->pop();
		cout << head->value << " ";
		if(head->left!=NULL)
			que->push(head->left);
		if (head->right != NULL)
			que->push(head->right);
	}
	delete que;
}
```





#### 3.求一棵树的宽度

利用宽度优先遍历，计算每行的个数

建立哈希表，记录各个节点的行，curnodelevel

curlevel为当前行

curlevelnode为curlevel的节点数

通过curlevel与curnodelevel对比来判断当前节点所在行，以及是否更新当前行curlevel的curlevelnode

```c++
void GetMaxWidth(TreeNode* head)
{
	queue<TreeNode*> *que = new queue<TreeNode*>;
	map<TreeNode*, int> *levelMap = new map<TreeNode*, int>;
	int curNodelevel=1;
	int curlevel = 1;
	int curlevelNode = 0;
	int Max = INT_MIN;
	que->push(head);
	levelMap->insert(make_pair(head, curNodelevel));
	while (!que->empty())
	{
		head = que->front();
		que->pop();
		curNodelevel = (*(levelMap->find(head))).second;
		if (curlevel == curNodelevel)
		{
			curlevelNode++;
		}
		else
		{
			Max = max(curlevelNode, Max);
			curlevelNode = 0;
			curlevel++;
			
		}

		if (head->left != NULL)
		{
			que->push(head->left);
			levelMap->insert(make_pair(head->left, curNodelevel + 1));
		}
		if (head->right != NULL)
		{
			que->push(head->right);
			levelMap->insert(make_pair(head->right, curNodelevel + 1));
		}

	}
	Max = max(curlevelNode, Max);
	cout << "最大宽度：" << Max;

}
```









#### 4.是否为搜索二叉树 IsBST(binary search tree)

​	搜索二叉树是一种特殊有序的二叉树，如果一棵树不为空，并且如果它的根节点左子树不为空，那么它左子树上面的所有节点的值都小于它的根节点的值，如果它的右子树不为空，那么它右子树任意节点的值都大于他的根节点的值，它的左右子树也是二叉搜索树。

​	**如果对二叉搜索树进行中序遍历（左中右），那么会得到一个从小到大的序列**

```c++
void InOrderRecur(TreeNode *head, queue<TreeNode*> InQueue)
{
	if (head == NULL)
		return;
	InOrderRecur(head->left, InQueue);
	InQueue.push(head);
	InOrderRecur(head->right, InQueue);
}

bool IsBST(TreeNode *head)
{
	int PreValue = INT_MIN;
	queue<TreeNode*> InQueue;
	InOrderRecur(head, InQueue);
	while (!InQueue.empty())
	{
		if (InQueue.front()->value >= PreValue)
			PreValue = InQueue.front()->value;
		else
			return false;
	}
	return true;
}
```







#### 5.是否为完全二叉树isCBT(Complete Binary Search)

​	若设二叉树的深度为h，除第 h 层外，其它各层 (1~h-1) 的结点数都达到最大个数，第 h 层所有的结点都连续集中在最左边，这就是完全二叉树。

​	判断标准：利用宽度优先遍历

​	1）其有右节点无左节点 false

​	2）出现左右节点不全或皆无，后序节点皆为叶子节点

```c++
bool isCBT(TreeNode*head)
{
	queue<TreeNode*> *que = new queue<TreeNode*>;
	bool leaf = false;
	TreeNode *l = NULL;
	TreeNode *r = NULL;

	que->push(head);
	while (!que->empty())
	{
		head = que->front();
		que->pop();
		l = head->left;
		r = head->right;

		if (leaf&(l != NULL || r != NULL) || (l == NULL && r != NULL))
		{
			delete que;
			return false;
		}
		if (head->left != NULL)
			que->push(head->left);
		if (head->right != NULL)
			que->push(head->right);
		else
		{
			leaf = true;
		}
			
	}
	delete que;
	return true;
}
```



#### 6.是否为满二叉树FBT(Full Binary Tree)

节点个数为N，层数为L，判断N==2^L-1?

```c++
void process(TreeNode*head, int m, int &Max,int &size)
{
	if (head == NULL)
		return;
	Max = max(m, Max);
	size++;
	process(head->left, m + 1, Max,size);
	process(head->right, m + 1, Max,size);
}

bool isFBT(TreeNode*head)
{
	int MaxLevel = INT_MIN;
	int size = 0;
	process(head, 1, MaxLevel, size);
	if (size == (2 ^ MaxLevel - 1))
		return true;
	else
		return false;
};
```







#### 7.是否为平衡二叉树

平衡二叉树：**任意节点的左右子树的高度差都小于等于 1**

树形DP思维：

设置一个返回结构，包含高度和是否为平衡二叉树

先向左子树获取返回结构体，再向右子树获取返回结构体

最终更新当前节点的返回结构体

```C++
//树形DP解法
struct ReturnType
{
	int height;
	bool isBalance;
	ReturnType(int he, bool isBla) :height(he), isBalance(isBla) {}
};

ReturnType process(TreeNode *head)
{
	if (head == NULL)
		return ReturnType(0, true);
	ReturnType isleft = process(head->left);
	ReturnType isright = process(head->right);
	int height = max(isleft.height, isright.height) + 1;
	bool isBalance = isleft.isBalance&&isright.isBalance && (abs(isleft.height - isright.height) <= 1);
	return ReturnType(height, isBalance);
}

bool IsBalancedTree(TreeNode *head)
{
	ReturnType result=process(head);
	return result.isBalance;
}
```













#### 8.树形DP

对二叉树进行动态规划，向左右子树要信息ReturnType，在对自己的信息进行更新再返回ReturnType。





#### 9.给定两个二叉树的节点node1和node2，找到他们的最低公共祖先节点

法1：记录每个节点的父亲节点，遍历node1的所有父亲节点，寻找与node2相同的父亲节点

法2：递归算法：前序遍历

​	若遇到node1或node2就返回node1或node2，遇到NULL就返回NULL

​	若左右子树返回皆不为空，则返回当前节点，此节点为最低公共祖先

​	若左右子树有一个不为空，则返回不为空的节点

```c++
void insertMap(TreeNode* head, map<TreeNode*, TreeNode*> *map1)
{
	if (head == NULL)
		return;
	if (head->left != NULL)
		map1->insert(make_pair(head->left, head));
	if (head->right != NULL)
		map1->insert(make_pair(head->right, head));
	insertMap(head->left, map1);
	insertMap(head->right, map1);
}

//利用哈希表记录各个节点的祖先，之后判断两个节点祖先的交集
void LowestCommonAncestor1(TreeNode* head, TreeNode* o1, TreeNode* o2)
{
	map<TreeNode*, TreeNode*> *map1 = new map<TreeNode*, TreeNode*>;
	set<TreeNode*> set1;
	map1->insert(make_pair(head, new TreeNode(0)));
	insertMap(head, map1);

	while (map1->count(o1))
	{
		set1.insert(o1);
		o1 = (*(map1->find(o1))).second;
	}
	while (!set1.count(o2)) 
	{
		o2 = (*(map1->find(o2))).second;
	}
	cout << "最低公共祖先 " << o2->value << endl;
}




TreeNode* LowestCommonAncestor2(TreeNode* head, TreeNode* o1, TreeNode* o2)
{
	if (head == NULL || head == o1 || head == o2)
		return head;
	TreeNode* left = LowestCommonAncestor2(head->left, o1, o2);
	TreeNode* right = LowestCommonAncestor2(head->right, o1, o2);

	if (left != NULL && right != NULL)
		return head;
	return left != NULL ? left : right;
}
```





#### 10.返回node节点的后继节点

只给一个在二叉树中的某个节点node，请实现返回node的后继节点的函数。 

在二叉树的中序遍历的序列中， node的下一个节点叫作node的后继节点。

解：1）若此节点的右子树存在，则后续节点右子树的最左侧节点

​	2）若无右子树，直至寻找到当前节点为父亲节点的左节点，此时父亲节点为后继节点

```c++
TreeNode* SuccessorNode(TreeNode* head)
{
	if (head->right != NULL)
	{
		head = head->right;
		while (head->left != NULL)
			head = head->left;
		return head;
	}
	TreeNode *parent = head->father;
	while (parent->left != head && parent != NULL)
	{
		head = parent;
		parent = head->father;
	}
	return parent;
}
```



#### 11.二叉树的序列化和反序列化

就是内存里的一棵树如何变成字符串形式，又如何从字符串形式变成内存里的树

```c++
//序列化
string serialByPre(TreeNode* head)
{
	if (head == NULL)
	{
		return "#";
	}
	string res = head->value + "";
	res += serialByPre(head->left);
	res += serialByPre(head->right);
	return res;
}



TreeNode* process(queue<char> *str)
{
	if (str->front() == '#')
	{
		str->pop();
		return NULL;
	}
	TreeNode *head = new TreeNode(str->front());
	str->pop();
	head->left = process(str);
	head->right = process(str);
	return head;
}
//反序列化
TreeNode* reconPreOrder(string preStr)
{
	queue<char> *QueStr = new queue<char>;
	for (size_t i = 0; i < preStr.size(); i++)
	{
		QueStr->push(preStr[i]);
	}
	return process(QueStr);
}
```













## 5.图

图是一种非线性[数据结构](https://so.csdn.net/so/search?q=数据结构&spm=1001.2101.3001.7020)，由「节点（顶点）vertex」和「边 edge」组成，每条边连接一对顶点。

根据边的方向有无，图可分为「有向图」和「无向图」

表示图的方法通常有两种：

- 邻接矩阵
- 邻接表

```c++
class Node;
class Edge;

class Graph
{
public:
	map<int, Node> nodes;
	set<Edge> edges;
};

class Node
{
public:
	int value;
	int in;
	int out;
	vector<Node> nexts;
	vector<Edge> edges;

	bool operator<(const Node&n) const
	{
		return this->value < n.value;
	}
	bool operator==(const Node&n) const
	{
		return this->value == n.value&& this->in == n.in&& this->out == n.out;
	}
};

class Edge
{
public:
	int weight;
	Node from;
	Node to;

	bool operator<(const Edge&n) const
	{
		return this->weight < n.weight;
	}
};
```



### 1.宽度优先遍历

1.利用队列实现

2.从源节点开始一次按照宽度进队，然后弹出

3.每弹出一个点，就把该节点所有的没有进过队列的直接邻接节点放进队列

4.一直弹出直到队列为空

```c++
void BFS(Node head)
{
	Node cur;
	queue<Node> QueNode;
	set<Node> SetNode;
	SetNode.insert(head);
	QueNode.push(head);
	while (!QueNode.empty())
	{
		cout << QueNode.front().value;
		cur = QueNode.front();
		QueNode.pop();
		for (auto next : cur.nexts)
		{
			if (SetNode.count(next) != 0)
			{
				QueNode.push(next);
				SetNode.insert(next);
			}
		}
		
	}
}
```









### 2.广度优先遍历

1，利用栈实现 

2，从源节点开始把节点按照深度放入栈，然后弹出

3，每弹出一个点，判断该点的后续节点是否已经遍历

4，若未遍历，把该节点以及下一个没有进过栈的邻接点放入栈 

5，重复3-4，直到栈变空

```c++
void DFS(Node head)
{
	Node cur;
	stack<Node> StaNode;
	set<Node> SetNode;
	SetNode.insert(head);
	StaNode.push(head);
	cout << StaNode.top().value;
	while (!StaNode.empty())
	{
		cur = StaNode.top();
		StaNode.pop();
		for (auto next : cur.nexts)
		{
			if (SetNode.count(next) != 0)
			{
				StaNode.push(cur);
				StaNode.push(next);
				SetNode.insert(next);
				cout << next.value << " ";
				break;
			}
		}
	}
}
```



### 3.图的拓扑排序

1丶什么是拓扑排序
对一个有向无环图(Directed Acyclic Graph简称DAG)G进行拓扑排序，是将G中所有顶点排成一个线性序列，使得图中任意一对顶点u和v，若边(u,v)∈E(G)，则u在线性序列中出现在v之前。通常，这样的线性序列称为满足拓扑次序(Topological Order)的序列，简称拓扑序列。简单的说，由某个集合上的一个偏序得到该集合上的一个全序，这个操作称之为拓扑排序。 无向图和有环的有向图没有拓扑排序拓扑排序其实就是离散上的偏序关系的一个应用。
2、拓扑排序的步骤：
1.按照一定的顺序进行构造有向图，记录后个节点的入度;
2.从图中选择一个入度为0的顶点,输出该顶点;
3.从图中删除该顶点及所有与该顶点相连的边;
4.重复上述两步，直至所有顶点输出;
5.或者当前图中不存在入度为0的顶点为止。此时可说明图中有环;
6.因此，也可以通过拓扑排序来判断一个图是否有环。

```c++
void TopologySort(Node head, Graph graph)
{
	map<Node, int> inMap;
	queue<Node> zeroInQueue;
	Node cur;
	for (auto it = graph.nodes.begin(); it != graph.nodes.end(); it++)
	{
		inMap.insert(make_pair((*it).second, (*it).second.in));
		if ((*it).second.in == 0)
			zeroInQueue.push((*it).second);
	}
	while (!zeroInQueue.empty())
	{
		cur = zeroInQueue.front();
		cout << cur.value << " ";
		zeroInQueue.pop();
		for (auto Node : cur.nexts)
		{
			inMap.insert(make_pair(Node, (*inMap.find(Node)).second - 1));
			if ((*inMap.find(Node)).second == 0)
				zeroInQueue.push(Node);
		}
	}
}
```





### 4.图的最小生成树

关于图的几个概念定义：
**连通图**：在无向图中，若任意两个顶点vivi与vjvj都有路径相通，则称该无向图为连通图。
**强连通图**：在有向图中，若任意两个顶点vivi与vjvj都有路径相通，则称该有向图为强连通图。
**连通网**：在连通图中，若图的边具有一定的意义，每一条边都对应着一个数，称为权；权代表着连接连个顶点的代价，称这种连通图叫做连通网。
**生成树**：一个连通图的生成树是指一个连通子图，它含有图中全部n个顶点，但只有足以构成一棵树的n-1条边。一颗有n个顶点的生成树有且仅有n-1条边，如果生成树中再添加一条边，则必定成环。
**最小生成树**：在连通网的所有生成树中，所有边的代价和最小的生成树，称为最小生成树。



#### **1. Kruskal算法**

此算法可以称为“加边法”，初始最小生成树边数为0，每迭代一次就选择一条满足条件的最小代价边，加入到最小生成树的边集合里

(无向图)k算法：从边角度出发，依次选择最小的边，如果加上这条边会形成环，则不加这条边，如果不会形成环，则加上这条边

```c++
//是否成环
bool isCircle(vector<Node>n1, vector<Node>n2)
{
	return n1 == n2;
}

//求并集
void SetUnion(vector<Node>&n1, vector<Node>&n2)
{
	vector<Node>n3;
	set_union(n1.begin(),n1.end(), n2.begin(), n2.end(), insert_iterator<vector<Node>>(n3, n3.begin()));
	n1 = n3;
	n2 = n3;
}

void Kruskal(Graph graph)
{
	int num = 0;
	map<Node, vector<Node>> IncludeMap;
	priority_queue<Edge> edges;
	vector<Edge> result;
	//设置每个点对应的地址，初始化为自己
	for (auto it = graph.nodes.begin(); it != graph.nodes.end(); it++)
	{
		IncludeMap.insert(make_pair((*it).second, vector<Node>{(*it).second}));
	}

	//将边排序
	for (auto curedge : graph.edges)
	{
		edges.push(curedge);
	}

	while (!edges.empty())
	{
		Edge outEdge = edges.top();
		edges.pop();
		vector<Node> n1 = (*IncludeMap.find(outEdge.from)).second;
		vector<Node> n2 = (*IncludeMap.find(outEdge.to)).second;
		//判断这条边是否会造成最小生成树成环
		if (!isCircle(n1,n2))
		{
			SetUnion(n1, n2);
			IncludeMap.insert(make_pair(outEdge.from, n1));
			IncludeMap.insert(make_pair(outEdge.to, n2));
			result.push_back(outEdge);
		}
	}
}
```









#### 2.Prim算法

首先选择一个点加入点集，之后选择点集所涉及的边中最小的边，此时解锁下一个节点，将其加入点集，再从点集中选择所涉及的边中最小的边，直至覆盖每一个顶点。

```c++
#include "Code05_Prim.h"
void Prim(Graph graph)
{
	//存储所选顶点的各个边
	priority_queue<Edge> priEdge;
	set<Node> SetNode;
	set<Edge> result;
	for (auto it = graph.nodes.begin(); it != graph.nodes.end(); it++)
	{
		//遍历每个节点，最终每个节点都有涉及的边进入结果
		Node cur = (*it).second;
		if(SetNode.find(cur) != SetNode.end())
		{
			//将解锁的node存入结果中
			SetNode.insert(cur);
			//将node所有的边放入优先级队列
			for (Edge curEdge : cur.edges)
			{
				priEdge.push(curEdge);
			}
			//寻找优先级队列中最小的边，但是其to不能包含在setNode中
			while (!priEdge.empty())
			{
				Edge curEdge = priEdge.top();
				priEdge.pop();
				Node next = curEdge.to;
				if (SetNode.find(next) != SetNode.end())
				{
					//将next加入setnode中
					SetNode.insert(next);
					//cur和node的这条边为选中的边
					result.insert(curEdge);
					for (Edge nextEdge : next.edges)
					{
						priEdge.push(nextEdge);
					}
				}
			}
		}
	}
}
```



#### 5.图中求单元最短路径(Dijkstra算法)

先记录出发点为当前距离出发点最近的点

2.记录当前最近的点到各个next点的距离，并此时计算next点到出发点的距离

3.寻找出除了已确定点外的此时距离出发点最近的点

4.确定该点距离

5.循环2-4，直至所有点的距离都确定完毕

```c++
void Dijkstra(Node head)
{
	//记录每个节点的距离初始点的距离
	map<Node, int> DistanceMap;
	//记录已经确定距离的点
	set<Node> SelectedNode;
	DistanceMap.insert(make_pair(head, 0));
	//获取所有未确定点中，此时距离初始点最短的点
	Node MinNode = getMinNode(DistanceMap, SelectedNode);
	while (MinNode.value != INT_MAX)
	{
		//记录当前到达MinNode点的距离
		int distance = (*DistanceMap.find(MinNode)).second;
		int Mindistance;
		Node next;
		//遍历每一个边，更新到达各个点的距离
		for (auto edge : MinNode.edges)
		{
			next = edge.to;
			//判断原距离列表中是否存在该点的距离
			if(DistanceMap.find(next)!= DistanceMap.end())
				DistanceMap.insert(make_pair(next, distance + edge.weight));
			//更新该点的距离
			Mindistance = min(distance + edge.weight, (*DistanceMap.find(next)).second);
			DistanceMap.insert(make_pair(next, Mindistance));
		}
		MinNode = getMinNode(DistanceMap, SelectedNode);
	}
}
```

















### 5.前缀树

  Trie树，即前缀树，又称单词查找树，字典树，是一种树形结构，是一种哈希树的变种。典型应用是用于统计和排序大量的字符串（但不仅限于字符串），所以经常被搜索引擎系统用于文本词频统计。

  Trie树的核心思想是空间换时间，利用字符串的公共前缀来降低查询时间的开销以达到提高效率的目的。 它的优点是：最大限度地减少无谓的字符串比较，查询效率比哈希表高。

根据一个例子来描述trie树的构建：
	**题目**：给定100000个长度不超过10的单词，判断每一个单词是否出现过，如果出现过，给出第一次出现的位置。
	**思路**：如果对每一个单词都遍历整个单词序列，那么时间复杂度就是O ( N^2 )，单词序列的长度是100000，显然这样的时间复杂度代价太高了。但是考虑100000个单词肯定有一些字符串的重复，trie树，即前缀树来解决这个问题最恰当不过了。一个前缀树的形式是什么样的呢？

![image-20220517222529243](https://s2.loli.net/2022/05/17/JSxnU2fCatL4lVB.png)





```c++
#pragma once
#include <iostream>
#include <string>
using namespace std;

class TrieNode
{
public:
	int pass;
	int end;
	TrieNode *next[26];
public:
	TrieNode(int p=0,int e=0):pass(p),end(e) {
		for (int i = 0; i < 26; i++)
		{
			next[i] = NULL;
		}
	}
	~TrieNode() {
		for (int i = 0; i < 26; i++)
		{
			delete next[i];
		}
		
	}
};

class TrieTree
{
private:
	TrieNode *root;
public:
	TrieTree()
	{
		root = new TrieNode();
	}
	void insert(string str);
	int search(string word);
	int prefixNumber(string pre);
	void deleteWord(string word);
};

//建立前缀树
inline void TrieTree::insert(string str)
{
	if (str == " ")
	{
		return;
	}
	//将当前节点设置为根节点
	TrieNode* head = root;
	head->pass++;
	int index = 0;
	for (size_t i = 0; i < str.size(); i++)
	{
		index = str[i] - 'a';
		if (head->next[index] == NULL)
		{
			head->next[index] = new TrieNode();
		}
		head = head->next[index];
		head->pass++;
	}
	head->end++;
}

//搜索字符串
inline int TrieTree::search(string word)
{
	TrieNode *node = this->root;
	for (size_t i = 0; i < word.size(); i++)
	{
		int index = word[i] - 'a';
		if (node->next[index] == NULL)
			return 0;
		node = node->next[index];
	}
	return node->end;
}

//寻找有多少个以pre为前缀的
inline int TrieTree::prefixNumber(string pre)
{
	TrieNode *node = this->root;
	for (size_t i = 0; i < pre.size(); i++)
	{
		int index = pre[i] - 'a';
		if (node->next[index] == NULL)
			return 0;
		node = node->next[index];
	}
	return node->pass;
}

void destory(TrieNode*root, const char*ch)
{
	if (root == NULL || ch == NULL)
	{
		return;
	}
	destory(root->next[*ch - 'a'], ++ch);
	delete root;
}

inline void TrieTree::deleteWord(string word)
{
	if (search(word) != 0)
	{
		TrieNode *node = root;
		node->pass--;
		const char* ch = word.c_str();
		for (size_t i = 0; i < word.size(); i++)
		{
			int index = *ch - 'a';
			if (--node->next[index]->pass == 0)
			{
				destory(node->next[index], ++ch);
			}
			node = node->next[index];
			//node->pass--;
			ch++;
		}
		//node->end--;
	}
}
```











## 6.贪心算法

贪婪算法(贪心算法)是指在对问题进行求解时，在每一步选择中都采取最好或者最优(即最有利)的选择，从而希望能够导致结果是最好或者最优的算法

算法所得到的结果不一定是最优的结果(有时候会是最优解)，但是都是相对近似(接近)最优解的结果

以上面的问题，若使用贪心算法求出的结果，有时候不一定是最优的结果，因为有可能成本问题不是最好的，但是它是相对接近最优解的





#### 例1

一块金条切成两半，是需要花费和长度数值一样的铜板的。比如长度为20的金条，不管切成长度多大的两半，都要花费20个铜板。 

一群人想整分整块金条，怎么分最省铜板? 

例如,给定数组{10,20,30}，代表一共三个人，整块金条长度为10+20+30=60。 金条要分成10,20,30三个部分。 如果先把长度60的金条分成10和50，花费60； 再把长度50的金条分成20和30，花费50；一共花费110铜板。 但是如果先把长度60的金条分成30和30，花费60；再把长度30金条分成10和20， 花费30；一共花费90铜板。 

输入一个数组，返回分割的最小代价。

**解**：

1）将数组中所有的数输入到一个小根堆中，

2）每次弹出两个元素，求和得到sum再弹入小根堆

3）重复步骤2，直至栈空

4）求和所有历史sum值，为所需要的最小花费

![image-20220518212024113](https://s2.loli.net/2022/05/18/zxTqmbvJRC6oduD.png)



```c++
int LessMoneySplitGold(int num[], int n)
{
	priority_queue<int,vector<int>,greater<int>> GoldQue;
	for (int i = 0; i < n; i++)
	{
		GoldQue.push(num[i]);
		
	}
	int cur = 0;
	int sum = 0;
	while (GoldQue.size()>1)
	{
		cur = GoldQue.top();
		GoldQue.pop();
		cur += GoldQue.top();
		GoldQue.pop();
		
		GoldQue.push(cur);
		sum += cur;
	}
	return sum;
}
```







#### 例2

一些项目要占用一个会议室宣讲，会议室不能同时容纳两个项目的宣讲。 给你每一个项目开始的时间和结束的时间(给你一个数 组，里面是一个个具体 的项目)，你来安排宣讲的日程，要求会议室进行的宣讲的场次最多。 返回这个最多的宣讲场次。

**解**：按照每个会议的结束时间排序

```c++
int BestArrange(vector<Program> programs)
{
	sort(programs.begin(), programs.end(), ProGramCom());
	int endtime=0;
	int n = 0;
	for (auto x:programs)
	{
		if (x.start >= endtime)
		{
			n++;
			endtime = x.end;
		}
	}
	return n;
}
```







#### 例3

输入： 

正数数组costs 

正数数组profits 

正数k 

正数m 

含义： 

costs[i]表示i号项目的花费 

profits[i]表示i号项目在扣除花费之后还能挣到的钱(利润) 

k表示你只能串行的最多做k个项目 

m表示你初始的资金 

说明： 你每做完一个项目，马上获得的收益，可以支持你去做下一个项目。 

输出： 你最后获得的最大钱数。



**解**：

1）利用小根堆来记录每个项目所需要的花费

2）利用大根堆来记录可以完成的项目的利润

从小根堆中弹出小于资金的项目进入大根堆，从大根堆中弹出此时利润最高的项目

循环直至大根堆中无项目或达到最大的k个串行项目

```c++
struct Project
{
public:
	int cost;
	int profit;
	Project(int cost,int profit):cost(cost),profit(profit){}
};

#include "Code05_IPO.h"

class MinCostCom
{
public:
	bool operator()(Project o1, Project o2)
	{
		return o1.cost < o2.cost;
	}
};

class MaxProfitCom
{
public:
	bool operator()(Project o1, Project o2)
	{
		return o1.profit > o2.profit;
	}
};

int IPO(vector<Project> projects, int k, int m)
{
	priority_queue<Project, vector<Project>, MinCostCom> MinCostQue;
	priority_queue<Project, vector<Project>, MaxProfitCom> MaxProfitQue;
	for (auto x : projects)
	{
		MinCostQue.push(x);
	}

	for (int i = 0; i < k; i++)
	{
		while (!MinCostQue.empty() && MinCostQue.top().cost <= m)
		{
			MaxProfitQue.push(MinCostQue.top());
			MinCostQue.top();
		}
		if (MaxProfitQue.empty())
		{
			return m;
		}
		m += MaxProfitQue.top().profit;
		MaxProfitQue.pop();
	}
	return m;

}
```













#### Leetcode

##### [763 划分字母区间](https://leetcode.cn/problems/partition-labels/)

字符串 `S` 由小写字母组成。我们要把这个字符串划分为尽可能多的片段，同一字母最多出现在一个片段中。返回一个表示每个字符串片段的长度的列表



**解**：1）遍历字符串，利用哈希表记录每个字符的最后出现的位置为end。

2）再次遍历字符串，记录当前字符片段的max_end=max(max_end,end),当遍历的i==max_end时，当前字符片段结束

```c++
vector<int> partitionLabels(string s) {
        map<char,int> endMap;
        vector<int> length;
        int start=0;
        int end=INT_MIN;
        for(int i=0;i<s.size();i++)
        {
            endMap[s[i]]=i;
        }
        for(int i=0;i<s.size();i++)
        {
            end=max(endMap[s[i]],end);
            if(i==end)
            {
                length.push_back(end-start+1);
                start=end+1;
            }
        }
        return length;
    }
```



##### [122 买卖股票最佳时机](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/)

给你一个整数数组 prices ，其中 prices[i] 表示某支股票第 i 天的价格。在每一天，你可以决定是否购买和/或出售股票。你在任何时候最多只能持有一股股票。你也可以先购买，然后在同一天出售。返回你能获得的最大利润 。

**解**：由于不限制交易次数，只要今天比昨天高就交易。

计算过程非实际交易过程，以[1,2,3,4]为例，4天持续上升，可以理解当天卖出，当天买入。

```c++
   int maxProfit(vector<int>& prices) {
        if(prices.size()<2)
            return 0;

        int res=0;
        for(int i=1;i<prices.size();i++)
        {
            int diff=prices[i]-prices[i-1];
            if(diff>0)
                res+=diff;
        }
        return res;
    }
```



##### [股票系列问题通解](https://leetcode.cn/circle/article/qiAgHn/)





##### [665 非递减序列](https://leetcode.cn/problems/non-decreasing-array/)

给你一个长度为 n 的整数数组 nums ，请你判断在最多改变 1 个元素的情况下，该数组能否变成一个非递减数列。

我们是这样定义一个非递减数列的： 对于数组中任意的 i (0 <= i <= n-2)，总满足 nums[i] <= nums[i + 1]。



**解**：采用贪心策略，每次需要看连续的三个元素，也就是瞻前顾后。若nums[i]<nums[i-1]，尽量缩小nums[i-1]，而不是扩大nums[i]，这样可以保证已经遍历过的得到的是非递减子序列

- 若nums[i-2]<=nums[i]，将nums[i-1]缩小至nums[i]
- 否则将nums[i]扩大至nums[i-1]

仅能修改一次

例外情况当i=1时，仅需将nums[0]=nums[1]

```c++
class Solution {
public:
    bool checkPossibility(vector<int>& nums) {
        int count=0;
        for(int i=1;i<nums.size();i++)
        {
            if(nums[i]<nums[i-1])
            {
                if(i==1)
                {
                    nums[i-1]=nums[i];
                }else if(nums[i-2]<=nums[i])
                {
                    nums[i-1]=nums[i];
                }else
                {
                    nums[i]=nums[i-1];
                }
                count++;
            }
        }
        return count<=1;
    }
};
```























## 7.暴力递归

暴力递归就是尝试 

1，把问题转化为规模缩小了的同类问题的子问题 

2，有明确的不需要继续进行递归的条件(base case) 

3，有当得到了子问题的结果之后的决策过程 

4，不记录每一个子问题的解







### 例1 汉诺塔问题

 打印n层汉诺塔从最左边移动到最右边的全部过程

**解：**1）将1~n-1层，从from移动到other(子问题)

2）将第n层，从from移动到to

3）将1~n-1层，从other移动到to（子问题）

最顶层，则直接从from移动到to

```c++
void process(int n,string start, string other, string end)
{
	if (n == 1)
		cout << "从" << start << "移动到" << end << endl;
	else {
		process(n - 1, start, end, other);
		cout << "从" << start << "移动到" << end << endl;
		process(n - 1, other, start, end);
	}
}

void Hanoi(int n)
{
	process(n, "左", "中", "右");
}
```









### 例2 打印字符串的全部子序列

打印一个字符串的全部子序列，包括空字符串



![在这里插入图片描述](https://s2.loli.net/2022/05/19/LVRoEu2tAIJTkgF.png)



```c++
//对每个字符进行要与不要两条路
//直至到最后一个字符，进行打印
void process(string str, int i,vector<char> &vec)
{
	if (i == str.size())
	{
		for (auto x : vec)
			cout << x;
		cout << endl;
	}
	else
	{
		vec.push_back(str[i]);
		process(str, i + 1, vec);

		vec.pop_back();
		process(str, i + 1, vec);
	}
	return;
}


void PrintAll(string str)
{
	vector<char> res;
	process(str, 0, res);
}

```









### 例3 打印一个字符串的全部排列

str[i...]范围上，i后面的所有字符都可以在i位置上

str[0...i-1]为之前确定的选择

到最后一个位置，将其加入到res中



```c++
#include "Code03_PrintAllPermutations.h"


void process(string str, int i,vector<string> &vec)
{
	if (i == str.size())
	{
		vec.push_back(str);
		return;
	}
	for (size_t j= i; j < str.size(); j++)
	{
		swap(str[i], str[j]);
		process(str, i + 1, vec);
		swap(str[i], str[j]);
	}
	return;
}

void process1(string str, int i, vector<string> &vec)
{
	if (i == str.size())
	{
		vec.push_back(str);
		return;
	}
	//记录当前位置，是否访问过
	bool visit[26] = { false };
	for (size_t j = i; j < str.size(); j++)
	{
		//若访问过则直接跳过
		if (!visit[str[j] - 'a'])
		{
			visit[str[j] - 'a'] = true;
			swap(str[i], str[j]);
			process1(str, i + 1, vec);
			swap(str[i], str[j]);
		}
		
	}
	return;
}

void PrintAllPermutations(string str)
{
	vector<string> vec;
	vector<string> vec1;
	ostream_iterator<string, char> out(cout, " ");
	
	process(str, 0, vec);
	cout << "未去重版本:";
	copy(vec.begin(), vec.end(), out);
	cout << endl;

	process1(str, 0, vec1);
	cout << "去重版本:";
	copy(vec1.begin(), vec1.end(), out);
	cout << endl;

}
```















### 例4 逆序栈

首先依次将栈底元素弹出

再利用递归栈，将栈底元素依次压入栈，从而达到逆序

```c++
//将栈底元素弹出
int GetLastandRemove(stack<int> &sta)
{
	int result = sta.top();
	sta.pop();
	if (sta.empty())
		return result;
	int last=GetLastandRemove(sta);
	sta.push(result);
	
	return last;
}
//反转栈
void ReverseStack(stack<int> &sta)
{
	if (sta.empty())
	{
		return;
	}
	int num = GetLastandRemove(sta);
	cout << num;
	ReverseStack(sta);
	sta.push(num);
}
```











### 例6

规定1和A对应、2和B对应、3和C对应... 那么一个数字字符串比如"111"，就可以转化为"AAA"、"KA"和"AK"。 给定一个只有数字字符组成的字符串str，返回有多少种转化结果。

**解**：1~26对应A~Z，

i之前的位置已经确定

判断i有多少种转换结果

```
int ConvertToLetterString(string str, int i)
{
	if (i == str.size())
	{
		return 1;
	}

	int res = 0;
	if (str[i] == '1')
	{
		res = ConvertToLetterString(str, i + 1);
		if (str[i] == '1' && (i + 1) < str.size())
			res += ConvertToLetterString(str, i + 2);
		return res;
	}

	if (str[i] == '2')
	{
		res = ConvertToLetterString(str, i + 1);
		if (str[i] == '2' && (i + 1) < str.size() && str[i + 1] < 7)
			res += ConvertToLetterString(str, i + 2);
		return res;
	}

	return ConvertToLetterString(str, i + 1);
		

}

```





### 例7 01背包问题

给定两个长度都为N的数组weights和values，weights[i]和values[i]分别代表 i号物品的重量和价值。给定一个正数bag，表示一个载重bag的袋子，你装的物 品不能超过这个重量。返回你能装下最多的价值是多少？

**解**：

返回要i号货物和不要i号货物更优的那个选择，对每个货物都进行判断

```c++
int process(int weights[], int values[], int n, int i, int alreadyweight, int bag)
{
	if (i == n)
	{
		return 0;
	}	

	if (alreadyweight <= bag)
	{
		if (alreadyweight + weights[i] > bag)
		{
			return process(weights, values, n, i + 1, alreadyweight, bag);
		}
		else
		{
			return max(process(weights, values, n, i + 1, alreadyweight, bag),
				values[i] + process(weights, values, n, i + 1, alreadyweight + weights[i], bag));
		}
	}
	else 
	{
		return 0;
	}
	
}

int Knapsack(int weights[], int values[], int n, int bag)
{
	return process(weights, values, n, 0, 0, bag);
}
```











### 例8 抽纸牌

​	给定一个整型数组arr，代表数值不同的纸牌排成一条线。玩家A和玩家B依次拿走每张纸 牌，规定玩家A先拿，玩家B后拿，但是每个玩家每次只能拿走最左或最右的纸牌，玩家A 和玩家B都绝顶聪明。请返回最后获胜者的分数。

解：

```c++
//定义函数f[i][j]表示arr[i...j]被绝顶聪明的人先拿得到的分数。
//       i==j时，就一张牌，直接返回arr[i]；否则该人只能拿arr[i]或arr[j]：
//       拿arr[i],剩下的arr[i+1...j]；拿arr[j],剩下的arr[i...j-1]，对于(j-i)张牌为先手，当先手摸了两侧的牌后，此时先手就变为后手，所以函数应该返回max(arr[i]+它作为后手的分数s[i+1][j], arr[j]+s[i][j-1])

//定义函数s[i][j]表示arr[i...j]被绝顶聪明的人后拿得到的分数。
//       i==j时，先拿的拿走，后拿的没有，返回0；否则先拿的人可能拿走arr[i]或arr[j]，此时对于（j-i）张牌来说他是后手，但是对于(j-i-1)牌来说他是先手，所以应返回此时他作为先手得到的最低分。所以函数返回min(f[i+1][j],f[i][j-1])
```

```c++
int f(int arr[], int i, int j)
{
	if (i == j)
		return arr[i];
	return max(arr[i] + s(arr, i + 1, j), arr[j] + s(arr, i, j - 1));
}

int s(int arr[], int i, int j)
{
	if (i == j)
		return 0;
	return min(f(arr, i + 1, j), f(arr, i, j - 1));
}


int win(int arr[], int n)
{
	return max(f(arr, 0, n - 1), s(arr, 0, n - 1));
}
```















## 其他



### 二分查找

​	首先，假设表中元素是按升序排列，将表中间位置记录的[关键字](https://baike.baidu.com/item/关键字)与查找关键字比较，如果两者相等，则查找成功；否则利用中间位置[记录](https://baike.baidu.com/item/记录/1837758)将表分成前、后两个子表，如果中间位置记录的关键字大于查找关键字，则进一步查找前一子表，否则进一步查找后一子表。重复以上过程，直到找到满足条件的[记录](https://baike.baidu.com/item/记录/1837758)，使查找成功，或直到子表不存在为止，此时查找不成功。

比较次数：
$$
a<\log_2n<b
$$

```c++
//在一个有序数组中，找某个数是否存在
bool BSExist(int SortArr[], int size, int num)
{
	int first = 0, last = size, medim;
	while (last > first)
	{
		medim = (first + last) >> 1;
		if (SortArr[medim] < num)
		{
			first = medim + 1;
		}
		else if (SortArr[medim] > num)
		{
			last = medim - 1;
		}
		else
			return true;
	}
	return false;
}
```



在一个有序数组中，找>=某个数最左侧的位置

```c++
int BSNearleft(int SortArr[], int size, int num)
{
	int medim, left = 0, right = size;
	int index = -1;
	while (right > left)
	{
		medim = (left + right) >> 1;
		if (SortArr[medim] >= num)
		{
			index = medim;
			right = medim - 1;
		}
		else
		{
			left = medim + 1;
		}
	}
	return index;
}
```









### 异或运算

1）0^N == N      N^N == 0 

2）异或运算满足交换律和结合率 

3）不用额外变量交换两个数



例：一个数组中有一种数出现了奇数次，其他数都出现了偶数次，怎么找到这一个数

```c++
int EvenTimesOddTimes(int arr[], int size)
{
	int Result = 0;
	for (int  i = 0; i < size; i++)
	{
		Result ^= arr[i];
	}
	return Result;
}
```

例：一个数组中有两种数出现了奇数次，其他数都出现了偶数次，怎么找到这两个数

```c++
int* EvenTimesOddTimes2(int arr[], int size)
{
	int Result = 0;
	int eor = 0, eor1 = 0;
	for (int i = 0; i < size; i++)
	{
		eor ^= arr[i];
	}
	//取eor最右侧的1
	int right = eor & (~eor + 1);

	for (int i = 0; i < size; i++)
	{
		if(right&arr[i])
			eor1 ^= arr[i];
	}
	eor ^= eor1;

	int arr1[] = { eor,eor1 };
	return arr1;
}
```









### Master公式

​	在编程中，递归是非常常见的一种算法，由于代码简洁而应用广泛，但递归相比顺序执行或循环程序，时间复杂度难以计算，而master公式就是用于计算递归程序的时间复杂度。
$$
T(N)=a*T(\frac{N}{b})+O(N^d)
$$
a：子过程的计算次数

N/b：子过程的样本量

O(N^d)：子结果合并的时间复杂度

N：母问题的样本量



满足如上公式的程序都可以根据master公式计算时间复杂度：

- log(b，a) > d ：时间复杂度为O(N^log(b，a))
- log(b，a) = d ：时间复杂度为O(N^d * logN)
- log(b，a) < d ：时间复杂度为O(N^d)



例：递归寻找数组中的最大值

```c++
int GetMax(int arr[],int l,int r)
{
	if (r == l)
		return arr[l];
	int medim = (l + r) >> 1;
	int leftMax=GetMax(arr, l, medim);
	int RightMax=GetMax(arr, medim+1, r);
	return leftMax > RightMax ? leftMax : RightMax;
}
```

a=2，b=2，O(N^d)=O(1)，T(N)=O(N)
$$
T(N)=2*T(\frac{N}{2})+O(1)=O(N^{\log_22})=O(N)
$$
