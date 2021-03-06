---
layout: post
title: Google Home A/C Azure How to join this cutting edge tech
date: 2018-01-17 13:00:38.000000000 +13:00
type: post
parent_id: '0'
published: true
status: publish
categories: [Azure]
tags: [Azure, Javascript]
# meta:
#   _edit_last: '1'
#   mashsb_timestamp: '1588847288'
#   _yoast_wpseo_content_score: '90'
#   mashsb_twitter_handle: willsam100
#   _yoast_wpseo_primary_category: '54'
#   mashsb_shares: '3'
#   mashsb_jsonshares: '{"total":3,"error":"","facebook_shares":0,"twitter":3,"facebook_total":0,"facebook_likes":0,"facebook_comments":0}'
#   mashsb_shorturl: http://www.codingwithsam.com/google-home-c-azure-join-cutting-edge-tech/
#   dsq_thread_id: '6419032798'
#   mashsb_og_image: '389'
# author:
#   login: sam
#   email: willsam100@gmail.com
#   display_name: Sam Williams
#   first_name: Sam
#   last_name: Williams
permalink: "/2018/01/17/google-home-c-azure-join-cutting-edge-tech/"
---
<img src="{{ site.baseurl }}/assets/img/GoogleMini.jpg" alt="Google Home Mini" title="Google Home Mini" />
This post is a holiday post and not what I normally post about. But I think it's well worth the read as the cool tech should make up for missing F#/mobile apps content.

During the holidays, my wife got me a Google Home Mini Speaker! I also have a heat pump (A/C unit) that is connected to Wi-Fi, with an app. Unfortunately they both don't talk to each other out of the box, so I thought a fun exercise would be for me to wire them up to talk to each other.
The first step is to see if I can programatically control the heat pump.

## Step 1: Talk to heat pump in code
A Google search turned up a <a href="https://github.com/lennyby93/node-mmcontrol">javascript project</a>, that appeared to do most of the required functions.

I tested it out locally via npm install and a node REPL, for some interactive coding.

