Agile CRM - Web Grabbers - Demo/Help
===================
#What are web rules?

Web rules allows you to perform certain actions when people visit your website. 

For example, when there is an anonymous visitor on the pricing page, pop up a signup form. Or, when a contact in your Agile CRM visits your support page, put him into a campaign that asks if they need any help.

#Prerequisites
Enable tracking code on your website as per instructions here - https://github.com/agilecrm/javascript-api/


#Usage

You can configure web rules in Agile CRM at 
https://YOUR_DOMAIN.agilecrm.com/#webrules


##Defining conditions

###Page Conditions:

####Page URL
- Is: You need to provide a complete URL here. his condition evaluates to true when the web page url is exactly the same as input URL
- Matches: This condition is satisfied when the URL of the page contains the input string.

####Referrer URL
The referrer or referring page is the URL of the previous webpage from which a link was followed.
- Is: You need to provide a complete URL here. This condition is true when the input URL completely matches the referrer of the current web page.
- Matches: This condition evaluates to true referrer URI contains the input string
is’nt: You need to provide a complete URL here. This condition is true when the input URL does not completely matches the referrer of the current web page.

####Visit
- First time: The visitor on the web page is visiting the page for the first time.
- Recurring: The visitor has visited the web page more than once in a session.

###Contact Data

For these set of conditions to work, you should have already setup visitor tracking on your website explained here (in section 1).
There conditions work only for visitors who are already being tracked and a contact is present for them in Agile CRM.
- Tag:
Checks the tags for the contact in your Agile CRM
- Tag and Created Date:
Checks the tag and its creation date in Agile CRM (example, people who have ‘Signup’ tag in last 1 month)
- Score:
Checks for the Score value of the contact.
- Created: 
This checks for the contact creation date in Agile CRM. 
- Company: 
Checks for the Company property of the Contact.
- Job Title: 
Checks the job title of the contact
- Owner: 
Checks the owner of the contact
- Custom Fields: 
You can use them to check the custom  field value of the contact. Only the custom fields that defined as *searchable* will come up here.

##Defining Actions
The defined actions are performed when all the conditions mentioned are satisfied. One can define multiple actions to be performed.
Actions are of multiple types as explained here below.
###Popups
This action displays a popup (modal window or a small corner popup) on the web page when all the web rules related to that web page are satisfied.

You can choose on of the 3 types of popup options available.
####Modal Popup
This shows a Model popup i.e a popup at the center of the screen with rest of the window greyed out. 
You can choose from 3 options here
- Confirmation
Shows a popup with a message and Yes/No buttons.
- Information
This displays information modal window with an Ok button.
- Custom HTML
This option can used to provide custom HTML code. The html content will be rendered inside the popup.

####Noty Message
This action displays a simple Noty popup on the web page at the specified location. You can use html tags for the content inside the popup.

####Form on website
Displays a predefined form on web page inside the modal window. You need to provide the ID for the form present in your html page.

### Campaign Actions

#### Add to Campaign:
Puts the contact (visitor)  into a Campaign already defined in Agile.

#### Remove from Campaign: 
Removes the contact (visitor) from the a Campaign if already present.

### Tags Actions

#### Add Tags:  Adds the specified Tags to the contact (visitor)

#### Remove Tags: Removes the specified Tags from the contact if present.

### Score

#### Add Score: Adds a set score to the contact (visitor)

#### Subtract Score: Decreases the contact score.

### Execute Code - Action

#### Javascript
You can provide javascript to be executed on the web page.  You can call javascript methods present on your webpage here or write some custom code.

## Timing your actions
For popup actions, you can time when to show the popups 
- Immediate: Shows the popup immediately after the page loads.
- After Certain Time: Show after a specified time in seconds.
- On Starting Scroll: Shows the popup when the user starts scrolling the page
- On reaching end of Page: Shows the popup when user reaches the bottom of the page.
