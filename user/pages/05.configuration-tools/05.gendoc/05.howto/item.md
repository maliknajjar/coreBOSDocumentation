---
title: 'Documentation Generation::How to Use'
metadata:
    description: 'How to use GenDoc'
    author: 'Joe Bordes'
content:
    items:
        - '@self.children'
    limit: 5
    order:
        by: date
        dir: desc
    pagination: true
    url_taxonomy_filters: true
taxonomy:
    category:
        - integration
    tag:
        - gendoc
---

How to use and configure coreBOS Documentation Generator.

===

## Install

The GenDoc extension consists of two installables; one is the GenDoc extension itself and the other is a utility extension that will help you list and obtain the available labels in your system.

Both are installed as any other module using the Module Manager.

## Activate

Once installed you will find both extensions accessible from the Tools menu but the normal usage will be through the detail view widget that will appear on all those modules that you activate the extension for. Click on the Settings icon for the document generator and enter the Activate Modules section to activate the extension on those modules you want.

This will create the necessary business actions for that module to work with GenDoc. The DetailViewWidget business action supports some additional features:

* `message` parameter. You can manually edit the Business Action and add this parameter to indicate if you want the user to see a message when he does not have access to any templates or not. `module=evvtgendoc&action=evvtgendocAjax&file=DetailViewWidget&formodule=$MODULE$&forrecord=$RECORD$&message=0`
* GenDoc_Confirm_ActionFor global variable: A comma-separated list of document IDs to check before proceeding with the action. A confirmation popup will be shown for these Document template IDs
* GenDoc_Confirm_Actions global variable: A comma-separated list of GenDoc actions that require user confirmation before execution
* GenDoc_Template_Access global variable: A comma-separated list of document IDs the user can access. If empty user can access all templates.

## Upload Templates

Templates are uploaded as documents in the Documents module. The only difference is that you must mark the "Template" checkbox and you must select the main module the template was created for in the "Module" picklist.

I recommend creating a folder to hold all your templates or various folders with names that make it easy to group the templates and distinguish them from other documents.

## Merge

The merge process can be done in various ways. The most common way will be to go to the entity we want to merge, select the template that appears in the action panel and click on one of the available options:

- **Export Document:** will merge the template starting from the record on screen and will send the result to the user
- **EMail Document:** will merge the template starting from the record on screen and will open the email send screen with the result attached and ready to send
- **Save Document:** will merge the template starting from the record on screen and will save it as a Document in the application. The application will save the document inside the first folder found but you can define where you want them to be saved using the **GenDoc_Save_Document_Folder** global variable

You can also execute a Mass Merge from the List view, where you will be able to select various records and a template and have the template merged for each selected record. You will be able to define if you want the output in individual PDFs or as one PDF.

Finally, the most flexible way to merge a template is by accessing the GenDoc extension directly. In this case, we will be presented with two capture fields where we will be able to select any template and any record of any entity and have the template merged with that record. We will also be able to specify the language we want the merge to use and if we want some verbose debug output which is rather useful while creating a new template.

Note that each template is created in one language and that is the language the process must use. By default, the process is run using the language of the user launching the process.

You can translate the directives to your language using the commands_en.php file inside the evvtgendoc folder.

## PDF Output

In order to obtain a PDF from the generated OpenOffice file, we must have a special OpenOffice converter service installed and configured.

This service is a libreoffice headless and unconv listener which is capable of converting the .ODT generated by coreBOS into a PDF file. In fact, this service can convert any .ODT into any other format. This service is not directly related to coreBOS in any way, it is a standard functionality of LibreOffice that can be used for many other use cases, we just use it as an easy way to solve the problem.

You can accomplish this in various ways

1.- install libreoffice headless and unconv in the same server you have coreBOS, then add the PDF Links which can be done in

```
Settings > Module Manager > Document Generator > Server Settings
```
With that, you should be able to generate PDFs. The hard part of this solution is to install all the necessary software in the server and make sure it can be called by your web server user. There are some interesting conversations about this in the forum and in github issues. If you want us to install this for you don't hesitate to contact us, it is a nice way of supporting the project. The instructions are basically:

```
apt update
apt-get install libreoffice-core unoconv
unoconv --listener &
```

and make sure that listener is on always

2.- use our (TSolucio) service. TSolucio has one prepared which you can use by either having a support contract with us or by purchasing our [coreBOS Subscription service](https://blog.corebos.org/blog/corebossubscription). This is also a very clean way of getting PDFs and supporting the project. Besides getting the service you get access to a lot of our developments. Once you have purchased the service we will send you the URL and access information which you will have to set in

```
Settings > Module Manager > Document Generator > Server Settings
```

Contact us for more details.

3.- use [this docker container](https://github.com/sfoxdev/docker-unoconv), then define the **GenDoc_Convert_URL** global variable (something like [http://server_ip:3000](http://server_ip:3000/)) and set the **PDF Links** which can be done in
```
Settings > Module Manager > Document Generator > Server Settings
```
To launch the docker image you can follow the instructions on their site, but I use:
```
docker run -d -p 8099:3000 --env-file=docker.env --name unoconv sfoxdev/unoconv
```
which leaves the service listening on port 8099. The docker.env file is an empty file (probably not even needed)

Obviously, you can also open the OpenOffice document and click on the "PDF" button to convert the ODT to PDF.

Let's add some indications about each type.


<br>
------------------------------------------------------------------------

[Next](../04.gramatica)| Chapter 2: Documentation Generation::Fields and Templates Grammar

------------------------------------------------------------------------