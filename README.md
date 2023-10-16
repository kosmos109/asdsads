using System;
using System.Collections.Generic;

namespace DailyPlanner
{
    class Program
    {
        static List<Note> notes;
        static int currentNoteIndex;

        static void Main(string[] args)
        {

            notes = new List<Note>();
            notes.Add(new Note("Заметка 1", "Описание 1", new DateTime(2022, 1, 6)));
            notes.Add(new Note("Заметка 2", "Описание 2", new DateTime(2022, 1, 8)));
            notes.Add(new Note("Заметка 3", "Описание 3", new DateTime(2022, 1, 13)));

            currentNoteIndex = 0;

            while (true)
            {
                Console.Clear();
                PrintMenu();
                var key = Console.ReadKey();
                Console.Clear();

                switch (key.Key)
                {
                    case ConsoleKey.LeftArrow:
                        SwitchNoteLeft();
                        break;
                    case ConsoleKey.RightArrow:
                        SwitchNoteRight();
                        break;
                    case ConsoleKey.Enter:
                        ShowNoteDetails();
                        break;
                }
            }
        }

        static void PrintMenu()
        {
            var currentNote = notes[currentNoteIndex];
            Console.WriteLine("----- Ежедневник -----");
            Console.WriteLine();
            Console.WriteLine("Дата: " + currentNote.Date.ToShortDateString());
            Console.WriteLine();

            foreach (var note in notes)
            {
                Console.WriteLine(note.Title);
            }
        }

        static void SwitchNoteLeft()
        {
            currentNoteIndex--;
            if (currentNoteIndex < 0)
                currentNoteIndex = notes.Count - 1;
        }

        static void SwitchNoteRight()
        {
            currentNoteIndex++;
            if (currentNoteIndex >= notes.Count)
                currentNoteIndex = 0;
        }

        static void ShowNoteDetails()
        {
            var currentNote = notes[currentNoteIndex];
            Console.WriteLine("----- Детали заметки -----");
            Console.WriteLine();
            Console.WriteLine("Название: " + currentNote.Title);
            Console.WriteLine("Описание: " + currentNote.Description);
            Console.WriteLine("Дата: " + currentNote.Date.ToLongDateString());
            Console.WriteLine("Выполнить к: " + currentNote.DueDate.ToLongDateString());
            Console.WriteLine();
            Console.WriteLine("Нажмите Enter для продолжения...");
            Console.ReadLine();
        }
    }

    class Note
    {
        public string Title { get; set; }
        public string Description { get; set; }
        public DateTime Date { get; set; }
        public DateTime DueDate { get; set; }

        public Note(string title, string description, DateTime date)
        {
            Title = title;
            Description = description;
            Date = date;
            DueDate = date;
        }
    }
}
