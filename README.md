using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;

namespace ConsoleApp21
{
    public class Program
    {
        public static void Main(string[] args)

        {
            int firstPlayerPadSize = 5;
            int secondPlayerPadSize = 5;
            bool ballDirectionUp = true; // Определяет, если направление мяча вверх
            bool ballDirectionRight = false; 
            int firstPlayerResult = 0;
            int secondPlayerResult = 0;
            Random randomGenerator = new Random();
            Console.ForegroundColor = ConsoleColor.Green;
            Console.BufferHeight = Console.WindowHeight;
            Console.BufferWidth = Console.WindowWidth;
            Program pr = new Program();
           int[]  mass = pr.SetInitialPositions(firstPlayerPadSize, secondPlayerPadSize);
           // Console.Write("first{0}", mass[0]);
            while (true)
            {
                if (Console.KeyAvailable)
                {
                    ConsoleKeyInfo keyInfo = Console.ReadKey();
                    if (keyInfo.Key == ConsoleKey.UpArrow)
                    {
                        if (mass[0] > 0)
                        {
                            mass[0]--;
                        }
                    }
                    else
                    {
                        if (keyInfo.Key == ConsoleKey.DownArrow)
                        {
                            if (mass[0] < Console.WindowHeight - firstPlayerPadSize)
                            {
                                mass[0]++;
                            }
                        }
                    }
                }
                int randomNumber = randomGenerator.Next(1, 101);

                if (randomNumber <= 70)
                {
                    if (ballDirectionUp == true)
                    {

                        if (mass[1] > 0)
                        {
                            mass[1]--;
                        }
                    }
                    else
                    {
                        if (mass[1] < Console.WindowHeight - secondPlayerPadSize)
                        {
                            mass[1]++;
                        }
                    }
                }
                 if (mass[3] == 0)
               {
                ballDirectionUp = false;
                }
            if (mass[3] == Console.WindowHeight - 1)
            {
                ballDirectionUp = true;
            }
            if (mass[2] == Console.WindowWidth - 1)
            {
               mass[2] = Console.WindowWidth / 2;
               mass[3] = Console.WindowHeight / 2;
               ballDirectionRight = false;
                ballDirectionUp = true;
                firstPlayerResult++;
                Console.SetCursorPosition(Console.WindowWidth / 2, Console.WindowHeight / 2);
                Console.WriteLine("First player wins!");
                Console.ReadKey();
            }
            if (mass[2] == 0)
                {
                    mass[2] = Console.WindowWidth / 2;
                    mass[3] = Console.WindowHeight / 2;
                    ballDirectionRight = true;
                ballDirectionUp = true;
                secondPlayerResult++;
                Console.SetCursorPosition(Console.WindowWidth / 2, Console.WindowHeight / 2);
                Console.WriteLine("Second player wins!");
                Console.ReadKey();
            }

            if (mass[2] < 3)
            {
                if ((mass[3] >= mass[0])&& (mass[3] < mass[0] + firstPlayerPadSize))
                {
                    ballDirectionRight = true;
                }
            }

            if (mass[2] >= Console.WindowWidth - 3 - 1)
            {
                if (mass[3] >= mass[1]
                    && mass[3] < mass[1] + secondPlayerPadSize)
                {
                    ballDirectionRight = false;
                }
            }

            if (ballDirectionUp)
            {
                    mass[3]--;
            }
            else
            {
                    mass[3]++;
            }


            if (ballDirectionRight)
            {
                    mass[2]++;
            }
            else
            {
                    mass[2]--;
            }
               Console.Clear();
                for (int y = mass[0]; y < mass[0] + firstPlayerPadSize; y++)
                {
                    PrintAtPosition(0, y, '|');
                    PrintAtPosition(1, y, '|');
                }

                for (int y = mass[1]; y < mass[1] + secondPlayerPadSize; y++)
                {
                    PrintAtPosition(Console.WindowWidth - 1, y, '|');
                    PrintAtPosition(Console.WindowWidth - 2, y, '|');
                }
                PrintAtPosition(mass[2],mass[3],'O');
                Console.SetCursorPosition(Console.WindowWidth / 2 - 1, 0);
                Console.Write("{0}-{1}", firstPlayerResult, secondPlayerResult);
                Thread.Sleep(60);
            }
        }
        public static void PrintAtPosition(int x, int y, char symbol)
        {
            Console.SetCursorPosition(x, y);
            Console.Write(symbol);
        }
        public int[] SetInitialPositions(int firstPlayerPadSize,int secondPlayerPadSize)
        {
            int firstPlayerPosition = 0;
            int secondPlayerPosition = 0;
            firstPlayerPosition = Console.WindowHeight  - firstPlayerPadSize ;
             
            secondPlayerPosition = Console.WindowHeight - secondPlayerPadSize ;
           int ballPositionX = Console.WindowWidth / 2;
           int ballPositionY = Console.WindowHeight / 2;
            int[] mass = { firstPlayerPosition, secondPlayerPosition, ballPositionX, ballPositionY };
            return mass;
        }
 
        
    }
}
