[gem]: https://rubygems.org/gems/rom-elasticsearch
[travis]: https://travis-ci.org/rom-rb/rom-elasticsearch
[codeclimate]: https://codeclimate.com/github/rom-rb/rom-elasticsearch
[inchpages]: http://inch-ci.org/github/rom-rb/rom-elasticsearch
[chat]: https://rom-rb.zulipchat.com

# rom-elasticsearch [![Join the chat at https://rom-rb.zulipchat.com](https://img.shields.io/badge/rom--rb-join%20chat-942283.svg)][chat]

[![Gem Version](https://badge.fury.io/rb/rom-elasticsearch.svg)][gem]
[![Build Status](https://travis-ci.org/rom-rb/rom-elasticsearch.svg?branch=master)][travis]
[![Code Climate](https://codeclimate.com/github/rom-rb/rom-elasticsearch/badges/gpa.svg)][codeclimate]
[![Test Coverage](https://codeclimate.com/github/rom-rb/rom-elasticsearch/badges/coverage.svg)][codeclimate]
[![Inline docs](http://inch-ci.org/github/rom-rb/rom-elasticsearch.svg?branch=master)][inchpages]

Elasticsearch support for [rom-rb](https://github.com/rom-rb/rom).

Resources:

- [User Documentation](http://rom-rb.org/learn/elasticsearch/)
- [API Documentation](http://rubydoc.info/gems/rom-elasticsearch)

Changes in this fork:
- Gemspec updated to support latest elasticsearch gems (7.x)
- Possibility to initialize gateway with existing elasticsearch client / http libraries

```ruby
transport_options = {request: { timeout: 60 }} # faraday request timeout, in seconds
host = ENV['ELASTICSEARCH_URL'] ? ENV['ELASTICSEARCH_URL'] : "localhost"
port = ENV['ELASTICSEARCH_PORT'] ? ENV['ELASTICSEARCH_PORT'] : 9200
client = Elasticsearch::Client.new transport_options: transport_options, host: host, port: port, retry_on_failure: true, log: false, trace: false do |f|
  f.use Faraday::Request::Multipart
  f.use Faraday::Request::UrlEncoded
  f.use Faraday::Response::RaiseError

  f.adapter  :typhoeus
end

conf = ROM::Configuration.new(:elasticsearch, client)
```

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'rom-elasticsearch'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install rom-elasticsearch

## License

See `LICENSE` file.
