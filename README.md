# Sample Code Snippet (Java + Selenium + TestNG)

```public class SignUpPage {
private WebDriver driver;

// Locators 
private By  firstnameField = By.id("firstname");
private By  lastnameField = By.id("lastname");
private By  dateofbirthField = By.id("dateofbirth");
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

public class SignupTest extends BaseTest {
```
