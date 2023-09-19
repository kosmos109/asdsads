using System;

class Calculator
{
    static void Main()
    {
        int operation = 0;

        do
        {
            Console.WriteLine("Выберите действие:");
            Console.WriteLine("1. Сложение");
            Console.WriteLine("2. Вычитание");
            Console.WriteLine("3. Умножение");
            Console.WriteLine("4. Деление");
            Console.WriteLine("5. Возведение в степень");
            Console.WriteLine("6. Квадратный корень");
            Console.WriteLine("7. Найти 1 процент");
            Console.WriteLine("8. Факториал");
            Console.WriteLine("9. Выход");

            string input = Console.ReadLine();
            if (!int.TryParse(input, out operation))
            {
                Console.WriteLine("Ошибка! Введите число от 1 до 9.");
                continue;
            }

            switch (operation)
            {
                case 1: // Сложение
                    Console.Write("Введите первое число: ");
                    double num1 = GetNumberFromInput();
                    Console.Write("Введите второе число: ");
                    double num2 = GetNumberFromInput();
                    double sum = num1 + num2;
                    Console.WriteLine("Сумма: " + sum);
                    break;

                case 2: // Вычитание
                    Console.Write("Введите первое число: ");
                    num1 = GetNumberFromInput();
                    Console.Write("Введите второе число: ");
                    num2 = GetNumberFromInput();
                    double difference = num1 - num2;
                    Console.WriteLine("Разность: " + difference);
                    break;

                case 3: // Умножение
                    Console.Write("Введите первое число: ");
                    num1 = GetNumberFromInput();
                    Console.Write("Введите второе число: ");
                    num2 = GetNumberFromInput();
                    double product = num1 * num2;
                    Console.WriteLine("Произведение: " + product);
                    break;

                case 4: // Деление
                    Console.Write("Введите первое число: ");
                    num1 = GetNumberFromInput();
                    Console.Write("Введите второе число: ");
                    num2 = GetNumberFromInput();
                    if (num2 == 0)
                    {
                        Console.WriteLine("Ошибка! Деление на 0 невозможно.");
                        break;
                    }
                    double quotient = num1 / num2;
                    Console.WriteLine("Частное: " + quotient);
                    break;

                case 5: // Возведение в степень
                    Console.Write("Введите число: ");
                    num1 = GetNumberFromInput();
                    Console.Write("Введите степень: ");
                    int power = GetIntegerFromInput();
                    double result = Math.Pow(num1, power);
                    Console.WriteLine("Результат: " + result);
                    break;

                case 6: // Квадратный корень
                    Console.Write("Введите число: ");
                    num1 = GetNumberFromInput();
                    if (num1 < 0)
                    {
                        Console.WriteLine("Ошибка! Извлечение корня из отрицательного числа невозможно.");
                        break;
                    }
                    double sqrt = Math.Sqrt(num1);
                    Console.WriteLine("Квадратный корень: " + sqrt);
                    break;

                case 7: // Найти 1 процент
                    Console.Write("Введите число: ");
                    num1 = GetNumberFromInput();
                    double percent = num1 / 100;
                    Console.WriteLine("1% от числа: " + percent);
                    break;
                case 8: // Факториал
                    Console.Write("Введите число: ");
                    num1 = GetIntegerFromInput();
                    long factorial = CalculateFactorial((int)num1);
                    Console.WriteLine("Факториал: " + factorial);
                    break;

                case 9: // Выход
                    Console.WriteLine("Программа завершена.");
                    break;

                default:
                    Console.WriteLine("Ошибка! Введите число от 1 до 9.");
                    break;
            }

        } while (operation != 9);
    }

    static double GetNumberFromInput()
    {
        double number;
        string input = Console.ReadLine();
        while (!double.TryParse(input, out number))
        {
            Console.WriteLine("Ошибка! Введите число.");
            input = Console.ReadLine();
        }
        return number;
    }

    static int GetIntegerFromInput()
    {
        int number;
        string input = Console.ReadLine();
        while (!int.TryParse(input, out number))
        {
            Console.WriteLine("Ошибка! Введите целое число.");
            input = Console.ReadLine();
        }
        return number;
    }

    static long CalculateFactorial(int n)
    {
        if (n == 0)
            return 1;

        long result = 1;
        for (int i = 2; i <= n; i++)
        {
            result *= i;
        }
        return result;
    }
}
