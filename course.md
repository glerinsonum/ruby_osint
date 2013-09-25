# Ruby Open Source Intelligence (OSINT)

## Introduction


### Required Rubygems

#### gem install whois
```bash
$ gem install whois
```
#### gem install nokogiri
```bash
gem install nokogiri
```

#### Requiring gems

```ruby
1.9.3-p392 :002 > require 'resolv'
 => true 
1.9.3-p392 :004 > require 'nokogiri'
 => true 
1.9.3-p392 :007 > require 'whois'
 => true 
```

#### Whois lookup by domain

```ruby
1.9.3-p392 :008 > w = Whois::Client.new
 => #<Whois::Client:0x007fe7c22f0088 @timeout=10, @settings={}> 
1.9.3-p392 :009 > w.lookup('google.com')
 =>  ...
```
#### Whois lookup by IP Address
```ruby
1.9.3-p392 :010 > w = Whois::Client.new
 => #<Whois::Client:0x007fe7c22f0088 @timeout=10, @settings={}> 
1.9.3-p392 :011 > w.lookup('8.8.8.8')
 =>  ...
```

#### Using Nokogiri

##### Fetching a webpage

```ruby
1.9.3-p392 :032 > require 'open-uri'
 => true 
1.9.3-p392 :033 > require 'nokogiri'
 => false 
1.9.3-p392 :034 > doc = Nokogiri::HTML(open('http://www.linkedin.com/in/janedoe'))
```

##### Retrieving Elements
```ruby
1.9.3-p392 :038 > doc.css('span.given-name').text
 => "Jane" 
1.9.3-p392 :039 > doc.css('span.family-name').text
 => "Doe"
1.9.3-p392 :048 > doc.css('span.locality').text.strip
 => "Brooklyn, New York" 
```

##### Retrieving PGP email addresses

First we create a ```fetch_pgp``` which fetch URL and places response in Nokogiri objects.
```ruby
1.9.3-p392 :181 > def fetch_pgp(domain)
1.9.3-p392 :182?>   Nokogiri::HTML(open("http://pgp.mit.edu:11371/pks/lookup?search=#{domain}&op=index&exact=on"))
1.9.3-p392 :183?> end
```
