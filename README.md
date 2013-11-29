# UI Development Guidelines

## Introduction

The purpose of these guidelines is to create and document appropriate coding standards for front-end/UI code (HTML, CSS and JavaScript) which can be used as a reference for developers both during development and code reviews. This is a living document and will be updated on an on-going basis.

## Separation of concerns

Throughout the application, content (HTML), presentation (CSS) and behaviour (JavaScript) are to be kept separate, which is achieved through the use of external CSS/JS files, proper use of semantic HTML elements, and appropriate naming of classes in CSS (amongst other things). This benefits maintenance, code visibility and maintains a true separation of UI components.

## HTML

### Doctype

The application uses a HTML5 doctype and, where practical, all HTML must be validated against this.

### Use of HTML5 elements

Whilst the application is written in HTML5, [support for legacy browsers is a requirement](#FrontEndDevelopmentGuidelines-Cross-browsertesting) and must be taken into consideration. This is likely to affect the use of HTML elements as opposed to element attributes.

### Formatting HTML

#### Case

All HTML must be written in lowercase.

#### Attributes

All attributes must be enclosed in double quotation marks, **NOT** single. Attributes must be written in alphabetical order according to the attribute name.
<table class="confluenceTable"><tbody><tr><th class="highlight-red confluenceTh" data-highlight-colour="red">

<span style="color: rgb(255,0,0);">Bad</span>
<pre>&lt;a title='View room' href='viewroom/'&gt;View room&lt;/a&gt;</pre></th><th class="highlight-green confluenceTh" data-highlight-colour="green">

<span style="color: rgb(51,153,102);">Good</span>
<pre>&lt;a href=&quot;/viewroom&quot; title=&quot;View room&quot;&gt;View room&lt;/a&gt;</pre></th></tr></tbody></table>

#### HTML5 attributes

In HTML5, not all attributes require a specific value. However, in order to maintain consistency throughout the application and minimize confusion and the possibility of cross-browser breakages, **ALL** attributes must have a specific value assigned.
<table class="confluenceTable"><tbody><tr><th class="highlight-red confluenceTh" data-highlight-colour="red">

<span style="color: rgb(255,0,0);">Bad</span>
<pre>&lt;input id=&quot;name=&quot; required /&gt;</pre></th><th class="highlight-green confluenceTh" data-highlight-colour="green">

<span style="color: rgb(51,153,102);">Good</span>
<pre>&lt;input id=&quot;name=&quot; required=&quot;required&quot; /&gt;</pre></th></tr></tbody></table>

#### Closing tags

All elements must have an opening and closing tag, with the exception of self-closing elements.

### Tables

Tables are to be used for tabular data **ONLY**. Tables are not to be used for layout purposes under any circumstance.

#### Table requirements

A table must contain the following attributes/elements

*   &lt;caption&gt; element
*   _id_ attribute on &lt;th&gt;
*   _scope_ attribute on &lt;th&gt;
*   _headers_ attribute on &lt;td&gt; to associate it with appropriate &lt;th&gt;

A correctly written table should resemble the following
<table class="confluenceTable"><tbody><tr><th class="confluenceTh">
<pre>&lt;table&gt;
    &lt;caption&gt;Football League Championship as of 22nd November 2013&lt;/caption&gt;
    &lt;tr&gt;
        &lt;th id=&quot;position&quot; scope=&quot;col&quot;&gt;Position&lt;/th&gt;
        &lt;th id=&quot;team&quot; scope=&quot;col&quot;&gt;Team&lt;/th&gt;
        &lt;th id=&quot;points&quot; scope=&quot;col&quot;&gt;Points&lt;/th&gt;
    &lt;/tr&gt;
    &lt;tr&gt;
        &lt;td headers=&quot;position&quot;&gt;1&lt;/td&gt;
        &lt;td headers=&quot;team&quot;&gt;Burnley&lt;/td&gt;
        &lt;td headers=&quot;points&quot;&gt;34&lt;/td&gt;
    &lt;/tr&gt;
    &lt;tr&gt;
        &lt;td headers=&quot;position&quot;&gt;2&lt;/td&gt;
        &lt;td headers=&quot;team&quot;&gt;Leicester City&lt;/td&gt;
        &lt;td headers=&quot;points&quot;&gt;32&lt;/td&gt;
    &lt;/tr&gt;
    &lt;tr&gt;
        &lt;td headers=&quot;position&quot;&gt;1&lt;/td&gt;
        &lt;td headers=&quot;team&quot;&gt;Queen's Park Rangers&lt;/td&gt;
        &lt;td headers=&quot;points&quot;&gt;32&lt;/td&gt;
    &lt;/tr&gt;
&lt;/table&gt;</pre>
</th></tr></tbody></table>

If the table is particularly complex (e.g: multiple headers, complicated cell/header relationships), we should also make use of the _summary_ attribute on the &lt;table&gt; element. In the _summary_, we should give a concise description of the table structure and data relationships.

### Forms

#### Fieldsets

Related inputs in a form should be grouped into a &lt;fieldset&gt; with a descriptive &lt;legend&gt; element.

#### Inputs and Labels

All &lt;input&gt; elements must have an associated &lt;label&gt;. The &lt;label&gt; must have a _for_ attribute which matches the _id_ attribute on the &lt;input&gt;

#### Input types

TODO: to imprvoe device usability, use specific inpuit types ([link to list](http://nativeformelements.com/))

#### Placeholders

Where possible, an &lt;input&gt; should have a _placeholder_ attribute in order to give a hint as to what the user should enter. This should be different from the &lt;label&gt;
<table class="confluenceTable"><tbody><tr><th class="confluenceTh"><pre>&lt;label for=&quot;email&quot;&gt;Your e-mail address&lt;/label&gt;
&lt;input id=&quot;email&quot; placeholder=&quot;someone@email.com&quot; type=&quot;email&quot; /&gt;</pre></th></tr></tbody></table>

#### Error messages

In the event of a user submitting invalid data, an error message must be shown on the form. This error message must be visually distinguishable from the surrounding elements and describe in clear language what the error is. Error messages must not be present in the HTML until an invalid input has been submitted.

The error message must be placed alongside the &lt;label&gt; of the invalid &lt;input&gt;. Ideally, this is done by appending it to the &lt;label&gt; so that it can be accessed via screen readers in forms mode.

In the case of a very long form with multiple errors, an error summary should be displayed at the top of the form listing the individual errors. By clicking on these errors, the user is jumped to the relevant &lt;input&gt;, where the associated &lt;label&gt; also displays the error.

#### Tab order

Forms must be written so that there is a logical tab order. This negates the need to use the _tabindex_ attribute on &lt;input&gt; elements which can cause accessibility issues.

#### Form example
<table class="confluenceTable"><tbody><tr><th class="confluenceTh">
<pre>&lt;form id=&quot;some-form&quot; action=&quot;&quot; method=&quot;&quot;&gt;
    &lt;p&gt;There were some errors when submitting your data. Please see the list below.&lt;/p&gt;
    &lt;ul&gt;
        &lt;li&gt;&lt;a href=&quot;#name&quot;&gt;Please enter your name&lt;/a&gt;&lt;/li&gt;
        &lt;li&gt;&lt;a href=&quot;#address1&quot;&gt;Please enter the first line of your address&lt;/a&gt;&lt;/li&gt;
    &lt;/ul&gt;
    &lt;fieldset&gt;
        &lt;legend&gt;Your details&lt;/legend&gt;
        &lt;label for=&quot;name&quot;&gt;Name &lt;span class=&quot;error&quot;&gt;Error - please enter your name&lt;/span&gt;&lt;/label&gt;
        &lt;input id=&quot;name&quot; placeholder=&quot;Joe Bloggs&quot; type=&quot;text&quot; /&gt;
        &lt;label for=&quot;email&quot;&gt;e-mail address&lt;/label&gt;
        &lt;input id=&quot;email&quot; placeholder=&quot;someone@email.com&quot; type=&quot;email&quot; /&gt;
        &lt;fieldset&gt;
            &lt;legend&gt;Gender&lt;/legend&gt;
            &lt;label for=&quot;male&quot;&gt;Male&lt;/label&gt;
            &lt;input id=&quot;male&quot; type=&quot;radio&quot; value=&quot;Male&quot; /&gt;
            &lt;label for=&quot;female&quot;&gt;Female&lt;/label&gt;
            &lt;input id=&quot;female&quot; type=&quot;radio&quot; value=&quot;Female&quot; /&gt;
        &lt;/fieldset&gt;
    &lt;/fieldset&gt;
    &lt;fieldset&gt;
        &lt;legend&gt;Your address&lt;/legend&gt;
        &lt;label for=&quot;address1&quot;&gt;Address line 1 &lt;span class=&quot;error&quot;&gt;Error - please enter the first line of your address&lt;/span&gt;&lt;/label&gt;
        &lt;input id=&quot;address1&quot; placeholder=&quot;1 Some Street&quot; type=&quot;text&quot; /&gt;
        &lt;label for=&quot;address2&quot;&gt;Address line 2&lt;/label&gt;
        &lt;input id=&quot;address2&quot; placeholder=&quot;Some city&quot; type=&quot;text&quot; /&gt;
        &lt;label for=&quot;address3&quot;&gt;Address line 3&lt;/label&gt;
        &lt;input id=&quot;address3&quot; placeholder=&quot;Some country&quot; type=&quot;text&quot; /&gt;
    &lt;/fieldset&gt;
&lt;/form&gt;</pre>
</th></tr></tbody></table>

## CSS

### Placement of CSS

All CSS files are to be linked to in the &lt;head&gt; of the document using the following format
<table class="confluenceTable"><tbody><tr><th class="confluenceTh"><pre>&lt;link href=&quot;/path/to/css/file.css&quot; media=&quot;all&quot; rel=&quot;stylesheet&quot; type=&quot;text/css&quot; /&gt;</pre></th></tr></tbody></table>

**<span style="color: rgb(255,0,0);">Inline CSS is NOT to used under any circumstances.</span>**
<table class="confluenceTable"><tbody><tr><th class="highlight-red confluenceTh" data-highlight-colour="red">

<span style="color: rgb(255,0,0);">Bad</span>
<pre>&lt;img style=&quot;display:block; /&gt;</pre></th></tr></tbody></table>

Embedded &lt;style&gt; blocks are strongly discouraged and every effort must be made to avoid their use.

By ensuring we only use linked CSS files, we have greater control over specificity and better visibility over which styles are being applied across the application.

### Use of IDs and classes

<span style="color: rgb(255,0,0);">**IDs are NOT to be used in CSS**</span> as it creates problems with specificity. An ID is 256 times more specific than a class, meaning that if an element has an ID with a property assigned to it, it would take 256 chained classes on the element to overwrite that property[[1]](/wiki/download/attachments/1638411/css-specificity.html?version=1&amp;modificationDate=1385036853871&amp;api=v2). With large CSS files/architecture this can lead to unnecessarily long selectors or (even worse) use of !important to overwrite declarations.

### Sass

#### Structure

A new Sass file should be created for each part of the application and saved into the ‘partials’ directory (for example, /css/sass/partials/_global-header.scss).

 At the top of each file, a comment should be included giving an overview of the CSS below. This is to assist scanning of the generated CSS. The comment should be laid out as follows.
<table class="confluenceTable"><tbody><tr><th class="highlight-grey confluenceTh" data-highlight-colour="grey"><pre>/*
 Main navigation bar
 -------------------------*/</pre></th></tr></tbody></table>

Each file is then to be loaded into a master sass.scss file which lives at the same level as the ‘partials’ directory.

 The generated CSS file is kept in the ‘css’ directory.

#### Mixins

Mixins are to be stored in a separate _mixins.scss file within the ‘partials’ directory. When naming mixins, the name should use camel-case, starting with a lowercase (e.g: @mixin boxShadow)

#### Variables

Variables are to be declared at the top of the CSS section to which they apply, for example
<table class="confluenceTable"><tbody><tr><th class="confluenceTh">
<pre>
/*
 Feedback messages
 -------------------------*/
 $errorPrimary: #ef0000;
 $warningPrimary: #ffd800;
 $successPrimary: #28d300;

 .error-msg {
     color:$errorPrimary;
 }
 .warning-msg {
     color:$warningPrimary;
 }
 .success-msg {
     color:$successPrimary;
 }</pre>
 </th></tr></tbody></table>

#### Nesting

Declarations should be nested no more than 3 levels deep to avoid overly-complicated depth and long selectors in the generated CSS.

### Naming selectors

Selectors should be named according to their purpose/function **NOT** their appearance.
<table class="confluenceTable"><tbody><tr><th class="highlight-red confluenceTh" data-highlight-colour="red">

<span style="color: rgb(255,0,0);">Bad</span>
<pre>.content-left</pre><pre>.red</pre></th><th class="highlight-green confluenceTh" data-highlight-colour="green">

<span style="color: rgb(51,153,102);">Good</span>
<pre>.content-secondary</pre><pre>.alert</pre></th></tr></tbody></table>

Selectors should **NOT** include a specific HTML element, again to avoid potential specificity conflicts and improve maintainability
<table class="confluenceTable"><tbody><tr><th class="highlight-red confluenceTh" data-highlight-colour="red">

<span style="color: rgb(255,0,0);">Bad</span>
<pre>ul.main-nav</pre></th><th class="highlight-green confluenceTh" data-highlight-colour="green">

<span style="color: rgb(51,153,102);">Good</span>
<pre>.main-nav</pre></th></tr></tbody></table>

Selectors should be named in lowercase and use hyphens to separate words
<table class="confluenceTable"><tbody><tr><th class="highlight-red confluenceTh" data-highlight-colour="red">

<span style="color: rgb(255,0,0);">Bad</span>
<pre>.mainNav</pre><pre>.main_nav</pre><pre>.mainnav</pre></th><th class="highlight-green confluenceTh" data-highlight-colour="green">

<span style="color: rgb(51,153,102);">Good</span>
<pre>.main-nav</pre></th></tr></tbody></table>

### Formatting

Selectors are to be written on one line with trailing opening brace.
<table class="confluenceTable"><tbody><tr><th class="highlight-red confluenceTh" data-highlight-colour="red">

<span style="color: rgb(255,0,0);">Bad</span>
<pre>.main-nav li</pre><pre>{</pre></th><th class="highlight-green confluenceTh" data-highlight-colour="green">

<span style="color: rgb(51,153,102);">Good</span>
<pre>.main-nav li {</pre></th></tr></tbody></table>

Multiple selectors are to be written on separate lines with an opening brace after the final selector.
<table class="confluenceTable"><tbody><tr><th class="highlight-red confluenceTh" data-highlight-colour="red">

<span style="color: rgb(255,0,0);">Bad</span>
<pre>.main-nav li, .main-nav a</pre><pre>{</pre></th><th class="highlight-green confluenceTh" data-highlight-colour="green">

<span style="color: rgb(51,153,102);">Good</span>
<pre>.main-nav li,
.main-nav a {</pre></th></tr></tbody></table>

Property declarations are to be written on separate lines with an indentation of 4 spaces. Properties are to be listed in alphabetical order according to their property name. Each declaration should have no space between the property and value, and also include a semi-colon after every value (including the final one). The closing brace should be placed on a new line after the final declaration, with no indentation.
<table class="confluenceTable"><tbody><tr><th class="highlight-red confluenceTh" data-highlight-colour="red">

<span style="color: rgb(255,0,0);">Bad</span>
<pre>.main-nav {width: 100%; height: 50px; border: 10px solid #cc0000; padding: 20px }</pre></th><th class="highlight-green confluenceTh" data-highlight-colour="green">

<span style="color: rgb(51,153,102);">Good</span>
<pre>.main-nav {
     <a>border:10px</a> solid #cc0000;
     <a>height:50px</a>;
     <a>padding:20px</a>;
     <a>width:100%</a>;
 }</pre></th></tr></tbody></table>

If Sass mixins are to be applied, these should be included before any other property declarations.
<table class="confluenceTable"><tbody><tr><th class="highlight-red confluenceTh" data-highlight-colour="red">

<span style="color: rgb(255,0,0);">Bad</span>
<pre>.ui-dialog {
     background:#fff;
     <a>padding:20px</a>;
     @include boxShadow(10px);
 }</pre></th><th class="highlight-green confluenceTh" data-highlight-colour="green">

<span style="color: rgb(51,153,102);">Good</span>
<pre>.ui-dialog {
     @include boxShadow(10px);
     background:#fff;
     <a>padding:20px</a>; 
 }</pre></th></tr></tbody></table>

## JavaScript

TODO: single quotes for strings, reduce DOM trips, only 1 'var' for multiple vars, declaring objects, declaring arrays, JS files at bottom, only call JS when needed

The application makes use of [jQuery](http://jquery.com/) and [Kendo UI](http://www.kendoui.com/), as well as plain JavaScript.

### Strings

Strings should be enclosed in single quotation marks, **NOT** double. By doing so, we are able to include HTML in a string whilst [observing the guideline for HTML attributes](#FrontEndDevelopmentGuidelines-Attributes) and negating the need to escape HTML attributes within the string.
<table class="confluenceTable"><tbody><tr><th class="highlight-red confluenceTh" data-highlight-colour="red">

<span style="color: rgb(255,0,0);">Bad</span>
<pre>var name = &quot;Joe Bloggs&quot;;
var nameDisplay = &quot;&lt;p class='name'&gt;&quot; + name + &quot;&lt;/p&gt;&quot;;
var nameDisplay = &quot;&lt;p class=\&quot;name\&quot;&gt; + name + &quot;&lt;/p&gt;&quot;;</pre></th><th class="highlight-green confluenceTh" data-highlight-colour="green">

<span style="color: rgb(51,153,102);">Good</span>
<pre>var name = 'Joe Bloggs';
var nameDisplay = '&lt;p class=&quot;name&quot;&gt; + name + '&lt;/p&gt;';</pre></th></tr></tbody></table>

Strings longer than 80 characters should be broken up and built using concatenation
<table class="confluenceTable"><tbody><tr><th class="highlight-red confluenceTh" data-highlight-colour="red">

<span style="color: rgb(255,0,0);">Bad</span>
<pre>var message = 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris ultrices elementum lorem, id porta elit porta id. Integer mollis fringilla erat, eget vestibulum nisi aliquet sit amet. Cras sed vulputate nulla. Cras ac risus vel arcu imperdiet malesuada ut at mi. Sed nec tincidunt quam, non accumsan nisi.';</pre></th></tr><tr><td class="highlight-green confluenceTd" data-highlight-colour="green">

<span style="color: rgb(51,153,102);">**Good**</span>
<pre>var message = 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.' +
    Mauris ultrices elementum lorem, id porta elit porta id.' +
    Integer mollis fringilla erat, eget vestibulum nisi aliquet sit amet.' +
    Cras sed vulputate nulla. Cras ac risus vel arcu imperdiet malesuada ut at mi.' +
    Sed nec tincidunt quam, non accumsan nisi.';</pre></td></tr></tbody></table>

### Declaring Objects

Objects should be declared using the literal syntax
<table class="confluenceTable"><tbody><tr><th class="highlight-red confluenceTh" data-highlight-colour="red">

<span style="color: rgb(255,0,0);">Bad</span>
<pre>var user = new Object();</pre></th><th class="highlight-green confluenceTh" data-highlight-colour="green">

<span style="color: rgb(51,153,102);">Good</span>
<pre>var user = {};</pre></th></tr></tbody></table>

### Declaring arrays

Arrays should be declared using the literal syntax
<table class="confluenceTable"><tbody><tr><th class="highlight-red confluenceTh" data-highlight-colour="red">

<span style="color: rgb(255,0,0);">Bad</span>
<pre>var items = new Array();</pre></th><th class="highlight-green confluenceTh" data-highlight-colour="green">

<span style="color: rgb(51,153,102);">Good</span>
<pre>var items = [];</pre></th></tr></tbody></table>

## Accessibility

TODO: Skip links (note known webkit bug), keyboard navigation, media fall-back (alt, noscript etc), same link phrases -&gt; same URL, link always goes to same place, colour contrast

### Skip links

At the top of the HTML document, there must be anchor links which enable to user to skip to the main navigation and main content area. These links should be hidden initially and made visible when they receive focus.

_Note: There is a [known bug](https://code.google.com/p/chromium/issues/detail?id=262171)__ with Webkit browsers whereby activating anchor links will visually move the page but the target will not receive focus._

### Keyboard navigation

The application must be navigable via the keyboard. As a basic rule-of-thumb; if a user can click on an element, they must also be able to tab to it and activate it by pressing Return.

All elements which have a _:hover_ pseudo-class must also have a _:focus_ pseudo-class.

#### Access keys

The _accesskey_ attribute is **NOT** to be used as it can cause conflicts with the default keyboard accessibility of screen readers.

### Media fall-backs

All media elements (images, audio, video etc) must have a suitable fall-back in the event that the media is not available or the user has disabled a feature in their browser.

#### Image _alt_ attributes

All &lt;img/&gt; elements must have an _alt_ attribute which contains a concise description of the image and/or it's purpose. If the &lt;img/&gt; is used purely for decorative purposes, the _alt_ attribute must still be included, but should have an empty value.

## Cross-browser testing

In a desktop environment, the application must work on the following browsers, across both Windows and Mac

*   Internet Explorer 7
*   Internet Explorer 8
*   Internet Explorer 9
*   Internet Explorer 10
*   Mozilla Firefox
*   Google Chrome
*   Safari (Mac only)

The application must be developed in a responsive way so that it is usable on a wide range of devices, including (but not limited to) iOS, Android and Windows devices.

## Useful resources

*   [HTML validator](http://validator.w3.org/)

*   [Can I Use?](http://caniuse.com/)