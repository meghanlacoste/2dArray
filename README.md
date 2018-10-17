package com.company;
import java.util.*;
import java.io.*;
import static com.company.ProjConstants.*;
public class Main {


    public static final int MAXDATA = 100;

    public static void main(String[] args) {



        // Creates a  2- dimensional String (aka. matrix) that Stores Strings and counts frequency (arrayStoreFreq)
        String arr_StoreFreq[][] = new String [MAXDATA][2];


        // Initialize the array to a known value
        // - loops over each row using "i", and columns using "j"
        // -  sets all array values to INVALID

        for(int i=0; i < MAXDATA; i++) {
            for(int j = 0; j < 2; j++){
                arr_StoreFreq[i][j] = "INVALID";
            }
        }


        // -------------------------------------------------------------------------


        // INITIALIZES/DECLARES VARIABLES:

        String userFileName;
        boolean replicatedWord;
        boolean fileDone = false;


        // -------------------------------------------------------------------------

        // Requests user for file name

        System.out.println("");
        System.out.println("Please type in the file name\n");

        // create a variable s of type scanner to process input from "System.in"
        Scanner scanSystemIn = new Scanner(System.in);

        // Use the Scanner "s" to get the "next" input from "System.in"
        userFileName = scanSystemIn.next();

        // Display the user input now stored in "userInput"
        System.out.println("\nThe user input: " + userFileName);



        // -------------------------------------
        //
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


                // sets boolean back to false at the start of each repetition
                replicatedWord = false;


                // --------------------------------------------------
                // The scanner checks if there is another string
                //

                if (scanUserFile.hasNext()) {

                    // converts string to lower case

                    String fileWord =  scanUserFile.next().toLowerCase();


                    // starting at the current index position 'i', loops backwards over previously stored
                    // strings in the array and checks if the file word is equal to any of the previous values

                    for (int index = i; index >= 0; index --) {

                        if (fileWord.equalsIgnoreCase(arr_StoreFreq[index][0])) {

                            // converts string stored in array to integer
                            int frequency = Integer.parseInt(arr_StoreFreq[index][1]);

                            // adds one to the frequency
                            frequency  += 1 ;

                            // stores the new frequency as a string
                            arr_StoreFreq [index][1] = Integer.toString(frequency);

                            replicatedWord = true;

                        }

                    }

                    // ---------------------------------------
                    //
                    //  pre-conditions:
                    //      - the word is unique

                    if (!replicatedWord) {

                        // stores the word from the file in the next position of the array
                        arr_StoreFreq[i][0] = fileWord;

                        // The frequency of the unique variable will be set to an initial value of 1.

                        int frequency2 = 1;

                        // the value of 1 will be converted into a string type so that it can be stored in the second colomn of the array.

                        arr_StoreFreq [i][1] = Integer.toString(frequency2);


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


        //-----------------------------------------------------------------------------------------------------

        // creates new 2d array with 3 columns
        String arr_subStrings [][] = new String [MAXDATA][3];

        // The data to be stored in each column is as follows:
        //      - first columns [][0] will be the substring
        //      - second column [][1] will be frequency of substring
        //      - third column [][2] will be lists of words containing that substring

        // Initialize the array to a known value
        // - loops over each row using "i", and columns using "j"
        // -  sets all array values to INVALID

        for(int i=0; i < MAXDATA; i++) {
            for(int j = 0; j < 2; j++){
                arr_subStrings[i][j] = "INVALID";
            }
        }



        for (int i = 0; i < MAXDATA; i++) {


            for (int index = i; index >= 0; index--)


                if (arr_StoreFreq[i][0].contains(arr_StoreFreq[index][0]) && (arr_StoreFreq[i][0] != "INVALID") && (i != index)) {

                    int frequency = Integer.parseInt(arr_StoreFreq[index][1]);

                    frequency = 1;

                    arr_subStrings[i][0] = arr_StoreFreq[index][0];

                    arr_subStrings[i][1] = Integer.toString(frequency);

                    arr_subStrings[i][2] = arr_StoreFreq[i][0];


                }

        } // for (int i = 0; i < MAXDATA; i++)


        // loops over subStrings array to check if any substrings are replicated

        for (int i = 0; i < MAXDATA; i++) {

            for (int index = i; index >= 0; index --) {

                //pre-conditions:
                //      - the substring stored is equal to another substring already stored in the array
                //      - the string stored is not the default set "INVALID"
                //      - the two substrings being compared are not at the same index position in the array
                //


                if (arr_subStrings[index][0].equalsIgnoreCase(arr_subStrings[i][0]) && (arr_subStrings[i][0] != "INVALID") && (i != index) ) {

                    // adds the word containing substring to the list in the row where the substring first appears
                    arr_subStrings[index][2] += (", " + arr_subStrings [i][2]);

                    // sets all values in the row where the substring is repeated
                    // back to the default "INVALID" removing the replication
                    //
                    arr_subStrings [i][0] = "INVALID";
                    arr_subStrings [i][1] = "INVALID";
                    arr_subStrings [i][2] = "INVALID";




                    // converts string stored in array to integer
                    int frequency = Integer.parseInt(arr_subStrings[index][1]);

                    // adds one to the frequency of the substring
                    frequency  += 1 ;

                    // stores the new frequency as a string
                    arr_subStrings [index][1] = Integer.toString(frequency);


                } // END if (arr_subStrings[index][0].equalsIgnoreCase(arr_subStrings[i][0]) && (arr_subStrings[i][0] != "INVALID") && (i != index) )

            }// END for (int index = i; index >= 0; index --) {

        }// END for (int i = 0; i < MAXDATA; i++)

        // Displays Results

        System.out.println("==========================================================================================");

        System.out.println("\n          WORD:            FREQUENCY:  \n");

        for (int i = 0; i < MAXDATA; i++) {
            if (arr_StoreFreq[i][0] != "INVALID") {

                System.out.printf("    %10.1000000000s\t %10.1000000s\n\n", arr_StoreFreq[i][0], arr_StoreFreq[i][1]);

            }
        }

        System.out.println();

        System.out.println("==========================================================================================\n");



        System.out.println("\n          SUBSTRING:            FREQUENCY:        WORDS CONTAINING SUBSTRING: \n");

        for (int i = 0; i < MAXDATA; i++) {
            if (arr_subStrings[i][0] != "INVALID") {

                System.out.printf("     %10.1000000000s\t\t\t%10.1000000s\t\t\t\t %10.1000000s\n\n", arr_subStrings[i][0], arr_subStrings[i][1],  arr_subStrings[i][2]);

            }
        }

        System.out.println();

        System.out.println("==========================================================================================\n");




    }// END MAIN METHOD
}// END MAIN CLASS

