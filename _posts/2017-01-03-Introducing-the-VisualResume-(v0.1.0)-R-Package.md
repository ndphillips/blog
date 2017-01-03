---
title: "Introducing the VisualResume (v0.1.0) R Package"

date: "January 3 2017"
layout: post
---



<section class="main-content">
<div id="visual-resumes-are-cool" class="section level2">
<h2>Visual Resumes are cool</h2>
<p>Some years ago, during the course of one of my regular Google image searches for inspiring designs, I discovered Visual Resumes (aka. Infographic Resumes) like this one from <a href="https://venngage-wordpress.s3.amazonaws.com/uploads/2016/05/michael-anderson.png">Michael Anderson</a>. I immediately fell in love. And of course, I quickly set out to create my own in R. The result is a new package called <code>VisualResume</code>. The main function in the package, <code>VisualResume()</code> will create a visual resume like the one below for our favorite anti-hero <a href="https://en.wikipedia.org/wiki/Walter_White_(Breaking_Bad)">Walter White</a>:</p>
<p><img src="{{ site.url }}{{ site.baseurl }}/knitr_files/VisualResume_Post_files/figure-html/unnamed-chunk-2-1.png" /><!-- --></p>
<div id="intallation" class="section level3">
<h3>Intallation</h3>
<p>Version <code>v0.1.0</code> of <code>VisualResume</code> is available on GitHub at <a href="http://www.github.com/ndphillips/VisualResume" class="uri">http://www.github.com/ndphillips/VisualResume</a>.</p>
<p>To use <code>VisualResume</code>, first, install the package from GitHub:</p>
<div class="sourceCode"><pre class="sourceCode r"><code class="sourceCode r"><span class="kw">install.packages</span>(<span class="st">&quot;devtools&quot;</span>) <span class="co"># Only if you don&#39;t have the devtools package</span>
devtools::<span class="kw">install_github</span>(<span class="st">&quot;ndphillips/VisualResume&quot;</span>)</code></pre></div>
</div>
<div id="visualresume" class="section level3">
<h3><code>VisualResume()</code></h3>
<p>The main function in the package is <code>VisualResume()</code>. When running <code>VisualResume()</code> you need to include several arguments that specify the content, size and location of the plotting elements. The function will automatically format the resume to fit your specifications.</p>
<div id="critical-arguments" class="section level4">
<h4>Critical arguments:</h4>
<p>Here are the critical arguments to the function:</p>
<table style="width:69%;">
<colgroup>
<col width="15%" />
<col width="54%" />
</colgroup>
<thead>
<tr class="header">
<th>Argument</th>
<th>Definition</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>titles.left</code>, <code>titles.right</code></td>
<td>Character vectors (length 3) indicating the header titles</td>
</tr>
<tr class="even">
<td><code>timeline</code></td>
<td>A dataframe with columns <code>title</code>, <code>sub</code>, <code>start</code>, <code>end</code>, <code>side</code>. The <code>title</code> and <code>sub</code> columns are character, <code>start</code> and <code>end</code> are integer, and <code>side</code> is binary (0 = bottom, 1 = top).</td>
</tr>
<tr class="odd">
<td><code>events</code></td>
<td>A dataframe with columns <code>title</code>, <code>year</code> specifying important events (e.g.; publications).</td>
</tr>
<tr class="even">
<td><code>interests</code></td>
<td>A list of named character vectors specifying interests. The more often a value occurs in a vector, the larger it will be displayed.</td>
</tr>
</tbody>
</table>
</div>
<div id="optional-arguments" class="section level4">
<h4>Optional arguments</h4>
<p>Here are some of the optional function arguments that will either add new elements to the plot, or adjust the attributes of existing elements.</p>
<table style="width:69%;">
<colgroup>
<col width="15%" />
<col width="54%" />
</colgroup>
<thead>
<tr class="header">
<th>Argument</th>
<th>Definition</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>timeline.labels</code></td>
<td>Character vector (length 2) indicating labels for the top and bottom of the timeline</td>
</tr>
<tr class="even">
<td><code>events</code></td>
<td>A dataframe with columns <code>title</code>, <code>year</code> specifying important events (e.g.; publications).</td>
</tr>
<tr class="odd">
<td><code>interests</code></td>
<td>A list of named character vectors specifying interests. The more often a value occurs in a vector, the larger it will be displayed.</td>
</tr>
<tr class="even">
<td><code>milestones</code></td>
<td>A dataframe with columns <code>title</code>, <code>sub</code>, <code>year</code> specifying some milestones (e.g. degrees earned).</td>
</tr>
<tr class="odd">
<td><code>titles.right.cex</code>, <code>titles.left.cex</code></td>
<td>Numeric vectors specifying the size of the header titles.</td>
</tr>
<tr class="even">
<td><code>year.steps</code></td>
<td>An integer specifying the step size between year labels.</td>
</tr>
<tr class="odd">
<td><code>col</code>, <code>trans</code></td>
<td>The color, and transparencies, of timeline elements</td>
</tr>
</tbody>
</table>
</div>
</div>
<div id="customising-timeline-locations" class="section level3">
<h3>Customising timeline locations</h3>
<p><code>VisualResume()</code> will do its best to put plotting elements, like boxes and boxes, in reasonable locations in the timeline. However, it won’t be perfect. In some cases, labels might overlap or just not look very elegant. If this happens, you can specify some plotting parameters in the <code>timeline</code> dataframe by including the columns <code>box.x0, box.x1, box.y1, box.y2</code>, which control the locations of the boxes, <code>point.x, point.y</code> which control the locations of the points, and <code>label.x, label.y, label.dir</code> which specify the locations and direction of the labels. See the help menu<code>?VisualResume</code> for additional details.</p>
</div>
<div id="walter-whites-visual-resume" class="section level3">
<h3>Walter White’s Visual Resume</h3>
<p>Here is the code that generates the visual resume for Walter White (my apologies for any errors in the data!):</p>
<div class="sourceCode"><pre class="sourceCode r"><code class="sourceCode r"><span class="co"># Walter White&#39;s Visual Resume</span>

