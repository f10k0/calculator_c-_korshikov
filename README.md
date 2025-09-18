



































using System;
using System.Text;
using System.Threading.Tasks;

namespace calculator
{
    class Program
    {
        static void Main(string[] args)
        {
            string value;
            do
            {
                long num1, num2;
                bool isValidNum1 = false;
                bool isValidNum2 = false;
                do
                {
                    Console.Write("Введите первое число (не более 5,000,000):");
                    if (long.TryParse(Console.ReadLine(), out num1))
                    {
                        if (Math.Abs(num1) <= 5000000)
                        {
                            isValidNum1 = true;
                        }
                        else
                        {
                            Console.WriteLine("Ошибка: Число не может превышать 5,000,000 по модулю!");
                        }
                    }
                    else
                    {
                        Console.WriteLine("Ошибка: Введите корректное число!");
                    }
                } while (!isValidNum1);

                do
                {
                    Console.Write("Введите второе число (не более 5,000,000):");
                    if (long.TryParse(Console.ReadLine(), out num2))
                    {
                        if (Math.Abs(num2) <= 5000000)
                        {
                            isValidNum2 = true;
                        }
                        else
                        {
                            Console.WriteLine("Ошибка: Число не может превышать 5,000,000 по модулю!");
                        }
                    }
                    else
                    {
                        Console.WriteLine("Ошибка: Введите корректное число!");
                    }
                } while (!isValidNum2);

                Console.Write("Введите операцию(/,+,-,*,%,^,sqrt):");
                string symbol = Console.ReadLine();

                switch (symbol)
                {
                    case "+":
                        try
                        {
                            checked
                            {
                                long sum = num1 + num2;
                                if (Math.Abs(sum) > 5000000)
                                {
                                    Console.WriteLine("Ошибка: Результат превышает 5,000,000!");
                                }
                                else
                                {
                                    Console.WriteLine("Сложение: " + sum);
                                }
                            }
                        }
                        catch (OverflowException)
                        {
                            Console.WriteLine("Ошибка: Результат слишком большой!");
                        }
                        break;

                    case "-":
                        try
                        {
                            checked
                            {
                                long diff = num1 - num2;
                                if (Math.Abs(diff) > 5000000)
                                {
                                    Console.WriteLine("Ошибка: Результат превышает 5,000,000!");
                                }
                                else
                                {
                                    Console.WriteLine("Вычитание: " + diff);
                                }
                            }
                        }
                        catch (OverflowException)
                        {
                            Console.WriteLine("Ошибка: Результат слишком большой!");
                        }
                        break;

                    case "*":
                        try
                        {
                            checked
                            {
                                long product = num1 * num2;
                                if (Math.Abs(product) > 5000000)
                                {
                                    Console.WriteLine("Ошибка: Результат превышает 5,000,000!");
                                }
                                else
                                {
                                    Console.WriteLine("Умножение: " + product);
                                }
                            }
                        }
                        catch (OverflowException)
                        {
                            Console.WriteLine("Ошибка: Результат слишком большой!");
                        }
                        break;

                    case "/":
                        if (num2 == 0)
                        {
                            Console.WriteLine("Ошибка: Деление на ноль запрещено!");
                        }
                        else
                        {
                            long quotient = num1 / num2;
                            if (Math.Abs(quotient) > 5000000)
                            {
                                Console.WriteLine("Ошибка: Результат превышает 5,000,000!");
                            }
                            else
                            {
                                Console.WriteLine("Деление: " + quotient);
                            }
                        }
                        break;

                    case "%":
                        if (num2 == 0)
                        {
                            Console.WriteLine("Ошибка: Деление на ноль запрещено!");
                        }
                        else
                        {
                            long remainder = num1 % num2;
                            if (Math.Abs(remainder) > 5000000)
                            {
                                Console.WriteLine("Ошибка: Результат превышает 5,000,000!");
                            }
                            else
                            {
                                Console.WriteLine("Остаток от деления: " + remainder);
                            }
                        }
                        break;

                    case "^":
                        if (num2 > 10000)
                        {
                            Console.WriteLine("Ошибка: Степень не может превышать 10,000!");
                        }
                        else if (num2 < 0)
                        {
                            Console.WriteLine("Ошибка: Отрицательные степени не поддерживаются!");
                        }
                        else
                        {
                            try
                            {
                                long powerResult = Power(num1, num2);
                                if (Math.Abs(powerResult) > 5000000)
                                {
                                    Console.WriteLine("Ошибка: Результат превышает 5,000,000!");
                                }
                                else
                                {
                                    Console.WriteLine("Возведение в степень: " + powerResult);
                                }
                            }
                            catch (OverflowException)
                            {
                                Console.WriteLine("Ошибка: Результат слишком большой!");
                            }
                        }
                        break;

                    case "sqrt":
                        if (num1 < 0)
                        {
                            Console.WriteLine("Ошибка: Нельзя извлекать корень из отрицательного числа!");
                        }
                        else
                        {
                            double sqrtResult = Math.Sqrt(num1);
                            if (sqrtResult > 5000000)
                            {
                                Console.WriteLine("Ошибка: Результат превышает 5,000,000!");
                            }
                            else
                            {
                                Console.WriteLine("Квадратный корень: " + sqrtResult);
                            }
                        }
                        break;

                    default:
                        Console.WriteLine("Неверный ввод операции");
                        break;
                }

                Console.Write("Хотите продолжить? (y/n):");
                value = Console.ReadLine();
            }
            while (value == "y" || value == "Y");
        }

        static long Power(long baseNum, long exponent)
        {
            if (exponent == 0) return 1;
            if (exponent == 1) return baseNum;

            long result = 1;
            for (long i = 0; i < exponent; i++)
            {
                checked
                {
                    result *= baseNum;
                }
            }
            return result;
        }
    }
}

