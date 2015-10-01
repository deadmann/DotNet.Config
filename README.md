# DotNet.Config

## About 

DotNet.Config is a small and powerful configuration library for .NET.  

For sys admins and non-technical end users, configuration settings are a breeze to edit in a simple ini-format text file.

For developers, it has the power to 'glue' configuration settings directly onto your classes based on the convention of member variables in classes matching the names of configuration settings.

## Features

* **Easy to add**: add a reference, create a new config.properties file, and with one line of code your class already has access to config settings.
* **Hassle free config files**: simple and straight forward text-based config files. No more HTML encoding settings in ugly XML files. 
* **Load anywhere**: configuration settings can be loaded by any component, whether the main .exe or a dll. No more fighting with .NET if you want to ship a dll with its own configuration.
* **Inspired by Java**: config.properties files are inspired by Java's simple text-based config files 
* **Variable substition**: baked in support for variable substitution in your config files. 
* **Flexible**: Full support of multi-line configuration settings
* **Glue it on**: features a unique "glue on" approach that applies configuration settings directly onto your class. It will even casting of int / enum /datetime datatypes!

## Usage

Start using DotNet.Config with one line of code.

1. Add a reference to DotNet.Config
2. Add "using DotNet.Config;" to your class imports
3. Create a config.properties file (properties->copy to outputdirectory) like this:

  ````dosini
  size=12
  dateTime=1/12/2014
  name=Terry Tester
  color=Blue
  quote=Today is $dateTime and the sky is
      bright $color.
  ````
4. And you're ready to go:

  ````csharp
  using DotNet.Config;
  public class MyClass {
  
    public enum Color { Red, Blue, Green };
  
    #region Glue-on properties
    //DotNet.Config will glue values from your config.properties directly onto your member variables:
    private int size; //casts non-string values 
    private DateTime dateTime;
    private string name;
    private string _quote; //supports private variables prefixed with an underscore
    private Color color; //supports enums
    #endregion
  
    public MyClass() {
  
      //this tells DotNet.Config to fetch the config.properties file and glue it onto this class
      **AppSettings.GlueOnto(this);**
  
      /*
      this.size == 12
      this.name == "Terry Tester"
      this.color == Color.Blue
      etc
      */
  
    }
  }
  ````
  

## History 

This code started out of a need to include a simple configuration system with Dll's written as a third party.
Over time, it evolved into a light weight configuration system that simply "glue" properties onto classes.


