---
published: false
layout: post
date: 2014-11-17
categories: data
tags: data map election
---

# Making an election map with Google Fusion Tables

I love Google Fusion Tables because they are great at whipping up quick maps and displaying some sort of data. However, they are not the best tool for the job in every situation. So if you're ever unsure of which mapping tool to use, it's probably best to contact the Web Team. And when in doubt, Google.

## Overview

Google Fusion Tables act like an oversimplified database with data vizualization built in. In other words, FT takes tabular data (like Excel files, CSVs or Google Spreadsheets) and creates a database with them. It's not a real database but it's close enough. Then you can take that data and apply it to maps or graphs or charts.

However, please note that once data is in a FT, it is difficult to edit. That is why, as you'll see below, I put all of my data into a Google Spreadsheet before I put it into a FT. This step is not always necessary but if you think the data could be messed up it might be worth it.

Also, note that this tutorial may be more than you need for a simple map. Take only the pieces that you absolutely need and apply them toward your project.

## Getting data

Enough talk, let's get to some data. For this example I'll be using unofficial 2014 election results which can be found on the [Oregon Secretary of State's website](http://oregonvotes.gov/results/2014G/2013928345.html).

You'll notice this data isn't in any file that we can download so we'll have to copy and paste from the HTML table. No problem, just open up Excel or Google Spreadsheets with a new sheet and copy in the table data.

![ft-copy](https://cloud.githubusercontent.com/assets/4853944/4942067/7ba4c19e-65e8-11e4-821e-654d4a8ba57e.gif)

**Note:** I did not pull in the column heads because they do not correspond directly with individual columns. FT needs one column head for each individual column so we can fill those in ourselves.

Go ahead and save that file as a CSV or comma-separated value format. That way it's a smaller file size and you don't have to worry about other people not having Excel. Also, CSV is awesome.

So now you have some data to play with. Go ahead and clean the data ([this may help out with that process](http://newsroom.registerguard.com/data/2014/10/01/data-journalism-primer.markdown)). But if you're following along with the election data it's pretty clean. Now is the time I would normally say to put your data into a Google Spreadsheet but this data is clean and we can skip that step.

## Getting FT

Now we have to install FT since it doesn't come with Google Drive. If you already have FT installed skip this section.

Go to your [Drive](http://drive.google.com) and on the left side click <kbd>Create</kbd> and then click the <kbd>Connect more apps</kbd> button on the bottom. From there a window will pop open and you'll want to search for "Fusion Tables". Click <kbd>Connect</kbd> and install it and accept and stuff. Disregard the warning that it is still "experimental" (it's been like that for years).

Boom. Now if you click <kbd>Create</kbd> you should see "Fusion Tables" as an option.

## Let's make a Fusion Table

Create a new FT. You should be given an option as to upload a file, select a Google Spreadsheet or create an empty fusion table.

![ft-create](https://cloud.githubusercontent.com/assets/4853944/4942704/3aa7bd30-65ee-11e4-902b-277e8d52214c.gif)

Since you have a CSV on your machine you'll want to upload it. Go through the steps and fill in any relevant information (I like to add attribution info from the start but other than that you're on your own).

So now we have data in a FT, now what? I'm going to take this opportunity to talk about geocoding.

### Geocoding

Geocoding is the process by which someone (Google in our case) takes a set of data and has to some how correspond that data to points on a map. It's not easy and historically has been a major concern. Google can geocode the following pretty reliably:

* Latitude and longitude coordinates (44.0519, -123.0867)
* Exact addresses (3500 Chad Drive, Eugene, OR 97408)
* KML geometry (like [this FT with KML geometry of Oregon counties](https://www.google.com/fusiontables/DataSource?docid=1ZN74DtlmOFs3dDPPM6djy3la22ewfZj2xbf9wA))

Being **exact** is imperative because Google has no idea if 123 Main Street is in Oregon or Colorado or England. The other potential issue is that Google does not know what countries or states or counties look like. So in order to colorize shapes (Oregon counties for our example) we have to give it lines to color in. This can be accomplished by using KML geometry that I mentioned above.

Long story short: Google can't read minds so you have to tell it exactly what you want it to do.

## Making the map

So if you have nice data with a column of geocodable data then this is the end of the road for you. You can click the red tab and it should make a map for you. But with the election data, we don't have that. We need to somehow connect geocodable data to our election data.

### Merging tables

To recap, we have a FT with data and the names of the associated counties but we haven't told Google what to map. We only have the names of the counties and Google doesn't know what those mean. There could be multiple Lane Counties across the U.S.

So, we have to go find some KML geometry that Google can understand. Luckily I have found it for you! Click [here](https://www.google.com/fusiontables/DataSource?docid=1ZN74DtlmOFs3dDPPM6djy3la22ewfZj2xbf9wA) for a pre-made FT with KML geometry. Now we need to merge the two tables, your table with data and the table with the geometry.

Go File > Merge... and paste in this URL `https://www.google.com/fusiontables/DataSource?docid=1ZN74DtlmOFs3dDPPM6djy3la22ewfZj2xbf9wA`. Say OK and open the new, merged table. This was done via the county row.

Now, you have the KML geometry (county polygons) and your election data are in the same table. If you're wondering how that was done, Google compares the two table and matches them up based on the specific column you tell it to.

If you click on the Map of Geometry tab you should see a map of counties in Oregon all colored red. If you click on each county you should display the data associated with that account.

![red](https://cloud.githubusercontent.com/assets/4853944/5075732/1f0760da-6e4a-11e4-8193-866d64e85970.png)


## Style the map

Ok, so you have a map that displays data when you click on different counties. That's great but it looks terrible.

Again Google can do this for you if you set it up appropriately.

In the map tab, look on the left hand bar and click <kbd>Change feature styles...</kbd>. In the new window, under polygons click <kbd>Fill color</kbd>, then click <kbd>Buckets</kbd> and set up the buckets as you see fit.

![ft-buckets](https://cloud.githubusercontent.com/assets/4853944/5075874/644275c6-6e4b-11e4-8773-ad42117f173e.gif)

### Marker icon vs. polygon

Some maps need marker icons, in our example we're using polygons. If you're data has specific points like addresses then you'll want to use points and a marker icon.

In our case we want to use polygons though.

### Buckets

Whether you use marker icons or polygons you can use buckets if you need to display a gradient of information. In our case we want to fill in the county polygons to display whether or not the measure passed. With buckets you can pick a column and display the fill color based on the data in that column.

If you have mareker icons you can do the same and simply color the points differently based on the data in the column you want.

**Note:** Using the predefined range in buckets can leave out the low or high end row as is what happened in our example. You may need to slide the low and high values down or up a decimal point or two.

![ft-bucket_range](https://cloud.githubusercontent.com/assets/4853944/5076091/294ee83a-6e4d-11e4-9dfe-c10774886cd2.png)


## Style the info window

Now that the map looks the way you want to you may also want to style the info window to display only the data that you need to show instad of every column.

To do this click <kbd>Change info window...</kbd> and click on the <kbd>Custom</kbd> tab. In here you can adjust the content of the info window with some minor HTML. Each `{columnName}` will display the associated value of that column for that row when shown. For example `{County}` with display `Lane` when Lane County is clicked on.

**Note:** Because Google is layering on a lot of styles, using a lot of HTML or CSS may make the info window act peculiar.

I used the follow code for my info window:

```
<div class='googft-info-window'>
<b>{County} County</b><br>
Yes: {Yes-votes} <b>({Yes-percent})</b><br>
No: {No-votes} <b>({No-percent})</b><br>
</div>
```

Which, for Lane County, translates to:

**Lane County**  
Yes: 82260 **(60.23%)**
No: 54314 **(39.77%)**

### HTML tips

* `<br>` is a line break. Think of it like hitting <kbd>Enter</kbd>.
* `<b>...</b>` are bold tags. Any text within these tags will be bolded.
* `<i>...</i>` are italic tags.

## Publish it

I tidied up the map to look like the following by tweaking the polygon bucket colors and updating the info window code I have above and the finished product looks like this:

![ft-final](https://cloud.githubusercontent.com/assets/4853944/5076333/ffa2b1f4-6e4e-11e4-9b3d-d9a3737f1f95.png)

So now that you have it, how do you get it into your story?

There are a few steps, I'll try to condense them as much as possible.

1. Click <kbd>Share</kbd> and make the FT available to anyone with the link. Click <kbd>Done</kbd>.
1. Click <kbd>Publish</kbd> under the "Map of geometry" tab drop down.
1. Copy the second field labeled "Paste HTML to embed in a website".
1. Open your story in DT. Make sure there is a DT Field called `WebEmbed`. Paste the code in there.
1. Now, this gets a little codey, sorry. Type `<div class="mm">` before the code you just pasted. And type `</div>` after the embed code.
1. One last thing. Look at the code you pasted in and find where it says `<iframe width=...>`. Between `iframe` and `width` type the following `class="embed"` and make sure there is one space on either side of it.
1. Save your story and the map should show up at the bottom of your story.

The final code should look like this:

```
<div class="mm"><iframe class="mm" width="500" height="300" scrolling="no" frameborder="no" src="https://www.google.com/fusiontables/embedviz?q=select+col4%3E%3E1+from+1ystmQ-eu60DrOIQd-UthlezYvs8eci6PFjv1KXAQ&amp;viz=MAP&amp;h=false&amp;lat=45.236637883426994&amp;lng=-123.53144873046875&amp;t=1&amp;z=8&amp;l=col4%3E%3E1&amp;y=2&amp;tmplt=2&amp;hml=KML"></iframe></div>
```

If you want it to show up at the top of your story, follow the above steps except put the code into the WebHTML field.

That should be it! Now you can put maps into all of your stories!

