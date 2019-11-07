# Captcha for Windows Application
## Requires
- Visual Studio 2010
## License
- Apache License, Version 2.0
## Technologies
- C#
- Windows Forms
## Topics
- CAPTCHA
## Updated
- 02/06/2014
## Description

<h1>Introduction</h1>
<p><em>captcha in C#.<br>
</em></p>
<h1><span>Building the Sample</span></h1>
<p><em>It requires two libraries System.Windows.Forms and System.Drawing.<br>
</em></p>
<p><span style="font-size:20px; font-weight:bold">Description</span></p>
<p><img id="107516" src="107516-captcha.jpg" alt="" width="304" height="303"></p>
<h1><strong>Captcha:</strong></h1>
<p>A CAPTCHA is acronym for <strong>C</strong>omplete <strong>A</strong>utomated <strong>
P</strong>ublic <strong>T</strong>uring test to tell <strong>C</strong>omputers and
<strong>H</strong>umans <strong>A</strong>part.</p>
<p>This term was coined in 2000 by Luis von Ahn,Manuel Blum, Nicholas Hopper and John Langford of Carnegie Mellon University. At the time they developed the first CAPTCHA to be used by Yahoo.</p>
<p>A CAPTCHA is a program that can generate and grade tests that humans can pass but current computer programs cannot. For Example, humans can read distorted text as the one shown below, but current computer can't.</p>
<p>This sample explains how to use Captcha in your windows application using c#.</p>
<p>Captcha is used to restrict autmated form registration/submission of data from unwanted program/virus/spam etc. It ensures the submission done by human being. In this process we are creating dynamically image for verification of 6 character code. The verification
 code contains alphanumeric, but you can change this as per your requirement.</p>