VisualResume::<span class="kw">VisualResume</span>(
<span class="dt">titles.left =</span> <span class="kw">c</span>(<span class="st">&quot;Walter White, PhD&quot;</span>, 
                <span class="st">&quot;Chemistry, Cooking, Pizza&quot;</span>, 
                <span class="st">&quot;*Built with love in R using the VisualResume package: www.ndphillips.github.io/VisualResume&quot;</span>),
<span class="dt">titles.left.cex =</span> <span class="kw">c</span>(<span class="dv">3</span>, <span class="fl">2.5</span>, <span class="dv">1</span>),
<span class="dt">titles.right.cex =</span> <span class="kw">c</span>(<span class="dv">3</span>, <span class="fl">2.5</span>, <span class="dv">1</span>),
<span class="dt">titles.right =</span> <span class="kw">c</span>(<span class="st">&quot;www.lospolloshermanos.com&quot;</span>, 
                 <span class="st">&quot;TheOneWhoKnocks@gmail.com&quot;</span>, 
                 <span class="st">&quot;Full Resume: https://ndphillips.github.io/cv.html&quot;</span>),
<span class="dt">timeline.labels =</span> <span class="kw">c</span>(<span class="st">&quot;Education&quot;</span>, <span class="st">&quot;Employment&quot;</span>),
<span class="dt">timeline =</span> <span class="kw">data.frame</span>(<span class="dt">title =</span> <span class="kw">c</span>(<span class="st">&quot;Grinnell Col&quot;</span>, <span class="st">&quot;Ohio U&quot;</span>, <span class="st">&quot;U of Basel&quot;</span>,
                                <span class="st">&quot;Max Planck Institute&quot;</span>, <span class="st">&quot;Old Van&quot;</span>, <span class="st">&quot;Gray Matter&quot;</span>,
                                <span class="st">&quot;Sandia Laboratories&quot;</span>, <span class="st">&quot;J.P. Wynne High School&quot;</span>, <span class="st">&quot;A1A Car Wash&quot;</span>),
                      <span class="dt">sub =</span> <span class="kw">c</span>(<span class="st">&quot;BA. Student&quot;</span>, <span class="st">&quot;MS. Student&quot;</span>, <span class="st">&quot;PhD. Student&quot;</span>, 
                              <span class="st">&quot;PhD. Researcher&quot;</span>, <span class="st">&quot;Methamphetamine Research&quot;</span>, <span class="st">&quot;Co-Founder&quot;</span>, 
                              <span class="st">&quot;Chemist&quot;</span>, <span class="st">&quot;Chemistry Teacher&quot;</span>, <span class="st">&quot;Co-Owner&quot;</span>),
                      <span class="dt">start =</span> <span class="kw">c</span>(<span class="dv">1976</span>, <span class="fl">1980.1</span>, <span class="fl">1982.2</span>, <span class="dv">1985</span>, 
                                <span class="fl">1996.5</span>, <span class="dv">1987</span>, <span class="dv">1991</span>, <span class="dv">1995</span>, <span class="dv">2001</span>),
                      <span class="dt">end =</span> <span class="kw">c</span>(<span class="dv">1980</span>, <span class="dv">1982</span>, <span class="dv">1985</span>, <span class="dv">1987</span>, <span class="dv">1998</span>, 
                              <span class="dv">1992</span>, <span class="dv">1995</span>, <span class="dv">1998</span>, <span class="dv">2003</span>),
                      <span class="dt">side =</span> <span class="kw">c</span>(<span class="dv">1</span>, <span class="dv">1</span>, <span class="dv">1</span>, <span class="dv">1</span>, <span class="dv">1</span>, <span class="dv">0</span>, <span class="dv">0</span>, <span class="dv">0</span>, <span class="dv">0</span>)),
<span class="dt">milestones =</span> <span class="kw">data.frame</span>(<span class="dt">title =</span> <span class="kw">c</span>(<span class="st">&quot;BA&quot;</span>, <span class="st">&quot;MS&quot;</span>, <span class="st">&quot;PhD&quot;</span>),
                        <span class="dt">sub =</span> <span class="kw">c</span>(<span class="st">&quot;Math&quot;</span>, <span class="st">&quot;Chemistry&quot;</span>, <span class="st">&quot;Chemistry&quot;</span>),
                        <span class="dt">year =</span> <span class="kw">c</span>(<span class="dv">1980</span>, <span class="dv">1982</span>, <span class="dv">1985</span>)),
<span class="dt">events =</span> <span class="kw">data.frame</span>(<span class="dt">year =</span> <span class="kw">c</span>(<span class="dv">1985</span>, <span class="dv">1995</span>, <span class="dv">1997</span>, <span class="dv">1999</span>, <span class="dv">2000</span>),
                    <span class="dt">title =</span> <span class="kw">c</span>(<span class="st">&quot;Contributed to Nobel Prize winning experiment.&quot;</span>,
                              <span class="st">&quot;Honorary mention for best Chemistry teacher of the year.&quot;</span>,
                              <span class="st">&quot;Created Blue Sky, the most potent methamphetamine ever produced.&quot;</span>,
                              <span class="st">&quot;Made first $1,000,000.&quot;</span>,
                              <span class="st">&quot;White, W., &amp; Pinkman, J. (2000). Blue Sky: A method of [...].</span><span class="ch">\n</span><span class="st">Journal of Psychopharmical Substances, 1(1),.&quot;</span>)),
<span class="dt">interests =</span> <span class="kw">list</span>(<span class="st">&quot;programming&quot;</span> =<span class="st"> </span><span class="kw">c</span>(<span class="kw">rep</span>(<span class="st">&quot;R&quot;</span>, <span class="dv">10</span>), <span class="kw">rep</span>(<span class="st">&quot;Python&quot;</span>, <span class="dv">1</span>), <span class="kw">rep</span>(<span class="st">&quot;JavaScript&quot;</span>, <span class="dv">2</span>), <span class="st">&quot;MatLab&quot;</span>),
                 <span class="st">&quot;statistics&quot;</span> =<span class="st"> </span><span class="kw">c</span>(<span class="kw">rep</span>(<span class="st">&quot;Trees&quot;</span>, <span class="dv">10</span>), <span class="kw">rep</span>(<span class="st">&quot;Bayesian&quot;</span>, <span class="dv">5</span>), <span class="kw">rep</span>(<span class="st">&quot;Regression&quot;</span>, <span class="dv">3</span>)),
                 <span class="st">&quot;leadership&quot;</span> =<span class="st"> </span><span class="kw">c</span>(<span class="kw">rep</span>(<span class="st">&quot;Motivation&quot;</span>, <span class="dv">10</span>), <span class="kw">rep</span>(<span class="st">&quot;Decision Making&quot;</span>, <span class="dv">5</span>), <span class="kw">rep</span>(<span class="st">&quot;Manipulation&quot;</span>, <span class="dv">30</span>)),
                 <span class="st">&quot;Chemistry&quot;</span> =<span class="st"> </span><span class="kw">c</span>(<span class="kw">rep</span>(<span class="st">&quot;Bio&quot;</span>, <span class="dv">10</span>), <span class="kw">rep</span>(<span class="st">&quot;Pharmaceuticals&quot;</span>, <span class="dv">50</span>))),
<span class="dt">year.steps =</span> <span class="dv">2</span>
)</code></pre></div>
</div>
<div id="bug-reports" class="section level3">
<h3>Bug-reports</h3>
<p>This package is very young and likely contains many bugs and room for improvement. Please submit bug reports and feature requests at <a href="https://github.com/ndphillips/VisualResume/issues" class="uri">https://github.com/ndphillips/VisualResume/issues</a></p>
</div>
</div>
</section>
