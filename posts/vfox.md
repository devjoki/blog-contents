![post_logo](../images/vfox.jpg)
# Say Goodbye to Version Hell
## Streamline Your Development Environment with VFox

Managing SDKs and development tools can be a huge pain, especially when different projects require different versions.
Manually configuring them in the IDE or constantly changing the PATH is very annoying, and sometimes forgetting to do it can cause some headaches.
There are some applications out there to manage these versions, but most of them only target a specific SDK or tool, so you have to find one for each. Or do you?

[VFox](https://vfox.lhan.me/) is here to the rescue! VFox is a really good version manager that handles multiple SDKs out of the box. The main features are:

* cross-platform
* pluggable - really easy to add support for new runtimes
* fast
* supports config files so it is easy to migrate
* shell auto-completion

### Usage
Listing all available plugins
```
vfox available
```
Adding a plugin
```
vfox add java
```
Installing a specific version
```
vfox install java@$JAVA_VERSION
```
Using a specific version globally
```
vfox use -g java@$JAVA_VERSION
```
<br/>
It really is a great tool in my opinion . Since I found it, I've been using it to manage everything from the Java SDK to Kubectl.<br/>
If you are struggling with version management, I recommend giving VFox a try. You will not regret it.<br/>
<br/>
I hope this was useful. See you next time!
