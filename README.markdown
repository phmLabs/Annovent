#Annovent

Annovent is a simple to use event dispatcher inspired by the symfony component event dispatching implementation. It tries to provide all the features symfony does with some useful extensions.

##Simple Usage

The Annovent dispatcher can be used in a simple and standard way as you are used from symfony:

```php
$dispatcher = new Dispatcher();
$dispatcher->connect('SomeComponent.Render', array($listener, 'Method1'));
$dispatcher->notify(new Event('SomeComponent.Render', array('foo' => 'bar'));
```

##Namespace

An extra feature of this event dispatcher is the so called namespacing. It is possible to register a lister to a complete set events belonging to a special namespace.

```php
$dispatcher->connect('SomeComponent.*', array($listener, 'Method1'));
$dispatcher->connect('*', array($listener, 'Method2'));
```

The first listener will be notified whenever a event is fired that starts with SomeComponent. The second one will always be notified.

##Annotation

Connection a listener to a special event is not limited to the connect method. It is also possible to register a listener using annotation (see doctrine common). 

```php

class Listener
{
  /**
   * @Event("SomeComponent.Render")
   */
  public function method1(Event $event)
  {
  }
}

$dispatcher->connectListener( new Listener );
```

Using the connectListener method it is possible to connect a bunch of callbacks at once. 

##Named Parameters

If desired the event dispatcher can be used with named parameters.

```php
class Listener2
{
  /**
   * @Event("SomeComponent.Render")
   */
  public function method1($argument1, $foo)
  {
  }
}
$dispatcher->notify(new Event('SomeComponent.Render', array('foo' => 'bar', 'argument1' => 'arg1' ));
```

