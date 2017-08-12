---
title: "Simplicity matters - 3 updates to the FFTrees universe"


date: "August 10, 2017"
layout: post
---


<section class="main-content">
<p><link rel="stylesheet" href="../font-awesome-4.7.0/css/font-awesome.min.css"></p>
<div id="why-simplicity-matters" class="section level2">
<h2>Why simplicity matters</h2>
<blockquote>
<p>Simplicity is the ultimate sophistication ~ Leonardo da Vinci</p>
</blockquote>
<blockquote>
<p>The art of being wise is the art of knowing what to overlook ~ William James</p>
</blockquote>
<blockquote>
<p>If [an algorithm] that measures up very well on the performance criterion is nevertheless totally incomprehensible to a human expert, can it be described as knowledge? Under the common-sense definition of this term […] it is not ~ Quinlan (1999)</p>
</blockquote>
<p>Data scientists are blessed with a plethora of advanced machine learning algorithms that they can easily apply to their data using R, from regression, to random forests, to support vector machines. How do data scientists select a machine learning algorithm for a specific task? In most cases, I’d bet they’ll focus on one criterion: prediction accuracy. That is, the algorithm with the best prediction performance, regardless of how <em>much</em> better it is than other algorithms, and regardless of how <em>interpretable</em> it is, will win out.</p>
<p>But there is a problem. If we evaluate algorithms <em>only</em> by their ranked prediction performance, then we may surround ourselves with algorithms that are completely incomprehensible (see <a href="https://www.technologyreview.com/s/604087/the-dark-secret-at-the-heart-of-ai/">The Dark Secret at the Heart of AI</a>), provide no insight to the data, use wasteful and distracting information, and when they fail, provide little to no guidance as to what exactly went wrong.</p>
<p>Instead, if in addition to pure prediction accuracy, we evaluate algorithms based on their insight, frugality, comprehensibility, and error guidance, we may select simple, comprehensible, frugal algorithms that provide real insight and decision-making guidance.</p>
<p>Moreover, after comparing the performance of simple to complex algorithms, we may find that the relationship between model complexity and prediction performance is much weaker than intuition might suggest. Indeed, simple algorithms may perform just as well, and even better, than their black-box counterparts (Gigerenzer &amp; Brighton, 2009).</p>
<div id="criteria-for-selecting-an-algorithm-that-have-nothing-to-do-with-accuracy" class="section level4">
<h4>4 criteria for selecting an algorithm (that have nothing to do with accuracy)</h4>
<ul>
<li><p><em>Insight</em>: What does the algorithm tell us about the data? After evaluating an algorithm, what do we know about the data that we did not know before? How can the algorithm inspire new questions and models?</p></li>
<li><p><em>Comprehensibility</em>: Will the algorithm be understood and accepted by a statistically novice audience that may be skeptical that an algorithm can replace human expertise?</p></li>
<li><p><em>Frugality</em>: Does the algorithm only use information that is necessary or does it also use a pile of relatively useless junk that is potentially more distracting than helpful to decision makers?</p></li>
<li><p><em>Error Guidance</em>: If the algorithm starts performing poorly in a new dataset, will the algorithm be able to show us what exactly went wrong? Or, will it provide no such guidance and require users to ‘start from scratch’?</p></li>
</ul>
</div>
</div>
<div id="fast-and-frugal-trees-ffts" class="section level2">
<h2>Fast-and-frugal Trees (FFTs)</h2>
<p>One class of algorithms that excel in each of these four areas are <em>fast-and-frugal decision trees</em> (FFTs). FFTs are highly restricted decision trees that try to use as little information as possible in making binary classification decisions. Formally, they are decision trees with two branches under each node, where one (or both) branches are exit branches that trigger an immediate decision (Martignon et al., 2008).</p>
<p>While there are many great packages (such as <a href="https://cran.r-project.org/web/packages/rpart/index.html">rpart</a>) that create decision trees that may or may not be fast-and-frugal, there are fewer packages that explicitly create fast-and-frugal trees. The <a href="https://cran.r-project.org/web/packages/FFTrees/index.html">FFTrees</a> package is one of them.</p>
<p>A few months ago, I wrote a <a href="http://nathanieldphillips.com/2016/08/making-fast-good-decisions-with-the-fftrees-r-package/">blog post</a> introducing FFTrees. But for new users, let’s do a quick example. We’ll use FFTrees applied to a dataset of medical patients to to classify patients as either having or not having heart disease on the basis of both demographic information and medical tests. Here is how the first few rows of the heartdisease dataset look:</p>
<table>
<caption>The heartdisease dataset</caption>
<thead>
<tr class="header">
<th align="right">diagnosis</th>
<th align="right">age</th>
<th align="right">sex</th>
<th align="left">cp</th>
<th align="right">trestbps</th>
<th align="right">chol</th>
<th align="right">fbs</th>
<th align="left">restecg</th>
<th align="right">thalach</th>
<th align="right">exang</th>
<th align="right">oldpeak</th>
<th align="left">slope</th>
<th align="right">ca</th>
<th align="left">thal</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="right">0</td>
<td align="right">63</td>
<td align="right">1</td>
<td align="left">ta</td>
<td align="right">145</td>
<td align="right">233</td>
<td align="right">1</td>
<td align="left">hypertrophy</td>
<td align="right">150</td>
<td align="right">0</td>
<td align="right">2.3</td>
<td align="left">down</td>
<td align="right">0</td>
<td align="left">fd</td>
</tr>
<tr class="even">
<td align="right">1</td>
<td align="right">67</td>
<td align="right">1</td>
<td align="left">a</td>
<td align="right">160</td>
<td align="right">286</td>
<td align="right">0</td>
<td align="left">hypertrophy</td>
<td align="right">108</td>
<td align="right">1</td>
<td align="right">1.5</td>
<td align="left">flat</td>
<td align="right">3</td>
<td align="left">normal</td>
</tr>
<tr class="odd">
<td align="right">1</td>
<td align="right">67</td>
<td align="right">1</td>
<td align="left">a</td>
<td align="right">120</td>
<td align="right">229</td>
<td align="right">0</td>
<td align="left">hypertrophy</td>
<td align="right">129</td>
<td align="right">1</td>
<td align="right">2.6</td>
<td align="left">flat</td>
<td align="right">2</td>
<td align="left">rd</td>
</tr>
<tr class="even">
<td align="right">0</td>
<td align="right">37</td>
<td align="right">1</td>
<td align="left">np</td>
<td align="right">130</td>
<td align="right">250</td>
<td align="right">0</td>
<td align="left">normal</td>
<td align="right">187</td>
<td align="right">0</td>
<td align="right">3.5</td>
<td align="left">down</td>
<td align="right">0</td>
<td align="left">normal</td>
</tr>
<tr class="odd">
<td align="right">0</td>
<td align="right">41</td>
<td align="right">0</td>
<td align="left">aa</td>
<td align="right">130</td>
<td align="right">204</td>
<td align="right">0</td>
<td align="left">hypertrophy</td>
<td align="right">172</td>
<td align="right">0</td>
<td align="right">1.4</td>
<td align="left">up</td>
<td align="right">0</td>
<td align="left">normal</td>
</tr>
<tr class="even">
<td align="right">0</td>
<td align="right">56</td>
<td align="right">1</td>
<td align="left">aa</td>
<td align="right">120</td>
<td align="right">236</td>
<td align="right">0</td>
<td align="left">normal</td>
<td align="right">178</td>
<td align="right">0</td>
<td align="right">0.8</td>
<td align="left">up</td>
<td align="right">0</td>
<td align="left">normal</td>
</tr>
</tbody>
</table>
<p>In the code chunk below I will use FFTrees to create an FFT predicting the binary classification variable <code>diagnosis</code>:</p>
<div class="sourceCode"><pre class="sourceCode r"><code class="sourceCode r"><span class="co"># install.packages(&quot;FFTrees&quot;) # Install FFTrees from CRAN</span>
<span class="kw">library</span>(FFTrees)

