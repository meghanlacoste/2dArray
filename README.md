package com.company;
import java.util.*;
import java.io.*;
import static com.company.ProjConstants.*;
public class Main {

    public static void main(String[] args) {
        // write your code here

        // Create 2- dimensional String (aka. matrix) that Stores Strings and counts frequency (arrayStoreFreq)
        String arrayStoreFreq[][] = new String [MAXDATA][2];



        // Initialize the array to a known value
        // - loops over each row using "i", and columns using "j"
        // -  sets all array values to INVALID

        for(int i=0; i < MAXDATA; i++) {
            for(int j = 0; j < 2; j++){
                arrayStoreFreq[i][j] = "invalid";
            }
        }



        String userFileName;
        boolean uniqueWord;
        boolean fileDone = false;



        System.out.println("");
        System.out.println("Please type in the file name\n");

        // create a variable s of type scanner to process input from "System.in"
        Scanner scanSystemIn = new Scanner(System.in);

        // Use the Scanner "s" to get the "next" input from "System.in"
        userFileName = scanSystemIn.next();

        // Display the user input now stored in "userInput"
        System.out.println("\nThe user input: " + userFileName);



        // ---------------------------------------------
        // This is where we "try" to process the file
        //

        try {
            // --------------------------------
            // create file, and scanner objects
            // - file object is called tempfilenums.txt and is in your project directory
            //   that is the same folder as the iml file
            //

            File userFile = new File(userFileName);
            Scanner scanUserFile = new Scanner(userFile);

            // ---------------------------------------------
            // Reads in values from the file in a for loop
            //

            for(int i = 0; i < MAXDATA; i++) {

                uniqueWord = false;

                // ---------------------------------------------
                // The scanner checks if there is another string
                //

                if (scanUserFile.hasNext()) {

                    // converts string to lower case

                    String fileWord =  scanUserFile.next().toLowerCase();


                    for (int index = i; index >= 0; index --) {

                        if (fileWord.equalsIgnoreCase(arrayStoreFreq[index][0])) {

                            int frequency = Integer.parseInt(arrayStoreFreq[index][1]);

                            frequency  += 1 ;

                            arrayStoreFreq [index][1] = Integer.toString(frequency);

                            uniqueWord = true;

                        }

                    }

                    if (!uniqueWord) {

                        // stores the word from the file in the next position of the array
                        arrayStoreFreq[i][0] = fileWord;

                        // The frequency of the unique variable will be set to an initial value of 1.

                        int frequency2 = 1;

                        // the value of 1 will be converted into a string type so that it can be stored in the second colomn of the array.

                        arrayStoreFreq [i][1] = Integer.toString(frequency2);


                    }



                }// end if scanner has next

                else {
                    // ---------------------------------------------
                    // The scanner detected no other integers
                    // - sets boolean "fileDone" to true
                    // - closes the scanner
                    // - breaks out of the for loop
                    //

                    fileDone = true;
                    scanUserFile.close();
                    break;
                }
            }

            // ---------------------------------------------
            // The file has been completely read into the array, so the user is notified.
            //

            System.out.println();
            if (fileDone) {
                System.out.println("\n\tFile data has been read into array\n");

            }

            // ---------------------------------------------
            // If there is not enough space in the array so make sure the user is notified that the file contains
            // more data than the array can hold.
            //

            if (!fileDone) {
                System.out.println("\n\tCAUTION: file has additional data, consider making array larger.\n");
            }


            // ---------------------------------------------
            // If the file cannot be found then an exception (error) is generated (thrown) that we have to
            // deal with (catch).
            // - we print "e" the exception, and
            // - show the user where it was using the "exceptions" stack trace information
            //

        } catch (FileNotFoundException e) {
            System.out.println(e);
            e.printStackTrace();
        }



            // Displays Results

            System.out.println("==========================================================================================");

        System.out.println("\n          WORD:            FREQUENCY:  \n");

            for (int i = 0; i < MAXDATA; i++) {
                 if (arrayStoreFreq[i][0] != "invalid") {

                      System.out.printf("    %10.1000000000s\t %10.1000000s\n", arrayStoreFreq[i][0], arrayStoreFreq[i][1]);

                 }
             }

             System.out.println();

            System.out.println("==========================================================================================\n");


            String subStrings [][] = new String [MAXDATA][3];

            // first columns [][0] will be the substring

            // second column [][1] will be frequency of substring

            // third column [][2] will be lists of words containing that substring

        // Initialize the array to a known value
        // - loops over each row using "i", and columns using "j"
        // -  sets all array values to INVALID

        for(int i=0; i < MAXDATA; i++) {
            for(int j = 0; j < 2; j++){
                subStrings[i][j] = "invalid";
            }
        }



        for (int i = 0; i < MAXDATA; i++){
            for (int index = i; index >= 0; index --)


            if (arrayStoreFreq[i][0].contains(arrayStoreFreq [index][0]) && (arrayStoreFreq[i][0] != "invalid") && (i !=index)) {

                 int frequency = Integer.parseInt(arrayStoreFreq[index][1]);

                frequency += 1;

                subStrings[i][0] = arrayStoreFreq[index][0];

                subStrings[i][1] = Integer.toString(frequency);

                subStrings[i][2] = arrayStoreFreq[i][0];


                System.out.println(" word: " + arrayStoreFreq[i][0] + " contains: " + arrayStoreFreq [index][0]);





            }
        }


        System.out.println("==========================================================================================");

        System.out.println("\n          SUBSTRING:            FREQUENCY:        WORDS CONTAINING SUBSTRING: \n");

        for (int i = 0; i < MAXDATA; i++) {
            if (subStrings[i][0] != "invalid") {

                System.out.printf("     %10.1000000000s\t\t\t%10.1000000s\t\t\t\t %10.1000000s\n", subStrings[i][0], subStrings[i][1],  subStrings[i][2]);

            }
        }

        System.out.println();

        System.out.println("==========================================================================================\n");




    }// END MAIN METHOD
}// END MAIN CLASS




/*
- Create two 2 dimensional arrays
- The first 2 Dimensional array is to be used to store strings, and the frequency a particular string occurs in a file
- Have the user provide the name of a file to be read
- strings (words) in the file are all to be converted into upper, or lower, case before being stored in the array, column 1,
 and the frequency is to be stored in column 2
- output the list of words and their frequency neatly to the screen
- once the file has been completely read it is to be closed
- use the data stored in the 2 Dimensional array (3 columns) and find all words that are sub-strings of others in the array,
store these in the first column of the new 2 Dimensional array, store the frequency in the second column, and store the list of words
containing the sub-string in the third column

All programs must have white space (blank lines) to help make the code more readable, use indentation for loops, conditionals and methods,
be appropriately commented, and use descriptive variable names.
 */
