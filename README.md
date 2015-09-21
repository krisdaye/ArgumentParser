---
Title: ArgumentParser
Authors: Sari Sabouh, Alix Rosarion, Nikki Pruitt, Kris Daye,
         Stephen Dudchock, and Yi Chen
Last Updated: 20 September, 2015
Description: Command-Line Argument Parser for Java

---

#ArgumentParser
==============

This group project provides a user-friendly command-line argument parser library that allows 
the user to make use of arguments entered from the command line. ArgumentParser will 
generate help and usage information when requested or when an input error
occurs. Arguments and optional arguments can be either coded into the program 
or read in through an XML file via our XMLParser, which is included. This 
XML parser also provides the function of writing arguments defined in a program to an XML file.  
The goal of this library is to provide an easy and reliable source for any situation needing 
to parse values from a command line in Java.

**[The full Git repository and latest version available here!](https://github.com/krisdaye/ArgumentParser.git)**


###My Role
----------

Throughout this project, I assisted with the programming and logic issues we faced as a team. However,
my main contribution to this project was working on the acceptance tests, unit tests, creating
and refactoring the test mains, creating the Javadoc API, and presenting our sprint reviews.

The **Javadoc API** is located at /build/docs/javadoc/index.html 


###Requirements
----------
- A [JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) is required
- [Gradle](https://gradle.org/gradle-download/)


###Tools
----------

The following are the tools used in creation of this library.

- **Gradle**: Build Tool
- **Git**: Version Control Software
- **JUnit**: Java Unit Testing software
- **JaCoCo**: Acceptance Testing Software
- **Javadoc**: For creating the ArgumentParser API


###Methodology
-----------

Implemented the Scrum methodology of Agile. 

###Features
----------

1. **Ease of Use**

	One of the goals of our team was to create an easy to use way to create
	and define the arguments of a program. Creating the argument "length," for
	example, would be done by calling a simple function "addArgument." 
	*All of the functions are listed and documented in the API.*
	
	Example: 
	
	'''  
	parser.addArgument("length", CommandLineArgument.DataType.Integer);  
	parser.setDescription("length", "the length of the box");
	
	'''
	
	*If an argument is instantiated without a data type, the data type is defaulted to String.*
	
2. **Default Help Text**

	The optional argument 'help' is included in every program that uses this 
	library by default. Help, when called or when an input error is thrown,
	will gather the program description and the argument's attributes then
	display the information for the user to see. To call help, the user must
	either use the full name "--help," or the short name "-h."

	The following is an example of the displayed help text of a simple volume calculator:
	
	'''  
	C:\ArgumentParser>java VolCalc --help  
	
	usage: java VolCalc length width height  
	Calculates the volume of an object  
	
	Positional Arguments:  
	length  integer the length of the box   restricted to: 7 4  
	width   float   the width of the box  
	height  integer the height of the box  
	
	Optional Arguments:
	--help, -h      boolean  
	--type  string  Shape of object to be calculated       required        restricted to: sphere pyramid  
	--noisy boolean mutual group: 1  
	--verbose       boolean mutual group: 1  
	--quiet boolean mutual group: 2  
	--silent        boolean mutual group: 2  
	'''  

	When help is called on the volume calculator, the above information is listed
	for all arguments, both positional and optional. Each are defined as in the program as with
	their attributes. It displays the name, the order the positional arguments are
	read in, any restricted values, the data type, and if the argument is required. 
	If help is called, it will stop the program and print the help text regardless
	of any errors or lack thereof. 
	
	
3. **Optional Arguments Can Be Read From Any Position**

	ArgumentParser has been designed so that an optional argument can be read in without
	disrupting the parsing of values. This adds for relaxed use for the users, because
	they do not have to worry about the location while executing the program.
	
	
4.  **Short Names for Optional Arguments**

	ArgumentParser has the feature to add a short name to the optional argument. 
	Instead	of having to type "--help," the user will be able to simply type "-h."
	Both the long and short names of the help argument are enabled by default.
	
	Here is an example of setting a short name for an optional argument:
	
	'''  
	parser.setShortOption("type", "t");
	
	'''
	
	*All optional arguments, other than help, can be assigned any short name that has not been assigned already.*
	
	
5. **Required Optional Arguments**

	Some programs, such as the volume calculator used above, need a required optional
	argument to perform its task. The volume calculator above, for example,
	requires the optional argument "--type" to be present in order to know what shape
	it is calculating the volume of. This is done by the setRequired() method.  
	
	'''  
	parser.setRequired("type");  
	
	'''
	
	*ArgumentParser assumes that all positional arguments are required, and therefore they do not need to be set as required.*
	
6. **Restricted Values**

	With the setRestricted() method, an argument can be set to only accept the
	listed values. If a value is parsed that is not in the restricted list, an
	error is thrown and the help text is displayed showing the user the values
	that are accepted. Multiple values can be set as the restricted values. These
	values will need to be separated by commas.  
	
	'''  
	parser.setRestricted("length", 6, 4);  
	
	'''
	
	
7.  **Default Values**

	Optional arguments can be defined to have a default value. This will enable
	the program to run with an optional argument already in place. This makes it so
	that an optional argument does not need to be declared then the program runs. However,  
	if the optional argument is declared, then the values are read in and the default value is  
	overwritten with the new value.
	
	
8.  **XMLParser**

	With the XMLParser, arguments can be loaded from a pre-existing XML file. 
	With the arguments defined in the file, all that is needed to load them into
	the program is to call the XML parser and state the file name. 
	Note: the file must be in the root directory for it to be read in.
	
	Here is an example on reading in an XML file:  
	'''  
	ArgumentParser parser = XMLParser.createArgumentParser("arguments.xml");
	
	'''
	
	The XML parser will use the tags to parse the arguments into the program. 
	If proper format is not followed an exception will be thrown and the program
	will exit. For proper format review the file "XMLformat.xml" in the root folder. 
	
	In addition to reading in arguments, XML parser gives the user the ability
	to write the arguments and their attributes to an XML file. If the XML file
	already exists it will be overwritten, and if it does not exist it will be
	created with the specified name. The file is automatically written in proper  
	format with	the tags included.  
	
	To save to a file:  
	
	'''  
	XMLParser.saveXMLFile("filename.xml");
	
	'''
	
9.  **Javadoc API**

	This library comes with a documented javadoc API for the whole library. The
	API is located at /build/docs/javadoc/index.html


###Installation
---------------

Once ArgumentParser is either cloned or extracted from the .zip file, the example
programs included are almost ready to you. In CMD, move to the location of the
repository on your machine. Once there, use Gradle to build the repository.
The files in the root folder, the folders need to remain, are optional and
were left for examples on using the various features of the library. 
The import used from a fresh copy of Argument Parser is:  
'''  
import edu.jsu.mcis.*;  

'''  

[Gradle User Guide](https://docs.gradle.org/current/userguide/userguide_single.html)