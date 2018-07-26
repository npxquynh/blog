---
title: "Parse Json"
date: 2018-07-26T15:26:00+02:00
draft: false
---

I usually use 2 ways to parse JSON.

### Oj

[Source code](https://github.com/ohler55/oj)

This one can parse Json really fast.

{{< highlight ruby >}}
require 'oj'

sample = '{"greeting": "hello", "name": "sunflower"}'
Oj.load(sample) # {"greeting"=>"hello", "name"=>"sunflower"}
Oj.load(sample, symbol_keys: true) # {:greeting=>"hello", :name=>"sunflower"}
Oj.load(sample, symbolize_names: true) # {:greeting=>"hello", :name=>"sunflower"}
{{< /highlight >}}

### JSON module from Ruby Stdlib

[Documentation](http://ruby-doc.org/stdlib-2.0.0/libdoc/json/rdoc/JSON.html)

{{< highlight ruby >}}
require 'json'

sample = '{"greeting": "hello", "name": "sunflower"}'
JSON.parse(sample) # {"greeting"=>"hello", "name"=>"sunflower"}
JSON.parse(sample, symbolize_names: true) # {:greeting=>"hello", :name=>"sunflower"}
{{< /highlight >}}

### Benchmark

I use the [Json Placeholder](https://jsonplaceholder.typicode.com/) to get some fake data in Json to measure the performance between `Oj.load` and `JSON.parse`. As shown below, the parsing is way faster with Oj.

{{< highlight ruby >}}
require 'benchmark/ips'
require 'net/http'
require 'oj'
require 'json'

uri = URI('https://jsonplaceholder.typicode.com/photos')
json_response = Net::HTTP.get(uri); nil # Just for suppresing the long output

Benchmark.ips do |x|
  x.report("oj") { Oj.load(json_response) }
  x.report("oj symbol keys") { Oj.load(json_response, symbolize_names: true) }
  x.report("JSON") { JSON.parse(json_response) }
  x.report("JSON symbol keys") { JSON.parse(json_response, symbolize_names: true) }
end
{{< /highlight >}}

```
Warming up --------------------------------------
                  oj     8.000  i/100ms
      oj symbol keys     8.000  i/100ms
                JSON     3.000  i/100ms
    JSON symbol keys     3.000  i/100ms
Calculating -------------------------------------
                  oj     86.352  (± 2.3%) i/s -    432.000  in   5.006384s
      oj symbol keys     87.404  (± 3.4%) i/s -    440.000  in   5.042169s
                JSON     29.249  (±34.2%) i/s -    129.000  in   5.024405s
    JSON symbol keys     38.874  (±20.6%) i/s -    186.000  in   5.033208s
```
