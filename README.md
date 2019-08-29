# TSYS Integration with CiviCRM Documentation

Throughout this example we'll use a WordPress site. The installation process may differ slightly for each CMS, but should be relatively similar.

You can use the companion [video walkthrough](TSYS_CiviCRM_InstallationWalkthrough.mp4) to see many of these steps narrated in action.

This document illustrates the installation procedures at the time of development. These methods may change, so the best source for information on the installation of extensions in CiviCRM are the official documentation pages found here: https://docs.civicrm.org


# Preparations

Make sure you have identified the specific website to use, and complete these steps:

* Login to the CMS (WordPress, Drupal, or Joomla) as an administrator

* Navigate to the CiviCRM dashboard
Click on the CiviCRM icon and link from the CMS menu.
In WordPress, find the left menu bar and select CiviCRM.
In Drupal, find the Modules menu and select CiviCRM.
In Joomla, find the Extensions menu and select CiviCRM.

* Check for system errors 
Navigate to the System Status page using the top Civi menu Administer > Administration Console > System Status
If there are any Errors, the installation process may not complete as expected. Contact a CiviCRM specialist before proceeding.

![](/Screenshots/SystemStatus.png)


# Install TSYS extension

## Identify the Extensions directory

Use the Civi menu Administer > System Settings > Directories to identify the extension directory.
![](/Screenshots/Directories.png)

The last field on this page is labeled "Extensions Directory". To get the full file path, click the ? symbol in the green text to find what path [civicrm.files] has. Add that together with any text afterwards to get the full file path.

![](/Screenshots/DirectoryPath.png)

Example:
Extensions Directory [civicrm.files]/ext/

We know from the Path Variable box that [civicrm.files] =  	/srv/www/cayandemo/public_html/wp-content/uploads/civicrm

So we'll take that and add the '/ext/' to the end to get:
 	/srv/www/cayandemo/public_html/wp-content/uploads/civicrm/ext/

This is the file path to use when installing the extension in the next step.

## Switch to the Command Line
* Connect by SSH to your web server 
Connect to the web server and navigate to the extension directory found previously.

Ex: 
~~~
      ssh webmaster@website.com
      cd /srv/www/cayandemo/public_html/wp-content/uploads/civicrm/ext/
~~~

* Download the extension file 

