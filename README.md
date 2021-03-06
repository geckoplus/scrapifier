# Scrapifier

[![Build Status](https://travis-ci.org/tiagopog/scrapifier.svg?branch=master)](https://travis-ci.org/tiagopog/scrapifier)
[![Code Climate](https://codeclimate.com/github/tiagopog/scrapifier.png)](https://codeclimate.com/github/tiagopog/scrapifier)
[![Dependency Status](https://gemnasium.com/tiagopog/scrapifier.svg)](https://gemnasium.com/tiagopog/scrapifier)
[![Gem Version](https://badge.fury.io/rb/scrapifier.svg)](http://badge.fury.io/rb/scrapifier)

It's a Ruby gem that brings a very simple way to extract meta information from URIs using the screen scraping technique.

Note: This gem is mainly focused on screen scraping URLs (presence of protocol, such as: "http", "https" and "ftp"), but it also works with URIs which have the "www" without any protocol defined, like: "www.google.com".

## Installation

Compatible with Ruby 1.9.3+

Add this line to your application's Gemfile:

    gem 'scrapifier'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install scrapifier

An then require the gem:

    $ require 'scrapifier'

## Usage

The String#scrapify method finds URIs in a string and then gets their metadata, e.g., the page's title, description, images, keywords, language, encode, "reply to" email, author and URI. All the data is returned in a well-formatted hash.

#### Default usage.

``` ruby
'Wow! What an awesome site: http://adtangerine.com!'.scrapify
#=> {
#   title: "AdTangerine | Boosting great ideas",
#   description: "Advertising social network that uses tangerines as a virtual currency..." ,
#   keywords: "ad network, ad, advertising, advertiser, publisher, social media",
#   lang: "en-us",
#   encode: "utf-8",
#   reply_to: "sayhello@adtangerine.com",
#   author: "Tiago Guedes, Jonatas de Paula, Raphael da Costa",
#   images: ["http://adtangerine.com/assets/logo_adt_og.png", "http://adtangerine.com/assets/logo_adt_og.png", "http://s3-us-west-2.amazonaws.com/adtangerine-prod/users/avatars/000/000/834/thumb/275747_1118382211_1929809351_n.jpg", "http://adtangerine.com/assets/foobar.gif"],
#   uri: "http://adtangerine.com"
# }
```

#### Allow only certain image types.

``` ruby
'Wow! What an awesome site: http://adtangerine.com!'.scrapify(images: :jpg)
#=> {
#   title: "AdTangerine | Boosting great ideas",
#   description: "Advertising social network that uses tangerines as a virtual currency..." ,
#   keywords: "ad network, ad, advertising, advertiser, publisher, social media",
#   lang: "en-us",
#   encode: "utf-8",
#   reply_to: "sayhello@adtangerine.com",
#   author: "Tiago Guedes, Jonatas de Paula, Raphael da Costa",
#   images: ["http://s3-us-west-2.amazonaws.com/adtangerine-prod/users/avatars/000/000/834/thumb/275747_1118382211_1929809351_n.jpg"],
#   uri: "http://adtangerine.com"
# }

'Wow! What an awesome site: http://adtangerine.com!'.scrapify(images: [:png, :gif])
#=> {
#   title: "AdTangerine | Boosting great ideas",
#   description: "Advertising social network that uses tangerines as a virtual currency..." ,
#   keywords: "ad network, ad, advertising, advertiser, publisher, social media",
#   lang: "en-us",
#   encode: "utf-8",
#   reply_to: "sayhello@adtangerine.com",
#   author: "Tiago Guedes, Jonatas de Paula, Raphael da Costa",
#   images: ["http://adtangerine.com/assets/logo_adt_og.png", "http://adtangerine.com/assets/logo_adt_og.png", "http://adtangerine.com/assets/foobar.gif"],
#   uri: "http://adtangerine.com"
# }
```

#### Choose which URI you want it to be scraped.

``` ruby
'Check out: http://adtangerine.com and www.twitflink.com'.scrapify(which: 1)
#=> {
#   title: "TwitFlink | Find a link!",
#   description: "TwitFlink is a very simple searching tool that allows people to find out links tweeted...",
#   keywords: "search, searching tool, link, twitter, social media",
#   lang: "en-us",
#   encode: "utf-8",
#   reply_to: "sayhello@adtangerine.com",
#   author: "Tiago Guedes",
#   images: ["http://www.twitflink.com//assets/tf_logo.png", "http://twitflink.com/assets/tf_logo.png"],
#   uri: "http://www.twitflink.com"
# }

'Check out: http://adtangerine.com and www.twitflink.com'.scrapify(which: 0, images: :gif)
#=> {
#   title: "AdTangerine | Boosting great ideas",
#   description: "Advertising social network that uses tangerines as a virtual currency..." ,
#   keywords: "ad network, ad, advertising, advertiser, publisher, social media",
#   lang: "en-us",
#   encode: "utf-8",
#   reply_to: "sayhello@adtangerine.com",
#   author: "Tiago Guedes, Jonatas de Paula, Raphael da Costa",
#   images: ["http://adtangerine.com/assets/foobar.gif"],
#   uri: "http://adtangerine.com"
# }
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
