!SLIDE 
# Ruby Poetry
## Andrew McDonough
## Co-founder and CTO, Tribesports
### Twitter: @andrewmcdonough
# <img src='file/images/tribesports.png'>

!SLIDE center
# Burns night
<img src='file/images/burns.jpg' />

!SLIDE center
# Good 
<img src='file/images/haggis.jpg'/>

!SLIDE center
# Bad
<img src='file/images/email.png' width = '100%'/>

!SLIDE
# What do poetry and programming <br/> have in common?

!SLIDE 
# Poetry Design Patterns
* Alliteration
* Assonance
* Iambic pentameter
* Sonnet
* Haiku

!SLIDE
# The rhyming couplet
## Western poetry's 'singleton'

!SLIDE
# What is a rhyming couplet
    @@@ Ruby
    def couplet?(a,b)
      a[-3,3] == b[-3,3]
    end 

!SLIDE
# Get the feed list
    @@@ Ruby
    fh = open("feeds.txt")
    feeds = fh.read.split "\n"

    # Create an array to store the headlines
    headlines = []

!SLIDE
# Headlines for each feed
    @@@ Ruby
    require 'rss'
    require 'open-uri'

!SLIDE 
    @@@ Ruby
    feeds.each do |feed|
      begin      
        file = open(feed)
        rss = RSS::Parser.parse(file.read) 
        feed_headlines = rss.items.map { |i| 
          i.title
        }
        headlines += feed_headlines 
      rescue
        puts "Error reading #{feed}"
      end
    end 

!SLIDE
# No need to compare every combination
    @@@ Ruby
    headlines.reject! { |h| 
      h.length < 10
    }

    headlines.sort! { |a,b| 
      a[-3,3] <=> b[-3,3]
    }

!SLIDE
# Check each pair in order for matches
    @@@ Ruby
    i = 0
    while (i < headlines.length-1) do
      a = headlines[i]
      b = headlines[i+1]
      if couplet?(a,b)
        i += 1
        puts "#{a}\n#{b}\n\n"
      end
      i += 1
    end

!SLIDE
# Problem: Repetition
## Chris Huhne may be charged within weeks
## Huhne may be charged within weeks

!SLIDE
# Anti-repetition couplets
    @@@ Ruby
    def couplet?(a,b)
      a[-3,3] == b[-3,3]
        && !(a[-5,5] == b[-5,5])
    end 

!SLIDE
# Approximate metre matching
    @@@ Ruby 
    def couplet?(a,b)
      a[-3,3] == b[-3,3] &&
        !(a[-5,5] == b[-5,5]) &&
        (a.length - b.length).abs < 10 &&
        (a.length > 30 && a.length < 70) &&
        (b.length > 30 && b.length < 70)
    end

!SLIDE
# Did it pass the Turing Test?

!SLIDE
# <div class='massive'>YES!</div>

!SLIDE
# Today's generated rhyming couplets

!SLIDE
# Thanks
## Andrew McDonough
### Twitter: @andrewmcdonough
## Tribesports is hiring
# <img src='file/images/tribesports.png'>


