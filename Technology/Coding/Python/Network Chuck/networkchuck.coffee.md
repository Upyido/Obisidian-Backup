
## v 1
```
#NetworkChuck.Coffee


print("Hello, Welcome to NetworkChuck.coffee!!!!!!!!!!!\n")

name = input("what is your name?\n")

print("hello " + name + ", thank you so much for coming in today!\n\n")

menu = "Black Coffee, Esspresso, latte, cappucino"

print(name + ", what would you like to order from our menu today? We are serving\n" + menu + "\n" )

order = input()

price = 8

quantity = input("Sounds good! How many would you like?\n")

total = price * int(quantity)

print("Outstanding! You're total will be $" + str(total) + ", we will have that right out for you")
```


## V 2
```
#CozyCove.Coffee

  

#def hello(to="Hello, Welcome to CozyCove.coffee!!!!!!!!!!!\n")

#````print("hello,", to)

#````

  

#Request Name

print("Hello, Welcome to CozyCove.coffee!!!!!!!!!!!\n")

#hello()

name = input("what is your name?\n").strip().title()

  

#splitting name - need to ignore if not enough values

first, last = name.split(" ")

  

print(f"hello {first}, Cthank you so much for coming in today!\n\n")

  

#Request order

menu = "Black Coffee, Esspreso, Latte, Cappucino"

  

print(f"{first}, what would you like to order from our menu today? We are serving\n" + menu + "\n" )

  

order = input().strip().capitalize()

price = 8

  

#Request amount to be purchased

quantity = input("Sounds good! How many would you like?\n")

  

total = price * int(quantity)

  

print("\n Outstanding! You're total will be $" + str(total) + ", we will have that right out for you")
```