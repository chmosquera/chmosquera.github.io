---
title: sCool Builder Game
date: 2020-07-09
image_path: assets/images/2020/sCool_theoretical_mode_build1.png
feed: show
showhomefeed: true
categories:
  - project
tags:
  - Research
  - C#
  - Unity Engine
  - Game Development  
---

This post showcases game mechanics in sCool's new Builder Game. It also serves as an aid for future development.

![](/assets/images/2020/sCool_theoretical_mode_build1.png)


_Scenario:_
The player encounters a villager who needs help building furniture. They gave you a blueprint of how to make it. Make sure you place all required blocks in the correct spot. And do your best to get the block's placement, size, rotation, and color as close as possible to the villager's wants.

_Technical Description_
The Blueprint class contains a list of blocks. Each instance of the Block object has properties it can change (e.g. position, scale, rotation, color). Using Unity's entity component system,  these properties can be changed by referencing an entity's (Block) component and then modifying a property of that component. 

![](/assets/images/2020/sCool_blockbuilder.png)
A Unity gameobject contains a Transform component which contains the properties: position, scale, and rotation.
	
_Example: To move the block to the right, we access the block gameobject's Transform component and change position's value._

## Workshop, Blueprint, and Block Classes
These classes make up the main visual aspects of the Builder Game, thus they all derive from Unity's Monobehaviour class.

### Block
The Block script is attached to a rendered mesh and as mentioned earlier, contains a list of Component instances, which then contains a list of Property instances. The Comonent and Property classes are needed to allow players to customize a block game object. More on this later. 

### Blueprint
The Blueprint script is attached to the parent game object of all the blocks. The script itself contains a reference to all of these blocks and it provides the infrastructure for where each block is placed. 

### Workshop
The Workshop script is attached to the parent game object of the blueprint. There can only be one instance of the workshop and it may be accessed using Workshop.Instance .  The workshop communicates between the user and the bluprint. It contains function that enable modifications to the blueprint and any of its blocks. These functions are linked to the UI which will be described later. 

## Other necessary classes
Property  this is used to define gameobjects that contain infromation about its associated Property<T,V>. For simplicity, it uses the Property templates defined in the Block script. 


## Components and Properties

### Accessing C# Classes, Fields, and Properties using C# LINQ Library and Reflection API

Blocks contain a list of components, and each component contains a list of properties. Components can be of different classes such as Transform and MeshRenderer. Therefore, we define the Components class as a generic class: Component<T>. 
Furthermore, to loop through a list of generic components, the components must share a similar interface. (Properties follow the same structure, but with two parameters). For both Component and Property, T is for Unity's Monobehaviour component (e.g. UnityEngine.Transform), and V is string of the name of the component's property (e.g. localPosition). The resulting code architecture looks like this:


```cs
public interface Icomponent {}
public class Component<T> : Icomponent {}

public interface IProperty {}
public class Property<T, V> : IProperty {}
```

### LINQ and Reflection

