# Overview
This tutorial will help you get your theme available for installation in Standard Notes. It'll be best if you have some experience with html/css, but It's possible to do by swapping out values of an existing theme css. I'll do my best to simplify the process.

**There will be, atleast, 3 files needed for making a theme.**
1. Extension Install Json  (I will refer to this as "extension.json", can be named whatever)
2. Theme CSS  (I will refer to this as "main.css")
3. "package.json" file
	 
### How-To Sections:
1.   Make Github Repo
2.   Make Theme (css)
3.   Extension Installation Json
4.   Local Hosting Theme for Development
5.   Publishing Theme

___
## 1. Make Github Repo
It'll be significantly easier to achieve if you use Github to host your theme/extension. and free... Just all around convenient.. **do it!**
 

**For your theme, the following items need to be apart of the Github Repo:**
1. Theme CSS  ("main.css")
	- example here: https://docs.standardnotes.com/extensions/themes/
	- Either use their example css or grab it from another theme.
2. "package.json"
	 - not much to it.. below is a bare bones example
	 
```
{
		"name": "[your theme name (I used my repo name)]",
		"version": "1.0",
		"sn": {
			"main": "[path to your css file.. if no folders then just main.css]"
		},
		"repository": {
			"type": "git",
			"url": "git://github.com/[username]/[repo name].git"
		}
}
```

3. *(Optionally) you can place your extension install json here too. However, I will choose to  use listed.to to host that file.*

___
# 2. Make Theme
- My top tip is to enable 'Developer Tools'.. `(view) > (Toggle Developer Tools)`

- find the styles tab and scroll down to :root{... where you can test out updating some various colors etc.

- most of the effort for getting your themeing will be to override those root color variables
- If you want to get more fancy you can try adding other styling

- ***In a later section, I describe how to locally host your theme for development***


---

# 3. Extension Installation Json
This is the file that you link to when you want to install your theme. It provides an overview of information like where the css file is hosted, the theme name, version, etc.

More good information can be found here: 
-https://docs.standardnotes.com/extensions/publishing/

### 3.1 Example

The `"statusBar" : "dark-content"`    -> can be removed if its not a dark theme.. this line is helpful for dark themes on mobile specifically

```
{
  "identifier": "tech.gunderson.sn-theme-monochrome-dark",
  "name": "Monochrome Dark",
  "content_type": "SN|Theme",
  "area": "themes",
  "version": "1.2",
  "description": "A near-monochrome dark theme for Standard Notes.",
  "url": "https://cdn.jsdelivr.net/gh/Parkertg/sn-theme-monochrome-dark@v1.2/main.css",
  "download_url": "https://github.com/Parkertg/sn-theme-monochrome-dark/archive/refs/tags/v1.2.zip",
  "marketing_url": "https://github.com/Parkertg/sn-theme-monochrome-dark",
  "thumbnail_url": "https://raw.githubusercontent.com/Parkertg/sn-theme-monochrome-dark/main/preview.png"
	"latest_url": "https://listed.to/p/eY9kuTLQzB",
  "dock_icon": {
    "type": "circle",
    "background_color": "#adadad",
    "foreground_color": "#ffffff",
    "border_color": "#ffffff"
  },
  "statusBar" : "dark-content"
}
```

### 3.2 Important !
Notice what I did with the url link.
`"url": "https://cdn.jsdelivr.net/gh/Parkertg/sn-theme-monochrome-dark@v1.2/main.css",`

**I used "https://cdn.jsdelivr.net/gh/" rather than "https://raw.githubusercontent.com/"**.  This is needed currently to make your theme work in browsers. the 'raw' github files aren't served with the proper MIME type, and is blocked by the browser (at least that's how I understand it).  Thus, we need to use something like jsDelivr which will serve it in a way that makes the browsers happy.  So far, it seems that only the url for the main.css needs this.

Also, You'll  need to **release your code on github with a Tag** for jsdelivr to work.  On Github make a new tag (example.. "v1.0.0") and use that in each link.

---

### 3.3 Using Listed.to for Extension.json hosting
It's works pretty well to use Standard Notes to host this file via listed.to. 

**Steps:**
1. Just make a note, 
2. paste your extension install json, 
3. At the top of the note, add  the metatype so that listed.to hosts the file properly

	```
	---
	  metatype: json
	---
	```

4. Publish the note to a private link.
5. **"Open Private link"**, copy that url
6. Update the "latest_url" to that copied url.  
7. Update your private post with your update

**Now, your install link is live and ready to go!!**

*Note: whenever you update your extension.json, make sure you also* **"Update Private Post"** *so the changes go live!*

---
# 4. Local Hosting Theme for Development (Optional)

if you want to host it on your local PC *(tested on windows desktop app only)*, you can try to following steps:
- *have 'git for windows' installed*
- in the directory you want your files downloaded run: `git clone {YOUR GIT REPO HERE}`
- Create the needed files if not already created
- *have python 3+  installed*
- Perferrably 1 directory up from where your files are located, run `python3 -m http.server`
	- this will allow access of the the files in the directory(s) via [http:localhost:8000/]()
	- you can try that link in your browser to see what's hosted.
- you'll need to update the file links in the extension.json file to make that paths.. for example 
	- "url" path might be something like [http:localhost:8000/my-theme/main.css]()
	- "download" might be something like - [http:localhost:8000/my-theme.zip]()
- For your extension.json, you can local host that too ([http:localhost:8000/extension.json]()) OR use your listed.to link. just make sure it has the localhost urls

Whenever you update your main.css, you'll need to (re)create a .zip file of your theme's directory. And unfortunately, as far as I know, you'll have to uninstall and reinstall the theme each time.. a bit tedious but oh well.

---
# 5. Publishing Theme
Finally, you're done developing...

You should have the following completed:
- Github repo for your Theme
	- main.css
	- package.json
		- version number is updated
	- released a Tag of your finished theme
- Extension.json hosted somewhere
	- links point to Github release Tag
	- colors for dock_icon are updated to match theme
	- version number is updated

You should be good to go.. share your install link.



---
# Examples
-Monochrome Dark Theme-
Github: https://github.com/Parkertg/sn-theme-monochrome-dark
Install Link: https://listed.to/p/eY9kuTLQzB


## Suggest Edit on Github
https://github.com/Parkertg/sn-theme-howtodocumentation
