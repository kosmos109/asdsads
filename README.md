using System;
using System.Collections.Generic;

public class Note
{
    public string zametka { get; set; }
    public string opis { get; set; }
    public DateTime Date { get; set; }
    public DateTime DueDate { get; set; }
}

public class nachalo
{
    private List<Note> notes;
    private int currentIndex;

    public nachalo()
    {
        notes = new List<Note>();
        // даты
        notes.Add(new Note { zametka = "Заметка 1", opis = "Прийти на пары (по желанию)", Date = new DateTime(2023, 10, 17), DueDate = new DateTime(2023, 10, 17) });
        notes.Add(new Note { zametka = "Заметка 2", opis = "Поесть (обязательно)", Date = new DateTime(2023, 10, 19), DueDate = new DateTime(2023, 10, 19) });
        notes.Add(new Note { zametka = "Заметка 3", opis = "Поспать (100 процентов обязательно)", Date = new DateTime(2023, 10, 21), DueDate = new DateTime(2023, 10, 21) });

        currentIndex = 0;
    }
    public void Startuy() // основа
    {
        Console.CursorVisible = false;

        while (true)
        {
            Console.Clear();
            Menushkaa();
            Detailsss();

            var key = Console.ReadKey(true).Key;

            switch (key)
            {
                case ConsoleKey.LeftArrow:
                    if (currentIndex > 0)
                        currentIndex--;
                    break;
                case ConsoleKey.RightArrow:
                    if (currentIndex < notes.Count - 1)
                        currentIndex++;
                    break;
                case ConsoleKey.Enter:
                    opendet();
                    Console.ReadKey();
                    break;
                case ConsoleKey.Escape:
                    return;
            }
        }
    }

    private void Menushkaa() // основа 2
    {
        Console.WriteLine("--------------Мой ежедневник--------------\n");

        for (int i = 0; i < notes.Count; i++)
        {
            if (i == currentIndex)
                Console.Write("--->");
            else
                Console.Write("  ");

            Console.WriteLine(notes[i].zametka);
        }

        Console.WriteLine("\n Cтрелки (<- и ->) влеов и вправо для переключения;");
        Console.WriteLine("\n Enter, чтобы посмотреть заметку");
        Console.WriteLine("\n И Escape с целью выйти из прекрасного кода");
        Console.WriteLine("\n Кстати, заметки написаны еще и снизу");
        Console.WriteLine("\n ↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓");
    }

    private void Detailsss() //
    {
        Console.WriteLine($"\n\nДата: {notes[currentIndex].Date.ToShortDateString()}");
        Console.WriteLine($"Срок выполнения: {notes[currentIndex].DueDate.ToShortDateString()}");
        Console.WriteLine($"Описание: {notes[currentIndex].opis}");
    }

    private void opendet() // не забудь
    {
        Console.Clear();
        Console.WriteLine($"\n{notes[currentIndex].zametka}\n");
        Console.WriteLine($"Дата: {notes[currentIndex].Date.ToShortDateString()}");
        Console.WriteLine($"Срок выполнения: {notes[currentIndex].DueDate.ToShortDateString()}");
        Console.WriteLine($"Описание: {notes[currentIndex].opis}");
    }
}

 

class Program
{
    static void Main(string[] args)
    {
        nachalo planner = new nachalo();
        planner.Startuy();
    }
}
