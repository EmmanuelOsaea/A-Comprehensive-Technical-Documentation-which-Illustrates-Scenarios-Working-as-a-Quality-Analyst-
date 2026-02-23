# Sample Code Snippet (Java + Selenium + TestNG) for Automation Framework Development for E-commerce Web Application

```
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.testng.Assert;
import org.testng.annotations.DataProvider;
import org.testng.annotations.Test;


public class SignUpPage {
private WebDriver driver;

// Locators 
private By  firstnameField = By.id("firstname");
private By  lastnameField = By.id("lastname");
private By  dateofbirthField = By.id("dateofbirth");
private By  emailField = By.id("email")
private By  passwordField = By.id("password")
private By  confirmpasswordField = By.id("confirmpassword");
private By  signupButton = By.id("signupBtn");

public SignUpPage(WebDriver driver) {
this.driver = driver;
}

public void enterFirstname(String firstname) {
driver.findElement(firstnameField).sendKeys(firstname);
}


public void enterLastname(String lastname) {
driver.findElement(lastnameField).sendKeys(lastname);
}

public void enterDateofbirth(String dateofbirth) {
driver.findElement(dateofbirthField).sendKeys(dateofbirth);
}

public void enterEmail(String email) {
driver.findElement(emailField).sendKeys(email);
}


public void enterPassword(String password) {
driver.findElement(passwordField).sendKeys(password);
}

public void confirmPassword(String password) {
driver.findElement(confirmpasswordField).sendKeys(confirmpassword);
}


public void clickSignup() {
driver.findElement(signupButton).click();
}
}

public class SignUpTest extends BaseTest {

@Test(dataProvider = "signupData")
public void testValidSignup(String firstname, String lastname, String dateofbirth, String email, String password, String confirmpassword) {
SignUpPage signupPage = new SignUpPage(driver);
signupPage.enterFirstname(firstname);
signupPage.enterLastname(lastname);
signupPage.enterDateofbirth(dateofbirth);
signupPage.enterEmail(email);
signupPage.enterPassword(password)
signupPage.enterConfirmpassword(confirmpassword);
signupPage.clickSignup();

// assert user is redirected to dashboard
Assert.assertTrue(drive.getTitle().contains("Dashboard"));
}

@Dataprovider(name = "signupData")
public Object[] [] getSignUpData() {
return new Object [] [] {

{ "Zachtu", "Zuch", "01/02/1885", "zachtu.zuch@example.com", "Password224"}
{ "Glaur", "Gluch", "04/06/1882", "glaur.gluch@example.com", "Password666"}
};
}
}
```

# API Testing to Validate Maintenance and System Storage

import io.restassured.RestAssured
import io.restassured.http.ContentType;
import io.restassured.response.Response;
import org.testng.Assert;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.Test;

public






