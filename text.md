using System;
using System.Collections.Generic;

class Program
{
    static Dictionary<ConsoleKey, int[]> octaves = new Dictionary<ConsoleKey, int[]>()
    {
        { ConsoleKey.F1, new int[] { 200, 300, 400 } },
        { ConsoleKey.F2, new int[] { 500, 600, 700 } },
        { ConsoleKey.F3, new int[] { 800, 900, 1000 } }
    };

    static int[] octava;

    static void Main(string[] args)
    {
        octava = octaves[ConsoleKey.F1];
        Console.WriteLine("Пианино");

        while (true)
        {
            ConsoleKeyInfo keyInfo = Console.ReadKey(true);

            switch (keyInfo.Key)
            {
                case ConsoleKey.F1:
                case ConsoleKey.F2:
                case ConsoleKey.F3:
                    ChangeOctave(keyInfo.Key);
                    break;
                default:
                    igrat();
                    break;
            }
        }
    }

    static void ChangeOctave(ConsoleKey octaveKey)
    {
        octava = octaves[octaveKey];
        Console.WriteLine($"Переключение на октаву {octaveKey}");
    }

    static void igrat()
    {
        Console.Beep(octava[0], 500);
        Console.Beep(octava[1], 500);
        Console.Beep(octava[2], 500);
    }
}
