# UiPathRPA-Libraries
Updating and using the updated Library.

1. Create two new components for the library which will:

   -- Download all invoices – and save the to a sample xlsx file called “All Invoices.xlsx”
    
   -- Download invoices of a certain vendor tax ID and save them to a sample xlsx file 
      called “All invoices for” + <vendorTaxID> “.xlsx”. 
      The vendor tax ID must be given via user input.

2. Create a workflow that lets the user choose between downloading all work items, downloading all invoices, 
   or downloading only the invoices that belong to a certain tax ID inputted by the user.
   
In UiPath Studio, create a new project and perform the following steps:

1. Updating the Library

    Sequence 1 – Navigating to invoices (private workflow):
    
      --  Invoke the “Navigate to home page” workflow;
      
      --  Use a ‘Hover’ activity to hover over the ‘Invoices’ button to access the secondary menu;
      
      --  Use a ‘Click’ activity to click on the ‘Search for Invoice’ button;
      
      --  Use a ‘Click’ activity to click on the ‘Display All Invoices’ button.

    You can use the recorder for capturing the activities 2-4.

    Sequence 2 – Downloading all invoices (public workflow)
    
      --  Invoke the ‘Navigate to invoices’ workflow;
      
      --  Use the ‘Data Scraping’ option (‘Extract structured data’ activity) to extract all the invoices 
          and details in a DataTable argument with Out direction.
      
    Sequence 3 – Navigating to search invoice by Vendor Tax ID (private workflow)
    
      --  Invoke the “Navigate to home page” workflow
      
      --  Use a ‘Hover’ activity to hover over the ‘Invoices’ button to access the secondary menu
      
      --  Use a ‘Click’ activity to click on the ‘Search for Invoice’ button.

          You can use the recorder for capturing the activities 2-3.

    Sequence 4 – Downloading all invoices of Vendor Tax ID (public workflow)
    
      --  Invoke the “Navigate to search invoice by vendorTaxID” workflow;
      
      --  Use a ‘Type into’ activity to write the input value in the search field. Use a String argument with the In direction;
      
      --  Use a ‘Click’ activity to click on the ‘Search’ button;
      
      --  Use the ‘Data Scraping’ option (‘Extract structured data’ activity) to extract all the invoices and details in a 
          DataTable argument with Out direction.

 

2. Creating the workflow

   -- Use an ‘Input Dialog’ to offer the user to choose between the 3 options;
    
   -- Use a ‘Get Secure Credential’ activity which is in the UiPath.Credential.Activities that can be installed from Manage Packages. 
      This way you can store the credentials in 2 String variables ("username" and "password");
      
   -- Use the ‘Login’ activity from the Library;
   
   -- Use a ‘Switch’ to execute the workflow corresponding to the user option:
   
    Case 1: Download all work items
    
      --  Start the workflow as a Sequence;
      
      --  Use the ‘Download all work items’ activity from the Library and assign the value of the DataTable argument to the DataTable variable;
      
      --  Use a ‘Write Range’ activity to write the data from the DataTable to an Excel file.
      
    Case 2: Download all invoices
    
      --  Use the ‘Download all activities’ activity from the Library and assign the value of the DataTable argument to the DataTable variable;
      
      --  Use a ‘Write Range’ activity to write the data from the DataTable to an Excel file.
      
    Case 3: Download invoices by Vendor Tax ID
    
      --  Use an ‘Input Dialog’ activity to get the tax ID from the user and store it in a String variable (“vendorTaxID”);
      
      --  Use the ‘Download all invoices of Vendor Tax ID’ activity from the Library, with the “vendorTaxID” argument equal to the “vendorTaxID” variable;
      
      --  Use an ‘If’ activity to check whether there were invoices corresponding to the inputted tax ID, using the ‘.Rows.Count’ method. 
          If so, use a ‘Write Range’ activity to write the data from the DataTable to an Excel file;
    
    Use the ‘Logout’ activity from the Library.
  
