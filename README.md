# Using Jekyll to process SCSS files

## Overview

This is my first time working with **Sass** so any input and comment is highly appreciated!
<br><br>
**The scope:** One of my clients asked me to implement a structure that allows editors to easily change basic settings on the site, like colors, fonts, logos, etc without having to fiddle with code. The projects are hosted on **CloudCannon**, a CMS for Jekyll which is quite awesome. The objective was to _allow editors using CloudCannon to use the CMS's UI for intuitive changes_ of these settings.

## Process

Please note that this process breakdown **assumes that you are famiiar with Sass**; if you are not, I highly recommend that you take a small tutorial on how it works. FreeCodeCamp has this great tutorial that covers some of the basic functions: https://www.youtube.com/watch?v=_a5j7KoflTs (don't be scared by the 2hr-lenght: focus on the first half hour for a good insight on how Sass works).

### File & Folder Set-up

- First, install a Sass/SCSS processor on your code editor (Atom, etc.). This will ensure that the SCSS file is processed into CSS when you save it.
- Set up your folder structure as usual; add some markup to your <code>index.html</code> file for reference.
- Create a <code>style.scss</code> file and place it on your <code>styles</code> folder: this is your **main** SCSS file which Jekyll will render
- Create a <code>_sass</code> folder and include all your **Sass** partials, mixins and all here (the Sass `'@import'` partials)
- Next, create a <code>_data</code> **_folder_** and create a <code>settings.yml</code> **_file_** inside of it: this is where you will put all the variable values for Jekyll to output from Liquid tags

### File Contents

#### <code>settings.yml</code>
Set up the structure & values of your variables here. Colors, font embed codes, images, etc... This will allow CloudCannon to display these keys in a user-friendly interface on their Explore view. They have a nice database of keys which are displayed with their own UI, which you can check here: https://docs.cloudcannon.com/editing/interfaces/inputs/

#### <code>style.scss</code>
This file needs to have empty Front Matter for Jekyll to process it; **do so by adding 2 lines of 3 dashes (<code>---</code>) at the top of the file**. Write your SCSS normally, and where you'd normally place the value for the Sass variables, place a Liquid tag to pass the values from the <code>settings.yml</code> file. Following this project's example, instead of <code>$primary_color: '#eee';</code>, you should set <code>$primary_color:{{site.data.settings.colors.primary_color}};</code>, to which Jekyll will output <code>$primary_color: '#eee';</code> on the <code>_site/styles/style.css</code> folder.

#### <code>_config.yml</code>
In case you are using partials, you must add the following code to your <code>_config.yml</code> file:<br>
```
sass:
    sass_dir: _sass
```

#### Sass partials
I have run into errors when trying to populate partials with YAML values, so the work around is to have all the Sass variables on your main `SCSS` file. If you know how to work around this, get in touch!
