GAIN Studio Configurations Guide and Best Practices
===================================================
How to use this guide
---------------------
This guide has three main parts:

### 1. Check list 'Definition of Done'
- This is AIM Software's definition of a fully DONE configuration in GAIN Studio
- You can use this checklist as 'crib-sheet'
- We'll show examples comparing a good DONE configuration vs. a NOT DONE one

### 2. Best Practices to reach 'Definition of Done'
- This section details each steps to achieve 'Definition of Done'

### 2. Best practices to structure a transformation
- This section gives advices to structure a transformation (derivation instrument, normalization Bloomberg instrument ...).

### 3. GAIN Studio Coding Reference
- A lot of rules contains same code piece:
   - if 
   - Mapping
   - ...
- The best is to copy a pattern available in this section and adapt to your particular case
- You are then sure to have good basis for your coding

\ Definition of Done
==============
Goal: Establish the Definition of DONE
--------------------------------------
A configuration is truly DONE only when it is:

- Clear and Easy to Understand
- Fully Tested
- Efficient

### Clear and Easy to Understand
- Is the configuration understandable and maintainable for people other than the original author?
- Does it include references to the original requirements (SpecFlow) that it is meant to satisfy?
- Is the configuration well commented to help others track the logic and choices made by the author?

### Fully Tested
- Has the configuration passed SpecFlow unit tests in GAIN Studio?
- Are the tests comprehensive and include situations that are likely to cause errors?

### Efficient
- Does the code benefit from reusable templates so that configurations can be written quickly?
- Does the code run efficiently so that it performs well over thousands of records?

Done in the Context of GAIN Studio - Checklist
----------------------------------
A clear, tested and efficient configuration in GAIN has the following minimum criteria:

1. A single consolidated SpecFlow .feature file exists for this configuration (multiple SpecFlows must be exceptions)
   SpecFlow must be at right place (rule 'Jump to test' opens  SpecFlows file)
1. The interpretation of the original business requirement is explicitly written and reviewed in the SpecFlow
   A comment details rule and how to read examples.
1. The SpecFlow contains sufficient test cases, including cases with missing data (all inputs are null).
1. The SpecFlow is associated directly to the configuration via GAIN Studio
   'Jump to test' opens  SpecFlows file.
1. The configuration has comments pointing to corresponding sections of the the SpecFlow for reference
1. All test cases PASS
     - No scripting/blocking errors
     - No business errors
1. The configuration code handles common sources of error [See Checklist of Common Errors]
1. The configuration uses efficient methods such as Mapping to optimize execution speed
   The code re-uses official templates as much as possible. 
2. Configuration has been checked by a second team member

\\ Example of a Configuration: BbgUniquId
======================================
DONE Configuration - Best Practice
----------------------
- ![](/greenCheck.png) A single consolidated SpecFlow .feature file exists for this configuration

SpecFlow must be at right place (rule 'Jump to test' opens  SpecFlows file)
HERE PICTURE JUMP TO TEST

- ![](/greenCheck.png) The SpecFlow is associated directly to the configuration via GAIN Studio
- ![](/greenCheck.png) The interpretation of the original business requirement is explicitly written in the SpecFlow
A comment details rule and how to read examples.
	![](/specFlowWithComment.PNG)
- ![](/greenCheck.png) The configuration has comments pointing to corresponding sections of the the SpecFlow for reference

	![](/configWithComment.PNG)
- ![](/greenCheck.png) The SpecFlow contains sufficient realworld test cases, including cases with missing data

	![](/testCases.PNG)
- ![](/greenCheck.png) The test cases run in GAIN Studio with no SpecFlow scripting or blocking errors
- ![](/greenCheck.png) All test cases PASS

	![](/passTests.PNG)
- ![](/greenCheck.png) The configuration code controls for common sources of error
- ![](/greenCheck.png) The configuration uses efficient methods such as Mapping to optomize execution speed

NOT DONE Configuration
------------------------
### Issues in NOT DONE Configuration
- ![](/greenCheck.png) A single consolidated SpecFlow .feature file exists for this configuration

	![](/singleTest.png)
