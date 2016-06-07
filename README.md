# Recursive-File-Finder
Simple code that will search recusively for files
package Recursive_File_Finder;

import java.io.File;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Scanner;

/**
 *
 * @author Eugene O' Regan
 */
public class FileLister {

    public static int count_of_files;
    public static List<String> Files_Found = new <String> ArrayList();

    public static void main(String[] args) {
        Scanner inputStr = new Scanner(System.in);
        System.out.println("Input the directory");
              
        String FilePath = inputStr.next().replace("\\", "\\\\"); // Folder to start searching from
        File startDir = new File(FilePath);
        System.out.println("Input the criteria");
        String searchCriteria = inputStr.next(); // File-type to search for
        searchCriteria = searchCriteria.toLowerCase();
        Searcher(startDir, searchCriteria, true);
        System.out.println("There are " + count_of_files + " " + searchCriteria + " files");
        System.out.println(Files_Found.toString());
}

    /**
     * Simple method that searches for files given a specific criteria, which
     * uses recursion.
     *
     * @param start Directory to start search
     * @param criteria File types looking for
     * @param recursiveSearch Do we do a recursive search i.e. look in subfolders
     * 
     */
    public static void Searcher(File start, String criteria, Boolean recursiveSearch) {
        File files[] = start.listFiles(); // Lists all files from the base directory
        /*
         A for ... each loop used to examine each file
         */
        System.out.println(Arrays.toString(files));
        for (File currentFile : files) {
            if (recursiveSearch && currentFile.isDirectory() ) // If the current file is a directory and doing a recursive search
            {
                System.out.println("Sub-Directory === " +currentFile.getName());
                Searcher(currentFile, criteria, recursiveSearch); // A recursive call
            } else if (currentFile.getName().toLowerCase().endsWith(criteria)) { // The else just lists the files
                
                count_of_files++; // Increment the number of files found for counter
                /*
                 * Add the name of the file to the ArrayList Files_Found 
                 */
                Files_Found.add(currentFile.getPath());
            } // End of if ... else if

        }// End of method
    }// End of main

} // End of class