<span class="co"># Create an FFTrees object predicting heart disease</span>
heart.fft &lt;-<span class="st"> </span><span class="kw">FFTrees</span>(<span class="dt">formula =</span> diagnosis ~.,
                     <span class="dt">data =</span> heart.train,              <span class="co"># Training data</span>
                     <span class="dt">data.test =</span> heart.test,          <span class="co"># Testing data (optional) </span>
                     <span class="dt">main =</span> <span class="st">&quot;Heart Disease FFT&quot;</span>,      <span class="co"># Some optional labels passed to other functions</span>
                     <span class="dt">decision.labels =</span> <span class="kw">c</span>(<span class="st">&quot;Low-risk&quot;</span>, <span class="st">&quot;High-risk&quot;</span>))</code></pre></div>
<p>Now let’s plot the object <code>heart.fft</code>. As you will see, this plot will show us almost everything we could want to know about the algorithm and how it performed:</p>
<div class="sourceCode"><pre class="sourceCode r"><code class="sourceCode r"><span class="co"># Plot the result with accuracy statistics in testing data</span>
<span class="kw">plot</span>(heart.fft, <span class="dt">data =</span> <span class="st">&quot;test&quot;</span>)</code></pre></div>
<p><img src="{{ site.url }}{{ site.baseurl }}/knitr_files/FFTreesAugust_post_files/figure-html/unnamed-chunk-4-1.png" width="100%" /></p>
<p>For more information about using the package, check out the <a href="https://cran.r-project.org/web/packages/FFTrees/vignettes/guide.html">package guide</a>.</p>
</div>
<div id="updates-to-the-fftrees-universe" class="section level2">
<h2>3 updates to the FFTrees universe</h2>
<p>Now, let’s get to the three updates in the FFTrees universe</p>
<div id="phillips-neth-woike-gaissmaier-2017" class="section level3">
<h3>1) Phillips, Neth, Woike &amp; Gaissmaier (2017)</h3>
<ul>
<li><a href="http://journal.sjdm.org/17/17217/jdm17217.pdf">PDF: FFTrees: A toolbox to create, visualize, and evalute fast-and-frugal decision trees</a>.</li>
</ul>
<div class="figure">
<img src="{{ site.url }}{{ site.baseurl }}/images/FFTManuscriptP2.png" alt="blah" />
<p class="caption">blah</p>
</div>
<p>We (<a href="http://ndphillips.github.io">myself</a>, <a href="https://www.spds.uni-konstanz.de/hans-neth">Hansjörg Neth</a>, <a href="https://www.mpib-berlin.mpg.de/en/staff/jan-k-woike">Jan Woike</a> and <a href="https://www.spds.uni-konstanz.de/wolfgang-gaissmaier">Wolfgang Gaissmaier</a>) recently published a paper in the journal of <a href="http://www.sjdm.org/journal/">Judgment and Decision Making</a> titled <em>FFTrees: A toolbox to create, visualize, and evaluate fast-and-frugal decision trees</em>. In the paper, we explain how FFTs work, how the algorithms in FFTrees build FFTs, and then show how well FFTs can predict data relative to more complex algorithms.</p>
<p>For example, in a prediction simulation, we found that, across 10 real world datasets, FFTs can predict data as well as many other algorithms ranging from non–frugal decision trees (CART), to, regularized logistic regression (RLR), to random forests (RF) and support vector machines (SVM).</p>
<p>Spoiler alert: FFTs can perform just as well as these algorithms. The plot below shows the distribution of prediction performance (measured by balanced accuracy, the average of specificity and sensitivity) of each algorithm in each dataset, as well as an example FFT created for that dataset. As you can see, FFTs (always on the far left in each plot), were very competitive with all other algorithms in every dataset.</p>
<div class="figure">
<img src="{{ site.url }}{{ site.baseurl }}/images/FFTreesCompetition.png" />

