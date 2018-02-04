****************************
Creating Core System Classes
****************************

Every time FSO runs there are several base classes that are initialized automatically as part of the core
framework. It is possible, however, to swap any of the core system classes with your own version or even just extend
the core versions.

**Most users will never have any need to do this, but the option to replace or extend them does exist for those
who would like to significantly alter the FSO core.**

.. note:: Messing with a core system class has a lot of implications, so make sure you know what you are doing before
    attempting it.

System Class List
=================

The following is a list of the core system files that are invoked every time FSO runs:

* Config\\Services
* FSO\\Autoloader\\Autoloader
* FSO\\Config\\DotEnv
* FSO\\Controller
* FSO\\Debug\\Exceptions
* FSO\\Debug\\Timer
* FSO\\Events\\Events
* FSO\\HTTP\\CLIRequest (if launched from command line only)
* FSO\\HTTP\\IncomingRequest (if launched over HTTP)
* FSO\\HTTP\\Request
* FSO\\HTTP\\Response
* FSO\\HTTP\\Message
* FSO\\Log\\Logger
* FSO\\Log\\Handlers\\BaseHandler
* FSO\\Log\\Handlers\\FileHandler
* FSO\\Router\\RouteCollection
* FSO\\Router\\Router
* FSO\\Security\\Security
* FSO\\View\\View
* FSO\\View\\Escaper

Replacing Core Classes
======================

To use one of your own system classes instead of a default one, ensure that the :doc:`Autoloader <../concepts/autoloader>`
can find your class, that  your new class extends the appropriate interface, and modify the appropriate
:doc:`Service <../concepts/services>` to load your class in place of the core class.

For example, if you have a new ``App\Libraries\RouteCollection`` class that you would like to use in place of
the core system class, you would create your class like this::

    namespace App\Libraries;

    class RouteCollection implements \FSO\Router\RouteCollectionInterface
    {

    }

Then  you would modify the ``routes`` service to load your class instead::

	public static function routes($getShared = false)
	{
		if (! $getShared)
		{
			return new \App\Libraries\RouteCollection();
		}

		return self::getSharedInstance('routes');
	}

Extending Core Classes
======================

If all you need to is add some functionality to an existing library - perhaps add a method or two - then it's overkill
to recreate the entire library. In this case it's better to simply extend the class. Extending the class is nearly
identical to replacing a class with a one exception:

* The class declaration must extend the parent class.

For example, to extend the native RouteCollection class, you would declare your class with::

    class RouteCollection extends \FSO\Router\RouteCollection
    {

    }

If you need to use a constructor in your class make sure you extend the parent constructor::

        class RouteCollection implements \FSO\Router\RouteCollection
        {
            public function __construct()
            {
                parent::__construct();
            }
        }

**Tip:**  Any functions in your class that are named identically to the methods in the parent class will be used
instead of the native ones (this is known as “method overriding”). This allows you to substantially alter the FSO core.

If you are extending the Controller core class, then be sure to extend your new class in your application controller’s
constructors::

	class Home extends App\BaseController {

	}

