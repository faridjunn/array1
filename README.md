# Array - Множество
Объект **Array**, как и массивы в других языках программирования, позволяет хранить набор из нескольких элементов под одним именем переменной и имеет члены для выполнения общих операций с массивами .

## Описание
В JavaScript массивы не являются примитивами , а представляют собой Arrayобъекты со следующими основными характеристиками:
-  **Массивы JavaScript могут изменять размер и могут содержать смесь различных** типов данных . (Если эти характеристики нежелательны, используйте вместо них типизированные массивы .)
- **Массивы JavaScript не являются ассоциативными массивами** , поэтому к элементам массива нельзя получить доступ, используя произвольные строки в качестве индексов, но к ним нужно обращаться, используя неотрицательные целые числа (или их соответствующую строковую форму) в качестве индексов.
- **Массивы JavaScript имеют** нулевой индекс : первый элемент массива находится в индексе 0, второй 1— в индексе и т. д., а последний элемент — в значении свойства массива  *length* минус 1.
- Операции копирования массива **в JavaScript создают** поверхностные копии . (Все стандартные встроенные операции копирования с любыми объектами JavaScript создают поверхностные копии, а не глубокие ).
- 

## Связь между длиной и числовыми свойствами

Свойство массива JavaScript *length* и числовые свойства связаны.

Некоторые из встроенных методов массива (например, *join(), slice(), indexOf()* и т. д.) учитывают значение *length* свойства массива при вызове.

Другие методы (например, *push(), splice(),* и т. д.) также приводят к обновлению свойства массива *length*.

- const fruits = [];
fruits.push("banana", "apple", "peach");
console.log(fruits.length); // 3

 
При установке свойства в массиве JavaScript, когда свойство является допустимым индексом массива, и этот индекс находится за пределами текущих границ массива, движок *length* соответствующим образом обновит свойство массива:

- fruits[5] = "mango";
console.log(fruits[5]); // 'mango'
console.log(Object.keys(fruits)); // ['0', '1', '2', '5']
console.log(fruits.length); // 6

###### Увеличение *length*.

- fruits.length = 10;
console.log(fruits); // ['banana', 'apple', 'peach', empty x 2, 'mango', empty x 4]
console.log(Object.keys(fruits)); // ['0', '1', '2', '5']
console.log(fruits.length); // 10
console.log(fruits[8]); // undefined

*length* Однако уменьшение свойства приводит к удалению элементов.

- fruits.length = 2;
console.log(Object.keys(fruits)); // ['0', '1']
console.log(fruits.length); // 2

Это объясняется далее на [*Array/length*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/length) странице.


#   Методы массива и пустые слоты

Пустые слоты в [разреженных массивах](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Indexed_collections#sparse_arrays) ведут себя непоследовательно между методами массива. Как правило, старые методы пропускают пустые слоты, а новые обрабатывают их как файлы *undefined*.

Среди методов, которые перебирают несколько элементов, следующие выполняют проверку **in** перед доступом к индексу и не объединяют пустые слоты с *undefined*:

-  concat()
-  copyWithin()
-  every()
-  filter()
-  flat()
-  flatMap()
-  forEach()
-  indexOf()
-  lastIndexOf()
-  map()
-  reduce()
-  reduceRight()
-  reverse()
-  slice()
-  some()
-  sort()
-  splice()

Как именно они обрабатывают пустые слоты, см. на странице каждого метода.

Эти методы обрабатывают пустые слоты так, как если бы они были undefined:
- entries()
- fill()
- find()
- findIndex()
- findLast()
- findLastIndex()
- group() Экспериментальный
- groupToMap() Экспериментальный
- includes()
- join()
- keys()
- toLocaleString()
- values()
- 
![The San Juan Mountains are beautiful!](/array/arrray.jpg "hello")

1. Мутирующий метод                 
copyWithin()                          
fill()                              	
pop()                                	
push(v1, v2)                         	
reverse()                            
shift()                             	
sort()                              	
splice()                            	
unshift(v1, v2)                         
2. 	Немутирующая альтернатива
	Нет альтернативы одному методу
Нет альтернативы одному методу 
slice(0, -1)
concat([v1, v2])
  	toReversed()
slice(1)
toSorted()
toSpliced()
toSpliced(0, 0, v1, v2)


Простой способ превратить мутирующий метод в немутирующий альтернативный — использовать синтаксис распространения или slice()сначала создать копию:

- arr.copyWithin(0, 1, 2); // mutates arr
const arr2 = arr.slice().copyWithin(0, 1, 2); // does not mutate arr
const arr3 = [...arr].copyWithin(0, 1, 2); // does not mutate arr

 # Итерационные методы
Многие методы массива принимают функцию обратного вызова в качестве аргумента. Функция обратного вызова вызывается последовательно и не более одного раза для каждого элемента массива, а возвращаемое значение функции обратного вызова используется для определения возвращаемого значения метода. Все они имеют одну и ту же подпись:
- method(callbackFn, thisArg)

Где *callbackFn* принимает три аргумента:

**element**
Текущий обрабатываемый элемент в массиве.

**index**
Индекс текущего обрабатываемого элемента в массиве.

**array**
Массив, к которому был вызван метод.

Ожидаемый результат *callbackFn* зависит от вызываемого метода массива.

В частности, **[every()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every), [find()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find), [findIndex()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex),[ findLast()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findLast), [findLastIndex()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findLastIndex)** и **[some()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some)**  не всегда вызываются *callbackFn* для каждого элемента — они останавливают итерацию, как только определяется возвращаемое значение.

Есть два других метода, которые берут функцию обратного вызова и запускают ее не более одного раза для каждого элемента массива, но они имеют немного отличающиеся сигнатуры от типичных итерационных методов (например, они не принимают ) *thisArg*:

- [reduce()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)
- [reduceRight()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduceRight)

Метод **[sort()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)** также принимает функцию обратного вызова, но это не итеративный метод. Он изменяет массив на месте, не принимает *thisArg* и может вызывать обратный вызов несколько раз для индекса.
