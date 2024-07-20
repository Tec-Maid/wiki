# CustomPreviewWindow (CPW)

<div align="center">

<img  width=60% src="./Images/CPW.png" alt="CPW Image">

</div>

Thank you for choosing the “CustomPreviewWindow” from TecMaid. This documentation contains everything you need to know to get started. If you have any questions, encounter a problem, or need help with integration, please do not hesitate to contact us at service@tecmaid.com.

## Table of Contents

- CustomPreviewWindow (CPW)
    - [Introduction](#introduction)
    - [Settings](#settings)
    - [Installation Instruction](#installation-instructions)
    - [Technical details](#technical-details)
    - [Requirements](#requirements)
    - [How to use](#how-to-use)
    - [Examples (Demo)](#examples-demo)
    - [Useful Links](#useful-links)


## Introduction

Ever miss the simplicity of preview windows from UGUI? Custom Preview Window, or CPW, brings back that practicality while tapping into Unity’s new UI Toolkit power. No fuss, no frills—just an easy preview integration with CPW. 
CPW is a custom control element designed to enhance your Unity UI Toolkit experience by letting you add a preview window into your Editor UIs and plugins developed using Unity UI Toolkit, which doesn’t support a Preview Window natively.
This tool is ideal for visualizing gameobjects, textures, materials, meshes and shaders.


## Settings

You can edit the visual settings of the CustomPreviewWindow using the included “CustomPreviewStyles.uss” file and editing the classes which are defined within.

<div align="center">

![Settings](Images/Settings.png)

</div>

## Installation Instructions

Here's a brief example of how to import "CustomPreviewWindow" into your Project:

1.	Open Unity and Your Project:
    - Open Unity Hub, select your project, and open it in the Unity Editor.

2.	Open the Package Manager:
    - Go to Window => Package Manager.

3.	Search for " CustomPreviewWindow ":
    - In the Package Manager window, make sure you’re the “Packages: XXX” setting is set to “Packages: My Assets”. 
    - Find " CustomPreviewWindow " in the results and click on it.

4.	Download and Import:
    - Click the "Download" button (if it's not already downloaded).
    - After downloading, click "Import".
    - In the "Import Unity Package" window, click "Import" to bring all the CustomPreviewWindow files into your project

5.	Verify Import:
    - Check the Assets folder in the Project window to ensure that the CustomPreviewWindow files are present.
    - You can now start using “CustomPreviewWindow” Demo via the Tools menu: Tools => DemoUXML.
    - By following these steps and the following “How to use” instructions, you can easily install and start using CustomPreviewWindow in your projects.


## Technical details
CPW supports the following major Unity versions:
- 2021.3+
- 2022
- 2023
- Unity 6

## Requirements
Visual Scripting (Unity Package, installed by default from version 2021.1)
Works with UI Toolkit (formerly known as UIElements) only, it's not compatible with Unity UI (UGUI).
Note: that Unity versions lower than 2021.1 are not supported, as those versions do not come with UI Builder built-in.

## How to use

This guide is for developers with knowledge of Unity, UI Toolkit, and C# scripting. 
It mentions the following topics:
- UXML
- USS
- UI Builder
- UI Toolkit
- Custom Controls

*Links to the respective topic documentation, can be found under “Useful Links” section.*


1. Open UI Builder: 

**Method 1:** To do this, go to Window => UI Toolkit => UI Builder. This will open the UI Builder window where you can create and edit UI elements.

<div align="center">

![Usage Methode 1](./Images/Usage_1.png)

</div>


**Method 2:** In the Project window, right-click in the Assets folder or any subfolder where you want to create the UI Document.
Select Create => UI Toolkit => UI Document.
A new UI Document (UXML) will be created. Rename it to something you like.
Double-Click on your created file and the UI-Builder Window should open.

<div align="center">

![Usage Methode 2](./Images/Usage_2.png)

</div>


2. In the UI Builder, go to the "Library" panel, then select the "Project" tab. Navigate to:
“Custom Controls (C#)” => “TecMaid_CustomPreviewWindow” => “CustomPreviewWindow”

<div align="center">

![Style Components](./Images/Usage_3.png)

</div>


3. How to Use in Project: 
CPW can be used like any other UI Builder Standard component. Drop "CustomPreviewWindow" script into your UXML project to add it.

<div align="center">

![Style Components](./Images/Usage_4.png)

</div>

4. To add styles to CPW components:

* Copy the content from the imported " CustomPreviewStyles.uss" into your own 
.USS file to edit the CPW part.

* In the UI Builder, go to the “StyleSheets” panel.

* Click the “+” button and select “Add Existing USS”.

* In the new window that opens, navigate to:
Assets\TecMaid\CustomPreviewWindow\Scripts\Styles\CustomPreviewStyles.uss

* Select “CustomPreviewStyles.uss”.

* This will import the stylesheet, allowing you to customize the CPW components


<div align="center">

![Style Components](./Images/Usage_5.png)

</div>

5. To add CPW to your editor Script:

* Create a new C# script by pressing right click in the Unity explorer then navigating
to “create” => “C# Script” or “Monobehaviour Script”.

* Open your newly created script and change the inherited class from 
"Monobehaviour" to "EditorWindow"

* Add the TecMaid CPW namespace by adding 
“using.TecMaid_CustomPreviewWindow” to your namespaces at the top of the 
script.

* Create a private field of class "CustomPreviewWindow". For example: private 
CustomPreviewWindow cpw;

* Create a function() that initializes cpw, give it the "rootVisualELement" parameter, 
and call it inside the Unity Editor function CreateGUI(). For example


```cs
namespace TecMaid_CustomPreviewWindow
{
    public class DemoWindow : EditorWindow
    {
        [SerializeField] private VisualTreeAsset _tree;// UI Document, UXML
        private ObjectField objField;//Local ObjectField
        private CustomPreviewWindow cpw;

        [MenuItem("Tools/DemoUMXL")]
        public static void ShowEditor()
        {
            var window = GetWindow<DemoWindow>();
            window.titleContent = new GUIContent("DemoUMXL");
        }

        private void CreateGUI()
        {
            _tree.CloneTree(rootVisualElement);
            cpw = new CustomPreviewWindow();
            InitFields();
            ExternalObjectField();
        }

        void InitFields()
        {
            //Initialising Local Components here:
            //Initialising CPW Components
            cpw.InitializeCPWComponents(rootVisualElement);
        }

        void ExternalObjectField()
        {
            //Setting Local ObjectField value to external CPW ObjectField value
            objField.RegisterValueChangedCallback(evt =>
            {
                cpw.SetCPWObjectField(evt.newValue);
            });
        }
    }
}

```


## Examples (Demo)

<div align="center">

![Demo 1](./Images/Examples_1.png)

![Demo 2](./Images/Examples_2.png)

</div>


## Useful Links

- [Unity Docs: UIE-simple-ui-toolkit-workflow](https://docs.unity3d.com/Manual/UIE-simple-ui-toolkit-workflow.html)
- [Unity Docs: UIElements](https://docs.unity3d.com/Manual/UIElements.html)
- [Unity Docs: UIE-UXML](https://docs.unity3d.com/Manual/UIE-UXML.html)
- [Unity Docs: UIE-USS](https://docs.unity3d.com/Manual/UIE-USS.html)
- [Unity Docs: UIBuilder](https://docs.unity3d.com/Manual/UIBuilder.html)
- [Unity Docs: UIE-custom-controls](https://docs.unity3d.com/Manual/UIE-custom-controls.html)
- [Unity Technologies Git Repository](https://github.com/Unity-Technologies/ui-toolkit-manual-code-examples/tree/master)