- ![](/redX.png) SpecFlow .feature file exists, but is not connected to configuration rule

	![Could Not Find](/couldNotFindTest.PNG)
- ![](/redX.png) No written intepretation of requirement in existing SpecFlow
- ![](/redX.png) Few Test Cases, unrealistic data

	![SpecFlow no comment](/specFlowNoComments.PNG)
- ![](/redX.png) No comments on configuration

	![](/incompleteBggUnique.PNG)
- ![](/redX.png) Tests have all failed

	![](/testsFailed.PNG)
- ![](/redX.png) Tests failed due to SpecFlow scripting failure

	![](/scriptingError.PNG)
- ![](/greenCheck.png) Configuration code is clean is efficient

\ Best Practices to reach 'Definition of Done'
=====================================
Checklist Overview
-------------------
This section details each step to pass 'Definition of Done'

- Every configuration should pass the checklist before sign-off on the configuration rule
- A significant focus of this checklist will be documentation and preparing automated tests
- Code efficiency and error control will be kept at a minimum in this section, reserved for 'Coding Guidelines'

Checklist Structure
-------------------
Each checklist item will contain

- An explanation of this step's purpose
- One or more examples of configurations that PASS this checklist item
- A list of common failure scenarios
- Supporting material or references to the core GAIN Studio documentation. 

Checklist Items
---------------

1. A single consolidated SpecFlow .feature file exists for this configuration (multiple SpecFlows must be exceptions)
   SpecFlow must be at right place (rule 'Jump to test' opens  SpecFlows file)
1. The interpretation of the original business requirement is explicitly written and reviewed in the SpecFlow
   A comment details rule and how to read examples.A comment details rule and how to read examples.
1. The SpecFlow contains sufficient test cases, including cases with missing data
1. The SpecFlow is associated directly to the configuration via GAIN Studio
   'Jump to test' opens  SpecFlows file.
1. The configuration has comments pointing to corresponding sections of the the SpecFlow for reference
1. All test cases PASS
     - No scripting/blocking errors
     - No business errors
1. The configuration code handles common sources of error [See Checklist of Common Errors]
1. The configuration uses efficient methods such as Mapping to optimize execution speed
   The code re-uses official templates as much as possible. 
2. Configuration has been checked by a second team member


\\ Only A Single SpecFlow File Should Exist in Test Folders
==============================================
Purpose
-------
If there is more than one .feature file for a single configuration, there's a danger of confusion and conflict. 
No file and No tests or requirements is also bad. 

PASS Example
------------
1. Navigate to Text Explorer
2. Type the name of the configuration's model field into the 'Filter' bar
3. Look for the one set of tests to appear for this transformation step and this model field

![](/singleTest.png)

Common Failure Scenarios
------------------------
- No SpecFlows Exist 
	- **Solution:** [generate a specflow]
- More than one test exist 
	- **Solution:** [consolidate specflows]

\\ The SpecFlow and Configuration Rule Must Be Associated
=====================================================
Purpose
-------
If the SpecFlow file exists but is not associated, you have two problems:

- You can't jump quickly from the configuration rule to the SpecFlow
- The SpecFlow may not function correctly and may be imporperly tagged

PASS Example
------------
1. Right-click on field of configuraiton
2. click 'Jump to Test'
3. Associated Specflow .feature file should open

![](/jumpToTestResult.png)

Common Failure Scenarios
------------------------
- Could not find test because no test exists
	- **Solution:** [generate a SpecFlow]
	- ![](/couldNotFind.png)
- SpecFlow file exists, but is not associated	
	- **Solution:** Generate a specflow
	- copy test cases from existing SpecFlow file(s) into the new Generated Specflow
	- Be careful to keep the test title tag of the generated test
	- Example - '@Derivation.InstrumentDerivation.FTSecurityLegalName2'
	- This tag is what is used to connect SpecFlows with configurations
	- Generating a new test also places the test automatically into the correct foler

\\ Business Requirement is Explicitly Written in the Specflow
=============================================
Purpose
-------
In GAIN, Specflows are the main document for communicating requirements between business and developers. 
Lack of explicit requirements cause:
- Potential confusion and incorrect configuration
- Difficulty for the developer to understand and implement
- Difficulty for future people to understand the original purpose of the configuration and review or revise

