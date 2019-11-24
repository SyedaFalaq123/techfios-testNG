package HomeWork2;

import java.util.Random;
import java.util.concurrent.TimeUnit;

import org.junit.Test;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.Select;
import org.openqa.selenium.support.ui.WebDriverWait;


public class UsersAddDeposit {
	
	
		// TODO Auto-generated method stub

		/*1: Open Browser and go to site http://techfios.com/test/billing/?ng=admin/
2. Enter username: techfiosdemo@gmail.com
3. Enter password: abc123
4. Click login button
5. Click on Add Deposit button on Dashboard Page
6. Click on Open An Account drop down to expand it,
7. Click on any account name,
8. Type any description,
9. Type any amount,
10. Click on submit button,
Visually check to make sure the deposit posted
*/
		
		
	@Test
	public void validUsersShouldBeAbleToLogIn() throws InterruptedException {
		
	//Set Chrome as default browser
		
		System.setProperty("webdriver.chrome.driver", "./driver/chromedriver");
	
	//Open Chrome Browserd
	
	WebDriver driver = new ChromeDriver();
	
	//Maximize the window
	// driver.manage().window().maximize();
	//Implicit wait
	
	driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
	
	//Go to TechFios Website
	
	driver.get("http://techfios.com/test/billing/?ng=admin/");
	
	//Type username in the username field
	
	driver.findElement(By.id("username")).sendKeys("techfiosdemo@gmail.com");
	
	
	//Type password in the password field
	driver.findElement(By.name("password")).sendKeys("abc123");

	//Click on Sign In button
	driver.findElement(By.name("login")).click();
	
	//====================================================
		//5. Click on Add Deposit button on Dashboard Page	
	
	driver.findElement(By.linkText("Add Deposit")).click();


//6. Click on Open An Account drop down to expand it,
	Thread.sleep(3000);
	WebElement element = driver.findElement(By.name("account"));
	Select select = new Select(element);
	select.selectByIndex(8);
	//driver.findElement(By.xpath("//select[@id='account']/option[@value='Sarker']")).click();
	
/*7. Click on any account name,
	8. Type any description,
	9. Type any amount,
	10. Click on submit button,*/
	
	Random rnd = new Random();
	
	int randomNumber = rnd.nextInt(676);
	String description = "Billing";
	
	String amount = String.valueOf(randomNumber);
	driver.findElement(By.name("description")).sendKeys(description);
	driver.findElement(By.name("amount")).sendKeys(amount);
	driver.findElement(By.id("submit")).click();
	//Thread.sleep(5000);
	By recentDepositLocator = By.linkText(description);
	
	
	WebDriverWait wait = new WebDriverWait(driver, 10);
	wait.until(ExpectedConditions.visibilityOfElementLocated(recentDepositLocator));
	boolean status = driver.findElement(recentDepositLocator).isDisplayed();
	if(status==true) {
	System.out.println("Test Passed");
	} else System.out.println("Test Failed!!");
	
	
	
	//Dashboard page should display

	driver.close();
	driver.quit();
	
	
	}
	
}



#techfios-testNG