<p>We are creating Image Dynamically and Storing in D drive temporary.</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>VB Script</span><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">vbs</span><span class="hidden">csharp</span>
<pre class="hidden">Private Sub CreateImage()
        Dim code As String = GetRandomText()
        Dim bitmap As New Bitmap(200, 50, PixelFormat.Format32bppArgb)
        Dim g As Graphics = Graphics.FromImage(bitmap)
        Dim pen As New Pen(Color.Yellow)
        Dim rect As New Rectangle(0, 0, 200, 50)
        Dim b As New SolidBrush(Color.Black)
        Dim White As New SolidBrush(Color.White)
        Dim counter As Integer = 0
        g.DrawRectangle(pen, rect)
        g.FillRectangle(b, rect)
        For i As Integer = 0 To code.Length - 1
            g.DrawString(code(i).ToString(), New Font(&quot;Georgia&quot;, 10 &#43; rand.[Next](14, 18)), White, New PointF(10 &#43; counter, 10))
            counter &#43;= 20
        Next
        DrawRandomLines(g)
        If File.Exists(&quot;d:/tempimage.bmp&quot;) Then
            Try
                File.Delete(&quot;d:/tempimage.bmp&quot;)
                bitmap.Save(&quot;d:/tempimage.bmp&quot;)
            Catch ex As Exception
                MessageBox.Show(ex.Message)
            End Try
        Else
            bitmap.Save(&quot;d:/tempimage.bmp&quot;)
        End If
        g.Dispose()
        bitmap.Dispose()
        PictureBox1.Image = Image.FromFile(&quot;d:/tempimage.bmp&quot;)
    End Sub</pre>
<pre class="hidden">private void CreateImage()
        {
            string code = GetRandomText();
            Bitmap bitmap = new Bitmap(200, 50, PixelFormat.Format32bppArgb);
            Graphics g = Graphics.FromImage(bitmap);
            Pen pen = new Pen(Color.Yellow);
            Rectangle rect = new Rectangle(0, 0, 200, 50);
            SolidBrush b = new SolidBrush(Color.Black);
            SolidBrush White = new SolidBrush(Color.White);
            int counter = 0;
            g.DrawRectangle(pen, rect);
            g.FillRectangle(b, rect);
            for (int i = 0; i &lt; code.Length; i&#43;&#43;)
            {
                g.DrawString(code[i].ToString(), new Font(&quot;Georgia&quot;, 10 &#43; rand.Next(14, 18)), White, new PointF(10 &#43; counter, 10));
                counter &#43;= 20;
            }
            DrawRandomLines(g);
            if (File.Exists(&quot;d:/tempimage.bmp&quot;))
            {
                try
                {
                    File.Delete(&quot;d:/tempimage.bmp&quot;);
                    bitmap.Save(&quot;d:/tempimage.bmp&quot;);
                }
                catch(Exception ex)
                {
                    MessageBox.Show(ex.Message);
                }
            }
            else
            {
                bitmap.Save(&quot;d:/tempimage.bmp&quot;);
            }
            g.Dispose();
            bitmap.Dispose();
            pictureBox1.Image = Image.FromFile(&quot;d:/tempimage.bmp&quot;);
        }</pre>
<div class="preview">
<pre class="vbs"><span class="vbScript__keyword">Private</span>&nbsp;<span class="vbScript__keyword">Sub</span>&nbsp;CreateImage()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="vbScript__keyword">Dim</span>&nbsp;code&nbsp;<span class="vbScript__keyword">As</span>&nbsp;<span class="vbScript__keyword">String</span>&nbsp;=&nbsp;GetRandomText()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="vbScript__keyword">Dim</span>&nbsp;bitmap&nbsp;<span class="vbScript__keyword">As</span>&nbsp;<span class="vbScript__keyword">New</span>&nbsp;Bitmap(<span class="vbScript__number">200</span>,&nbsp;<span class="vbScript__number">50</span>,&nbsp;PixelFormat.Format32bppArgb)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="vbScript__keyword">Dim</span>&nbsp;g&nbsp;<span class="vbScript__keyword">As</span>&nbsp;Graphics&nbsp;=&nbsp;Graphics.FromImage(bitmap)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="vbScript__keyword">Dim</span>&nbsp;pen&nbsp;<span class="vbScript__keyword">As</span>&nbsp;<span class="vbScript__keyword">New</span>&nbsp;Pen(Color.Yellow)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="vbScript__keyword">Dim</span>&nbsp;rect&nbsp;<span class="vbScript__keyword">As</span>&nbsp;<span class="vbScript__keyword">New</span>&nbsp;Rectangle(<span class="vbScript__number">0</span>,&nbsp;<span class="vbScript__number">0</span>,&nbsp;<span class="vbScript__number">200</span>,&nbsp;<span class="vbScript__number">50</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="vbScript__keyword">Dim</span>&nbsp;b&nbsp;<span class="vbScript__keyword">As</span>&nbsp;<span class="vbScript__keyword">New</span>&nbsp;SolidBrush(Color.Black)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="vbScript__keyword">Dim</span>&nbsp;White&nbsp;<span class="vbScript__keyword">As</span>&nbsp;<span class="vbScript__keyword">New</span>&nbsp;SolidBrush(Color.White)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="vbScript__keyword">Dim</span>&nbsp;counter&nbsp;<span class="vbScript__keyword">As</span>&nbsp;<span class="vbScript__keyword">Integer</span>&nbsp;=&nbsp;<span class="vbScript__number">0</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;g.DrawRectangle(pen,&nbsp;rect)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;g.FillRectangle(b,&nbsp;rect)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="vbScript__keyword">For</span>&nbsp;i&nbsp;<span class="vbScript__keyword">As</span>&nbsp;<span class="vbScript__keyword">Integer</span>&nbsp;=&nbsp;<span class="vbScript__number">0</span>&nbsp;<span class="vbScript__keyword">To</span>&nbsp;code.Length&nbsp;-&nbsp;<span class="vbScript__number">1</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;g.DrawString(code(i).ToString(),&nbsp;<span class="vbScript__keyword">New</span>&nbsp;Font(<span class="vbScript__string">&quot;Georgia&quot;</span>,&nbsp;<span class="vbScript__number">10</span>&nbsp;&#43;&nbsp;rand.[<span class="vbScript__keyword">Next</span>](<span class="vbScript__number">14</span>,&nbsp;<span class="vbScript__number">18</span>)),&nbsp;White,&nbsp;<span class="vbScript__keyword">New</span>&nbsp;PointF(<span class="vbScript__number">10</span>&nbsp;&#43;&nbsp;counter,&nbsp;<span class="vbScript__number">10</span>))&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;counter&nbsp;&#43;=&nbsp;<span class="vbScript__number">20</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="vbScript__keyword">Next</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;DrawRandomLines(g)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="vbScript__keyword">If</span>&nbsp;File.Exists(<span class="vbScript__string">&quot;d:/tempimage.bmp&quot;</span>)&nbsp;<span class="vbScript__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="vbScript__keyword">Try</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File.Delete(<span class="vbScript__string">&quot;d:/tempimage.bmp&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bitmap.Save(<span class="vbScript__string">&quot;d:/tempimage.bmp&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="vbScript__keyword">Catch</span>&nbsp;ex&nbsp;<span class="vbScript__keyword">As</span>&nbsp;Exception&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MessageBox.Show(ex.Message)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="vbScript__keyword">End</span>&nbsp;<span class="vbScript__keyword">Try</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="vbScript__keyword">Else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bitmap.Save(<span class="vbScript__string">&quot;d:/tempimage.bmp&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="vbScript__keyword">End</span>&nbsp;<span class="vbScript__keyword">If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;g.Dispose()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bitmap.Dispose()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;PictureBox1.Image&nbsp;=&nbsp;Image.FromFile(<span class="vbScript__string">&quot;d:/tempimage.bmp&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="vbScript__keyword">End</span>&nbsp;<span class="vbScript__keyword">Sub</span></pre>
</div>
</div>
</div>
<p>This method contains the Random generation of lines</p>
<p>&nbsp;</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>Visual Basic</span><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">vb</span><span class="hidden">csharp</span>
<pre class="hidden"> Private Sub DrawRandomLines(ByVal g As Graphics)
        Dim green As New SolidBrush(Color.Green)
        'For Creating Lines on The Captcha
        For i As Integer = 0 To 19
            g.DrawLines(New Pen(green, 2), GetRandomPoints())
        Next
    End Sub</pre>
<pre class="hidden"> private void DrawRandomLines(Graphics g)
        {
            SolidBrush green = new SolidBrush(Color.Green);
             //For Creating Lines on The Captcha
            for (int i = 0; i &lt; 20; i&#43;&#43;)
            {
                g.DrawLines(new Pen(green, 2), GetRandomPoints());
            }

        }</pre>
<div class="preview">
<pre class="vb">&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;DrawRandomLines(<span class="visualBasic__keyword">ByVal</span>&nbsp;g&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;Graphics)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;green&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">New</span>&nbsp;SolidBrush(Color.Green)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'For&nbsp;Creating&nbsp;Lines&nbsp;on&nbsp;The&nbsp;Captcha</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">For</span>&nbsp;i&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;=&nbsp;<span class="visualBasic__number">0</span>&nbsp;<span class="visualBasic__keyword">To</span>&nbsp;<span class="visualBasic__number">19</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;g.DrawLines(<span class="visualBasic__keyword">New</span>&nbsp;Pen(green,&nbsp;<span class="visualBasic__number">2</span>),&nbsp;GetRandomPoints())&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span></pre>
</div>
</div>
</div>
<div class="endscriptcode">This method Contains the Random generation of points.</div>
<div class="endscriptcode">
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>Visual Basic</span><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">vb</span><span class="hidden">csharp</span>
<pre class="hidden"> Private Function GetRandomPoints() As Point()
        Dim points As Point() = {New Point(rand.[Next](10, 150), rand.[Next](10, 150)), New Point(rand.[Next](10, 100), rand.[Next](10, 100))}
        Return points
    End Function</pre>
<pre class="hidden"> private Point[] GetRandomPoints()
        {
            Point[] points = { new Point(rand.Next(10, 150), rand.Next(10, 150)), new Point(rand.Next(10, 100), rand.Next(10, 100)) };
            return points;
        }</pre>
<div class="preview">
<pre class="vb">&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Function</span>&nbsp;GetRandomPoints()&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;Point()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;points&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;Point()&nbsp;=&nbsp;{<span class="visualBasic__keyword">New</span>&nbsp;Point(rand.[<span class="visualBasic__keyword">Next</span>](<span class="visualBasic__number">10</span>,&nbsp;<span class="visualBasic__number">150</span>),&nbsp;rand.[<span class="visualBasic__keyword">Next</span>](<span class="visualBasic__number">10</span>,&nbsp;<span class="visualBasic__number">150</span>)),&nbsp;<span class="visualBasic__keyword">New</span>&nbsp;Point(rand.[<span class="visualBasic__keyword">Next</span>](<span class="visualBasic__number">10</span>,&nbsp;<span class="visualBasic__number">100</span>),&nbsp;rand.[<span class="visualBasic__keyword">Next</span>](<span class="visualBasic__number">10</span>,&nbsp;<span class="visualBasic__number">100</span>))}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Return</span>&nbsp;points&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Function</span></pre>
</div>
</div>
</div>
<div class="endscriptcode">you can generate random text by using this method.</div>
<div class="endscriptcode">
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>Visual Basic</span><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">vb</span><span class="hidden">csharp</span>
<pre class="hidden"> Private code As String
    Private Function GetRandomText() As String
        Dim randomText As New StringBuilder()
        If [String].IsNullOrEmpty(code) Then
            Dim alphabets As String = &quot;abcdefghijklmnopqrstuvwxyz1234567890&quot;
            Dim r As New Random()
            For j As Integer = 0 To 5
                randomText.Append(alphabets(r.[Next](alphabets.Length)))
            Next
            code = randomText.ToString()
        End If
        Return code
    End Function</pre>
<pre class="hidden">        string code;
        private string GetRandomText()
        {
            StringBuilder randomText = new StringBuilder();
            if (String.IsNullOrEmpty(code))
            {
                string alphabets = &quot;abcdefghijklmnopqrstuvwxyz1234567890&quot;;
                Random r = new Random();
                for (int j = 0; j &lt;= 5; j&#43;&#43;)
                {
                    randomText.Append(alphabets[r.Next(alphabets.Length)]);
                }
                code = randomText.ToString();
            }
            return code;
        }</pre>
<div class="preview">
<pre class="vb">&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;code&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">String</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Function</span>&nbsp;GetRandomText()&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">String</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;randomText&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">New</span>&nbsp;StringBuilder()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;[<span class="visualBasic__keyword">String</span>].IsNullOrEmpty(code)&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;alphabets&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">String</span>&nbsp;=&nbsp;<span class="visualBasic__string">&quot;abcdefghijklmnopqrstuvwxyz1234567890&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;r&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">New</span>&nbsp;Random()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">For</span>&nbsp;j&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;=&nbsp;<span class="visualBasic__number">0</span>&nbsp;<span class="visualBasic__keyword">To</span>&nbsp;<span class="visualBasic__number">5</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;randomText.Append(alphabets(r.[<span class="visualBasic__keyword">Next</span>](alphabets.Length)))&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;code&nbsp;=&nbsp;randomText.ToString()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Return</span>&nbsp;code&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Function</span></pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
</div>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h1><span>Source Code Files</span></h1>
<ul>
<li><em>source code file name #1 - summary for this source code file.</em> </li><li><em><em>source code file name #2 - summary for this source code file.</em></em>
</li></ul>
<h1>More Information</h1>
<p><em>For more information on X, see ...?</em></p>