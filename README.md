using System;
internal class Program
{
    static void Line()
    {
        Console.WriteLine("-------------------------------");
    }
    static void DC()
    {
        Console.ForegroundColor = ConsoleColor.DarkCyan;
    }
    static void C()
    {
        Console.ForegroundColor = ConsoleColor.Cyan;
    }
    static void R()
    {
        Console.ForegroundColor = ConsoleColor.Red;
    }
    static void Test(ref int min, ref int max)
    {
        if (min > max)
        {
            int temp = min;
            min = max;
            max = temp;
        }
    }
    static void Main(string[] args)
    {
        DC();
        Random random = new Random();
        Console.Write("Введите диапазон здоровья у первого персонажа (минимальное значение): ");
        int healthMin1 = int.Parse(Console.ReadLine()!);
        Console.Write("Введите диапазон здоровья у первого персонажа (максимальное значение): ");
        int healthMax1 = int.Parse(Console.ReadLine()!);

        C();
        Console.Write("Введите диапазон урона у первого персонажа (минимальное значение): ");
        int minDamage1 = int.Parse(Console.ReadLine()!);
        Console.Write("Введите диапазон урона у первого персонажа (максимальное значение): ");
        int maxDamage1 = int.Parse(Console.ReadLine()!);

        Line();
        DC();
        Console.Write("Введите диапазон здоровья у второго персонажа (минимальное значение): ");
        int healthMin2 = int.Parse(Console.ReadLine()!);
        Console.Write("Введите диапазон здоровья у второго персонажа (максимальное значение): ");
        int healthMax2 = int.Parse(Console.ReadLine()!);

        C();
        Console.Write("Введите диапазон урона у второго персонажа (минимальное значение): ");
        int minDamage2 = int.Parse(Console.ReadLine()!);
        Console.Write("Введите диапазон урона у второго персонажа (максимальное значение): ");
        int maxDamage2 = int.Parse(Console.ReadLine()!);

        if (healthMin1 <= 0 || healthMax1 <= 0 || minDamage1 <= 0 || maxDamage1 <= 0 || healthMin2 <= 0 || healthMax2 <= 0 || minDamage2 <= 0 || maxDamage2 <= 0)
            throw new ArgumentException("\nЗначения не могут быть равны НУЛЮ или меньше, тогда игра сразу окончиться, попробуй ввести положительные числа");

        Test(ref healthMin1, ref healthMax1);

        Test(ref minDamage1, ref maxDamage1);

        Test(ref healthMin2, ref healthMax2);

        Test(ref minDamage2, ref maxDamage2);

        int health1 = random.Next(healthMin1, healthMax1 + 1);
        int health2 = random.Next(healthMin2, healthMax2 + 1);

        DC();
        Line();
        Console.WriteLine($"Первый гладиатор готов\n{health1} хп\n[{minDamage1} - {maxDamage1}] - диапазон урона");
        Line();

        C();
        Console.WriteLine($"Второй гладиатор готов\n{health2} хп\n[{minDamage2} - {maxDamage2}] - диапазон урона");
        Line();

        int quantity = 1;

        while (health1 > 0 && health2 > 0)
        {
            int damage1 = random.Next(minDamage1, maxDamage1 + 1);
            int damage2 = random.Next(minDamage2, maxDamage2 + 1);

            health1 -= damage2;
            health2 -= damage1;

            Thread.Sleep(3000);

            R();
            Console.WriteLine($"{quantity} столкновение");

            DC();

            Line();
            Thread.Sleep(3000);
            Console.WriteLine($"Первый гладиатор нанес {damage1} урона");

            Thread.Sleep(3000);
            C();
            Console.WriteLine($"Второй гладиатор отвечает он сносит {damage2} урона");
            Line();

            Thread.Sleep(3000);
            Console.WriteLine($"У первого {health1} хп");
            Console.WriteLine($"А у второго {health2} хп");
            Line();
            quantity++;
        }
        R();
        if (health1 <= 0 && health2 <= 0)
        {
            Console.WriteLine("Оба гладиатора погибли");
        }
        else if (health1 <= 0)
        {
            Console.WriteLine("Второй гладиатор одержал победу!");
        }
        else if (health2 <= 0)
        {
            Console.WriteLine("Первый гладиатор одержал победу!");
        }
        C();

        Console.ReadKey();
    }
}