After entering my credentials and trying out a few commands it appears the library works perfectly and achieve everything that I need.
Here was the code for the first test:
<table class="pre">
<tr>
<td class="lines">
<pre class="fssnip"><span class="l"> 1: </span>
<span class="l"> 2: </span>
<span class="l"> 3: </span>
<span class="l"> 4: </span>
<span class="l"> 5: </span>
<span class="l"> 6: </span>
<span class="l"> 7: </span>
<span class="l"> 8: </span>
<span class="l"> 9: </span>
<span class="l">10: </span>
<span class="l">11: </span>
<span class="l">12: </span>
<span class="l">13: </span>
<span class="l">14: </span>
<span class="l">15: </span>
<span class="l">16: </span>
<span class="l">17: </span>
<span class="l">18: </span>
<span class="l">19: </span>
</pre>
</td>
<td class="snippet">
<pre class="fssnip highlighted"><code lang="fsharp"><span class="id">var</span> <span class="id">MMcontrol</span> <span class="o">=</span> <span class="id">require</span><span class="pn">(</span><span class="id">&#39;</span><span class="id">mmcontrol&#39;</span><span class="pn">)</span><span class="pn">;</span>

<span class="id">var</span> <span class="id">controller</span> <span class="o">=</span> <span class="k">new</span> <span class="id">MMcontrol</span><span class="pn">(</span><span class="pn">{</span>
    <span class="id">&#39;</span><span class="id">username&#39;</span><span class="pn">:</span> <span class="id">&#39;</span><span class="id">username</span><span class="id">@</span><span class="id">domain</span><span class="pn">.</span><span class="id">com&#39;</span><span class="pn">,</span>
    <span class="id">&#39;</span><span class="id">password&#39;</span><span class="pn">:</span> <span class="id">&#39;</span><span class="id">mypassword&#39;</span>
<span class="pn">}</span><span class="pn">)</span><span class="pn">;</span>

<span class="id">controller</span><span class="pn">.</span><span class="id">connect</span><span class="pn">(</span><span class="k">true</span><span class="pn">,</span> <span class="k">function</span> <span class="pn">(</span><span class="id">err</span><span class="pn">)</span> <span class="pn">{</span>
    <span class="k">if</span> <span class="pn">(</span><span class="id">err</span><span class="pn">)</span> <span class="pn">{</span>
        <span class="id">console</span><span class="pn">.</span><span class="id">log</span><span class="pn">(</span><span class="s">&quot;couldn&#39;t connect: &quot;</span> <span class="o">+</span> <span class="id">err</span><span class="pn">)</span><span class="pn">;</span>
    <span class="pn">}</span> <span class="k">else</span> <span class="pn">{</span>
        <span class="id">controller</span><span class="pn">.</span><span class="id">setMode</span><span class="pn">(</span><span class="n">0</span><span class="pn">,</span> <span class="id">&#39;</span><span class="id">cool&#39;</span><span class="pn">,</span> <span class="k">function</span> <span class="pn">(</span><span class="id">err</span><span class="pn">)</span> <span class="pn">{</span>
        <span class="k">if</span> <span class="pn">(</span><span class="id">err</span><span class="pn">)</span> <span class="pn">{</span>
            <span class="id">console</span><span class="pn">.</span><span class="id">log</span><span class="pn">(</span><span class="s">&quot;couldn&#39;t set the mode: &quot;</span> <span class="o">+</span> <span class="id">err</span><span class="pn">)</span>
        <span class="pn">}</span> <span class="k">else</span> <span class="pn">{</span>
            <span class="id">console</span><span class="pn">.</span><span class="id">log</span><span class="pn">(</span><span class="s">&quot;mode set&quot;</span><span class="pn">)</span><span class="pn">;</span>
        <span class="pn">}</span>
        <span class="pn">}</span><span class="pn">)</span><span class="pn">;</span>
    <span class="pn">}</span><span class="pn">)</span><span class="pn">;</span>
</code></pre>
</td>
</tr>
</table>
Step one is now complete.

## Step 2: Make a simple Google Home app
Google has some great documentation on this with <a href="https://developers.google.com/actions/dialogflow/first-app">a tutorial</a>. The tutorial will have you create an app called Silly Name Maker.

Most of the required setup uses the tool titled DialogFlow.

The tutorial creates a Google Assistant app that changes your name. The code is in Javascript and hosted with Google's Firebase (Cloud Platform).
I followed that tutorial and most things worked. There was one thing that I did have a problem with, which was that the firebase init method did not create the required files.

To get around this you can add a folder titled <code>functions</code>, and then create the two files in the folder <code>index.js</code> and <code>package.json</code>.

<img src="{{ site.baseurl }}/assets/img/Screen-Shot-2018-01-11-at-8.03.45-PM.png" alt="Folder Structure" title="Folder Structure" />

## Step 3: Connecting the dots
It's now time to update the cloud function to talk to the heat pump.

I left the intents the same as the Silly Name Maker app (I reused the code from the tutorial in Step 2), since that was not important at this stage.

For proof-of-concept I just wanted to do the simplest thing possible, by testing the architecture. So when the Firebase API is called, I hard-coded it set the heat pump to cool. This test will check that each component can talk to each other: ie DialogFlow -&gt; Firebase -&gt; Heat Pump.

<img src="{{ site.baseurl }}/assets/img/HardCodeAllThe.png" alt="Hard code all the things" title="Hard code all the things" width="200" height="200" align="middle" />

The rest of the code was the same as the local test:
<table class="pre">
<tr>
<td class="lines">
<pre class="fssnip"><span class="l"> 1: </span>
<span class="l"> 2: </span>
<span class="l"> 3: </span>
<span class="l"> 4: </span>
<span class="l"> 5: </span>
<span class="l"> 6: </span>
<span class="l"> 7: </span>
<span class="l"> 8: </span>
<span class="l"> 9: </span>
<span class="l">10: </span>
<span class="l">11: </span>
<span class="l">12: </span>
<span class="l">13: </span>
<span class="l">14: </span>
<span class="l">15: </span>
<span class="l">16: </span>
<span class="l">17: </span>
<span class="l">18: </span>
<span class="l">19: </span>
<span class="l">20: </span>
<span class="l">21: </span>
<span class="l">22: </span>
<span class="l">23: </span>
<span class="l">24: </span>
<span class="l">25: </span>
<span class="l">26: </span>
<span class="l">27: </span>
<span class="l">28: </span>
<span class="l">29: </span>
<span class="l">30: </span>
<span class="l">31: </span>
<span class="l">32: </span>
<span class="l">33: </span>
<span class="l">34: </span>
<span class="l">35: </span>
<span class="l">36: </span>
<span class="l">37: </span>
<span class="l">38: </span>
<span class="l">39: </span>
<span class="l">40: </span>
</pre>
</td>
<td class="snippet">
<pre class="fssnip highlighted"><code lang="fsharp"><span class="id">process</span><span class="pn">.</span><span class="id">env</span><span class="pn">.</span><span class="id">DEBUG</span> <span class="o">=</span> <span class="id">&#39;</span><span class="id">actions</span><span class="o">-</span><span class="id">on</span><span class="o">-</span><span class="id">google</span><span class="pn">:</span><span class="pn">*</span><span class="id">&#39;</span><span class="pn">;</span>
<span class="k">const</span> <span class="id">App</span> <span class="o">=</span> <span class="id">require</span><span class="pn">(</span><span class="id">&#39;</span><span class="id">actions</span><span class="o">-</span><span class="id">on</span><span class="o">-</span><span class="id">google&#39;</span><span class="pn">)</span><span class="pn">.</span><span class="id">DialogflowApp</span><span class="pn">;</span>
<span class="k">const</span> <span class="id">MMcontrol</span> <span class="o">=</span> <span class="id">require</span><span class="pn">(</span><span class="id">&#39;</span><span class="id">mmcontrol&#39;</span><span class="pn">)</span><span class="pn">;</span>
<span class="k">const</span> <span class="id">functions</span> <span class="o">=</span> <span class="id">require</span><span class="pn">(</span><span class="id">&#39;</span><span class="id">firebase</span><span class="o">-</span><span class="id">functions&#39;</span><span class="pn">)</span><span class="pn">;</span>

<span class="id">exports</span><span class="pn">.</span><span class="id">sillyNameMaker</span> <span class="o">=</span> <span class="id">functions</span><span class="pn">.</span><span class="id">https</span><span class="pn">.</span><span class="id">onRequest</span><span class="pn">(</span><span class="pn">(</span><span class="id">request</span><span class="pn">,</span> <span class="id">response</span><span class="pn">)</span> <span class="o">=&gt;</span> <span class="pn">{</span>
    <span class="k">const</span> <span class="id">app</span> <span class="o">=</span> <span class="k">new</span> <span class="id">App</span><span class="pn">(</span><span class="pn">{</span><span class="id">request</span><span class="pn">,</span> <span class="id">response</span><span class="pn">}</span><span class="pn">)</span><span class="pn">;</span>
    <span class="id">console</span><span class="pn">.</span><span class="id">log</span><span class="pn">(</span><span class="id">&#39;</span><span class="id">Request</span> <span class="id">headers</span><span class="pn">:</span> <span class="id">&#39;</span> <span class="o">+</span> <span class="id">JSON</span><span class="pn">.</span><span class="id">stringify</span><span class="pn">(</span><span class="id">request</span><span class="pn">.</span><span class="id">headers</span><span class="pn">)</span><span class="pn">)</span><span class="pn">;</span>
    <span class="id">console</span><span class="pn">.</span><span class="id">log</span><span class="pn">(</span><span class="id">&#39;</span><span class="id">Request</span> <span class="id">body</span><span class="pn">:</span> <span class="id">&#39;</span> <span class="o">+</span> <span class="id">JSON</span><span class="pn">.</span><span class="id">stringify</span><span class="pn">(</span><span class="id">request</span><span class="pn">.</span><span class="id">body</span><span class="pn">)</span><span class="pn">)</span><span class="pn">;</span>

    <span class="id">var</span> <span class="id">controller</span> <span class="o">=</span> <span class="k">new</span> <span class="id">MMcontrol</span><span class="pn">(</span><span class="pn">{</span>
        <span class="id">&#39;</span><span class="id">username&#39;</span><span class="pn">:</span> <span class="id">&#39;</span><span class="id">username</span><span class="id">@</span><span class="id">domain</span><span class="pn">.</span><span class="id">com&#39;</span><span class="pn">,</span>
        <span class="id">&#39;</span><span class="id">password&#39;</span><span class="pn">:</span> <span class="id">&#39;</span><span class="id">mypassword&#39;</span><span class="pn">,</span> 
        <span class="id">&#39;</span><span class="id">persistence&#39;</span><span class="pn">:</span> <span class="k">false</span>
    <span class="pn">}</span><span class="pn">)</span><span class="pn">;</span>

    <span class="k">function</span> <span class="id">makeName</span> <span class="pn">(</span><span class="id">app</span><span class="pn">)</span> <span class="pn">{</span>
        <span class="id">controller</span><span class="pn">.</span><span class="id">connect</span><span class="pn">(</span><span class="k">true</span><span class="pn">,</span> <span class="k">function</span> <span class="pn">(</span><span class="id">err</span><span class="pn">)</span> <span class="pn">{</span>
            <span class="k">if</span> <span class="pn">(</span><span class="id">err</span><span class="pn">)</span> <span class="pn">{</span>
                <span class="id">console</span><span class="pn">.</span><span class="id">log</span><span class="pn">(</span><span class="s">&quot;couldn&#39;t connect: &quot;</span> <span class="o">+</span> <span class="id">err</span><span class="pn">)</span><span class="pn">;</span>
            <span class="pn">}</span> <span class="k">else</span> <span class="pn">{</span>
                <span class="id">console</span><span class="pn">.</span><span class="id">log</span><span class="pn">(</span><span class="s">&quot;connection established&quot;</span><span class="pn">)</span><span class="pn">;</span>
                <span class="id">controller</span><span class="pn">.</span><span class="id">setMode</span><span class="pn">(</span><span class="n">0</span><span class="pn">,</span> <span class="id">&#39;</span><span class="id">cool&#39;</span><span class="pn">,</span> <span class="k">function</span> <span class="pn">(</span><span class="id">err</span><span class="pn">)</span> <span class="pn">{</span>
                <span class="k">if</span> <span class="pn">(</span><span class="id">err</span><span class="pn">)</span> <span class="pn">{</span>
                    <span class="id">console</span><span class="pn">.</span><span class="id">log</span><span class="pn">(</span><span class="s">&quot;couldn&#39;t set the mode: &quot;</span> <span class="o">+</span> <span class="id">err</span><span class="pn">)</span>
                    <span class="id">app</span><span class="pn">.</span><span class="id">tell</span><span class="pn">(</span><span class="id">&#39;</span><span class="id">Oh</span> <span class="id">no!</span> <span class="id">There</span> <span class="id">was</span> <span class="id">an</span> <span class="id">error</span><span class="pn">.</span> <span class="id">Please</span> <span class="k">try</span> <span class="id">again&#39;</span><span class="pn">)</span><span class="pn">;</span>
                <span class="pn">}</span> <span class="k">else</span> <span class="pn">{</span>
                    <span class="id">console</span><span class="pn">.</span><span class="id">log</span><span class="pn">(</span><span class="s">&quot;mode set&quot;</span><span class="pn">)</span><span class="pn">;</span>
                    <span class="id">app</span><span class="pn">.</span><span class="id">tell</span><span class="pn">(</span><span class="id">&#39;</span><span class="id">Alright</span><span class="pn">,</span> <span class="id">I</span> <span onmouseout="hideTip(event, 'fs1', 1)" onmouseover="showTip(event, 'fs1', 1)" class="id">set</span> <span class="id">your</span> <span class="id">heat</span> <span class="id">pump</span> <span class="k">to</span> <span class="id">cool&#39;</span><span class="pn">)</span><span class="pn">;</span>
                <span class="pn">}</span>
                <span class="pn">}</span><span class="pn">)</span><span class="pn">;</span>
            <span class="pn">}</span>
        <span class="pn">}</span><span class="pn">)</span><span class="pn">;</span>
    <span class="pn">}</span>  

    <span class="k">let</span> <span class="id">actionMap</span> <span class="o">=</span> <span class="k">new</span> <span onmouseout="hideTip(event, 'fs2', 2)" onmouseover="showTip(event, 'fs2', 2)" class="id">Map</span><span class="pn">(</span><span class="pn">)</span><span class="pn">;</span>
    <span class="id">actionMap</span><span class="pn">.</span><span class="id">set</span><span class="pn">(</span><span class="id">NAME_ACTION</span><span class="pn">,</span> <span class="id">makeName</span><span class="pn">)</span><span class="pn">;</span>

    <span class="id">app</span><span class="pn">.</span><span class="id">handleRequest</span><span class="pn">(</span><span class="id">actionMap</span><span class="pn">)</span><span class="pn">;</span>
<span class="pn">}</span><span class="pn">)</span><span class="pn">;</span>
</code></pre>
</td>
</tr>
</table>
One thing that I noticed when locally testing out the heat pump controller (step 2) was that the session and cookies were saved locally (persistence is on by default). I did not want this to be done on the server, so I set this to be off when creating the controller on the server. To do this, an extra field ```persistence``` was set to false as follows:
<table class="pre">
<tr>
<td class="lines">
<pre class="fssnip"><span class="l">1: </span>
<span class="l">2: </span>
<span class="l">3: </span>
<span class="l">4: </span>
<span class="l">5: </span>
</pre>
</td>
<td class="snippet">
<pre class="fssnip highlighted"><code lang="fsharp"><span class="id">var</span> <span class="id">controller</span> <span class="o">=</span> <span class="k">new</span> <span class="id">MMcontrol</span><span class="pn">(</span><span class="pn">{</span>
    <span class="id">&#39;</span><span class="id">username&#39;</span><span class="pn">:</span> <span class="id">&#39;</span><span class="id">username</span><span class="id">@</span><span class="id">domain</span><span class="pn">.</span><span class="id">com&#39;</span><span class="pn">,</span>
    <span class="id">&#39;</span><span class="id">password&#39;</span><span class="pn">:</span> <span class="id">&#39;</span><span class="id">mypassword&#39;</span><span class="pn">,</span> 
    <span class="id">&#39;</span><span class="id">persistence&#39;</span><span class="pn">:</span> <span class="k">false</span>
<span class="pn">}</span><span class="pn">)</span><span class="pn">;</span>
</code></pre>
</td>
</tr>
</table>
Time to do the test.

### It Failed :(
Nothing happened.
I found and checked the logs for Firebase. A connection exception was thrown and after a quick Google search, and I found out why.
The error was due to the Firebase account being on a free tier, that restricts all external API calls. The next tier (that allows external API calls from Firebase) is $25/month which seems like a high price for a proof of concept (POC)
A new plan is needed! So I decided to replace Firebase with Azure Functions

## Step 4: Creating the Azure Function
I've used Azure functions a little bit before so it seems like the next logical step.
Here's the new plan to make this work.

<img src="{{ site.baseurl }}/assets/img/Screen-Shot-2018-01-11-at-7.50.09-PM.png" alt="Diagram" title="Diagram" />
I thought this would be a simple copy and paste of the code, but there were a few details that I missed.
Creating the function is not too hard (there are many other blog posts on this).

If you don't have an Azure account, create one, for a free trial with $200 credit.
For this Proof-Of-Concept, I don't need the scaling features that Azure Functions offer, so I opted for a free service tier rather than a consumption plan (the consumption plan still gives you a number of API calls that are free, but will scale in event of demand).
I created a Javascript Web-hook Function:
<img src="{{ site.baseurl }}/assets/img/CreateAzureFunction.gif" alt="Create Azure Function" title="Create Azure Function" />
It's now time to add the required bits and pieces to talk to the heat pump.

## Step 5: Talking to the heat pump
I first tried to upload the package.json file (I thought I needed this, as I was planning to use the same libraries).

The first editor did not work that well, but I found the online editor, titled 'App Service Editor', that is much better (It looks like Visual Studio Code)
<img src="{{ site.baseurl }}/assets/img/App-Service-Editor-1.png" alt="App Service Editor" title="App Service Editor" />

I was able to see the upload package.json file (and import the library), but it turned out that I didn't need it.
In the firebase example, an npm package was used with dialogue flow to parse the request and response. It was unclear how to use that with azure, and I didn't want to figure it out.

All I needed was the structure of the response to continue. And the input data as well if the this step works.

<img src="{{ site.baseurl }}/assets/img/22hbwz.jpg" alt="Rewrite" title="Rewrite all the things" width="200" height="200" align="middle" />

At this stage, I only cared about sending the speech text in the response. I found <a href="" title="https://dialogflow.com/docs/fulfillment#section-format-of-request-to-the-service">the docs</a> on how to send the response to Google for the speech.
<table class="pre">
<tr>
<td class="lines">
<pre class="fssnip"><span class="l">1: </span>
<span class="l">2: </span>
<span class="l">3: </span>
<span class="l">4: </span>
<span class="l">5: </span>
<span class="l">6: </span>
<span class="l">7: </span>
<span class="l">8: </span>
</pre>
</td>
<td class="snippet">
<pre class="fssnip highlighted"><code lang="fsharp"><span class="id">Body</span><span class="pn">:</span>
<span class="pn">{</span>
    <span class="s">&quot;speech&quot;</span><span class="pn">:</span> <span onmouseout="hideTip(event, 'fs3', 3)" onmouseover="showTip(event, 'fs3', 3)" class="id">string</span><span class="pn">,</span>
    <span class="s">&quot;displayText&quot;</span><span class="pn">:</span> <span onmouseout="hideTip(event, 'fs3', 4)" onmouseover="showTip(event, 'fs3', 4)" class="id">string</span><span class="pn">,</span>
    <span class="s">&quot;data&quot;</span><span class="pn">:</span> <span class="pn">{</span><span class="o">..</span><span class="pn">.</span><span class="pn">}</span><span class="pn">,</span>
    <span class="s">&quot;contextOut&quot;</span><span class="pn">:</span> <span class="pn">[</span><span class="o">..</span><span class="pn">.</span><span class="pn">]</span><span class="pn">,</span>
    <span class="s">&quot;source&quot;</span><span class="pn">:</span> <span onmouseout="hideTip(event, 'fs3', 5)" onmouseover="showTip(event, 'fs3', 5)" class="id">string</span>
<span class="pn">}</span>
</code></pre>
</td>
</tr>
</table>
I wrapped that in a function as follows:
<table class="pre">
<tr>
<td class="lines">
<pre class="fssnip"><span class="l"> 1: </span>
<span class="l"> 2: </span>
<span class="l"> 3: </span>
<span class="l"> 4: </span>
<span class="l"> 5: </span>
<span class="l"> 6: </span>
<span class="l"> 7: </span>
<span class="l"> 8: </span>
<span class="l"> 9: </span>
<span class="l">10: </span>
<span class="l">11: </span>
<span class="l">12: </span>
<span class="l">13: </span>
<span class="l">14: </span>
<span class="l">15: </span>
</pre>
</td>
<td class="snippet">
<pre class="fssnip highlighted"><code lang="fsharp"><span class="id">var</span> <span class="id">setResponse</span> <span class="o">=</span> <span class="k">function</span> <span class="pn">(</span><span class="id">speech</span><span class="pn">)</span> <span class="pn">{</span>
    <span class="id">context</span><span class="pn">.</span><span class="id">res</span> <span class="o">=</span> 
    <span class="pn">{</span> 
        <span class="id">status</span><span class="pn">:</span> <span class="n">200</span><span class="pn">,</span> 
        <span class="id">body</span><span class="pn">:</span> 
        <span class="pn">{</span>
            <span class="s">&quot;speech&quot;</span><span class="pn">:</span> <span class="id">speech</span><span class="pn">,</span>
            <span class="s">&quot;displayText&quot;</span><span class="pn">:</span> <span class="s">&quot;&quot;</span><span class="pn">,</span>
            <span class="s">&quot;data&quot;</span><span class="pn">:</span> <span class="pn">{</span><span class="pn">}</span><span class="pn">,</span>
            <span class="s">&quot;contextOut&quot;</span><span class="pn">:</span> <span class="pn">[</span><span class="pn">]</span><span class="pn">,</span>
            <span class="s">&quot;source&quot;</span><span class="pn">:</span> <span class="s">&quot;&quot;</span>
        <span class="pn">}</span>
    <span class="pn">}</span><span class="pn">;</span> 
    <span class="id">context</span><span class="pn">.</span><span class="k">done</span><span class="pn">(</span><span class="pn">)</span><span class="pn">;</span>
<span class="pn">}</span>
</code></pre>
</td>
</tr>
</table>
And then copying the code I had before, making the changes to set the response:
<table class="pre">
<tr>
<td class="lines">
<pre class="fssnip"><span class="l"> 1: </span>
<span class="l"> 2: </span>
<span class="l"> 3: </span>
<span class="l"> 4: </span>
<span class="l"> 5: </span>
<span class="l"> 6: </span>
<span class="l"> 7: </span>
<span class="l"> 8: </span>
<span class="l"> 9: </span>
<span class="l">10: </span>
<span class="l">11: </span>
<span class="l">12: </span>
<span class="l">13: </span>
<span class="l">14: </span>
<span class="l">15: </span>
<span class="l">16: </span>
<span class="l">17: </span>
<span class="l">18: </span>
<span class="l">19: </span>
<span class="l">20: </span>
<span class="l">21: </span>
<span class="l">22: </span>
<span class="l">23: </span>
<span class="l">24: </span>
<span class="l">25: </span>
</pre>
</td>
<td class="snippet">
<pre class="fssnip highlighted"><code lang="fsharp"><span class="k">const</span> <span class="id">MMcontrol</span> <span class="o">=</span> <span class="id">require</span><span class="pn">(</span><span class="id">&#39;</span><span class="id">mmcontrol&#39;</span><span class="pn">)</span><span class="pn">;</span>
<span class="k">module</span><span class="pn">.</span><span class="id">exports</span> <span class="o">=</span> <span class="k">function</span> <span class="pn">(</span><span class="id">context</span><span class="pn">,</span> <span class="id">request</span><span class="pn">)</span> <span class="pn">{</span>
    <span class="id">var</span> <span class="id">controller</span> <span class="o">=</span> <span class="k">new</span> <span class="id">MMcontrol</span><span class="pn">(</span><span class="pn">{</span>
        <span class="id">&#39;</span><span class="id">username&#39;</span><span class="pn">:</span> <span class="id">&#39;</span><span class="id">username</span><span class="id">@</span><span class="id">domain</span><span class="pn">.</span><span class="id">com&#39;</span><span class="pn">,</span>
        <span class="id">&#39;</span><span class="id">password&#39;</span><span class="pn">:</span> <span class="id">&#39;</span><span class="id">mypassword&#39;</span><span class="pn">,</span> 
        <span class="id">&#39;</span><span class="id">persistence&#39;</span><span class="pn">:</span> <span class="k">false</span>
    <span class="pn">}</span><span class="pn">)</span><span class="pn">;</span>

    <span class="id">controller</span><span class="pn">.</span><span class="id">connect</span><span class="pn">(</span><span class="k">true</span><span class="pn">,</span> <span class="k">function</span> <span class="pn">(</span><span class="id">err</span><span class="pn">)</span> <span class="pn">{</span>
        <span class="k">if</span> <span class="pn">(</span><span class="id">err</span><span class="pn">)</span> <span class="pn">{</span>
            <span class="id">console</span><span class="pn">.</span><span class="id">log</span><span class="pn">(</span><span class="s">&quot;couldn&#39;t connect: &quot;</span> <span class="o">+</span> <span class="id">err</span><span class="pn">)</span><span class="pn">;</span>
        <span class="pn">}</span> <span class="k">else</span> <span class="pn">{</span>
            <span class="id">console</span><span class="pn">.</span><span class="id">log</span><span class="pn">(</span><span class="s">&quot;connection established&quot;</span><span class="pn">)</span><span class="pn">;</span>
            <span class="id">controller</span><span class="pn">.</span><span class="id">setMode</span><span class="pn">(</span><span class="n">0</span><span class="pn">,</span> <span class="id">&#39;</span><span class="id">cool&#39;</span><span class="pn">,</span> <span class="k">function</span> <span class="pn">(</span><span class="id">err</span><span class="pn">)</span> <span class="pn">{</span>
            <span class="k">if</span> <span class="pn">(</span><span class="id">err</span><span class="pn">)</span> <span class="pn">{</span>
                <span class="id">console</span><span class="pn">.</span><span class="id">log</span><span class="pn">(</span><span class="s">&quot;couldn&#39;t set the mode: &quot;</span> <span class="o">+</span> <span class="id">err</span><span class="pn">)</span>
                <span class="id">setResponse</span><span class="pn">(</span><span class="id">&#39;</span><span class="id">Oh</span> <span class="id">no!</span> <span class="id">There</span> <span class="id">was</span> <span class="id">an</span> <span class="id">error</span><span class="pn">.</span> <span class="id">Please</span> <span class="k">try</span> <span class="id">again&#39;</span><span class="pn">)</span><span class="pn">;</span>
            <span class="pn">}</span> <span class="k">else</span> <span class="pn">{</span>
                <span class="id">console</span><span class="pn">.</span><span class="id">log</span><span class="pn">(</span><span class="s">&quot;mode set&quot;</span><span class="pn">)</span><span class="pn">;</span>
                <span class="id">setResponse</span><span class="pn">(</span><span class="id">&#39;</span><span class="id">Alright</span><span class="pn">,</span> <span class="id">I</span> <span onmouseout="hideTip(event, 'fs1', 6)" onmouseover="showTip(event, 'fs1', 6)" class="id">set</span> <span class="id">your</span> <span class="id">heat</span> <span class="id">pump</span> <span class="k">to</span> <span class="id">cool&#39;</span><span class="pn">)</span><span class="pn">;</span>
            <span class="pn">}</span>
            <span class="pn">}</span><span class="pn">)</span><span class="pn">;</span>
        <span class="pn">}</span>
    <span class="pn">}</span><span class="pn">)</span><span class="pn">;</span>
<span class="pn">}</span>   
</code></pre>
</td>
</tr>
</table>
With this, a test is now possible.
Over the Google Assistant portal, fire off the request, and....

### Success
The heat pump went from heat to cool.

## Step 6: Handle Input
The last part is to handle input, and clean up the code a little bit. The docs contained the details of the input as well, though I just logged request, and then had a look for what I wanted. There were two things that I needed, the action and the parameters. Each could be pulled out of the request body as follows:
<table class="pre">
<tr>
<td class="lines">
<pre class="fssnip"><span class="l">1: </span>
<span class="l">2: </span>
</pre>
</td>
<td class="snippet">
<pre class="fssnip highlighted"><code lang="fsharp"><span class="id">request</span><span class="pn">.</span><span class="id">body</span><span class="pn">.</span><span class="id">result</span><span class="pn">.</span><span class="id">action</span>
<span class="id">request</span><span class="pn">.</span><span class="id">body</span><span class="pn">.</span><span class="id">result</span><span class="pn">.</span><span class="id">parameters</span>
</code></pre>
</td>
</tr>
</table>
The ```action``` contains the string name of the action that was invoked in DialogFlow. I used this for different settings on the heat pump (e.g. one for power on/off, another action for the mode).
The ```parameters``` contains a dictionary of names and values that were invoked on the action. For example, I had <code>Mode</code> with various values such as ```heat``` or ```cool```.
The result looked like this:
<table class="pre">
<tr>
<td class="lines">
<pre class="fssnip"><span class="l"> 1: </span>
<span class="l"> 2: </span>
<span class="l"> 3: </span>
<span class="l"> 4: </span>
<span class="l"> 5: </span>
<span class="l"> 6: </span>
<span class="l"> 7: </span>
<span class="l"> 8: </span>
<span class="l"> 9: </span>
<span class="l">10: </span>
<span class="l">11: </span>
<span class="l">12: </span>
</pre>
</td>
<td class="snippet">
<pre class="fssnip highlighted"><code lang="fsharp"><span class="k">if</span> <span class="pn">(</span><span class="id">request</span><span class="pn">.</span><span class="id">body</span><span class="pn">.</span><span class="id">result</span><span class="pn">.</span><span class="id">action</span> <span class="o">==</span> <span class="id">&#39;</span><span class="id">mode&#39;</span><span class="pn">)</span> <span class="pn">{</span>
    <span class="id">var</span> <span class="id">modeAction</span> <span class="o">=</span> <span class="id">request</span><span class="pn">.</span><span class="id">body</span><span class="pn">.</span><span class="id">result</span><span class="pn">.</span><span class="id">parameters</span><span class="pn">.</span><span class="id">Mode</span><span class="pn">.</span><span class="id">toLowerCase</span><span class="pn">(</span><span class="pn">)</span><span class="pn">;</span>
    <span class="id">context</span><span class="pn">.</span><span class="id">log</span><span class="pn">(</span><span class="id">&#39;</span><span class="id">Action</span> <span class="id">value</span><span class="pn">:</span><span class="id">&#39;</span><span class="pn">,</span> <span class="id">modeAction</span><span class="pn">)</span><span class="pn">;</span>
    <span class="id">perform</span><span class="pn">(</span><span class="id">&#39;</span><span class="id">setMode&#39;</span><span class="pn">,</span> <span class="id">modeAction</span><span class="pn">,</span> <span class="id">&#39;</span><span class="id">That</span> <span class="id">is</span> <span class="k">done</span><span class="pn">.</span> <span class="id">Your</span> <span class="id">heat</span> <span class="id">pump</span> <span class="id">is</span> <span class="id">now</span> <span onmouseout="hideTip(event, 'fs1', 7)" onmouseover="showTip(event, 'fs1', 7)" class="id">set</span> <span class="k">to</span> <span class="id">&#39;</span> <span class="o">+</span> <span class="id">modeAction</span><span class="pn">)</span><span class="pn">;</span>
    
<span class="pn">}</span> <span class="k">else</span> <span class="k">if</span> <span class="pn">(</span><span class="id">request</span><span class="pn">.</span><span class="id">body</span><span class="pn">.</span><span class="id">result</span><span class="pn">.</span><span class="id">action</span> <span class="o">==</span> <span class="id">&#39;</span><span class="id">heat_pump_power&#39;</span><span class="pn">)</span> <span class="pn">{</span>
    <span class="id">var</span> <span class="id">powerAction</span> <span class="o">=</span> <span class="id">request</span><span class="pn">.</span><span class="id">body</span><span class="pn">.</span><span class="id">result</span><span class="pn">.</span><span class="id">parameters</span><span class="pn">.</span><span class="id">HeatPumpPower</span><span class="pn">.</span><span class="id">toLowerCase</span><span class="pn">(</span><span class="pn">)</span><span class="pn">;</span>
    <span class="id">context</span><span class="pn">.</span><span class="id">log</span><span class="pn">(</span><span class="id">&#39;</span><span class="id">Action</span> <span class="id">value</span><span class="pn">:</span><span class="id">&#39;</span><span class="pn">,</span> <span class="id">powerAction</span><span class="pn">)</span><span class="pn">;</span>
    <span class="id">perform</span><span class="pn">(</span><span class="id">&#39;</span><span class="id">setPower&#39;</span><span class="pn">,</span> <span class="id">powerAction</span><span class="pn">,</span> <span class="id">&#39;</span><span class="id">That</span> <span class="id">is</span> <span class="k">done</span><span class="pn">.</span> <span class="id">Your</span> <span class="id">heat</span> <span class="id">pump</span> <span class="id">will</span> <span class="id">turn</span> <span class="id">&#39;</span> <span class="o">+</span> <span class="id">powerAction</span> <span class="o">+</span> <span class="id">&#39;</span> <span class="id">soon&#39;</span><span class="pn">)</span><span class="pn">;</span>

<span class="pn">}</span>
<span class="c">// rest of code</span>
</code></pre>
</td>
</tr>
</table>

## Step 7: Update DialogFlow with the intents and entities
Now that the Azure Function was in place, the last thing left was to update all the values in DialogFlow. Most of them were simple enough to fill out but there was one last part.

## Updating the Intents
This was easy and was just a case of changing the strings. Here is what the final list of intents looks like:
<img src="{{ site.baseurl }}/assets/img/Screen-Shot-2018-01-16-at-12.35.54-PM.png" alt="Intents" title="Intents" />
And here is the the details for the power intent. Note the enum type shown is explained next:
<img src="{{ site.baseurl }}/assets/img/Screen-Shot-2018-01-16-at-12.36.07-PM.png" alt="ModeIntent" title="ModeIntent" />

## Defining enums
The <code>Entities</code> section of DialogFlow is for this, and it is really good. Create a name for the entity eg <code>Mode</code> and then give it some different values: <code>Heat</code>, <code>Cool</code>, <code>Dry</code> etc. I also found that you can defined synonyms. So for <code>heat</code> you can also say <code>warm</code>.
Once all of the following, it was time for the final test. My Javascript skills were a little rusty (along with my typing/spelling), a few attempts latter and it was all working.
<img src="{{ site.baseurl }}/assets/img/Screen-Shot-2018-01-13-at-2.03.19-PM.png" alt="Entities" title="Entities" />

## Wrap up

## Change the name:
i got tired of saying <code>Ok Google, talk to my test app</code> all the time. So changed it.
From DialogFlow click on integrations, and then click on Google Assistant. In the page that pops, it's possible to update the information about the app, and change it's name.

I changed mine to <code>living room aircon</code>. Note that it does not allow a single word for the name.
It was now possible to say <code>Ok Google, ask living room aircon to turn on</code> in one sentence.
