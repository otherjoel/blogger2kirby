blogger2kirby
=============

Python script for moving Blogger blogs (with images and comments) to Kirby CMS. 

Blogger allows you to export your blog as a single large XML file. My script takes this file, parses out just the blog posts and comments, and creates a folder and a text file in Markdown format for each post.

* Any images are downloaded and given a unique filename in the post's folder
* Image links are converted to Kirby format (looks like `(image: image01.jpg)`)
* Comments are appended to the end of each post, with comment author names/links and timestamps
* Tags are preserved in the post's metadata

The resulting folders can simply be dropped into the content folder of a Kirby-based site, and boom: the blog has moved.

## Requirements

The script is in Python 3. I couldn't use v2 because of problems with Unicode data.

[Pandoc](http://johnmacfarlane.net/pandoc/index.html) (version 1.13.1 or later) is also required for the HTML to Markdown conversion process.

The script also requires these libraries:

* `lxml`, for parsing XML
* `BeautifulSoup`, for parsing HTML
* `python-rfc3339`, for parsing Atom timestamps in RFC3339 format (<https://github.com/tonyg/python-rfc3339>)
* `requests`, for downloading images over HTTP

On my Mac running Yosemite, the simplest way to get all these prerequisites was to install Homebrew, then run the following commands:

    brew install python3
    pip3 install git+https://github.com/tonyg/python-rfc3339.git
    pip3 install lxml
    pip3 install beautifulsoup4
    pip3 install requests
    
    brew install pandoc

## Usage

Place your Blogger XML file in the same folder as the script, and name it `blog.xml`. Then run `python3 blogger2kirby.py`. 

You can also run `chmod u+x blogger2kirby.py` to make it executable and then just run it as `./blogger2kirby.py`, assuming your python3 lives in `/usr/local/bin/python3` (if you installed it with Homebrew, that's where it would be).

You will see a lot of messages fly by about the posts being parsed out.

Afterwards there will be a folder named `out` in the current folder, containing a single folder for each post in the format `YYYYMMDD-post-slug` -- the slug will be the same as the filename on the post's original Blogger URI but without the `.html` -- this will allow for easy redirects.

## Acknowledgements

https://gist.github.com/larsks/4022537