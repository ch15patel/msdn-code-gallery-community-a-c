# ASP.NET File Manager
## Requires
- Visual Studio 2015
## License
- MIT
## Technologies
- ASP.NET
## Topics
- asp.net file manager
## Updated
- 08/08/2019
## Description

<h1>FileUltimate: ASP.NET File Manager</h1>
<p>File Manager Control for ASP.NET WebForms and ASP.NET MVC 3&#43; (.NET Framework 4.0&#43;).</p>
<p>Integrate a file manager into your ASP.NET application or site rapidly.&nbsp;</p>
<ul>
<li>Browse and manage files with access control.&nbsp; </li><li>Accept files with the advanced upload functionality. </li><li>Offer a structured and neat download area. </li><li>Preview documents (70&#43; file formats, including PDF &amp; Microsoft Office), images, audios and videos.
</li></ul>
<p><img id="153279" src="153279-asp-net-file-manager.png" alt="" width="736" height="590"></p>
<p><strong>Note:</strong> This project&nbsp;contains a fully working version of the product, however without a license key it will run in trial mode. For more information, please see&nbsp;<a href="http://www.gleamtech.com/fileultimate">FileUltimate: ASP.NET
 File Manager</a>&nbsp;product page.</p>
<div>
<div class="highlight highlight-text-xml"></div>
<div>
<div></div>
</div>
</div>
<div class="mcePaste" id="_mcePaste" style="left:-10000px; top:286px; width:1px; height:1px; overflow:hidden">
<h3 style="line-height:1.25; margin-top:24px; margin-bottom:16px; font-size:1.25em; color:#24292e">
To use FileUltimate in an ASP.NET MVC Project, do the following in Visual Studio:</h3>
<ol style="padding:0px 40px 0px 2em; margin-top:0px; margin-bottom:16px; color:#24292e; font-size:16px">
<li>
<p style="margin-top:16px; margin-bottom:16px">Add references to FileUltimate assemblies. There are two ways to perform this: &nbsp;</p>
<ul style="padding:0px 40px 0px 2em; margin-top:0px; margin-bottom:0px">
<li>
<p style="margin-top:16px; margin-bottom:16px">Add reference to&nbsp;<span style="font-weight:600">GleamTech.Core.dll</span>&nbsp;and&nbsp;<span style="font-weight:600">GleamTech.FileUltimate.dll</span>&nbsp;found in &quot;Bin&quot; folder of FileUltimate-vX.X.X.X.zip
 package which you already downloaded and extracted. &nbsp;</p>
<blockquote style="font-style:italic; font-family:Georgia,Times,&quot;Times New Roman&quot;,serif; padding:0px 1em; margin:0px 0px 16px; color:#6a737d; border:0px 0px 0px 0.25em solid #cccccc #cccccc #cccccc #dfe2e5">
<p style="margin-top:0px; margin-bottom:0px">The other DLLs in the same folder, i.e.&nbsp;<span style="font-weight:600">GleamTech.ImageUltimate.dll</span>,&nbsp;<span style="font-weight:600">GleamTech.VideoUltimate.dll</span>&nbsp;and&nbsp;<span style="font-weight:600">GleamTech.DocumentUltimate.dll</span>&nbsp;are
 assemblies that FileUltimate depends on for some of the features. They are separate assemblies as they are also standalone products with the same names. MSbuild or Visual Studio will automatically copy these 3 DLLs along with the main referenced assembly&nbsp;<span style="font-weight:600">GleamTech.FileUltimate.dll</span>&nbsp;to
 your bin folder during build so they don't need to be referenced directly (unless you are using these products separately in the same project and you have a license for them). Note that even without these 3 DLLs, FileUltimate will work but it will just turn
 off the corresponding features such as generating image or video thumbnails or the document viewer. So with this modular approach, you can opt-out of the features you do not need by excluding the corresponding DLL, i.e. MSBuild or Visual Studio would automatically
 copy a dependency only if that DLL is found in the same folder as the main referenced DLL so you can simply delete/move a DLL to opt-out.</p>
</blockquote>
</li><li style="margin-top:0.25em">
<p style="margin-top:16px; margin-bottom:16px">Or install NuGet package and add references automatically via NuGet Package Manager in Visual Studio: Go to&nbsp;<span style="font-weight:600">Tools -&gt; NuGet Package Manager -&gt; Package Manager Console</span>&nbsp;and
 run this command:</p>
<p style="margin-top:16px; margin-bottom:16px"><code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">Install-Package FileUltimate -Source https://get.gleamtech.com/nuget/default/</code></p>
<p style="margin-top:16px; margin-bottom:16px">If you prefer using the user interface when working with NuGet, you can also install the package this way:</p>
<ul style="padding:0px 40px 0px 2em; margin-top:0px; margin-bottom:0px">
<li>
<p style="margin-top:16px; margin-bottom:16px">&nbsp;GleamTech has its own NuGet feed so first you need to add this feed to be able to find GleamTech's packages. Go to&nbsp;<span style="font-weight:600">Tools -&gt; NuGet Package Manager -&gt; Package Manager
 Settings</span>&nbsp;and then click the&nbsp;<span style="font-weight:600">&#43;</span>&nbsp;button to add a new package source. Enter&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">GleamTech</code>&nbsp;in&nbsp;<span style="font-weight:600">Name</span>&nbsp;field
 and&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">https://get.gleamtech.com/nuget/default/</code>&nbsp;in&nbsp;<span style="font-weight:600">Source</span>field
 and click&nbsp;<span style="font-weight:600">OK</span>.</p>
</li><li style="margin-top:0.25em">
<p style="margin-top:16px; margin-bottom:16px">Go to&nbsp;<span style="font-weight:600">Tools -&gt; NuGet Package Manager -&gt; Manage NuGet Packages for Solution</span>, select&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">GleamTech</code>&nbsp;or&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">All</code>&nbsp;in
 the Package source dropdown on the top right. Now enter&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">FileUltimate</code>&nbsp;in the search field, and click&nbsp;<span style="font-weight:600">Install</span>button
 on the found package.</p>
</li></ul>
</li></ul>
</li><li style="margin-top:0.25em">
<p style="margin-top:16px; margin-bottom:16px">Set FileUltimate's global configuration. For example, you may want to set the license key. Insert some of the following lines (if overriding a default value is required) into the&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">Application_Start</code>&nbsp;method
 of your&nbsp;<span style="font-weight:600">Global.asax.cs</span>:</p>
<div class="highlight highlight-source-cs" style="margin-bottom:16px">
<pre style="white-space:pre-wrap; word-wrap:normal; font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal"><span class="pl-c" style="color:#6a737d">//Set&nbsp;this&nbsp;property&nbsp;only&nbsp;if&nbsp;you&nbsp;have&nbsp;a&nbsp;valid&nbsp;license&nbsp;key,&nbsp;otherwise&nbsp;do&nbsp;not&nbsp;</span>
<span class="pl-c" style="color:#6a737d">//set&nbsp;it&nbsp;so&nbsp;FileUltimate&nbsp;runs&nbsp;in&nbsp;trial&nbsp;mode.&nbsp;&nbsp;</span>
<span class="pl-en" style="color:#6f42c1">FileUltimateConfiguration.Current.LicenseKey</span>&nbsp;=&nbsp;&quot;QQJDJLJP34...&quot;;</pre>
</div>
<p style="margin-top:16px; margin-bottom:16px">Alternatively you can specify the configuration in&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">&lt;appSettings&gt;</code>&nbsp;tag
 of your Web.config.</p>
<div class="highlight highlight-text-xml" style="margin-bottom:16px">
<pre style="white-space:pre-wrap; word-wrap:normal; font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal">&lt;<span class="pl-ent" style="color:#22863a">add</span> <span class="pl-e" style="color:#6f42c1">key</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>FileUltimate:LicenseKey<span class="pl-pds">&quot;</span></span> <span class="pl-e" style="color:#6f42c1">value</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>QQJDJLJP34...<span class="pl-pds">&quot;</span></span> /&gt; </pre>
</div>
<p style="margin-top:16px; margin-bottom:16px">As you would notice,&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">FileUltimate:</code>&nbsp;prefix maps to&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">FileUltimateConfiguration.Current</code>.
 &nbsp;</p>
</li><li style="margin-top:0.25em">
<p style="margin-top:16px; margin-bottom:16px">Open one of your View pages (eg. Index.cshtml) and at the top of your page add the necessary namespaces:</p>
<div class="highlight highlight-source-cs" style="margin-bottom:16px">
<pre style="white-space:pre-wrap; word-wrap:normal; font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal">@<span class="pl-k" style="color:#d73a49">using</span>&nbsp;<span class="pl-en" style="color:#6f42c1">GleamTech.AspNet.Mvc</span>
@<span class="pl-k" style="color:#d73a49">using</span>&nbsp;<span class="pl-en" style="color:#6f42c1">GleamTech.FileUltimate</span></pre>
</div>
<p style="margin-top:16px; margin-bottom:16px">Alternatively you can add the namespaces globally in&nbsp;<span style="font-weight:600">Views/Web.config</span>&nbsp;under&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">&lt;system.web.webPages.razor&gt;/&lt;pages&gt;/&lt;namespaces&gt;</code>&nbsp;tag
 to avoid adding namespaces in your pages every time:</p>
<div class="highlight highlight-text-xml" style="margin-bottom:16px">
<pre style="white-space:pre-wrap; word-wrap:normal; font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal">&lt;<span class="pl-ent" style="color:#22863a">add</span> <span class="pl-e" style="color:#6f42c1">namespace</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>GleamTech.AspNet.Mvc<span class="pl-pds">&quot;</span></span> /&gt;
&lt;<span class="pl-ent" style="color:#22863a">add</span> <span class="pl-e" style="color:#6f42c1">namespace</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>GleamTech.FileUltimate<span class="pl-pds">&quot;</span></span> /&gt;</pre>
</div>
<p style="margin-top:16px; margin-bottom:16px">Now in your page insert these lines:</p>
<div class="highlight highlight-source-cs" style="margin-bottom:16px">
<pre style="white-space:pre-wrap; word-wrap:normal; font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal">&lt;!DOCTYPE html&gt;
@{
    <span class="pl-k" style="color:#d73a49">var</span> <span class="pl-en" style="color:#6f42c1">fileManager </span>= <span class="pl-k" style="color:#d73a49">new</span> <span class="pl-en" style="color:#6f42c1">FileManager</span>
    {
        Width = <span class="pl-c1" style="color:#005cc5">800</span>,
        Height = <span class="pl-c1" style="color:#005cc5">600</span>,
        Resizable = <span class="pl-c1" style="color:#005cc5">true</span>
    };

    <span class="pl-k" style="color:#d73a49">var</span> <span class="pl-en" style="color:#6f42c1">rootFolder </span>= <span class="pl-k" style="color:#d73a49">new</span> <span class="pl-en" style="color:#6f42c1">FileManagerRootFolder</span>
    {
        Name = <span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>A Root Folder<span class="pl-pds">&quot;</span></span>,
        Location = <span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>~/App_Data/RootFolder1<span class="pl-pds">&quot;</span></span>
    };

    rootFolder.AccessControls.Add(<span class="pl-k" style="color:#d73a49">new</span> <span class="pl-en" style="color:#6f42c1">FileManagerAccessControl</span>
    {
        Path = <span class="pl-s" style="color:#032f62">@&quot;\&quot;</span>,
        AllowedPermissions = FileManagerPermissions.Full
    });

    fileManager.RootFolders.Add(rootFolder);
}
&lt;<span class="pl-en" style="color:#6f42c1">html</span>&gt;
&lt;html&gt;
    &lt;head&gt;
        &lt;title&gt;File Manager&lt;/title&gt;
        @this.<span class="pl-en" style="color:#6f42c1">RenderHead</span>(fileManager)
    &lt;/head&gt;
    &lt;body&gt;
        @this.<span class="pl-en" style="color:#6f42c1">RenderBody</span>(fileManager)
    &lt;/body&gt;
&lt;/html&gt;</pre>
</div>
<p style="margin-top:16px; margin-bottom:16px">This will render a file manager control in the page which displays one root folder named &quot;A Root Folder&quot; which points to &quot;~/App_Data/RootFolder1&quot; with Full permissions.</p>
</li></ol>
<h3 style="line-height:1.25; margin-top:24px; margin-bottom:16px; font-size:1.25em; color:#24292e">
<a id="user-content-to-use-fileultimate-in-an-aspnet-webforms-project-do-the-following-in-visual-studio" class="anchor" href="https://github.com/GleamTech/FileUltimate#to-use-fileultimate-in-an-aspnet-webforms-project-do-the-following-in-visual-studio" style="color:#0366d6; background-color:transparent; float:left; padding-right:4px; margin-left:-20px; line-height:1"></a>To
 use FileUltimate in an ASP.NET WebForms Project, do the following in Visual Studio:</h3>
<ol style="padding:0px 40px 0px 2em; margin-top:0px; margin-bottom:16px; color:#24292e; font-size:16px">
<li>
<p style="margin-top:16px; margin-bottom:16px">Add references to FileUltimate assemblies. There are two ways to perform this: &nbsp;</p>
<ul style="padding:0px 40px 0px 2em; margin-top:0px; margin-bottom:0px">
<li>
<p style="margin-top:16px; margin-bottom:16px">Add reference to&nbsp;<span style="font-weight:600">GleamTech.Core.dll</span>&nbsp;and&nbsp;<span style="font-weight:600">GleamTech.FileUltimate.dll</span>&nbsp;found in &quot;Bin&quot; folder of FileUltimate-vX.X.X.X.zip
 package which you already downloaded and extracted. &nbsp;</p>
<blockquote style="font-style:italic; font-family:Georgia,Times,&quot;Times New Roman&quot;,serif; padding:0px 1em; margin:0px 0px 16px; color:#6a737d; border:0px 0px 0px 0.25em solid #cccccc #cccccc #cccccc #dfe2e5">
<p style="margin-top:0px; margin-bottom:0px">The other DLLs in the same folder, i.e.&nbsp;<span style="font-weight:600">GleamTech.ImageUltimate.dll</span>,&nbsp;<span style="font-weight:600">GleamTech.VideoUltimate.dll</span>&nbsp;and&nbsp;<span style="font-weight:600">GleamTech.DocumentUltimate.dll</span>&nbsp;are
 assemblies that FileUltimate depends on for some of the features. They are separate assemblies as they are also standalone products with the same names. MSbuild or Visual Studio will automatically copy these 3 DLLs along with the main referenced assembly&nbsp;<span style="font-weight:600">GleamTech.FileUltimate.dll</span>&nbsp;to
 your bin folder during build so they don't need to be referenced directly (unless you are using these products separately in the same project and you have a license for them). Note that even without these 3 DLLs, FileUltimate will work but it will just turn
 off the corresponding features such as generating image or video thumbnails or the document viewer. So with this modular approach, you can opt-out of the features you do not need by excluding the corresponding DLL, i.e. MSBuild or Visual Studio would automatically
 copy a dependency only if that DLL is found in the same folder as the main referenced DLL so you can simply delete/move a DLL to opt-out.</p>
</blockquote>
</li><li style="margin-top:0.25em">
<p style="margin-top:16px; margin-bottom:16px">Or install NuGet package and add references automatically via NuGet Package Manager in Visual Studio: Go to&nbsp;<span style="font-weight:600">Tools -&gt; NuGet Package Manager -&gt; Package Manager Console</span>&nbsp;and
 run this command:</p>
<p style="margin-top:16px; margin-bottom:16px"><code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">Install-Package FileUltimate -Source https://get.gleamtech.com/nuget/default/</code></p>
<p style="margin-top:16px; margin-bottom:16px">If you prefer using the user interface when working with NuGet, you can also install the package this way:</p>
<ul style="padding:0px 40px 0px 2em; margin-top:0px; margin-bottom:0px">
<li>
<p style="margin-top:16px; margin-bottom:16px">&nbsp;GleamTech has its own NuGet feed so first you need to add this feed to be able to find GleamTech's packages. Go to&nbsp;<span style="font-weight:600">Tools -&gt; NuGet Package Manager -&gt; Package Manager
 Settings</span>&nbsp;and then click the&nbsp;<span style="font-weight:600">&#43;</span>&nbsp;button to add a new package source. Enter&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">GleamTech</code>&nbsp;in&nbsp;<span style="font-weight:600">Name</span>&nbsp;field
 and&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">https://get.gleamtech.com/nuget/default/</code>&nbsp;in&nbsp;<span style="font-weight:600">Source</span>field
 and click&nbsp;<span style="font-weight:600">OK</span>.</p>
</li><li style="margin-top:0.25em">
<p style="margin-top:16px; margin-bottom:16px">Go to&nbsp;<span style="font-weight:600">Tools -&gt; NuGet Package Manager -&gt; Manage NuGet Packages for Solution</span>, select&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">GleamTech</code>&nbsp;or&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">All</code>&nbsp;in
 the Package source dropdown on the top right. Now enter&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">FileUltimate</code>&nbsp;in the search field, and click&nbsp;<span style="font-weight:600">Install</span>button
 on the found package.</p>
</li></ul>
</li></ul>
</li><li style="margin-top:0.25em">
<p style="margin-top:16px; margin-bottom:16px">Set FileUltimate's global configuration. For example, you may want to set the license key. Insert some of the following lines (if overriding a default value is required) into the&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">Application_Start</code>&nbsp;method
 of your&nbsp;<span style="font-weight:600">Global.asax.cs</span>:</p>
<div class="highlight highlight-source-cs" style="margin-bottom:16px">
<pre style="white-space:pre-wrap; word-wrap:normal; font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal"><span class="pl-c" style="color:#6a737d">//Set&nbsp;this&nbsp;property&nbsp;only&nbsp;if&nbsp;you&nbsp;have&nbsp;a&nbsp;valid&nbsp;license&nbsp;key,&nbsp;otherwise&nbsp;do&nbsp;not&nbsp;</span>
<span class="pl-c" style="color:#6a737d">//set&nbsp;it&nbsp;so&nbsp;FileUltimate&nbsp;runs&nbsp;in&nbsp;trial&nbsp;mode.&nbsp;&nbsp;</span>
<span class="pl-en" style="color:#6f42c1">FileUltimateConfiguration.Current.LicenseKey</span>&nbsp;=&nbsp;&quot;QQJDJLJP34...&quot;;</pre>
</div>
<p style="margin-top:16px; margin-bottom:16px">Alternatively you can specify the configuration in&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">&lt;appSettings&gt;</code>&nbsp;tag
 of your Web.config.</p>
<div class="highlight highlight-text-xml" style="margin-bottom:16px">
<pre style="white-space:pre-wrap; word-wrap:normal; font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal">&lt;<span class="pl-ent" style="color:#22863a">add</span> <span class="pl-e" style="color:#6f42c1">key</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>FileUltimate:LicenseKey<span class="pl-pds">&quot;</span></span> <span class="pl-e" style="color:#6f42c1">value</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>QQJDJLJP34...<span class="pl-pds">&quot;</span></span> /&gt; </pre>
</div>
<p style="margin-top:16px; margin-bottom:16px">As you would notice,&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">FileUltimate:</code>&nbsp;prefix maps to&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">FileUltimateConfiguration.Current</code>.
 &nbsp;</p>
</li><li style="margin-top:0.25em">
<p style="margin-top:16px; margin-bottom:16px">Open one of your pages (eg. Default.aspx) and at the top of your page add add the necessary namespaces:</p>
<div class="highlight highlight-text-html-asp" style="margin-bottom:16px">
<pre style="white-space:pre-wrap; word-wrap:normal; font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal"><span class="pl-s1"><span class="pl-pse">&lt;%</span>@&nbsp;Register&nbsp;TagPrefix<span class="pl-k" style="color:#d73a49">=</span><span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>GleamTech<span class="pl-pds">&quot;</span></span>&nbsp;Namespace<span class="pl-k" style="color:#d73a49">=</span><span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>GleamTech.FileUltimate<span class="pl-pds">&quot;</span></span>&nbsp;Assembly<span class="pl-k" style="color:#d73a49">=</span><span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>GleamTech.FileUltimate<span class="pl-pds">&quot;</span></span>&nbsp;<span class="pl-pse">%&gt;</span></span></pre>
</div>
<p style="margin-top:16px; margin-bottom:16px">Alternatively you can add the namespaces globally in&nbsp;<span style="font-weight:600">Web.config</span>&nbsp;under&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">&lt;system.web&gt;/&lt;pages&gt;/&lt;controls&gt;</code>&nbsp;tag
 to avoid adding namespaces in your pages every time:</p>
<div class="highlight highlight-text-xml" style="margin-bottom:16px">
<pre style="white-space:pre-wrap; word-wrap:normal; font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal">&lt;<span class="pl-ent" style="color:#22863a">add</span> <span class="pl-e" style="color:#6f42c1">tagPrefix</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>GleamTech<span class="pl-pds">&quot;</span></span> <span class="pl-e" style="color:#6f42c1">namespace</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>GleamTech.FileUltimate<span class="pl-pds">&quot;</span></span> <span class="pl-e" style="color:#6f42c1">assembly</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>GleamTech.FileUltimate<span class="pl-pds">&quot;</span></span> /&gt;</pre>
</div>
<p style="margin-top:16px; margin-bottom:16px">Now in your page insert these lines:</p>
<div class="highlight highlight-text-html-asp" style="margin-bottom:16px">
<pre style="white-space:pre-wrap; word-wrap:normal; font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal">&lt;!DOCTYPE html&gt;
&lt;<span class="pl-ent" style="color:#22863a">html</span>&gt;
    &lt;<span class="pl-ent" style="color:#22863a">head</span> <span class="pl-e" style="color:#6f42c1">runat</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>server<span class="pl-pds">&quot;</span></span>&gt;
        &lt;<span class="pl-ent" style="color:#22863a">title</span>&gt;Document Viewer&lt;/<span class="pl-ent" style="color:#22863a">title</span>&gt;
    &lt;/<span class="pl-ent" style="color:#22863a">head</span>&gt;
    &lt;<span class="pl-ent" style="color:#22863a">body</span>&gt;
        &lt;<span class="pl-ent" style="color:#22863a">GleamTech:FileManagerControl</span> <span class="pl-e" style="color:#6f42c1">ID</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>fileManager<span class="pl-pds">&quot;</span></span> <span class="pl-e" style="color:#6f42c1">runat</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>server<span class="pl-pds">&quot;</span></span> 
                                <span class="pl-e" style="color:#6f42c1">Width</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>800<span class="pl-pds">&quot;</span></span>
                                <span class="pl-e" style="color:#6f42c1">Height</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>600<span class="pl-pds">&quot;</span></span> 
                                <span class="pl-e" style="color:#6f42c1">Resizable</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>True<span class="pl-pds">&quot;</span></span>&gt;
            
            &lt;<span class="pl-ent" style="color:#22863a">GleamTech:FileManagerRootFolder</span> <span class="pl-e" style="color:#6f42c1">Name</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>A Root Folder<span class="pl-pds">&quot;</span></span> <span class="pl-e" style="color:#6f42c1">Location</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>~/App_Data/RootFolder1<span class="pl-pds">&quot;</span></span> &gt; 
                &lt;<span class="pl-ent" style="color:#22863a">GleamTech:FileManagerAccessControl</span> <span class="pl-e" style="color:#6f42c1">Path</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>\<span class="pl-pds">&quot;</span></span> <span class="pl-e" style="color:#6f42c1">AllowedPermissions</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>Full<span class="pl-pds">&quot;</span></span>/&gt; 
            &lt;/<span class="pl-ent" style="color:#22863a">GleamTech:FileManagerRootFolder</span>&gt;

        &lt;/<span class="pl-ent" style="color:#22863a">GleamTech:FileManagerControl</span>&gt; 
    &lt;/<span class="pl-ent" style="color:#22863a">body</span>&gt;
&lt;/<span class="pl-ent" style="color:#22863a">html</span>&gt;</pre>
</div>
<p style="margin-top:16px; margin-bottom:16px">This will render a file manager control in the page which displays one root folder named &quot;A Root Folder&quot; which points to &quot;~/App_Data/RootFolder1&quot; with Full permissions.</p>
</li></ol>
<h3 style="line-height:1.25; margin-top:24px; margin-bottom:16px; font-size:1.25em; color:#24292e">
<a id="user-content-optional" class="anchor" href="https://github.com/GleamTech/FileUltimate#optional" style="color:#0366d6; background-color:transparent; float:left; padding-right:4px; margin-left:-20px; line-height:1"></a>Optional:</h3>
<p style="margin-top:0px; margin-bottom:16px; color:#24292e; font-size:16px">FileUltimate does not depend on any Web.config settings to work (it's config-free for easy deployment).&nbsp;However if you want to support the lowest level upload method Html4 which
 is the only possible method&nbsp;for old browsers without Html5 or Flash or Silverlight support, then&nbsp;you will need to&nbsp;increase the request limits (ASP.NET's default is 4MB) so that you can upload&nbsp;files larger than 4MB on these browsers. Edit
 your project's Web.config file and add the following settings inside &lt;configuration&gt; tag: &nbsp;</p>
<div class="highlight highlight-text-xml" style="margin-bottom:16px; color:#24292e; font-size:16px">
<pre style="white-space:pre-wrap; word-wrap:normal; font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal">&nbsp;&nbsp;<span class="pl-c" style="color:#6a737d"><span class="pl-c">&lt;!--</span>&nbsp;</span>
<span class="pl-c" style="color:#6a737d">&nbsp;&nbsp;&nbsp;&nbsp;Html4&nbsp;upload&nbsp;method&nbsp;requires&nbsp;the&nbsp;limits&nbsp;to&nbsp;be&nbsp;set&nbsp;to&nbsp;the&nbsp;maximum&nbsp;value&nbsp;(2&nbsp;GB).</span>
<span class="pl-c" style="color:#6a737d">&nbsp;&nbsp;&nbsp;&nbsp;Other&nbsp;upload&nbsp;methods&nbsp;use&nbsp;chunking&nbsp;so&nbsp;there&nbsp;is&nbsp;no&nbsp;2GB&nbsp;limit&nbsp;for&nbsp;them.</span>
<span class="pl-c" style="color:#6a737d">&nbsp;&nbsp;<span class="pl-c">--&gt;</span></span>
&nbsp;&nbsp;&lt;<span class="pl-ent" style="color:#22863a">location</span>&nbsp;path=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>fileuploader.ashx<span class="pl-pds">&quot;</span></span>&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&lt;<span class="pl-ent" style="color:#22863a">system</span>.webServer&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;<span class="pl-ent" style="color:#22863a">security</span>&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;<span class="pl-ent" style="color:#22863a">requestFiltering</span>&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="pl-c" style="color:#6a737d"><span class="pl-c">&lt;!--</span>&nbsp;</span>
<span class="pl-c" style="color:#6a737d">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Maximum&nbsp;value&nbsp;for&nbsp;maxAllowedContentLength&nbsp;(in&nbsp;bytes)&nbsp;is&nbsp;2147483648&nbsp;(2GB).&nbsp;</span>
<span class="pl-c" style="color:#6a737d">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;maxAllowedContentLength&nbsp;should&nbsp;be&nbsp;always&nbsp;equal&nbsp;to&nbsp;(or&nbsp;greater&nbsp;than)&nbsp;maxRequestLength&nbsp;x&nbsp;1024.</span>
<span class="pl-c" style="color:#6a737d">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="pl-c">--&gt;</span></span>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;<span class="pl-ent" style="color:#22863a">requestLimits</span>&nbsp;maxAllowedContentLength=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>2147483648<span class="pl-pds">&quot;</span></span>/&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/<span class="pl-ent" style="color:#22863a">requestFiltering</span>&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/<span class="pl-ent" style="color:#22863a">security</span>&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&lt;/<span class="pl-ent" style="color:#22863a">system</span>.webServer&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&lt;<span class="pl-ent" style="color:#22863a">system</span>.web&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="pl-c" style="color:#6a737d"><span class="pl-c">&lt;!--</span>&nbsp;Maximum&nbsp;value&nbsp;for&nbsp;maxRequestLength&nbsp;(in&nbsp;kilobytes)&nbsp;is&nbsp;2097152&nbsp;(2GB)&nbsp;<span class="pl-c">--&gt;</span></span>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;<span class="pl-ent" style="color:#22863a">httpRuntime</span>&nbsp;maxRequestLength=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>2097152<span class="pl-pds">&quot;</span></span>/&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&lt;/<span class="pl-ent" style="color:#22863a">system</span>.web&gt;
&nbsp;&nbsp;&lt;/<span class="pl-ent" style="color:#22863a">location</span>&gt;</pre>
</div>
</div>
<div>
<h3 style="margin-top:24px; margin-bottom:16px; font-size:1.25em; font-weight:600; line-height:1.25; color:#24292e">
To use FileUltimate in an ASP.NET MVC Project, do the following in Visual Studio:</h3>
<ol style="padding-left:2em; margin-top:0px; margin-bottom:16px; color:#24292e; font-size:16px">
<li>
<p style="margin-top:16px; margin-bottom:16px">Add references to FileUltimate assemblies. There are two ways to perform this: &nbsp;</p>
<ul style="padding-left:2em; margin-top:0px; margin-bottom:0px">
<li>
<p style="margin-top:16px; margin-bottom:16px">Add reference to&nbsp;<span style="font-weight:600">GleamTech.Core.dll</span>&nbsp;and&nbsp;<span style="font-weight:600">GleamTech.FileUltimate.dll</span>&nbsp;found in &quot;Bin&quot; folder of FileUltimate-vX.X.X.X.zip
 package which you already downloaded and extracted. &nbsp;</p>
<blockquote style="margin:0px 0px 16px; padding:0px 1em; color:#6a737d; border-left-width:0.25em; border-left-color:#dfe2e5">
<p style="margin-top:0px; margin-bottom:0px">The other DLLs in the same folder, i.e.&nbsp;<span style="font-weight:600">GleamTech.ImageUltimate.dll</span>,&nbsp;<span style="font-weight:600">GleamTech.VideoUltimate.dll</span>&nbsp;and&nbsp;<span style="font-weight:600">GleamTech.DocumentUltimate.dll</span>&nbsp;are
 assemblies that FileUltimate depends on for some of the features. They are separate assemblies as they are also standalone products with the same names. MSbuild or Visual Studio will automatically copy these 3 DLLs along with the main referenced assembly&nbsp;<span style="font-weight:600">GleamTech.FileUltimate.dll</span>&nbsp;to
 your bin folder during build so they don't need to be referenced directly (unless you are using these products separately in the same project and you have a license for them). Note that even without these 3 DLLs, FileUltimate will work but it will just turn
 off the corresponding features such as generating image or video thumbnails or the document viewer. So with this modular approach, you can opt-out of the features you do not need by excluding the corresponding DLL, i.e. MSBuild or Visual Studio would automatically
 copy a dependency only if that DLL is found in the same folder as the main referenced DLL so you can simply delete/move a DLL to opt-out.</p>
</blockquote>
</li><li style="margin-top:0.25em">
<p style="margin-top:16px; margin-bottom:16px">Or install NuGet package and add references automatically via NuGet Package Manager in Visual Studio: Go to&nbsp;<span style="font-weight:600">Tools -&gt; NuGet Package Manager -&gt; Package Manager Console</span>&nbsp;and
 run this command:</p>
<p style="margin-top:16px; margin-bottom:16px"><code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">Install-Package FileUltimate -Source https://get.gleamtech.com/nuget/default/</code></p>
<p style="margin-top:16px; margin-bottom:16px">If you prefer using the user interface when working with NuGet, you can also install the package this way:</p>
<ul style="padding-left:2em; margin-top:0px; margin-bottom:0px">
<li>
<p style="margin-top:16px; margin-bottom:16px">&nbsp;GleamTech has its own NuGet feed so first you need to add this feed to be able to find GleamTech's packages. Go to&nbsp;<span style="font-weight:600">Tools -&gt; NuGet Package Manager -&gt; Package Manager
 Settings</span>&nbsp;and then click the&nbsp;<span style="font-weight:600">&#43;</span>&nbsp;button to add a new package source. Enter&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">GleamTech</code>&nbsp;in&nbsp;<span style="font-weight:600">Name</span>&nbsp;field
 and&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">https://get.gleamtech.com/nuget/default/</code>&nbsp;in&nbsp;<span style="font-weight:600">Source</span>field
 and click&nbsp;<span style="font-weight:600">OK</span>.</p>
</li><li style="margin-top:0.25em">
<p style="margin-top:16px; margin-bottom:16px">Go to&nbsp;<span style="font-weight:600">Tools -&gt; NuGet Package Manager -&gt; Manage NuGet Packages for Solution</span>, select&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">GleamTech</code>&nbsp;or&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">All</code>&nbsp;in
 the Package source dropdown on the top right. Now enter&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">FileUltimate</code>&nbsp;in the search field, and click&nbsp;<span style="font-weight:600">Install</span>button
 on the found package.</p>
</li></ul>
</li></ul>
</li><li style="margin-top:0.25em">
<p style="margin-top:16px; margin-bottom:16px">Set FileUltimate's global configuration. For example, you may want to set the license key. Insert some of the following lines (if overriding a default value is required) into the&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">Application_Start</code>&nbsp;method
 of your&nbsp;<span style="font-weight:600">Global.asax.cs</span>:</p>
<div class="highlight highlight-source-cs" style="margin-bottom:16px">
<pre style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; word-wrap:normal; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal"><span class="pl-c" style="color:#6a737d">//Set&nbsp;this&nbsp;property&nbsp;only&nbsp;if&nbsp;you&nbsp;have&nbsp;a&nbsp;valid&nbsp;license&nbsp;key,&nbsp;otherwise&nbsp;do&nbsp;not&nbsp;</span>
<span class="pl-c" style="color:#6a737d">//set&nbsp;it&nbsp;so&nbsp;FileUltimate&nbsp;runs&nbsp;in&nbsp;trial&nbsp;mode.&nbsp;&nbsp;</span>
<span class="pl-en" style="color:#6f42c1">FileUltimateConfiguration.Current.LicenseKey</span>&nbsp;=&nbsp;&quot;QQJDJLJP34...&quot;;</pre>
</div>
<p style="margin-top:16px; margin-bottom:16px">Alternatively you can specify the configuration in&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">&lt;appSettings&gt;</code>&nbsp;tag
 of your Web.config.</p>
<div class="highlight highlight-text-xml" style="margin-bottom:16px">
<pre style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; word-wrap:normal; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal">&lt;<span class="pl-ent" style="color:#22863a">add</span> <span class="pl-e" style="color:#6f42c1">key</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>FileUltimate:LicenseKey<span class="pl-pds">&quot;</span></span> <span class="pl-e" style="color:#6f42c1">value</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>QQJDJLJP34...<span class="pl-pds">&quot;</span></span> /&gt; </pre>
</div>
<p style="margin-top:16px; margin-bottom:16px">As you would notice,&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">FileUltimate:</code>&nbsp;prefix maps to&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">FileUltimateConfiguration.Current</code>.
 &nbsp;</p>
</li><li style="margin-top:0.25em">
<p style="margin-top:16px; margin-bottom:16px">Open one of your View pages (eg. Index.cshtml) and at the top of your page add the necessary namespaces:</p>
<div class="highlight highlight-source-cs" style="margin-bottom:16px">
<pre style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; word-wrap:normal; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal">@<span class="pl-k" style="color:#d73a49">using</span>&nbsp;<span class="pl-en" style="color:#6f42c1">GleamTech.AspNet.Mvc</span>
@<span class="pl-k" style="color:#d73a49">using</span>&nbsp;<span class="pl-en" style="color:#6f42c1">GleamTech.FileUltimate</span></pre>
</div>
<p style="margin-top:16px; margin-bottom:16px">Alternatively you can add the namespaces globally in&nbsp;<span style="font-weight:600">Views/Web.config</span>&nbsp;under&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">&lt;system.web.webPages.razor&gt;/&lt;pages&gt;/&lt;namespaces&gt;</code>&nbsp;tag
 to avoid adding namespaces in your pages every time:</p>
<div class="highlight highlight-text-xml" style="margin-bottom:16px">
<pre style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; word-wrap:normal; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal">&lt;<span class="pl-ent" style="color:#22863a">add</span> <span class="pl-e" style="color:#6f42c1">namespace</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>GleamTech.AspNet.Mvc<span class="pl-pds">&quot;</span></span> /&gt;
&lt;<span class="pl-ent" style="color:#22863a">add</span> <span class="pl-e" style="color:#6f42c1">namespace</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>GleamTech.FileUltimate<span class="pl-pds">&quot;</span></span> /&gt;</pre>
</div>
<p style="margin-top:16px; margin-bottom:16px">Now in your page insert these lines:</p>
<div class="highlight highlight-source-cs" style="margin-bottom:16px">
<pre style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; word-wrap:normal; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal">&lt;!DOCTYPE html&gt;
@{
    <span class="pl-k" style="color:#d73a49">var</span> <span class="pl-en" style="color:#6f42c1">fileManager </span>= <span class="pl-k" style="color:#d73a49">new</span> <span class="pl-en" style="color:#6f42c1">FileManager</span>
    {
        Width = <span class="pl-c1" style="color:#005cc5">800</span>,
        Height = <span class="pl-c1" style="color:#005cc5">600</span>,
        Resizable = <span class="pl-c1" style="color:#005cc5">true</span>
    };

    <span class="pl-k" style="color:#d73a49">var</span> <span class="pl-en" style="color:#6f42c1">rootFolder </span>= <span class="pl-k" style="color:#d73a49">new</span> <span class="pl-en" style="color:#6f42c1">FileManagerRootFolder</span>
    {
        Name = <span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>A Root Folder<span class="pl-pds">&quot;</span></span>,
        Location = <span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>~/App_Data/RootFolder1<span class="pl-pds">&quot;</span></span>
    };

    rootFolder.AccessControls.Add(<span class="pl-k" style="color:#d73a49">new</span> <span class="pl-en" style="color:#6f42c1">FileManagerAccessControl</span>
    {
        Path = <span class="pl-s" style="color:#032f62">@&quot;\&quot;</span>,
        AllowedPermissions = FileManagerPermissions.Full
    });

    fileManager.RootFolders.Add(rootFolder);
}
&lt;<span class="pl-en" style="color:#6f42c1">html</span>&gt;
&lt;html&gt;
    &lt;head&gt;
        &lt;title&gt;File Manager&lt;/title&gt;
        @this.<span class="pl-en" style="color:#6f42c1">RenderHead</span>(fileManager)
    &lt;/head&gt;
    &lt;body&gt;
        @this.<span class="pl-en" style="color:#6f42c1">RenderBody</span>(fileManager)
    &lt;/body&gt;
&lt;/html&gt;</pre>
</div>
<p style="margin-top:16px; margin-bottom:16px">This will render a file manager control in the page which displays one root folder named &quot;A Root Folder&quot; which points to &quot;~/App_Data/RootFolder1&quot; with Full permissions.</p>
</li></ol>
<h3 style="margin-top:24px; margin-bottom:16px; font-size:1.25em; font-weight:600; line-height:1.25; color:#24292e">
<a id="user-content-to-use-fileultimate-in-an-aspnet-webforms-project-do-the-following-in-visual-studio" class="anchor" href="https://github.com/GleamTech/FileUltimate#to-use-fileultimate-in-an-aspnet-webforms-project-do-the-following-in-visual-studio" style="background-color:transparent; color:#0366d6; float:left; padding-right:4px; margin-left:-20px; line-height:1"></a>To
 use FileUltimate in an ASP.NET WebForms Project, do the following in Visual Studio:</h3>
<ol style="padding-left:2em; margin-top:0px; margin-bottom:16px; color:#24292e; font-size:16px">
<li>
<p style="margin-top:16px; margin-bottom:16px">Add references to FileUltimate assemblies. There are two ways to perform this: &nbsp;</p>
<ul style="padding-left:2em; margin-top:0px; margin-bottom:0px">
<li>
<p style="margin-top:16px; margin-bottom:16px">Add reference to&nbsp;<span style="font-weight:600">GleamTech.Core.dll</span>&nbsp;and&nbsp;<span style="font-weight:600">GleamTech.FileUltimate.dll</span>&nbsp;found in &quot;Bin&quot; folder of FileUltimate-vX.X.X.X.zip
 package which you already downloaded and extracted. &nbsp;</p>
<blockquote style="margin:0px 0px 16px; padding:0px 1em; color:#6a737d; border-left-width:0.25em; border-left-color:#dfe2e5">
<p style="margin-top:0px; margin-bottom:0px">The other DLLs in the same folder, i.e.&nbsp;<span style="font-weight:600">GleamTech.ImageUltimate.dll</span>,&nbsp;<span style="font-weight:600">GleamTech.VideoUltimate.dll</span>&nbsp;and&nbsp;<span style="font-weight:600">GleamTech.DocumentUltimate.dll</span>&nbsp;are
 assemblies that FileUltimate depends on for some of the features. They are separate assemblies as they are also standalone products with the same names. MSbuild or Visual Studio will automatically copy these 3 DLLs along with the main referenced assembly&nbsp;<span style="font-weight:600">GleamTech.FileUltimate.dll</span>&nbsp;to
 your bin folder during build so they don't need to be referenced directly (unless you are using these products separately in the same project and you have a license for them). Note that even without these 3 DLLs, FileUltimate will work but it will just turn
 off the corresponding features such as generating image or video thumbnails or the document viewer. So with this modular approach, you can opt-out of the features you do not need by excluding the corresponding DLL, i.e. MSBuild or Visual Studio would automatically
 copy a dependency only if that DLL is found in the same folder as the main referenced DLL so you can simply delete/move a DLL to opt-out.</p>
</blockquote>
</li><li style="margin-top:0.25em">
<p style="margin-top:16px; margin-bottom:16px">Or install NuGet package and add references automatically via NuGet Package Manager in Visual Studio: Go to&nbsp;<span style="font-weight:600">Tools -&gt; NuGet Package Manager -&gt; Package Manager Console</span>&nbsp;and
 run this command:</p>
<p style="margin-top:16px; margin-bottom:16px"><code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">Install-Package FileUltimate -Source https://get.gleamtech.com/nuget/default/</code></p>
<p style="margin-top:16px; margin-bottom:16px">If you prefer using the user interface when working with NuGet, you can also install the package this way:</p>
<ul style="padding-left:2em; margin-top:0px; margin-bottom:0px">
<li>
<p style="margin-top:16px; margin-bottom:16px">&nbsp;GleamTech has its own NuGet feed so first you need to add this feed to be able to find GleamTech's packages. Go to&nbsp;<span style="font-weight:600">Tools -&gt; NuGet Package Manager -&gt; Package Manager
 Settings</span>&nbsp;and then click the&nbsp;<span style="font-weight:600">&#43;</span>&nbsp;button to add a new package source. Enter&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">GleamTech</code>&nbsp;in&nbsp;<span style="font-weight:600">Name</span>&nbsp;field
 and&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">https://get.gleamtech.com/nuget/default/</code>&nbsp;in&nbsp;<span style="font-weight:600">Source</span>field
 and click&nbsp;<span style="font-weight:600">OK</span>.</p>
</li><li style="margin-top:0.25em">
<p style="margin-top:16px; margin-bottom:16px">Go to&nbsp;<span style="font-weight:600">Tools -&gt; NuGet Package Manager -&gt; Manage NuGet Packages for Solution</span>, select&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">GleamTech</code>&nbsp;or&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">All</code>&nbsp;in
 the Package source dropdown on the top right. Now enter&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">FileUltimate</code>&nbsp;in the search field, and click&nbsp;<span style="font-weight:600">Install</span>button
 on the found package.</p>
</li></ul>
</li></ul>
</li><li style="margin-top:0.25em">
<p style="margin-top:16px; margin-bottom:16px">Set FileUltimate's global configuration. For example, you may want to set the license key. Insert some of the following lines (if overriding a default value is required) into the&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">Application_Start</code>&nbsp;method
 of your&nbsp;<span style="font-weight:600">Global.asax.cs</span>:</p>
<div class="highlight highlight-source-cs" style="margin-bottom:16px">
<pre style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; word-wrap:normal; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal"><span class="pl-c" style="color:#6a737d">//Set&nbsp;this&nbsp;property&nbsp;only&nbsp;if&nbsp;you&nbsp;have&nbsp;a&nbsp;valid&nbsp;license&nbsp;key,&nbsp;otherwise&nbsp;do&nbsp;not&nbsp;</span>
<span class="pl-c" style="color:#6a737d">//set&nbsp;it&nbsp;so&nbsp;FileUltimate&nbsp;runs&nbsp;in&nbsp;trial&nbsp;mode.&nbsp;&nbsp;</span>
<span class="pl-en" style="color:#6f42c1">FileUltimateConfiguration.Current.LicenseKey</span>&nbsp;=&nbsp;&quot;QQJDJLJP34...&quot;;</pre>
</div>
<p style="margin-top:16px; margin-bottom:16px">Alternatively you can specify the configuration in&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">&lt;appSettings&gt;</code>&nbsp;tag
 of your Web.config.</p>
<div class="highlight highlight-text-xml" style="margin-bottom:16px">
<pre style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; word-wrap:normal; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal">&lt;<span class="pl-ent" style="color:#22863a">add</span> <span class="pl-e" style="color:#6f42c1">key</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>FileUltimate:LicenseKey<span class="pl-pds">&quot;</span></span> <span class="pl-e" style="color:#6f42c1">value</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>QQJDJLJP34...<span class="pl-pds">&quot;</span></span> /&gt; </pre>
</div>
<p style="margin-top:16px; margin-bottom:16px">As you would notice,&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">FileUltimate:</code>&nbsp;prefix maps to&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">FileUltimateConfiguration.Current</code>.
 &nbsp;</p>
</li><li style="margin-top:0.25em">
<p style="margin-top:16px; margin-bottom:16px">Open one of your pages (eg. Default.aspx) and at the top of your page add add the necessary namespaces:</p>
<div class="highlight highlight-text-html-asp" style="margin-bottom:16px">
<pre style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; word-wrap:normal; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal"><span class="pl-s1"><span class="pl-pse">&lt;%</span>@&nbsp;Register&nbsp;TagPrefix<span class="pl-k" style="color:#d73a49">=</span><span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>GleamTech<span class="pl-pds">&quot;</span></span>&nbsp;Namespace<span class="pl-k" style="color:#d73a49">=</span><span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>GleamTech.FileUltimate<span class="pl-pds">&quot;</span></span>&nbsp;Assembly<span class="pl-k" style="color:#d73a49">=</span><span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>GleamTech.FileUltimate<span class="pl-pds">&quot;</span></span>&nbsp;<span class="pl-pse">%&gt;</span></span></pre>
</div>
<p style="margin-top:16px; margin-bottom:16px">Alternatively you can add the namespaces globally in&nbsp;<span style="font-weight:600">Web.config</span>&nbsp;under&nbsp;<code style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; padding:0.2em 0.4em; margin:0px">&lt;system.web&gt;/&lt;pages&gt;/&lt;controls&gt;</code>&nbsp;tag
 to avoid adding namespaces in your pages every time:</p>
<div class="highlight highlight-text-xml" style="margin-bottom:16px">
<pre style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; word-wrap:normal; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal">&lt;<span class="pl-ent" style="color:#22863a">add</span> <span class="pl-e" style="color:#6f42c1">tagPrefix</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>GleamTech<span class="pl-pds">&quot;</span></span> <span class="pl-e" style="color:#6f42c1">namespace</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>GleamTech.FileUltimate<span class="pl-pds">&quot;</span></span> <span class="pl-e" style="color:#6f42c1">assembly</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>GleamTech.FileUltimate<span class="pl-pds">&quot;</span></span> /&gt;</pre>
</div>
<p style="margin-top:16px; margin-bottom:16px">Now in your page insert these lines:</p>
<div class="highlight highlight-text-html-asp" style="margin-bottom:16px">
<pre style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; word-wrap:normal; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal">&lt;!DOCTYPE html&gt;
&lt;<span class="pl-ent" style="color:#22863a">html</span>&gt;
    &lt;<span class="pl-ent" style="color:#22863a">head</span> <span class="pl-e" style="color:#6f42c1">runat</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>server<span class="pl-pds">&quot;</span></span>&gt;
        &lt;<span class="pl-ent" style="color:#22863a">title</span>&gt;Document Viewer&lt;/<span class="pl-ent" style="color:#22863a">title</span>&gt;
    &lt;/<span class="pl-ent" style="color:#22863a">head</span>&gt;
    &lt;<span class="pl-ent" style="color:#22863a">body</span>&gt;
        &lt;<span class="pl-ent" style="color:#22863a">GleamTech:FileManagerControl</span> <span class="pl-e" style="color:#6f42c1">ID</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>fileManager<span class="pl-pds">&quot;</span></span> <span class="pl-e" style="color:#6f42c1">runat</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>server<span class="pl-pds">&quot;</span></span> 
                                <span class="pl-e" style="color:#6f42c1">Width</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>800<span class="pl-pds">&quot;</span></span>
                                <span class="pl-e" style="color:#6f42c1">Height</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>600<span class="pl-pds">&quot;</span></span> 
                                <span class="pl-e" style="color:#6f42c1">Resizable</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>True<span class="pl-pds">&quot;</span></span>&gt;
            
            &lt;<span class="pl-ent" style="color:#22863a">GleamTech:FileManagerRootFolder</span> <span class="pl-e" style="color:#6f42c1">Name</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>A Root Folder<span class="pl-pds">&quot;</span></span> <span class="pl-e" style="color:#6f42c1">Location</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>~/App_Data/RootFolder1<span class="pl-pds">&quot;</span></span> &gt; 
                &lt;<span class="pl-ent" style="color:#22863a">GleamTech:FileManagerAccessControl</span> <span class="pl-e" style="color:#6f42c1">Path</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>\<span class="pl-pds">&quot;</span></span> <span class="pl-e" style="color:#6f42c1">AllowedPermissions</span>=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>Full<span class="pl-pds">&quot;</span></span>/&gt; 
            &lt;/<span class="pl-ent" style="color:#22863a">GleamTech:FileManagerRootFolder</span>&gt;

        &lt;/<span class="pl-ent" style="color:#22863a">GleamTech:FileManagerControl</span>&gt; 
    &lt;/<span class="pl-ent" style="color:#22863a">body</span>&gt;
&lt;/<span class="pl-ent" style="color:#22863a">html</span>&gt;</pre>
</div>
<p style="margin-top:16px; margin-bottom:16px">This will render a file manager control in the page which displays one root folder named &quot;A Root Folder&quot; which points to &quot;~/App_Data/RootFolder1&quot; with Full permissions.</p>
</li></ol>
<h3 style="margin-top:24px; margin-bottom:16px; font-size:1.25em; font-weight:600; line-height:1.25; color:#24292e">
<a id="user-content-optional" class="anchor" href="https://github.com/GleamTech/FileUltimate#optional" style="background-color:transparent; color:#0366d6; float:left; padding-right:4px; margin-left:-20px; line-height:1"></a>Optional:</h3>
<p style="margin-top:0px; margin-bottom:16px; color:#24292e; font-size:16px">FileUltimate does not depend on any Web.config settings to work (it's config-free for easy deployment).&nbsp;However if you want to support the lowest level upload method Html4 which
 is the only possible method&nbsp;for old browsers without Html5 or Flash or Silverlight support, then&nbsp;you will need to&nbsp;increase the request limits (ASP.NET's default is 4MB) so that you can upload&nbsp;files larger than 4MB on these browsers. Edit
 your project's Web.config file and add the following settings inside &lt;configuration&gt; tag: &nbsp;</p>
<div class="highlight highlight-text-xml" style="margin-bottom:16px; color:#24292e; font-size:16px">
<pre style="font-family:SFMono-Regular,Consolas,&quot;Liberation Mono&quot;,Menlo,Courier,monospace; font-size:13.6px; margin-top:0px; margin-bottom:0px; word-wrap:normal; padding:16px; overflow:auto; line-height:1.45; background-color:#f6f8fa; word-break:normal">&nbsp;&nbsp;<span class="pl-c" style="color:#6a737d"><span class="pl-c">&lt;!--</span>&nbsp;</span>
<span class="pl-c" style="color:#6a737d">&nbsp;&nbsp;&nbsp;&nbsp;Html4&nbsp;upload&nbsp;method&nbsp;requires&nbsp;the&nbsp;limits&nbsp;to&nbsp;be&nbsp;set&nbsp;to&nbsp;the&nbsp;maximum&nbsp;value&nbsp;(2&nbsp;GB).</span>
<span class="pl-c" style="color:#6a737d">&nbsp;&nbsp;&nbsp;&nbsp;Other&nbsp;upload&nbsp;methods&nbsp;use&nbsp;chunking&nbsp;so&nbsp;there&nbsp;is&nbsp;no&nbsp;2GB&nbsp;limit&nbsp;for&nbsp;them.</span>
<span class="pl-c" style="color:#6a737d">&nbsp;&nbsp;<span class="pl-c">--&gt;</span></span>
&nbsp;&nbsp;&lt;<span class="pl-ent" style="color:#22863a">location</span>&nbsp;path=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>fileuploader.ashx<span class="pl-pds">&quot;</span></span>&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&lt;<span class="pl-ent" style="color:#22863a">system</span>.webServer&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;<span class="pl-ent" style="color:#22863a">security</span>&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;<span class="pl-ent" style="color:#22863a">requestFiltering</span>&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="pl-c" style="color:#6a737d"><span class="pl-c">&lt;!--</span>&nbsp;</span>
<span class="pl-c" style="color:#6a737d">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Maximum&nbsp;value&nbsp;for&nbsp;maxAllowedContentLength&nbsp;(in&nbsp;bytes)&nbsp;is&nbsp;2147483648&nbsp;(2GB).&nbsp;</span>
<span class="pl-c" style="color:#6a737d">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;maxAllowedContentLength&nbsp;should&nbsp;be&nbsp;always&nbsp;equal&nbsp;to&nbsp;(or&nbsp;greater&nbsp;than)&nbsp;maxRequestLength&nbsp;x&nbsp;1024.</span>
<span class="pl-c" style="color:#6a737d">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="pl-c">--&gt;</span></span>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;<span class="pl-ent" style="color:#22863a">requestLimits</span>&nbsp;maxAllowedContentLength=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>2147483648<span class="pl-pds">&quot;</span></span>/&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/<span class="pl-ent" style="color:#22863a">requestFiltering</span>&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/<span class="pl-ent" style="color:#22863a">security</span>&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&lt;/<span class="pl-ent" style="color:#22863a">system</span>.webServer&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&lt;<span class="pl-ent" style="color:#22863a">system</span>.web&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="pl-c" style="color:#6a737d"><span class="pl-c">&lt;!--</span>&nbsp;Maximum&nbsp;value&nbsp;for&nbsp;maxRequestLength&nbsp;(in&nbsp;kilobytes)&nbsp;is&nbsp;2097152&nbsp;(2GB)&nbsp;<span class="pl-c">--&gt;</span></span>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;<span class="pl-ent" style="color:#22863a">httpRuntime</span>&nbsp;maxRequestLength=<span class="pl-s" style="color:#032f62"><span class="pl-pds">&quot;</span>2097152<span class="pl-pds">&quot;</span></span>/&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&lt;/<span class="pl-ent" style="color:#22863a">system</span>.web&gt;
&nbsp;&nbsp;&lt;/<span class="pl-ent" style="color:#22863a">location</span>&gt;</pre>
</div>
</div>
