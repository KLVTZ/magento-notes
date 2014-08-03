Magento Directory Structure
===========================

We will look at locating various files in directory structure. We will notice
that in our magento root, we have a hierarchy is based on keyword-based logic.
The files under application are never accessed by a browser.

Root
----

* app
  * code: contains the magento code seperated into code pools
  * design: contains the magento design templates and custom design templates
  * Contains localizations for different languags

* js
  * calander: calendar JS widget library
  * enterprise: JS libraries contributed within enterpise modules
  * Extjs
  * lib: A set of 3rd party JS libraries
  * mage: js developed by magento
  * prototype: prototype js libraries
  * scriptaculous: js library
  * tiny_mce
  * varien "old" magento libraries namespace

* lib --Autoloader access this directory
  * Varien: "another magento" libraries namespace
  * Zend: Framework
  * LinLibertineFont

* media - exclude in verion control
  * catalog: media files store here
  * custmer
  * downloadable
  * import

* skin
  * adminhtml: admin area skin files
  * Front area skin files
  * install wizard skin files

* var: transient data. emptied out, whenever.
  * cache: system and user cache
  * session: session files
  * tmp: plan for temp files


Module directory structure
--------------------------

* Block --must
* controllers
* etc --must
* Helper --must
* Model --must
* sql

Block:
------
is an additional layer between controllers and view representation of
the application. For Blocks, we use create block. We would see:
`Mage_Catalog_Block_Product_View` called is
`createBlock('catalog/product_view')`. Catalog maps to a prefix and after the
slash means the actual block info path.

Controllers
-----------
Controllers provided by module. An action (or case) controlle rprocess web
server requests. The controller is a conventional routing systems based upon
paths. The controllers are not included by the auto-loader.


etc
---
Contains module configuration and system files. You can store anything and set
anything in configuration, It is all merged together. Your Magento application
will go through the app/etc/module folder first, before here.

Helper
------
Helper is an auxillary class that encapsulates some commonly used module
functionality and makes it publicly available to other modules. Different
factory method.

sql
---
Contains module data base setup and upgrade files. Very cool if you need to
setup some configuration for a team environment that is setup automatically.

Code Pools
----------
Inside `app/code` is `local`, `community`, `core`. This is a unique directory
that consists of grouped code. As usual it identifies a high level of code
organization. The system looks in local, community, and then core.

You will never edit your `app/code/core` team only. Just make sure to get rid of
added whitespace and any die and dumps.

PHP Include Path Order
----------------------
```php
# app/Mage.php
$paths = array();
$paths[] = BP . DS . 'app' . DS . 'code' . DS . 'local';
$paths[] = BP . DS . 'app' . DS . 'code' . DS . 'community';
$paths[] = BP . DS . 'app' . DS . 'code' . DS . 'core';
$paths[] = BP . DS . 'lib';

$appPath = implode(PS, $paths);
set_include_path($appPath . PS . Mage::registry('original_include_path'));
include_once "Mage/Core/functions.php";
include_once "Varien/Autoload.php";
```
We register the included path and then use Varien's Autoloader to load each
module:

```php
# ap
/**
 * Load class source code
 *
 * @param string $class
 */
public function autoload($class)
{
	if ($this->_collectClasses) {
		$this->_arrLoadedClasses[self::$_scope][] = $class;
	}
	if ($this->_isIncludePathDefined) {
		$classFile =  COMPILER_INCLUDE_PATH . DIRECTORY_SEPARATOR . $class;
	} else {
		$classFile = str_replace(' ', DIRECTORY_SEPARATOR, ucwords(str_replace('_', ' ', $class)));
	}
	$classFile.= '.php';
	//echo $classFile;die();
	return include $classFile;
}
```

Namespace
---------
Is a unique name that usually identifies a company or an organization. Each
contributing or an organization. Each contributing member of the magento
community should use their own Namespaces name when creating the modules in
order to avoid colliding with another user's code. The namespace is going to be
the folder strucure. It keeps us from installing a module that may override.

`app/code/local/Training/Fool`. If we where to use the Mage core catalog view,
the magento core wouldn't be available. Because the autoloader would check in
the local code pool first. That is not good. The only time used in a justifiable
way is to override an abstract class. Usually this is bad for a use case. If
your solution is to override an entire class, you're doing it wrong.

Locating Templates
------------------
`app/design/[AREA_NAME]/[PACKAGE_NAME]/[THEME_NAME]/template/[MODULE NAME]`.

To find templates in magento apps, this is where you look in your
`app/design/frontend` or if it was admin, then it would be
`app/design/adminhtml`. Those are area names

Package names are just folder, speicifed in the admin or theme. There is a whole
other system that has a design fallback. Depending on whether magento finds a
certain file in place. An important thing to remember is that a template file
must set a template, providing a file path relative to a folder.

Everything is just a folder.

Locating Layout XML
-------------------
`app/design/[AREA_NAME] + [PACKAGE_NAME]/[THEME_NAME]/layout/[NAMESPACE_NAME]

Your default templates are under base default folders.

Locating Skins
--------------
`skin/[AREA_NAME]/[PACKAGE_NAME]/[THEME_NAME]/js/css/images/[NAMESPACE_NAME]`

Locating JavaScript
-------------------

`js/[NAMESPACE_NAME]/[MODULE_NAME]/`

Locating Temporary Directory
----------------------------
var/import/[MODULE_NAME]
  /export/[MODULE_NAME]
  /tmp/[MODULE_NAME]

You don't have to do this, but it is not recommended.


Exercise
--------
We can go to any of our config.xml files within our module namespace and find
that each are determined by a class prefix. This prefix is used within our XML
file that then represents are applications order.

```xml
    <global>
        <models>
            <catalog>
                <class>Mage_Catalog_Model</class>
```


Collections are a special type of model. They are found in a different
configured path.
