# Measurement-Program
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IO;
using System.Threading;


namespace Measurement
{
    class Program
    {
        static private readonly string path = Path.Combine(Environment.CurrentDirectory, @"Data\");
        static double grams = 28.35;
        static double pounds = 16.0;
        static double PoundsKilo = 0.45359237;
        static double Pint = 0.568;
        static double inch = 2.5;
        static double mile = 63360.0;

        static void Main(string[] args)
        {

            LoadConversionValues();
            // creating local variables
            int userOption = 0;
            int SelectMeasurementChoice = 0;
                           
            double result = 0;
                       
            // End local variables
            // display the menu
            while (userOption != 7) // allowing the user to exit the program
            {
                userOption = DisplayMenu();

                if (userOption == 7)
                    return;

                // Get the Numbers
                Console.WriteLine("Please input the first Number and hit the enter key.");
                SelectMeasurementChoice = getNumber();
                 
                // Now implementing value for the measurement

                if (userOption == 1) // converting one Ounce to how many Grams 
                {
                    result = SelectMeasurementChoice * grams;
                    SaveData(result, SelectMeasurementChoice);
                }
                else if (userOption == 2) //converting one Pound to how many Ounces 
                {
                    result = SelectMeasurementChoice * pounds;
                    SaveData(result, SelectMeasurementChoice);
                }
                else if (userOption == 3) //converting one Pound to how many Kilograms 
                {
                    result = SelectMeasurementChoice * PoundsKilo;
                    SaveData(result, SelectMeasurementChoice);
                }
                else if (userOption == 4) //converting one Pint to how many Litres 
                {
                    result = SelectMeasurementChoice * Pint;
                    SaveData(result, SelectMeasurementChoice);
                }
                else if (userOption == 5) //converting one inch to how many Centimetres 
                {
                    result = SelectMeasurementChoice - inch;
                    SaveData(result, SelectMeasurementChoice);
                }
                else if (userOption == 6) //converting one mile to how many Inches 
                {
                    result = SelectMeasurementChoice * mile;
                    SaveData(result, SelectMeasurementChoice);
                }
                else
                { 
                    //Nothing became of it
                }

                // showing the result of equations
                Console.WriteLine("The result of your options is: " + result);
            }


            //End display menu
        }
       
        private static int getNumber()
        {
            try     //get the number and parse the result
            {
                int number = int.Parse(Console.ReadLine());
                return number;
            }
            catch
            {
                // if there is an error, catch it and return 0
                Console.WriteLine("Error in input!");
                return 0;
            }
        }


            /// < SUMMARY >
            /// Display the actual menu
            ///  </summary>
            ///  <returns> Returns an int that represents the user's action</returns>
        private static int DisplayMenu()
        {
            Console.WriteLine("Jack Whetton Measurement system");
            Console.WriteLine(""); // To help make it look clearer
            Console.WriteLine("Enter in the corresponding number with Measurement you want to use");
            Console.WriteLine("");
            Console.WriteLine("1. Convert Ounce value to a Gram Value" + Environment.NewLine + "2. Convert Pound value to a Ounce Value" + Environment.NewLine
                + "3. Convert Pound value to a Kilogram Value" + Environment.NewLine + "4. Convert Pint value to a Litre Value" + Environment.NewLine +
                "5. Convert inch value to a centimetre Value" + Environment.NewLine + "6. Convert Mile value to a inch Value" + Environment.NewLine +
                "7. End Program" + Environment.NewLine);

            // measurement option for the user to select

            int optionValue;
            try
            {
                optionValue = int.Parse(Console.ReadLine());
            }
            catch
            {
                optionValue = 0;
            }
            return optionValue;
        }
        /// <Loading the Txt data measurement on to the conversion>
        ///load Conversion Value to allow the numbers to be taken from the text file. 
        /// Which should then split, enabling the program to take the number required.
        /// </summary>
        static public void LoadConversionValues() 
        {
            StreamReader loadConversionData;
            loadConversionData = new StreamReader(path + "convert.txt");
            // the name of txt file where it will load the coversion data

            string[] Firstline = loadConversionData.ReadLine().Split(',');
            grams = Convert.ToDouble(Firstline[2]); // The 3 value in txt file is 2 in number due it starts from 0
            // I also convert all value to double in order to get a more percise result
            string[] SecondLine = loadConversionData.ReadLine().Split(',');
            pounds = Convert.ToDouble(SecondLine[2]);

            string[] ThirdLine = loadConversionData.ReadLine().Split(',');
            PoundsKilo = Convert.ToDouble(ThirdLine[2]);

            string[] FourthLine = loadConversionData.ReadLine().Split(',');
            Pint = Convert.ToDouble(FourthLine[2]);

            string[] FifthLine = loadConversionData.ReadLine().Split(',');
            inch = Convert.ToDouble(FifthLine[2]);

            string[] SixthLine = loadConversionData.ReadLine().Split(',');
            mile = Convert.ToDouble(SixthLine[2]);

            loadConversionData.Close();
        }
        /// <summary>
        ///  so here i need to get the users to select the measurement from menu above
        ///  then from load conversion data the results will be saved in the debug file 
        ///  you can find the data which saves each value the user converts.
        /// </summary>
        /// <param name="result"></param>
        /// <param name="selectedchoice"></param>
        static public void SaveData(double result, int selectedchoice)
        {
            StreamWriter resultlog;
            resultlog = new StreamWriter(path + "Results.txt", true);
            // The is where all the data saves the result of user choose to the file system.

            switch (selectedchoice)
            {
                case 1:
                    resultlog.WriteLine("The Number of Ounces equal to " + result + "  in Grams");
                    break;
                case 2:
                    resultlog.WriteLine("The Number of Pounds equal to " + result + "  in Ounces");
                    break;
                case 3:
                    resultlog.WriteLine("The Number of Pounds equal to " + result + " in Kilograms");
                    break;
                case 4:
                    resultlog.WriteLine("The Number of Pints equal to " + result + " in Litres");
                    break;
                case 5:
                    resultlog.WriteLine("The Number of Inches equal to " + result + " in Centimetres");
                    break;
                case 6:
                    resultlog.WriteLine("The Number of Miles Equal to " + result + "in Inches");
                    break;
            }
           
            //New Measurement\Measurement\Measurement\bin\Debug\Data\Results
            // This allow the user to go over there previous results of mesurement conversions
            resultlog.Close();
        }
    }
}