PASS Example
------------
1. Look at the Scenario Outline title area
2. Does an explanation exist?
3. Does it match the test cases?

![](/specFlowWithComment.PNG)

Common Failure Scenarios
------------------------
- No explicit explanation of the rule logic
	- **Solution:** Interpret the requirement based on the Test Case
	- Write the interpretation down
	- Ask for a review and approval by BA and Business User

\\ Configuration Code Must Have Comments Pointing to SpecFlow Scenario Outlines
===========================================
Purpose
-------
In long SpecFlows with multiple logic parts and conditions, the following is needed:
- Comments in the configuration code need to exist in each code section
- Comments should point to granular portions of the SpecFlow
- Individual Scenario Outlines within a SpecFlow are perfect anchors

PASS Example
------------
1. Comment each Scenario Outline
2. If Scenario Outline has sub-rules, comment those as well

![](/commentsLongRule.PNG)

Common Failure Scenarios
------------------------
- No comments in the configuration
	- Add a comment, no brainer

\\ SpecFlow Has Enough Test Cases
=========================
Purpose
-------
Every SpecFlow should have enough cases to cover all reasonable scenarios

PASS Example
------------
![](/tests.png)


![](/testOutputGood2.png)


\\ All Test Cases Pass
======================
Purpose
-------
The configuration cannot be considered DONE until it passes all Tests defined in the SpecFlow

PASS Example
----------
- Check that all test cases pass, if not adjust the transformation
- If a test fails because the test case has errors, comment out the test case or make adjustments. 

![](/runTest.png)

 
1. No scripting/blocking errors

Purpose
-------
Before writing or updating a configuration rule, you can run the Specflow first to check for SpecFlow errors.
- This ensures that the SpecFlow works in Test Explorer
- A working SpecFlow means you can run tests as you configure
- At the end of your configuration you don't have to debug SpecFlow errors and Configuration errors simultaenously

PASS Example
---------
1. [Run feature tests]
2. Right click a failed test and select 'Test Output'
3. Check that all fields are appearing correctly and there are no run-time errors.
4. Error should exisit only because expected and actual strings differ
	- all others are SpecFlow errors
	- also check that all required inputs and outputs are registering
   

2. No business errors
     


\\ Code is Dependable and Efficient
=================
Purpose
------
The configuration code should be dependable and resilient. Good configuration code should:

- Correct for common sources or error
- Manage empty and null values
- Be short and compact as possible
- Use efficient structures such as Mappings
- Properly utilize Run conditions to avoid needless processing

PASS Examples
---------
Examples and details are given in [GAIN Specific Coding Guidelines]

\\ Four-eyes Check by Second Developer or BA
=================
Purpose
-------
To be completely DONE, all rules should be reviewed by another team member and approved

PASS Example
------------
- After review, a comment should be made in the SpecFlow to indicate the date and team member providing review

![](/specFlowWithComment.PNG)

\ Extra Example Walkthroughs
============================
Purpose
-------
These walkthrough provide extra step-by-step examples of how to use the Definition of DONE checklist. Each walkthrough contains multiple checklist items.

Walkthroughs
-----------
1. Checking for an Associated SpecFlow
2. Does the SpecFlow Run Without Errors

\\ Walkthrough 1 - Checking for an Associated SpecFlow
=============================
Purpose
-------
- The SpecFlow .feature files serve as both the functional requirement documentation and unit-level test for each configuration rule. 
- **Maintenance**: Without an associated SpecFlow in GainStudio, it is impossible to trace the configuration back to specific requirements making maintenance and verification impossible
- **Testing**: A SpecFlow must be associated to run individual configuration level unit tests in GAIN Studio. These test are much faster to run than tests involving full instrument creation and tranformation, and provide error messages and debugging.

### Step 1 - 'Jump to Test'
The fastest way to check if an associated test exists is to right-click on the configuration rule in question and click 'Jump to Test'. After a few seconds, the associated .feature file will be opened or you will find recieve a *Could not find related test* message.

