Factory Class Groups
====================
This is essential in learning how overrides happen. We are going to start by
instantiating object in Magento.

Gang of four came up with with the Abstract Factory. A class that is dedicated
to instantiating other classes. This is what defines a factory pattern

Realization in Magento
----------------------
`Mage::getModel($modelClass = '', $arguments = [])`
This will then call an instance:
`getModelInstance($modelClass='', $constructArguments=[])`
In turn:
`getModelClassName($modelClass);`
And then we will get the group class name:
`getGroupedClassName=($groupType, $classid, $groupRootNode=null)`.

Magento will always interface within `Mage_Core_Model_Config`. Any answer to
configuration lies in here.

```php
$product = Mage::getModel('catalog/product');

/**
 * Retrieve model object
 *
 * @link Mage_Core_Model_Config::getModelInstance
 * @param string $modelClass
 * @param array $arguments
 * @return Mage_Core_Model_Abstract
 */
public static function getModel($modelClass = '', $arguments = [])
{
	return self::getConfig()->getModelInstance($modelClass, $arguments);
}
```
- grab a model: `Mage::getModel('catalog/_');`
-  grab a resource model: `Mage::getResourceModel('catalog/_);`
- grab a helper: Mage::helper('sales') == sales/data

```xml
<config>
	<global>
		<helpers>
			<sales>
				<class>Mage_Sales_Helper
```

These factory methods interact with the config files and you get objects.

An easy way to dump models, model resources, or even helpers:

```php
Zend_Debug::dump(
	Mage::getResourceModel('catalog/product')
);
die(get_class(Mage::getResourceModel('catalog/product')));
die(get_class(Mage::helper('sales')));
die(get_class(Mage::app()->getLayout()->createBlock('core/template')));
```
