- [مقدمه](#%D9%85%D9%82%D8%AF%D9%85%D9%87)

- [باکس دوم](#%باکس-دوم)

## مقدمه

متن معمولی - لطفا برا وارد کردن عنوان‌ها و منو از کارکتر‌های عددی در ابتدای متن و پرانتز و # و کارکترهای خاص استفاده نکنید.

برای وارد کردن آیتم‌های بولتی از این می‌توانید استفاده کنید:

- آیتم اول

- آیتم دوم

- آیتم سوم

<br/>

ایجاد باکس کد با لینک سوئگر‌: 

``` python

import random

min = 1

max = 6

roll_again = "yes"

while roll_again == "yes" or roll_again == "y":

    print "Rolling the dices..."

    print "The values are...."

    print random.randint(min, max)

    print random.randint(min, max)

    roll_again = raw_input("Roll the dices again?")

```


<div class="swaggerLink">http://yourlink</div>

<div class="box-end">

</div>

## باکس دوم

ایجاد تب با دو آیتم : 

<div class="tab-start">

</div>

# [C#](#tab/csharp)

``` csharp

// custom type

public class User : IComparable

{

  // ...

  // implement IComparable interface

  public int CompareTo(object obj)

  {

    if (obj is User) {

      return this.Name.CompareTo((obj as User).Name);  // compare user names

    }

    throw new ArgumentException("Object is not a User");

  }

}

```


<div class="swaggerLink">http://yourlink</div>

# [javascript](#tab/javascript')

``` javascript

var address=  

{  

    company:"Javatpoint",  

    city:"Noida",  

    state:"UP",  

    fullAddress:function()  

        {  

            return this.company+" "+this.city+" "+this.state;  

        }  

};  

var fetch=address.fullAddress();  

document.writeln(fetch);  

```


<div class="swaggerLink">http://yourlink</div>

<div class="tab-end">

</div>

شما می توانید به نمونه کدها از طریق لینک زیر دسترسی داشته باشید:

[دانلود نمونه کد](https://github.com/podiumir/samples/tree/master/src/csharp/Plan)

<div class="box-end">

</div>
