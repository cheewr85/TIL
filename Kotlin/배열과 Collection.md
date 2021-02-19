## 배열
### Array
- 배열이 필요한 이유
	- 그룹(모음집)이 필요할 때
```Kotlin
fun main(array: Array<String>){

    // 배열을 생성하는 방법(1)
    var number: Int = 10
    var group1 = arrayOf<Int>(1, 2, 3, 4, 5) // Int만 들어갈 수 있는 배열 생성
    println(group1 is Array)

    // 배열을 생성하는 방법(2)
    var number1 = 10
    var group2 = arrayOf(1,2,3.5,"Hello") // 위와 다르게 타입을 정해주지 않아도 여러가지 타입을 담을 수 있음

    // Index란
    // -> 순서(번째)
    // [1,2,3,4,5]
    // "0"부터 시작
    // index 0 -> 1, index 1 -> 2

    // 배열의 값을 꺼내는 방법(1)
    val test1 = group1.get(0) // .get 함수를 호출한 것임
    val test2 = group1.get(4)
    println(test1)
    println(test2)

    // 배열의 값을 꺼내는 방법(2)
    val test3 = group1[0]
    println(test3)

    // 배열의 값을 바꾸는 방법(1)
    group1.set(0, 100)
    println(group1[0])

    // 배열의 값을 바꾸는 방법(2)
    group1[0] = 200
    println(group1[0])
}
```

## 실습
```Kotlin
fun main(array: Array<String>){

    val array = arrayOf<Int>(1, 2, 3)

    // get, set
    val number = array.get(0)
    println(number)
    // val number1 = array.get(100) // 인덱스를 주의 해야함

    array.set(0,100)
    val number2 = array.get(0)
    println(number2)

    array.set(100, 100) // IndexOutOfBounds 에러뜸

    // Array의 Bounds
    // - 처음 만들때 결정됨

    // Array를 만드는 방법(3)
    val a1 = intArrayOf(1, 2, 3)
    val a2 = charArrayOf('b', 'c') // char -> '', string -> ""
    val a3 = doubleArrayOf(1.2, 100.345)
    val a4 = booleanArrayOf(true, false, true)

    // Array를 만드는 방법(4) -> lambda를 활용한 방법
    var a5 = Array(10, {0}) // {} -> lambda
    var a6 = Array(5, {1; 2; 3; 4; 5;})
}
```

## Collection
### list, set, map
```Kotlin
// List

fun main(args: Array<String>){

    // Immutable Collections
    // 아래의 Collection은 값을 변경할 수 없는 Collection임
    // List -> 중복을 허용함
    val numberList = listOf<Int>(1, 2, 3, 3)
    println(numberList)
    println(numberList.get(0))
    println(numberList[0])

    // Set
    // -> 중복을 허용하지 않음
    // -> 순서가 없음, get을 쓸 수 없음, 인덱스가 없음
    val numberSet = setOf<Int>(1,2,3,3,3)
    println()
    numberSet.forEach{ // numberSet 하나씩 출력함
        println(it)
    }

    // Map -> Key, value 방식으로 관리함
    val numberMap = mapOf<String, Int>("one" to 1, "two" to 2 )
    println()
    println(numberMap.get("one"))


    // Mutable Collection (변경가능)
    val mNumberList = mutableListOf<Int>(1,2,3)
    mNumberList.add(3,4) // 3번째 인덱스에 4추가
    println()
    println(mNumberList)

    val mNumberSet = mutableSetOf<Int>(1,2,3,4,4,4)
    mNumberSet.add(10)
    println(mNumberSet)

    val mNumberMap = mutableMapOf<String, Int>("one" to 1)
    mNumberMap.put("two",2)
    println(mNumberMap)
}
```

## 실습
```Kotlin
fun main(array: Array<String>){

    val a = mutableListOf<Int>(1, 2, 3)
    a.add(4) // 맨 뒤에 값을 넣어둠, 인덱스를 기준으로
    println(a)
    a.add(0,100) // 이미 값이 있을 경우 기존값을 우측으로 밀어서 해당 인덱스에 넣어둠
    println(a)
    a.set(0, 200) // set으로 해당 인덱스 값을 바꿈
    println(a)
    a.removeAt(1) // 해당 인덱스 값을 지움
    println(a)

    val b = mutableSetOf<Int>(1, 2, 3, 4)
    println()
    b.add(2) // 중복을 허용하지 않으므로 추가되지 않음, 순서가 없으므로 인덱스를 넣을 필요 없음
    println(b)
    b.remove(2) // 해당 값을 지워버림
    println(b)
    b.remove(100) // 에러는 나지 않음 그냥 실행은 됨
    println(b)

    val c = mutableMapOf<String, Int>("one" to 1)
    println()
    c.put("two", 2)
    println(c)
    c.replace("two",3) // 해당 키 값에 대응하는 value를 3으로 바꿔줌
    println(c)
    println(c.keys)
    println(c.values)
    c.clear() // 값을 다 지워버림
    println(c)
}
```