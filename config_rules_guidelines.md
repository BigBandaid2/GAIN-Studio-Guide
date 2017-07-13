GAIN Studio Configurations Guide and Best Practices
===================================================
Goal: Establish the Definition of Done
--------------------------------------
A configuration is truly complete only when it is:
- Clear and Easy to Understand
- Fully Tested
- Efficient

### Clear and Easy to Understand
- Is the configuration must be understandable and maintainable for people other than the original author?
- Does it include references to the original requirments that it is meant to satisfy?
- Is the configuration and well commented to help others track the logic and choices made by the author?

### Fully Tested
- Has the configuration passed SpecFlow unit tests in GAIN Studio?
- Are the tests comprehensive and include situations that are likely to cause errors?

### Efficient
- Does the code benefit from reusable templates so that configurations can be written quickly
- Does the code run efficiently so that it performs well over thousands of records

How to use this guide
---------------------
This guide has two main parts:
1. *GAIN Studio Coding Reference* - This includes templates and explanations for common rules types and scenarios. These templates apply methods that are most efficient in GAIN and control for common sources of error that can be inadvertently introduced in configuration rules

2. *GAIN Best Practices Beyond Configuration Code* - Aside from functional and efficient configuration code, our goal is also to present a non-technical checklist that can be followed for each configuration to ensure that configurations are maintainable and testable going forward.
	
\ GAIN Specific Coding Guidelines
=================================
Guideline Structure
-------------------
Each page in this section will cover a common scenario, provide a code template or example, and explain the reasoning for the recommended method. This section will assume basic familiarity with programming terminology and concepts.

Beyond this three part structure, further reading and explaination for the feature will refer to the core GAIN Studio guide documentation.

\ Testing and Documentation Checklist
=====================================
Checklist Structure
-------------------
This section will provide a non-technical guide for code review and validation based on a checklist that should be followed for sign-off on the configuration rule. A significant focus of this section will be documentation and preparing automated tests.

For each step of the checklist we will provide an explanation of this step's purpose, a walkthrough example and supporting material or references to the core GAIN Studio documentation. 

Checklist Items
---------------
1. Does a SpecFlow exist in GAIN Studio that is associated to this configuration rule?
2. Does the Spec Flow run without scripting errors (regardless of test Pass/Fail)?
	- If not, errors must be cleared so that the expected inputs and outputs appear in the Test Output.
3. Are the functional requirements of the configuration rule described explicitly and clearly in the associated SpecFlow?


\\ Check 1 - Does an Associated SpecFlow Exist
==============================================
Purpose
-------
The SpecFlow .feature files serve as both the functional requirement documentation and unit-level test for each configuration rule. This is important for both review, maintainance and testing.

**Maintenance** Without an associated SpecFlow in GainStudio, it is impossible to trace the configuration back to specific requirements making maintenance and verification impossible

**Testing** A SpecFlow must be associated to run individual configuration level unit tests in GAIN Studio. These test are much faster to run than tests involving full instrument creation and tranformation, and provide error messages and debugging.

Walkthrough
-----------
###Step 1 - 'Jump to Test'
The fastest way to check if an associated test exists is to right-click on the configuration rule in question and click 'Jump to Test'. After a few seconds, the associated .feature file will be opened or you will find recieve a *Could not find related test* message.

![jumpToTest.png]
![couldNotFind.png]

>**PASS/FAIL**
>
>IF .feature file opens, Check 1 
>THEN PASSED
>
>ELSE, move to Step 2 - Search for Tests

###Step 2 - Search for Tests and Consolidate
Often there are existing tests in the Test Explorer folder. If multiple exist for the same configuration, these tests should be consolidated to one .feature file and associated to the target configuration.

[Search for test instruction][Search for feature test]

??? How to associate with an existing test case

>**PASS/FAIL**
>
>IF there one .feature file in the correct folder corresponding to this configuration
>THEN PASSED
>
>Else, move to Step 3 - Generate Test

###Step 3 - Generate Test
If no associated test is found, you should use 'Generate Test' to create a new feature file. GAIN Studio's 'Generate Test' feature is preferable to copying feature files into a test folder for the following reasons:
- .feature file will automatically be correctly associated, placed into the correct folder
- The correct Given, When, and Then commands will be automatically generated based on the Model and Configuration with no danger of mispellings or other user errors
- Any variables used in the configuration logic, will also automatically appear with no risk of user error

To create a test for a specific field:
1. Open the transformation and locate the field.
2. Open the context menu of the field in the transformation target window and select Generate test:

![generateTest.png]
![generatedSpecFlow.png]
	
