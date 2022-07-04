Задание 1.
====

![Снимок экрана от 2022-07-04 20-00-36](https://user-images.githubusercontent.com/60341565/177195952-c3c16a2f-a80b-4544-b0f7-71751d5e48d6.png)

Задание 2.
===

Ознакомился.

Задание 3.
===
1.

    package main

    import "fmt"

    func main() {
        fmt.Print("Введите кол-во метров: ")
        var input float64
        fmt.Scanf("%f", &input)
        output := input / 0.3048
        fmt.Println("Результат в футах: ", output)    
        }
        
2.

      package main

      import "fmt"
      import "sort"

      func GetMin (toSort []int)(minNum int) {
        sort.Ints(toSort)
        minNum = toSort[0]
        return
      }

      func main() {
        x := []int{48,96,86,68,57,82,63,70,37,34,83,27,19,97,9,17,}
        y := GetMin(x)
        fmt.Printf("Наименьшее число в списке: %v\n", y)
      }
      
3.

    package main

    import "fmt"

    func FilterList ()(devidedWithNoReminder []int) {
      for i := 1;  i <= 100; i ++ {
        if	i % 3 == 0 { 
          devidedWithNoReminder = append(devidedWithNoReminder, i)
        }
      }	
      return
    }

    func main() {
      toPrint := FilterList()
      fmt.Printf("Числа от 1 до 100, которые делятся на 3 без остатка: %v\n", toPrint)
    }
    
