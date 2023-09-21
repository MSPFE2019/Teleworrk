### How to Create a Power App Using Microsoft PowerApps

#### 1. **Initial Navigation**:
   - Visit [office.com](https://www.office.com/).
   - Click on the waffle (App Launcher), a grid-like icon, located at the upper left-hand corner.
   - Scroll and select 'Power Apps'.

#### 2. **Setting Up the App**:
   - Once in Power Apps, click on 'Create new app' and opt for 'Canvas app'.
   - Choose between two Canvas app formats: phone or tablet. Select 'Tablet'.
   - Give your app a meaningful name, for example, 'Telework Agreement Form'.
   - Pick the App and set the property to “On Start”. Insert `Set(vardisplay,false)`. This command sets up an initial variable that we'll use later in our design.

#### 3. **Adding a Data Source**:
   - On the left navigation, click on the cylinder icon (representing data sources).
   - Click 'Add data source' and choose the green 'SharePoint' icon.
   - Enter the URL of your SharePoint site on the right side and confirm its accuracy.
   - When prompted, choose the relevant SharePoint list for your app.
   - Press 'Save' to integrate your data source with your Power App.

#### 4. **Designing the Form**:
   - Navigate to scr_main and in the top menu, select `Insert` -> `INPUT` -> `Edit Form`.
   - Add the following fields in the specified order to capture essential details:
      - TeleWorkerType
      - Telework
      - TeleworkLocation
      - SecondaryLocation
      - ODJFSOffice
      - Monday to Saturday (work schedule)
      - Title (for unique identification)
   - Adjust the form settings on the right:
     - Set the layout to 'Two columns'.
     - Organize the layout to 'Vertical'.
     - Set the form mode to 'New'.

#### 5. **Customizing Fields**:
   - For each 'Day' field, access its card and click on 'Data card value'.
   - Provide a 'Hint Text' for each day, e.g., "Time Format 8:00 am - 5:00 pm".
   - For the 'Title' field, modify the default value with the formula: `User().FullName&"-"&Now()`. This creates a unique title by combining the user's name and the current timestamp.

#### 6. **Button Creation and Configuration**:
   - Choose `Insert` and select 'Button' to position a button at the bottom.
   - Update the 'OnSelect' property in the formula bar to: `OnSelect - Set(vardisplay, true)`. This command sets up an action for the button.
   - Add a blank container for the disclaimer and configure its visible property to vardisplay.
   - Within this container, insert a label for the disclaimer text and a checkbox for user consent. Select both the container and label, right-click, and choose ['Group'](https://github.com/MSPFE2019/Teleworrk/blob/main/Grouping) for better organization.
   - Configure the checkbox so that 'Oncheck' is set to: `Set(vardisplay, false);Set(varSubmit, DisplayMode.Edit)`.
   - Update the 'Submit' button's display mode property to the 'varSubmit' variable, toggling its visibility based on the disclaimer's confirmation.

#### 7. **Modify the Submit Button**:
   - Access the 'Submit' button.
   - In the formula bar, input the following combined command:
```PowerApps
SubmitForm(Form2);
Trace("Form submitted by: " & User().FullName & " for item: " & Form2.LastSubmit.Title, TraceSeverity.Information);
ResetForm(Form2);
```
The `Trace()` function logs each submission, recording the user's name and the item's title, which aids in auditing and troubleshooting.

#### 8. **Enforcing Required Fields**:

**Using SharePoint**:
1. Visit your SharePoint site and access the associated list.
2. Edit the column (field) you wish to make mandatory.
3. Select 'Column settings' > 'Edit'.
4. Switch 'Require that this column contains information' to 'Yes'.
5. Save your changes and refresh your Power App to implement them.

**Using Power Apps**:
1. Open the screen containing the form.
2. Select the desired field.
3. Change the 'Required' property from `false` to `true`.
4. Optionally, tailor the 'OnError' property for personalized error messages.

**Note**: Ensure the required fields in SharePoint align with those in Power Apps to maintain data consistency.

#### 9. **Creating a Title Bar**:
   - Access the screen where you want the title bar.
   - Insert a rectangle using `Insert` > `Icons` to serve as the background.
   - Customize its appearance to your preference.
   - Add a label for the title and adjust its settings.
   - You can also insert icons or additional details for enhanced aesthetics.
   - Group all the title bar elements together for streamlined management.
   - Duplicate and paste the title bar onto other screens as needed, updating the label to reflect each screen's purpose. The title bar provides a consistent header and aids in user navigation.

[Create flow](https://github.com/MSPFE2019/Teleworrk/blob/main/Flow)
