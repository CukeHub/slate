---
title: API Reference

language_tabs:
  - ruby

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction
Welcome to the CukeHub API! 

CukeHub is the endpoint for all of your Cucumber Scenarios.  

Store and Share your Cuke Results at CukeHub.

# CukeHub API
### HTTP Request
`POST https://cukehub.com/api/v1/results`
## Parameters

Parameter         | Description
---------         | -----------
<b>api_key:</b>   | API Key generated in your CukeHub App.
<b>name:</b>      | Cucumber Scenario Name.
<b>steps:</b>     | Cucumber Scenario Steps.
<b>location:</b>  | Cucumber Feature File Path.
<b>tag:</b>       | Cucumebr Tag(s) associated with the Cucumber Scenario.
<b>status:</b>    | Cucumber Scenario Status at Runtime [PASSED, FAILED, PENDING]
<b>machine:</b>   | Machine or Device that executed the Cucumber Scenario.
<b>os:</b>        | Operating System the Cucumber Scenario was executed in. [OSX, LINUX, WINDOWS]
<b>runtime:</b>   | Total Runtime of the Cucumber Scenario.
<b>branch:</b>    | The git branch the Cucumber Scenario ran in.
<b>sha:</b>       | The git SHA the Cucumber Scenario ran in.
<b>browser:</b>   | The brower the Scenario ran in for a Browser Integration Test.
<b>domain:</b>    | The domain the Scenario ran against for a Browser Integration Test. 
<b>exception:</b> | The Exception Error for a FAILED Cuke.

# Get Started with Ruby

``` ruby
#features/support/env.rb
require 'cukehub'

Before do
  @cukehub_api_key = '<api_key>'
  #@browser = 'Set @browser in order to see Browser Results at CukeHub'
  #@domain = 'Set @domain in order to see Test Domain at CukeHub'
end


```
 Step    | Description
--------- | -----------
	1.	  | Install the [CukeHub](https://rubygems.org/gems/cukehub) RubyGem or add `gem 'cukehub'` to your Gemfile
	2.    | `$ bundle install`
    3.    | Create a New <b>App</b> at [cukehub.com/apps](https://cukehub.com/apps).
	4.    | Copy the <b>api_key</b> for the <b>App</b>.
	5.    | Add `require 'cukehub'` to your features/support/env.rb.
	6.    | Paste `@cukehub_api_key = <api_key>` into your features/support/env.rb file <b>Before Hook</b>.
	7.    | Run your Cukes`$ cucumber`
	8.    | See your Cuke Results at [cukehub.com/apps](https://cukehub.com/apps).
	9.    | Invite your Team and Share Results.

<aside class="success">
Happy Cuking!
</aside>


