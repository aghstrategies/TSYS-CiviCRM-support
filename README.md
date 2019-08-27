# TSYS Integration with CiviCRM Documentation

Throughout this example we'll use a WordPress site. The installation process may differ slightly for each CMS, but should be relatively similar.

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
~~
      ssh webmaster@website.com
      cd /srv/www/cayandemo/public_html/wp-content/uploads/civicrm/ext/
~~

* Download the extension file 

Use the latest version found on (https://github.com/aghstrategies/com.aghstrategies.tsys/archive/v1.1.0.zip).

*The specific file path may change as the software is updated. Please check this link for the latest archive: https://github.com/aghstrategies/com.aghstrategies.tsys/archive and replace "v1.1.0.zip" with the latest stable version.

~~
      sudo wget https://github.com/aghstrategies/com.aghstrategies.tsys/archive/v1.1.0.zip
~~

This will download the file "master.zip" to this directory which will need to be unzipped.

* Unzip the extension file
~~
      sudo unzip master.zip
~~

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

## Processor Details for Test Payments

Repeat all the information above

Merchant Name: This is provided by your Cayan representative (same as above)
Web API Key: This is provided by your Cayan representative (same as above)
Merchant Site Key: This is provided by your Cayan representative (same as above)
Merchant Site ID:	This is provided by your Cayan representative (same as above)
Site URL:	https://cayan.accessaccountdetails.com/
Recurring Payments URL: https://cayan.accessaccountdetails.com/

Click Save

## Using a Processor on a Civi page


Backend donation spits out rejection code
Could be 

CiviCRM Scheduled Job that check for recurring contributions

How to cancel a recurring contribution
Create and Cancel a recurring contribution

Example for each kind of transaction

# Troubleshooting

## "My recurring contributions are not going through, but regular contributions are working fine"
  This is likely due to a problem with the scheduled job for TSYS in CiviCRM. Try running the job manually and then re-enabling it from the Scheduled Job's page. Get here from the Civi menu Administer > System Settings > Scheduled Jobs
Find the job labeled "TSYS Payments Recurring Contributions (Daily)" and check the information there about the last time it was run and whether or not it is enabled.

### Mannually run the TSYS job
Use the "more" link to select "Execute Now"
This should run any scheduled payments, including any that have been queued up since the last run.

### Enable the TSYS job
If the job runs successfully when executed manually, click the "more" link again and select "Enable" to allow the job to run automatically, once a day.



![](/Screenshots/)
![](/Screenshots/)
![](/Screenshots/)
![](/Screenshots/)
![](/Screenshots/)

