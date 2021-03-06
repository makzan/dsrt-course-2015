# Copied/Inspired from Pro Git 2
# https://github.com/progit/progit2/blob/master/Rakefile

namespace :book do
  desc 'prepare build'
  task :prebuild do
    Dir.mkdir 'output' unless Dir.exists? 'output'
    Dir.mkdir 'output/images' unless Dir.exists? 'output/images'
    Dir.mkdir 'images' unless Dir.exists? 'images'
    Dir.glob("book/*/images/*").each do |image|
      FileUtils.copy(image, "images/" + File.basename(image))
    end
    Dir.glob("images/*").each do |image|
      FileUtils.copy(image, "output/images/" + File.basename(image))
    end

    # Stylesheet folder
    Dir.mkdir 'output/stylesheets' unless Dir.exists? 'output/stylesheets'
    Dir.glob("stylesheets/*").each do |cssFile|
      FileUtils.copy(cssFile, "output/stylesheets/" + File.basename(cssFile))
    end

    # Copy anything in public
    Dir.glob("public/*").each do |file|
      FileUtils.copy(file, "output/" + File.basename(file))
    end
  end

  desc 'build basic book formats'
  task :build => :prebuild do
    puts "Converting to HTML..."
    `bundle exec asciidoctor -a stylesheet=stylesheets/web.css -a source-highlighter=highlightjs -D output dsrt-course-2015.adoc`
    puts " -- HTML output at output/dsrt-course-2015.html"

    puts "Converting to EPub..."
    `bundle exec asciidoctor-epub3 -D output dsrt-course-2015.adoc`
    puts " -- Epub output at output/dsrt-course-2015.epub"

    puts "Converting to Mobi (kf8)..."
    `bundle exec asciidoctor-epub3 -a ebook-format=kf8 -D output dsrt-course-2015.adoc`
    puts " -- Mobi output at output/dsrt-course-2015.mobi"

    puts "Converting to PDF... (this one takes a while)"
    `bundle exec asciidoctor-pdf -D output dsrt-course-2015.adoc 2>/dev/null`
    puts " -- PDF  output at output/dsrt-course-2015.pdf"
  end

  desc 'build each chapter'
  task :build_chapter_html => :prebuild do
    puts "Converting chapters to HTML..."
    `bundle exec asciidoctor -D output index.adoc`
    `bundle exec asciidoctor -a stylesheet=stylesheets/web.css -a source-highlighter=highlightjs -a linkcss -D output book/*/*.adoc`
    puts " -- HTML output done in output/"
  end
end

task :default => "book:build"
