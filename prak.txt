using System;

class Program
{
    static void Main(string[] args)
    {
        int choice;
        double num1, num2;
        bool validChoice;
        string input;

        do
        {
            Console.WriteLine("Выберите действие:");
            Console.WriteLine("1. Сложить 2 числа");
            Console.WriteLine("2. Вычесть первое из второго");
            Console.WriteLine("3. Перемножить два числа");
            Console.WriteLine("4. Разделить первое на второе");
            Console.WriteLine("5. Возвести в степень N первое число");
            Console.WriteLine("6. Найти квадратный корень из числа");
            Console.WriteLine("7. Найти 1 процент от числа");
            Console.WriteLine("8. Найти факториал из числа");
            Console.WriteLine("9. Выйти из программы");

            validChoice = false;

            do
            {
                Console.Write("Введите номер операции (1-9): ");
                input = Console.ReadLine();

                if (int.TryParse(input, out choice))
                {
                    if (choice >= 1 && choice <= 9)
                    {
                        validChoice = true;
                    }
                    else
                    {
                        Console.WriteLine("Некорректный ввод! Пожалуйста, введите число от 1 до 9.");
                    }
                }
                else
                {
                    Console.WriteLine("Некорректный ввод! Пожалуйста, введите число от 1 до 9.");
                }

            } while (!validChoice);


            switch (choice)
            {
                case 1:
                    Console.Write("Введите первое число: ");
                    num1 = GetValidNumber();
                    Console.Write("Введите второе число: ");
                    num2 = GetValidNumber();
                    Console.WriteLine($"Результат: {num1 + num2}");
                    break;
                case 2:
                    Console.Write("Введите первое число: ");
                    num1 = GetValidNumber();
                    Console.Write("Введите второе число: ");
                    num2 = GetValidNumber();
                    Console.WriteLine($"Результат: {num2 - num1}");
                    break;
                case 3:
                    Console.Write("Введите первое число: ");
                    num1 = GetValidNumber();
                    Console.Write("Введите второе число: ");
                    num2 = GetValidNumber();
                    Console.WriteLine($"Результат: {num1 * num2}");
                    break;
                case 4:
                    Console.Write("Введите первое число: ");
                    num1 = GetValidNumber();
                    Console.Write("Введите второе число: ");
                    num2 = GetValidNumber();
                    if (num2 != 0)
                    {
                        Console.WriteLine($"Результат: {num1 / num2}");
                    }
                    else
                    {
                        Console.WriteLine("Деление на ноль недопустимо!");
                    }
                    break;
                case 5:
                    Console.Write("Введите число: ");
                    num1 = GetValidNumber();
                    Console.Write("Введите степень: ");
                    int power = GetValidInt();
                    Console.WriteLine($"Результат: {Math.Pow(num1, power)}");
                    break;
                case 6:
                    Console.Write("Введите число: ");
                    num1 = GetValidNumber();
                    if (num1 >= 0)
                    {
                        Console.WriteLine($"Результат: {Math.Sqrt(num1)}");
                    }
                    else
                    {
                        Console.WriteLine("Невозможно извлечь квадратный корень из отрицательного числа!");
                    }
                    break;
                case 7:
                    Console.Write("Введите число: ");
                    num1 = GetValidNumber();
                    Console.WriteLine($"Результат: {num1 * 0.01}");
                    break;
                case 8:
                    Console.Write("Введите число: ");
                    num1 = GetValidInt();
                    Console.WriteLine($"Результат: {Factorial(num1)}");
                    break;
                case 9:
                    Console.WriteLine("Программа завершена.");
                    break;
            }

            Console.WriteLine();

        } while (choice != 9);
    }

    static double GetValidNumber()
    {
        double num;
        bool validInput;
        string input;

        do
        {
            input = Console.ReadLine();
            validInput = double.TryParse(input, out num);

            if (!validInput)
            {
                Console.WriteLine("Некорректный ввод! Пожалуйста, введите число.");
            }

        } while (!validInput);

        return num;
    }

    static int GetValidInt()
    {
        int num;
        bool validInput;
        string input;

        do
        {
            input = Console.ReadLine();
            validInput = int.TryParse(input, out num);

            if (!validInput)
            {
                Console.WriteLine("Некорректный ввод! Пожалуйста, введите целое число.");
            }

        } while (!validInput);

        return num;
    }

    static double Factorial(double num)
    {
        if (num == 0)
        {
            return 1;
        }
        else
        {
            return num * Factorial(num - 1);
        }
    }
}

