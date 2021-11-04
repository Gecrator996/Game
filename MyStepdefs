package test;

import org.junit.Test;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import java.util.concurrent.TimeUnit;
import java.io.IOException;
import java.net.HttpURLConnection;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.List;


public class MyStepdefs {

    public static String answer = "";

    public static boolean websiteCheckAlive (WebDriver driver) throws MalformedURLException, IOException{

        boolean check;

        driver.manage().timeouts().implicitlyWait(4, TimeUnit.SECONDS);
        // establish and open connection with URL
        HttpURLConnection cn = (HttpURLConnection) new
                URL("https://clicktime-wordgame-exercise.vercel.app/")
                .openConnection();
        // set the HEAD request with setRequestMethod
        cn.setRequestMethod("HEAD");
        // connection initiated and obtain status code
        cn.connect();
        int c = cn.getResponseCode();
        System.out.println("Http status code: " + c);
        if (c == 200) {
            check = true;
        }
        else {
            check = false;
        }
        return check;

    }

    //This function creates a list of all 27  alphabet characters, and retrieves each letter from alphabet to see if it matches each letter in our required answer. (for instance: the first alphabet letter is A and the first letter of our first answer in our List of answers is F, A doesn't match F so the loop goes on until eachAlphabetChar(A, B, C etc) matches our oneLetter(F) and it goes on)
    public static void typingWords (String answer, List<WebElement> list, WebDriver driver) {

        list = driver.findElements(By.xpath("(//span[contains(@class,'text')])")); //xPaths for all 27 letter from alphabet

        //retrieves each character from the alphabet
        for (WebElement eachAlphabetChar: list) {

            //gets text from the webElement which are (A, B, C etc)
            String character = eachAlphabetChar.getText();

            int i;

            //this loop runs as many times as there are letter in our string 'answer' which is defined below. For instance first string of our list of answers is 'FRIENDS' which has 7 letters, so the loop will be running 7 times.
            for (i = 0; i < answer.length(); i++) {

                //this code retrieves each letter from the string 'answer' which is 'FRIENDS' etc
                String oneLetter = answer.substring(i, i+1);

                //this code verifies if the letter from the alphabet matches the letters from our string with answers
                if(character.matches(oneLetter)) {

                    //if the letters are matching, then the code will click on the webElement(button) with the matching letter
                    eachAlphabetChar.click();

                }
            }

            //and when the code reaches the last letter of the 'answer' string it breaks the loop for retrieving the alphabetic characters
            if(i == (answer.length() - 1 )) {
                break;
            }

        }

    }


    @Test
    public static void main(String[] args) throws Exception {

        WebDriver driver = new ChromeDriver();
        System.setProperty("webdriver.chrome.driver","C:\\Users\\ghs6kor\\Desktop\\Java\\chromedriver.exe");

        //Creating the list of all 6 answers for the game
        List<String> listOfAnswers = List.of("FRIENDS", "THE MATRIX", "CRIME AND PUNISHMENT", "NEW YORK", "SUSHI", " ");

        //Creating the list of sections for the game to choose from
        List<String> listOfSections = List.of("TV Shows", "Movies", "Books", "Places", "Foods", "Animals");

        System.out.println(websiteCheckAlive(driver));

        //Here we retrieve each string from our lists of strings
        for (int i = 0; i < listOfAnswers.size(); i++) {

            //Retrieve 1st, 2ns etc String from the listOfAnswers list, our answers
            answer = listOfAnswers.get(i);

            //Retrieve 1st, 2ns etc String from the listOfSections list, the sections for the game
            String section = listOfSections.get(i);

            //Here we create the list with WebElements which can be found by this xPath (//span[contains(@class,'text')]) all 27 xPaths
            List<WebElement> list = driver.findElements(By.xpath("(//span[contains(@class,'text')])"));

            //Opening the website
            driver.get("https://clicktime-wordgame-exercise.vercel.app/");

            //If 10 has passed and there is no response from the server, fail
            driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);

            //Maximize the window
            driver.manage().window().maximize();

            //Typing "Test" into the "Username" input field
            driver.findElement(By.xpath("//input[@class='input_input__SUO-5']")).sendKeys("Test");

            //Clicking the dropdown menu
            driver.findElement(By.xpath("//select[contains(@class,'2eNun')]")).click();

            //Click on the corresponding section of the dropdown menu
            driver.findElement(By.xpath("//option[contains(text(),'" + section + "')]")).click();

            //Clicking the "Load Game" button
            driver.findElement(By.xpath("(//button[contains(@class,'6jxn1')])[1]")).click();

            //Waiting for all of the elements to be loaded, without this code might fail since no elements are loaded and the code is executed
            TimeUnit.SECONDS.sleep(1);

            //Creating a list for the window when you open the website or press the "Restart Game" button.
            List<WebElement> window = driver.findElements(By.xpath("//div[contains(@class, 'IiR-3')]"));

            //Below is an if statement if the code detected the window that means the "Load Game" button cannot be pressed and the code fails.
            if(window.size() > 0) {
                System.out.println("Could not execute the Test " + (i + 1) + ". The window is still open.");
            } else {

                typingWords(answer, list, driver);

                driver.findElement(By.xpath("//button[contains(@class,'button_st')]")).click();

                System.out.println("Test " + (i + 1) + " was finished!");

            }
        }
        //Close the browser
        driver.quit();
    }
}
