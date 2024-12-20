using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Задание_5
{
    internal class Program
    {

        static string QuickSort(char[] array)
        {
            if (array.Length <= 1) return new string(array);
            char pivot = array[array.Length / 2];
            var less = array.Where(x => x < pivot).ToArray();
            var equal = array.Where(x => x == pivot).ToArray();
            var greater = array.Where(x => x > pivot).ToArray();
            return QuickSort(less) + new string(equal) + QuickSort(greater);
        }

        static string TreeSort(char[] array)
        {
            return new string(array.OrderBy(c => c).ToArray());
        }

        static string FindLongestVowelSubstring(string str)
        {
            string vowels = "aeiouy";
            string longest = string.Empty;

            for (int i = 0; i < str.Length; i++)
            {
                for (int j = i + 1; j < str.Length; j++)
                {
                    if (vowels.Contains(str[i]) && vowels.Contains(str[j]))
                    {
                        string substring = str.Substring(i, j - i + 1);
                        if (substring.Length > longest.Length)
                        {
                            longest = substring;
                        }
                    }
                }
            }
            return longest;
        }
        static string ReverseString(string str)
        {
            char[] chars = str.ToCharArray();
            Array.Reverse(chars);
            return new string(chars);
        }
        static void PrintRepeatFrequency(string str)
        {
            var repeat = new Dictionary<char, int>();
            foreach (char c in str)
            {
                if (repeat.ContainsKey(c))
                {
                    repeat[c]++;
                }
                else
                {
                    repeat[c] = 1;
                }
            }
            foreach (var kvp in repeat)
            {
                Console.WriteLine($"{kvp.Key}: {kvp.Value}");
            }
        }
        static void Main(string[] args)
        {
            string a = Console.ReadLine();
            string result; 
            int k = 0;
            Console.WriteLine(a);

            List<char> invalid = new List<char>();
            foreach (char c in a)
            {
                if (c < 'a' || c > 'z')
                {
                    invalid.Add(c);
                }
            }

            if (invalid.Count > 0)
            {
                Console.WriteLine("Ошибка: введены неподходящие символы: " + string.Join(", ", invalid));
                Console.ReadKey();

            }

            if (a.Length % 2 == 0) {
                k = a.Length / 2;
                string first = a.Substring(0, k);
                string second = a.Substring(k);
                result = ReverseString(first) + ReverseString(second);
            }
            else {
                result = ReverseString(a) + a;
            }

            string longestVowelSubstring = FindLongestVowelSubstring(result);

            if (longestVowelSubstring == "")
            {
                Console.WriteLine("Подстрока не найдена");
            }
            else
            {
                Console.WriteLine("Обработанная строка: " + result);
                PrintRepeatFrequency(result);
                Console.WriteLine("Наибольшая подстрока, начинающаяся и заканчивающаяся на гласную: " + longestVowelSubstring);

                Console.WriteLine("Выберите алгоритм сортировки (1 - Быстрая сортировка, 2 - Сортировка деревом):");
                int choice = int.Parse(Console.ReadLine());
                string sortedString;

                if (choice == 1)
                {
                    sortedString = QuickSort(result.ToCharArray());
                }
                else
                {
                    sortedString = TreeSort(result.ToCharArray());
                }

                Console.WriteLine("Отсортированная строка: " + sortedString);
            }

           

            Console.ReadKey();


        }

    }
}