![](/jumpToTest.png)

> **PASS/FAIL**
>
> IF .feature file opens, Check 1 
> THEN PASSED
>
> ELSE, move to Step 2 - Search for Tests

### Step 2 - Search for Tests and Consolidate
Often there are existing tests in the Test Explorer folder. If multiple exist for the same configuration, these tests should be consolidated to one .feature file and associated to the target configuration.

[Search for feature test]

> **PASS/FAIL**
>
> IF there one .feature file in the correct folder corresponding to this configuration
> THEN PASSED
>
> Else, move to Step 3 - Generate Test

### Step 3 - Generate Test
If no associated test is found, you should use 'Generate Test' to create a new feature file:

- .feature file will automatically be correctly associated, placed into the correct folder
- The correct Given, When, and Then commands will be automatically generated
- Any variables used in the configuration logic, will also automatically appear
- No danger of mispellings or other user errors

To create a test for a specific field:

1. Open the transformation and locate the field.
2. Open the context menu of the field in the transformation target window and select Generate test:
3. Fill out a test case, input and output should be the same, remove Process Context if it is not used in the current rule
4. Delete and type '|' on the last pipe of the table, this will auto-format and align the columns to make more readable test cases

![](/specFlowNoComments.PNG)

[Further Guidance on Generating Tests]

\\ Walkthrough 2 - Does the SpecFlow Run Without Errors
=================================================
Purpose
-------
The first step of implementing a new automated SpecFlow is the ensure that the testing script works:

- All inputs and outputs register correctly
- The correct model is used
- No breaking errors are triggered in the current configuration
- No breaking errors are triggered in any of the configurations that precede it (more on this later)

The objective of this check is not to Pass tests, but simply that the test script produces a testable output. Why?

- Ignoring this step makes troubleshooting harder later
- Errors caused by incorrect SpecFlow setup can be isolated and fixed before configuring
- Configuration becomes easier because intermediate tests can be run on the fly

Walkthrough
-----------
### Step 1 - Run the SpecFlow in Test Explorer
Run the SpecFlow in Test Explorer and Check that expected inputs, outputs and models are registering in the test.

1. [Search for feature test]
2. [Run feature tests]
3. Test cases will likely fail
4. right click a failed test and select 'Test Output'
5. Check that all fields are appearing correctly and there are no run-time errors.

![](/testOutput.png)

### Step 2 - Check Test Output that expected inputs, outputs and models are registering in the test with no errors
> **PASS/FAIL**
> IF test succeeds
> OR
> IF no errors are displayed 
> AND all input fields in the Given section are populated 
> AND the output field in the Then section is populated
> THEN PASSED
>
> ELSE, move to Step 3 - Troubleshoot errors

