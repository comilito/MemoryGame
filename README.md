# MemoryGame
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.IO;
using System.Linq;

namespace MemoryGame
{
    class Program
    {
        static List<string> readFromFile() {
            List<string> wordslist = new List<string>();
            var lines = File.ReadAllLines("Words.txt");
            foreach (var line in lines)
            {
                wordslist.Add(line);
            }
            var rnd = new Random();
            var randomized = wordslist.OrderBy(item1 => rnd.Next());
            List<string> wordslistR = randomized.ToList();
            return wordslistR;

        }
        static void printMatrix(string[,] array2D, int guess,int size)
        {
            if(size == 4) { 
            Console.Write("\n\n Level: Easy\n Guess chances: {0} \n", guess);
            Console.Write("{0,-12}{1,-12}{2,-12}{3,-12}{4,-12}\n", " ", 1, 2, 3, 4);
            }
            else
            {
                Console.Write("\n\n Level: Hard\n Guess chances: {0} \n", guess);
                Console.Write("{0,-12}{1,-12}{2,-12}{3,-12}{4,-12}{5,-12}{6,-12}{7,-12}{8,-12}\n", " ", 1, 2, 3, 4,5,6,7,8);
            }
            for (int i = 0; i < 2; i++)
            {
                if (i == 0)
                    Console.Write("{0,-12}", " A");
                else
                    Console.Write("{0,-12}", " B");
                for (int j = 0; j < size; j++)
                {
                    Console.Write("{0,-12}", array2D[i, j]);
                }
                Console.WriteLine();
            }
            Console.Write("\n    >> ");

        }
        static void playEasyGame(List<string> firstRow, List<string> secondRow) {
            int guess = 10;
            int win = 0;
            string userInput;
            string[,] array2D = new string[2, 4];
            for (int i = 0; i < 4; i++)
            {
                
                array2D[0, i] = "X";
                array2D[1, i] = "X";

            }

            Console.Write("\n\t --- Enter the coordinate to reveal thier position --- \n\n Cordinates are:  A1  A2  A3  A4 \n\t\t  B1  B2  B3  B4 \n\n Press Any Key To Continue ... ");
            Console.ReadKey();
            while (true)
            {
                Console.Clear();
                printMatrix(array2D, guess,4);

                userInput = Console.ReadLine();
                int num = Convert.ToInt32(userInput[1]) - 49;
                int i1 = 0;
                int j1 = 0;
                if (userInput[0] == 'A' || userInput[0] == 'a')
                {
                    if (num < 4)
                    {
                        i1 = 0;
                        j1 = num;
                        array2D[0, num] = firstRow.ElementAt(num);
                    }
                }
                else if (userInput[0] == 'B' || userInput[0] == 'b')
                {
                    if (num < 4)
                    {
                        i1 = 1;
                        j1 = num;
                        array2D[1, num] = secondRow.ElementAt(num);
                    }
                }
                Console.Clear();
                printMatrix(array2D, guess, 4);
                userInput = Console.ReadLine();
                num = Convert.ToInt32(userInput[1]) - 49;
                if (userInput[0] == 'A' || userInput[0] == 'a')
                {
                    if (num < 4)
                    {
                        if (String.Equals(array2D[i1, j1], firstRow.ElementAt(num)))
                        {
                            Console.WriteLine("\n !!! Correct !!! \n");
                            win++;
                            array2D[0, num] = firstRow.ElementAt(num);
                            Console.WriteLine("\n Press Any key to continue .... \n");
                            Console.ReadLine();
                        }
                        else
                        {
                            Console.WriteLine("\n !!! Wrong !!! \n");
                            array2D[i1, j1] = "X";
                            guess--;
                            Console.WriteLine("\n Press Any key to continue .... \n");
                            Console.ReadLine();

                        }
                    }
                }
                else if (userInput[0] == 'B' || userInput[0] == 'b')
                {
                    if (num < 4)
                    {
                        if (String.Equals(array2D[i1, j1], secondRow.ElementAt(num)))
                        {
                            win++;
                            Console.WriteLine("\n !!! Correct !!! \n");
                            array2D[1, num] = secondRow.ElementAt(num);
                            Console.WriteLine("\n Press Any key to continue .... \n");
                            Console.ReadLine();
                        }
                        else
                        {
                            Console.WriteLine("\n !!! Wrong !!! \n");
                            Console.WriteLine("\n Press Any key to continue .... \n");
                            Console.ReadLine();
                            array2D[i1, j1] = "X";
                            guess--;
                        }
                    }
                }
                if (guess == 0)
                {
                    Console.WriteLine("\n Zero Chances Left \n \n\t ---- GAME OVER --- \n\n");
                    break;
                }
                if (win == 4)
                {
                    printMatrix(array2D, guess, 4);
                    Console.WriteLine("\n All words Guessed Correctly \n \n\t ---- GAME WON --- \n\n");
                    break;


                }
            }
            }
        static void playHardGame(List<string> firstRow, List<string> secondRow)
        {

            int guess = 15;
            int win = 0;
            string userInput;
            string[,] array2D = new string[2, 8];
            for (int i = 0; i < 8; i++)
            {

                array2D[0, i] = "X";
                array2D[1, i] = "X";

            }

            Console.Write("    --- Enter the coordinate to reveal thier position --- \n\n Cordinates are:  A1  A2  A3  A4  A5  A6  A7  A8 \n\t\t  B1  B2  B3  B4  B5  B6  B7  B8 \n\n Press Any Key To Continue ... ");
            Console.ReadKey();

            while (true)
            {

                Console.Clear();
                printMatrix(array2D, guess, 8);
                userInput = Console.ReadLine();
                int num = Convert.ToInt32(userInput[1]) - 49;
                int i1 = 0;
                int j1 = 0;
                if (userInput[0] == 'A' || userInput[0] == 'a')
                {
                    if (num < 8)
                    {
                        i1 = 0;
                        j1 = num;
                        array2D[0, num] = firstRow.ElementAt(num);
                    }
                }
                else if (userInput[0] == 'B' || userInput[0] == 'b')
                {
                    if (num < 8)
                    {
                        i1 = 1;
                        j1 = num;
                        array2D[1, num] = secondRow.ElementAt(num);
                    }
                }
                Console.Clear();
                printMatrix(array2D, guess, 8);

                userInput = Console.ReadLine();
                num = Convert.ToInt32(userInput[1]) - 49;
                if (userInput[0] == 'A' || userInput[0] == 'a')
                {
                    if (num < 8)
                    {
                        if (String.Equals(array2D[i1, j1], firstRow.ElementAt(num)))
                        {
                            Console.WriteLine("\n !!! Correct !!! \n");
                            win++;
                            array2D[0, num] = firstRow.ElementAt(num);
                            Console.WriteLine("\n Press Any key to continue .... \n");
                            Console.ReadLine();
                        }
                        else
                        {
                            Console.WriteLine("\n !!! Wrong !!! \n");
                            array2D[i1, j1] = "X";
                            guess--;
                            Console.WriteLine("\n Press Any key to continue .... \n");
                            Console.ReadLine();

                        }
                    }
                }
                else if (userInput[0] == 'B' || userInput[0] == 'b')
                {
                    if (num < 8)
                    {
                        if (String.Equals(array2D[i1, j1], secondRow.ElementAt(num)))
                        {
                            win++;
                            Console.WriteLine("\n !!! Correct !!! \n");
                            array2D[1, num] = secondRow.ElementAt(num);
                            Console.WriteLine("\n Press Any key to continue .... \n");
                            Console.ReadLine();
                        }
                        else
                        {
                            Console.WriteLine("\n !!! Wrong !!! \n");
                            Console.WriteLine("\n Press Any key to continue .... \n");
                            Console.ReadLine();
                            array2D[i1, j1] = "X";
                            guess--;
                        }
                    }
                }

                if (guess == 0)
                {
                    Console.WriteLine("\n Zero Chances Left \n \n\t ---- GAME OVER --- \n\n");
                    break;
                }
                if (win == 8)
                {
                    printMatrix(array2D, guess, 8);
                    Console.WriteLine("\n All words Guessed Correctly \n \n\t ---- GAME WON --- \n\n");
                    break;


                }
            }
        }



