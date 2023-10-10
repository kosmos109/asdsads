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

    static int[] currentOctave;

    static void Main(string[] args)
    {
        currentOctave = octaves[ConsoleKey.F1]; 
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
                    PlaySound();
                    break;
            }
        }
    }

    static void ChangeOctave(ConsoleKey octaveKey)
    {
        currentOctave = octaves[octaveKey];
        Console.WriteLine($"Переключение на октаву {octaveKey}");
    }

    static void PlaySound()
    {
        Console.Beep(currentOctave[0], 500);
        Console.Beep(currentOctave[1], 500);
        Console.Beep(currentOctave[2], 500);
    }
}
