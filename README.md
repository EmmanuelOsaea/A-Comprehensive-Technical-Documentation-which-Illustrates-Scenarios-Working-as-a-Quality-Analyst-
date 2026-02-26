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
{ "Glaur", "Gluch", "04/06/1882", "glaur.gluch@example.com", "Password222"}
};
}
}
```

# API Testing to Validate Maintenance and System Storage(Bonus)
```
import io.restassured.RestAssured
import io.restassured.http.ContentType;
import io.restassured.response.Response;
import org.testng.Assert;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.Test;

public class MaintenanceStorageApiTest {

@BeforeClass {
public void setup() {
// Base URL for my system's api
RestAssured.baseURL = "https://github.com/EmmanuelOsaea/Quiz-app-Front-end-Web-design-";
}

@Test
public void testTriggerMaintenanceCleanup() {
// Step 1: Trigger maintenance cleanup via POST request
Response response = RestAssured.given()
.contentType(ContentType.JSON)
.body("{\"operation\":\"cleanup\"}")
.when()
.post("/api/maintenance/trigger")
.then()
.statusCode(200) // Expect success status
.extract()
.response();

// Step 2: Verify response message
String message = response.jsonPath().getString("message");
Assert.assertEquals(message, "Cleanup started successfully", "Maintenance trigger message mismatch");
}

@Test(dependsOnMethods = "testTriggerMaintenanceCleanUp")
public void testCheckStorageStatus() {
// Step 3: Check storage usage and status
Response response = RestAssured.given()
 .when()
 .get("/api/storage/status")
 .then()
 .statusCode(200)
 .extract()
 .response();
 
@Test(dependsOnMethods = "testTriggerMaintenanceCleanup")
public void testCheckupStorageStatus() {
// Step 4: Verifies storage capacity and used space
int totalCapacity = response.jsonPath().getInt("totalCapacityGB");
int usedSpace = response.jsonPath().getInt("usedSpaceGB");
boolean isHealthy = response.jsonPath().getInt("isHealthy")

Assert.assertTrue(totalCapacity > 0, "Total capacity should be greater than zero")
Assert.assertTrue(usedSpace >= 0 && usedSpace <= totalCapacity, "Used space should be used within capacity");
Assert.assertTrue(isHealthy, "Storage system should be healthy");
}

@Test(dependsOnMethods = "testCheckStorageStatus")
public void testValidateStoredDataIntegrity() {
// Step 5: Verify data integrity by fetching a sample stored item
String sampleDataId = "data678";

Response response = RestAssured.given()
.when()
.get("/api/storage/data" + sampleDataId)
.then()
.statusCode(200)
.extract();
.response();

String dataId = response.jsonPath().getString("id");
String checksum = response.jsonPath().getString("checksum");
String expectedChecksum = "dbf678rst"; // Expected checksum for verification

Assert.assertEquals(dataId, sampleDataId, "Data id should be similar");
Assert.assertEquals(checksum, expectedChecksum, "Data checksum should be similar to the expected value");
}
}
```


# Api Testing to Validate Integrations & System Communication

# a) Configuration 
 # (ApiConfig.java)
```
package com.example.config;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.beans.factory.annotation.Value

@Configuration
public class ApiConfig {

@Value("${api.base.url}")
private String baseUrl;

public String getBaseUrl() {
return baseUrl;
}
}
```
# b) HTTP Client Wrapper
# (ApiClient.java)
```
package com.example.client;

import org.springframework.ResponseEntity;
import org.springframework.stereotype.Component;
import org.springframework.web.client.RestTemplate;

@Component
public class ApiClient {

private final RestTemplate restTemplate = new RestTemplate();

public ResponseEntity<String> get(Stringurl, Object request) {
return restTemplate.getForentity(url, String.class);
}

public ResponseEntity<String> post(Stringurl, Object request) {
return restTemplate.getForentity(url, request, String.class);
}

}
```
# c) Integration Service
# (IntegrationService.java)

```
package.com.example.service;

import com.example.client.ApiClient;
import com.example.client.ApiConfig;
import org.springframework.http.ResponseEntity;
import org.springframework.stereotype.Service;

@Service

public class IntegrationService {

private final ApiClient apiClient;
private final ApiConfig apiConfig;

public IntegrationService(ApiClient apiClient, ApiConfig apiConfig) {
this.apiClient = apiClient;
this.apiConfig = ApiConfig;
}

public ResponseEntity<String> sendData(Object data) {
String url  = apiConfig.getBaseUrl() + "/data";
return.apiClient.post(url, data);
}

}
```

# d) Api Integration Tests
# (ApiIntegrationsTests.java)
```
package com.example.tests;

import com.example.service.IntegrationService;
import org.junit.jupiter.api.Assertion;
import org.junit.jupiter.api.test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.context.ResponseEntity

@SpringBootTest
public class ApiIntegrationTest {

@AutoWired
private IntegrationService integrationService;

@Test
public void testSystemStatusEndpoint() {
     ResponseEntity<String> response = integrationService.getSystemStatus();
     Assertions.assertEquals(200, response.getStatusCodeValue());
     Assertions.assertTrue(response.getBody().contains("status"));
}

@Test
public void testSendDataEndpoint() {

ResponseEntity<String> response = integrationService.sendData(sampleData);
Assertions.assertEquals(200, response.getStatusCodeValue());
Assertions.assertTrue(response.getBody().contains("status"));
}
}
```
# 3. Configuration File
# ( application.properties )
```
api.base.url=https://github.com/EmmanuelOsaea/Quiz-app-Front-end-Web-design-
```

# 2. Key Components

# a) Api Configuration
# (ApiConfig.java)
```
package com.example.config;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.factory.annotation.Configuration;

@Configuration
public class ApiConfig {

@Value("${api.base.url}")
private String baseUrl;

public String getBaseUrl() {
return baseUrl;
}
}
```

# b) Database Configuration
# ( DatabaseConfig.java )
 ```
 package com.example.config;

 import org.springframework.context.annotation.Bean;
 import org.springframework.context.annotation.Configuration;
 import org.springframework.jdbc.core.JdbcTemplate;
 import javax.sql.DataSource;
 import org.springframework.boot.jdbc.DataSourceBuilder;
 
 @Configuration
 public class DatabaseConfig {

  @Bean
  public Datasource datasource() {
  return DatasourceBuilder.create()
   .url("jdbc:mysql://localhost:3306/yourdb")
   .username("youruser")
   .password("yourpassword")
   .driverClassName("com.mysql.cj.jdbc.Driver")
   .build();
 }

@Bean
public JdbcTemplate JdbcTemplate(Datasource dataSource) {
return new JdbcTemplate(dataSource);
}
}
```

# c) API Client (ApiClient.java)
```
package com.example.client
import org.springframework.http.ResponseEntity;
import org.springframework.stereotype.Component;
import org.springframework.web.client.RestTemplate;

@Component
public Class ApiClient {

private final RestTemplate restTemplate = new RestTemplate();

public ResponseEntity<String> get(String url) {
return restTemplate.getForEntity(url, String.class);
}

public ResponseEntity<String> get(String url) {
return restTemplate.getForEntity(url, String.class);
}
}
```

# d) Database Repository
# (DatabaseRepository.java)
```
package.com.example.repository;

import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.stereotype.Repository;

@Repository
public class DatabaseRepository {

private final JdbcTemplate jdbcTemplate;

public DatabaseRepository(JdbcTemplate jdbcTemplate) {
   this.jdbcTemplate = jdbcTemplate;

public int countRecords(string tableName) {
String sql = "SELECT COUNT(*) + "FROM" + tableName + " WHERE id = ?";
return jdbcTemplate.queryForObject(sql, Integer.class);












