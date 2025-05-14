```c#
using System;
using System.Threading;

class Program
{
    static void Main()
    {
        const int screenHeight = 16; 
        bool keyPressed = false;

        Console.WriteLine("Mantén presionada una tecla para dibujar. Suéltala para borrar. Presiona ESC para salir.");

        while (true)
        {
            if (Console.KeyAvailable) 
            {
                var key = Console.ReadKey(true);

                if (key.Key == ConsoleKey.Escape) 
                    break;

                keyPressed = true;
            }
            else
            {
                keyPressed = false;
            }

            Console.Clear(); 

            if (keyPressed)
            {
                for (int i = 0; i < screenHeight; i++)
                {
                    Console.WriteLine("################"); 
                }
            }

            Thread.Sleep(50); 
        }
    }
}


```
