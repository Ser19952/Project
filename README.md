public class Main {
    public static void main(String[] args){
        Calculator calc = Calculator.instance.get();
        int a = calc.plus.apply(1, 2);              // (x, y) -> x + y  ответ а 3; метод apply() это скорее всего метод который вызывается от этих типов данных: BinaryOperator<Integer> plus в классе Calculator
        int b = calc.minus.apply(1, 1);             // (x, y) -> x - y ответ b 0; метод apply() это скорее всего метод который вызывается от этих типов данных: BinaryOperator<Integer> minus в классе Calculator
        try {
            int c = calc.devide.apply(a, b);        // a / b ответ с); метод apply() это  метод который вызывается от этих типов данных: BinaryOperator<Integer> devide в классе Calculator
            calc.println.accept(c);                 // Деление на ноль нельзя
        } catch (ArithmeticException exception) {
            System.out.println("Делить на ноль нельзя");
        }
    }
}



import java.util.function.*;

public class Calculator {

    static Supplier<Calculator> instance = Calculator::new;

    BinaryOperator<Integer> plus = (x, y) -> x + y;
    BinaryOperator<Integer> minus = (x, y) -> x - y;
    BinaryOperator<Integer> multiply = (x, y) -> x * y;
    BinaryOperator<Integer> devide = (x, y) -> x / y;

    UnaryOperator<Integer> pow = x -> x * x;
    UnaryOperator<Integer> abs = x -> x > 0 ? x : x * -1;  // x > 0, если ДА, то это x, если НЕТ, то это x * -1

    Predicate<Integer> isPositive = x -> x > 0;

    Consumer<Integer> println = System.out::println;
}