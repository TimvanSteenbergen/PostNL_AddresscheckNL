# PostNL_AddresscheckNL
Dutch Address Check by PostNL. This is a Mendix module, using the PostNL-API 'Addresscheck National'.

The documentation on PostNL, https://developer.postnl.nl/browse-apis/addresses/adrescheck-nationaal/documentation-rest/, says: 
Adrescheck Nationaal
Simply use the API to check Dutch address data that is entered in your webshop or CRM.
Method

The following methods are defined within the Adrescheck Nationaal.
Method
	Description
https://api.postnl.nl/address/national/v1/validate
	API that validates national addresses in a general format (send any of a list of pre-defined fields)
Please note: You can opt to require users to fill in a complete address (with all pre-defined fields that make up an address) or choose to only use a smaller set of fields. It can be attractive to use one of these input structures instead of requiring users to fill out a complete address format to help increase conversion rate of the form.

Unique Dutch addresses can be found based on the following 2 input structures (next to presenting all pre-defined fields) that make use of fewer input fields;

    Postalcode + HouseNumber + Addition (advised to include, although not all HouseNumber ranges include additions)
    Street + HouseNumber + Addition (advised to include, although not all HouseNumber ranges include additions) + City

Note: This API supports the POST method
Call details

Preview the API call buildup below.

Method: https://api.postnl.nl/address/national/v1/validate
Guidelines

The Adrescheck Nationaal is available in 2 different forms that differ on the input fields structure. The different methods provide an optimal way to implement the address verification in your tooling (webform, CRM etc).

General format (send any of a list of pre-defined fields). You can opt to require users to fill in a complete address (with all pre-defined fields that make up an address) or choose to choose a subset of fields. Unique Dutch addresses can be found based on the PostalCode+HouseNumber+Addition (dependant on the existence of an Addition in the HouseNumber range) or Street+HouseNumber+Addition+City. It can be attractive to use one of these subsets instead of requiring users to fill out a complete address format. To reduce the amount of fields the single line method can be, depending on your preference, even more attractive.

Scenario’s
Scenario 1; When given a correct Postalcode, Housenumber and Addition combination was entered, the output should be a single output.

Scenario 2; When the housenumber is not found for a given Postalcode, an empty response is returned.

Besides these two, numerous combinations are possible. Below there are listed, including the expected outcome.

Input
	

Scenario
	

Expected outcome

Input = Postalcode + Housenumber
	

1. existing Postalcode + Housenumber
	

All addresses with the exact Postalcode-Housenumber combination are returned.
If there are known Addresses with Addition for this this combination they are returned as well.

Input = Postalcode + Housenumber
	

2. non-existing Postalcode + Housenumber
	

Error 

Input = Postalcode + Housenumber
	

3. existing Postalcode + non-existing Housenumber
	

Error 

Input = Postalcode + Housenumber + Addition
	

1. existing Postalcode + Housenumber, in the scenario that all these combinations contain an Addition.
	

All addresses that are known are returned, including subnumbers (for example the Addition “A” is given while only “A01”and “A02” exist).
If the given Addition is not found, all Addresses with Additions are returned for the user to choose from.

Input = Postalcode + Housenumber + Addition
	

2. non-existing Postalcode + Housenumber with an Adddition. In those cases that only addresses including an Addition exist.
	

Error

Input = Postalcode + Housenumber + Addition
	

3. existing Postalcode + Housenumber. In those cases that Addresses with and without known Additions exist.
	

All addresses that are known are returned, including subnumbers (for example the Addition “A” is given while only  “A01”and “A02” exist).
If the given Addition is not found, all Addresses with Additions are returned for the user to choose from.

Input = Postalcode + Housenumber + Addition
	

4. non-existing Postalcode + Housenumber. In those cases that Addresses with and without known Additions exist.
	

Error

Input = Postalcode + Housenumber + Addition
	

5. existing Postalcode + Housenumber. In those cases that no known Additions exist.
	

All addresses that are known are returned, including subnumbers (for example the Addition “A” is given while only “A01”and “A02” exist).
If the given Addition is not found, all Addresses with Additions are returned for the user to choose from.