Use the latest version found on (https://github.com/aghstrategies/com.aghstrategies.tsys/archive/v1.1.0.zip).

*The specific file path may change as the software is updated. Please check this link for the latest archive: https://github.com/aghstrategies/com.aghstrategies.tsys/archive and replace "v1.1.0.zip" with the latest stable version.

~~~
      sudo wget https://github.com/aghstrategies/com.aghstrategies.tsys/archive/v1.1.0.zip
~~~

This will download the file "master.zip" to this directory which will need to be unzipped.

* Unzip the extension file
~~~
      sudo unzip master.zip
~~~

You are finished with the command line, so you can leave by typing 'exit'

## Switch to the web interface
Switch back to the web browser to install the TSYS extension through CiviCRM's extension interface by using the Civi menu Administer > System Settings > Extensions

![](/Screenshots/ExtensionPage.png)

* Click the Refresh button to display the TSYS extension

![](/Screenshots/RefreshExtensions.png)

Click the Install link on the right of the TSYS lsiting and click Install again on the following page.

![](/Screenshots/InstallExt.png)

You'll be returned to the Extensions page, with TSYS Enabled

![](/Screenshots/ExtEnabled.png)

# Configure a TSYS Payment Processor

Now that Civi has the capability of talking to TSYS, we need to configure a Civi payment processor to use TSYS.

* Use the Civi menu to navigate to Administer > System Settings > Payment Processors
* Click the Add Payment Processor button
![](/Screenshots/NavigateProcessors.png)



## Payment Processor Fields

|Field|Value|Notes|
|---|---|---|
|Payment Processor Type | TSYS ||
|Name | Displayed by default on public pages when the payment processor is chosen | Consider using something generic like "Credit Card"|
|Description | Open text field | Used for your own organization, not required|
|Financial Account| Payment Processor Account |Default is typical, use this unless you have a reason to change it|
|Payment Method| Credit Card | This information shows up on any contribution record created using this processor as the payment method. Options may be added by the user on the fly using the wrench icon|
|Is this Payment Process active?|check|If checked, this processor will be available to use on your site to take payments and donations|
|Is this Payment Processor the default?|check|If checked, any new contribution page or event created will assume credit card payments will be taken using this TSYS processor|
|Accepted Credit Card Types| Check all: Visa, MasterCard, Amex, Discover ||

![](/Screenshots/ConfigureProcessor.png)

## Processor Details for Live Payments
Merchant Name: This is provided by your Cayan representative
Web API Key: This is provided by your Cayan representative
Merchant Site Key: This is provided by your Cayan representative
Merchant Site ID:	This is provided by your Cayan representative
Site URL:	https://cayan.accessaccountdetails.com/
Recurring Payments URL: https://cayan.accessaccountdetails.com/

![](/Screenshots/ConfigureDetails.png)

## Processor Details for Test Payments

Repeat all the information above

Merchant Name: This is provided by your Cayan representative (same as above)
Web API Key: This is provided by your Cayan representative (same as above)
Merchant Site Key: This is provided by your Cayan representative (same as above)
Merchant Site ID:	This is provided by your Cayan representative (same as above)
Site URL:	https://cayan.accessaccountdetails.com/
Recurring Payments URL: https://cayan.accessaccountdetails.com/

![](/Screenshots/ConfigureTest.png)

Click Save

# Using a Processor on a web page
Now that CiviCRM can talk to TSYS with a Payment Processor, we need to add that processor to a page to be able to take credit cards.

## Adding to a contribution page

First, find the contribution page you want to edit from the Civi menu Contributions > Manage Contribution Pages

![](/Screenshots/NavigateContributions.png)

On the right side of the listing, click the Configure Link and select Contribution Amounts

![](/Screenshots/ConfigureContribution.png)

Next to the Payment Processor field, you should see your new payment processor available. Check the box next to it and uncheck any others that may be selected already.

![](/Screenshots/SelectCredit.png)

Click the Save and Done button. This page will now be able to take credit card payments through TSYS.

## Adding to an event registration page
First, find the event you want to edit from the Civi menu Events > Manage Events

On the right side of the listing, click the Configure Link and select Fees

![](/Screenshots/EventFees.png)

Next to the Payment Processor field, you should see your new payment processor available. Check the box next to it and uncheck any others that may be selected already.

![](/Screenshots/CreditEvent.png)

Click the Save and Done button. This page will now be able to take credit card payments through TSYS.

# Completing a transaction from the backend
Sometimes you will need to process transactions without the need for completing a web page form like a donation or event registration page. To administratively process payments from the back end you will begin by finding the contact record of the individual or organization making the transaction. Donations and Event Registrations are handled separately, so make sure you do not record an event registration fee as a donation.

Identify and navigate to the target contact record.

## Backend Contribution

![](/Screenshots/BackendContribution.png)

On the contact record select the Contributions tab, then click the "Submit Credit Card Contribution" button.

Make sure that the name you used to set up the process (Credit Card in our example) is selected in the dropdown for Payment Processor. Enter the remaining required fields and click "Save" or "Save and New" to execute the transaction.

## Backend Event Registration

![](/Screenshots/BackendEvent.png)

On the contact record select the Contributions tab, then click the "Submit Credit Card Contribution" button.

Event - Select the name of the event from the first dropdown.
Participant Role - Set this to "Attendee" unless there's a reason to change it.
Ensure that the name you used to set up the process (Credit Card in our example) is selected in the dropdown for Payment Processor. 
Enter the remaining required fields and click "Save" or "Save and New" to execute the transaction.


# Cancelling a recurring contribution
Recurring contributions are held on the contact record under the Contributions tab, in a sub-tab called Recurring Contributions.

![](/Screenshots/CancelRecurring.png)

Click the Cancel link on the right side of the recurring contribution to cancel future transactions.

# Refunding a contribution
Refunds to credit cards must be initiated through your TSYS interface. At this time refunds can not be initiated from CiviCRM.

After you refund a transaction, you will need to record that refund in CiviCRM. Use the Civi menu Search > Find Contributions to enter contribution details that will allow you to click View on the contribution record. It should look something like this:

![](/Screenshots/RefundContribution.png)

Click the Edit button on the bottom of the record

Change Contribution Status to Refunded, and make any other necessary edits and click Save

![](/Screenshots/Refunded.png)

# Troubleshooting

## "My recurring contributions are not going through, but regular contributions are working fine"

This is likely due to a problem with the scheduled job for TSYS in CiviCRM. Try running the job manually and then re-enabling it from the Scheduled Job's page. Get here from the Civi menu Administer > System Settings > Scheduled Jobs

![](/Screenshots/ScheduledJobs.png)

Find the job labeled "TSYS Payments Recurring Contributions (Daily)" and check the information there about the last time it was run and whether or not it is enabled.


### Mannually run the TSYS job
Use the "more" link to select "Execute Now"
This should run any scheduled payments, including any that have been queued up since the last run.

![](/Screenshots/RunScheduledJob.png)

### Enable the TSYS job
If the job runs successfully when executed manually, click the "edit" link. 
Check the "Is this Scheduled Job active?" box if it is not checked.

![](/Screenshots/ActivateScheduledJob.png)

## Official Documentation Links
The full suite of official documentation sets for CiviCRM can be found https://docs.civicrm.org

These specific links are the most relevant places you may need to reference related to the TSYS integration.

* System Administrator's Guide to [Payment Processors](https://docs.civicrm.org/sysadmin/en/latest/setup/payment-processors/)
* User's Guide to [Payment Processors](https://docs.civicrm.org/user/en/latest/contributions/payment-processors/)
* System Administrator's Guide to [Extensions](https://docs.civicrm.org/sysadmin/en/latest/customize/extensions/)
* User's Guide to [Extensions](https://docs.civicrm.org/user/en/latest/introduction/extensions/)
