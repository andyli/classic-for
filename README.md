Classic "for"
=============

A library that enables C-style `for` loops within Haxe.

Usage
-----

Installation:

    haxelib install classic-for

In project.xml (if using OpenFL):

    <haxelib name="classic-for" />

In build.hxml (if using pure Haxe):

    -lib classic-for

In Example.hx:

    @:build(ClassicFor.build())
    class Example {
        public static function add1To10():Int {
            var sum:Int = 0;
            
            @for(var i:Int = 1, i <= 10, i++) {
                sum += i;
            }
            
            return sum;
        }
    }

Alternately:

    class Example implements ClassicFor {
        public static function factorial(n:Int):Int {
            var total:Int = 1;
            
            @for(n > 1, n--) {
                total *= n;
            }
            
            return total;
        }
    }

Notes
-----

- Haxe does not allow semicolons between parentheses, so it is not possible to use the exact same syntax as C.
- If you provide exactly three loop arguments, the macro will treat the loop exactly like a `for` loop in C. Otherwise, it will be forced to guess what the arguments mean.
  - When guessing, the macro finds the first argument that is not an assignment operation or variable declaration. This will be considered the "loop condition."
  - Everything before the condition will be considered "initialization code," and everything afterwards will be considered "increment code."
  - If no condition is found, the loop will repeat endlessly. (Or until a `break` statement.)