</div>
<p>The paper is free to view on the Society for Judgment and Decision Making website at <a href="http://journal.sjdm.org/17/17217/jdm17217.pdf" class="uri">http://journal.sjdm.org/17/17217/jdm17217.pdf</a>.</p>
</div>
<div id="fftrees-v1.3.3" class="section level3">
<h3>2) FFTrees v1.3.3</h3>
<p>FFTrees v1.3.3 has several new features. Here are a few of them:</p>
<p><em>Manually define and test your own FFT ‘in words’</em></p>
<p>Because FFTs are so simple, it’s easy to define an FFT verbally, and then have R convert the verbal definition to an FFTrees object. For example, let’s say you wanted to see how well an alternative heart disease FFT performs that only uses the cues <code>age</code> and <code>thal</code>. You can easily specify such a tree as a character string “If age &gt; 60, predict True. If thal = {rd,fd}, predict True. Otherwise, predict False”:</p>
<div class="sourceCode"><pre class="sourceCode r"><code class="sourceCode r"><span class="co"># Define an FFT verbally using the my.tree argument</span>
<span class="co"># Braces indicate factors</span>

my.heart.fft &lt;-<span class="st"> </span><span class="kw">FFTrees</span>(<span class="dt">formula =</span> diagnosis ~.,
                        <span class="dt">data =</span> heartdisease,
                        <span class="dt">my.tree =</span> <span class="st">&quot;If age &gt; 60, predict True.</span>
<span class="st">                                   If thal = {rd,fd}, predict True. Otherwise, predict False&quot;</span>)</code></pre></div>
<p>Running this code will bypass the FFT construction algorithms, and apply the specific tree we defined to the data. This is a great way to play around with different trees and test how different decision thresholds and cue orders affect decisions.</p>
<p><em>Multiple FFT building algorithms</em></p>
<p>FFTrees v1.3.3 now contains several algorithms for building FFTs. From the <em>ifan</em> and <em>dfan</em> algorithms developed specifically for the FFTrees package, to the max and zig-zag algorithms introduced by Martignon et al. (2008).</p>
<p><em>Include cue costs</em></p>
<p>If your data contains predictors that have real costs to use (i.e.; medical tests), you can now include those costs as an argument <code>cost.cues</code> to FFTrees. When you do so, the tree building algorithm will select predictors as a joint function of their prediction accuracy <em>and</em> their costs. <em>Note: This is an experimental feature that hasn’t been fully tested</em></p>
<div class="sourceCode"><pre class="sourceCode r"><code class="sourceCode r"><span class="co"># Create FFTs that minimize costs of predictors (i.e.; medical testing costs) and outcomes</span>

