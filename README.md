using System;
using System.Collections.Generic;

class Note
{
    public string Title { get; set; }
    public string Description { get; set; }
    public DateTime Date { get; set; }

    public Note(string title, string description, DateTime date)
    {
        Title = title;
        Description = description;
        Date = date;
    }
}

class DailyPlanner
{
    private List<Note> notes = new List<Note>();
    private int currentIndex = 0;

    public DailyPlanner()
    {
        // Инициализация примерами заметок
        notes.Add(new Note("Заметка 1", "Поесть (обязательно)", new DateTime(2023, 10, 12)));
        notes.Add(new Note("Заметка 2", "Выучить с#", new DateTime(2023, 10, 13)));
        notes.Add(new Note("Заметка 3", "Сделать 20 подтягиваний (по желанию)", new DateTime(2023, 10, 14)));
        notes.Add(new Note("Заметка 4", "Поспать (если вы не студент)", new DateTime(2023, 10, 15)));
        notes.Add(new Note("Заметка 5", "Создать свой личный c# (обязательно)", new DateTime(2023, 10, 16)));
    }

    public void StartPlanner()
    {
        bool isRunning = true;
        while (isRunning)
        {
            Console.Clear();
            PrintNotes();
            Console.WriteLine("Используйте стрелки (лево) ← → (вправо) для переключения между заметками. Нажмите Enter для подробной информации.");
            Console.WriteLine("Для редактирования текущей заметки нажмите Q. Для добавления новой заметки нажмите W. Нажмите Escape для выхода.");
            var key = Console.ReadKey(true).Key;
            switch (key)
            {
                case ConsoleKey.LeftArrow:
                    MoveToPreviousNote();
                    break;
                case ConsoleKey.RightArrow:
                    MoveToNextNote();
                    break;
                case ConsoleKey.Enter:
                    ShowDetailedNote();
                    break;
                case ConsoleKey.Q:
                    EditNote();
                    break;
                case ConsoleKey.W:
                    AddNewNote();
                    break;
                case ConsoleKey.Escape:
                    isRunning = false;
                    break;
            }
        }
    }

    private void PrintNotes()
    {
        for (int i = 0; i < notes.Count; i++)
        {
            if (i == currentIndex)
            {
                Console.BackgroundColor = ConsoleColor.Gray;
                Console.ForegroundColor = ConsoleColor.Black;
            }

            Console.Write($"[{notes[i].Date.ToShortDateString()}] {notes[i].Title}    ");

            if (i == currentIndex)
            {
                Console.ResetColor();
            }
        }
        Console.WriteLine();
    }

    private void ShowDetailedNote()
    {
        Console.Clear();
        Console.WriteLine($"Название: {notes[currentIndex].Title}");
        Console.WriteLine($"Дата: {notes[currentIndex].Date.ToShortDateString()}");
        Console.WriteLine($"Описание: {notes[currentIndex].Description}");
        Console.WriteLine("Нажмите Escape для возврата к списку заметок.");
        while (Console.ReadKey(true).Key != ConsoleKey.Escape) { }
    }

    private void MoveToPreviousNote()
    {
        if (currentIndex > 0)
        {
            currentIndex--;
        }
        else
        {
            currentIndex = notes.Count - 1;
        }
    }

    private void MoveToNextNote()
    {
        if (currentIndex < notes.Count - 1)
        {
            currentIndex++;
        }
        else
        {
            currentIndex = 0;
        }
    }

    private void EditNote()
    {
        Console.Clear();
        Console.WriteLine("Введите новое название:");
        string newTitle = Console.ReadLine();
        Console.WriteLine("Введите новое описание:");
        string newDescription = Console.ReadLine();
        notes[currentIndex].Title = newTitle;
        notes[currentIndex].Description = newDescription;
        Console.WriteLine("Заметка успешно отредактирована. Нажмите любую клавишу для продолжения.");
        Console.ReadKey(true);
    }
    private void AddNewNote()
    {
        Console.Clear();
        Console.WriteLine("Введите название новой заметки:");
        string newTitle = Console.ReadLine();
        Console.WriteLine("Введите описание новой заметки:");
        string newDescription = Console.ReadLine();
        Console.WriteLine("Введите дату новой заметки (гггг-мм-дд):");
        DateTime newDate;
        while (!DateTime.TryParse(Console.ReadLine(), out newDate))
        {
            Console.WriteLine("Некорректный формат даты. Пожалуйста, введите дату в формате (гггг-мм-дд):");
        }
        notes.Add(new Note(newTitle, newDescription, newDate));
        Console.WriteLine("Новая заметка успешно добавлена. Нажмите любую клавишу для продолжения.");
        Console.ReadKey(true);
    }
}

class Program
{
    static void Main(string[] args)
    {
        DailyPlanner planner = new DailyPlanner();
        planner.StartPlanner();
    }
}
