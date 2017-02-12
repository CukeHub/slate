---
title: API Reference

language_tabs:
  - shell
  - ruby

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the CukeHub API! You can use our API to access CukeHub API endpoints, which can get information on your Cucumber Test Results.

We have language bindings in Shell, Ruby, and Python! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.


# RubyGem

## Hooks

```ruby
require 'httparty'
require 'os'

if OS.mac? then
  os = "OSX"
elsif OS.linux?
  os = "Linux"
elsif OS.doze?
  os = "Win"
end

Before do
    @start = Time.now
end

After do |scenario|
  IO.popen("git symbolic-ref --short HEAD") {|pipe| puts @git_branch = pipe.read }
  params = {
    api_key: @cukehub_api_key,
    name:   scenario.name,
    location: scenario.location,
    tag: scenario.source_tag_names,
    status: scenario.status.upcase,
    machine: Socket.gethostname,
    os: os,
    runtime: (Time.now - @start),
    domain: @domain,
    branch: @git_branch.chomp
  }
  params[:browser] = @browser.browser.upcase unless @browser.nil?
  params[:exception]=scenario.exception.message unless scenario.passed?

  HTTParty.post("https://cukehub.com/api/v1/results", body: params)
end   
```

```shell
  params = {
    api_key: <cukehub_api_key>,
    name:   "As a User, I login to CukeHub",
    location: "feature/authentication.feature",
    tag: "@authentication",
    status: PASSED,
    machine: "rich_macbookpro",
    os: "OSX",
    runtime: 20,
    domain: "https://cukehub.com",
    branch: "user_authentication_branch"
	browser: "CHROME"
  }

  HTTParty.post("https://cukehub.com/api/v1/results", body: params)
```


This endpoint captures all the Cukes from all the machines.

### HTTP Request

`POST https://cukehub.com/api/v1/results`

### Query Parameters

Parameter  | Description
---------  | -----------
api_key:   | Stores Cucumber Scenarios and Runs for a specific App at CukeHub.
name:      | Stores the Cucumber Scenario Name.
location:  | Stores the Cucumber Feature File Path.
tag:       | Stores the Cucumebr Tag associated with the Cucumber Scenario.
status:    | Stores the Cucumber Scenario Status at Runtime [PASSED, FAILED, PENDING]
machine:   | Stores the Machine the Cucumber Scenario was executed on. [Socket.gethostname]
os:        | Stores the Operating System the Cucumber Scenario was executed in. [OSX, LINUX, WINDOWS]
runtime:   | Stores the Total Runtime it took for the Cucumber Scenario to complete.
exception: | If the param exists, Stores the Exception Error for a FAILED Cucumber Scenario.
branch:    | If the param exists, Stores the git branch the Scenario ran on.
domain:    | If the param exists, CukeHub stores the domain the Scenario ran against.  [ ex. @domain = staging.cukehub.com ] 
browser:   | If the param exists, CukeHub stores the brower the Scenario ran in. [ ex. @browser = Selenium::WebDriver.for :chrome ]

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

