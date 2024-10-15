# Advanced Software Engineering

## Katalon Studio - Mobile Testing

### Application Under Test (AUT)

- **AUT**: Sunflower.apk (available on Moodle)

### Goals

- Design, plan, and execute test cases
- Use a mobile testing environment

## Mobile Execution Environment

### Android Execution Environment

- **SDK**: Android device or emulator
- **Android Studio**: Device Manager >> Emulator

### Appium and Drivers

To install Appium:

```bash
npm install appium@1.22.3
```

For more details, visit:  
<https://docs.katalon.com/katalon-studio/docs/mobile-on-windows.html>

### Update Katalon Studio Preferences

- Go to **Katalon** > **Mobile** > **Appium Directory**
- Example: `$/usr/local/lib/node_modules/appium`

## Setup Testing Environment

### Appium 2.0

- [Katalon Blog: Appium 2.0](https://katalon.com/resources-center/blog/appium-2-0)
- [Katalon Documentation: Appium 2.x Setup](https://docs.katalon.com/docs/proof-of-concept/execute-mobile-tests-with-appium-2.x-in-katalon-studio-poc)

## Mobile Testing

### Scenario: Check Core Content on Screen

1. Start the AUT (Sunflower.apk)
2. Validate if the “Add Plant” button exists
3. Close the AUT

**Steps**:

1. **Set up a mobile project**
2. **Create the test case**
3. **Record the test case** (Mobile Recorder)
4. **Verification in the test case**: Replace “Tap” with “Verify Element Exists”
5. **Run the test case**

## Work Proposal

### Scenario 1: Check Eggplant Details

1. Start the AUT (Sunflower.apk)
2. Tap the **Add Plant** button
3. Tap the **Eggplant** button
4. Verify if the text at the top of the details screen is **Eggplant**
5. Close the AUT

### Scenario 2: Add a Plant to Your Garden

1. Start the AUT (Sunflower.apk)
2. Add a plant to your garden
3. Close the AUT

- **Task**: Design and create test cases for each scenario.
- **Goal**: Group test cases into test suites.

## Sample Feature Files

### `CheckCoreContent.feature`

```gherkin
Feature: Check Core Content
  As a user
  I want to start the AUT (Sunflower.apk)
  So that I can start interacting with the AUT
  
Scenario: Check "Add Plant" button is present
  Given I have the device ready
  When I start the application
  Then I verify that the button "Add Plant" is present
  And I close the AUT
```

### `CheckEggPlantDetails.feature`

```gherkin
Feature: Check Eggplant Details
  As a user
  I want to choose the Eggplant from the list
  So that I can see the details for the Eggplant

Scenario: See Eggplant Details
  Given I start the application
  When I tap the "Add Plant" button
  And I choose the Eggplant button
  Then I see that the Eggplant details are shown
  And I close the AUT
```

### `CheckPlantDetails.feature`

```gherkin
Feature: Check Plant Details
  As a user
  I want to choose a plant from the list
  So that I can see the details for that plant

Background:
  Given I start the application
  When I tap the "Add Plant" button

Scenario Outline: See Plant Details
  When I tap the <plantname> image button
  Then I see that the <plantdetails> details are shown
  And I close the AUT

Examples:
  | plantname      | plantdetails   |
  | Apple          | Apple          |
  | Avocado        | Avocado        |
  | Beet           | Beet           |
  | Bougainvillea  | Bougainvillea  |
  | Cilantro       | Cilantro       |
  | Eggplant       | Eggplant       |
```

## Code Reuse

You can reuse the same **Step Definitions** by updating:

1. The name of the objects
2. The step definition
3. Clean up other step definitions

### `CheckPlantDetailsStepDefs.groovy`

```groovy
@When("I tap the (.*) image button")
def I_tap_the_image_button(String plantname) {
    Mobile.tap(findTestObject('android.widget.TextView0 - ' + plantname), 0)
}

@Then("I see that the (.*) details are shown")
def I_verify_the_status_in_step(String plantdetails) {
    Mobile.verifyElementText(findTestObject('android.widget.TextView0 - ' + plantdetails), plantdetails)
    Mobile.closeApplication()
}
```
