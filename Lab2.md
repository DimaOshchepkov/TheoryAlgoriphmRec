## Лабораторная работа 9.2. Анализ рекурсивных алгоритмов. Сортировка слиянием, сортировка Хоара, бинарный поиск

###### 1) Выполнить сравнительный анализ сортировки слиянием и сортировки Хоара.

Сортировка слиянием

```
MergeSort(arr, left, right):
    if left > right 
        return
    mid = (left+right)/2
    mergeSort(arr, left, mid)
    mergeSort(arr, mid+1, right) 
    merge(arr, left, mid, right)
end
```
```if left > right -> O(1)```
```mid = (left+right)/2 -> O(1)```
```mergeSort(arr, left, mid) -> T(n/2)```
```mergeSort(arr, mid+1, right) -> T(n/2)```
```merge(arr, left, mid, right) -> O(n)```


$$ T(n) = 2T(n/2) + O(n) $$

$ n^{log_2{2}} $ имеет такой же темп роста -> второй слуйчай теоремы ->
$$ T(n) = O(n*log_2{n})$$

Быстрая сортировка:
```
function QUICKSORT(ARRAY, START, END)			
    # base case size <= 1		
    if START >= END then					    	
        return						           
    end if							      
    PIVOTINDEX = PARTITION(ARRAY, START, END)	
    QUICKSORT(ARRAY, START, PIVOTINDEX – 1)		
    QUICKSORT(ARRAY, PIVOTINDEX + 1, END)	
end function						
```

```PIVOTINDEX = PARTITION(ARRAY, START, END) -> D(n)=O(n)``` 
```QUICKSORT(ARRAY, START, PIVOTINDEX – 1) -> T(n1)```
```QUICKSORT(ARRAY, PIVOTINDEX + 1, END) -> T(n2)```
Выход из рекурсии O(1)

$$ T(n) = T(n_1) + T(n_2) + O(n) $$

В худшем случае:
$$ T(n) = T(n - 1) + T(1) + O(n)$$
$$ T(n) = O(n^2) $$


###### 2) Выполнить анализ временной сложности рекурсивной реализации бинарного поиска.

```
int bisearch(int val, int* array, size_t min, size_t max)
{
    if ( max < min ) 
        return -1;
    size_t midpoint = ( min + max ) / 2;  
    if ( array[midpoint] > val ) 
        return bisearch(val, array, min, midpoint - 1 );
    if ( array[midpoint] < val ) 
        return bisearch(val, array, midpoint + 1, max);
    if ( val == array[midpoint] ) 
        return 0;
    return -1;
}
```

```return bisearch(val, array, min, midpoint - 1 ); -> T(n/2) || 0```
```return bisearch(val, array, midpoint + 1, max); -> T(n/2) || 0```
```if ( val == array[midpoint] ) -> O(1)```

$$ T(n) = T(n/2) + O(1) $$
По второй теореме
$$ T(n) = O(log_2{n}) $$

###### 3) Оценить временную сложность рекурсивного алгоритма двумя способами

```
Procedure Soch (i : Integer);
    Var k : Integer;
    Begin
        If i>n Then Print(a)
        Else For k:=1 To n Do
            Begin
                a[i]:=k;
                Soch(i+1);
            End;
    End;
```
```If i>n Then Print(a) -> O(print) || 0```
```Else For k:=1 To n Do -> O(n) || 0```
```a[i]:=k; -> O(n)```
```Soch(i+1); -> ```  $\sum_{1}^{n}T(i+1)$


$$ T(n) =  O(n)+ \sum_{1}^{n}T(i+1)$$

$$ T(n) =  O(n) +  \sum_{1}^{n}O(n+1)+ \sum_{1}^{n}\sum_{1}^{n}T(i+2)$$

$$ T(n) =  O(n) +  \sum_{1}^{n}O(n+1)+ \sum_{1}^{n}\sum_{1}^{n}O(n+2) + \sum_{1}^{n}\sum_{1}^{n}\sum_{1}^{n}T(i+3) $$

$$ T(n) =  O(n) +  \sum_{1}^{n}O(n+1)+ \sum_{1}^{n}\sum_{1}^{n}O(n+2) + \sum_{1}^{n}\sum_{1}^{n}\sum_{1}^{n}T(i+3) $$

$$ T(n) =  O(n) +  nO(n+1)+ n^{2}O(n+2) + n^3O(n+3) + ... n^{n-i}O(2n)$$

$$ T(n) = O(n^n) $$