Input = Postalcode + Housenumber + Addition
	

6. non-existing Postalcode + Housenumber with no known Additions
	

Error

Input = Street + Housenumber + Addition + City
	

1. existing Street + existing City + Housenumber. In those cases that only addresses including an Addition exist.
	

All addresses that are known are returned, including subnumbers (for example the Addition “A” is given while only “A01”and “A02” exist).
If the given Addition is not found, all Addresses with Additions are returned for the user to choose from.

Input = Street + Housenumber + Addition + City
	

2. existing Street + non-existing City + Housenumber.  In those cases that only addresses including an Addition exist.
	

Error

Input = Street + Housenumber + Addition + City
	

3. existing Street + existing City + Housenumber. In those cases that Addresses with and without known Additions exist.
	

All addresses that are known are returned, including subnumbers (for example the Addition “A” is given while only “A01”and “A02” exist).
If the given Addition is not found, all Addresses with Additions are returned for the user to choose from.

Input = Street + Housenumber + Addition + City
	

4. existing Street + non-existing City + Housenumber. In those cases that Addresses with and without known Additions exist.
	

Error

Input = Street + Housenumber + Addition + City
	

5. existing Street + existing City + Housenumber. In those cases that no known Additions exist.
	

All addresses that are known are returned, including subnumbers (for example the Addition “A” is given while only  “A01”and “A02” exist).
If the given Addition is not found, all Addresses with Additions are returned for the user to choose from.

Input = Street + Housenumber + Addition + City
	

6. existing Street + non-existing City + Housenumber with no known Additions.
	

Error

Input = Street + Housenumber + Addition + City
	

7. non-existing Street + existing City + Housenumber. In those cases that only addresses including an Addition exist.
	

All addresses that are known are returned, including subnumbers (for example the Addition “A” is given while only “A01”and “A02” exist).
If the given Addition is not found, all Addresses with Additions are returned for the user to choose from.

Input = Street + Housenumber + Addition + City
	

8. non-existing Street + non-existing City + Housenumber. In those cases that only addresses including an Addition exist.
	

Error

Input = Street + Housenumber + Addition + City
	

9. non-existing Street + existing City + Housenumber. In those cases that Addresses with and without known Additions exist.
	

If possible suggestions

Input = Street + Housenumber + Addition + City
	

10. non-existing Street + non-existing City + Housenumber. In those cases that Addresses with and without known Additions exist.
	

Error

Input = Street + Housenumber + Addition + City
	

11. non-existing Street + existing City + Housenumber. In those cases that no known Additions exist.
	

If possible suggestions
Requests

The following input parameters should be used
Attribute	Mandatory	Format	Description	Example
Country		String [2]	The ISO2 country codes	NL
Street		String [0-95]	The streetname of the delivery address	Siriusdreef
HouseNumber		String [0-35]	The housenumber of the delivery address	42
Addition		String [0-35]	Housenumber extension	A
PostalCode		String [4-10]	Zipcode of the address	2132WT
City		String [0-35]	City of the address	Hoofddorp

The following output parameters are returned:
Attribute	Format	Description	Example
Street	String [0-95]	The streetname of the delivery address	Siriusdreef
HouseNumber	String [0-35]	The housenumber of the delivery address	42
Addition	String [0-35]	Housenumber extension	A
PostalCode	String [4-10]	Zipcode of the address	2132WT
City	String [0-35]	City of the address 	HOOFDDORP
FormattedAddress	3 Strings [0-95]	Full formatted address	Siriusdreef 42 A 2132WT HOOFDDORP
Example (scenario 1)

Request

{
    "PostalCode": "2132WT", 
    "City": " ",
    "Street": " ",
    "HouseNumber": "42",
    "Addition": "A"
}

Copy

Response

[
  {
    "City": "HOOFDDORP",
    "PostalCode": "2132WT",
    "Street": "Siriusdreef",
    "HouseNumber":42,
    "Addition": "A",
    "FormattedAddress": [
      "Siriusdreef 42 A",
      "2132WT HOOFDDORP"
    ]
  }
]
