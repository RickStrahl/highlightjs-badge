#  HighlightJs Copy Code Badge-JS (extension) Component
This small JavaScript library complements the [highlightJs Syntax Highligher](https://highlightjs.org/) by providing a badge in the top right corner of highlightJs code snippets.

* Shows active Syntax for the code block
* Allows copying the code block to Clipboard

You can install it [from NPM](https://www.npmjs.com/package/highlightjs-badgejs):

```ps
npm install highlightjs-badge
```

### Usage
To use this library is very simple - you add a script file and call `highlightJsBadge()` after highlightJS has been applied.

The following is a typical configuration for both highlightJs and highlightJs-Badge:

```html
<!-- load highlightjs first -->
<link href="scripts/highlightjs/styles/vs2015.css" rel="stylesheet" />
<script src="scripts/highlightjs/highlight.pack.js"></script>

<!-- then add this badge component -->
<script src="scripts/highlightjs-badgejs.min.js"></script>

<script>
    // apply HighlightJS
    var pres = document.querySelectorAll("pre>code");
    for (var i = 0; i < pres.length; i++) {
       hljs.highlightBlock(pres[i]);
    }
    
    // add HighlightJS-badge (options are optional)
    var options = {   // optional
       contentSelector: "#ArticleBody",
       
       // CSS class(es) used to render the copy icon.
       copyIconClass: "fas fa-copy",
       // CSS class(es) used to render the done icon.
       checkIconClass: "fas fa-check text-success"
    };
    window.highlightJsBadge(options);
</script>
```

#### Options 

Some other options added from the original: 

* <b>title</b> : allow to set a different title on hover 
* <b>label</b> : allow to set a prefix on badge name
* <b>clickableBadge</b> : if set "true" allow to have pointer and click event on badge in addition to icon click
* <b>hasLineNumber</b> : if set "true" indicates that content as line number plugin activated 


### Styling
The default script includes default styling that should work great with dark themed syntax, and fairly well with light themed syntax.

You can customize the styling and the layout of badge by either overriding existing styles or by:

* Overriding styles
* Copying complete styles and template into page

#### Overriding styles
The easiest way to modify behavior is to override individual styles. The stock script includes a hardcoded style sheet and you can override the existing values with hard CSS overrides.

For example to override the background and icon sizing you can:

```css
<style>
    .code-badge {
        padding: 8px !important;
        background: pink !important;
    }
    .code-badge-copy-icon {
        font-size: 1.3em !important;
    }
</style>
```

#### Replace the Template and Styling Completely
Alternately you can completely replace the template and styling. If you look at the source file at the end of the file is a commented section that contains the complete template and you can copy and paste that template into your HTML page - at the bottom near the `</body>` tag.

```html
<style>
    "@media print {
        .code-badge { display: none; }
    }
    .code-badge-pre {
        position: relative; 
    }
    .code-badge {
        display: flex;
        flex-direction: row;
        white-space: normal;
        background: transparent;
        background: #333;
        color: white;
        font-size: 0.8em;
        opacity: 0.5;
        border-radius: 0 0 0 7px;
        padding: 5px 8px 5px 8px;
        position: absolute;
        right: 0;
        top: 0;
    }
    .code-badge.active {
        opacity: 0.8;
    }
    .code-badge:hover {
        opacity: .95;
    }
    .code-badge a,
    .code-badge a:hover {
        text-decoration: none;
    }

    .code-badge-language {
        margin-right: 10px;
        font-weight: 600;
        color: goldenrod;
    }
    .code-badge-copy-icon {
        font-size: 1.2em;
        cursor: pointer;
        padding: 0 7px;
        margin-top:2;
    }
    .fa.text-success:{ color: limegreen !important}    
</style>
<div id="CodeBadgeTemplate" style="display:none">
    <div class="code-badge">
        <div class="code-badge-language">{{language}}</div>
        <div title="Copy to clipboard">
            <i class="{{copyIconClass}} code-badge-copy-icon"></i>
        </div>
     </div>
</div>
```

This is the same template that the library internally holds and injects into the page, but if `#CodeBadgeTemplate` exists in the document then that is used instead of the embedded template. When using your own template no styling is applied. so you neeed to include both the CSS and the `CodeBadgeTemplate`.

You can optionally separate out the CSS into a separate file and only include the `#CodeBadgeTemplate` `<div>` element - that's sufficient for your custom template and styling to kick in.

### Requirements
This library is a self-contained JavaScript file so there are no direct external dependencies. However, there are a couple of requirements:

#### Some ES6 Usage
The library uses a couple of ES6 functions:

* [Object.assign](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign#Polyfill)
* [String.trim](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/Trim#Polyfill)

and you can add the polyfills linked above for old browser (Internet Explorer) support.

#### FontAwesome by Default, Custom Icon Overrides
The library by default also uses [FontAwesome icons](https://fontawesome.com/icons?from=io) for the copy and check icons. The icon styles used work with Font Awesome 4 and 5 (both free and pro). 

The default rendering uses:

```html
<i class="fa fa-copy"></i>
```
The icon is changed to `fa-check` check after content's been copied for 2 seconds.

If you want to use different icons you can use separate styling for the icon classes. For example to change the icons used you affect the `class` attribute on the icon setting. 

For example to use Material Icons:

```javascript
var options = {
        // CSS class(es) used to render the copy icon.
        copyIconClass: "material-icons",  
        copyIconContent: "copy_files",
        
        // CSS class(es) used to render the done icon.
        checkIconClass: "material-icons",
        checkIconContent: "check"
};
window.highlightJsBadge(options);
```

### License 
Licensed under the MIT License. There's no charge to use, integrate or modify the code for this project. You are free to use it in personal, commercial, government and any other type of application.


### Version History

### v0.0.2

### v0.0.1

* **Added new options**  
* <b>title</b> : allow to set a different title on hover 
* <b>label</b> : allow to set a prefix on badge name
* <b>clickableBadge</b> : if set "true" allow to have pointer and click event on badge in addition to icon click
* <b>hasLineNumber</b> : if set "true" indicates that content as line number plugin activated 

* **Fixed bugs**  
* Options not correctly initialized