my.heart.fft &lt;-<span class="st"> </span><span class="kw">FFTrees</span>(<span class="dt">formula =</span> diagnosis ~.,
                        <span class="dt">data =</span> heartdisease,
                        
                        <span class="co"># Include costs of some cues</span>
                        <span class="dt">cost.cues =</span> <span class="kw">data.frame</span>(<span class="st">&quot;cue&quot;</span> =<span class="st"> </span><span class="kw">c</span>(<span class="st">&quot;thal&quot;</span>, <span class="st">&quot;cp&quot;</span>, <span class="st">&quot;ca&quot;</span>),
                                               <span class="st">&quot;cost&quot;</span> =<span class="st"> </span><span class="kw">c</span>(<span class="fl">102.9</span>, <span class="fl">1.00</span>, <span class="fl">100.9</span>)),
                        
                        <span class="co"># Include cost of outcomes (hits, false-alarms, misses, and correct rej)</span>
                        <span class="dt">cost.outcomes =</span> <span class="kw">c</span>(<span class="dv">0</span>, <span class="dv">50</span>, <span class="dv">50</span>, <span class="dv">0</span>),
                        
                        <span class="co"># Tell the algorithm to minimize costs</span>
                        <span class="dt">goal =</span> <span class="st">&#39;cost&#39;</span>,
                        <span class="dt">goal.chase =</span> <span class="st">&#39;cost&#39;</span>)</code></pre></div>
<!-- For example, the dataframe `heart.cost` contains a cost for each predictor in the dataset. -->
<!-- ```{r, echo = FALSE} -->
<!-- knitr::kable(heart.cost) -->
<!-- ``` -->
<!-- For example, here is a heartdisease FFT created ignoring cue costs. This tree will use the default values of `goal = 'bacc'` and `goal.chase = 'bacc'`  -->
<!-- ```{r, message = FALSE} -->
<!-- # Create a tree using default -->
<!-- heart.nc.fft <- FFTrees(formula = diagnosis ~., -->
<!--                         data = heartdisease, -->
<!--                         goal = "bacc", -->
<!--                         goal.chase = "bacc", -->
<!--                         cost.cues = heart.cost, -->
<!--                         cost.outcomes = c(0, 1, 1, 0)) -->
<!-- # Show tree 'in words' -->
<!-- inwords(heart.nc.fft)$v1 -->
<!-- # What is the overall accuracy? -->
<!-- heart.nc.fft$tree.stats$train$bacc[1] -->
<!-- # What is the average cost? -->
<!-- mean(heart.nc.fft$cost$train$total[,1]) -->
<!-- ``` -->
<!-- This tree uses the cues thal (cost of \$102.90), cp (cost of \$1.00) and ca (cost of \$100.90) and has a balanced accuracy of around 81%, at a mean cost of $121. -->
<!-- Now, let's do it again, but this time we'll tell the algorithm to minimize costs by setting `goal = 'cost'` and `goal.chase = 'cost'` -->
<!-- ```{r, message = FALSE} -->
<!-- heart.cost.fft <- FFTrees(formula = diagnosis ~., -->
<!--                         data = heartdisease, -->
<!--                         cost.cues = heart.cost, -->
<!--                         cost.outcomes = c(0, 1, 1, 0), -->
<!--                         goal = "cost", -->
<!--                         goal.chase = "cost") -->
<!-- # Show tree 'in words' -->
<!-- inwords(heart.cost.fft)$v1 -->
<!-- # What is the overall accuracy? -->
<!-- heart.cost.fft$tree.stats$train$bacc[1] -->
<!-- # What is the average cost? -->
<!-- mean(heart.cost.fft$cost$train$total[,1]) -->
<!-- ``` -->
<!-- This tree , has only a slightly lower balanced accuracy of around 77%, but at a *much* lower mean cost of only $2 because it is using much cheaper predictors: cp (cost of \$1.00) age (cost of \$1) and sex (cost of \$1) -->
<p><em>Missing Values</em></p>
<p>Missing values, both in the predictors (aka cues, features) and the criterion, are now acceptable. Cases with missing values in predictors will simply be classified by the first decision node containing a non-missing predictor.</p>
</div>
<div id="shinyfftrees" class="section level3">
<h3>3) ShinyFFTrees</h3>
<ul>
<li>ShinyFFTrees Link: <a href="https://econpsychbasel.shinyapps.io/shinyfftrees/" class="uri">https://econpsychbasel.shinyapps.io/shinyfftrees/</a></li>
</ul>
<p>If you want to use FFTrees, but don’t want to fire up R, there’s also ShinyFFTrees. ShinyFFTrees is a <a href="http://shiny.rstudio.com">Shiny</a> app that allows you to utilize most of the features of the FFTrees package entirely in a web-browser. The app contains most of the functionality of the R package, and even lets you create FFTs from your own, uploaded data.</p>
<p>Here is ShinyFFTrees displayed within this page (performance is better if you open the link in a new window):</p>
<iframe src="https://econpsychbasel.shinyapps.io/shinyfftrees/" , height="500px," width="900px," align="middle">
</iframe>
</div>
<div id="conclusion" class="section level3">
<h3>Conclusion</h3>
<p>There is no free lunch in machine learning algorithms (Wolpert, 1996). No one algorithm is better than another <em>a priori</em>. For some decision tasks, complex black box algorithms such as deep learning and random forests will be appropriate. For other tasks, simple algorithms will perform just as well or even better than complex algorithms, while providing meaningful insights that otherwise would have been buried in a mountain of ‘big data’. We hope that, for those tasks, FFTrees will provide a valuable tool.</p>
</div>
<div id="collaborate-and-contact-us" class="section level3">
<h3>Collaborate and Contact us!</h3>
<p>GitHub: <a href = "https://github.com/ndphillips/ShinyFFTrees"><i class='fa fa-github fa-3x'></i></a> Email: <a href = mailto:Nathaniel.D.Phillips.is@gmail.com?Subject=ShinyFFTrees><i class='fa fa-envelope-o fa-3x'></i></a></p>
<p>We are very interested in collaborations and user feedback on FFTrees. If you use FFTrees for your own data, and have spectacular successes (or failures), or could use a critical new feature, please contact me at Nathaniel.D.Phillips.is@gmail.com, or post an issue on <a href="https://github.com/ndphillips/FFTrees">GitHub</a>.</p>
</div>
</div>
<div id="references" class="section level1">
<h1>References</h1>
<p>Gigerenzer, G., &amp; Brighton, H. (2009). Homo heuristicus: Why biased minds make better inferences. Topics in cognitive science, 1(1), 107-143.</p>
<p>Martignon, L., Katsikopoulos, K. V., &amp; Woike, J. K. (2008). Categorization with limited resources: A family of simple heuristics. Journal of Mathematical Psychology, 52(6), 352–361.</p>
<p>Phillips, N. D., Neth, H., Woike, J. K., &amp; Gaissmaier, W. (2017). FFTrees: A toolbox to create, visualize, and evaluate fast-and-frugal decision trees. Judgment and Decision Making, 12(4), 344-368.</p>
<p>Quinlan, J. R. (1987). Simplifying decision trees. International journal of man-machine studies, 27(3), 221-234.</p>
<p>Wolpert, D. H. (1996). The existence of a priori distinctions between learning algorithms. Neural Computation, 8(7), 1391–1420.</p>
</div>
</section>
