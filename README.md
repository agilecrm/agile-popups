Agile CRM - Web Rules
===================
#What are web rules?

Web rules allows you to perform certain actions when people visit your website. 

For example, when there is an anonymous visitor on the pricing page, pop up a signup form. Or, when a contact in your Agile CRM visits your support page, put him into a campaign that asks if they need any help.

#Setup.

Setup this visitor tracking and web rules code on your website 

```javascript
<script type="text/javascript"
 src="https://YOUR_DOMAIN.agilecrm.com/stats/min/agile-min.js"> 
</script>
<script type="text/javascript"
 src="https://d2l6lw2yloivu1.cloudfront.net/web-grabbers/lib/head.load.min.js">
</script> 
<script type="text/javascript"
 src="https://d2l6lw2yloivu1.cloudfront.net/web-grabbers/agile-webrules.js">
</script>
<script  type="text/javascript">
    function all() {
        _agile.set_account('YOUR_API_KEY', 'YOUR_DOMAIN');
        // _agile.track_page_view(); only if tracking is enabled
        _agile_webrules();
        }
    if (window.addEventListener) 
    window.addEventListener("load", all, false);
    else if (window.attachEvent)
     window.attachEvent("onload", all);
    else window.onload = all;
</script>
```
You need to change  YOUR_DOMAIN (in 2 places) & YOUR_API_KEY accordingly. 



#Usage

##Defining conditions

You need to define condition(s) first, and then choose the action(s) that need to be performed when *all* the conditions are met. 
For defining the conditions, you have the following options.

###Page Conditions:

Conditions related to which page the user is on referrer URL.

####Page URL
- Is: You need to provide a complete URL here. This condition evaluates to true when the web page url is exactly the same as input URL
- Matches: This condition is satisfied when the URL of the page contains the input string.

####Referrer URL
The referrer or referring page is the URL of the previous webpage from which a link was followed.
- Is: You need to provide a complete URL here. This condition is true when the input URL completely matches the referrer of the current web page.
- Matches: This condition evaluates to true if the referrer URL contains the input string. You do not need to provide a complete URL here. 

####Show
- Every time: The action is performed everytime
- Once per session: The action is performed once per session (till browser is reopened). Session cookie is stored to ensure that it's being shown only once. 
- Only Once: The visitor is shown only once per browser.

###Contact Data

For these set of conditions to work, you should have already setup visitor tracking on your website explained here - https://github.com/agilecrm/javascript-api (in section 1). You do not to put up the code present there since the above code covers that.
There conditions work only for visitors who are already being tracked and exist as a Contact in Agile CRM.
- Tag:
Checks the tags for the contact in your Agile CRM
- Tag and Created Date:
Checks the tag and its creation date in Agile CRM (for example, people who have the ‘Signup’ tag in the last one month)
- Score:
Checks for the value of the Lead Score of the contact.
- Created: 
Checks for the contact creation date in Agile CRM. 
- Company: 
Checks for the Company name of the Contact.
- Job Title: 
Checks the job title of the contact.
- Owner: 
Checks the owner of the contact (who would be a user of the CRM).
- Custom Fields: 
Checks the values in custom fields for the contact. Only the custom fields that defined as *searchable* will come up here.

##Defining Actions
The defined actions are performed when all the conditions mentioned are satisfied. One can define multiple actions to be performed.
Actions are of multiple types as explained here below.
###Popups
This action displays a popup (modal window or a small corner popup) on the web page when all the web rules related to that web page are satisfied.

You can choose on of the 3 types of popup options available.
####Modal Popup
This shows a modal popup i.e a popup at the center of the screen with rest of the window greyed out. 
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
Puts the contact (visitor) into a Campaign already defined in Agile CRM.

#### Remove from Campaign: 
Removes the contact (visitor) from the a Campaign if already present.

### Tags Actions

- Add Tags:  Adds the specified Tags to the contact (visitor)

- Remove Tags: Removes the specified Tags from the contact if present.

### Score

- Add Score: Adds a specific score to the contact (visitor).

- Subtract Score: Decreases the contact score.

### Execute Code

#### Javascript
You can provide javascript to be executed on the web page.  You can call javascript methods present on your webpage here or write some custom code.

## Timing your actions
For popup actions, you can time when to show the popups 
- Immediate: Shows the popup immediately after the page loads.
- After Certain Time: Shows after a specified time in seconds.
- On Starting Scroll: Shows the popup when the user starts scrolling the page
- On reaching end of Page: Shows the popup when user reaches the bottom of the page.
- About to exit page: Shows the popup for the abandoning visitors.


#Controlling Popups using API

You can close the popup, initialize a form using the contact data (if already present) or save the form data to Agile CRM.

```
_agile_close_modal() // Closing Popup
_agile_load_fields() // Load fields
_agile_save_form(boolean should_close, function callback) // Save and execute callback if any. should_close determines if the popup should be closed automatically.
```

#Forms & Agile Sync

Forms are now supported in the popups. 

## Saving Form Fields to Agile

For Agile to correctly identify the mapping, you should mark the attribute of the input field with the name of field in Agile.

```
<input type="text" name="name" agile-field="first_name" required>
```

If you are mapping to a custom field, you should use "agile-custom-field" as the attribute
```
<input type="number" name="form-quantiy" agile-field="quantity" required>
```

## Initiating Fields in Popup with the Contact Data

You can initialize the forms with the data of the contact (if available) in the forms.

```
_agile_load_fields() 
```