3. Fill out a test case, input and output should be the same, remove Process Context if it is not used in the current rule
4. Delete and type '|' on the last pipe of the table, this will auto-format and align the columns to make more readable test cases

[Further Guidance on Generating Tests]

\\ Check 2 - Does the SpecFlow Run Without Errors
=================================================
Purpose
-------
The first step of implementing a new automated SpecFlow is the ensure that all inputs and outputs register correctly, and the correct model is used, and that no breaking errors are triggered in the current configuration or any of the configurations that precede it.

The objective of this check is not to Pass tests, but simply that the test script produces a testable output. It is critical the perform this check in order to seperate test failures caused by incomplete configuration vs. test failures caused by incomplete SpecFlow setup.

Walkthrough
-----------
### Step 1 - Run the SpecFlow in Test Explorer
Run the SpecFlow in Test Explorer and Check that expected inputs, outputs and models are registering in the test.
1. [Search for feature test]
2. [Run feature tests]
3. Test cases will likely fail, right click a failed test and select 'Test Output'. Check that all fields are appearing correctly and there are no run-time errors.

![checkTestOutput.png]

### Step 2 - Check Test Output that expected inputs, outputs and models are registering in the test with no errors

>**PASS/FAIL**
>IF test succeeds
>OR
>IF no errors are displayed 
>AND all input fields in the Given section are populated 
>AND the output field in the Then section is populated
>THEN PASSED
>
>ELSE, move to Step 3 - Troubleshoot errors

