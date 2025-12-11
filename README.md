using System;
using System.Collections.Generic;

namespace DocumentRenderingSystem
{
    public abstract class Document
    {
        public string Author { get; protected set; }
        
        public Document(string author)
        {
            Author = author;
        }
        
        public abstract void Render();
    }

    public class TextDocument : Document
    {
        public string Content { get; private set; }
        
        public TextDocument(string author, string content) : base(author)
        {
            Content = content;
        }
        
        public override void Render()
        {
            Console.WriteLine("---");
            Console.WriteLine($"[Текст] Автор: {Author}");
            Console.WriteLine($"Содержимое: {Content}");
            Console.WriteLine();
        }
    }

    public class ImageDocument : Document
    {
        public string Resolution { get; private set; }
        
        public ImageDocument(string author, string resolution) : base(author)
        {
            Resolution = resolution;
        }
        
        public override void Render()
        {
            Console.WriteLine("---");
            Console.WriteLine($"[Изображение] Автор: {Author}");
            Console.WriteLine($"Рендеринг изображения с разрешением {Resolution}");
            Console.WriteLine();
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("### — Рендеринг документов —");
            Console.WriteLine("Начинаю рендеринг...\n");

            List<Document> documents = new List<Document>();
            
            documents.Add(new TextDocument("Лев Толстой", 
                "Все счастливые семьи похожи друг на друга..."));
            
            documents.Add(new ImageDocument("Иван Шишкин", "3558x2180"));
            
            documents.Add(new TextDocument("Михаил Булгаков", 
                "В белом плаще с кровавым подбоем..."));

            foreach (Document doc in documents)
            {
                doc.Render();
            }
            
            Console.WriteLine("Рендеринг завершен!");
            Console.ReadKey();
        }
    }
}