A little bit about LINQ and Reflection. LINQ, or Language Integrated Query, "is a uniform query syntax in C# and VB.NET to retrieve data from different sources and formats." [[Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/linq/) / [TutorialsTeacher](https://www.tutorialsteacher.com/linq/what-is-linq)]  Reflection is "used to examine the metadata in a .NET assembly and create collections of types, type members, parameters, and so on that are in that assembly." [[Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/linq/how-to-query-an-assembly-s-metadata-with-reflection-linq)].

#### What do we need LINQ and Reflection for?
In order to create Component<T>  classes and Property<T,V> classes at runtime, we define a function with multiple parameters (strings and objects), and then use LINQ and Reflection libraries. This is done from the Block class, thus "this" refers a Block instance.

Here are the functions and how to use them:
```cs

// Calling the functions
AddComponent("UnityEngine.Transform, UnityEngine", new object[] { this.transform });

AddProperty("UnityEngine.Transform", "UnityEngine.Vector3, UnityEngine", new object[] { icomponent, new Vector3(1, 0, 1), "localPosition" });


// Function definitions
public IComponent AddComponent(string componentTypeName, object[] componentArgs)
{
	// Don't add components that already exist in the list
	Type componentType = Type.GetType(componentTypeName); 
	if (FindComponent(componentType.ToString()) != null) {
		Debug.Log(this.name + ": Component '" + componentType.ToString() + "' already exists.");
		return FindComponent(componentTypeName);
	}
	// 1 Generate component
	IComponent component = GenerateComponent(componentTypeName, componentArgs);
	// 2 Add to list
	components.Add(componentType.ToString(), component);
	return component;
}

public IProperty AddProperty(string componentID, string propertyTypeName, object[] propertyArgs) {

    string propertyName = (string)propertyArgs[2];  // will be used as ID 

    // Generate an instance of Property<componentName,propertyName>
    Type propertyType = Type.GetType(propertyTypeName);
    Type componentType = components[componentID].GetType();
    Type genericBase = typeof(Property<,>);                         // Property
    Type[] dataType = new Type[] { componentType, propertyType};    // + <T,V>    
    Type combinedType = genericBase.MakeGenericType(dataType);      // = Property<T,V>
    IProperty property = (IProperty)Activator.CreateInstance(combinedType, propertyArgs);                

    // Add property to component            
    components[componentID].GetProperties().Add(propertyName,property);

    return property;

}
```

#### Working with strings can be a bit tedious, and I can't remember what goes into the array of objects! Do I need to do this everytime I want to add a component or property?


Kind of but not really? We define some common templates of components and properties, so the tedious string and object[] stuff only needs to be defined in one place in the code. Then, you can expand the list of templates

```cs
public enum PropertyTemplates { localPosition, localScale };
public enum ComponentTemplates { Transform };

public IComponent AddComponent(ComponentTemplates template) {
	IComponent component = null;
	switch(template) {
	case ComponentTemplates.Transform:
		component = AddComponent("UnityEngine.Transform, UnityEngine", new object[] { this.transform });
		break;
		
		// Extend this list with more components
	}
	return component;
}

public IProperty AddProperty(PropertyTemplates template) {
IProperty property = null;
	switch (template) {
		case PropertyTemplates.localPosition:
			IComponent icomponent = FindComponent("UnityEngine.Transform");
			if (icomponent == null) {
				icomponent = AddComponent(ComponentTemplates.Transform);
				Debug.Log(this.name + ": Generated new component, '" + icomponent.GetName());
			}
			property = AddProperty("UnityEngine.Transform", "UnityEngine.Vector3, UnityEngine", new object[] { icomponent, new Vector3(1, 0, 1), "localPosition" });
			break;
			
		// Extend this list with more properties
	}
	return property;
}
```

## UI: Drag and Drop System
Players interact with a drag and drop system to add blocks, properties, and extensions.  UI elements that can be dragged we will refer to as a "draggables", which contain a Draggable<T> script, and a defined place we are allowed to drop draggables onto will be referred to as "placeholders", which contain a Placeholder<T> script. 

Again we are using generic classes here. This is to differentiate draggables/placeholders for different items: blocks, properties, and extensions (tbd). 

```cs
	public class Draggable<T> : MonoBehaviour, IDraggable, IBeginDragHandler, IDragHandler, IEndDragHandler, IPointerDownHandler, IPointerUpHandler {}
	
	public class BlockDraggable : Draggable<Block> {}
	public class PropertyDraggable : Draggable<Property> {}
	
	public class BlockPlaceholder : Placeholder<Block> {}
	public class PropertyPlaceholder : Placeholder<Property> {}
	
```	
	
Here are some rules about how draggables or placeholders work:
	- Clone or swap
	- Draggables of type T can only be placed on Placeholders of type T. 
	

### DragDropSystem
The DragDropSystem script contains many UnityEvents which are invoked within the `Draggable<T>` script.  Functions can be added to the UnityEvents by using Unity's Editor interface. Working very closely with the Workshop game object, this part is essential in connecting the UI to the rest of the game. 


%%# A walk-through example of the whole process
Prompt: _I want blocks to be customized to light up!_%%

%%This section is in progress%%



