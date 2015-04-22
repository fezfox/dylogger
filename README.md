# dylogger


dylogger.rb is a ruby script for automatic generation of **DayOne** entries. This can be useful for **lifelogging**.

When correctly setup up it can collate data from multiple sources into either "streamed" or "single" DayOne posts.

It allows you to look back at your journal and think:

 *"Oh, I was reading that book back then, and listening to those songs. This is what I posted on Instagram, this is how many photos I took with my phone, this is a movie I watched."*

It is inspired by [siffter](http://craigeley.com/01-07-2014/sifttter-an-ifttt-to-day-one-logger/) by Craig Eley and [Gifttdy](http://giftttdy.gadgetcoma.com) by GadgetComa. The former is written in ruby, and must be run on a schdule daily, whereas the latter is triggered by hazel. Both write DayOne entries directly into dropbox.

![](/images/ss_dayone.png)


###Overview
1. hazel monitors a folder (it could be anywhere)
2. when a file appears in there, it runs the **dylogger.rb** script
3. the script parses the file and creates a DayOne entry in your Dropbox

![](/images/dylogger_flow.png)

###Installation
* Place the dylogger.rb script wherever you like. It needs to be given permissioon to be executable. So you need to navigate to itslocation using terminal and then excute
    chmod +x dylogger.rb

    (Ruby is installed by default in OSX Mavericks and Yosemite. If ou avhe an older version of OSX you will need to isntall ruby)
* Decide where your text and json files will be located. I use ~/Dropbox/Apps/IFTTT/dylogger but could be anywear
* Setup hazel rules for this folder for txt and json files

![](/images/ss_hazel_1.png)

![](/images/ss_hazel_2.png)

###File types
Currently, it can process two types of files
1. text files, in the format used by giftttdy (more about this later)
2. json files - currently only those produced by the iOS app [reporter](http://reporterapp.com)

###File Sources
The text files can come from many sources. Presently I generate them via [IFTTT](http://ifttt.com) from a variety of triggers, and I also create them using [Workflow](http://workflowapp.com) and iOS app that can be used to do a whole range of things. I use it to create entries for movies I watch, and to enter my weight. It produces text files in dropbox that can then be parsed by **dylogger.rb**.

IFTTT can be used to create entries such as music tracks played on spotify (via track "scrobbling" performed by [last.fm](http://last.fom), books read on [GoodReads](http://goodreads.com) and much more.

###Text file formats
One of the strengths of dylogger is that you can use a multitude of sources to create the structured text files it works on (and hopefully in the future, json files). You simply need to know the format, and get your source to produce the correctly formatted output.

The text files contain 6 pieces of data, separated by three "pipes" |||. For example:

    Instagram Post|||Instagram|||April 13, 2015 at 02:52PM||| http://ift.tt/1IC7AZx |||Homemade friands|||Single

These pieces of data are
1. The title of the "stream" that will be created (more later)
2. tag for the DayOne entry
3. date of the post
4. an image (or "NOPIC")
5. title of the entry
6. whether its a "stream" or a "single" entry

###Stream vs Single
If the final field is "TRUE" (legacy from gifttdy) or "stream", then dylogger will search for an existing entry for the day, and add it to the day's "lifestream", under the title of that stream. If this field is "single" then a new entry will be created for that file. For example, it might make sense for each [Instagram](http://instagram.com) post, with its picture, or each movie, with a full description, to get a single DayOne entry. On the other hand, tracks played on [spotify](http://spotify.com) are better in a list of tracknames in a single post. Of course its up to you how you want to do it. 

###Images
As you may know, DayOne only allows a single image for each entry. Dylogger will use the first image it receives to add to a "stream", but new images will be lost.

###IFTTT recipes
You can find receipes already created by GadgetComa on [IFTTT](https://ifttt.com/recipes/search?q=giftttdy&ac=false) by searching for "giftttdy"
