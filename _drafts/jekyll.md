- `gem install jekyll` 
- `jekyll new folder_name` to create a new project or use `jekyll new .` to init current dir as jekyll project
- Pygment for syntax highlighting using python http://pygments.org/
- Or Rouge https://github.com/jayferd/rouge (smaller set of languages)
    {% highlight ruby %}
    def foo
      puts 'foo'
    end
    {% endhighlight %}
    - `highlight` method take `ruby` as argument. 
    - See more at http://jekyllrb.com/docs/templates/#code-snippet-highlighting
- `jekyll build` will build a site
- `jekyll serve` will run dev server
- [Config Options](http://jekyllrb.com/docs/configuration/) can be put into `_config.yml` for build configs
- Once you've got the hang of it, simply start writing. 

# Import Wordpress blog to Jekyll
- `gem install jekyll-import`
- Export your wordpress site to xml by using the tool in wp-admin
- Once the xml is in hand use

    $ ruby -rubygems -e 'require "jekyll-import";
      JekyllImport::Importers::WordpressDotCom.run({
        "source" => "wordpress.xml",
        "no_fetch_images" => false,
        "assets_folder" => "assets"
      })'

- All the images will be downloaded and placed in assets
- All the files will come with HTML extension, you may use it to convert them back to markdown later
- Import was pretty quick
    Imported 98 attachments
    Imported 2 pages
    Imported 70 posts
- Build takes quite a long long time. if 
- 