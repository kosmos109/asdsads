using System;
using System.Collections.Generic;

class Program
{
    static List<Note> notes = new List<Note>
    {
        new Note { Title = "Проснуться (по желанию)", Description = "Поехать в мпт (также, по желанию)", Date = new DateTime(2023, 10, 10) },
        new Note { Title = "Сходить в зал (обязательно)", Description= "Надо пить протеин, а мышцы сами вырастут", Date = new DateTime(2023, 10,11) },
        new Note { Title = "Сделать д/з (нет)", Description = "Лучше в зал", Date = new DateTime(2023, 10, 12) },
        new Note { Title = "Выучить c#", Description = "Выучить c# и придумать новый", Date = new DateTime(2023, 10, 13) },
        new Note { Title = "Поесть (обязательно)", Description = "Рис и курица", Date = new DateTime(2023, 10, 14) }
    };

    static int currentNoteIndex = 0;

    static void Main()
    {
        Console.CursorVisible = false;

        while (true)
        {
            Console.Clear();
            ShowMenu();
            HandleInput();
        }
    }

    static void ShowMenu()
    {
        Console.WriteLine("Ежедневник");
        Console.WriteLine("-----------");

        for (int i = 0; i < notes.Count; i++)
        {
            if (i == currentNoteIndex)
            {
                Console.Write("--->");
            }
            else
            {
                Console.Write("   ");
            }
            Console.WriteLine($"{notes[i].Date.ToShortDateString()} - {notes[i].Title}");
        }

        Console.WriteLine("'добавить' для новой заметки, или 'удалить' для удаления,'редактировать' для редактирования");
        Console.WriteLine("Нажмите enter, чтобы увидеть информацию о заметке");
        Console.WriteLine("Используйте стрелки для навигации.");
    }

    static void ShowDetails()
    {
        Console.Clear();
        Console.WriteLine("Подробная информация");
        Console.WriteLine("--------------------");
        Console.WriteLine($"Дата: {notes[currentNoteIndex].Date.ToShortDateString()}");
        Console.WriteLine($"Название: {notes[currentNoteIndex].Title}");
        Console.WriteLine($"Описание: {notes[currentNoteIndex].Description}");
        Console.WriteLine("Нажмите enter для возврата к списку");
        Console.ReadLine();
    }

    static void AddNote()
    {
        Console.Write("Введите название новой заметки: ");
        string title = Console.ReadLine();
        Console.Write("Введите описание новой заметки: ");
        string description = Console.ReadLine();
        Console.Write("Введите дату (гггг-мм-дд) новой заметки: ");
        DateTime date = DateTime.Parse(Console.ReadLine());
        notes.Add(new Note { Title = title, Description = description, Date = date });
    }

    static void EditNote()
    {
        Console.Write("Введите новое название: ");
        notes[currentNoteIndex].Title = Console.ReadLine();
        Console.Write("Введите новое описание: ");
        notes[currentNoteIndex].Description = Console.ReadLine();
        Console.Write("Введите новую дату (гггг-мм-дд): ");
        notes[currentNoteIndex].Date = DateTime.Parse(Console.ReadLine());
    }

    static void DeleteNote()
    {
        notes.RemoveAt(currentNoteIndex);
        if (currentNoteIndex >= notes.Count)
        {
            currentNoteIndex--;
        }
    }

    static void HandleInput()
    {
        ConsoleKeyInfo key = Console.ReadKey(true);

        if (key.Key == ConsoleKey.RightArrow)
        {
            if (currentNoteIndex < notes.Count - 1)
            {
                currentNoteIndex++;
            }
        }
        else if (key.Key == ConsoleKey.LeftArrow)
        {
            if (currentNoteIndex > 0)
            {
                currentNoteIndex--;
            }
        }
        else if (key.Key == ConsoleKey.Enter)
        {
            ShowDetails();
        }
        else
        {
            string input = Console.ReadLine().ToLower();

            switch (input)
            {
                case "добавить":
                    AddNote();
                    break;
                case "редактировать":
                    EditNote();
                    break;
                case "удалить":
                    DeleteNote();
                    break;
                default:
                    if (int.TryParse(input, out int selectedIndex) && selectedIndex > 0 && selectedIndex <= notes.Count)
                    {
                        currentNoteIndex = selectedIndex - 1;
                    }
                    else
                    {
                        Console.WriteLine("Неверный ввод.");
                        Console.ReadLine();
                    }
                    break;
            }
        }
    }

    class Note
    {
        public string Title { get; set; }
        public string Description { get; set; }
        public DateTime Date { get; set; }
    }
}