- Potential errors: {Model doesn't exist, field not appearing, field appears as placeholder}
- [Test Output Common Errors and Messages]

\\ Walkthrough 3 - Are Requirements Explicitly Documented
==============================
Purpose
-------
Configurations can only be maintainable if:

- The trail from requirements to test cases and code can be easily tracked
- All documents are accessible within GAIN Studio 
- Comments exisit within the configuration code pointing to Scenario Outlines
- Good explanation of logic exists in comments

Walkthrough
-----------
### Step 1 - Refer to spec flow and interpret the requirement
- Summarize the logic of the transformation rule if not already written in SpecFlow
- write the interpretation and logic summary under the Scenario Outline

### Step 2 - Refer to specific Scenario Outlines in the Configuration Code
- Comment the code block with a reference to the Test Scenario Outline that it is based on

```
// Begin Configuration Rule
// Corresponds to reqs and test in Scenario Outline: ISIN 
if (idIsin == "N.A.")
   return null;
else
   return idIsin;
```

\ Best practices to structure a transformation
=================================

MARTIAL
 - I would set these tips in a dedicated section (distinct from coding templates/tips)
 - I would set this section before section coding tips


This section provides generic advices on how to organize your transformation (InstrumentDerivation, Bloomberg normalization, ...).
The next section provides guidelines on how to best code each rule.


\\ Run conditions
==========
Explanation
---------- 
- Don't use run conditions to validate data. Run condition should only reflect business
- requirements that dictate a rule does not need to run. Better for the rule to rule and return null or existing value
- that for the rule to not run at all without total confidence that it's not needed
- Run condition considering more than the source source value of the current field must point to a spec flow requirement dictating this behavior
- Don’t put complex rules in the run conditions, as they are supposed to be used as precalculation. They should be fast.
- Using run conditions may speed up the process, as it can block a rule from running (important by complex rules).

\\ Order of the Rules
=====================
Explanation
-----------
- Keys should be normalizaed as first
- If a rule is dependant on another one, it should be lower in the normalization/derivation list.

\\ Miscellaneous Tips
=====================
Explanation
-----------
- Avoid excessive usage of ProcessContext.
- Avoid unnecessary usage of extension methods.
- Remember that complex rules slow down the normalization/derivation.

\\ Usings
=========
Explanation
---------
- Remember that usings can be only normalized, never derived (underlying, issuer).
- Remember there’s no selection rules for usings. Usings are never overriden. If it’s set to a non null value, it will stay like this ?
- The validation rules for using should be done at the entity level (i.e. issuer should be validated in the validation rule for the whole instrument).
- The normalization/derivation of components must be done as a child derivation of a parent class (example: ratings, schedules).

\ GAIN Specific Coding Guidelines
=================================
Guideline Structure
-------------------

A lot of rules contains same code piece:
   - if 
   - Mapping
   - ...

The best practice is to copy a pattern available in this section and adapt to your particular case.
You are then sure to have good basis for your coding.

Each page in this section will cover a common scenario. 
Each page contains:
- A code template or example of Best Practice
- Explanation for the recommended method
 
This section will assume basic familiarity with programming terminology and concepts. 
Beyond this three part structure, further reading and explaination for the feature will refer to the core GAIN Studio guide documentation.

Focus
-----
This section focues on:
- Controlling for common errors
- Shortcuts to save developer time
- Efficient code structure to speed up runtime

Contents
---------------
### Complete Rules
- 1:1 Transformation With Lookup

### Components and Concepts
- Assigning Variables for easier use and null-checking
- If...Else
- Lookups

\\ 1:1 Transfer with Lookup
========================================
MARTIAL: 
 - Sorry i don t understand what tranfer means here
 - For each rule you must give context: situation and target -> will help a lot to understand

Components
----------
- [If...Else]
- [Lookups]
- [Null Checking]

Best Practice Code Template 1
----------------

Context:
- Silver Copy field CountryOfRisk is associated to lookup Country
- Rule 
   - IF SC.CountryOfRisk IsNoNull THEN SC.CountryOfRisk = BBG.CNTRY_OF_RISK (no transformation)
   - ELSE SC.CountryOfRisk = Null

```
// Declare and assign variables
   // String
var countryOfRisk = Source.DescriptiveInfo != null && !string.IsNullOrEmpty(Source.DescriptiveInfo.CNTRY_OF_RISK) ? Source.DescriptiveInfo.CNTRY_OF_RISK : "";

// Begin configuration rule
if (!string.IsNullOrEmpty(countryOfRisk))
{
   return Lookups.Countries.GetItemById(countryOfRisk);
}
return null;
```

Explanation 1
------------
- DescriptiveInfo is null checked separately and before CNTRY_OF_RISK to prevent errors caused by invoking an empty - object
- Input from source is assigned to a local variable for easier handling
- GetItemById() always runs on a string which has been assigned to a local variable, never a null
- GetItemById requires lookup names in plural: Lookups.Countries.GetItemById (how to better express?)

Best Practice Code Template 2
----------------
```
// Begin Rule
// Corresponds to reqs and tests in PaymentRank: BBG.PAYMENT_RANK
if (Source.DescriptiveInfo != null && !string.IsNullOrEmpty(Source.DescriptiveInfo.PAYMENT_RANK))
{
	return Lookups.PaymentRanks.GetItemById(Source.DescriptiveInfo.PAYMENT_RANK.ToString());
}
else
	return null;
```

MARTIAL: i don t see added value compared to example 1, this is same thing no?
Explanation 2
-----------
- Sub-group of the Source, 'DescriptiveInfo', is null-checked before trying to access it's properties
- PAYMENT_RANK is string and checked using a string function
- No unneccesary type conversions
- Comments noting Test Scenarios in SpecFlow
- End with 'return null' as the final condition

Sub-optimal Configuration
-------------------------
```
if (Source.DescriptiveInfo.PAYMENT_RANK == null)
{
   return null;
}
else
   return Lookups.PaymentRanks.GetItemById(Source.DescriptiveInfo.PAYMENT_RANK.ToString());
```



\\ 1:1 Transfer with Mapping and Lookup
========================
Components
----------
- [If...Else]
- [Lookups]
- [Null Checking]
- [Mapping]
- [Assigning Variables]

Best Practice Code Template
----------------

Context:
- Candidate field FTSecurityType is associated to lookup FTSecurityType
- Candidate field FTIOClass is associated to lookup FTIOClasses
- Rule: FTIOClass is equal to ouput of mapping FTSecurityTypeToFTIOClass (FTSecurityType)
 


```
// Declare and assign variables
   // Lookups
var ftSecurityType = Target.FTSecurityType != null ? Target.FTSecurityType.ReferenceCode : "";
   // Output
var ftIOClass = "";

// Begin Rule
// Corresponds to reqs and tests in Scenario Outline: FTSecurityType
var result = !string.IsNullOrEmpty(ftSecurityType) ? Mappings.FTSecurityTypeToFTIOClass.Transform(ftSecurityType) : null;
ftIOClass = result != null ? result.FTIOClass : "";

return Lookups.FTIOClasses.GetItemById(ftIOClass);
```

Explanation
-----------
- The Lookup field, 'FTSecurityType', is null-checked before trying to access it's property, 'Reference Code'
- FTSecurityType is assigned to a string for easier use later
- Transform() and GetItemById() functions require strings and can't accept Null
- so variables used in those functions are checked and assigned beforehand
- Mapping can return Null if no match is found, so this is assigned to an intermediate var 'result'
- 'result' is null check before accesssing its property
- Comments noting Test Scenarios in SpecFlow

\\ Component - Assigning Variables
=====================
Best Practice Code Template
---------------------------


Context:
- Rule is complex, integrate a lot variables
 
 
```
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
```

Explanation
-----------
Assigning variables at the top has the following benefits:
- Easy to see all inputs used by this configuration
- shorter and easier to remember variable names
- Null checks that have multiple parts can be conducted once so that they don't need to be repeated later
- 'Generate Test' can include all fields before configuration rule is complete
- Variables can be organized by type for quick reference without leaving the configuration

More Information
----------
```
// Declare and assign variables
   // String
var countryOfRisk = Source.DescriptiveInfo != null && !string.IsNullOrEmpty(Source.DescriptiveInfo.CNTRY_OF_RISK) ? Source.DescriptiveInfo.CNTRY_OF_RISK : '';
```
In this example, country of risk comes from a connected level of the source called 'DescriptiveInfo'

- To correctly prevent errors caused by empty values, we must first check that the connected level exists
- Then check that the value that we are seeking exists
- This two step check can be performed one time at the beginning of the rule
- It is then only a single check when used later in the code.

\\ Component - Comments
=======================
Best Practice Code Template
---------------------------

Context:
- You must implement a rule specified in SpecFlow
- Each part of code refers to a specific scenario

```
 
// Begin Configuration Rules
// Corresponds to reqs and tests in Scenario Outline: XXYYZZ
if (...
...

// Corresponds to reqs and tests in Scenario Outline: ZZWWXX
if (...
...


Explanation
-----------
- Easy to find corresponding SpecFlow and Scenario
- Especially important in long configurations with multipart requirements
- Mark beginning of confirmation rules and indicate the Scenario Outline corresponding to each section
- At minimum, provide comment pointing the the reqs/test/specflow that defines this logic


\\ Component - Lookups: Equalities and Conditionals
===================================================
Best Practice Code Template
---------------------------
```
// securityCountryOfIncorporation uses the Country lookup, and has not been assigned to a string yet
if (securityCountryOfIncorporation == Countries.IE) {
	// something executed
}
// Conditionals with multiple arguments
if (securityCountryOfIncorporation == Countries.IE || securityCountryOfIncorporation == Countries.US) {
	// something executed
}

// ftIOClass is a string assigned earlier
if (ftIOClass == FTIOClasses.EQ.ReferenceCode) {
	// something executed
}
// Conditionals with multiple arguments, use || and && to combine conditions
if (ftIOClass == FTIOClasses.CS.ReferenceCode || ftIOClass == FTIOClasses.FI.ReferenceCode) {
	// something executed
}
```

Explanation
-----------
- When comparing lookups, don't compare strings, use the plural form of the lookup name to use a directory
- You can compare lookups directly to lookups, without going to the Reference Code
- This saves keystrokes when coding and saves a null-check on the Lookup
- Remember, Lookups class doesn't always match the name of the field (ex. SecurityCountryOfIncorporation => Countries)

Best Practice Code Template 2
--------------
```
if (Target.FTIOClass == FTIOClasses.EQ || Target.FTIOClass == FTIOClasses.FU || Target.FTIOClass == FTIOClasses.OP)
{
   return Source.DescriptiveInfo != null && !string.IsNullOrEmpty(Source.DescriptiveInfo.TICKER) ? Source.DescriptiveInfo.TICKER : null;
} 
else
{
   return null;
}
```

Sub Optimal Code 2
----------
```
# Sub-Optimal Code Example
if (Target.FTIOClass != null && Target.FTIOClass.ReferenceCode == "EQ" || Target.FTIOClass.ReferenceCode == "FU" || Target.FTIOClass.ReferenceCode == "OP")
{
   return Source.DescriptiveInfo != null && !string.IsNullOrEmpty(Source.DescriptiveInfo.TICKER) ? Source.DescriptiveInfo.TICKER : null;
} 
else
{
   return null;
}
```
Explanation 2
-----------
- Saves keystrokes
- Fewer transformations
- Less opportunity for error
- You are certain that you a using a valid lookup value

\\ Component - Mappings
=======================
Best Practice Code Template
---------------------------

Context:
- You must use ouput of mapping ExchangeCodeToCountry, input field Exchange

```
// exchange is a string assigned earlier
var result = !string.isNullorEmpty(exchange) ? Mappings.ExchangeCodeToCountry.Transform(exchange) : null;
countryOfListing = result != null ? result.Country : "";
```

Explanation
-----------
- Mappings: for single input mapping, input of a mapping must be a string.
- Assign result of Mapping to a new variable, then check Null on the variable to prevent error
- New variable will be a Mapping object, to get the value, you must access property of the result object
- You must always specifies the ouput field you want from mapping (result.Country), even if mapping has only 1 output field
- Mapping saves you from writing long multi-part if statements or case-switch statements
- Mappings can be reused between configurations
- Shorter code, faster run-time execution

More About Mappings
-------------
A mapping is basically a table that converts input data into an output value:

- Input fields: minimum 1, no maximum
- Output fields: minimum 1, no maximum
- A table of many mapped values can exist centrally and be called upon whenever needed.

An example of a situation to use mapping is to find the Country that an and exchange belongs in. (ie, NYSE -> US, Japan Stock Exchange -> JP, Deutche Borse -> DE)

### To use an existing Mapping, use the Transform() function
```
Mappings.XMappingClassX.Transform(inputs)
```
Every time you use the mapping, you must first assign the result to a variable, and then check that the result exists.

### Looking up Mappings
To find the mappings, you can locate the navigation here:

![](/mappings.png)

For more information on Lookup, look here
```
// Declare and assign variables
   // Output
string resetFrequency = "N";
var refixFreq = Source.FloatingRateInfo != null && Source.FloatingRateInfo.REFIX_FREQ.HasValue ? Source.FloatingRateInfo.REFIX_FREQ : null;

// Corresponding test cases Scenario Outline: ResetFrequency: REFIX_FREQ via mapping
if (refixFreq.HasValue)
{
   var ResetFrequencyMapped = Mappings.ResetFrequencyBbgToGainMapping.Transform(refixFreq);
   if (ResetFrequencyMapped != null)
   {
      resetFrequency = ResetFrequencyMapped.ResetFrequency;
   }
}
return Lookups.ResetFrequencies.GetItemById(resetFrequency);
```

\\ Component - Lookups: GetItemById
=================================== 
Best Practice Code Template
---------------------------
```
Lookups.XLookupClassX.GetItemById(XReferenceCodeX)
// ftIOClass is a string assigned earlier
return Lookups.FTIOClasses.GetItemById(ftIOClass);
```

Explanation
-----------
- When configuring fields that are a Lookup, you must return a lookup
- GetItemByID() changes a reference code in form of a string, to a lookup record

\\ Component - Null Checking
============================
Best Practice Code Template
---------------------------

Context
- 

```
	// Lookups
var exchange = Source.Exchange != null ? Source.Exchange.ReferenceCode : "";
var ftIOClass = Source.FTIOClass != null ? Source.FTIOClass.ReferenceCode : "";
	// Joined Objects
var underlying_countryOfListing = (Source.Underlying != null && Source.Underlying.CountryofListing != null) ? Source.Underlying.CountryofListing.ReferenceCode : "";
var maturity = Source.DescriptiveInfo != null && Source.DescriptiveInfo.MATURITY.HasValue ? Source.DescriptiveInfo.MATURITY : null;
	// Boolean
var isRegS = Source.IsRegS.HasValue ? (bool ?)Source.IsRegS.Value : null;
var is144A = Source.Is144A.HasValue ? (bool ?)Source.Is144A.Value : null;
	// Date
var maturityDate = Source.MaturityDate.HasValue ? Source.MaturityDate : null;
var expirationDate = Source.ExpirationDate.HasValue ? Source.ExpirationDate : null;
	// String
var referenceIndex = !string.IsNullOrEmpty(Source.ReferenceIndex) ? Source.ReferenceIndex : "";
var loanFacilityName = !string.IsNullOrEmpty(Source.LoanFacilityName) ? Source.LoanFacilityName : "";
```
Explanation
-----------
- Accessing the reference code or description of a Lookup value risk error if Lookup itself is null
- Accessing a value of any joined object such as Issuer of the Security or Underlying Security of an Option
	- Joined object must be checked for existence or there will be an error
- Dates, numbers and boolean should be checked with .HasValue property
- Strings should be checked with string.IsNullOrEmpty() to catch empty strings ""

\\ Arrays: Matching
==========================
Best Practice Code Template
---------------------------
Context
- You must determine if SecurityType of instrument is part of a list of 4 values

```
// Set the array
string[] ftSecurityTypeArrayRule2 = {"ADR", "GDR", "IDR", "DPP"};
// check if contains
if (ftSecurityTypeArrayRule2.Contains(ftSecurityType)) {}
```

Explanation
-----------
- Arrays are the Middle Ground between If...Else conditionals and Mappings. 
- They should be used sparingly and converted to Mappings wherever sensible.
- Appropriate usage of arrays for matching in conditionals is when there are many potential matching input values but few different output results. 
- In this case, matching an array can be more efficient than mappings or if...else statements.

\\ Arrays: Building up a String Made of Parts
==========================
Best Practice Code Template
---------------------------
```
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
```

Explanation
-----------
- Useful when building up a long string made of multiple parts and variable length
- This is better than directly concatenating string because it avoids trailing seperators (ie. commas, spaces)

\\ Formatting: Dates and Decimals
=====
Best Practice Code Template: Dates
Context
 - You want to convert a date field (MaturityDate) into a string, format Month/Day/Year
---------------------------
```
Source.MaturityDate.Value.Date.ToString("MM/dd/yyyy");
```

Best Practice Code Template: Decimals
---------------------------
```
// remove trailing zeros
	name_parts[i] = Source.CouponRate.Value.ToString("G29");
// remove first zero if it's less than 1
if (Source.CouponRate.Value < 1) {
	name_parts[i] = name_parts[i].Substring(1, name_parts[i].Length - 1);
}
```