        static void Main(string[] args)
        {
            while (true) {
            var rnd = new Random();
            List<string> RandomWords = readFromFile();

            Console.Write("\n\n --- Welcome To Word Guessing game--- \n\n 1- Easy Mode \n 2- Hard Mode \n 3- Quit \n \n Your Choice >> ");
            int choice = 0;
            string userInput = Console.ReadLine();
            choice = Convert.ToInt32(userInput);
                if (choice == 1)
                {

                    Stopwatch stopwatch = new Stopwatch();
                    stopwatch.Start();
                    Console.Clear();
                    Console.WriteLine("\n\t       --- Easy Mode --- \n\t --- 4 Words, 10 Chances --- \n\n");
                    var firstRow1 = RandomWords.Take(4);
                    List<string> firstRow = firstRow1.ToList();
                    var randomized = firstRow.OrderBy(item => rnd.Next());

                    List<string> secondRow = randomized.ToList();
                    playEasyGame(firstRow, secondRow);
                    stopwatch.Stop();
                    TimeSpan stopwatchElapsed = stopwatch.Elapsed;
                    Console.WriteLine("\n ---- This Game Took {0} seconds to complete.---- \n", Convert.ToInt32(stopwatchElapsed.TotalSeconds));
                    Console.WriteLine("\n Press Any key to continue .... \n");
                    Console.ReadLine();
                    Console.Clear();


                }
                else if (choice == 2)
                {
                    Stopwatch stopwatch = new Stopwatch();
                    stopwatch.Start();
                    
                    Console.Clear();
                    Console.WriteLine("\n\t       --- Hard Mode --- \n\t --- 8 Words, 15 Chances --- \n\n");

                    var firstRow1 = RandomWords.Take(8);
                    List<string> firstRow = firstRow1.ToList();
                    var randomized = firstRow.OrderBy(item => rnd.Next());

                    List<string> secondRow = randomized.ToList();

                    playHardGame(firstRow, secondRow);
                    stopwatch.Stop();
                    TimeSpan stopwatchElapsed = stopwatch.Elapsed;
                    Console.WriteLine("\n ---- This Game Took {0} seconds to complete.---- \n",Convert.ToInt32(stopwatchElapsed.TotalSeconds));
                    Console.WriteLine("\n Press Any key to continue .... \n");
                    Console.ReadLine();
                    Console.Clear();

                }
                else if (choice == 3)
                {
                    Console.WriteLine("\n Program Terminated, Thanks for playing!!! \n");
                    break;
                }
                else {
                    Console.WriteLine(" \n Invalid Choice, Try Again \n");
                    Console.WriteLine("\nPress Any key to continue .... \n");
                    Console.ReadLine();
                    Console.Clear();

                }
            }

          


        }

       
    }
}
