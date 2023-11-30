using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.IO;
using System.Linq;
using System.Text.Json;
using System.Threading;
using System.Threading.Tasks;

class User
{
    public string Name { get; set; }
    public int CharsPerMinute { get; set; }
    public int CharsPerSecond { get; set; }
}

static class RecordsTable
{
    private const string filePath = "records.json";
    private static List<User> users = new List<User>();

    public static void LoadRecords()
    {
        if (File.Exists(filePath))
        {
            string json = File.ReadAllText(filePath);
            users = JsonSerializer.Deserialize<List<User>>(json);
        }
    }

    public static void SaveRecords()
    {
        string json = JsonSerializer.Serialize(users);
        File.WriteAllText(filePath, json);
    }

    public static void AddRecord(User user)
    {
        users.Add(user);
        SaveRecords();
    }

    public static void DisplayRecords()
    {
        Console.WriteLine("\nТаблица рекордов:");

        foreach (var user in users)
        {
            Console.WriteLine($"{user.Name}: {user.CharsPerMinute} символов в минуту, {user.CharsPerSecond} символов в секунду");
        }
    }
}

class TypingTest
{
    private static string userName;

    private static readonly string testText = "В темном лесу, под густой листвой, спрятан дом. В доме темно, только светит луна сквозь окно.";

    private static int correctChars;
    private static int currentPosition;
    private static Stopwatch stopwatch;
    private static List<ConsoleColor> colors;

    public static void StartTest()
    {
        GetUserName();
        Console.Clear();

        Console.WriteLine($"Привет, {userName}! Напечатайте следующий текст:");
        Console.WriteLine(testText);

        currentPosition = 0;
        correctChars = 0;

        colors = Enumerable.Repeat(ConsoleColor.White, testText.Length).ToList();

        Console.WriteLine("Если готовы, нажмите Enter для начала теста.");
        Console.ReadLine(); // Ждем, пока пользователь нажмет Enter

        Console.Clear();

        stopwatch = Stopwatch.StartNew();

        do
        {
            UpdateInputText();
            UpdateTimer();

            Thread.Sleep(10); // Добавим короткую задержку для снижения нагрузки на процессор
        } while (currentPosition < testText.Length && stopwatch.Elapsed.TotalSeconds < 60);

        stopwatch.Stop();

        Console.WriteLine(); // Переход на новую строку после таймера
        Console.WriteLine($"Тест завершен, {userName}! Вы напечатали {correctChars} символов верно.");

        double elapsedTime = stopwatch.Elapsed.TotalMinutes;

        int charsPerMinute = (int)(correctChars / elapsedTime);
        int charsPerSecond = (int)(correctChars / elapsedTime / 60);

        Console.WriteLine($"Ваш результат: {charsPerMinute} символов в минуту, {charsPerSecond} символов в секунду.");

        RecordsTable.DisplayRecords();
        RecordsTable.AddRecord(new User { Name = userName, CharsPerMinute = charsPerMinute, CharsPerSecond = charsPerSecond });
    }

    private static void GetUserName()
    {
        Console.Write("Введите свое имя: ");
        userName = Console.ReadLine();
    }

    private static void UpdateInputText()
    {
        Console.SetCursorPosition(0, 2); // Перемещаемся в строку, где начинается текст

        for (int i = 0; i < testText.Length; i++)
        {
            Console.ForegroundColor = colors[i];
            Console.Write(testText[i]);
        }

        Console.SetCursorPosition(correctChars, 2); // Возвращаемся на текущую позицию

        ConsoleKeyInfo key = Console.ReadKey(true);
        if (key.Key != ConsoleKey.Enter)
        {
            if (key.KeyChar == testText[correctChars])
            {
                colors[correctChars] = ConsoleColor.Blue;
                correctChars++;
            }
            currentPosition++;
        }
    }

    private static void UpdateTimer()
    {
        TimeSpan remainingTime = TimeSpan.FromSeconds(60) - stopwatch.Elapsed;
        Console.SetCursorPosition(0, 4); // Позиция для таймера
        Console.WriteLine($"Таймер: {remainingTime.TotalSeconds} сек");

        if (remainingTime.TotalSeconds <= 0)
        {
            EndTest();
        }
    }

    private static void EndTest()
    {
        Console.Clear();
        Console.WriteLine("Тест завершен по таймеру.");
        DisplayResults();
        Environment.Exit(0);
    }

    private static void DisplayResults()
    {
        Console.WriteLine(); // Переход на новую строку после таймера
        Console.WriteLine($"Тест завершен, {userName}! Вы напечатали {correctChars} символов верно.");

        double elapsedTime = stopwatch.Elapsed.TotalMinutes;

        int charsPerMinute = (int)(correctChars / elapsedTime);
        int charsPerSecond = (int)(correctChars / elapsedTime / 60);

        Console.WriteLine($"Ваш результат: {charsPerMinute} символов в минуту, {charsPerSecond} символов в секунду.");
    }
}

class Program
{
    static void Main()
    {
        RecordsTable.LoadRecords();
        TypingTest.StartTest();
    }
}
