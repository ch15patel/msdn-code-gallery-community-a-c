# Azure Automation Using .Net Nugget and Powershell
## Requires
- Visual Studio 2013
## License
- MIT
## Technologies
- Azure Automation
## Topics
- Azure Automation
## Updated
- 01/26/2015
## Description

<h2><a name="what-is-azure-automation"></a>What is Azure Automation?</h2>
<p>Microsoft Azure Automation provides a way for users to automate the manual, long-running, error-prone, and frequently repeated tasks that are commonly performed in a cloud environment. You can create, monitor, manage, and deploy resources in your Azure environment
 using runbooks, which are based on Windows PowerShell workflows.&nbsp;</p>
<p>For detailed steps fo creating Azure Automation account and runbook using azure management portal , please see below link</p>
<p><a href="http://azure.microsoft.com/en-us/documentation/articles/automation-create-runbook-from-samples/#automationaccount">http://azure.microsoft.com/en-us/documentation/articles/automation-create-runbook-from-samples/#automationaccount</a></p>
<p>Below we will see how to do the same using Azure Automation Nugget&nbsp;</p>
<p><a href="https://www.nuget.org/packages/Microsoft.Azure.Management.Automation/">https://www.nuget.org/packages/Microsoft.Azure.Management.Automation/</a></p>
<h1><span>Building the Sample</span></h1>
<p><em>Create a C# Console Application and using Package Console add below nuget:</em></p>
<p>PM&gt; Install-Package Microsoft.Azure.Management.Automation -Pre<em> &nbsp;</em></p>
<p>then add below code to program.cs</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">csharp</span>
<pre class="hidden">public static void CreateAutomationRunbook()
        {
            try
            {
                Microsoft.Azure.SubscriptionCloudCredentials creds;
                creds = CertificateAuthenticationHelper.GetCredentials(ConfigurationManager.AppSettings[&quot;SubscriptionID&quot;], ConfigurationManager.AppSettings[&quot;Certificate&quot;]);
                AutomationManagementClient automationClient = new AutomationManagementClient(creds);
                //Create Runbook
                FileStream fs = new FileStream(AzureAutomationSchema.ScriptFileLocation, FileMode.Open, FileAccess.Read);
                // Get Runbook Response
                var runbookversion = automationClient.RunbookVersions.Create(AzureAutomationSchema.automationAccount, fs);
                Trace.TraceInformation(&quot;Status of RunbookVersion Create request:&quot; &#43; runbookversion.StatusCode.ToString() &#43; &quot;.RunbookVersionId &quot; &#43; runbookversion.RunbookVersion.Id &#43; &quot;  Created.&quot;);

                var runbook = automationClient.Runbooks.ListByName(AzureAutomationSchema.automationAccount, AzureAutomationSchema.runbookname);

                // Get Runbook Publish Response
                Microsoft.Azure.Management.Automation.Models.RunbookPublishResponse pubresponse = automationClient.Runbooks.Publish(AzureAutomationSchema.automationAccount, new Microsoft.Azure.Management.Automation.Models.RunbookPublishParameters(runbook.Runbooks[0].Id, &quot;Joe&quot;));
                Trace.TraceInformation(&quot;Status of RunbookPublish request:&quot; &#43; pubresponse.StatusCode.ToString() &#43; &quot;. PublishedRunbookVersionId &quot; &#43; pubresponse.PublishedRunbookVersionId &#43; &quot;  Created.&quot;);

                Microsoft.Azure.Management.Automation.Models.Schedule RuleEngineSchedule = new Microsoft.Azure.Management.Automation.Models.Schedule();
                //Define Automation Schedule
                Microsoft.Azure.Management.Automation.Models.ScheduleCreateParameters scheduleParam = new Microsoft.Azure.Management.Automation.Models.ScheduleCreateParameters();
                scheduleParam.Schedule = RuleEngineSchedule;
                scheduleParam.Schedule.Description = AzureAutomationSchema.ScheduleDescription;
                scheduleParam.Schedule.StartTime = AzureAutomationSchema.ScheduleStartTime;
                scheduleParam.Schedule.IsEnabled = AzureAutomationSchema.ScheduleIsEnabled;
                scheduleParam.Schedule.DayInterval = AzureAutomationSchema.ScheduleDayInterval;
                scheduleParam.Schedule.Name = AzureAutomationSchema.ScheduleName;
                if (AzureAutomationSchema.ScheduleScheduleType == &quot;DailySchedule&quot;)
                {
                    scheduleParam.Schedule.ScheduleType = Microsoft.Azure.Management.Automation.Models.ScheduleType.DailySchedule;
                }
                if (AzureAutomationSchema.ScheduleScheduleType == &quot;HourlySchedule&quot;)
                {
                    scheduleParam.Schedule.ScheduleType = Microsoft.Azure.Management.Automation.Models.ScheduleType.HourlySchedule;
                }
                scheduleParam.Schedule.ExpiryTime = AzureAutomationSchema.ScheduleExpiryTime;
                // Get RunbookSchedule  response
                var response = automationClient.Schedules.Create(AzureAutomationSchema.automationAccount, scheduleParam);
                Trace.TraceInformation(&quot;Status of Schedule request:&quot; &#43; response.StatusCode.ToString() &#43; &quot;. &quot; &#43; response.Schedule.Name &#43; &quot;  Created.&quot;);

                Microsoft.Azure.Management.Automation.Models.RunbookCreateScheduleLinkParameters RuleEngineScheduleLink = new Microsoft.Azure.Management.Automation.Models.RunbookCreateScheduleLinkParameters();
                RuleEngineScheduleLink.RunbookId = runbook.Runbooks[0].Id;
                RuleEngineScheduleLink.ScheduleId = response.Schedule.Id;

                //Adding Parameters to Automation Schedule
                foreach (var param in ConfigurationManager.AppSettings.AllKeys.Where(key =&gt; key.StartsWith(&quot;Param&quot;)))
                {
                    RuleEngineScheduleLink.Parameters.Add(AddParametersToScheduleLink(param.Replace(&quot;Param&quot;, &quot;&quot;), ConfigurationManager.AppSettings[param]));
                }

                // Get RunbookSchedule link response
                Microsoft.Azure.Management.Automation.Models.RunbookCreateScheduleLinkResponse RuleEngineScheduleLinkResponse = automationClient.Runbooks.CreateScheduleLink(AzureAutomationSchema.automationAccount, RuleEngineScheduleLink);
                Trace.TraceInformation(&quot;Status of ScheduleLink request:&quot; &#43; RuleEngineScheduleLinkResponse.StatusCode.ToString() &#43; &quot;. JobContextID &quot; &#43; RuleEngineScheduleLinkResponse.JobContextId &#43; &quot;  Created.&quot;);
            }
            catch(Exception ex)
            {
                Trace.TraceError(ex.Message);
                throw ex;
            }
        }

        // Adding Azure Schedule Link Parameters
        public static Microsoft.Azure.Management.Automation.Models.NameValuePair AddParametersToScheduleLink(string Key, string Value)
        {
            Microsoft.Azure.Management.Automation.Models.NameValuePair param1 = new Microsoft.Azure.Management.Automation.Models.NameValuePair();
            param1.Name = Key;
            param1.Value = Value;
            return param1;


        }</pre>
<div class="preview">
<pre class="csharp"><span class="cs__keyword">public</span>&nbsp;<span class="cs__keyword">static</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;CreateAutomationRunbook()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">try</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Microsoft.Azure.SubscriptionCloudCredentials&nbsp;creds;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;creds&nbsp;=&nbsp;CertificateAuthenticationHelper.GetCredentials(ConfigurationManager.AppSettings[<span class="cs__string">&quot;SubscriptionID&quot;</span>],&nbsp;ConfigurationManager.AppSettings[<span class="cs__string">&quot;Certificate&quot;</span>]);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AutomationManagementClient&nbsp;automationClient&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;AutomationManagementClient(creds);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//Create&nbsp;Runbook</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FileStream&nbsp;fs&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;FileStream(AzureAutomationSchema.ScriptFileLocation,&nbsp;FileMode.Open,&nbsp;FileAccess.Read);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Get&nbsp;Runbook&nbsp;Response</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;runbookversion&nbsp;=&nbsp;automationClient.RunbookVersions.Create(AzureAutomationSchema.automationAccount,&nbsp;fs);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Trace.TraceInformation(<span class="cs__string">&quot;Status&nbsp;of&nbsp;RunbookVersion&nbsp;Create&nbsp;request:&quot;</span>&nbsp;&#43;&nbsp;runbookversion.StatusCode.ToString()&nbsp;&#43;&nbsp;<span class="cs__string">&quot;.RunbookVersionId&nbsp;&quot;</span>&nbsp;&#43;&nbsp;runbookversion.RunbookVersion.Id&nbsp;&#43;&nbsp;<span class="cs__string">&quot;&nbsp;&nbsp;Created.&quot;</span>);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;runbook&nbsp;=&nbsp;automationClient.Runbooks.ListByName(AzureAutomationSchema.automationAccount,&nbsp;AzureAutomationSchema.runbookname);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Get&nbsp;Runbook&nbsp;Publish&nbsp;Response</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Microsoft.Azure.Management.Automation.Models.RunbookPublishResponse&nbsp;pubresponse&nbsp;=&nbsp;automationClient.Runbooks.Publish(AzureAutomationSchema.automationAccount,&nbsp;<span class="cs__keyword">new</span>&nbsp;Microsoft.Azure.Management.Automation.Models.RunbookPublishParameters(runbook.Runbooks[<span class="cs__number">0</span>].Id,&nbsp;<span class="cs__string">&quot;Joe&quot;</span>));&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Trace.TraceInformation(<span class="cs__string">&quot;Status&nbsp;of&nbsp;RunbookPublish&nbsp;request:&quot;</span>&nbsp;&#43;&nbsp;pubresponse.StatusCode.ToString()&nbsp;&#43;&nbsp;<span class="cs__string">&quot;.&nbsp;PublishedRunbookVersionId&nbsp;&quot;</span>&nbsp;&#43;&nbsp;pubresponse.PublishedRunbookVersionId&nbsp;&#43;&nbsp;<span class="cs__string">&quot;&nbsp;&nbsp;Created.&quot;</span>);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Microsoft.Azure.Management.Automation.Models.Schedule&nbsp;RuleEngineSchedule&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;Microsoft.Azure.Management.Automation.Models.Schedule();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//Define&nbsp;Automation&nbsp;Schedule</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Microsoft.Azure.Management.Automation.Models.ScheduleCreateParameters&nbsp;scheduleParam&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;Microsoft.Azure.Management.Automation.Models.ScheduleCreateParameters();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;scheduleParam.Schedule&nbsp;=&nbsp;RuleEngineSchedule;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;scheduleParam.Schedule.Description&nbsp;=&nbsp;AzureAutomationSchema.ScheduleDescription;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;scheduleParam.Schedule.StartTime&nbsp;=&nbsp;AzureAutomationSchema.ScheduleStartTime;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;scheduleParam.Schedule.IsEnabled&nbsp;=&nbsp;AzureAutomationSchema.ScheduleIsEnabled;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;scheduleParam.Schedule.DayInterval&nbsp;=&nbsp;AzureAutomationSchema.ScheduleDayInterval;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;scheduleParam.Schedule.Name&nbsp;=&nbsp;AzureAutomationSchema.ScheduleName;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(AzureAutomationSchema.ScheduleScheduleType&nbsp;==&nbsp;<span class="cs__string">&quot;DailySchedule&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;scheduleParam.Schedule.ScheduleType&nbsp;=&nbsp;Microsoft.Azure.Management.Automation.Models.ScheduleType.DailySchedule;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(AzureAutomationSchema.ScheduleScheduleType&nbsp;==&nbsp;<span class="cs__string">&quot;HourlySchedule&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;scheduleParam.Schedule.ScheduleType&nbsp;=&nbsp;Microsoft.Azure.Management.Automation.Models.ScheduleType.HourlySchedule;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;scheduleParam.Schedule.ExpiryTime&nbsp;=&nbsp;AzureAutomationSchema.ScheduleExpiryTime;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Get&nbsp;RunbookSchedule&nbsp;&nbsp;response</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;response&nbsp;=&nbsp;automationClient.Schedules.Create(AzureAutomationSchema.automationAccount,&nbsp;scheduleParam);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Trace.TraceInformation(<span class="cs__string">&quot;Status&nbsp;of&nbsp;Schedule&nbsp;request:&quot;</span>&nbsp;&#43;&nbsp;response.StatusCode.ToString()&nbsp;&#43;&nbsp;<span class="cs__string">&quot;.&nbsp;&quot;</span>&nbsp;&#43;&nbsp;response.Schedule.Name&nbsp;&#43;&nbsp;<span class="cs__string">&quot;&nbsp;&nbsp;Created.&quot;</span>);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Microsoft.Azure.Management.Automation.Models.RunbookCreateScheduleLinkParameters&nbsp;RuleEngineScheduleLink&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;Microsoft.Azure.Management.Automation.Models.RunbookCreateScheduleLinkParameters();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;RuleEngineScheduleLink.RunbookId&nbsp;=&nbsp;runbook.Runbooks[<span class="cs__number">0</span>].Id;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;RuleEngineScheduleLink.ScheduleId&nbsp;=&nbsp;response.Schedule.Id;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//Adding&nbsp;Parameters&nbsp;to&nbsp;Automation&nbsp;Schedule</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">foreach</span>&nbsp;(var&nbsp;param&nbsp;<span class="cs__keyword">in</span>&nbsp;ConfigurationManager.AppSettings.AllKeys.Where(key&nbsp;=&gt;&nbsp;key.StartsWith(<span class="cs__string">&quot;Param&quot;</span>)))&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;RuleEngineScheduleLink.Parameters.Add(AddParametersToScheduleLink(param.Replace(<span class="cs__string">&quot;Param&quot;</span>,&nbsp;<span class="cs__string">&quot;&quot;</span>),&nbsp;ConfigurationManager.AppSettings[param]));&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Get&nbsp;RunbookSchedule&nbsp;link&nbsp;response</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Microsoft.Azure.Management.Automation.Models.RunbookCreateScheduleLinkResponse&nbsp;RuleEngineScheduleLinkResponse&nbsp;=&nbsp;automationClient.Runbooks.CreateScheduleLink(AzureAutomationSchema.automationAccount,&nbsp;RuleEngineScheduleLink);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Trace.TraceInformation(<span class="cs__string">&quot;Status&nbsp;of&nbsp;ScheduleLink&nbsp;request:&quot;</span>&nbsp;&#43;&nbsp;RuleEngineScheduleLinkResponse.StatusCode.ToString()&nbsp;&#43;&nbsp;<span class="cs__string">&quot;.&nbsp;JobContextID&nbsp;&quot;</span>&nbsp;&#43;&nbsp;RuleEngineScheduleLinkResponse.JobContextId&nbsp;&#43;&nbsp;<span class="cs__string">&quot;&nbsp;&nbsp;Created.&quot;</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">catch</span>(Exception&nbsp;ex)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Trace.TraceError(ex.Message);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">throw</span>&nbsp;ex;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Adding&nbsp;Azure&nbsp;Schedule&nbsp;Link&nbsp;Parameters</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">public</span>&nbsp;<span class="cs__keyword">static</span>&nbsp;Microsoft.Azure.Management.Automation.Models.NameValuePair&nbsp;AddParametersToScheduleLink(<span class="cs__keyword">string</span>&nbsp;Key,&nbsp;<span class="cs__keyword">string</span>&nbsp;Value)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Microsoft.Azure.Management.Automation.Models.NameValuePair&nbsp;param1&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;Microsoft.Azure.Management.Automation.Models.NameValuePair();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;param1.Name&nbsp;=&nbsp;Key;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;param1.Value&nbsp;=&nbsp;Value;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">return</span>&nbsp;param1;&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</pre>
</div>
</div>
</div>
<pre>Now as we can see to connect to azure subscription we are using Microsoft.Azure.SubscriptionCloudCredentials hence add below class to work with Azure Subscription using management certificate:</pre>
<pre><div class="scriptcode"><div class="pluginEditHolder" pluginCommand="mceScriptCode"><div class="title"><span>C#</span></div><div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div><span class="hidden">csharp</span><pre class="hidden">using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Security.Cryptography.X509Certificates;
using Microsoft.Azure;

namespace AzureAPILibrary
{
    internal class CertificateAuthenticationHelper
    {
        internal static SubscriptionCloudCredentials GetCredentials(string subscriptionId,string base64encodedcert)
        {
            return new CertificateCloudCredentials(subscriptionId, new X509Certificate2(Convert.FromBase64String(base64encodedcert)));
        }
    }
}
</pre>
<div class="preview">
<pre class="csharp"><span class="cs__keyword">using</span>&nbsp;System;&nbsp;
<span class="cs__keyword">using</span>&nbsp;System.Collections.Generic;&nbsp;
<span class="cs__keyword">using</span>&nbsp;System.Linq;&nbsp;
<span class="cs__keyword">using</span>&nbsp;System.Text;&nbsp;
<span class="cs__keyword">using</span>&nbsp;System.Threading.Tasks;&nbsp;
<span class="cs__keyword">using</span>&nbsp;System.Security.Cryptography.X509Certificates;&nbsp;
<span class="cs__keyword">using</span>&nbsp;Microsoft.Azure;&nbsp;
&nbsp;
<span class="cs__keyword">namespace</span>&nbsp;AzureAPILibrary&nbsp;
{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">internal</span>&nbsp;<span class="cs__keyword">class</span>&nbsp;CertificateAuthenticationHelper&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">internal</span>&nbsp;<span class="cs__keyword">static</span>&nbsp;SubscriptionCloudCredentials&nbsp;GetCredentials(<span class="cs__keyword">string</span>&nbsp;subscriptionId,<span class="cs__keyword">string</span>&nbsp;base64encodedcert)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">return</span>&nbsp;<span class="cs__keyword">new</span>&nbsp;CertificateCloudCredentials(subscriptionId,&nbsp;<span class="cs__keyword">new</span>&nbsp;X509Certificate2(Convert.FromBase64String(base64encodedcert)));&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
}&nbsp;
</pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
Call AzureAutomation.CreateAutomationRunbook(); in program.cs Main function and can verify in Manage Azure portal</pre>
<pre>like below:</pre>
<pre><img id="133030" src="133030-automationimage.jpg" alt="" width="899" height="353"><br></pre>
<ul>
</ul>
<h1>Next Poweshell</h1>
<p>what we did using Nuget can also be doe using below powershell script:</p>
<p>pwershell workflow:</p>
<p>&nbsp;</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>PowerShell Workflow</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">powershellworkflow</span>
<pre class="hidden">&lt;# 
.SYNOPSIS 
    Provides a simple example of a Azure Automation runbook.   
 
.DESCRIPTION 
    This runbook provides the &quot;Hello World&quot; example for Azure Automation.  If you are  
    brand new to Automation in Azure, you can use this runbook to explore testing  
    and publishing capabilities.   
 
    The runbook takes in an optional string parameter.  If you leave the parameter blank, the  
    default of $Name will equal &quot;World&quot;.  The runbook then prints &quot;Hello&quot; concatenated with $Name. 
    
 
.PARAMETER Name 
    String value to print as output 
 
.EXAMPLE 
    Write-HelloWorld -Name &quot;World&quot; 
 
.NOTES 
    Author: System Center Automation Team  
    Last Updated: 3/3/2014    
#&gt; 
 
 
workflow Write-HelloWorld { 
    param ( 
         
        # Optional parameter of type string.  
        # If you do not enter anything, the default value of Name  
        # will be World 
        [parameter(Mandatory=$false)] 
        [String]$Name = &quot;World&quot; 
    ) 
 
        Write-Output &quot;Hello $Name&quot; 
 
}</pre>
<div class="preview">
<pre class="powershellworkflow"><span class="powerShellWorkflow__mlcom">&lt;#&nbsp;&nbsp;
.SYNOPSIS&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Provides&nbsp;a&nbsp;simple&nbsp;example&nbsp;of&nbsp;a&nbsp;Azure&nbsp;Automation&nbsp;runbook.&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;
.DESCRIPTION&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;This&nbsp;runbook&nbsp;provides&nbsp;the&nbsp;&quot;Hello&nbsp;World&quot;&nbsp;example&nbsp;for&nbsp;Azure&nbsp;Automation.&nbsp;&nbsp;If&nbsp;you&nbsp;are&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;brand&nbsp;new&nbsp;to&nbsp;Automation&nbsp;in&nbsp;Azure,&nbsp;you&nbsp;can&nbsp;use&nbsp;this&nbsp;runbook&nbsp;to&nbsp;explore&nbsp;testing&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;and&nbsp;publishing&nbsp;capabilities.&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;The&nbsp;runbook&nbsp;takes&nbsp;in&nbsp;an&nbsp;optional&nbsp;string&nbsp;parameter.&nbsp;&nbsp;If&nbsp;you&nbsp;leave&nbsp;the&nbsp;parameter&nbsp;blank,&nbsp;the&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;default&nbsp;of&nbsp;$Name&nbsp;will&nbsp;equal&nbsp;&quot;World&quot;.&nbsp;&nbsp;The&nbsp;runbook&nbsp;then&nbsp;prints&nbsp;&quot;Hello&quot;&nbsp;concatenated&nbsp;with&nbsp;$Name.&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;
.PARAMETER&nbsp;Name&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;String&nbsp;value&nbsp;to&nbsp;print&nbsp;as&nbsp;output&nbsp;&nbsp;
&nbsp;&nbsp;
.EXAMPLE&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Write-HelloWorld&nbsp;-Name&nbsp;&quot;World&quot;&nbsp;&nbsp;
&nbsp;&nbsp;
.NOTES&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Author:&nbsp;System&nbsp;Center&nbsp;Automation&nbsp;Team&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Last&nbsp;Updated:&nbsp;3/3/2014&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
#&gt;</span>&nbsp;&nbsp;
&nbsp;&nbsp;
&nbsp;&nbsp;
<span class="powerShellWorkflow__keyword">workflow</span>&nbsp;Write<span class="powerShellWorkflow__operator">-</span>HelloWorld&nbsp;{&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="powerShellWorkflow__keyword">param</span>&nbsp;(&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="powerShellWorkflow__com">#&nbsp;Optional&nbsp;parameter&nbsp;of&nbsp;type&nbsp;string.&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="powerShellWorkflow__com">#&nbsp;If&nbsp;you&nbsp;do&nbsp;not&nbsp;enter&nbsp;anything,&nbsp;the&nbsp;default&nbsp;value&nbsp;of&nbsp;Name&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="powerShellWorkflow__com">#&nbsp;will&nbsp;be&nbsp;World&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[parameter(Mandatory=<span class="powerShellWorkflow__variable">$false</span>)]&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[String]<span class="powerShellWorkflow__variable">$Name</span>&nbsp;=&nbsp;<span class="powerShellWorkflow__string">&quot;World&quot;</span>&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;)&nbsp;&nbsp;
&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Write<span class="powerShellWorkflow__operator">-</span>Output&nbsp;<span class="powerShellWorkflow__string">&quot;Hello&nbsp;$Name&quot;</span>&nbsp;&nbsp;
&nbsp;&nbsp;
}</pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>PowerShell</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">powershell</span>
<pre class="hidden">##Creating Azure Automation workflow and schedule
# Get Automation Account details from Get-AzureAutomationAccount
#Parameter Set: ByDaily
#New-AzureAutomationSchedule [-AutomationAccountName] &lt;String&gt; [-Name] &lt;String&gt; [-StartTime] &lt;DateTime&gt; -DayInterval &lt;Int32&gt; [-Description &lt;String&gt; ] [-ExpiryTime &lt;DateTime&gt; ] 

#Parameter Set: ByHourly
#New-AzureAutomationSchedule [-AutomationAccountName] &lt;String&gt; [-Name] &lt;String&gt; [-StartTime] &lt;DateTime&gt; -HourInterval &lt;Int32&gt; [-Description &lt;String&gt; ] [-ExpiryTime &lt;DateTime&gt; ] 

#Parameter Set: ByOneTime
#New-AzureAutomationSchedule [-AutomationAccountName] &lt;String&gt; [-Name] &lt;String&gt; [-StartTime] &lt;DateTime&gt; -OneTime [-Description &lt;String&gt; ] 

$AzureAutomationAccount=&quot;AutomationAccountname&quot;
$StartDate = Get-Date -Day 12 -Month 6 -Year 2016
$EndDate = Get-Date -Day 12 -Month 6 -Year 2023
$runbookName=&quot;Write-HelloWorld&quot;
$runbookSchedule=&quot;Write-HelloWorldSchedule&quot;
#Get-AzureAutomationAccount [[-Name] &lt;String&gt; ] [[-Location] &lt;String&gt; ] 
New-AzureAutomationRunbook -AutomationAccountName $AzureAutomationAccount -Path &quot;D:\Disco\AzureAutomationHelloWorkflow.ps1&quot;  -Description &quot;This is a sample runbook&quot;
Publish-AzureAutomationRunbook -AutomationAccountName $AzureAutomationAccount -Name $runbookName
New-AzureAutomationSchedule -AutomationAccountName $AzureAutomationAccount -Name $runbookSchedule -StartTime $StartDate -DayInterval 1 -Description &quot;daily schedule for runbook.&quot; -ExpiryTime $EndDate 
Set-AzureAutomationSchedule -AutomationAccountName $AzureAutomationAccount -Name $runbookSchedule -IsEnabled $true
Register-AzureAutomationScheduledRunbook -AutomationAccountName $AzureAutomationAccount -Name $runbookName -ScheduleName $runbookSchedule </pre>
<div class="preview">
<pre class="powershell"><span class="powerShell__com">##Creating&nbsp;Azure&nbsp;Automation&nbsp;workflow&nbsp;and&nbsp;schedule</span>&nbsp;
<span class="powerShell__com">#&nbsp;Get&nbsp;Automation&nbsp;Account&nbsp;details&nbsp;from&nbsp;Get-AzureAutomationAccount</span>&nbsp;
<span class="powerShell__com">#Parameter&nbsp;Set:&nbsp;ByDaily</span>&nbsp;
<span class="powerShell__com">#New-AzureAutomationSchedule&nbsp;[-AutomationAccountName]&nbsp;&lt;String&gt;&nbsp;[-Name]&nbsp;&lt;String&gt;&nbsp;[-StartTime]&nbsp;&lt;DateTime&gt;&nbsp;-DayInterval&nbsp;&lt;Int32&gt;&nbsp;[-Description&nbsp;&lt;String&gt;&nbsp;]&nbsp;[-ExpiryTime&nbsp;&lt;DateTime&gt;&nbsp;]&nbsp;</span>&nbsp;
&nbsp;
<span class="powerShell__com">#Parameter&nbsp;Set:&nbsp;ByHourly</span>&nbsp;
<span class="powerShell__com">#New-AzureAutomationSchedule&nbsp;[-AutomationAccountName]&nbsp;&lt;String&gt;&nbsp;[-Name]&nbsp;&lt;String&gt;&nbsp;[-StartTime]&nbsp;&lt;DateTime&gt;&nbsp;-HourInterval&nbsp;&lt;Int32&gt;&nbsp;[-Description&nbsp;&lt;String&gt;&nbsp;]&nbsp;[-ExpiryTime&nbsp;&lt;DateTime&gt;&nbsp;]&nbsp;</span>&nbsp;
&nbsp;
<span class="powerShell__com">#Parameter&nbsp;Set:&nbsp;ByOneTime</span>&nbsp;
<span class="powerShell__com">#New-AzureAutomationSchedule&nbsp;[-AutomationAccountName]&nbsp;&lt;String&gt;&nbsp;[-Name]&nbsp;&lt;String&gt;&nbsp;[-StartTime]&nbsp;&lt;DateTime&gt;&nbsp;-OneTime&nbsp;[-Description&nbsp;&lt;String&gt;&nbsp;]&nbsp;</span>&nbsp;
&nbsp;
<span class="powerShell__variable">$AzureAutomationAccount</span>=<span class="powerShell__string">&quot;AutomationAccountname&quot;</span>&nbsp;
<span class="powerShell__variable">$StartDate</span>&nbsp;=&nbsp;<span class="powerShell__cmdlets">Get-Date</span>&nbsp;<span class="powerShell__operator">-</span>Day&nbsp;12&nbsp;<span class="powerShell__operator">-</span>Month&nbsp;6&nbsp;<span class="powerShell__operator">-</span>Year&nbsp;2016&nbsp;
<span class="powerShell__variable">$EndDate</span>&nbsp;=&nbsp;<span class="powerShell__cmdlets">Get-Date</span>&nbsp;<span class="powerShell__operator">-</span>Day&nbsp;12&nbsp;<span class="powerShell__operator">-</span>Month&nbsp;6&nbsp;<span class="powerShell__operator">-</span>Year&nbsp;2023&nbsp;
<span class="powerShell__variable">$runbookName</span>=<span class="powerShell__string">&quot;Write-HelloWorld&quot;</span>&nbsp;
<span class="powerShell__variable">$runbookSchedule</span>=<span class="powerShell__string">&quot;Write-HelloWorldSchedule&quot;</span>&nbsp;
<span class="powerShell__com">#Get-AzureAutomationAccount&nbsp;[[-Name]&nbsp;&lt;String&gt;&nbsp;]&nbsp;[[-Location]&nbsp;&lt;String&gt;&nbsp;]&nbsp;</span>&nbsp;
New<span class="powerShell__operator">-</span>AzureAutomationRunbook&nbsp;<span class="powerShell__operator">-</span>AutomationAccountName&nbsp;<span class="powerShell__variable">$AzureAutomationAccount</span>&nbsp;<span class="powerShell__operator">-</span>Path&nbsp;<span class="powerShell__string">&quot;D:\Disco\AzureAutomationHelloWorkflow.ps1&quot;</span>&nbsp;&nbsp;<span class="powerShell__operator">-</span>Description&nbsp;<span class="powerShell__string">&quot;This&nbsp;is&nbsp;a&nbsp;sample&nbsp;runbook&quot;</span>&nbsp;
Publish<span class="powerShell__operator">-</span>AzureAutomationRunbook&nbsp;<span class="powerShell__operator">-</span>AutomationAccountName&nbsp;<span class="powerShell__variable">$AzureAutomationAccount</span>&nbsp;<span class="powerShell__operator">-</span>Name&nbsp;<span class="powerShell__variable">$runbookName</span>&nbsp;
New<span class="powerShell__operator">-</span>AzureAutomationSchedule&nbsp;<span class="powerShell__operator">-</span>AutomationAccountName&nbsp;<span class="powerShell__variable">$AzureAutomationAccount</span>&nbsp;<span class="powerShell__operator">-</span>Name&nbsp;<span class="powerShell__variable">$runbookSchedule</span>&nbsp;<span class="powerShell__operator">-</span>StartTime&nbsp;<span class="powerShell__variable">$StartDate</span>&nbsp;<span class="powerShell__operator">-</span>DayInterval&nbsp;1&nbsp;<span class="powerShell__operator">-</span>Description&nbsp;<span class="powerShell__string">&quot;daily&nbsp;schedule&nbsp;for&nbsp;runbook.&quot;</span>&nbsp;<span class="powerShell__operator">-</span>ExpiryTime&nbsp;<span class="powerShell__variable">$EndDate</span>&nbsp;&nbsp;
Set<span class="powerShell__operator">-</span>AzureAutomationSchedule&nbsp;<span class="powerShell__operator">-</span>AutomationAccountName&nbsp;<span class="powerShell__variable">$AzureAutomationAccount</span>&nbsp;<span class="powerShell__operator">-</span>Name&nbsp;<span class="powerShell__variable">$runbookSchedule</span>&nbsp;<span class="powerShell__operator">-</span>IsEnabled&nbsp;<span class="powerShell__variable">$true</span>&nbsp;
Register<span class="powerShell__operator">-</span>AzureAutomationScheduledRunbook&nbsp;<span class="powerShell__operator">-</span>AutomationAccountName&nbsp;<span class="powerShell__variable">$AzureAutomationAccount</span>&nbsp;<span class="powerShell__operator">-</span>Name&nbsp;<span class="powerShell__variable">$runbookName</span>&nbsp;<span class="powerShell__operator">-</span>ScheduleName&nbsp;<span class="powerShell__variable">$runbookSchedule</span>&nbsp;</pre>
</div>
</div>
</div>
<h1 class="endscriptcode">&nbsp;Happy Learning !</h1>