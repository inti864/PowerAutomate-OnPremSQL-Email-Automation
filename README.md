Title : PowerAutomate-OnPremSQL-Email-Automation

Description: Workflow using Power Automate to automate email reports to clients

Goal: Client was using an ERP software to manually email reports with status of their order and events, they had several employee's who would email this information manually, but due to human error sometimes they would accidentally send the wrong information to the wrong client. Automating this process helped save manual effort and reduced human error to 0%


Tools used: Power Automate, Microsoft SQL Server, Microsoft Gateway, Sharepoint, Outlook

Flow Steps
1. Recurrence - The time the emails need to be sent out and frequency, such as every day at 10AM or even twice a day
2. Get Rows - Retrieves data from On Prem Database, Specifically a view that was created with specific customer data
3. Condition - This was added to verify if the flow has any information to email or does not, if TRUE will follow the flow for sending an email, if FALSE will terminate and show success as the result. This step is to avoid emailing blank information to the client if there are no updates to send
4. Apply to each (Add row into a Table) - this gets the information from the SQL database and then apply's it to each row individually, so if there are 50 rows of data in SQL, it will add each row one by one into Excel on Sharepoint until all rows are added, in addition this is where you pull the column data from SQL and assign it to specific columns in Excel to match data
5. Delay - to avoid synchronization delays and issues with Sharepoint I added a 3 minute delay before moving to the next step in order to avoid excel sheets being emailed with partial data or cutoff information due to delays in Synchronization
6. Get File Content Using Path - This retreives data from the Excel file in Sharepoint to allow the following node to pull this data
7. Send an email - this is where the email is created, using a template for Body and subject line we pull the information from the previous node and then add recipients and email the list
8. Delay - This is added once more to avoid any synchronization issues
9. Run script fropm Sharepoint Library - Once the information is added to the Excel file, it stays on the Excel file so to prep for the next automated email with new updated information I added a script to Sharepoint to delete the previous data on it, so when the new Excel sheet is emailed it is emailed with new data and does not retain old data. This Completes the automation cycle
   
![Power Automate Flow](https://github.com/inti864/PowerAutomate-OnPremSQL-Email-Automation/blob/main/2025-05-16%2015_56_43-Clipboard.png?raw=true)
