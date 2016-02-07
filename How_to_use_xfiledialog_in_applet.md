## Procedures: how to use xfiledialog in applets ##

Demo of XFileDialog in Applet:
https://sites.google.com/site/jtvmaker/Home/xfiledialog-online-demo

### Step 1 ###
> If you do not have any certificate, buy one or create a self-signed certificate at first.

> to create a self-signed certificate:
```
      keytool -genkey -alias personalkey
```

### Step 2 ###
> Package all class and resource files into a jar.

> e.g.
> In xfiledialog's root directory, run the following two commands
> (use ant if you wish)
```
      jar cvf appletdemo/hello.jar helloapplet.class
      jar uvf appletdemo/hello.jar -C src_java net
```


### Step 3 ###
> Use the certificate to sign the jar.
> e.g.
> In xfiledialog's root directory
```
   cd appletdemo
   jarsigner hello.jar personalkey
```

### Step 4 ###
> Package the xfiledialog.dll, xfiledialog64.dll into a jar file.
> e.g.
> In xfiledialog's appletdemo directory
```
   cd ..
   jar cvf win_x86_dll.jar  xfiledialog.dll xfiledialog.dll.manifest
   jar cvf win_x64_dll.jar  xfiledialog64.dll xfiledialog64.dll.manifest
   move win_x86_dll.jar appletdemo
   move win_x64_dll.jar appletdemo
   cd appletdemo
```

### Step 5 ###
> Important! Sign the nativelib jar file too!

```
   jarsigner win_x86_dll.jar personalkey 
   jarsigner win_x64_dll.jar personalkey
```

> Otherwise, the applet can not load the library and may throw an
> UnsatisfiedLinkError Exception.

### Step 6 ###
> Deploy the applet.
> Applets with native dlls should be deployed with jnlp and deployJava.js

  * Copy the deployJava.js from Sun/Oracle to your server at first. As the internet connection is not always stable, this javascript file and the jar file should be kept on the same server.

> http://www.java.com/js/deployJava.js

  * Write a jnlp file to tell the applet how to find the native dll

```
	<?xml version="1.0" encoding="UTF-8"?>
	<jnlp spec="1.0+" codebase="" href="">
	    <information>
        	<title>helloapplet</title>
	        <vendor>stevpan</vendor>
	</information>

	    <resources os="Windows" arch="x86">
		<nativelib href="win_x86_dll.jar" />
	    </resources>

	    <resources os="Windows" arch="amd64">
		<nativelib href="win_x64_dll.jar" />
	    </resources>

	    <resources>
        	<!-- Application Resources -->
	        <j2se version="1.6+"
        	      href="http://java.sun.com/products/autodl/j2se" />
	        <jar href="hello.jar" main="true" />
	    </resources>


	    <applet-desc 
        	 name="helloapplet"
	         main-class="helloapplet"
        	 width="640"
	         height="480">
	     </applet-desc>
	     <update check="background"/>
	</jnlp>				
```

  * Write the html/javascript code
```
    <script src="deployJava.js"></script>
    <script> 
        var attributes = { code:'helloapplet',  width:600, height:400} ; 
        var parameters = {jnlp_href: 'applet.jnlp'} ; 
        deployJava.runApplet(attributes, parameters, '1.6'); 
    </script>
```


---

### References ###

  * code signing
> http://java.sun.com/developer/onlineTraining/Programming/JDCBook/signed.html

  * new method for applet deployment
> http://java.sun.com/javase/6/docs/technotes/guides/jweb/deployment_advice.html