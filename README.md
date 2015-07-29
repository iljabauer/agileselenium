# Getting Started

## Provider
To configurate the NatSpec Selenium Library you have to create a class wich extends the `AgileSeleniumProvider` class and implements the `ISyntaxpatternProvider` interface. In this class all available pages of your application are registered with its components. 

To create the provider class you have to import three dependencies from NatSpec:
```java
de.devboost.natspec,
de.devboost.agileselenium.patternprovider,
de.devboost.natspec.testscripting.java

```

An example of this class could look like this:
```java
package de.agileselenium.provider;

import de.devboost.agileselenium.patternprovider.AgileSeleniumProviderEN;
import de.devboost.agileselenium.patternprovider.Component;
import de.devboost.agileselenium.patternprovider.ComponentType;
import de.devboost.agileselenium.patternprovider.Page;
import de.devboost.natspec.patterns.ISyntaxPatternProvider;


public class PatternProvider extends AgileSeleniumProviderEN implements ISyntaxPatternProvider {

	public PatternProvider() {
		super("/de.agileselenium.test/", 
				
				new Page("HomeScreen", "/", 
						new Component("#password_field", "Password", ComponentType.PASSWORDFIELD),
						new Component("#username_field", "Username", ComponentType.TEXTFIELD),
						new Component("#submit", "Submit", ComponentType.BUTTON)	
				),
				
				new Page("OrderScreen", "/order", 
						new Component("#order_table", "OrderTable",ComponentType.TABLE)
						/* ... */
				)
				/* ... */
		);
	}
}
```
You have to implement a parameterless constructor for this class. The first argument of the super call is the qualified name of the package that contains your Selenium Tests. In this example it is `"/de.agileselenium.test/"`. All other arguments are instances of the `IPage` interface which define the registered Pages of your application. You can use the already implemented `Page` class:
```java
new Page("HomeScreen", "/", 
  	new Component("#password_field", "Password", ComponentType.PASSWORDFIELD),
  	new Component("#username_field", "Username", ComponentType.TEXTFIELD),
  	new Component("#submit", "Submit", ComponentType.BUTTON)	
)
```
The first argument is the name of the screen which is used in your NatSpec tests, the second the url of the screen. All other arguments are instances of `IComponent` to specify the components that are in your page. To create a component you can use the `Component` class. You have to define the CSS-Selector of the component (`#password_field`) the name which is used in the tests (`Password`) and the type of the component (`ComponentType.PASSWORDFIELD`). 

The pages and the components you define in the Provider class are used to generate the NatSpec sentence you can use in your Selenium Tests. For example you can use the `Navigate to HomeScreen` sentence when you have declared your HomeScreen in the provider class.

## Testing with NatSpec and Selenium
After you have finished the configuration you can start writing your NatSpec tests. All you have to do is to create a _NatspecTemplate

<!---
dependencies
## Project Setup
3 plugins: provider, configuration, tests

##provider
add
>MANIFEST.MF
Bundle-ClassPath: bin/,
.


##tests
_NatSpecTemplate:
private SeleniumSupport seleniumSupport.
-->
