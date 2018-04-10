
# Omega-Server


# Links

[Omega](https://github.com/TeamLazaro/Omega)

[Omega-FrontEnd v0.9-alpha](https://github.com/TeamLazaro/Omega-FrontEnd)

[Omega-Server v0.9-alpha](https://github.com/TeamLazaro/Omega-Server)

[Omega-ExternalServices v0.9-alpha](https://github.com/TeamLazaro/Omega-ExternalServices)



  
# todo
- [ ] Check if expired cookies are sent to the server
- Put an ID for the each enquiry log entry
- Add rupee symbol to the pricing sheet
- Return the URL of the pricing sheet to node
- Wrap up the mods toggling on the front-end
- Convert shortcodes to human readable descriptions
- Notify us of an error in the log



## File Structure

- controller
	- index.js
	- lib
		- datetime.js
		- enquiry-fields.js
		- enquiry-processor.js
		- other.js
		- scheduler.js
- db
	- log.json
	- users.json
- end-points
	- php-mailer
	- twillio-sms
	- zoho-crm
- front-end-helpers
	- lead-validator
	- user-login
	- user-register
- generate-document
	- index.php
	- lib
		- templating.php
		- util.php
	- templates
		- unit-quotation
		- unit-term-sheet
- media
- node_modules
- vendor
	- dompdf
	- phpmailer



## Research Backlog
- Figure out TrueCaller's API
- How is static apartment data going to be queried on the Pricing Engine front-end? From memory? From a database on the server?
- Making AJAX request to cross-domain endpoints. For example, retrieving the Spreadsheet or an AWS Lambda endpoint
- If using AWS Lambda, where are static assets stored?
- How to store all the versions of the spreadsheet on AWS and how to update Lambda to use the latest version?

---

## Structure

#### Website Server (weekly maintenance)
- Website Code
- Front-end Boilerplate
	- Pricing Engine Code
	- pricing_spreadsheet.xlsx
	- sheets.js ( a.k.a. xlsx.js )
	- xlsx-calc.js
- Form Validation
	- PHP: Checks with TrueCaller and the CRM and returns

#### Omega Server (yearly maintenance)
- Node: Build a Queue ( Concurrency )
- Node: Log Enquirers ( File vs SQL vs MongoDB )
- PHP: pass data through the HTML Template
- PHP: pass the template through domPDF
- PHP: Save File
- PHP: return a response to Node ( success / failure )
- if success:: Node: Hands off the File and Form Data to Endpoints Server
- if failure:: Node: Communicate the failed Log ID with the Form data to us so that we may resolve it manually. Next we go about fixing the omega server and submit the customer data manually on their behalf on a bare-bones manual form.
- Endpoints (monthly maintenance for the time being)
	- Exposes single endpoint (eg: endpointserver.com/)
	- PHP: Sends out email(s)
	- PHP: Ingests lead to the CRM
	- PHP: Other Miscellaneous endpoint actions

---

## Implementation Time-line

#### Phase 1
- **Front-end Boilerplate v1** [ 6hr ]
	- Pricing Engine Code
	- pricing_spreadsheet.xlsx
	- sheets.js ( a.k.a. xlsx.js )
	- xlsx-calc.js
- **Omega Server v1**
	- Node: Queue + Log [ 5hr ]
	- PHP: PDF Generator [ 3hr ]
- **Form Validation v1**
	- True Caller API [ 5hr ]
	- ZOHO CRM API [ 2hr ]
- **Endpoint Server v1**
	- PHP eMailer [ 2hr ]
	- ZOHO CRM [ 4hr ]

#### Phase 2
- **Front-end Boilerplate v2**
	- Pricing Engine Code
- **AWS Lambda v1**
	- pricing_spreadsheet.xlsx [ 3hr ]
	- sheets.js ( a.k.a. xlsx.js ) + xlsx-calc.js [ 5hr ]
- **Omega Server v2**
	- Log Monitor [ 3hr ]
	- pricing_spreadsheet.xlsx (Version Control File Manager) [ 4hr ]
	- PDF File (File Manager) [ 2hr ]
- **Endpoints v2**
	- ZOHO Campaigns [ 4hr ]
	- SMS [ 6hr ]
  
 
