# BackInfo System Information Utility 
Hey everyone!
<!-- wp:paragraph -->
<p>Unfortunately, the binaries are no longer exist. The only way to acquire this tool these days is from the community :) I've created a Github repo, that contains the binaries of the utility, in an attempt to keep lights on for this utility. </p>
<!-- /wp:paragraph -->
<!-- wp:image {"align":"center","id":2400,"sizeSlug":"large","linkDestination":"none"} -->
<div class="wp-block-image"><figure class="aligncenter size-large"><img src="https://www.markou.me/wp-content/uploads/2022/01/image-3-1200x614.png" alt="" class="wp-image-2400"/><figcaption>BackInfo - look and feel</figcaption></figure></div>
<!-- /wp:image -->
<!-- wp:paragraph -->
<p>Feel free to use the following link down below to grab a copy!</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><a href="https://github.com/george-markou/BackInfo/raw/main/Backinfo.zip">Download Li</a><a href="https://github.com/george-markou/BackInfo/raw/main/Backinfo.zip" data-type="URL" data-id="https://github.com/george-markou/BackInfo/raw/main/Backinfo.zip">nk</a> - File Hash SHA256: 977168A6FA431A439FA26792B798B0D5C39A8A219746E8FABC4531A43B7627</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>How to use it</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Now that you hold a copy of this utility, how can you make use of it? Well, if you examine closely the contents of the folder, you will notice 2 files, the application .exe file, and the configuration .ini file. No setup or installation is needed.</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":2399,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full"><img src="https://www.markou.me/wp-content/uploads/2022/01/image-2.png" alt="" class="wp-image-2399"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>If you do like the information illustrated in the picture up above, then you don't need to make any changes to the configuration file. In case you would like to add or remove information to be displayed, then feel free to edit the configuration file. <em><strong>These two files must and should always remain within the same folder!</strong></em></p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>File Placement</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>I usually prefer to place the application files under "C:\Program Files\BackInfo" but nevertheless, you could always choose a different location on your systems.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Make BackInfo load during system startup</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>In order for this utility to function properly, and display system information, it must be executed during system startup. In order to accomplish that, there are three possible methods:</p>
<!-- /wp:paragraph -->

<!-- wp:list {"style":{"typography":{"fontSize":"18px"}}} -->
<ul style="font-size:18px"><li><strong>Registry</strong></li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Create, set, and forget, a registry key under subkey "HKLM:\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Run" that will point to the application file. This will ensure that the application will run during system startup. </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Use the following PowerShell one-liner to create the required key, modify the path of the application in case that is stored elsewhere other than Program Files.</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="powershell" class="language-powershell">New-ItemProperty -Path "HKLM:\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Run" -Name BackInfo -Type String -Value "C:\Program Files\BackInfo\Backinfo.exe"</code></pre>
<!-- /wp:code -->

<!-- wp:list {"style":{"typography":{"fontSize":"18px"}}} -->
<ul style="font-size:18px"><li><strong>Placing application shortcut on Startup folder</strong></li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Create a shortcut pointing to the application under  "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp".  This will ensure that the application will run during system startup.  </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p> Use the following PowerShell script to create the required shortcut, modify the path of the application in case that is stored elsewhere other than Program Files. </p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="powershell" class="language-powershell">$SourceFilePath = "C:\Program Files\BackInfo\BackInfo.exe"
$ShortcutPath = "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp\BackInfo.lnk"
$WScriptObj = New-Object -ComObject ("WScript.Shell")
$shortcut = $WscriptObj.CreateShortcut($ShortcutPath)
$shortcut.TargetPath = $SourceFilePath
$shortcut.Save()</code></pre>
<!-- /wp:code -->

<!-- wp:list {"style":{"typography":{"fontSize":"18px"}}} -->
<ul style="font-size:18px"><li><strong>A combination of any of the above methods with Group Policy</strong></li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>When managing a large number of servers or even a dozen, going manual as described above definitely is not an option. The most suitable option would be PSRemoting, DSC but the best one, if the servers are domain members, would be <strong>Group Policy</strong>.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->
<h4>C<strong>onfiguring BackInfo on multiple servers using Group Policy</strong></h4>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol><li>Place the files on a network location that is accessible by all server systems within your environment. This might be e.g a File Server or the Netlogon Folder.</li><li>Create a new Group Policy Object.</li></ol>
<!-- /wp:list -->

<!-- wp:image {"id":2406,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full"><img src="https://www.markou.me/wp-content/uploads/2022/01/image-4.png" alt="" class="wp-image-2406"/><figcaption>3. Computer Configuration -&gt; Preferences -&gt; Windows Settings -&gt; Folders -&gt; New Folder. Use the following settings, on Tab Common make sure that "Remove this item when it is no longer applied" is checked. </figcaption></figure>
<!-- /wp:image -->

<!-- wp:image {"align":"center","id":2407,"sizeSlug":"full","linkDestination":"none"} -->
<div class="wp-block-image"><figure class="aligncenter size-full"><img src="https://www.markou.me/wp-content/uploads/2022/01/image-5.png" alt="" class="wp-image-2407"/><figcaption> GPO - New Folder Properties </figcaption></figure></div>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>4.  Computer Configuration -&gt; Preferences -&gt; Windows Settings -&gt; Files -&gt; New File. Use the following settings, on Tab Common make sure that "Remove this item when it is no longer applied" is checked.  </p>
<!-- /wp:paragraph -->

<!-- wp:image {"align":"center","id":2408,"sizeSlug":"full","linkDestination":"none"} -->
<div class="wp-block-image"><figure class="aligncenter size-full"><img src="https://www.markou.me/wp-content/uploads/2022/01/image-6.png" alt="" class="wp-image-2408"/><figcaption>GPO - New File Properties</figcaption></figure></div>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>5.  Computer Configuration -&gt; Preferences -&gt; Windows Settings -&gt; Shortcuts -&gt; New Shortcut. Use the following settings, on Tab Common make sure that "Remove this item when it is no longer applied" is checked. </p>
<!-- /wp:paragraph -->

<!-- wp:image {"align":"center","id":2409,"sizeSlug":"full","linkDestination":"none"} -->
<div class="wp-block-image"><figure class="aligncenter size-full"><img src="https://www.markou.me/wp-content/uploads/2022/01/image-7.png" alt="" class="wp-image-2409"/><figcaption>GPO - New Shortcut Properties</figcaption></figure></div>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>6. Link the newly created Group Policy to the OU of your preference. </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>7. Wait for the effect to take place. By default, the computer&nbsp;<strong>Group Policy</strong>&nbsp;is refreshed every 90 minutes.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>8. Enjoy!</p>
<!-- /wp:paragraph -->

<p>Feel free to drop your comment or question below.</p>
<!-- /wp:paragraph -->
