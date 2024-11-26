# NOSTERIIHI PowerShell automation

## ✍🏽 Outline

<!-- This is a placeholder for PowerShell content on this site -->

<!-- Consider consluting the MS PowerShell style guide:                                                                                        -->
<!-- https://learn.microsoft.com/en-us/powershell/scripting/community/contributing/powershell-style-guide?view=powershell-7.4  etc. -->

### 📋 Tasks

Present details on PowerShell Markdown functionality, including sections on:

+ [ ] Demonstrate how code and text fragments can be assembled to a full HTML document
+ [ ] Find out how to define Web page style with Cascaded Style Sheets (CSS) and PowerShell 
+ [ ] Find a Cascaded Style Sheet (CSS) which emulates the default GitHub style
+ [ ] Extend Markdown with PowerShell table functionality
+ [ ] Convert Markdown to PDF
+ [ ] Fine-tune how markdown is rendered on a VT100 console

---

## Display Markdown in your default browser

Starting with version 7.2, PowerShell includes useful functionality which facilitates integration between Mardown, PowerShell and VisualStudio Code. If you have a sample document called page.md in the current location of your local terminal, you should be able to view your Markdown file in a WWW browser. Let's use the example above of an unordered list:

    # Sample Markdown page to be stored in page.md
    
    * Demonstrate how code and text fragments can be assembled to a full HTML document
    * Find out how to define Web page style with Cascaded Style Sheets (CSS) and PowerShell 
    * Extend Markdown with PowerShell table functionality
    * Convert Markdown to PDF
    * Fine-tune how markdown is rendered on a VT100 console

Use the copy functionality of the code window above (upper right hand corner) and store the content in a file called page.md in your PowerShell terminal. Then execute a single command, `Show-Markdown` with the `-UseBrowser` argument:

    # Render Markdown content to be displayed with the default browser:
    Show-Markdown -Path .\page.md -UseBrowser

---

## Convert from Markdown to HTML fragment

Most useful is the PowerShell conversion command `ConvertFrom-Markdown` which translates a Markdown page into HTML usable at your WWW site. 

Here you are:

    # Translate Markdown to HTML which is directly usable as a WWW page in a HTTP service
    ConvertFrom-Markdown -Path ./page.md | Select-Object -ExpandProperty Html | Set-Content -Path ./page.htm

The file actually contains only a HTML fragment, without even the `<html>` and `<body>` containers (not to speak of even a document type declaration, `<head>`, `<title>` etc.):

    <h1 id="sample-markdown-page-to-be-stored-in-page.md">Sample Markdown page to be stored in page.md</h1>
    <ul>
    <li>Demonstrate how code and text fragments can be assembled to a full HTML document</li>
    <li>Find out how to define Web page style with Cascaded Style Sheets (CSS) and PowerShell</li>
    <li>Extend Markdown with PowerShell table functionality</li>
    <li>Convert Markdown to PDF</li>
    <li>Fine-tune how markdown is rendered on a VT100 console</li>
    </ul>

---

## Convert from Markdown to a VT100 encoded string

This variation is useful in a configuration equipped with a VT100 console. This is the case if development work is e.g. carried out on the Visual Studio Code IDE.

    # Render Markdown content in Visual Studio Code (or any VT100 compatible console):
    Show-Markdown -Path .\page.md
   
The conversion can be fine-tuned with a related PowerShell command `Set-MarkdownOption` which sets the color and style used for rendering Markdown text:

    Set-MarkdownOption

The command also supports two themes. Try out the two predefined color sets, which are called  `Dark` and `Light`. Like this:

    Set-MarkdownOption -Theme Dark
  
The PowerShell documentation states the obvious fact, that "If the terminal doesn't support ANSI color escape sequences (VT100), then colors are not displayed."

<!-- Check out https://github.com/read-0nly/PSRepo/tree/master/colorDemo -->
