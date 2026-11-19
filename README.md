# Dart OOP Assignment: Kigali Bus Card

**Name:** Jamad Nzikou Miere  
**Student ID:** 27165  

## My numbers
D = 65  
L = 5  
Starting balance = 1650 RWF  
Bus fare = 265 RWF  
Student discount = 15%  

## Output of main.dart
```text
Error: name too short
Owner: Ama | Balance: 1650 RWF
Owner: Jamad Nzikou Miere | Balance: 1650 RWF
Error: top-up must be 500 to 50000 RWF
Topped up 2000 RWF
Paid 265 RWF
Paid 265 RWF
Owner: Jamad Nzikou Miere | Balance: 3120 RWF
Student discount: 39 RWF
Paid 226 RWF
Owner: Jamad Nzikou Miere | Balance: 1424 RWF
Student card: 15% off
```

## Part 1: Why no setter for balance?
A public setter for `_balance` would allow any part of the program to directly overwrite the card's balance (for example, `card.balance = 999999` or setting a negative balance) without paying or following validation rules. By keeping `_balance` private and only modifying it through `topUp()` and `pay()`, the card ensures money is only added within valid limits (500–50,000 RWF) and only deducted when there are sufficient funds.

## Part 2: What does ~/ do?
The `~/` operator performs **integer division** (truncating division). It divides two numbers and discards the decimal remainder, returning a whole `int`.
* `print(237 * 17 / 100);` prints `40.29` (a `double` with decimals).
* `print(237 * 17 ~/ 100);` prints `40` (an `int` with the `.29` dropped).

## Part 4: Bug table

| Bug | The line | Why it is wrong (your words) | Your fix |
| :--- | :--- | :--- | :--- |
| 1 | `String _brand;` and `int _battery;` | Non-nullable fields in Dart must be initialized with a starting value when declared (or marked `late`). | Changed them to `String _brand = '';` and `int _battery = 0;`. |
| 2 | `SmartPhone (String brand, int battery, String system) {` | The child constructor does not pass `brand` and `battery` to the parent `Phone` constructor using `super`. | Added `: super(brand, battery)` to the constructor header. |
| 3 | `_system = system;` | The field declared in `SmartPhone` is named `system` (without an underscore), so `_system` does not exist. | Renamed the field declaration to `String _system = '';`. |
| 4 | `@override void restart() {` | `@override` tells Dart to replace a method from the parent class, but `Phone` does not have a `restart()` method. | Removed the `@override` annotation. |
| 5 | `print(p.battery());` (and missing setter) | `battery` is a getter, not a regular method, so calling it with `()` causes an error. Also, `p.battery = 100;` needs a setter in `Phone`. | Changed to `print(p.battery);` and added `set battery(int value)` accepting `0` to `100`. |
| Not a bug | `Phone p = new Phone ('Tecno', 50);` | In Dart, the `new` keyword is optional when creating an object—writing it is old-style syntax, not an error. | (none) |

## Part 5
My prediction:  
The program will print:
```text
1
5
```

Why:
1. `Bag a = Bag();` starts with `_items = 0`. `a.add();` increases `_items` by 1 (to `1`). `a.items = -5;` calls the setter, which ignores `-5` because it is not `>= 0`. So `print(a.items);` prints `1`.
2. `BigBag b = BigBag();` starts with `_items = 0`. `BigBag`'s `add()` calls `super.add()` twice, adding 2 items per call. Calling `b.add();` twice adds `2 + 2 = 4` items. Then `b.items = b.items + 1;` sets `_items` to `4 + 1 = 5`. So `print(b.items);` prints `5`.

Real output:
```text
1
5
```

Was I right?  
Yes, my prediction matched the real output completely.