- Potential errors: {Model doesn't exist, field not appearing, field appears as placeholder}
- [Test Output Common Errors and Messages]

![

The SpecFlow

\ Guiding Principles for Configuration Best Practices
=====================================================

Four goals of defining and following best practices
---------------------------------------------------
GAIN Studio allows people with a broad spectrum of business and technical skills to have an unprecedented level
of access, control, and customizability to the rules that define business process behavior within the GAIN ecosystem.

However, this flexibility also means that there are more opportunities for confusion and sub-optimal code to be introduced
to live production systems causing unexpected errors or a headache for maintenance down the road.

Our goal for this guide is to help put all team members writing configuration rules for on the same footing by providing
a basic set of coding standards, testing requirements, and documentation language so that every configuration rule
written in GAIN achieves the following important criteria:

1. ### Dependable ###
	The configuration must be functional and resilient, accounting for common issues such as missing data that can create errors.
2. ### Maintainable ###
	The configuration must be understandable and maintainable for people other than the original author. Every configuration must
	include references to the requirments that it is meant to satisfy and well commented to help other track the logic and choices
	made by the authors.
3. ### Testable ###
	Every new configuration must be accompanied by unit (rule) level tests to valid that the rule is working correctly.
	These test should be formatted such that they can be excuted by GAIN Studio's built in testing suite.
4. ### Efficient ###
	Finally, rules should be written so that perform efficiently. Every implementation includes hundreds of rules which must
	run again thousands of records regularly. As a result small tweaks that optimize code performance can have major rewards.

Throughout the remainder of this guide. We will refer back to these four goals to provide context and motivation for 
each best practice suggestion.

\ Configuration Examples
========================

This section of the guide will provide a series of detailed walkthroughs covering configurations and testing for rules in GAIN Studio.
The examples will begin with the very simple and increase in complexity with a goal of introducing a few new best practices in each.

Example Series:
---------------
### Simple 1:1 Mapping ###
**Description:** Straight forward 1 input to 1 output mapping with no documented requirements and no transformation logic.

**Concepts:**

- Generating a SpecFlow Automated Test
- Adding test data to an automated test case
- Running Automated tests with Test Explorer
- Basic Commenting in the configuration rule
- Basic Commenting in the test case

**Features:**

- Field already exists in the AIM model
- One input, One output
- No Run Condition
- Simple If...Else Transformation
	
2. Declaring and Assigning Variables
Translating Functional Requirements to Automation
Writing Your First Transformation Logic

# Links
Baseline Rule Minimum Requirement (1:1 Rule)
Basic Rule With Spec Flow Requirements
Basic Rule With Lookup

\ Components
============
# Links
If...Else
Lookups

\\ Baseline 1:1 Rule Minimum Requirement
========================================
BbgUniqueId

- Field exist in AIM Model
- One input, one output, string
- No Run Condition
- No Transformation Logic
- No pre-existing SpecFlow or requirments

Step 1. Drag the desired source field to the desired target field
- [Dependable] This will create a single line of code
# code example
return Source.SecurityIdentifiers.ID_BB_UNIQUE;
# end code example

Step 2. Generate an Automated Test
- [Testable] Once all variables are declared, save and right-click in the transform model -> Generate Test
	- this will produce a SpecFlow Template associated with the field, using all correct parameters and variables
	- if an implemented SpecFlow already exists, this will open to correct file so that duplicates are not created
- [Testable] Fill out a test case, input and output should be the same, remove Process Context as this in not used in the current rule
- [Maintainable] Delete and type '|' on the last pipe of the table, this will auto-format and align the columns to make more readable test cases
# screenshot - SpecFlow
- [Maintainable] Add comment to the transformation rule referring to the Scenario Outline in the automated test case
# code example
// Begin Rule
// Corresponds to reqs and tests in Scenario Outline: BbgUniqueId
# end code example

Step 3. Run Test
- [Functional] Check that all test cases pass, if not adjust the transformation or test cases accordingly

Step 4. Place final comments on test
- [Maintainable] Summarize the logic of the transformation rule if not already written in SpecFlow
	- write the interpretation and logic summary under the Scenario Outline
- [Maintainable] Tag the spec flow with the team that reviewed and implemented so that it can be traced back
	- tags: {defined, cleaned, implemented, signedOff}
	- examples: {AIM-implemented, FT-defined, Sapient-signedOff}
# screenshot - final SpecFlow

# Second Example
Martial's current 1:1 rule text

\\ Basic Rule With Spec Flow Requirements
=========================================

ISIN
----
- Field already exists in the AIM model
- One input, One output
- No Run Condition
- Simple If...Else Transformation

Step 1. Refer to spec flow and interpret the requirement
- [Maintainable] Summarize the logic of the transformation rule if not already written in SpecFlow
	- write the interpretation and logic summary under the Scenario Outline
- [Maintainable] Tag the spec flow with the team that reviewed and implemented so that it can be traced back
	- tags: {defined, cleaned, implemented, signedOff}
	- examples: {AIM-implemented, FT-defined, Sapient-signedOff}
	
Step 2. Generate an Automated Test
Step 3. Translate First Scenario Outline to the Generated SpecFlow
- [Testable] Move the header up to Scenario Outline and interpreted explanation, above 'Given data...' line from requirement SpecFlow to automated SpecFlow
	- This retains the generated fields and prevents automation errors from mispellings, etc.
	- Remove Process Context inputs if not used
- [Testable] Copy/Paste the Test Case lines (keep the generate column headings) and realign the data columns
	- This prevents the test case field headings from becoming misaligned with the expected inputs
	- Care must be taken the align the test data with the correct headings
	- At the end, delete the last pipe in any line and type '|' again to activate auto-formatting the straighten columns
	
Step 4. Run the SpecFlow in Test Explorer and Check that expected inputs, outputs and models are registering in the test
- [Testable] Test cases should all fail, right click a failed test and select 'Test Output'. Check that all fields are appearing correctly and there are no run-time errors
- [Testable] Potential errors: {Model doesn't exisit, field not appearing, field appears as placeholder}
	- Link to list of errors

Step 5. Write Your Cofiguration Rule Logic
- [Maintainable] Comment the code block with a reference to the Test Scenario Outline that it is based on
# code example
// Begin Configuration Rule
// Corresponds to reqs and test in Scenario Outline: ISIN 
# end code example
- [Dependable] For ISIN, write and solid If...Else statement
# code example
if (idIsin == "N.A.")
	return null;
else
	return idIsin;
# end code example
- [Dependable] For more on writing good If...Else statements, refer to here [link: IF...ELSE]

Step 6. Run the SpecFlow in Test Explorer
- [Dependable] Check that all test cases pass, if not adjust the transformation
- [Testable] If a test fails because the test case has errors, comment out the test case or make adjustments. 
	- Always leave a comment on adjusted test cases and mark with '#?' so that it can be readily found and reviewed
- [Maintainable] Consolidate and clean out redundant or inactive Spec Flows so that only one SpecFlow exists for each transformation step of each field


Basic Rule With Lookup
======================
CountryOfRisk

- Field already exists in the AIM model
- Two inputs, One output
- No Run Condition
- If...Else Condition + Return Lookup Value

Step 1. Refer to spec flow and interpret the requirement
Step 2. Declare and assign all variables 
- [Maintainable] Begin the transformation block with all variables that will be used so that they are easy to see at a glance, end with a simple return of a declared variable
# code example
// Declare and assign variables
	// String
var idIsin = Source.SecurityIdentifiers.ID_ISIN;
	return idIsin;
# end code example
- [Testable] Once all variables are declared, save and right-click in the transform model -> Generate Test
	- this will produce a SpecFlow Template associated with the field, using all correct parameters and variables
	- if an implemented SpecFlow already exists, this will open to correct file so that duplicates are not created
Step 3. Translate First Scenario Outline to the Generated SpecFlow
- [Testable] Here the SpecFlow must be cleaned to create testable cases. Each field can only contain one value
Step 4. Run the SpecFlow in Test Explorer and Check that expected inputs, outputs and models are registering in the test
Step 5. Write Your Cofiguration Rule Logic
- [Dependable]


More
====

# Declare and assign commonly used variables. Convert values to strings for easier exception handling
// Validate all fields at the top of the rule
// Assign all inputs to a local camelCase version of the variable
// Organize lookups, strings, decimal, integer, Boolean, and variables from joined objects
// Lookups should be assigned to a string of their reference code or "" if null

# Code template
// Declare and assign variables
	// Output
var countryOfListing = "";
	// Lookups
var exchange = Source.Exchange != null ? Source.Exchange.ReferenceCode : "";
var ftIOClass = Source.FTIOClass != null ? Source.FTIOClass.ReferenceCode : "";
var ftSecurityType = Source.FTSecurityType != null ? Source.FTSecurityType.ReferenceCode : "";
var issueCurrency = Source.IssueCurrency != null ? Source.IssueCurrency.ReferenceCode : "";
var securityCountryOfIncorporation = Source.SecurityCountryOfIncorporation != null ? Source.SecurityCountryOfIncorporation.ReferenceCode : "";
var couponType = Source.CouponType != null ? Source.CouponType.ReferenceCode : "";
	// Joined
var underlying_countryOfListing = (Source.Underlying != null && Source.Underlying.CountryofListing != null) ? Source.Underlying.CountryofListing.ReferenceCode : "";
var maturity = Source.DescriptiveInfo != null && Source.DescriptiveInfo.MATURITY.HasValue ? Source.DescriptiveInfo.MATURITY : null;
	// Decimal
var parValue = Source.ParValue;
var couponRate = Source.CouponRate;
	// Boolean
var isRegS = Source.IsRegS.HasValue ? (bool ?)Source.IsRegS.Value : null;
var is144A = Source.Is144A.HasValue ? (bool ?)Source.Is144A.Value : null;
	// Date
var maturityDate = Source.MaturityDate.HasValue ? Source.MaturityDate : null;
var expirationDate = Source.ExpirationDate.HasValue ? Source.ExpirationDate : null;
	// String
var referenceIndex = !string.IsNullOrEmpty(Source.ReferenceIndex) ? Source.ReferenceIndex : "";
var loanFacilityName = !string.IsNullOrEmpty(Source.LoanFacilityName) ? Source.LoanFacilityName : "";

# Mark beginning of confirmation rules and indicate the Scenario Outline corresponding to each section
# We must align as much as possible SpecFlow and code
// Begin Configuration Rules
// Corresponds to reqs and tests in Scenario Outline: XXYYZZ

# In conditionals involving lookups, use the helper function of the desired class.
# Remember, Lookups class doesn't always match the name of the field (ex. SecurityCountryOfIncorporation => Countries)
# Code template
if (ftIOClass == FTIOClasses.EQ.ReferenceCode) {}
if (securityCountryOfIncorporation == Countries.IE.ReferenceCode) {}

# Mappings - for single input mapping, input of a mapping must be a string.
# assign result of Mapping to a new variable, then check Null on the variable to prevent error
# new variable will be a Mapping object, to get the value, you must access property of the result object
# Code template
var result = !string.isNullorEmpty(exchange) ? Mappings.ExchangeCodeToCountry.Transform(exchange) : null;
countryOfListing = result != null ? result.Country : "";

# Conditionals with multiple arguments, use || and && to combine conditions
# Code template
if (ftIOClass == FTIOClasses.CS.ReferenceCode || ftIOClass == FTIOClasses.FI.ReferenceCode) {}

# Lookups - GetItemByID()
Lookups.XLookupClassX.GetItemById(XReferenceCodeX)

# Null Checking
// Boolean
Source.IsRemarketed.HasValue

# Matching against arrays
# Code template
// Set the array
string[] ftSecurityTypeArrayRule2 = {"ADR", "GDR", "IDR", "DPP"};
// check if contains
if (ftSecurityTypeArrayRule2.Contains(ftSecurityType)) {}

# Building up a long string made of multiple parts and variable length
# This is better than directly concatenating string because it avoids trailing seperators (ie. commas, spaces)
# Code template
// create an array that will hold all the potential parts, up to the maximum count of parts
// initial a pointer to navigate the array
string[] name_parts = new string[3];
int i = 0;

// add elements to the array according to rules and increment the pointer
name_parts[i] = Source.Issuer.LongName;
i++;

// truncate the array according to the pointer, concatenate the array with desired seperator
Array.Resize(ref name_parts, i);
ftSecurityLegalName1 = string.Join(", ", name_parts);

# Formatting dates
# Code template
Source.MaturityDate.Value.Date.ToString("MM/dd/yyyy");

# Formatting decimals to remove trailing or leading zeros
# Code template
// remove trailing zeros
	name_parts[i] = Source.CouponRate.Value.ToString("G29");
// remove first zero if it's less than 1
if (Source.CouponRate.Value < 1) {
	name_parts[i] = name_parts[i].Substring(1, name_parts[i].Length - 1);
}

# Simple Rules
# 1 to 1 with Lookup
// Corresponds to reqs and tests in PaymentRank: BBG.PAYMENT_RANK
if (Source.DescriptiveInfo.PAYMENT_RANK == null)
{
	return null;
}
else
	return Lookups.PaymentRanks.GetItemById(Source.DescriptiveInfo.PAYMENT_RANK.ToString());

# 1 to 1 with Mapping nd Lookup
// Declare and assign variables
	// Lookups
var ftSecurityType = Target.FTSecurityType != null ? Target.FTSecurityType.ReferenceCode : "";
	// Output
var ftIOClass = "";

var result = !string.IsNullOrEmpty(ftSecurityType) ? Mappings.FTSecurityTypeToFTIOClass.Transform(ftSecurityType) : null;
ftIOClass = result != null ? result.FTIOClass : "";

return Lookups.FTIOClasses.GetItemById(ftIOClass);
	

# Run conditions - 
// Don't use run conditions to validate data. Run condition should only reflect business
// requirements that dictate a rule does not need to run. Better for the rule to rule and return null or existing value
// that for the rule to not run at all without total confidence that it's not needed
// Run condition considering more than the source source value of the current field must point to a spec flow requirement dictating this behavior
// Don’t put complex rules in the run conditions, as they are supposed to be used as precalculation. They should be fast.

// Using run conditions may speed up the process, as it can block a rule from running (important by complex rules).

# Notation in comments
// #? Or //? Is comment tag for an open question
// Comments your code !!! At minimum, provide comment pointing the the reqs/test/specflow that defines this logic

# Tips for speeding up testing automation
// Run the specflow with just trigger conditions and placeholder values first to ensure that inputs and outputs are being read correctly before writing rule
// Implemented SpecFlow is mandatory

# Tips for creating robust test cases
// Add an all Null inputs test case for each Test Scenario

# Order of the rules:
// 1. Keys should be normalizaed as first
// 2. If a rule is dependant on another one, it should be lower in the normalization/derivation list.

# Programming tips
// Avoid excessive usage of ProcessContext.
// Avoid unnecessary usage of extension methods.
// Remember that complex rules slow down the normalization/derivation.

# Usings
// Remember that usings can be only normalized, never derived (underlying, issuer).
// Remember there’s no selection rules for usings. Usings are never overriden. If it’s set to a non null value, it will stay like this ?
// The validation rules for using should be done at the entity level (i.e. issuer should be validated in the validation rule for the whole instrument).
// The normalization/derivation of components must be done as a child derivation of a parent class (example: ratings, schedules).

Cutting Floor
=============
This best practice guide contains the following resources:
A toolbox of sample code and solutions for frequently occurring scenarios
	- This section will include common topics and example code templates of ideal configurations to help developers save time
A quick overview of guiding principles for good configurations
A set of configuration rule examples demonstrating the exec
	- These walkthroughs will introduce our checklist of 7 key steps required to follow GAIN Studio standard best practices
	
	Each Walkthrough is Arranged in Order of Progressing Complexity. These walkthroughs cover simple configuration rules but are meant to introduce best practice documentation, testing, and exception handling that is often neglected when writing configuration rules. Adopting these best practices are essential to creating maintainable, dependable and efficient code.
Outline
Basic 1:1 Rule - Basic commenting and creating your first automated test
	- Drag and drop rule configuration
	- Generating a test case temple
	- Running an automated test with test explorer
Simple Conditional Logic from Requirements - Translating requirements into configuration rules and tests
	- Interpreting and documenting a requirement properly
	- Translating SpecFlow requirements to executable SpecFlow test scenarios
	- Checking for execution errors in SpecFlow test scenarios and troubleshooting
	- Writing simple configurations and proper association of rules to requirements
Introducing Lookups - The correct way to use lookups
	- Declaring and assigning variables for proper exception handling
	- Best Practice for using Lookups
Introducing Mappings - The correct way to use mappings
	- Best Practice for using Mappings