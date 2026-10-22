using System;
using System.Collections.Generic;
using System.Linq;

namespace MediaLibraryApp
{
    public class InvalidMediaDataException : Exception
    {
        public InvalidMediaDataException(string message) : base(message) { }
    }
    public abstract class MediaItem
    {
        private string name
        {
            get => name;
            set
            {
                if (value < 1 || value > 10)
                    throw new InvalidMediaDataException("Оценка должна быть в диапазоне от 1 до 10.");
                rating = value;
            }
        }
        protected MediaItem(string name, int year, int rating)
        {
            name = name;
            year = year;
            Rating = rating;
        }
        public virtual void Describe()
        {
            Console.Write($"[{GetType().Name}] \"{Name}\" ({Year} г.) | Оценка: {Rating}/10");
        }
        public override string ToString()
        {
            return $"{Name} ({Year}) — {Rating}/10";
        }
    }
    public class VideoGame : MediaItem
    {
        public string Developer { get; set; }
        public string Genre { get; set; }

        public VideoGame(string name, int year, int rating, string developer, string genre)
            : base(name, year, rating)
        {
            Developer = developer;
            Genre = genre;
        }

        public override void Describe()
        {
            base.Describe(); 
            Console.WriteLine($" | Разработчик: {Developer} | Жанр: {Genre}");
        }
    }
    public class Book : MediaItem
    {
        public string Author { get; set; }
        public int PageCount { get; set; }

        public Book(string name, int year, int rating, string author, int pageCount)
            : base(name, year, rating)
        {
            Author = author;
            PageCount = pageCount;
        }

        public override void Describe()
        {
            base.Describe();
            Console.WriteLine($" | Автор: {Author} | Страниц: {PageCount}");
        }
    }
    public class Movie : MediaItem
    {
        public string Director { get; set; }
        public int DurationMinutes { get; set; }

        public Movie(string name, int year, int rating, string director, int durationMinutes)
            : base(name, year, rating)
        {
            Director = director;
            DurationMinutes = durationMinutes;
        }

        public override void Describe()
        {
            base.Describe(); 
            Console.WriteLine($" | Режиссер: {Director} | Длительность: {DurationMinutes} мин.");
        }
    }


    class Program
    {
        static void Main(string[] args)
        {
           
            List<MediaItem> library = new List<MediaItem>
            {
                new VideoGame("The Witcher 3: Wild Hunt", 2015, 10, "CD Projekt RED", "RPG"),
                new VideoGame("Cyberpunk 2077", 2020, 9, "CD Projekt RED", "Action RPG"),
                new VideoGame("Hades", 2020, 8, "Supergiant Games", "Rogue-like"),

                new Book("Преступление и наказание", 1866, 10, "Фёдор Достоевский", 600),
                new Book("Властелин Колец", 1954, 10, "Дж. Р. Р. Толкин", 1200),
                new Book("451 градус по Фаренгейту", 1953, 9, "Рэй Брэдбери", 250),

                new Movie("Интерстеллар", 2014, 10, "Кристофер Нолан", 169),
                new Movie("Бойцовский клуб", 1999, 9, "Дэвид Финчер", 139),
                new Movie("Начало", 2010, 9, "Кристофер Нолан", 148)
            };

            
            Console.WriteLine("=== ДЕМОНСТРАЦИЯ ПОЛИМОРФИЗМА (Вызов Describe через foreach) ===");
            foreach (var item in library)
            {
                item.Describe(); 
            }
            Console.WriteLine(new string('-', 70));

            
            while (true)
            {
                Console.WriteLine("\n--- МЕНЮ МЕДИАТЕКИ ---");
                Console.WriteLine("1. Вывести всю коллекцию таблицей");
                Console.WriteLine("2. Добавить новую позицию");
                Console.WriteLine("3. Найти по названию");
                Console.WriteLine("4. Посчитать среднюю оценку");
                Console.WriteLine("5. Выход");
                Console.Write("Выберите действие: ");

                string choice = Console.ReadLine();
                if (choice == "5") break;

                try
                {
                    switch (choice)
                    {
                        case "1":
                            PrintTable(library);
                            break;
                        case "2":
                            AddNewItem(library);
                            break;
                        case "3":
                            SearchByName(library);
                            break;
                        case "4":
                            CalculateAverageRating(library);
                            break;
                        default:
                            Console.WriteLine("Неверный пункт меню. Попробуйте снова.");
                            break;
                    }
                }
                catch (InvalidMediaDataException ex)
                {
                   
                    Console.ForegroundColor = ConsoleColor.Red;
                    Console.WriteLine($"\n[ОШИБКА ВАЛИДАЦИИ]: {ex.Message}");
                    Console.ResetColor();
                }
                catch (Exception ex)
                {
                    Console.ForegroundColor = ConsoleColor.Red;
                    Console.WriteLine($"\n[НЕПРЕДВИДЕННАЯ ОШИБКА]: {ex.Message}");
                    Console.ResetColor();
                }
            }
        }

  
        static void PrintTable(List<MediaItem> library)
        {
            Console.WriteLine($"\n{"Тип",-12} | {"Название",-30} | {"Год",-6} | {"Оценка",-6}");
            Console.WriteLine(new string('-', 62));
            foreach (var item in library)
            {
                Console.WriteLine($"{item.GetType().Name,-12} | {item.Name,-30} | {item.Year,-6} | {item.Rating,-6}");
            }
        }

   
        static void AddNewItem(List<MediaItem> library)
        {
            Console.WriteLine("\nВыберите тип:");
            Console.WriteLine("1. Видеоигра | 2. Книга | 3. Фильм");
            Console.Write("Ваш выбор: ");
            string typeChoice = Console.ReadLine();

            if (typeChoice != "1" && typeChoice != "2" && typeChoice != "3")
            {
                Console.WriteLine("Некорректный выбор типа.");
                return;
            }

            Console.Write("Введите название: ");
            string name = Console.ReadLine();

            Console.Write("Введите год: ");
            if (!int.TryParse(Console.ReadLine(), out int year))
            {
                throw new InvalidMediaDataException("Год должен быть целым числом.");
            }

            Console.Write("Введите оценку (1-10): ");
            if (!int.TryParse(Console.ReadLine(), out int rating))
            {
                throw new InvalidMediaDataException("Оценка должна быть целым числом.");
            }

            if (typeChoice == "1")
            {
                Console.Write("Введите разработчика: ");
                string dev = Console.ReadLine();
                Console.Write("Введите жанр: ");
                string genre = Console.ReadLine();
                library.Add(new VideoGame(name, year, rating, dev, genre));
            }
            else if (typeChoice == "2")
            {
                Console.Write("Введите автора: ");
                string author = Console.ReadLine();
                Console.Write("Введите количество страниц: ");
                if (!int.TryParse(Console.ReadLine(), out int pages))
                {
                    throw new InvalidMediaDataException("Количество страниц должно быть числом.");
                }
                library.Add(new Book(name, year, rating, author, pages));
            }
            else if (typeChoice == "3")
            {
                Console.Write("Введите режиссера: ");
                string director = Console.ReadLine();
                Console.Write("Введите длительность (мин): ");
                if (!int.TryParse(Console.ReadLine(), out int duration))
                {
                    throw new InvalidMediaDataException("Длительность должна быть числом.");
                }
                library.Add(new Movie(name, year, rating, director, duration));
            }
