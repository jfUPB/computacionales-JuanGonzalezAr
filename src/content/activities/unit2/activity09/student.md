```c#
using System;
using System.Threading;

class Program
{
    static void Main()
    {
        Console.WriteLine("Mantén presionada una tecla para dibujar. Suéltala para borrar. Presiona ESC para salir.");

        while (true)
        {
            if (Console.KeyAvailable) 
            {
                var tecla = Console.ReadKey(true); 

                if (tecla.Key == ConsoleKey.Escape) 

                Console.WriteLine("############"); 
                Thread.Sleep(50); // Pequeña pausa
            }
            else 
            {
                if (Console.CursorTop > 1) 
                {
                    Console.SetCursorPosition(0, Console.CursorTop - 1);
                    Console.Write("            "); ¿
                    Console.SetCursorPosition(0, Console.CursorTop);
                }

                Thread.Sleep(50); 
            }
        }
    }
}

```
