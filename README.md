# TSYS Integration with CiviCRM Documentation


# Preparations

Make sure you have identified the specific website to use, and complete these steps:

* login to the CMS (WordPress, Drupal, or Joomla) as an administrator
* Navigate to the CiviCRM dashboard
* Check that cron is running and that the TSYS scheduled job is enabled

![](/Screenshots/01-NavigateToCivi.png)

https://github.com/aghstrategies/TSYS-CiviCRM-support/blob/Josh/Screenshots/01-NavigateToCivi.png

# Install TSYS extension
* Use the Civi menu Administer > System Settings > Directories to identify the extension directory.
[screen shot]
*Note, you can use the ? symbol in the green text in place of the variables to get the full absolute paths on your server for each directory.


## Switch to the Command Line
Connect by SSH to your web server (ex: webmaster@website.com) and navigate to the extension directory found above
Ex: 
      ssh webmaster@website.com
      cd /var/www/website/wp-content/uploads/civicrm/ext/

Download the extension file and unzip it. Use the latest version found on (https://github.com/aghstrategies/com.aghstrategies.tsys/archive/v1.1.0.zip)
Ex: 
      sudo wget https://github.com/aghstrategies/com.aghstrategies.tsys/archive/v1.1.0.zip
      sudo unzip v1.1.0.zip

*The specific file path may change as the software is updated. Please check this link for the latest stable archive: https://github.com/aghstrategies/com.aghstrategies.tsys/archive

## Switch to the web interface


* Use the Civi menu Administer > System Settings > Extensions
* Click the Refresh button
[screen shot before refresh]  
[screen shot after refresh]  

Click the Install link on the right of the TSYS lsiting
[screen shot]

You'll be returned to the Extensions page, with TSYS Enabled


# Configure a TSYS Payment Processor

Now that Civi has the capability of talking to TSYS, we need to configure a Civi payment processor to use TSYS.

* Use the Civi menu to navigate to Administer > System Settings > Payment Processors
* Click the Add Payment Processor button
[screen shot of payment processor configuration]

## Payment Processor Fields
Payment Processor Type: Choose TSYS
Name: This is displayed by default on public pages when the payment processor is chosen. Consider using something like Credit Card.
Description: Open text field for your own organization
Financial Account: Defaul is Payment Processor Account, leave it unless you have a reason to change it.
Payment Method: This information shows up on any contribution record created using this processor as the payment method. Default is Credit Card, we recommend you leave it unless you have a reason to change it.

Ensure the "Is this Payment Process active?" box is checked, this makes the processor available to use on contribution and event pages.

If the " Is this Payment Processor the default?" box is checked, any new contribution page or event created will allow credit card payments using this TSYS processor.

Accepted Credit Card Types
Select Visa, MasterCard, Amex, and Discover


## Processor Details for Live Payments
Merchant Name: This is provided by your TSYS representative
Web API Key: This is provided by your TSYS representative
Merchant Site Key: This is provided by your TSYS representative
Merchant Site ID:	This is provided by your TSYS representative
Site URL:	https://cayan.accessaccountdetails.com/
Recurring Payments URL: https://cayan.accessaccountdetails.com/

## Processor Details for Test Payments

Repeat all the information above

Merchant Name: This is provided by your TSYS representative (same as above)
Web API Key: This is provided by your TSYS representative (same as above)
Merchant Site Key: This is provided by your TSYS representative (same as above)
Merchant Site ID:	This is provided by your TSYS representative (same as above)
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



