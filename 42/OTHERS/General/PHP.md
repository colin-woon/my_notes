# All php code must be executed in this way **if embedded in html**:
```
<?php {your-php-code-here}?>;
```

# Variables start with:
```
${variable-name};
```

# Constants:
```
define({VARIABLE-NAME}, {value});
```
When referencing:
```
{VARIABLE-NAME};
```

# Variable scoping:
```
$variable = 'outside';

function sayVariable($variable){
	$variable = "inside"; 
	echo $variable;  //Result: "inside"
}
sayVariable($variable);  //Result: "outside"
---------------------------------------------------
function sayVariableAgain(){
	global $variable;
	$variable = "inside";
}
sayVariableAgain();
echo $variable;  //Result: "inside"

function sayVariable(&$variable){
	$variable = "outside"; 
	echo $variable;  //Result: "outside"
}
sayVariable($variable);  //Result: "outside"
```

# For strings:
```
"This is a ${variable-name}";    //Will reference the variable

'This is not a $variable';       //Will not reference the variable

'This is a ' . ${variable-name}; //Concatenate the variable
```

# Arrray
```
$indexedArray = ['0','1','2'];
print_r($indexedArray);

//--Two ways to append:
$indexedArray[] = '3';
array_push($indexedArray[3], '3');

count($indexedArray); //counts number of elements

//--Another way to create index
$associativeArray = array('1stIndex' => '0', '2ndIndex' => '1', '3rdIndex' => '2');

$multidimensionalArray = [
[firstArray],
[secondArray],
[thirdArray],
];
```
When referencing:
```
echo indexedArray[1stIndex]; // = 1
echo "This is {$multidimensionalArray[secondArray]}.";
```

# Functions
```
function aFunction($param1 = {default-value, $param2 = {default-value2}}){
	return {OPTIONAL};
}
```

# include & require
If error, will print "Continues":
```
<?php include({filepath}); ?>
echo "Continues";
```

If error, will **NOT** print "Continues": (similar to a break)
```
<?php require({filepath}); ?>
echo "Continues";
```


# Referencing Object Properties
```
${classInstance}->{property-name}; //Get the object value
${classInstance}->{property-method}(); //Can access the object method
```